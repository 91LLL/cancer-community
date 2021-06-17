<template>
  <view class="login-content">
    <u-form ref="uForm" :model="form" label-width="auto">
      <u-form-item label="手机号码" prop="name">
        <u-input v-model="form.name" />
      </u-form-item>
      <u-form-item label="验证码" prop="intro">
        <u-input v-model="form.intro" />
      </u-form-item>
    </u-form>
    <u-button @click="submit">提交</u-button>
  </view>
</template>

<script>
export default {

}
</script>

<style lang="scss">
.login-content{
  padding: 0 100rpx;
}
</style>
