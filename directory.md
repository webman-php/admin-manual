# 目录结构

```
plugin/admin
├── app
│   ├── controller     // 控制器目录
│   │   ├── IndexController.php   // 主页
│   │   ├── AccountController.php // 账户相关
│   │   ├── AdminController.php   // 管理员管理
│   │   ├── ConfigController.php  // 配置管理
│   │   ├── DevController.php     // 开发辅助
│   │   ├── DictController.php    // 字典管理
│   │   ├── InstallController.php // 安装
│   │   ├── PluginController.php  // 插件管理
│   │   ├── RoleController.php    // 角色管理
│   │   ├── RuleController.php    // 菜单权限管理
│   │   ├── TableController.php   // 数据库管理
│   │   ├── UploadController.php  // 上传管理
│   │   ├── UserController.php    // 会员管理
│   │   ├── Base.php              // 控制器基类
│   │   └── Crud.php              // 增删改查基类
│   ├── model          // Model
│   ├── view           // 视图
│   ├── exception      // 异常控制
│   ├── middleware     // 中间件
│   ├── functions.php  // 函数定义
│   └── common               // 通用类目录
│       ├── Layui.php  // Layui代码生成相关
│       └── Util.php   // 工具类
├── api    // 供其它项目调用的api目录
│   ├── Auth.php       // 权限接口
│   ├── Install.php    // 安装
│   ├── Menu.php       // 菜单接口
│   └── Middleware.php // 鉴权中间件接口
├── config    // 配置目录
├── public    // 静态文件目录
│   ├── admin     // admin目录，放置与页面有关的css js
│   ├── component // 组件目录
│   ├── config    // admin前端配置目录
│   ├── demos     // 一些页面demo
│   ├── resource  // 资源目录
│   └── upload    // 上传目录
└── webman-admin.sql    // 数据库表结构
```

