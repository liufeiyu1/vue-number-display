# Vue Number Display

一个基于 Vue 的数字滚动展示组件，支持自定义样式、动画效果和背景图片。适用于数据大屏、计数器、统计数据展示等场景。

## 特性

- 🎯 平滑的数字滚动动画效果
- 🎨 完全可自定义的样式（宽度、高度、颜色、字体大小等）
- 🖼️ 支持本地和网络背景图片
- 🔢 支持显示/隐藏前导零
- 📱 响应式设计，适配各种屏幕尺寸
- 🚀 轻量级，CSS自动内联到JS中，无需单独引入样式文件

## 安装

```bash
npm install vue-number-display
```

或

```bash
yarn add vue-number-display
```

## 使用方法

### 全局注册

```js
import { createApp } from 'vue';
import App from './App.vue';
import VueNumberDisplay from 'vue-number-display';

const app = createApp(App);
app.use(VueNumberDisplay);
app.mount('#app');
```

### 局部注册

```vue
<template>
  <div>
    <number-display :value="12345" />
  </div>
</template>

<script>
import { NumberDisplay } from 'vue-number-display';

export default {
  components: {
    NumberDisplay
  }
}
</script>
```

## 属性

| 属性名 | 类型 | 默认值 | 说明 |
| --- | --- | --- | --- |
| value | Number/String | - | 要显示的数字（必填） |
| minLength | Number | 6 | 最小显示位数 |
| hasZeroPrefix | Boolean | false | 是否显示前导零，true时不足位数会在前面补0，false时直接显示数字 |
| title | String | '' | 标题文本 |
| digitWidth | Number/String | 40 | 数字容器宽度 |
| digitHeight | Number/String | 54 | 数字容器高度 |
| fontSize | Number/String | 30 | 数字字体大小 |
| titleFontSize | Number/String | 16 | 标题字体大小 |
| textColor | String | 'linear-gradient(to bottom, #FFFFFF, #7FC4FC)' | 数字颜色，支持渐变色 |
| titleColor | String | 'white' | 标题颜色 |
| showBackground | Boolean | true | 是否显示背景图片 |
| backgroundImage | String | 内置图片 | 普通数字背景图片（支持本地和网络图片） |
| zeroBackgroundImage | String | 内置图片 | 前导零的背景图片（支持本地和网络图片） |
| digitSpacing | Number/String | 2 | 数字间距 |
| animationDuration | Number | 800 | 动画持续时间（毫秒） |

## 示例

### 基础用法

```vue
<template>
  <number-display :value="12345" />
</template>
```

### 显示前导零

```vue
<template>
  <number-display 
    :value="123" 
    :min-length="8"
    :has-zero-prefix="true"
    title="总数"
  />
</template>
```

### 前导零与非前导零使用不同背景

```vue
<template>
  <number-display 
    :value="102030" 
    :min-length="8"
    :has-zero-prefix="true"
    background-image="path/to/normal-bg.png"
    zero-background-image="path/to/zero-bg.png"
  />
</template>

<script>
import { NumberDisplay } from 'vue-number-display';

export default {
  components: {
    NumberDisplay
  }
}
</script>
```

### 使用网络图片

```vue
<template>
  <number-display 
    :value="12345" 
    background-image="https://example.com/background.png"
    zero-background-image="https://example.com/zero-background.png"
  />
</template>
```

### 动态数据展示

```vue
<template>
  <div>
    <number-display :value="count" title="访问量" />
    <button @click="increment">增加数值</button>
  </div>
</template>

<script>
import { ref } from 'vue';
import { NumberDisplay } from 'vue-number-display';

export default {
  components: {
    NumberDisplay
  },
  setup() {
    const count = ref(10000);
    
    const increment = () => {
      count.value += Math.floor(Math.random() * 1000);
    };
    
    return {
      count,
      increment
    };
  }
}
</script>
```

### 多组数据展示

