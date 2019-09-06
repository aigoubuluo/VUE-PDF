<template>
  <div class="app-wrapper">
    <!-- 头 star-->
    <navbar />
    <!-- 头 end-->

    <!-- 主体部分 -->
    <div class="mainPartStyle">
      <el-row>
        <!-- 左侧菜单 star -->
        <el-col :span="leftSpan">
          <left-sidebar :leftSidebarData="leftSidebarData"  :leftSidebarSearchValue="leftSidebarSearchValue" :leftMenuState="leftMenuState" @mainPDFData="mainTitleBtn" />
        </el-col>
        <!-- 左侧菜单 end -->

        <!-- 左侧折叠按钮 star -->
        <PackUpLeftBtn :leftStateData="leftStateData" :mainSpanData="mainSpan" @leftFoldingFunc="leftFoldingFunc"/>
        <!-- 左侧折叠按钮 end -->

        <!-- 中间显示区域 star -->
        <el-col :span="mainSpan">
          <AppMain  :mainDataTitle="mainTitle" :PDFData="PDFData" :PDFKey="PDFKey" />
        </el-col>
        <!-- 中间显示区域 end -->

        <!-- 右侧折叠按钮 star -->
        <PackUprightBtn :rightStateData="rightStateData" :mainSpanData="mainSpan" @rightFoldingFunc="rightFoldingFunc"/>
        <!-- 右侧折叠按钮 end -->

        <!-- 右侧菜单 star -->
        <el-col :span="rightSpan">
          <right-sidebar :rightSidebarData="rightSidebarData" @rightChangeHandler="changeHandlerBtn" />
        </el-col>
        <!-- 右侧菜单 end -->

      </el-row>
    </div>

  </div>
</template>

<script>
import { Navbar, leftSidebar, rightSidebar,  AppMain, PackUpLeftBtn, PackUprightBtn } from './components'
import ResizeMixin from './mixin/ResizeHandler'

