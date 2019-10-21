## skynet_monitor.* 源码

### define
```c
```

### 变量
```c
```

### 结构体
```c
struct skynet_monitor {
    int version;
    int check_version;
    uint32_t source;
    uint32_t destination;
};
```

### 函数
```c
struct skynet_monitor* skynet_monitor_new();
void skynet_monitor_delete(struct skynet_monitor *sm);
void skynet_monitor_trigger(struct skynet_monitor *sm, uint32_t source, uint32_t destination);
void skynet_monitor_check(struct skynet_monitor *sm);
```
