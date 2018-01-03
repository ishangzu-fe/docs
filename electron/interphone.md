# 系统间通讯 - Interphone

## 介绍

主要用于客户端程序（Electron App）与子系统间（webview）之间的通讯 - 基于 Node.EventEmitter。
Interphone 将同步消息（Message）以及异步动作（Action）作为消息的载体在系统间相互传递。

---

## Message

Message 的同步，并不代表“触发”的同步，而是“触发”的“动作”应该是同步的。代码上，消息事件的处理函数体应该是同步的，例如：

```JavaScript
this.$phone.on('system-message', (message) => {
    // Do something sync
});
```

其他系统发送来的消息，被命名为 “本系统名-message”，所以监听它就可以了。

发送消息无需定义，可以直接通过 send 发放来发送，主要有两种方式：
1. 通过 URL
2. 通过 Message 对象

#### 通过 URL
```JavaScript
// 告诉客户端需要打开本系统
this.$phone.send('system://page-route?action=show&others=1');
```

#### 通过 URL
```JavaScript
// 告诉客户端需要打开本系统
this.$phone.send({
    target: 'system'
    // 或者直接指定消息名
    name: 'messageName',
    // others
});
```

---

## Action

同样的，Action 的异步代表着处理函数可以是异步的，例如：

```JavaScript
this.$phone.define('actionName', (params, next[, interphone]) => {
    // Do something async
    // 不要忘记调用 next 方法
    next();
});
```

Action 等同于 Vuex 中的 Action，触发的方式也很像：

```JavaScript
this.$phone.dispatch('actionName', {
    // Params
    // 触发指定系统的动作
    system: ''
})
```

---

## API