<template>
  <div class="main-app">
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span class="titleStyle"> {{mainTitle}}</span>
        </div>
        <div class="text item el-card__body">
          <input type="file" name="myfile" id="myfile" @change="preview($event)"/>
          <!--<button @click="changeLocal">点击预览本地pdf</button>-->
          <iframe v-if="showPdf" id='previewPdf' :src="'/static/pdf/web/viewer.html?file=' + fileUrl" height="560" width="100%"></iframe>
          <!-- <img src="@/assets/img/PDF.png" class="imagePdf" alt=""> -->
          <!--服务器-->
          <button @click="checkNormal">查看有效</button>
        </div>
      </el-card>
    </div>
</template>

<script>
export default {
  name: 'AppMain',
  props: {
    mainDataTitle: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      mainTitle:'',
      fileUrl: '',
      showPdf: false,
      contractVisable: false,
    }
  },
  mounted() {
    this.mainTitle = this.mainDataTitle;
  },
  watch: {
    mainDataTitle: {
      immediate: true,
      handler (val) {
        this.mainTitle = val
      }
    }
  },
  methods:{
    checkNormal() {
        let url = 'http://image.cache.timepack.cn/nodejs.pdf'  // 有效 服务器配置跨域处理
        window.open('/static/pdf/web/viewer.html?file=' + url)
    },
    // 这是打开本地文件进行预览
    preview(event) {
        let files = document.getElementById('myfile').files[0]
        if (files.type !== 'application/pdf') {
            alert('只能上传一份pdf文件哦～')
            return
        }
        this.showPdf = true
        this.fileUrl = this.getObjectURL(files)

    },
    getObjectURL(file) {
      console.log('file:',file)
        let url = null;
        if (window.createObjectURL != undefined) { // basic
            url = window.createObjectURL(file);
        } else if (window.webkitURL != undefined) { // webkit or chrome
            url = window.webkitURL.createObjectURL(file);
        } else if (window.URL != undefined) { // mozilla(firefox)
            url = window.URL.createObjectURL(file);
        }
        return url;
    },
  }
}
</script>

<style scoped>
  .main-app{
    background-color:#fff; 
    height: 820px;
  }
  .el-card__body {
    height: 725px;
    overflow-y: auto;
  }
  .imagePdf{
    height: 585px; 
    width: 100%;
  }
  .titleStyle{
    color:#057DE4;
  }
  .titleStyle::before {
      content: '`';
      color: rgb(17, 134, 237);
      background: rgb(17, 134, 237);
  }
</style>
