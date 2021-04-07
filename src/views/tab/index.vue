<template>
  <div class="tab-container">
    <el-button @click="printOut">截图</el-button>
    <el-tag>mounted times ：{{ createdTimes }}</el-tag>
    <el-alert :closable="false" style="width:200px;display:inline-block;vertical-align: middle;margin-left:30px;" title="Tab with keep-alive" type="success" />
    <el-tabs v-model="activeName" style="margin-top:15px;" type="border-card" class="jietu">
      <el-tab-pane v-for="item in tabMapOptions" :key="item.key" :label="item.label" :name="item.key">
        <keep-alive>
          <tab-pane v-if="activeName==item.key" :type="item.key" @create="showCreatedTimes" />
        </keep-alive>
      </el-tab-pane>
    </el-tabs>
  </div>
</template>

<script>
import TabPane from './components/TabPane'
import $ from 'jquery'
import html2canvas from 'html2canvas'

export default {
  name: 'Tab',
  components: { TabPane },
  data() {
    return {
      tabMapOptions: [
        { label: 'China', key: 'CN' },
        { label: 'USA', key: 'US' },
        { label: 'Japan', key: 'JP' },
        { label: 'Eurozone', key: 'EU' }
      ],
      activeName: 'CN',
      createdTimes: 0
    }
  },
  watch: {
    activeName(val) {
      this.$router.push(`${this.$route.path}?tab=${val}`)
    }
  },
  created() {
    // init the default selected tab
    const tab = this.$route.query.tab
    if (tab) {
      this.activeName = tab
    }
  },
  methods: {
    showCreatedTimes() {
      this.createdTimes = this.createdTimes + 1
    },
      dataURLToBlob(dataurl) {
      //ie 图片转格式
      var arr = dataurl.split(","),
        mime = arr[0].match(/:(.*?);/)[1],
        bstr = atob(arr[1]),
        n = bstr.length,
        u8arr = new Uint8Array(n);
      while (n--) {
        u8arr[n] = bstr.charCodeAt(n);
      }
      return new Blob([u8arr], { type: mime });
    },
    downloadResult(name) {
      // let canvasID = document.body;
      console.log(document.getElementsByClassName("jietu"));
      let canvasID = document.getElementsByClassName("el-tabs__content")[0];
      let a = document.createElement("a");
      html2canvas(canvasID).then((canvas) => {
        let dom = document.body.appendChild(canvas);
        dom.style.display = "none";
        a.style.display = "none";
        document.body.removeChild(dom);
        let blob = this.dataURLToBlob(dom.toDataURL("image/png"));
        //兼容ie，ie会进入if
        if (window.navigator.msSaveOrOpenBlob) {
          navigator.msSaveOrOpenBlob(blob, name + ".png");
        } else {
          a.setAttribute("href", URL.createObjectURL(blob));
          a.setAttribute("download", name + ".png");
          document.body.appendChild(a);
          a.click();
          URL.revokeObjectURL(blob);
          document.body.removeChild(a);
        }
      });
    },
    printOut(name) {
      // 个人观察只是截取可见范围以及以下的区域，所以先将滚动条置顶
      $(window).scrollTop(0); // jQuery 的方法
      document.body.scrollTop = 0; // IE的
      document.documentElement.scrollTop = 0; // 其他
      this.downloadResult(name);
    },
  }
}
</script>

<style scoped>
  .tab-container {
    margin: 30px;
  }
</style>
