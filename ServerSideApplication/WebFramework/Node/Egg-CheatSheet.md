[![返回目录](https://parg.co/UCb)](https://github.com/wxyyxc1992/Awesome-CheatSheet)

# Egg 快速入门与实践手册

Eggjs 的[官方文档](https://eggjs.org/zh-cn/)已然深入浅出地介绍了 Eggjs 的用法，以及 [eggjs/examples](https://github.com/eggjs/examples) 中的示例。

# 基础使用

在 [egg-core/egg.js](https://github.com/eggjs/egg-core/blob/master/lib/egg.js) 文件中可以了解到：

```js
class EggCore extends KoaApplication {}
```

Egg.js 也是遵循了约定优于配置的理念，

自动加载与依赖注入的机制带来便利的同时，也削弱了显式依赖声明的可读性，可能会使初学者一头雾水；但是沉心细读，很快就能掌握其使用。

如果我们希望在 VSCode 中调试 Egg.js 应用，那么可以参考 [Node.js CheatSheet]() 中的 VSCode 集成部分，首先安装 [vscode-eggjs](https://github.com/eggjs/vscode-eggjs)，然后为 VSCode 添加如下配置：

```json
// .vscode/launch.json
{
  "version": "0.2.0",
  "configurations": [
    {
      "name": "Launch Egg",
      "type": "node",
      "request": "launch",
      "cwd": "${workspaceRoot}",
      "runtimeExecutable": "npm",
      "windows": { "runtimeExecutable": "npm.cmd" },
      // 启动我们的 egg-bin debug 并默认是 brk
      "runtimeArgs": ["run", "debug", "--", "--inspect-brk"],
      // 日志输出到 Terminal，否则启动期的日志看不到
      "console": "integratedTerminal",
      "protocol": "auto",
      // 进程重启后自动 attach
      "restart": true,
      // 因为无需再 proxy，故改回原来的 9229 端口
      "port": 9229,
      // 自动 attach 子进程
      "autoAttachChildProcesses": true
    }
  ]
}
```

## 配置

## TypeScript

# 内部对象

## Application

譬如数据库实例等全局对象。

```js
// app/extend/application.js
const REDIS_SYMBOL = Symbox('REDIS_SYMBOL');

module.exports = {
  get redis() {
    const options = this.config.redis;

    // 判断是否初始化，若为初始化则创建实例
    if (!this[REDIS_SYMBOL]) {
      this[REDIS_SYMBOL] = new RedisClient(options);
    }

    return this[REDIS_SYMBOL];
  }
};
```

## Context

```js
// app/extend/context.js
module.exports = {
  get redis() {
    return this.app.redis;
  }
};
```

# 请求

## Session 与 Cookie

## 权限校验

## 安全过滤

# 响应

## 响应体设置

更全面的 Node.js 流相关介绍参考 [Node.js CheatSheet](https://parg.co/m56)。

## 静态资源

## 模板渲染

## 国际化

# 服务调用

## 定时服务

# 数据存储

## 数据库连接

[egg-mysql](https://github.com/eggjs/egg-mysql)

```js
knex
  .from('users')
  .leftJoin('user_addresses', 'users.id', '=', 'user_addresses.user_id')
  .options({ nestTables: true })
  .then(results => {
    // do something with results ...
  });

// result 结果如下
{
  users: {
    id: 3,
    username: 'somename',
    email:
  },
  user_addresses: {
    id: 1, // or whatever format your id is in
    user_id: 3,
    street: 'somestreet',
    postcode: 'somepostcode'
  }
}
```

## Sequelize ORM

# 开发实践

## 异常处理

## 测试

## 中间件

# 线上部署
