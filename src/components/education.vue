<template>
    <div>
        <div class="title">
            <h2 class="title">教育经历</h2>
        </div>
        <ul>
            <li v-for="education in educations" :key="education.id" class="list-item-education">
                <span class="school">{{ education.school }}</span>
                <span class="major">{{ education.major }}</span>
                <span class="date">{{ education.date }}</span>
            </li>
        </ul>

    </div>
</template>
<script>
export default {
  name: 'Education',
  data: function () {
    return {}
  },
  computed: {
    educations: function () {
      var resumeJson = require('@/assets/resume.json')
      return resumeJson.educations
    }
  }
}
</script>

<style lang="less">
.list-item-education {
  font-size: 18px;
  font-weight: bold;
  display: flex;
  justify-content: space-between;
  background: #f6f7f7;
  padding: 20px;
  .school {
    width: 40%;
  }
  .major {
    width: 35%;
  }
  .date {
    width: 25%;
    text-align: right;
  }
}
</style>
