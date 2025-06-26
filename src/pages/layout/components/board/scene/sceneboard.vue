<script lang="ts" setup>
const value = ref('item1')
</script>

<template>
  <wd-collapse v-model="value">
    <wd-collapse-item title="标签1" name="item1">
      这是一条简单的示例文字。
    </wd-collapse-item>
    <wd-collapse-item title="标签2" name="item2">
      这是一条简单的示例文字。
    </wd-collapse-item>
    <wd-collapse-item name="item3">
      <template #title="{ expanded }">
        <view class="header">
          <text style="color: red">
            通过 slot 自定义标题
          </text>
          <text>{{ expanded ? '我展开了' : '我已收起' }}</text>
        </view>
      </template>
      这是一条简单的示例文字。
    </wd-collapse-item>
  </wd-collapse>
</template>
