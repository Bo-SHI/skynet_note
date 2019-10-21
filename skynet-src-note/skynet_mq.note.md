## skynet_mq.*源码

### 与定义
```c
typedef void (*message_drop) (struct skynet_message*, void*);
```

### 变量
```c
static struct global_queue *Q = NULL;
```

### 结构体
```c
struct skynet_message {
    uint32_t source;
    int session;
    void *data;
    size_t sz;
};

struct message_queue {
    struct spinlock lock;
    uint32_t handle;
    int cap;
    int head;
    int tail;
    int release;
    int in_global;
    int overload;
    int overload_threshhold;
    struct skynet_message *queue;
    struct message_queue *next;
};

struct global_queue {
    struct message_queue *head;
    struct message_queue *tail;
    struct spinlock lock;
};

```

### 函数
```c
void skynet_globalmq_push(struct message_queue *queue);
struct message_queue* skynet_globalmq_pop();
struct message_queue* skynet_mq_create(uint32_t handle);
uint32_t skynet_mq_handle(struct message_queue *q);
int skynet_mq_length(struct message_queue *q);
int skynet_mq_overload(struct message_queue *q);
int skynet_mq_pop(struct message_queue *q, struct skynet_message *message);
void skynet_mq_push(struct message_queue *q, struct skynet_message *message);
void skynet_mq_mark_release(struct message_queue *q);
void skynet_mq_release(struct message_queue *q, message_drop drop_func, void *ud);

void skynet_mq_init();

static void _release(struct message_queue *q);
static void expand_size(struct message_queue *q);
static void _drop_queue(struct message_queue *q, message_drop drop_func, void *ud);
```
