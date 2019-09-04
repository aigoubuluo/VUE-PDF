<template>
    <el-input placeholder="请输入关键字" size="mini" class="input-with-select">
      <el-select v-model="select" slot="prepend" placeholder="请选择">
        <el-option label="全部" value="1"></el-option>
        <el-option label="下拉菜单1" value="2"></el-option>
        <el-option label="下拉菜单2" value="3"></el-option>
      </el-select>
      <el-button slot="append" style="color:#558EE2" icon="el-icon-search"></el-button>
    </el-input>
</template>

<script>
export default {
  name: 'leftSearch',
  props: {
    // collapse: {
    //   type: Boolean,
    //   required: true
    // }
  },
  data() {
    return {
      select: '',
    }
  }
}
</script>

<style lang="scss" scoped>

</style>
