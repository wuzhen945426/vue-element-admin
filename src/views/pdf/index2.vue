<template>
      <el-button @click="print">
        Click to download PDF
      </el-button>
</template>

<script>


import printHtml from "@/utils/print.js"
 
export default {
  methods: {
    print() {
      let printData = `<div>打印内容1111111</div>`
      printHtml(printData)
    }
  },
}


</script>