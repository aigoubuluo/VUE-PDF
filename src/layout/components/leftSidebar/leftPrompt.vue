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
      promptText:"请选择右侧瑕疵点进行文件筛选"
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
