<template>
  <page-wraper>
    <wd-toast></wd-toast>
    <demo-block hor="0" title="基础用法" transparent>
      <wd-tabbar bordered @change="handleChange">
        <wd-tabbar-item title="首页" icon="home"></wd-tabbar-item>
        <wd-tabbar-item title="分类" icon="cart"></wd-tabbar-item>
        <wd-tabbar-item title="我的" icon="user"></wd-tabbar-item>
      </wd-tabbar>
    </demo-block>

    <demo-block hor="0" title="通过名称匹配" transparent>
      <wd-tabbar bordered @change="handleChange" v-model="tabbar1">
        <wd-tabbar-item name="home" title="首页" icon="home"></wd-tabbar-item>
        <wd-tabbar-item name="cart" title="分类" icon="cart"></wd-tabbar-item>
        <wd-tabbar-item name="setting" title="设置" icon="setting"></wd-tabbar-item>
        <wd-tabbar-item name="user" title="我的" icon="user"></wd-tabbar-item>
      </wd-tabbar>
    </demo-block>

    <demo-block hor="0" title="徽标提示" transparent>
      <wd-tabbar v-model="tabbar5" @change="handleChange">
        <wd-tabbar-item name="1" is-dot :value="2" title="点状" icon="home"></wd-tabbar-item>
        <wd-tabbar-item name="2" :value="2" icon="cart" title="分类"></wd-tabbar-item>
        <wd-tabbar-item name="3" :value="30" title="我的" icon="user"></wd-tabbar-item>
        <wd-tabbar-item name="4" :value="200" title="最大值" icon="user"></wd-tabbar-item>
      </wd-tabbar>
    </demo-block>
    <demo-block hor="0" title="悬浮标签栏" transparent>
      <wd-tabbar shape="round" v-model="tabbar2" @change="handleChange">
        <wd-tabbar-item name="1" title="首页" is-dot :value="2" icon="home"></wd-tabbar-item>
        <wd-tabbar-item name="2" title="分类" :value="2" icon="cart"></wd-tabbar-item>
        <wd-tabbar-item name="3" title="相册" :value="30" icon="photo"></wd-tabbar-item>
        <wd-tabbar-item name="4" title="我的" :value="200" icon="user"></wd-tabbar-item>
      </wd-tabbar>
    </demo-block>

    <demo-block hor="0" title="自定义图标" transparent>
      <wd-tabbar v-model="tabbar4" @change="handleChange">
        <wd-tabbar-item name="1" :value="2" title="首页" icon="home"></wd-tabbar-item>
        <wd-tabbar-item name="2" :value="2" icon="cart" title="分类">
          <template #icon>
            <wd-img round height="40rpx" width="40rpx" src="https://img.yzcdn.cn/vant/cat.jpeg"></wd-img>
          </template>
        </wd-tabbar-item>
        <wd-tabbar-item name="3" :value="3" title="我的" icon="user"></wd-tabbar-item>
      </wd-tabbar>
    </demo-block>

    <demo-block hor="0" title="自定义颜色" transparent>
      <wd-tabbar v-model="tabbar5" @change="handleChange" active-color="#ee0a24" inactive-color="#7d7e80">
        <wd-tabbar-item name="1" is-dot :value="2" title="点状" icon="home"></wd-tabbar-item>
        <wd-tabbar-item name="2" :value="2" icon="cart" title="分类"></wd-tabbar-item>
        <wd-tabbar-item name="3" :value="30" title="我的" icon="user"></wd-tabbar-item>
        <wd-tabbar-item name="4" :value="200" title="最大值" icon="photo"></wd-tabbar-item>
        <wd-tabbar-item name="5" :value="10" title="客服" icon="chat"></wd-tabbar-item>
      </wd-tabbar>
    </demo-block>
    <demo-block hor="0" title="监听切换事件" transparent>
      <wd-tabbar v-model="tabbar6" @change="handleChange1" active-color="#ee0a24" inactive-color="#7d7e80">
        <wd-tabbar-item name="1" title="首页" icon="home"></wd-tabbar-item>
        <wd-tabbar-item name="2" title="分类" icon="cart"></wd-tabbar-item>
        <wd-tabbar-item name="3" title="我的" icon="user"></wd-tabbar-item>
        <wd-tabbar-item name="4" title="相册" icon="photo"></wd-tabbar-item>
        <wd-tabbar-item name="5" title="客服" icon="chat"></wd-tabbar-item>
      </wd-tabbar>
    </demo-block>

    <demo-block hor="0" title="固定底部" transparent>
      <wd-tabbar fixed v-model="tabbar3" @change="handleChange" bordered safeAreaInsetBottom placeholder>
        <wd-tabbar-item name="1" :value="2" is-dot title="首页" icon="home"></wd-tabbar-item>
        <wd-tabbar-item name="2" title="分类" icon="cart"></wd-tabbar-item>
        <wd-tabbar-item name="3" title="我的" icon="user"></wd-tabbar-item>
        <wd-tabbar-item name="4" :value="200" title="相册" icon="photo"></wd-tabbar-item>
        <wd-tabbar-item name="5" :value="10" title="客服" icon="chat"></wd-tabbar-item>
      </wd-tabbar>
    </demo-block>
  </page-wraper>
</template>
<script lang="ts" setup>
import { useToast } from '@/uni_modules/wot-design-uni'
import { ref } from 'vue'
const { show } = useToast()
const tabbar1 = ref('home')
const tabbar2 = ref('2')
const tabbar3 = ref('2')
const tabbar4 = ref('1')
const tabbar5 = ref('1')
const tabbar6 = ref('1')

function handleChange(event: any) {
  console.log(event)
}

function handleChange1({ value }: { value: string }) {
  show(`选中标签:${value}`)
}
</script>
<style lang="scss" scoped>
:deep(.page-wraper) {
  background: #f6f6f6;
}
</style>
