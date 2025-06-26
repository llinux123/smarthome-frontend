<route lang="json5" type="home">
{
  "layout": "tabbar",
  "style": {
    "navigationStyle": "custom",
    "navigationBarTitleText": "登录"
  }
}
</route>

<!-- pages/login/index.vue -->
<script lang="ts" setup>
// pages/login/index.vue
const form = reactive({ username: '', password: '' })

function handleReset() {
  // getCode()
  console.log('重置表单')
  uni.reLaunch({
    url: '/pages/login/login',
  })
}
async function handleLogin() {
  uni.navigateTo({
    url: '/pages/layout/layout',
  })
}

function handleForget() {
  uni.navigateTo({
    url: '/pages/forget/forget',
  })
}
</script>

<template>
  <view class="p-4">
    <view class="login-container">
      <view class="login-header">
        <wd-icon name="home" size="32" color="#d14328" />
        SmartHome
      </view>
      <wd-form ref="form" :model="form" class="h-full w-full flex items-center justify-center">
        <wd-cell-group border class="w-full flex flex-col items-center">
          <wd-input
            v-model="form.username" label="用户名" label-width="100px" prop="value1" clearable placeholder="请输入用户名"
            :rules="[{ required: true, message: '请填写用户名' }]"
          />
          <wd-input
            v-model="form.password" label="密码" label-width="100px" prop="value2" clearable show-password
            placeholder="请输入密码" :rules="[{ required: true, message: '请填写密码' }]"
          />
          <wd-button type="primary" size="large" block @click="handleLogin">
            登录
          </wd-button>
          <view class="footer mt-4 flex justify-between">
            <wd-button type="default" size="large" block @click="handleReset">
              重置
            </wd-button>
            <wd-button type="primary" size="large" block @click="handleForget">
              忘记
            </wd-button>
          </view>
        </wd-cell-group>
      </wd-form>
    </view>
  </view>
</template>

<style scoped></style>
