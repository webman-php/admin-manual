# 目录结构

```
admin/
├── app
│   ├── controller   
│   │   ├── auth                // 菜单、角色等权限相关控制器
│   │   ├── common              // 登录、安装、账户设置等控制器
│   │   ├── database            // 数据库管理相关控制器
│   │   ├── plugin              // 插件相关控制器
│   │   ├── user                // 用户相关控制器
│   │   ├── Base.php            // 控制器基类
│   │   ├── Crud.php            // 控制器增删改查公共
│   │   └── IndexController.php // admin主页
│   ├── exception     // 异常类
│   ├── middleware    // 中间件
│   ├── model         // Model
│   ├── view          // 视图
│   ├── functions.php // 一些公共函数
│   └── Util.php      // 一些公用工具方法
├── public                    // 静态文件目录     
│   ├── _app.config.js  // 前端公共配置
│   ├── assets          // 图片等资源
│   ├── resource        // js css 等资源
│   ├── upload          // 上传目录
│   ├── avatar.png      // 默认头像
│   ├── favicon.ico     // ico图标
│   └── index.html      // index.html
├── api                // api目录是对外提供的接口
│   ├── Auth.php       // 权限接口，供其它应用插件调用
│   ├── Menu.php       // 菜单相关接口，供其它应用插件调用
│   ├── Middleware.php // 鉴权中间件，供其它应用插件接入admin权限时使用
│   └── Install.php    // 安装脚本，升级时使用
├── config // 配置目录
└── webman-admin.sql // 安装时用的sql文件
```

