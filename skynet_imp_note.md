## skynet_imp.* 源码

### define
```c
#define THREAD_WORKER 0
#define THREAD_MAIN 1
#define THREAD_SOCKET 2
#define THREAD_TIMER 3
#define THREAD_MONITOR 4
```

### 变量
```c
```

### 结构体
```c
struct skynet_config {
    int thread;
    int harbor;
    int profile;
    const char *daemon;
    const char *module_path;
    const char *bootstrap;
    const char *logger;
    const char *logservice;
};
```

### 函数
```c
void skynet_start(struct skynet_config *config);
```
