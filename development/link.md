# 其它系统接入

如果已经有了自己的管理后台，想接入webman-admin，或是想以相对独立的方式接入此系统请参考本章节。

## 原理
1. 通过统一的鉴权中间件来鉴权
2. 设置菜单以iframe引入页面

**下面假设本地有一个admin应用需要接入`webman/admin`系统，其中一个页面url地址为`/admin/user/list`，对应的控制器为`app\admin\controller\User`**

## 统一鉴权
`webman/admin` 提供了一个统一的鉴权中间件，在`config/middleware.php`如下

```
<?php
return [
    // 本地admin应用使用统一的webman/admin管理后台鉴权
    'admin' => [
        plugin\admin\api\Middleware::class
    ]
];
```

更多鉴权相关请参考[鉴权](auth.md)

## 设置菜单
由于鉴权是以菜单为入口，所以需要把控制器`app\admin\controller\User`与菜单绑定。
进入"菜单管理"，将标识字段填写为 `app\admin\controller\User`，url字段填写为`/admin/user/list` 如图
![img_1.png](img_1.png)


**至此，已经将`/admin/user/list`页面及权限接入到了`webman/admin`后台**
