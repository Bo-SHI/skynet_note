## skynet_handle.* 源码

### 变量
```c
static struct handle_storage *H = NULL;
```

### 结构体
```c
struct handle_name {
    char *name;
    uint32_t handle;
};

struct handle_storage {
    struct rwlock lock;

    uint32_t harbor;
    uint32_t handle_index;
    int slot_size;
    struct skynet_context **slot;

    int name_cap;
    int name_count;
    struct handle_name *name;
};
```

### 函数
```c
uint32_t skynet_handle_register(struct skynet_context *ctx);
int skynet_handle_retire(uint32_t handle);
void skynet_handle_retireall();
structn skynet_context* skynet_handle_grab(uint32_t handle);
uint32_t skynet_handle_findname(const char *name);
const char* skynet_handle_namehandle(uint32_t handle, const char *name);

void skynet_handle_init(int harbor);

static void _insert_name_before(struct handle_storage *s, char *name, uint32_t handle, int before);
static const char* _insert_name(struct handle_storage *s, const char *name, uint32_t handle);
```
