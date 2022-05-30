# Vue sass 获取 data 中的值

------

### 场景：使用 uview 框架时，需要动态改变元素的字体颜色

```html
<!-- template -->
<u-cell
  :title="`列表长度-${index + 1}`"
  :style="cssVars"
  icon="file-text"
  :isLink="true"
   :value="33"
/>
```

```js
// js
computed:{
  cssVars() {
    return {
      "--color": this.color
    };
  },
}
```

```css
<style lang="scss" scoped>
::v-deep .uicon-arrow-right > span {
  color: var(--color);
}
</style>
```