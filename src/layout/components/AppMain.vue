<template>
  <div class="main-app">
      <el-card class="box-card">
        <div slot="header" class="clearfix">
          <span class="titleStyle"> {{mainTitle}}</span>
        </div>
        <div class="PDFStyle">
          <iframe v-if="showPdf" id='previewPdf' :src="'/pdf/web/viewer.html?file=' + fileUrl + '&PDFKey='+ findKey" height="100%" width="100%"></iframe>
          <div v-else class="noResultsStyle">
            <svg-icon icon-class="noResults" class="NSIcon"/>
            <p>还没有选择要处理的文件~</p>
          </div>
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
    },
    PDFData: {
      type: String,
      required: true
    },
    PDFKey: {
      type: String,
      required: true
    }
  },
  data() {
    return {
      mainTitle:'',
      fileUrl: '',
      findKey:'',
      showPdf: false,
      contractVisable: false,
    }
  },
  mounted() {
    this.mainTitle = this.mainDataTitle;
    this.fileUrl = this.PDFData;
    this.findKey = this.PDFKey;
  },
  watch: {
    mainDataTitle: {
      immediate: true,
      handler (val) {
        this.mainTitle = val;
      }
    },
    PDFData: {
      immediate: true,
      handler (val) {
        this.fileUrl = val;
        if (this.fileUrl) {
          this.showPdf = true;
        }
      }
    },
    PDFKey: {
      immediate: true,
      handler (val) {
        this.findKey = val;
      }
    },
  },
  methods:{

  }
}
</script>

<style scoped>
  .main-app{
    background-color:#fff; 
    height: 820px;
  }
  .PDFStyle {
    height: 724px;
    padding: 0px;
    /* overflow-y: auto; */
  }
  .titleStyle{
    color:#057DE4;
  }
  .titleStyle::before {
      content: '`';
      color: rgb(17, 134, 237);
      background: rgb(17, 134, 237);
  }
  .noResultsStyle{
    padding-top: 250px;
    color: rgba(31, 94, 150, 0.591);
    text-align: center;
  }
  .NSIcon.svg-icon {
      width: 10em;
      height: 10em;
  }
</style>
