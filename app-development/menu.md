# 菜单
在安装插件时，webman-admin会自动导入`plugin/插件/config/menu.php`配置里的菜单，卸载插件时也会根据此配置删除菜单。

menu.php 内容类似如下
```php
<?php

use plugin\queue\app\controller\redis\DelayController;
use plugin\queue\app\controller\redis\FailedController;
use plugin\queue\app\controller\redis\NormalController;

return [
    [
        'title' => '消息队列',
        'key' => 'queue',
        'icon' => 'layui-icon-align-left',
        'weight' => 0,
        'type' => 0,
        'children' => [
            [
                'title' => '正常队列',
                'key' => NormalController::class,
                'href' => '/app/queue/redis/normal',
                'type' => 1,
                'weight' => 0,
            ],
            [
                'title' => '延迟队列',
                'key' => DelayController::class,
                'href' => '/app/queue/redis/delay',
                'type' => 1,
                'weight' => 0,
            ],
            [
                'title' => '失败队列',
                'key' => FailedController::class,
                'href' => '/app/queue/redis/failed',
                'type' => 1,
                'weight' => 0,
            ]
        ]
    ]
];
```

### 字段说明
各字段说明如下

#### title
菜单名称

#### type
类型，0为目录，1为菜单，2为权限节点(权限节点会自动生成，一般不用配置)

#### key
菜单标识，要求全局唯一。
* 一级目录要求格式为`插件名`
* 二级及以上目录要求格式为`插件名-任意字符串`
* 如果是菜单，则填写控制器类的名称(带命名空间)

#### href
url路径，一般填写控制器对应的url路径

#### icon
显示图标，只有一级目录或者顶级菜单才会显示图标。目前只支持layui图标，可选值参考[layui图标](https://layui.gitee.io/v2/docs/element/icon.html)

#### weight
权重，用来排序，值大的在前，值小的在后

## 测试安装
如果你的应用插件是使用 `php webman app-plugin:create` 命令生成的，则会生成一个`plugin/插件名/api/Install.php`类，类里面install方法用于安装菜单，uninstall方法用于卸载菜单。我们可以通过以下命令来测试install以及uninstall方法。

**安装菜单**
`php webman app-plugin:install 插件名`

**卸载菜单**
`php webman app-plugin:uninstall 插件名`

> **提示**
> 如果你的应用插件需要在安装或者卸载时触发某个操作，可以写在`Install`类里的`install`或`uninstall`方法中



