<template>
  <div>
    <div class="title">
      <h2 class="title">技能</h2>
    </div>
    <ul>
      <li v-for="skill in skills" :key="skill.id" class="list-item-skill">
        <span class="skillname">{{skill.skill_name}}</span>
        <span class="line">
          <span class="show" :style="{ width: skill.percent + '%', background: skill.color }"></span>
        </span>
        <span class="input">
          {{skill.percent}}%
        </span>
      </li>
    </ul>

  </div>
</template>
<script>
export default {
  name: 'Skill',
  data: function () {
    return {
      selectColor: '',
      colors: ['#41b883', '#2883c6', '#f49b16', '#e62120', '#33475c', '#cc146f']
    }
  },
  props: {
    parent_data: {}
  },
  computed: {
    skills: function () {
      var index = 0
      this.parent_data.skills.forEach(element => {
        if (typeof element.color === 'undefined') {
          this.$set(element, 'color', this.colors[index++])
        }
      })
      return this.parent_data.skills
    }
  }
}
</script>

<style lang="less">
.list-item-skill {
  position: relative;
  display: flex;
  justify-content: space-between;
  align-items: center;
  font-size: 20px;
  background: #f6f7f7;
  padding: 20px;
  .skillname {
    width: 30px;
    text-align: right;
  }
  span.line {
    position: relative;
    display: inline-block;
    width: 520px;
    height: 8px;
    background-color: #c2c2c2;
    .show {
      content: '';
      position: absolute;
      height: 100%;
    }
  }
}
</style>
