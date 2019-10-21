## skynet_harbor.* 源码

### define
```c
#define GLOBALNAME_LENGTH 16
#define REMOTE_MAX 256
```

### 变量
```c
static struct skynet_context * REMOTE = 0;
static unsigned int HARBOR = ~0;
```

### 结构体
```c
struct remote_name {
    char name[GLOBALNAME_LENGTH];
    uint32_t handle;
};

struct remote_message {
    struct remote_name destination;
    const void *message;
    size_t sz;
    int type;
};
```

### 函数
```c
void skynet_harbor_send(struct remote_message *rmgs, uint32_t source, int session);
int skynet_harbor_message_isremote(uint32_t handle);
void skynet_harbor_init();
void skynet_harbor_start(void *ctx);
void skynet_harbor_exit();

static inline int invalid_type(int type);
```
