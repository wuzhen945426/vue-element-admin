# vue-element-admin
根据开源vue-admin项目学习整体框架设计并改编成为一个自己的后台管理项目

1、发布及表格接收模块
   封装的是Tinymce富文本编辑器，点击发布后用form来接受到页面所有的信息，（由于无后端，所以不能存储form数据并且供表格页面去掉接口，并且深浅拷贝当数据源为空数据也会消失，最终采用了localstorage来暂存数据）。整个项目采用momentjs来处理时间格式。细节之处在于富文本编辑完成后转化为代码再有v-html来显示在列表里，这就意味着可以在富文本编辑的格式样式可以在表格里排版正确。
<p align="center">
  <img width="320" src="https://i.loli.net/2021/04/08/RcklInG1JH2Epva.png">
   <img width="320" src="https://i.loli.net/2021/04/08/lgTKcD7WVXuy9sm.png">
</p>
