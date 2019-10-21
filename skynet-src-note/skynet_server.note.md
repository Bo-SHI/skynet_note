## skynet_server.* 源码

### 变量
```c
static skynet_node G_NODE;
```

### 结构体

__skynet_context:__
```c
struct skynet_context {
    void *instance;
    skynet_module *mod;
    void *cb_ud;
    skynet_cb cb;
    struct message_queue *queue;
    FILE *logfile;
    uint64_t cpu_cost; // in microsec 微秒
    uint64_t cpu_strat; // in microsec
    char result[32];
    uint32_t handle;
    int session_id;
    int ref;
    int message_count;
    bool init;
    bool endless;
    bool profile;
};
```

__skynet_node:__
```c
struct skynet_node {
    int total;
    int init;
    uint32_t monitor_exit;
    pthread_key_t handle_key;
    bool profile; // default off
};
```

__drop_t:__
```c
struct drop_t {
    uint32_t handle;
};
```

### 函数
```c
int skynet_context_total();
uint32_t skynet_current_handle(void);

struct skynet_context* skynet_new_context(const char *name, const char *param);
int skynet_context_newsession(struct skynet_context *ctx);
void skynet_context_grab(struct skynet_context* ctx);
void skynet_context_reserve(struct skynet_context* ctx);
struct skynet_context* skynet_context_release(struct skynet_context* ctx);
int skynet_context_push(uint32_t handle, struct skynet_message *message);
void skynet_context_endless(uint32_t handle);
void skynet_context_dispatchall(struct skynet_context *ctx);
int skynet_isremote(struct skynet_context *ctx, uint32_t handle, int *harbor);
struct message_queue* skynet_context_message_dispatch(struct skynet_monitor *sm, struct message_queue *q, int weight);
uint32_t skynet_queryname(struct skynet_context *ctx, const char *name);
int skynet_send(struct skynet_context *ctx, uint32_t source, uint32_t destination, int type, int session, void *data, size_t sz);
int skynet_sendname(struct skynet_context *ctx, uint32_t source, const char *addr, int type, int session, void *data, size_t sz);
uint32_t skynet_context_handle(struct skynet_context *ctx);
void skynet_callback(struct skynet_context *ctx, void *ud, skynet_cb cb);
void skynet_context_send(struct skynet_context *ctx, void *msg, size_t sz, uint32_t source, int type, int session);

static void context_inc();
static void context_dec();
static void id_to_hex(char *str, uint32_t id);
static void drop_message(struct skynet_message *msg, void *ud);
static void delete_context(struct skynet_context* ctx);
static void copy_name(char name[GLOBALNAME_LENGTH], const char *addr);
static void _filter_args(struct skynet_context *ctx, int type, int *session, void **data, size_t *sz);
```

### cmd
```c
static void handle_exit(struct skynet_context *ctx, uint32_t handle);
static uint32_t tohandle(struct skynet_context *ctx, const char *param);

struct command_func {
    const char *name;
    const char *(*func) (struct skynet_context* ctx, const char *param);
};

static const char* cmd_timeout(struct skynet_context *ctx, const char *param);
static const char* cmd_reg(struct skynet_context *ctx, const char *param);
static const char* cmd_query(struct skynet_context *ctx, const char *param);
static const char* cmd_name(struct skynet_context *ctx, const char *param);
static const char* cmd_exit(struct skynet_context *ctx, const char *param);
static const char* cmd_kill(struct skynet_context *ctx, const char *param);
static const char* cmd_launch(struct skynet_context *ctx, const char *param);
static const char* cmd_setenv(struct skynet_context* ctx, const char *param);
static const char* cmd_getenv(struct skynet_context* ctx, const char *param);
static const char* cmd_starttime(struct skynet_context* ctx, const char *param);
static const char* cmd_abort(struct skynet_context* ctx, const char *param);
static const char* cmd_monitor(struct skynet_context* ctx, const char *param);
static const char* cmd_stat(struct skynet_context* ctx, const char *param);
static const char* cmd_logon(struct skynet_context* ctx, const char *param);
static const char* cmd_logoff(struct skynet_context* ctx, const char *param);
static const char* cmd_signal(struct skynet_context* ctx, const char *param);

static struct command_func cmd_funcs[] = {
    {"TIMEOUT", cmd_timeout},
    {"REG", cmd_reg},
    {"QUERY", cmd_query},
    {"NAME", cmd_name},
    {"EXIT", cmd_exit},
    {"KILL", cmd_kill},
    {"LAUCH", cmd_lauch},
    {"SETENV", cmd_setenv},
    {"GETENV", cmd_getenv},
    {"STARTTIME", cmd_starttime},
    {"ABORT", cmd_abort},
    {"MONITOR", cmd_monitor},
    {"STAT", cmd_stat},
    {"LOGON", cmd_logon},
    {"LOGOFF", cmd_logoff},
    {"SIGNAL", cmd_signal},
    {NULL, NULL}
};

const char* skynet_command(struct skynet_context *ctx, const char *cmd, const char *param);
```

### global
```c
void skynet_globalinit(void);
void skynet_globalexit(void);
void skynet_initthread(int m);
void skynet_profile_enable(bool enable);
```
