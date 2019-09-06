<template>
  <div class="heardTitle2">
      <el-row>
        <el-col :span="20">
          <span>
            <b>测试（B510000000000029387178293）</b>
          </span> 
          <el-tag size="mini" type="danger" effect="dark">
              危害国家安全案
          </el-tag>
        </el-col>
        <el-col :span="1">
          <svg-icon icon-class="trajectory"/>
          <span>轨迹</span>
        </el-col>
        <el-col :span="1">
          <svg-icon icon-class="Emap"/>
          <span>图谱</span>
        </el-col>
        <el-col :span="1">
          <svg-icon icon-class="full-screen"/>
          <span>全屏</span>
        </el-col>
        <el-col :span="1">
          <svg-icon icon-class="back"/>
          <span>返回</span>
        </el-col>
      </el-row>
    </div>
</template>

<script>
export default {
  name: 'Hamburger',
  props: {
    isActive: {
      type: Boolean,
      default: false
    }
  },
  methods: {
    toggleClick() {
      this.$emit('toggleClick')
    }
  }
}
</script>

<style scoped>
.heardTitle2{
    padding-left: 20px;
    font-size: 12px;
    padding-top: 75px;
    padding-bottom: 8px;
    color: #057DE4;
    background-color: #fff;
    border-bottom: 1px solid rgba(90, 176, 250, 0.4);
}
</style>
