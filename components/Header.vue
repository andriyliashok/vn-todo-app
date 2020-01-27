<template>
  <view class="header">
    <text class="header__title">{{ title }}</text>
  </view>
</template>

<script>
export default {
  name: 'Header',
  props: {
    title : {
      type: String,
      default: '',
    },
  }
}

</script>

<style lang="scss" scoped>
  .header {
    height: 50px;
    padding: 10px;
    background-color: black;
  }

  .header__title {
    font-size: 30px;
    text-align: center;
    color: #FFFFFF;
    font-weight: 600;
    text-transform: uppercase;
    margin: 0;
  }
</style>
