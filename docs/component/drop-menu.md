<frame/>

# DropMenu 下拉菜单

## 代码演示

## 基础用法

基础用法需要绑定 `v-model` 值以及 `options` 属性。

`options` 属性是一个一维对象数组，数组项的数据结构为：label（选项文本），value（选项值），tip（选项说明）。

因为`uni-app`组件无法监听点击自己以外的地方，为了在点击页面其他地方时，可以自动关闭 `dropmenu` ，建议引入组件库的 `clickOut` 函数（会关闭所有 dropmenu、popover、toast、swipeAction），在页面的根元素上监听点击事件的冒泡。

:::warning
如果存在用户手动点击 `dropmenu` 以外某个地方如按钮弹出 `dropmenu` 的场景，则需要在点击的元素（在这里上按钮）加上 @click 阻止事件冒泡到根元素上，避免触发 `clickOut` 把要手动打开的 `dropmenu` 关闭了。
:::

```html
<view @click="clickoutside">
  <wd-drop-menu>
    <wd-drop-menu-item v-model="value1" :options="option1" @change="handleChange1" />
    <wd-drop-menu-item v-model="value2" :options="option2" @change="handleChange2" />
  </wd-drop-menu>
</view>
```

```typescript
import { clickOut } from '@/uni_modules/wot-design-uni'

function clickoutside() {
  clickOut.closeOutside()
}
const value1 = ref<number>(0)
const value2 = ref<number>(0)

const option1 = ref<Record<string, any>>([
  { label: '全部商品', value: 0 },
  { label: '新款商品', value: 1 },
  { label: '活动商品', value: 2 }
])
const option2 = ref<Record<string, any>>([
  { label: '综合', value: 0 },
  { label: '销量', value: 1 },
  { label: '上架时间', value: 2 }
])

function handleChange1({ value }) {
  console.log(value)
}
function handleChange2({ value }) {
  console.log(value)
}
```

## 自定义菜单内容

通过插槽 `default` 可以自定义 `DropMenuItem` 的内容，此时需要使用实例上的 `close` 方法手动控制菜单的关闭。

可以通过 `title` 设置菜单标题。

> 这时候不要传入 options 和 value

```html
<wd-drop-menu>
  <wd-drop-menu-item v-model="value" :options="option" @change="handleChange" />
  <wd-drop-menu-item title="筛选" ref="dropMenu">
    <view>
      <wd-cell title="标题文字" value="内容" />
      <wd-cell title="标题文字" label="描述信息" value="内容" />
      <wd-button block size="large" suck @click="confirm">主要按钮</wd-button>
    </view>
  </wd-drop-menu-item>
</wd-drop-menu>
```

```typescript
const dropMenu = ref()


const value = ref<number>(0)
const option = ref<Record<string, any>>([
  { label: '全部商品', value: 0 },
  { label: '新款商品', value: 1 },
  { label: '活动商品', value: 2 }
])
function handleChange({ value }) {
  console.log(value)
}

function confirm() {
  dropMenu.value.close()
}

```

## 自定义菜单选项

自己通过 flex 布局做自定义筛选展示。

```html
<view style="display: flex; background: #fff; text-align: center;">
  <wd-drop-menu style="flex: 1; min-width: 0;">
    <wd-drop-menu-item  v-model="value1" :options="option" @change="handleChange1" />
  </wd-drop-menu>
  <view style="flex: 1;">
    <wd-sort-button v-model="value2" title="上架时间" @change="handleChange2" />
  </view>
</view>
```

## 向上展开

将 `direction` 属性值设置为 `up`，菜单即可向上展开

```html
<wd-drop-menu direction="up">
  <wd-drop-menu-item v-model="value1" :options="option1" @change="handleChange1" />
  <wd-drop-menu-item v-model="value2" :options="option2" @change="handleChange2" />
</wd-drop-menu>
```

## 禁用菜单

```html
<wd-drop-menu>
  <wd-drop-menu-item v-model="value1" disabled :options="option2" @change="handleChange1" />
  <wd-drop-menu-item v-model="value2" :options="option1" @change="handleChange2" />
</wd-drop-menu>
```

## DropMenu Attributes

| 参数                 | 说明                                 | 类型    | 可选值    | 默认值 | 最低版本 |
| -------------------- | ------------------------------------ | ------- | --------- | ------ | -------- |
| direction            | 菜单展开方向，可选值为`up` 或 `down` | string  | up / down | down   | -        |
| modal                | 是否展示蒙层                         | boolean | -         | true   | -        |
| close-on-click-modal | 是否点击蒙层时关闭                   | boolean | -         | true   | -        |
| duration             | 菜单展开收起动画时间，单位 ms        | number  | -         | 200    | -        |

## DropMenuItem Attributes

| 参数      | 说明                                                                   | 类型            | 可选值 | 默认值 | 最低版本 |
| --------- | ---------------------------------------------------------------------- | --------------- | ------ | ------ | -------- |
| v-model     | 当前选中项对应选中的 value                                             | string / number | -      | -      | -        |
| disabled  | 禁用菜单                                                               | boolean         | -      | false  | -        |
| options   | 列表数据，对应数据结构 `[{text: '标题', value: '0', tip: '提示文字'}]` | array           | -      | -      | -        |
| icon-name | 选中的图标名称(可选名称在 wd-icon 组件中)                              | string          | -      | check  | -        |
| title     | 菜单标题                                                               | string          | -      | -      | -        |
| value-key | 选项对象中，value 对应的 key                                           | string          | -      | value  | -        |
| label-key | 选项对象中，展示的文本对应的 key                                       | string          | -      | label  | -        |
| tip-key   | 选项对象中，选项说明对应的 key                                         | string          | -      | tip    | -        |

## DropdownItem Events

| 方法名      | 说明             | 参数                                                                          | 最低版本 |
| ----------- | ---------------- | ----------------------------------------------------------------------------- | -------- |
| change | 绑定值变化时触发 | event.detail = { value, selectedItem }, value 为选中值，selectedItem 为选中项 | -        |
| close  | 关闭菜单         | -                                                                             | -        |
| open   | 展开菜单         | -                                                                             | -        |

## DropdownItem Methods

通过 `this.selectComponent('#selector')` 可以获取到 DropdownItem 实例并调用实例方法

| 方法名 | 说明     | 参数 | 返回值 | 最低版本 |
| ------ | -------- | ---- | ------ | -------- |
| close  | 关闭菜单 | -    | -      | -        |
| open   | 展开菜单 | -    | -      | -        |

## DropMenu Slot

| name    | 说明     | 最低版本 |
| ------- | -------- | -------- |
| default | 菜单内容 | -        |

## DropMenuItem Slot

| name    | 说明               | 最低版本 |
| ------- | ------------------ | -------- |
| default | 菜单自定义内部内容 | -        |

## DropMenu 外部样式类

| 类名         | 说明                | 最低版本 |
| ------------ | ------------------- | -------- |
| custom-class | DropMenu 根节点样式 | -        |

## DropMenuItem 外部样式类

| 类名         | 说明                        | 最低版本 |
| ------------ | --------------------------- | -------- |
| custom-class | DropMenuItem 根节点样式     | -        |
| custom-title | DropMenuItem 左侧文字样式   | -        |
| custom-icon  | DropMenuItem 右侧 icon 样式 | -        |
