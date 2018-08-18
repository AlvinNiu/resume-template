<template>
  <div>
    <div class="title">
      <h2 class="title">关于我</h2>
    </div>
    <p class="aboutme">{{parent_data.aboutme}}</p>
  </div>
</template>
<script>
export default {
  name: 'AboutMe',
  props: {
    parent_data: {}
  }
}
</script>
<style lang="less">
.aboutme {
  background: #f6f7f7;
  padding: 20px;
}
</style>
