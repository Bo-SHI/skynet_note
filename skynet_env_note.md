## skynet_env.* 源码

### define
```c
```

### 变量
```c
static struct skynet_env *E = NULL;
```

### 结构体
```c
struct skynet_env {
    struct spinlock lock;
    lua_State *L;
};
```

### 函数
```c
void skynet_env_init();
void skynet_setenv(const char *key, const char *value);
const char* skynet_getenv(const char *key);
```
