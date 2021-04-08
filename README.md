# vue-element-admin
根据开源vue-admin项目学习整体框架设计并改编成为一个自己的后台管理项目

1、发布及表格接收模块
   封装的是Tinymce富文本编辑器，点击发布后用form来接受到页面所有的信息，（由于无后端，所以不能存储form数据并且供表格页面去掉接口，并且深浅拷贝当数据源为空数据也会消失，最终采用了localstorage来暂存数据）。整个项目采用momentjs来处理时间格式。细节之处在于富文本编辑完成后转化为代码再有v-html来显示在列表里，这就意味着可以在富文本编辑的格式样式可以在表格里排版正确。
<p align="center">
  <img  src="https://i.loli.net/2021/04/08/RcklInG1JH2Epva.png">
   <img src="https://i.loli.net/2021/04/08/lgTKcD7WVXuy9sm.png">
</p>


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
git clone https://github.com/PanJiaChen/vue-element-admin.git

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

