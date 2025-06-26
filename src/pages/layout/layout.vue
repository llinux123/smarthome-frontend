<script lang="ts" setup>
import { nextTick, ref } from 'vue'
import DeviceSceneboard from './components/board/board.vue'

const active = ref<number>(1)
const scrollTop = ref<number>(0)
const subCategories = Array.from({ length: 24 }).fill({ title: '标题文字', label: '这是描述这是描述' }, 0, 24)

const board1 = ref(true)
const board2 = ref(false)
const board3 = ref(false)
// 设备与场景、数据面板、安防警报等分类

const categories = ref([
  {
    label: '设备与场景',
    title: '设备与场景',
    icon: 'thumb-up',
    items: subCategories,
    disabled: false,
  },
  {
    label: '数据面板',
    title: '数据面板',
    icon: 'thumb-up',
    items: subCategories,
    disabled: false,
  },
  {
    label: '安防警报',
    title: '安防警报',
    icon: 'thumb-up',
    items: subCategories.slice(0, 18),
    disabled: false,
  },

  {
    label: '分类七',
    title: '标题七',
    icon: 'thumb-up',
    items: subCategories,
    disabled: true,
  },
])

function handleChange({ value }) {
  active.value = value
  scrollTop.value = -1
  nextTick(() => {
    scrollTop.value = 0
  })
}
</script>

<template>
  <view id="sidebar">
    <view class="wraper">
      <wd-sidebar v-model="active" @change="handleChange">
        <wd-sidebar-item
          v-for="(item, index) in categories" :key="index" :value="index" :label="item.label"
          :icon="item.icon" :disabled="item.disabled"
        />
      </wd-sidebar>
      <view class="content" :style="`transform: translateY(-${active * 100}%)`">
        <scroll-view
          v-for="(item, index) in categories" :key="index" class="category" scroll-y
          scroll-with-animation :show-scrollbar="false" :scroll-top="scrollTop" :throttle="false"
        >
          <DeviceSceneboard v-if="board1" />
          <Databoard v-if="board2" />
          <SecurityAlarmBoard v-if="board3" />
          <!-- <wd-cell-group :title="item.title" border>
                        <wd-cell v-for="(cell, index) in item.items" :key="index" :title="cell.title"
                            :label="cell.label">
                            <wd-icon name="github-filled" size="24px"></wd-icon>
                        </wd-cell>
                    </wd-cell-group> -->
        </scroll-view>
      </view>
    </view>
  </view>
  <view />
</template>

<style lang="scss" scoped>
.wraper {
    display: flex;
    height: calc(100vh - var(--window-top));
    height: calc(100vh - var(--window-top) - constant(safe-area-inset-bottom));
    height: calc(100vh - var(--window-top) - env(safe-area-inset-bottom));
    overflow: hidden;
}

.content {
    flex: 1;
    background: #fff;
    transition: transform 0.3s ease;
}

.category {
    box-sizing: border-box;
    height: 100%;
}
</style>
