<template>
  <div style="background-color:#fff;padding: 10px; height: 820px;">
    <!-- 搜索栏 star-->
    <left-search />
    <!-- 搜索栏 end-->

    <el-divider></el-divider>

    <!-- 主题菜单 star-->
    <sidebar-item :itemSidebarData="itemSidebarData" @mainPDFData="mainPDFDataItem" v-if="leftMenuSidebarState"/>
    <!-- 主题菜单 end-->

    <!-- 温馨提示 star-->
    <left-prompt v-else />
    <!-- 温馨提示 end-->

  </div>
</template>

<script>
import { mapGetters } from 'vuex'

import leftSearch from './leftSearch'// 顶部搜索输入框
import SidebarItem from './SidebarItem'// 主题菜单
import leftPrompt from './leftPrompt'// 友好提示

export default {
  name:"leftSidebar",
  components: { SidebarItem, leftSearch, leftPrompt },
  props: {
    leftSidebarData: {
      type: Object,
      required: true
    },
    leftSidebarSearchValue: {
      type: String,
      required: true
    },
    leftMenuState: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      itemSidebarData:{},
      leftMenuSidebarState:false
    }
  },
  mounted() {
    this.itemSidebarData = this.leftSidebarData;
    this.leftMenuSidebarState = this.leftMenuState;
  },
  watch: {
    leftSidebarData: {
      immediate: true,
      handler (val) {
        this.itemSidebarData = val
      }
    },
    leftMenuState: {
      immediate: true,
      handler (val) {
        this.leftMenuSidebarState = val
      }
    }
  },
  computed: {
    ...mapGetters([
      'sidebar'
    ]),
  },
  methods: {
    mainPDFDataItem(e){
      this.$emit('mainPDFData', e)
    }
    
  }
}
</script>
