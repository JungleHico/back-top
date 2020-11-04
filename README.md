# BackTop 回到顶部按钮

## 组件使用
```html
<template>
    <div>
        <back-top></back-top>
    </div>
</template>

<script>
import BackTop from './BackTop'

export default {
    components: {
        BackTop
    },
    data() {
        return {

        }
    }
}
</script>
```

## API

参数

| 参数 | 说明 | 类型 | 默认值 |
| - | - | - | - |
| width | 按钮宽度 | `Number` | 64 |
| height | 按钮高度 | `Number` | 64 |
| offsetX | 水平方向位置，默认为距右边距离 | `Number` | 50 |
| offsetY | 垂直方向位置，默认为距底部距离 | `Number` | 50 |
| circle | 按钮是否为圆形，使用 `slot` 后不生效 | `Boolean` | true |
| delay | 回到顶部动画时间，为 0 时无动画 | `Number` | 250 |

slot

| 名称 | 说明 |
| - | - |
| 默认/无 | 自定义按钮的内容 |

## 兼容性

兼容IE10及以上版本的浏览器，使用 `slot` 自定义按钮可以兼容IE9。
