<template>
  <el-col :span="1" v-if="foldingData.leftState">
    <img src="@/assets/img/packUpLeft.png" v-on:click="leftBtn" class="packUpLeftStyle" />
  </el-col>
  <el-col :span="1" v-else>
    <img src="@/assets/img/openLeft.png" v-on:click="openLeftBtn" class="packUpLeftStyle" />
  </el-col>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'PackUpLeftBtn',
  props: {
    leftStateData: {
      type: Boolean,
      required: true
    },
    mainSpanData:{
      type: Number,
      required: true
    }
  },
  computed: {
    ...mapGetters([
      // 'sidebar',
      // 'avatar'
    ])
  },
  data(){
    return {
      foldingData : {
        leftState : true,
        leftSpan : 5,
        mainSpan : 12
      }
    }
  },
  mounted() {
    this.foldingData.leftState = this.leftStateData;
  },
  watch: {
    leftStateData: {
      immediate: true,
      handler (val) {
        this.foldingData.leftState = val
      }
    },
    mainSpanData: {
      immediate: true,
      handler (val) {
        this.foldingData.mainSpan = val
      }
    }
  },
  methods: {
    // 折叠事件
    leftBtn(){
      this.foldingData.leftState=!this.foldingData.leftState;
      this.foldingData.leftSpan = 0;
      if (this.foldingData.mainSpan === 12) {
        this.foldingData.mainSpan = 17
        this.$emit('leftFoldingFunc', this.foldingData)
      } else {
        this.foldingData.mainSpan = 22
        this.$emit('leftFoldingFunc', this.foldingData)
      }
    },
    // 展开事件
    openLeftBtn(){
      this.foldingData.leftState=!this.foldingData.leftState;
      this.foldingData.leftSpan = 5;
      if (this.foldingData.mainSpan === 22) {
        this.foldingData.mainSpan = 17
        this.$emit('leftFoldingFunc', this.foldingData)
      } else {
        this.foldingData.mainSpan = 12
        this.$emit('leftFoldingFunc', this.foldingData)
      }
    }
  }
}
</script>

<style lang="scss" scoped>
.packUpLeftStyle{
  height: 50%; 
  width: 50%; 
  margin-left: -8px; 
  margin-top: 380px;
}
</style>
