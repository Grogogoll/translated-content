---
title: <input type="color">
slug: Web/HTML/Element/Input/color
---

**`<input type="color">`元素**是{{HTMLElement("input")}}元素中的一个特定种类，用来创建一个允许用户使用颜色选择器，或输入兼容 CSS 语法的颜色代码的区域。（不支持 Alpha 通道）

此元素的外观会因浏览器不同而不同，可能是简单的验证颜色输入格式的文本框，也可能使用平台原生或自定义样式的颜色选择器。其 UI 除要能接收文本格式的颜色外，未要求其他特性。（[更多信息](https://www.w3.org/TR/html5/forms.html#color-state-%28type=color%29)）

<table class="properties">
 <tbody>
  <tr>
   <th scope="row"><a href="/zh-CN/docs/Web/Guide/HTML/Content_categories">内容分类</a></th>
   <td><a href="/zh-CN/docs/Web/Guide/HTML/Content_categories#Flow_content">流动区域</a>, <a href="/zh-CN/docs/Web/Guide/HTML/Content_categories#Form_listed">列表</a>, <a href="/zh-CN/docs/Web/Guide/HTML/Content_categories#Form_submittable">可提交</a>, <a href="/zh-CN/docs/Web/Guide/HTML/Content_categories#Form_resettable">可重置</a>, <a href="/zh-CN/docs/Web/Guide/HTML/Content_categories#Form-associated_content">表单相关元素</a>, <a href="/zh-CN/docs/Web/Guide/HTML/Content_categories#Phrasing_content">短语内容</a>, 可标记元素，可触摸元素。</td>
  </tr>
  <tr>
   <th scope="row">允许的内容</th>
   <td>无，这是一个 {{Glossary("empty element")}}。</td>
  </tr>
  <tr>
   <th scope="row">标签省略</th>
   <td>必须有开始标签，必须没有结束标签。</td>
  </tr>
  <tr>
   <th scope="row">允许的父级元素</th>
   <td>任何接受<a href="/zh-CN/docs/Web/Guide/HTML/Content_categories#Phrasing_content">短语内容</a>的元素。</td>
  </tr>
  <tr>
   <th scope="row">DOM 接口</th>
   <td>{{domxref("HTMLInputElement")}}</td>
  </tr>
 </tbody>
</table>

## 属性

该元素具有下面属性及其他的[全局属性](/zh-CN/docs/Web/HTML/Global_attributes)。

- {{htmlattrdef("autocomplete")}}
  - : 设置颜色区域的 autocomplete 值。如果为 true，则将自动填充颜色选择器上次存储的值。
- {{htmlattrdef("autofocus")}}
  - : 此布尔值属性使你可以指定当页面加载时，表单区域是否应当获得输入焦点。除非用户的操作覆盖这个属性，例如：在其他区域内进行输入。在整个文档中，只有一个元素可以拥有**autofocus**属性，值为布尔值。
- {{htmlattrdef("disabled")}}
  - : 此布尔值标明颜色选择其是否不可用于交互。另外，disabled 时的值不会随表单提交。
- {{htmlattrdef("name")}}
  - : 随表单一起提交的颜色选择器的 name。
- {{htmlattrdef("value")}}
  - : 颜色选择器的 value，指定颜色选择器默认选择的颜色。input 的 value 值必须是长度为 7 的字符串，以#开始，包含 16 进制格式的颜色值。例如：#FF0000 为红色的 16 进制值。

## 使用

`"color"`类型的输入内容比较简单。

```html
<input type="color" />
```

### 默认值

你可以给上面的例子添加一个默认值，对元素本身和选色器都生效。

```html
<input type="color" value="#ff0000" />
```

上述代码会创建一个默认选择红色的颜色选择器。

{{EmbedLiveSample("Providing_a_default_color", 700, 30)}}

下面的图片展示了 macOS 平台 Chrome 浏览器的颜色选择器：

![This is how an input type color looks on Mac and within Chrome](https://mdn.mozillademos.org/files/12311/Input_Type_Color_sample.png)

如果你没有手动指定的话，元素的默认值为`"#000000"`，即黑色。输入必须为 7 个字符，以"#"符号开始，后跟代表红、绿、蓝的十六进制字符各 2 个，形如`"#rrggbb"`。如果你想输入的颜色是其他格式（比如 CSS 中的`rgb()`或`rgba()`记法），在设定`value`值时必须将其转换为这种格式。

### 监听颜色变化

正如其他类型的{{HTMLElement("input")}}元素，有两个和值的改变相关的事件，{{event("input")}}和{{event("change")}}：

- 每次颜色变更都会触发元素上的`input`事件。
- 用户关闭选色器之后会触发`change`事件。

对于这两个事件，都可以通过{{domxref("HTMLInputElement.value", "value")}}属性获取新值。

```js
colorPicker.addEventListener("input", updateFirst, false);
colorPicker.addEventListener("change", watchColorPicker, false);

function watchColorPicker(event) {
  document.querySelectorAll("p").forEach(function(p) {
    p.style.color = event.target.value;
  });
}
```

### 选取值

如果浏览器的实现不支持为`"color"`类型的{{HTMLElement("input")}}元素提供选色器而只有一个文本框，可以使用{{domxref("HTMLInputElement.select", "select()")}}方法选取输入内容。如果浏览器提供了选色器，`select()`方法将会什么也不做。因此，需要留心这两种情况下方法行为的差异。

```js
colorWell.select();
```

### 实现差异

如上文所说，如果浏览器不提供选色器，此元素将会显示为一个具备输入验证功能的文本框。例如，在 Safari 10.1 中，你将会看到以下内容：

![Screenshot of the example taken in Safari.](https://mdn.mozillademos.org/files/14899/input-color-safari.png)

而相同的内容在 Firefox 55 下则会显示成：

![Screenshot of the example taken in Firefox 55 for macOS](https://mdn.mozillademos.org/files/14901/input-color-firefox.png)

如果点击元素，则会弹出选色器，在此例中，为 macOS 平台的选色器。

![Screenshot of the element with the color picker open in Firefox Mac.](https://mdn.mozillademos.org/files/14903/input-with-picker-firefox-mac.png)

## 验证

如果当前的{{Glossary("user agent")}}下，用户输入无法转换为 7 个字符的十六进制 RGB 形式，会被判定为非法输入。在这种情况下，{{cssxref(":invalid")}}伪类会生效。

## 规范

{{Specifications}}

## 浏览器兼容性

{{Compat}}
