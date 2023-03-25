# 通用接口

webman-admin在`plugin/admin/api`目录提供了一些通用接口供第三方调用。

## Auth 权限接口
```php
<?php
namespace plugin\admin\api;

use plugin\admin\app\model\Role;
use plugin\admin\app\model\Rule;
use support\exception\BusinessException;
use function admin;

/**
 * 对外提供的鉴权接口
 */
class Auth
{
    /**
     * 判断是否有权限访问某个控制器和方法，无权限时抛出异常
     * @param string $controller
     * @param string $action
     * @return void
     * @throws \ReflectionException|BusinessException
     */
    public static function access(string $controller, string $action)
    {}

    /**
     * 判断是否有权限访问某个控制器和方法，有权限返回true，无权限返回false
     * @param string $controller
     * @param string $action
     * @param int $code
     * @param string $msg
     * @return bool
     * @throws \ReflectionException|BusinessException
     */
    public static function canAccess(string $controller, string $action, int &$code = 0, string &$msg = ''): bool
    {}
    
}
```

## Menu 菜单接口
```php
class Menu
{

    /**
     * 根据key获取菜单
     * @param $key
     * @return array
     */
    public static function get($key)
    {}

    /**
     * 根据id获得菜单
     * @param $id
     * @return array
     */
    public static function find($id): array
    {}

    /**
     * 添加菜单
     * @param array $menu
     * @return int
     */
    public static function add(array $menu)
    {}

    /**
     * 导入菜单
     * @param array $menu_tree
     * @return void
     */
    public static function import(array $menu_tree)
    {}

    /**
     * 按照key删除菜单
     * @param $key
     * @return void
     */
    public static function delete($key)
    {}

}
```

> **提示**
> 一般来说应用插件无需手动调用Menu菜单接口，开发者只需要准备好[menu.php菜单配置](../app-development/menu.md)，通过webman-admin安装插件时会自动导入菜单。

## Middleware 中间件
为了让其它系统能够[接入webman-admin的权限体系](link.md)，webman-admin提供了一个鉴权中间件，实现如下

```php
<?php
namespace plugin\admin\api;

use Webman\Http\Request;
use Webman\Http\Response;
use Webman\MiddlewareInterface;
use support\exception\BusinessException;

/**
 * 对外提供的鉴权中间件
 */
class Middleware implements MiddlewareInterface
{
    /**
     * 鉴权
     * @param Request $request
     * @param callable $handler
     * @return Response
     * @throws \ReflectionException
     * @throws BusinessException
     */
    public function process(Request $request, callable $handler): Response
    {
        $controller = $request->controller;
        $action = $request->action;

        $code = 0;
        $msg = '';
        if (!Auth::canAccess($controller, $action, $code, $msg)) {
            if ($request->expectsJson()) {
                $response = json(['code' => $code, 'msg' => $msg, 'type' => 'error']);
            } else {
                $response = \response($msg, 401);
            }
        } else {
            $response = $request->method() == 'OPTIONS' ? response('') : $handler($request);
        }
        return $response;
    }

}
```

> **提示**
> 如果此中间件无法满足开发者需求，开发者可以在自己的项目中实现自己的鉴权中间件，不一定强制用此鉴权中间件

## 快捷函数
webman-admin提供了几个快捷函数，说明如下
```php
<?php

/**
 * 获取当前管理员id
 * @return integer|null
 */
function admin_id(): ?int
{}

/**
 * 获取当前管理员
 * @param null|array|string $fields
 * @return array|mixed|null
 */
function admin($fields = null)
{}

/**
 * 当前是否是超级管理员
 * @return bool
 */
function is_supper_admin(): bool
{}

/**
 * 获取当前管理员权限
 * @return array
 */
function admin_rules(): array
{}
```
