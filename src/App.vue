<template>
  <div id="app">
    <!-- <img src="./assets/logo.png">
    <router-view/> -->
    <div class="resume">
      <div class="left">
        <brief :parent_data="result_data"></brief>
        <contact :parent_data="result_data"></contact>
      </div>
      <div class="right">
        <about-me class="bottom" :parent_data="result_data"></about-me>
        <skill class="bottom" :parent_data="result_data"></skill>
        <education class="bottom" :parent_data="result_data"></education>
        <experience class="bottom" :parent_data="result_data"></experience>
      </div>
    </div>
  </div>
</template>

<script>
import Brief from '@/components/brief'
import Contact from '@/components/contact'
import AboutMe from '@/components/about_me'
import Skill from '@/components/skill'
import Education from '@/components/education'
import Experience from '@/components/experience'
export default {
  name: 'App',
  data: function () {
    return {
      result_data: require('@/assets/resume.json')}
  },
  components: { Brief, Contact, AboutMe, Skill, Education, Experience }
}
</script>

<style lang="less">
body {
  padding: 0;
  margin: 0;
}
ul {
  padding: 0;
  margin: 0;
  li {
    list-style: none;
  }
}
p {
  margin: 0 0 12px 0;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: left;
  color: #2c3e50;
  background-color: white;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  padding: 40px 0;
  .resume {
    width: 1247px;
    height: 1754px;
    border: 1px solid #dad8d7;
    background-color: white;
    overflow: hidden;
    .left {
      width: 380px;
      height: 100%;
      box-sizing: border-box;
      float: left;
      background-color: #fdfefe;
      .brief {
        height: 630px;
        background-color: #f6f7f7;
        .avatar {
          height: 500px;
          display: flex;
          flex-direction: column;
          align-items: center;
          justify-content: center;
          & > .img {
            margin-bottom: 45px;
          }
          .name {
            font-size: 32px;
            margin-bottom: 14px;
          }
          .job {
            font-size: 24px;
            color: #555;
            margin-bottom: 16px;
          }
          .location {
            display: flex;
            align-itmes: center;
            .location-name {
              font-size: 20px;
              font-weight: bold;
              margin-left: 10px;
            }
          }
        }
        .info {
          height: 128px;
          ul {
            height: 100%;
            display: flex;
            border-top: 1px solid #dad8d7;
            border-bottom: 1px solid #dad8d7;
            li:not(:last-child) {
              border-right: 1px solid #dad8d7;
            }
            li {
              width: 33.3333333%;
              display: flex;
              flex-direction: column;
              justify-content: center;
              text-align: center;
              .value {
                margin-bottom: 10px;
                font-size: 24px;
                font-weight: bold;
              }
              .key {
                font-size: 16px;
                font-weight: bold;
                color: #555;
              }
            }
          }
        }
      }
    }
    .right {
      box-sizing: border-box;
      width: 867px;
      float: left;
      padding: 50px 40px;
      p {
        font-size: 20px;
        line-height: 32px;
        color: #555;
        text-align: justify;
      }
    }
  }
  button.sap {
    position: absolute;
    top: 65px;
    left: 50%;
    margin-left: 478px;
    background-color: white;
    border: 1px solid #dad8d7;
    cursor: pointer;
    padding: 5px 8px;
    border-radius: 4px;
    &:hover {
      background-color: #f8f8f8;
    }
  }
  .guide {
    border: 1px solid #dad8d7;
    width: 1247px;
    margin-top: 15px;
    height: 120px;
    ul {
      width: 100%;
      height: 100%;
      display: flex;
      justify-content: space-around;
      align-items: center;
      li {
        display: flex;
        align-items: center;
        img {
          margin: 0 10px;
        }
        h3 {
          margin: 0 0 6px 0;
        }
        p {
          margin: 0;
          font-size: 16px;
        }
      }
    }
  }
  .footer {
    line-height: 50px;
    a {
      text-decoration: none;
      color: #4aa74f;
      &:first-child {
        display: block;
        text-align: center;
        line-height: 0;
        margin-top: 15px;
      }
    }
  }
}
.bottom {
  margin-bottom: 30px;
}
</style>
