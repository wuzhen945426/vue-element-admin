# vue-element-admin
根据开源vue-admin项目学习整体框架设计并改编成为一个自己的后台管理项目
```
1、发布及表格接收模块
   封装的是Tinymce富文本编辑器，点击发布后用form来接受到页面所有的信息
   （由于无后端，所以不能存储form数据并且供表格页面去掉接口，并且深浅拷贝当数据源为空数据也会消失，最终采用了localstorage来暂存数据）
   整个项目采用momentjs来处理时间格式，细节之处在于富文本编辑完成后转化为代码再有v-html来显示在列表里，这就意味着可以在富文本编辑的格式样式可以在表格里排版正确。
   
2、table
   重新封装了一下分页组件，在el-table里面，js做了一个根据名称来搜索的小功能，目前最常用的就是搜索了
   
3、带截图的表格
   找了一个表格demo来写截图逻辑：此逻辑依靠html2canvas强行把某区域（可根据class）转化为图片并下载下来，目前做到ie兼容

4、局部刷新方法例子
    点击切换字体大小步骤：
      1、赋值给全局字体大小$ELEMENT.size
      2、提交更新store里的setSize（this.$store.dispatch('app/setSize', size)
      3、取当前路由路径并重定向实现刷新

5、图表界面使用了echarts
    封装了几个简单echarts图 注意点:
     1、类似echarts这种需要拿到demo才开始工作的插件来说，在初始化时要在mounted生命周期进行初始化 
     2、随数据改变时实时更新可以在watch进行监听，有变化就重新setOption（deep深度监听） 
     3、有的时候组件放在el-table或者el-dialog里面时，发现宽度显示有问题，来监听改变的动作，然后手动调用echarts的resize()方法；如果是 el-dialog之中放图表就比较简单了，只要在 dialog 出现之后再 init 图表就可以了
 
 6、PDF
    1、window.print()利用浏览器自带的打印功能实现打印或者是转为PDF下载  index.vue里按原框架意思可将打印的代码放入content通过v-html指令转化并打印
    2、自定义封装一个print()组件，可直接引用使用  index2.vue是例子
    3、此方法需要设置浏览器打印的设置勾选背景图形，所以这里要注意如果是给用户使用的话让每个用户勾选不太方便 在以下的代码可给想要打印的最外层设置css，例如boby
     boby {
           -webkit-print-color-adjust:exact;
           -moz-print-color-adjust:exact;
           -ms-print-color-adjust:exact;
           print-color-adjust:exact;
          }
 7、登录
    1、点击登录触发this.$store.dispatch('user/login', this.loginForm)
    2、登录成功后，服务端会返回一个 token（该token的是一个能唯一标示用户身份的一个key），之后我们将token存储在本地cookie之中，这样下次打开页面或者刷新页面的时候能记住用户的登录状态，不用再去登录页面重新登录了。
    3、permission.js会验证是否存在token并且开始获取用户信息getInfo，token不存在则进入白名单逻辑
    
    
```
## Features

```
- Login / Logout

- Permission Authentication
  - Page permission
  - Directive permission
  - Permission configuration page
  - Two-step login

- Multi-environment build
  - Develop (dev)
  - sit
  - Stage Test (stage)
  - Production (prod)

- Global Features
  - I18n
  - Multiple dynamic themes
  - Dynamic sidebar (supports multi-level routing)
  - Dynamic breadcrumb
  - Tags-view (Tab page Support right-click operation)
  - Svg Sprite
  - Mock data
  - Screenfull
  - Responsive Sidebar

- Editor
  - Rich Text Editor
  - Markdown Editor
  - JSON Editor

- Excel
  - Export Excel
  - Upload Excel
  - Visualization Excel
  - Export zip

- Table
  - Dynamic Table
  - Drag And Drop Table
  - Inline Edit Table

- Error Page
  - 401
  - 404

- Components
  - Avatar Upload
  - Back To Top
  - Drag Dialog
  - Drag Select
  - Drag Kanban
  - Drag List
  - SplitPane
  - Dropzone
  - Sticky
  - CountTo

- Advanced Example
- Error Log
- Dashboard
- Guide Page
- ECharts
- Clipboard
- Markdown to html
```

## Getting started

```bash
# clone the project
https://github.com/wuzhen945426/vue-element-admin.git

# enter the project directory
cd vue-element-admin

# install dependency
npm install

# develop
npm run dev
```

This will automatically open http://localhost:9527

## Build

```bash
# build for test environment
npm run build:stage

# build for production environment
npm run build:prod
```

## Advanced

```bash
# preview the release environment effect
npm run preview

# preview the release environment effect + static resource analysis
npm run preview -- --report

# code format check
npm run lint

# code format check and auto fix
npm run lint -- --fix
```