export default {
  name: 'Layout',
  components: { Navbar, leftSidebar, rightSidebar, AppMain, PackUpLeftBtn, PackUprightBtn },
  mixins: [ResizeMixin],
  data() {
    return {

      /**
       * 封装左侧菜单栏参数 开始
       * leftSidebarData:菜单树数据 Object；
       * leftSidebarSearchValue:搜索参数 String；
       * leftMenuState: 控制菜单内容显隐 Boolean 默认状态：false；
       * leftStateData: 控制菜单折叠按钮 Boolean 默认状态：true；
       */
      leftSidebarData : {},
      leftSidebarSearchValue : '',
      leftMenuState : false,
      leftStateData : true,
      
      /**
       * 封装右侧菜单栏参数 开始
       * rightSidebarData:菜单树数据 Object；
       * rightStateData: 控制菜单折叠按钮 Boolean 默认状态：true；
       */
      rightSidebarData : {},
      rightStateData : true,

      /**
       * 主体部分标题 开始
       * mainTitle:主体部分标题 String 
       * PDFData:PDF数据源地址 String 
       * PDFKey:PDF锚点值 String 
       */
      mainTitle:'请选择要处理的文件',
      PDFData:'',
      PDFKey:'',
      /**
       * 界面布局参数 开始
       * leftSpan:左侧菜单占比 number 默认值：5
       * mainSpan:主内容部分占比 number 默认值：12
       * rightSpan:右侧菜单占比 number 默认值：5
       * leftState:左侧菜单内容显隐 Boolean 默认值：true
       * rightState:右侧菜单内容显隐 Boolean 默认值：true
       */
      leftSpan:5,
      mainSpan:12,
      rightSpan:5,
      leftState:true,
      rightState:true,


      /**
       * 以下为测试数据 JSON  开始
       */
      leftMenuList1:{ //左侧菜单JSON数据
        litigationDocument:{
            name:'诉讼文书卷',
            list:[
              {
                index : '1-1',
                name : '受案登记表',
                tagState:'1', //是否有标签
                type : '',//标签背景色
                tagName : '',//标签名
                number : '',//数量
                PDFUrl:'1.pdf',//PDF数据源地址
                PDFKey:'建立必须填写的字段'//PDF锚点值
              },{
                index : '1-2',
                name : '受案回执',
                tagState:'0', //是否有标签
                type : 'danger',//标签背景色
                tagName : '不规范',//标签名
                number : '1',//数量
                PDFUrl:'1.pdf',//PDF数据源地址
                PDFKey:'建立必须填写的字段'//PDF锚点值
              }
          ],
        },
        volumeOfEvidence:{
            name:'证据材料卷',
            list:[
              {
                index : '2-1',
                name : '证据材料卷',
                tagState:'0', //是否有标签
                type : 'danger',//标签背景色
                tagName : '不规范',//标签名
                number : '1',//数量
                PDFUrl:'1.pdf',//PDF数据源地址
                PDFKey:'建立必须填写的字段'//PDF锚点值
              },{
                index : '2-2',
                name : '证据材料卷回执',
                tagState:'1', //是否有标签
                type : '',//标签背景色
                tagName : '',//标签名
                number : '',//数量
                PDFUrl:'1.pdf',//PDF数据源地址
                PDFKey:'建立必须填写的字段'//PDF锚点值
              }
          ],
        }
      },
      leftMenuList2:{ //左侧菜单JSON数据
        litigationDocument:{
            name:'诉讼文书卷2',
            list:[
              {
                index : '1-1',
                name : '受案登记表2',
                tagState:'1', //是否有标签
                type : '',//标签背景色
                tagName : '',//标签名
                number : '',//数量
                PDFUrl:'1.pdf',//PDF数据源地址
                PDFKey:'导航菜单'//PDF锚点值
              },{
                index : '1-2',
                name : '受案回执2',
                tagState:'0', //是否有标签
                type : 'danger',//标签背景色
                tagName : '不规范',//标签名
                number : '1',//数量
                PDFUrl:'1.pdf',//PDF数据源地址
                PDFKey:'导航菜单'//PDF锚点值
              }
          ],
        },
        volumeOfEvidence:{
            name:'证据材料卷2',
            list:[
              {
                index : '2-1',
                name : '证据材料卷2',
                tagState:'0', //是否有标签
                type : 'danger',//标签背景色
                tagName : '不规范',//标签名
                number : '1',//数量
                PDFUrl:'1.pdf',//PDF数据源地址
                PDFKey:'导航菜单'//PDF锚点值
              },{
                index : '2-2',
                name : '证据材料卷回执2',
                tagState:'1', //是否有标签
                type : 'danger',//标签背景色
                tagName : '不规范',//标签名
                number : '1',//数量
                PDFUrl:'1.pdf',//PDF数据源地址
                PDFKey:'导航菜单'//PDF锚点值
              }
          ],
        }
      },
      leftMenuList3:{ //左侧菜单JSON数据
        litigationDocument:{
            name:'诉讼文书卷3',
            list:[
              {
                index : '1-1',
                name : '受案登记表3',
                tagState:'1', //是否有标签
                type : '',//标签背景色
                tagName : '',//标签名
                number : '',//数量
                PDFUrl:'1.pdf',//PDF数据源地址
                PDFKey:'用户'//PDF锚点值
              },{
                index : '1-2',
                name : '受案回执3',
                tagState:'0', //是否有标签
                type : 'danger',//标签背景色
                tagName : '不规范',//标签名
                number : '1',//数量
                PDFUrl:'1.pdf',//PDF数据源地址
                PDFKey:'用户'//PDF锚点值
              }
          ],
        },
        volumeOfEvidence:{
            name:'证据材料卷3',
            list:[
              {
                index : '2-1',
                name : '证据材料卷3',
                tagState:'0', //是否有标签
                type : 'danger',//标签背景色
                tagName : '不规范',//标签名
                number : '1',//数量
                PDFUrl:'1.pdf',//PDF数据源地址
                PDFKey:'用户'//PDF锚点值
              },{
                index : '2-2',
                name : '证据材料卷回执3',
                tagState:'1', //是否有标签
                type : 'danger',//标签背景色
                tagName : '不规范',//标签名
                number : '1',//数量
                PDFUrl:'1.pdf',//PDF数据源地址
                PDFKey:'用户'//PDF锚点值
              }
          ],
        }
      },
      rightMenuList:{ // 右侧菜单JSON数据
        list:[
          {
            name:'不规范扫描件---图片重复上传',
            tagState:'1', //是否有标签
            tagList:[
              {
                type : 'danger',//标签背景色
                tagName : '重要'//标签名
              }
            ],
            radioLabel:'1',
            popoverState:'0',
            popoverContent:'证据图片重复上传'
          },{
            name:'组卷规范，警综平台已填写证据类型',
            tagState:'1', //是否有标签
            tagList:[
              {
                type : 'primary',//标签背景色
                tagName : '普通'//标签名
              }
            ],
            radioLabel:'2',
            popoverState:'1',
            popoverContent:''
          },{
            name:'格式错误',
            tagState:'1', //是否有标签
            tagList:[
              {
                type : 'danger',//标签背景色
                tagName : '重要'//标签名
              },{
                type : 'success',//标签背景色
                tagName : '人工标注'//标签名
              }
            ],
            radioLabel:'3',
            popoverState:'1',
            popoverContent:''
          },
        ]
      }
      /**
       * 以上为测试数据 JSON  结束
       */
    }
  },
  computed: {
    sidebar() {
      return this.$store.state.app.sidebar
    },
    device() {
      return this.$store.state.app.device
    },
    fixedHeader() {
      return this.$store.state.settings.fixedHeader
    },
    classObj() {
      return {
        hideSidebar: !this.sidebar.opened,
        openSidebar: this.sidebar.opened,
        withoutAnimation: this.sidebar.withoutAnimation,
        mobile: this.device === 'mobile'
      }
    }
  },
  created() {
    // 初始化右侧组件菜单数据
    this.rightSidebarData = this.rightMenuList;
  },
  methods: {
    
    // 获取左侧菜单子组件传递的参数
    leftFoldingFunc(e){
      this.leftSpan = e.leftSpan;
      this.leftState = e.leftState;
      this.mainSpan = e.mainSpan;
    },

    // 获取右侧菜单子组件传递的参数
    rightFoldingFunc(e){
      this.rightSpan = e.rightSpan;
      this.rightState = e.rightState;
      this.mainSpan = e.mainSpan;
    },

    // 左右菜单联动事件
    changeHandlerBtn(e){
      switch (e) {
        case '1':
          this.leftSidebarData = this.leftMenuList1;
          this.leftMenuState = true;
          break;
        case '2':
          this.leftSidebarData = this.leftMenuList2;
          this.leftMenuState = true;
          break;
        case '3':
          this.leftSidebarData = this.leftMenuList3;
          this.leftMenuState = true;
          break;
        default:
          break;
      }
    },

    // 左侧菜单与主内容互动事件
    mainTitleBtn(e){
      this.mainTitle = e.name;
      this.PDFData = e.PDFUrl;
      if (e.PDFKey) {
        this.PDFKey = e.PDFKey;
      } else {
        localStorage.removeItem('gethighLightWords');
      }
      console.log('layout-PDFKey:',e.PDFKey);
    }
  }
}
</script>

<style lang="scss" scoped>
  @import "~@/styles/mixin.scss";
  @import "~@/styles/variables.scss";

  .app-wrapper {
    @include clearfix;
    position: relative;
    height: 100%;
    width: 100%;
    &.mobile.openSidebar{
      position: fixed;
      top: 0;
    }
  }
  .mainPartStyle{
    padding-top: 10px;
  }
  .drawer-bg {
    background: #000;
    opacity: 0.3;
    width: 100%;
    top: 0;
    height: 100%;
    position: absolute;
    z-index: 999;
  }
  
  .imgStyle{
    width: 32px;
    height: 32px;
    vertical-align: middle;
    margin-right: 12px;
  }
  .fixed-header {
    position: fixed;
    top: 0;
    right: 0;
    z-index: 9;
    width: calc(100% - #{$sideBarWidth});
    transition: width 0.28s;
  }

  .hideSidebar .fixed-header {
    width: calc(100% - 54px)
  }

  .mobile .fixed-header {
    width: 100%;
  }
</style>
