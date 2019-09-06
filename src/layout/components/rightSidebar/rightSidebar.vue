<template>
  <div style="background-color:#fff; padding: 10px; height: 820px; " >
    <template>
      <el-tabs v-model="activeName" class="tabPane">
        <el-tab-pane label="问题锚点列表(3)" name="first">

          <!-- 搜索栏 star-->
          <right-search />
          <!-- 搜索栏 end-->

          <el-divider></el-divider>

          <!-- 主题菜单 star-->
          <sidebar-item :itemSidebarData="itemSidebarData" @rightChangeHandler="rightChangeHandlerItem"/>
          <!-- 主题菜单 end-->

          <el-divider></el-divider>

          <!-- 底部功能按钮 star-->
          <el-row :gutter="12">
            <el-col :span="10" :offset="2" class="offsetBtnNo">
              <el-button type="danger" size="medium" round>有问题</el-button>
            </el-col>
            <el-col :span="10" :offset="2" class="offsetBtnMES">
              <el-button type="primary" size="medium" round>没问题</el-button>
            </el-col>
          </el-row>
          <!-- 底部功能按钮 end-->

        </el-tab-pane>
        <el-tab-pane label="已确认锚点列表(0)" name="second">
          <!-- 请在此处编写已通过校验点界面代码 -->
          <rightPrompt />
        </el-tab-pane>
      </el-tabs>
    </template>
    
  </div>

</template>

<script>
import { mapGetters } from 'vuex'

import rightSearch from './rightSearch'// 顶部搜索输入框
import SidebarItem from './SidebarItem'// 主题菜单
import rightPrompt from './rightPrompt'// 友好提示

export default {
  name:"leftSidebar",
  components: { SidebarItem, rightSearch, rightPrompt},
  props: {
    rightSidebarData: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      activeName:'first', // 右侧菜单栏TAB默认选中第一个标签
      itemSidebarData:{},
    }
  },
  mounted() {
    this.itemSidebarData = this.rightSidebarData;
  },
  watch: {
    rightSidebarData: {
      immediate: true,
      handler (val) {
        this.itemSidebarData = val
      }
    }
  },
  computed: {
    ...mapGetters([
      'sidebar'
    ]),
  },
  methods: {
    rightChangeHandlerItem(e){
      this.$emit('rightChangeHandler', e)
    }
  }
}
</script>

<style  lang="scss" scoped>
.tabPane{
    font-size: 12px;
  }
.offsetBtnNo{
    text-align:right;
  }
.offsetBtnMES{
  text-align:left;
}
</style>

