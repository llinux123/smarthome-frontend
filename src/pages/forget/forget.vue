<route lang="json5">
{
  "layout": "tabbar",
  "style": {
    "navigationStyle": "custom",
    "navigationBarTitleText": "忘记密码"
  }
}
</route>

<!-- pages/forget/forget.vue -->
<script lang="ts" setup>
// pages/forget/forget.vue
import { httpGet } from '@/utils/http'

const form = reactive({ username: '', code: '' })
function handleSubmit() {
  // getCode()
  uni.navigateTo({
    url: '/pages/login/login',
  },
  )
}

function handleSendcode() {
  interface IFooItem { }

  const { loading, error, data, run } = useRequest<IFooItem>(() => httpGet('/foo', { name: '菲鸽' }))

  // const { loading, error, data } = useRequest<IFooItem>(() => httpGet('/api/login/code', {}))
  // if (loading) {
  //     console.log('Loading...');
  //     uni.showToast({
  //         title: '验证码正在发送',
  //         icon: 'success'
  //     })
  // }
  // if (error) {
  //     console.log('Error:', error);
  //     uni.showToast({
  //         title: '验证码发送失败',
  //         icon: 'none'
  //     })
  // }
  // else {
  //     console.log('Data:', data);
  //     uni.showToast({
  //         title: '验证码已发送',
  //         icon: 'success'
  //     })
  // }
}

// const handleSendcode = async () => {
//     // if (!form.username) {
//     //     uni.showToast({
//     //         title: '请填写用户名',
//     //         icon: 'none'
//     //     })
//     //     return
//     // }
//     // const res = await getCode(form.username)

// }
</script>

<template>
  <view class="p-4">
    <view class="border border-r rounded-lg p-4">
      <view class="login-header">
        <wd-icon name="home" size="32" color="#d14328" />
        SmartHome
      </view>
      <wd-form ref="form" :model="form" class="h-full flex items-center justify-center">
        <wd-cell-group border class="">
          <view class="p-4">
            <wd-input
              v-model="form.username" label="用户名" label-width="100px" clearable placeholder="请输入用户名"
              :rules="[{ required: true, message: '请填写用户名' }]"
            />
          </view>
          <view class="flex p-4">
            <!-- #ifdef H5 -->
            <wd-input
              v-model="form.code" label="验证码" label-width="100px" clearable show-password
              placeholder="请输入验证码" :rules="[{ required: true, message: '验证码错误' }]"
            />
            <!-- #endif -->
            <!-- #ifdef MP-WEIXIN| APP -->
            <wd-number-keyboard v-model="form.code" :maxlength="4" />

            <!-- #endif -->
            <wd-button
              class-prefix="fish" icon="kehuishouwu" class="box-border size-32 border-4"
              @click="handleSendcode"
            >
              发送
            </wd-button>
          </view>
          <view class="">
            <view class=" ">
              <wd-button type="primary" size="large" block @click="handleSubmit">
                提交
              </wd-button>
            </view>
          </view>
        </wd-cell-group>
      </wd-form>
    </view>
  </view>
</template>

<style scoped></style>