```vue
<template>
  <div class="dashboard">
    <number-display :value="visitors" title="访问量" text-color="#42b883" />
    <number-display :value="orders" title="订单数" text-color="#ff7e67" />
    <number-display :value="revenue" title="收入" text-color="#ffcb77" />
  </div>
</template>

<script>
import { ref } from 'vue';
import { NumberDisplay } from 'vue-number-display';

export default {
  components: {
    NumberDisplay
  },
  setup() {
    const visitors = ref(12345);
    const orders = ref(678);
    const revenue = ref(98765);
    
    return {
      visitors,
      orders,
      revenue
    };
  }
}
</script>

<style>
.dashboard {
  display: flex;
  gap: 20px;
  justify-content: center;
}
</style>
```

## 背景图片规则

- 当 `hasZeroPrefix` 设为 `true` 时，前导零（数字开头的零）使用 `zeroBackgroundImage`
- 其他所有数字（包括非前导的0）使用 `backgroundImage`
- 支持三种类型的图片：
  1. 本地导入的图片对象：`import bg from './assets/bg.png'`
  2. 网络图片URL：`https://example.com/image.jpg`
  3. 数据URL：`data:image/png;base64,...`

### 使用网络图片的注意事项

如果使用网络图片，请确保：
1. 图片URL是完整的（包含http或https前缀）
2. 图片服务器允许跨域访问（CORS）
3. 图片链接是稳定的，避免使用临时链接

示例：
```vue
<template>
  <number-display 
    :value="12345" 
    background-image="https://img.58tg.com/up/allimg/sj03/240301125515H09-0-lp.jpg"
  />
</template>
```

## 应用场景

- 数据大屏展示
- 实时统计数据
- 倒计时/正计时
- 金额/数量展示
- 游戏分数计数器
- 网站访问量统计

## 浏览器兼容性

- 支持所有现代浏览器
- Chrome、Firefox、Safari、Edge最新版本
- 不支持IE浏览器

## 常见问题

### hasZeroPrefix属性有什么作用？

`hasZeroPrefix` 属性用于控制是否显示前导零：

- 当设置为 `true` 时，数字不足 `minLength` 位数时，会在前面自动补零
- 当设置为 `false` 时，直接显示原始数字，不会补零

例如，当 `minLength` 为 8 时：
```vue
<!-- 显示为"00000123" -->
<number-display :value="123" :min-length="8" :has-zero-prefix="true" />

<!-- 显示为"123" -->
<number-display :value="123" :min-length="8" :has-zero-prefix="false" />
```

### 前导零和非前导零有什么区别？

在数字中，前导零是指数字开头的零，例如"00123"中的前两个"0"。非前导零是指数字中间的零，例如"10203"中的"0"。

当设置 `hasZeroPrefix` 为 `true` 时：
- 前导零使用 `zeroBackgroundImage` 作为背景
- 非前导零（包括数字中间的"0"）使用 `backgroundImage` 作为背景

例如：
```vue
<!-- 数字"00102030"中，前两位"00"使用zeroBackgroundImage，其他位（包括中间的"0"）使用backgroundImage -->
<number-display 
  :value="102030" 
  :min-length="8" 
  :has-zero-prefix="true"
  background-image="normal-bg.png"
  zero-background-image="zero-bg.png"
/>
```

### 如何修改数字颜色？

可以通过`textColor`属性设置数字颜色，支持普通颜色和渐变色：

```vue
<!-- 普通颜色 -->
<number-display :value="12345" text-color="#ff5733" />

<!-- 渐变色 -->
<number-display :value="12345" text-color="linear-gradient(to bottom, #ff5733, #c70039)" />
```

### 如何隐藏背景图片？

设置`showBackground`属性为`false`即可隐藏背景图片：

```vue
<number-display :value="12345" :show-background="false" />
```

### 如何调整动画速度？

通过`animationDuration`属性设置动画持续时间（毫秒）：

```vue
<!-- 快速动画 -->
<number-display :value="12345" :animation-duration="300" />

<!-- 慢速动画 -->
<number-display :value="12345" :animation-duration="1500" />
```

### 网络图片不显示怎么办？

如果网络图片不显示，可能有以下原因：
1. 图片URL不正确或图片已失效
2. 图片服务器不允许跨域访问
3. 网络连接问题

解决方法：
- 检查图片URL是否正确且可访问
- 使用允许跨域的图片服务
- 考虑将图片下载到本地，通过import方式使用

## 许可证

MIT