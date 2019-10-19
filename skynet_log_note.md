## skynet_log.* 源码

### define
```c
```

### 变量
```c
```

### 结构体
```c
```

### 函数
```c
FILE* skynet_log_open(struct skynet_context *ctx, uint32_t handle);
void skynet_log_close(struct skynet_context *ctx, FILE *f, uint32_t handle);
void skynet_log_output(FILE *f, uint32_t source, int type, int session, void *buffer, size_t sz);

static void log_blob(FILE *f, void *buffer, size_t sz);
static void log_socket(FILE *f, struct skynet_socket_message *msg, size_t sz);
```
