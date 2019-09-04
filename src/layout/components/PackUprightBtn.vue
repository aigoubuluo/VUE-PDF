<template>
  <el-col :span="1" v-if="rightFoldingData.rightState">
    <img src="@/assets/img/packUpright.png" v-on:click="rightBtn" class="packUprightStyle" />
  </el-col>
  <el-col :span="1" v-else>
    <img src="@/assets/img/openRight.png" v-on:click="openRightBtn" class="packUprightStyle" />
  </el-col>
</template>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'PackUprightBtn',
  props: {
    rightStateData: {
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
      rightFoldingData : {
        rightState : true,
        rightSpan : 5,
        mainSpan : 12
      }
    }
  },
  mounted() {
    this.rightFoldingData.rightState = this.rightStateData;
  },
  watch: {
    rightStateData: {
      immediate: true,
      handler (val) {
        this.rightFoldingData.rightState = val
      }
    },
    mainSpanData: {
      immediate: true,
      handler (val) {
        this.rightFoldingData.mainSpan = val
      }
    }
  },
  methods: {
    // 折叠事件
    rightBtn(){
      this.rightFoldingData.rightState=!this.rightFoldingData.rightState;
      this.rightFoldingData.rightSpan = 0;
      if (this.rightFoldingData.mainSpan === 12) {
        this.rightFoldingData.mainSpan = 17
        this.$emit('rightFoldingFunc', this.rightFoldingData)
      } else {
        this.rightFoldingData.mainSpan = 22
        this.$emit('rightFoldingFunc', this.rightFoldingData)
      }
    },

    // 展开事件
    openRightBtn(){
      this.rightFoldingData.rightState=!this.rightFoldingData.rightState;
      this.rightFoldingData.rightSpan = 5;
      if (this.rightFoldingData.mainSpan === 22) {
        this.rightFoldingData.mainSpan = 17
        this.$emit('rightFoldingFunc', this.rightFoldingData)
      } else {
        this.rightFoldingData.mainSpan = 12
        this.$emit('rightFoldingFunc', this.rightFoldingData)
      }
    },
  }
}
</script>

<style lang="scss" scoped>
.packUprightStyle{
  height: 50%; 
  width: 50%; 
  margin-left: 50px; 
  margin-top: 380px;
}
</style>
