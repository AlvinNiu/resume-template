<template>
    <div>
        <div class="title">
            <h2 class="title">关于我</h2>
        </div>
        <p class="aboutme">{{aboutme}}</p>
    </div>
</template>
<script>
export default {
  name: 'AboutMe',
  data: function () {
    return require('@/assets/resume.json')
  }
}
</script>
<style lang="less">
.aboutme {
  background: #f6f7f7;
  padding: 20px;
}
</style>
