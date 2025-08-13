## 需求

根据 input checkbox 的勾选情况，决定卡片是否展示。

## 案例

**示例代码：**

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
    <style>
        .container {
            display: flex;
            height: 100vh;
        }
        .left {
            background: #F0F0F0;
        }
        .card {
            width: 300px;
            height: 300px;
            background: green;
            float: left;
            margin: 16px;
        }
        .hide {
            display: none;
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="left">
            <div>
                <label>Topic1
                    <input id="man-checkbox" type="checkbox" checked onchange="onChange(0, this)">
                </label>
            </div>
            <div>
                <label>Topic2
                    <input id="man-checkbox" type="checkbox" checked onchange="onChange(1, this)">
                </label>
            </div>
            <div>
                <label>Topic3
                    <input id="man-checkbox" type="checkbox" checked onchange="onChange(2, this)">
                </label>
            </div>
        </div>

        <div class="content">
            <div class="card">内容1</div>
            <div class="card">内容2</div>
            <div class="card">内容3</div>
        </div>
    </div>

    <script> 
        function onChange(index, input) {
            const cards = document.getElementsByClassName('card')
            const card = cards[index]

            if (input.checked) {
                card.classList.remove('hide')
            } else {
                card.classList.add('hide')
            }
        }
    </script>
</body>
</html>
```

**代码解释：**

- javascript 代码放在 `<script></scirpt>` 标签中（另外一种是引用 js 文件：`<scipt src="..."></script>`）。

- javascript 代码中定义了一个包含 2 个参数的函数 `onChange`，第 1 个参数 `index` ，用来确定点击的哪个checkbox；第 2 个参数是 `input`，是当前点击的 input checkbox 对象。

- `document.getElementsByClassName` API 用来从文档中获取指定了给定 class 的元素，返回的是元素的数组（因为可能有多个元素具有相同的 class）。类似的 API

  还有 `document.getElementById` ，它是根据 id 去选择元素，返回值是单个元素（HTML规范规定文档中同名的 id 只能有1个）。

- `<input onchange="onChange(xxx, this)"></input>` 代码中的 onchange 属性用来为 input 指定一个值变化的监听器，当 input 的勾选状态发生变化时，对应的代码 `onChange(xxx, this)` 会被执行。

- 由于各个 input 调用 onChange 时，传入的 index 正好与对应 card 的下标对应，因此`const card = cards[index]` 可得到点击的 checkbox 对应的 card 元素。

- `input.checked` API 可获取该 input 的勾选状态，true 表示勾选；否则是未勾选。

- element.classList API 可读取该元素的 class 属性列表。

- `classList.remove` API 表示从 class 属性列表中删除给定的 class；`classList.add` 表示从 class 属性列表中添加给定的 class。

- `.hide {display: none;}` 定义一个 hide class，将 hide class 添加给某个元素，可以让其隐藏。

## 扩展

javascript 打印 API `console.log`，用于在控制台打印数据，如：

```javascript
console.log("hello")
```

右键点击浏览器空白处，选择【检查】，可打开 Chrome 开发者工具。选择 【Console】选项卡可看到打印的日志 `hello`。点击 `hello` 右侧的代码标号，可直接跳转到对应的打印代码处。