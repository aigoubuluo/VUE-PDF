<template>
    <p class="promptStyle">
      <span class="promptTitleStyle">{{promptTitle}}</span>  <br><br>
      {{promptText}}
    </p>
</template>

<script>
export default {
  name: 'leftPrompt',
  data() {
    return {
      promptTitle:"温馨提示",
      promptText:"暂时没有处理好的数据哦！"
    }
  }
}
</script>

<style lang="scss" scoped>
.promptStyle{
  padding-top: 160px;
  color: rgba(31, 94, 150, 0.591);
  margin: 20px; 
  text-align:center;
}
.promptTitleStyle{
  font-size: 20px;
  color: #558EE2;
  font-weight:bold;
}
</style>
