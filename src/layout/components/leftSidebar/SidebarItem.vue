<template>
  <el-menu
      default-active="1-1"
      class="el-menu-vertical-demo">
      <el-submenu index="1">
        <template slot="title">
          <svg-icon icon-class="referee-doc"/>
          <span>{{leftMenuList.litigationDocument.name}}</span>
        </template>
        <el-menu-item-group v-for="(item,key) in leftMenuList.litigationDocument.list" :key="key">
          <el-menu-item :index="item.index" v-on:click="PDFBtn(item)">{{item.name}}
            <el-tag size="mini" :type="item.type" effect="plain" v-if="item.tagState==='0'">
                {{item.tagName}}
            </el-tag>
            <el-tag size="mini" :type="item.type" effect="plain" v-if="item.tagState==='0'">
                {{item.number}}
            </el-tag>
          </el-menu-item>
        </el-menu-item-group>
      </el-submenu>
      <el-submenu index="2">
        <template slot="title">
          <svg-icon icon-class="seal"/>
          <span slot="title">{{leftMenuList.volumeOfEvidence.name}}</span>
        </template>
        <el-menu-item-group v-for="(item,key) in leftMenuList.volumeOfEvidence.list" :key="key">
          <el-menu-item :index="item.index" v-on:click="WPSBtn(item)">{{item.name}}
            <el-tag size="mini" :type="item.type" effect="plain" v-if="item.tagState==='0'">
                {{item.tagName}}
            </el-tag>
            <el-tag size="mini" :type="item.type" effect="plain" v-if="item.tagState==='0'">
                {{item.number}}
            </el-tag>
          </el-menu-item>
        </el-menu-item-group>
      </el-submenu>
    </el-menu>
</template>

<script>

export default {
  name: 'SidebarItem',
  props: {
    itemSidebarData: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      leftMenuList:{},
    }
  },
  mounted() {
    this.leftMenuList = this.itemSidebarData;
  },
  watch: {
    itemSidebarData: {
      immediate: true,
      handler (val) {
        this.leftMenuList = val
      }
    }
  },
  methods:{
    PDFBtn(e){
      this.$emit('mainPDFData', e)
    },

    WPSBtn(e){
      this.$emit('mainPDFData', e)
    }
  }
}
</script>
<style lang="scss" scoped>
.el-menu-vertical-demo {
  color: #fff;
  border-right: solid 1px #fff; 
  list-style: none;
  position: relative;
  margin: 0;
  padding-left: 0;
  background-color: #FFF;
}
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 100%;
}
</style>
