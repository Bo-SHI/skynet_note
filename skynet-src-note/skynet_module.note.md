## skynet_module.* 源码

### define
```c
typedef void *(skynet_dl_create)(void);
typedef int (*skynet_dl_init)(void *inst, struct skynet_context* ctx, const char *param);
typedef void (*skynet_dl_release)(void *inst);
typedef void (*skynet_dl_signal)(void *inst, int signal);
```

### 变量
```c
static struct modules *M = NULL;
```

### 结构体
```c
struct module {
    const char *name;
    void *module;
    skynet_dl_create create;
    skynet_dl_init init;
    skynet_dl_release release;
    skynet_dl_signal signal;
};

struct modules {
    int count;
    struct spinlock lock;
    const char *path;
    struct skynet_module m[MAX_MODULE_TYPE];
};
```

### 函数
```c
struct skynet_module* skynet_module_query(const char *name);
void skynet_module_insert(struct skynet_module *mod);
void* skynet_module_instance_create(struct skynet_module *mod);
int skynet_module_instance_init(struct skynet_module *mod, void *inst, struct skynet_context *ctx, const char *param);
void skynet_module_instance_release(struct skynet_module *mod, void *inst);
void skynet_module_instance_signal(struct skynet_module *mod, void *inst, int signal);
void skynet_module_init(const char *path);

static void* _try_open(struct modules *m, const char *name);
static struct skynet_module* _query(const char *name);
static void* get_api(struct module *mod, const char *api_name);
static int open_sym(struct module* mod);
```
