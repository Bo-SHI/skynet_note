## skynet_timer.* 源码

### define
```c
typedef void (*timer_execute_func)(void *ud, void *arg);

#define TIMER_NEAR_SHIFT 8
#define TIMER_NEAR (1 << TIMER_NEAR_SHIFT)
#define TIMER_LEVEL_SHIFT 6
#define TIMER_LEVEL (1 << TIMER_LEVEL_SHIFT)
#define TIMER_NEAR_MASK (TIMER_NEAR - 1)
#define TIMER_LEVEL_MASK (TIMER_LEVEL - 1)
```

### 变量
```c
static struct timer *TI = NULL;
```

### 结构体
```c
struct timer_event {
    uint32_t handle;
    int session;
};

struct timer_node {
    struct timer_node *next;
    uint32_t expire;
};

struct link_list {
    struct timer_node head;
    struct timer_node *tail;
};

struct timer {
    struct link_list near[TIMER_NEAR];
    struct link_list t[4][TIMER_LEVEL];
    struct spinlock lock;
    uint32_t time;
    uint32_t starttime;
    uint64_t current;
    uint64_t current_point;
};
```

### 函数
```c
int skynet_timeout(uint32_t handle, int time, int session);
void skynet_updatetime(void);
uint32_t skynet_starttime(void);
uint64_t skynet_now();
void skynet_timer_init();
uint64_t skynet_thread_time();

static inline struct timer_node* link_clear(struct link_list *list, struct timer_node *node);
static inline void link(struct link_list *list, struct timer_node *node);
static void add_node(struct timer *T, struct timer_node *node);
static void timer_add(struct timer *T, void *arg, size_t sz, int time);
static void move_list(struct timer *T, int level, int idx);
static void timer_shift(struct timer *T);
static inline void dispatch_list(struct timer_node *current);
static inline void timer_execute(struct timer *T);
static void timer_update(struct timer *T);
static struct timer* timer_create_timer();

static void systime(uint32_t *sec, uint32_t *cs);
static uint64_t gettime();
```
