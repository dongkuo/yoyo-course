## 需求

实现卡片轮播效果。

## 案例

**示例代码：**

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>滑动固定问题</title>
    <style>
        html,
        body {
            margin: 0;
            padding: 0;
        }

        .container {
            display: flex;
            width: 100%;
            height: 100vh;
            overflow: hidden;
        }

        .left-wrapper {
            width: 300px;
            background: #f0f0f0;
        }

        .right-wrapper {
            flex: 1;
            overflow: auto;
        }

        .topic-box {
            list-style-type: none;
            margin: 0;
            padding: 10px;
        }

        .topic {
            margin: 10px 0;
        }

        .card-box {
            display: flex;
            gap: 10px;
        }

        .card-scroll-container {
            flex: 1;
            display: flex;
            overflow: hidden;
            position: relative;
        }

        .card-scroll-wrapper {
            display: flex;
            gap: 10px;
            transition: transform 0.3s ease;
            /* transform: translateX(-310px); */
        }

        .card {
            width: 300px;
            height: 300px;
            background: green;
            display: inline-block;
            color: #f0f0f0;
            text-align: center;
            line-height: 300px;
        }

        .control-btn {
            position: absolute;
            height: 100%;
            opacity: 0.5;
            z-index: 1;
        }

        .previous-btn {
            left: 0;
        }

        .next-btn {
            right: 0;
        }
    </style>
</head>

<body>
    <div class="container">
        <div class="left-wrapper">
            <ul class="topic-box">
                <li class="topic">Tipic 1</li>
                <li class="topic">Tipic 2</li>
                <li class="topic">Tipic 3</li>
                <li class="topic">Tipic 4</li>
                <li class="topic">Tipic 5</li>
            </ul>
        </div>
        <div class="right-wrapper">
            <div class="card-box">
                <div class="card">固定不变的盒子</div>

                <div class="card-scroll-container">
                    <button class="control-btn previous-btn">⬅️</button>
                    <div class="card-scroll-wrapper">
                        <div class="card">卡片1</div>
                        <div class="card">卡片2</div>
                        <div class="card">卡片3</div>
                        <div class="card">卡片4</div>
                        <div class="card">卡片5</div>
                        <div class="card">卡片6</div>
                        <div class="card">卡片7</div>
                    </div>
                    <button class="control-btn next-btn">➡️</button>
                </div>

            </div>
        </div>
    </div>

    <script>
        const previousBtn = document.querySelector('.previous-btn');
        const nextBtn = document.querySelector('.next-btn');
        const scrollContainer = document.querySelector('.card-scroll-container');
        const scrollWrapper = document.querySelector('.card-scroll-wrapper');

        let scrollPosition = 0;
        let maxScroll = scrollWrapper.scrollWidth - scrollContainer.clientWidth;
        let scrollStep = 310;

        function scrollTo(position) {
            scrollPosition = Math.max(0, Math.min(position, maxScroll));
            scrollWrapper.style.transform = `translateX(-${scrollPosition}px)`;
        }

        previousBtn.addEventListener('click', () => {
            console.log('previous');
            scrollTo(scrollPosition - scrollStep);
        });

        nextBtn.addEventListener('click', () => {
            console.log('next');
            scrollTo(scrollPosition + scrollStep);
        });
    </script>
</body>
</html>
```

**代码解释：**

- `document.querySelector` API 可以根据传入的 css 选择器选择元素。
- `element.style.transform` API 可为指定元素定义移动位置。translateX(n) ，n 若大于0，是水平向右移动 n 个像素；n 若小于0，是水平向左移动 n 个像素；
- `element.addEventListener` API 可为指定元素添加事件监听器。
- `element.clientWidth` API 可获得指定元素的宽度。
- `scrollTo` 函数实现的效果是，将 `scrollWrapper` 移动到指定的位置（0是不移动，n(n>0) 是向左移动n像素的位置）。
- 点击向左移动时，需要将 `scrollWrapper` 移动到的位置是：当前位置减去移动步长；点击向右移动时，需要将 `scrollWrapper` 移动到的位置是：当前位置加上移动步长；
- 移动步长 = 卡片的宽度 + 间距。
