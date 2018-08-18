<template>
  <div>
    <!-- 联系方式 -->
    <div class="contact">
      <div class="list-heading icon-class">
        <div class="title">
          <EditImage :src="require('@/assets/title-contact.png')" height="36" width="36" class="img"></EditImage>
          <h2 class="title">{{contactTitle}}</h2>
        </div>
      </div>
      <ul class="list-ul">
        <li v-for="contact in contacts" :key="contact.type" class="list-item">
          <EditImage :src="contact.image" class="img"></EditImage>
          <span>{{ contact.title }}</span>
        </li>
      </ul>
    </div>
    <!-- 社交论坛 -->
    <div class="contact">
      <div class="list-heading icon-class">
        <div class="title">
          <EditImage :src="require('@/assets/title-contact.png')" height="36" width="36" class="img"></EditImage>
          <h2 class="title">{{socialTitle}}</h2>
        </div>
      </div>
      <ul class="list-ul">
        <li v-for="social in socials" :key="social.type" class="list-item">
          <EditImage :src="social.image" class="img"></EditImage>
          <span>{{ social.title }}</span>
        </li>
      </ul>
    </div>
  </div>
</template>
<script>
import EditImage from '@/components/edit-image'
export default {
  name: 'Contact',
  data: function () {
    return {
      contactTitle: '联系方式',
      socialTitle: '社交论坛'
    }
  },
  props: {
    parent_data: {}
  },
  components: {
    EditImage
  },
  computed: {
    contacts: function () {
      return this.parent_data.contacts
    },
    socials: function () {
      return this.parent_data.socials
    }
  }
}
</script>

<style lang="less">
.contact {
  width: 100%;
  margin-bottom: 30px;
  .list-heading {
    display: flex;
    justify-content: space-between;
    align-items: center;
    .title {
      display: flex;
      align-items: center;
      .img {
        margin: 0 20px 0 50px;
      }
    }
    &:hover .add {
      display: block;
    }
    .add {
      display: none;
    }
  }
}
.icon-class {
  background-color: #f6f7f7;
  border-bottom: 1px solid #e9e8e8;
}
.icon-margin-bottom {
  margin-bottom: 0;
}
.icon-margin-right {
  margin-right: 15px;
}
.list-item {
  position: relative;
  & > span:first-child {
    // border-right: 1px solid #dad8d7;
    border-radius: 4px 0 0 4px;
  }
  & > span:last-child {
    border-radius: 0 4px 4px 0;
  }
  display: flex;
  align-items: center;
  border-bottom: 1px solid #e9e8e8;
  height: 80px;
  .img {
    margin: 0 20px 0 50px;
  }
  span {
    font-size: 20px;
    color: #555;
  }
}
</style>
