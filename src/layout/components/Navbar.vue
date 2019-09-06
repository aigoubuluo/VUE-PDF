<template>
  <div>
    <div class="heardTitle">
      <el-row :gutter="20">
        <el-col :span="18">
          <span style="color:#fff">{{heardTitleText}}</span> 
        </el-col>
        <el-col :span="6" >
          <!--  自定义功能按钮请在此处编写  -->
        </el-col>
      </el-row>
    </div>
    <hamburger />
  </div>
  
</template>

<script>
import { mapGetters } from 'vuex'
import Hamburger from '@/components/Hamburger/Hamburger'

export default {
  components: {
    Hamburger
  },
  computed: {
    ...mapGetters([
      // 'sidebar',
      // 'avatar'
    ])
  },
  data() {
    return {
      heardTitleText:"智能辅助办案系统"
    }
  },
  methods: {
    // 填写自定义方法
  }
}
</script>

<style lang="scss" scoped>
.heardTitle{
    padding-left: 20px;
    background-color:#558EE2; 
    height: 60px; 
    width: 100%; 
    color:#fff;
    position:fixed; 
    z-index:9999; 
    border-bottom: 1px solid #558EE2;
    font-size: 18px;
    padding-top: 18px;
    font-weight:bold;
    background-repeat: no-repeat;
    background-size: cover;
    background-image: url('../../assets/img/heardbg.png')
  }
</style>
