# vue-panel

> vue-panel

## Build Setup

```bash
# install dependencies
npm install

# serve with hot reload at localhost:8080
npm run dev

# build for production with minification
npm run build

# build for qa with minification
npm run qa

# build for production and view the bundle analyzer report
npm run build --report

# run unit tests
npm run unit

# run e2e tests
npm run e2e

# run all tests
npm test

# 生成组件文档（src/components/docs.md）
# 读取src/components文件夹下的所有.vue$文件，并读取里面文件的docs块，生成文档文件
npm run docs
```

## 说明

> 项目是由 vue-cli 创建，并再次基础上做了一些修改。

1. `main.js` 由框架根据 `extend/main.js` 自动生成
1. 引入插件机制，在`src`目录下创建已下四种文件夹：`minixs`、`filters`、`directives`、`plugins`并在文件夹下创建以`g_`开头的文件，就会被自动引入到全局。

    > 以上四个目录对应 vue 的四种插件机制，编写参考[vue插件](https://cn.vuejs.org/v2/guide/plugins.html)（这个待定，后期有好的方案可能会变化）
1. 引入中间件机制， 在路由进行切换之前会按照根目录的`med.config.js`文件中的`middlewares`字段设定的顺序依次执行，然后再运行`src/middlewares`中的其他中间件，当所有的都运行完毕后才会进入路由。

1. 自动菜单功能，根据路由的配置，和当前登录用户的权限自动生成菜单，所以菜单就需要一些编写规范，后面单独列出

1. 一键生成文档功能

1. vuex 模块自动导入功能

## 编写规范

1. 自动菜单：

    * 添加的路由一律写在 `src/router/dynamic.js`文件夹下的`dynamicRouteMap`数组中，不能写在`src/router/index.js`
    * 菜单的功能主要是根据`meta`字段确定，可选属性如下:
      * `[permission] {array}`：哪些权限能进入该菜单
      * `[menu] {boolean}`：是否生成菜单，默认 true
      * `[avtiveMenu] {string}`：当 menu===false 时，进入到路由时，菜单上没有对应的菜单项，此时就没有了选中项，指定该参数能将选中项指定到其他菜单上

2. 文档生成功能

    * `src/components`文件用于存放组件，每个单文件组件都有一个可选自定义块`docs`，可以编写 markdown 格式对该文件进行功能和用法进行说明。推荐为每一个组件写上文档。
    * 根目录运行如下命令，会在`src/components`文件夹下生成`docs.md`文件
      > npm run docs

3. vuex 模块自动导入功能

    * 新建一个 vuex 模块，只需要在`src/store`目录下创建一个文件，然后按照 vuex 语法编写导出一个 store 配置对象。

4. 推荐将常量单独写在`src/constant`目录下，然后导入使用，后期如果发生变更只需要更改这一处即可，不需要全项目查找

5. 所有的接口调用都写在`src/api`下，并且按照功能分开，统一管理。
