# EM 还是 REM

使用 `em` 和 `rem` 这种相对长度单位对页面进行排版是 Web 开发中的最佳实践，根据设备尺寸缩放显示元素的大小，这就使得组件在不同设备上都能达到最佳的显示效果成为可能。

* [EM](#em)
* [REM](#rem)
* [EM 还是 REM](#em-还是-rem)

## EM

`em` 是相对长度单位，它相对于当前元素的字体尺寸，即 `font-size` 。举例来说，如果当前元素的字体是 20px ，那么当前元素中的 `1em` 就等于 20px 。

```css
h1 {
    font-size: 20px; /* 1em = 20px */
}

p {
    font-size: 16px; /* 1em = 16px */
}
```

如果当前元素没有指定字体大小，就需要根据其父元素的字体大小，来计算当前元素的字体大小。如果父元素是 `<html>` ，且 `<html>` 元素的字体大小是 16px ，就可以计算出当前元素的字体大小是 32px 。

```css
h1 {
    font-size: 2em; /* 2em = 32px */
}
```

`em` 还能用来指定除字体大小意外的其它属性，像 `margin` 或 `padding` 等属性都可以用 `em` 来表示。

```css
h1 {
    font-size: 2em; /* 2em = 32px */
    margin-bottom: 1em; /* 1em = 32px */
}

p {
    font-size: 1em; /* 1em = 16px */
    margin-bottom: 1em; /* 1em = 16px */
}
```

## REM

`rem` 是相对于根元素的长度单位，这里根元素就是 `<html>` ，这意味着任何元素的 `1rem` 总是等于 `<html>` 中定义的字体大小。

```css
h1 {
    font-size: 2rem; /* 2rem = 32px */
    margin-bottom: 1rem; /* 1rem = 16px */
}

p {
    font-size: 1rem; /* 1rem = 16px */
    margin-bottom: 1rem; /* 1rem = 16px */
}
```

## EM 还是 REM

在项目开发中究竟是选用 `rem` 还是 `em` 一直以来争议不断，一些开发人员不使用 `rem` ，因为 `rem` 使组件不那么模块化；而另一些开发人员喜欢 `rem` 的简单性，即使用 `rem` 处理所有元素。

那么，在实际项目开发中，究竟是该使用 `em` 还是 `rem` 呢？答案是应该结合使用两者，利用各自的优势，从而实现较好代码质量和显示效果。当属性值的大小需要根据当前元素的字体大小缩放时，就使用 `em` ，其它的情况都使用更简单的 `rem` 。
