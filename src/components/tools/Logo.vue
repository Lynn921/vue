<template>
  <div class="logo">
    <router-link :to="{name:'project'}">
      <img src="~@/assets/logo.svg" alt="logo">
      <h1>{{ title }}</h1>
    </router-link>
  </div>
</template>

<script>
  export default {
    name: 'Logo',
    props: {
      title: {
        type: String,
        default: 'Jeecg-Boot Pro',
        required: false
      },
      showTitle: {
        type: Boolean,
        default: true,
        required: false
      }
    }
  }
</script>
<style lang="scss" scoped>
  /*缩小首页布 局顶部的高度*/
  $height: 59px;

  .sider {
    box-shadow: none !important;
    .logo {
      padding-left:  10px;
      height: $height !important;
      line-height: $height !important;
      box-shadow: none !important;
      transition: background 300ms;
      color: #fff;
      a {
        color: white;
        &:hover {
          color: rgba(255, 255, 255, 0.8);
        }
      }
    }

    &.light .logo {
      background-color: #1890ff;
    }
  }
</style>