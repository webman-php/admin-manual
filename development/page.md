# 添加页面

如果`webman/admin`的 [一键菜单功能](../base/create-menu.md) 无法满足需要，开发者也可以利用 [admin-vue-src](https://github.com/webman-php/admin-vue-src) 建立新的前端页面，在新页面基础上二次开发。

> **注意**
> 不推荐此方法开发页面，因为一旦`webman/admin`升级，将覆盖修改后的前端编译页面，为此你需要重新编译`admin-vue-src`再发布。推荐以iframe方式接入，参考[其它系统接入](link.md)，iframe方式不仅不影响升级，而且开发者可以使用自己喜欢的技术栈


# 利用admin-vue-src添加页面步骤如下

### 安装nodejs
ubuntu `apt-get install nodejs`  
centos `yum install nodejs`  
mac `brew install nodejs`  
windows 下载地址 https://nodejs.org/en/download/  

### 安装pnpm
```
npm install pnpm
```

### 下载admin-vue-src前端
```
git clone https://github.com/webman-php/admin-vue-src
```

### 安装依赖
```
cd admin-vue-src && pnpm install
```

### 更改配置
如果你的`webman/admin`是运行在本地的在8787端口则忽略此步骤，否则请更改
`admin-vue-src/.env.development` 里 `VITE_PROXY` 的配置，将`http://localhost:8787` 改成正确的值。

### 启动 admin-vue-src
```
pnpm serve
```
命令执行后监听一个端口，一般是`https://localhost:3100/`

### 启动webman-admin
```
php start.php start
```

### 进入页面
进入 `https://localhost:3100/` 并登录

> **提示**
> 页面里发起的请求会被代理到 webman-admin

### 一键生成菜单
创建一个test表，然后利用[一键生成菜单](../base/create-menu.md)生成一个一级菜单(也就是上级菜单留空)，此时系统会生成test表对应的控制器和model文件。

> **提示**
> 这里为了演示方便，生成的是一级菜单

### 复制vue页面
新建目录`admin-vue-src/src/views/test/`
将文件`admin-vue-src/src/views/user/user/index.vue` 复制到 `admin-vue-src/src/views/test/index.vue`
更改`admin-vue-src/src/views/test/index.vue` 里
```
const selectUrl = '/app/admin/user/user/select';
const insertUrl = '/app/admin/user/user/insert';
const updateUrl = '/app/admin/user/user/update';
const deleteUrl = '/app/admin/user/user/delete';
const schemaUrl = '/app/admin/user/user/schema';
```
为
```
const selectUrl = '/app/admin/test/select';
const insertUrl = '/app/admin/test/insert';
const updateUrl = '/app/admin/test/update';
const deleteUrl = '/app/admin/test/delete';
const schemaUrl = '/app/admin/test/schema';
```


### 更改菜单
进入菜单管理页面，将刚生成的菜单的`前端组件`字段改为`/test/index`(也就是`src/views/test/index.vue`去掉`src/views`前缀和`.vue`后缀名)

### 刷新页面
刷新页面后点击刚生成的菜单就进入了新生成的`src/views/test/index.vue`页面，开发者通过更改这个页面及model、控制器就可以增加自己需要的功能特性了。

### 编译发布
在`admin-vue-src`目录执行命令
```
pnpm build
```

将`admin-vue-src/dist/`下的编译文件拷贝到 `{原项目}/plugin/admin/public/ `目录下完成发布。


### 前端文档
webman-admin前端是基于vue-vben-admin开发，文档参考  
https://vvbin.cn/doc-next/guide/introduction.html  
https://vvbin.cn/doc-next/components/introduction.html  


