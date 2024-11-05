---
title: obsidian的编辑与格式
categories: obsidian
tags:
  - obsidian
abbrlink: 5c9e6bb5
date: 2024-11-05 22:28:13
---

# 标签

## 添加标签

要创建标签，在编辑器中输入井号 (`#`)，然后跟上主题词即可。例如，`#会议`。
也可以在`tags`属性中添加标签。此时，标签则被格式化为列表形式：

```markdown
---
tags:
  - 食谱
  - 烹饪
---
```

## 使用标签查找笔记

可以在搜索词中使用`tag`搜索符，例如`tag:#会议`进行搜索。也可以通过在笔记中点击标签来查找包含该标签的笔记。

## 嵌套标签

嵌套标签定义了标签层次结构，使查找和筛选相关标签更加容易。
通过在标签名中添加斜杠（`/`）创建嵌套标签，例如`#收件箱/待阅读`和`#收件箱/处理中`。

# 标注

要创建标注，将`[!info]`添加到引用块的第一行即可。其中`info`是_类型标识符_。类型标识符决定了标注的外观。

```markdown
> [!info]
> 这是一个标注块。
> 它支持 **Markdown**、[[Internal links|内部链接]] 和 [[Embed files|嵌入]]！> ![[Engelbart.jpg]]
```

展示的样式：
![image.png](https://gitee.com/wc2017/blog-img/raw/master/20241105/145709622-20241105145627-6e5e5.png)

## 修改标题

默认情况下，标注的标题是其类型标识符。你可以在类型标识符后添加文本来更改它：

```markdown
> [!tip] 标注可以有自定义标题
> 就像这个一样。
```

![image.png](https://gitee.com/wc2017/blog-img/raw/master/20241105/163011986-20241105163008-ee7ac.png)

## 可折叠标注

可以通过在类型标识符后添加加号（+）或减号（-）来使标注可折叠。
加号表示标注默认展开，减号表示标注收起。

```markdown
> [!faq]- 标注可以折叠吗？
> 可以！在可折叠标注中，当标注收起时，内容会被隐藏。
```

![image.png](https://gitee.com/wc2017/blog-img/raw/master/20241105/163150271-20241105163146-3a16f.png)

## 嵌套标注

```markdown
> [!question] 标注可以嵌套吗？
> > [!todo] 可以。
> > > [!example]  你甚至可以使用多层嵌套。
```

![image.png](https://gitee.com/wc2017/blog-img/raw/master/20241105/163242539-20241105163238-989cb.png)

## 自定义标注

CSS
代码片段和第三方插件可以定义自定义标注，[参照样式](https://publish.obsidian.md/help-zh/%E7%BC%96%E8%BE%91%E4%B8%8E%E6%A0%BC%E5%BC%8F%E5%8C%96/%E6%A0%87%E6%B3%A8)

## 标注支持的类型

```markdown
> [!note]
> Lorem ipsum dolor sit amet
```

```markdown
> [!Abstract]
> Lorem ipsum dolor sit amet
可以使用别名：summary，tldr 替换 Abstract
```


```markdown
> [!info]
> Lorem ipsum dolor sit amet
```

```markdown
> [!todo]
> Lorem ipsum dolor sit amet
```

```markdown
> [!tip]
> Lorem ipsum dolor sit amet
可以使用别名别名：hint，important 替换 tip
```

```markdown
> [!success]
> Lorem ipsum dolor sit amet
可以使用别名别名：check，done 替换 success
```

```markdown
> [!question]
> Lorem ipsum dolor sit amet
可以使用别名别名：help，faq替换 question
```

```markdown
> [!warning]
> Lorem ipsum dolor sit amet
可以使用别名别名：caution，attention 替换 warning
```


```markdown
> [!failure]
> Lorem ipsum dolor sit amet
可以使用别名别名：fail，missing 替换 failure
```


```markdown
> [!danger]
> Lorem ipsum dolor sit amet

可以使用别名别名：error 替换 danger
```

```markdown
> [!bug]
> Lorem ipsum dolor sit amet
```

```markdown
> [!example]
> Lorem ipsum dolor sit a
```

```markdown
> [!quote]
> Lorem ipsum dolor sit amet
```


