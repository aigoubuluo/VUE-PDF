<template>
  <div class="mainStyle">

    <el-row :gutter="12" style="margin-bottom: 10px;"  v-for="(item,key) in rightMenuList.list" :key="key">
      <el-col :span="24">
        <el-card :shadow="(radio == item.radioLabel)?'always':'hover'">
          <p :class="(radio == item.radioLabel)?'always':'hover'">{{key+1}} {{item.name}}
            <el-popover
              v-if="item.popoverState==='0'"
              placement="top-start"
              width="200"
              height="10"
              trigger="hover"
              :content="item.popoverContent">
              <svg-icon icon-class="notes" slot="reference"/> 
            </el-popover> 
          </p>
          <el-radio v-model="radio" :label="item.radioLabel" v-on:change="changeHandler">
            <el-tag style="margin-left: 10px;" size="mini" v-for="(e,key) in item.tagList" :type="e.type" effect="plain" :key="key" v-if="item.tagState==='1'">
                {{e.tagName}}
            </el-tag>
          </el-radio>
        </el-card>
      </el-col>
    </el-row>

  </div>

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
      rightMenuList:{},
      radio: '',
    }
  },
  mounted() {
    this.rightMenuList = this.itemSidebarData;
  },
  watch: {
    itemSidebarData: {
      immediate: true,
      handler (val) {
        this.rightMenuList = val
      }
    }
  },
  methods:{
    changeHandler(e){
      this.$emit('rightChangeHandler', e)
    }
  }
}
</script>
<style lang="scss" scoped>
.mainStyle{
  height: 570px;
  overflow-y: auto;
  overflow-x: hidden;
}
.always{
  color:#558EE2;
  font-weight:bold;
}
.hover{
  color:#9F9DA1;
}
</style>
