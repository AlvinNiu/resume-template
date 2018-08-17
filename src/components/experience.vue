<template>
    <div>
        <div class="title">
            <h2 class="title">工作经历</h2>
        </div>
        <ul>
            <li v-for="experience in experiences" :key="experience.id" class="list-item-experience">
                <div class="heading">
                    <span class="company">{{ experience.company_name }}</span>
                    <span class="job">{{ experience.job }}</span>
                    <span class="date">{{ experience.date }}</span>
                </div>
                <p>
                    {{ experience.description }}
                </p>
                <!-- <h4>项目</h4> -->
                <ul>
                    <li v-for="project in experience.projects" :key="project.id" class="project-li">
                        <div class="project-heading">
                            <span class="project-name">{{project.project_name}}</span>
                            <span class="project-name">{{project.role}}</span>
                            <div>
                                <span v-for="skill in project.skills" :key="skill.id" class="skill-list" :style="{ width: '30%', padding: '3px', background: skill.color}">{{skill.skill_name}}</span>

                            </div>
                        </div>
                        <div class="description-div">
                            <p v-for="(item, index) in project.description" :key="index" class="decription" style="    font-size: 17px;    line-height: 18px;">
                                {{item}}
                            </p>
                        </div>
                    </li>
                </ul>
            </li>
        </ul>

    </div>
</template>
<script>
export default {
  name: 'Experience',
  data: function () {
    return {
      colors: ['#41b883', '#2883c6', '#f49b16', '#e62120', '#33475c', '#cc146f']
    }
  },
  computed: {
    experiences: function () {
      var resumeJson = require('@/assets/resume.json')
      resumeJson.woring_experence.forEach(item => {
        item.projects.forEach(project => {
          var index = 0
          project.skills.forEach(element => {
            if (typeof element.color === 'undefined') {
              this.$set(element, 'color', this.colors[index++])
            }
          })
        })
      })
      return resumeJson.woring_experence
    }
  }
}
</script>

<style lang="less">
.list-item-experience {
  margin-top: 20px;
  .heading {
    font-size: 18px;
    font-weight: bold;
    display: flex;
    justify-content: space-between;
    margin-bottom: 12px;
    .company {
      width: 40%;
    }
    .job {
      width: 35%;
    }
    .date {
      width: 25%;
      text-align: right;
    }
  }
}
.project-heading {
  font-size: 16px;
  font-weight: bold;
  display: flex;
  justify-content: space-between;
  margin-bottom: 12px;
}
.project-li {
  background: #f6f7f7;
  padding: 20px;
}
.project-name {
  width: 30%;
}
.skill-list {
  margin-left: 12px;
  border-radius: 5px;
}
.description-div {
  margin-top: 20px;
}
</style>
