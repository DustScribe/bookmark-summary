Title: Maple Mono

URL Source: https://font.subf.dev/zh-cn/

Markdown Content:
Smooth your coding flow

我们用代码将创意构筑成产品，而字体如同旅途中沉默的基石，熟视无睹，却塑造着每天编码的体验。Maple Mono 专为极客匠心打造，它以一种内敛的优雅，提升您的工作效率，让您在阅读和编写每一行代码时都能感受到丝滑和愉悦。

为什么再做一个字体？
----------

市面上有这么多优秀的等宽字体，经由专业的设计师设计，看起来整洁美观。但是，当我真正把它们作为主要字体用来写代码时，我发现其中很多的字体总有一些地方让我不太满意，例如：

*   _JetBrains Mono_ 虽然字形设计精炼、排版整齐划一，但是风格有些死板
*   _Fira Code_ 虽然有丰富的连字，但是缺少斜体，自动生成的的斜体角度过大
*   _Victor Mono_ 虽然具有手写风格的斜体，但是其稍显夸张的风格让我有些难以接受
*   _Sarasa Gothic_ 虽然中英文2:1等宽，但是英文部分过于狭窄，阅读体验不太好
*   很少有等宽字体设计有圆角
*   很少有等宽字体对 Nerd-Font 和 中文 优先支持

因此，我制作了这一款 字形整洁、拥有手写风格的斜体、细粒度配置、内置 Nerd-Font、中英文2:1等宽 的字体，用于提升自己的工作效率，希望它也能对其他人有所帮助。

特性
--

一款字体，无限字重
---------

可变字体支持，随心所欲获取想要的字重。

独特字形，流畅设计
---------

圆角设计，全新的字形设计，手写体风格的斜体样式。

智能连字，数量丰富
---------

大量智能连字，纯文本标签，连接字母，将字体能力提升到新的水平。

<\>a??b!==c...d|-\>

<!--e++f!!g~\>h</\>

<\=i###j:=k<\==\>l|\>

### Special Ligatures

\[DEBUG\] \[INFO\] \[WARN\] \[ERROR\]

\[TODO\] todo)) \[FIXME\] fIxMe))

从纯文本创建标签，可用于日志显示和任务提醒。

精美图标，拥抱现代
---------

一流的 Nerd-Font 支持，用图标装饰你的现代化终端。

![Image 1: Nerd-Font showcase image](https://font.subf.dev/_astro/zsh.BuXnmYOa_ZpJrFy.webp)

你的喜好，你的字体
---------

```
{
  "$schema": "./source/schema.json",
  "family_name": "Maple Mono",
  "use_hinted": true,
  "pool_size": 4,
  "ligature": true,
  "feature_freeze": {
    // ...
  }
}
```

随心配置或强制开关 OpenType 功能，创建你完美的字体。

[查看指南](https://github.com/subframe7536/maple-font/blob/variable/README_CN.md#%E8%87%AA%E5%AE%9A%E4%B9%89%E6%9E%84%E5%BB%BA)

对比
--

了解 Maple Mono 与其他流行的编程字体的对比。

预览
--

看看字体在真实的代码片段中的效果。

TypeScript JSX

```
function Counter() {
  const [count, setCount] = createSignal(1);
  const inc = () =>
    setCount(count => count + 1);

  return (
    <button type="button" onClick={inc}>
      {count()}
    </button>
  );
}
```

Vue

```
<script setup>
import { ref, computed } from 'vue'

const count = ref(0)
const dbl = computed(() => count.value * 2)
</script>

<template>
  {{ dbl }}
  <button @click="count++">Count</button>
</template>
```

Java

```
@SpringBootApplication
public class TodoApplication {

    public static void main(String[] args) {
        SpringApplication.run(TodoApplication.class, args);

        Arrays.asList("foo", "bar", "baz")
          .stream()
          .map(String::toUpperCase)
          .forEach(System.out::println)
    }

}
```

Go

```
func main() {
    http.HandleFunc("/", func(writer http.ResponseWriter, request *http.Request) {
        message := strings.Join([]string{"Hello", "world!"}, " ")
        _, err := writer.Write([]byte(message))
        if err != nil {
            panic(err)
        }
    })

    if err := http.ListenAndServe(":8080", nil); err != nil {
        panic(err)
    }
}
```

Python

```
def merge(x1, x2):
    if isinstance(x1, dict) and isinstance(x2, dict):
        res = x1.copy()
        for k, v in x2.items():
            res[k] = merge(res[k], v) if k in res else v
        return res
    elif isinstance(x1, list) and isinstance(x2, list):
        res = list(x1)
        res.extend(x2)
        return res
    elif x1 == x2:
        return x1
    else:
        raise ValueError(f"Cannot merge '{x1!r}' and '{x2!r}'")


if __main__ == "main":
    merge(0x23, 0xa1)        
```

C++

```
void quicksort(auto begin, auto end) {
    if (begin != end) {
        Comparable auto pivot = *std::next(begin, n:std::distance(begin, end) / 2);
        const auto [lt, gt] = ::partition(begin, end, pivot, pred:std::less<>());
        quicksort(begin, lt);
        quicksort(gt, end);
    }
}

int main() {
    std::vector<int> Vec{5, 0, 1, 5, 3, 7, 4, 2};
    quicksort(Vec.begin(), Vec.end());
    std::for_each(
        Vec.begin(),
        Vec.end(),
        f:[](const int Elem) {std::cout << Elem << " "; }
    );
}
```

用户评价
----

加入成千上万喜爱上 Maple Mono 的开发者行列。

> ┏需要一款带点个性的🌟和优秀的斜体的字体。@subframe7536 的 Maple Mono NF 是我的新宠编程字体。正是我在厌倦 JetBrains Mono 后一直在寻找的字体。它从 JBM 和其他优秀的字体中汲取了灵感。┛

> ┏使用 Maple Mono 已经一个月了。Nerd Font 支持非常棒，并且能够自定义字体功能正是我所需要的。干得漂亮！┛

> ┏换了 Maple Mono 字体，部分内容开了斜体连笔，感觉在清晰好用的基础上又多了几分灵动😄不错┛

> ┏对于希望字体圆一些、“可爱”一些的人，Maple Mono 可能是一个很好的选择。它封装了 CJK 字体，且保证 2:1 的宽度。前后大概有两三个同事夸过我编辑器和终端配得很好看。┛

> ┏我喜欢 Maple Mono，因为它非常像我的笔迹。我写字时混合了印刷体和手写体，所以感觉就像在看我的笔迹。而且用手写体的风格而不是更单调的印刷体来查看代码也让人非常愉悦。┛

鸣谢
--

Maple Mono 站在巨人的肩膀上。
