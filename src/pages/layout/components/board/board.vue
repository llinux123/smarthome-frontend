<script lang="ts" setup>
import deviceboard from './device/deviceboard.vue'
import sceneboard from './scene/sceneboard.vue'

const tab = ref(0)
const tabref = {
  1: '设备',
  2: '场景',
}
</script>

<template>
  <view>
    <view>
      <wd-tabs v-model="tab">
        <block v-for="item in tabref" :key="item">
          <wd-tab :title="`${item}`">
            <deviceboard v-if="item === '设备'" />
            <sceneboard v-if="item === '场景'" />
            <view v-else class="content">
              暂无内容
            </view>
          </wd-tab>
        </block>
      </wd-tabs>
    </view>
    <view />
  </view>
</template>

<style scoped>
.content {
    line-height: 120px;
    text-align: center;
}
</style>

<route lang="json5" type="home">
{
  "layout": "tabbar",
  "style": {
    "navigationStyle": "custom",
    "navigationBarTitleText": "智慧家居"
  }
}
</route>
