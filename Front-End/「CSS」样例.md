### 1. 心形动画

[参考视频](https://www.bilibili.com/video/BV1ba4y1475n)

```html
<ul class="loading-wrapper">
    <li class="loading-item"></li>
    <li class="loading-item"></li>
    <li class="loading-item"></li>
    <li class="loading-item"></li>
    <li class="loading-item"></li>
    <li class="loading-item"></li>
    <li class="loading-item"></li>
    <li class="loading-item"></li>
    <li class="loading-item"></li>
</ul>
```

```css
/* 加载动画 */
.loading-wrapper {
    width: 100%;
    height: 100%;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
}
.loading-item {
    width: 10px;
    height: 10px;
    border-radius: 5px;
    margin: 3px;
}
.loading-item:nth-child(1) {
    background-color: red;
    animation: stretch1 0.8s 0s infinite ;
}
.loading-item:nth-child(2) {
    background-color: darkturquoise;
    animation: stretch2 0.8s 0.05s infinite ;
}
.loading-item:nth-child(3) {
    background-color: darksalmon;
    animation: stretch3 0.8s 0.1s infinite ;
}
.loading-item:nth-child(4) {
    background-color: deeppink;
    animation: stretch4 0.8s 0.15s infinite ;
}
.loading-item:nth-child(5) {
    background-color: yellow;
    animation: stretch5 0.8s 0.2s infinite ;
}
.loading-item:nth-child(6) {
    background-color: deeppink;
    animation: stretch4 0.8s 0.25s infinite ;
}
.loading-item:nth-child(7) {
    background-color: darksalmon;
    animation: stretch3 0.8s 0.3s infinite ;
}
.loading-item:nth-child(8) {
    background-color: darkturquoise;
    animation: stretch2 0.8s 0.35s infinite ;
}
.loading-item:nth-child(9) {
    background-color: red;
    animation: stretch1 0.8s 0.4s infinite ;
}
@keyframes stretch1{
    30%,50%{
        height: 33px;
        transform: translateY(-15px);
    }
    70%,100%{
        height: 0px;
        transform: translateY(0px);
    }
}
@keyframes stretch2{
    30%,50%{
        height: 60px;
        transform: translateY(-17px);
    }
    70%,100%{
        height: 0px;
        transform: translateY(0px);
    }
}
@keyframes stretch3{
    30%,50%{
        height: 80px;
        transform: translateY(-15px);
    }
    70%,100%{
        height: 0px;
        transform: translateY(0px);
    }
}
@keyframes stretch4{
    30%,50%{
        height: 90px;
        transform: translateY(-5px);
    }
    70%,100%{
        height: 0px;
        transform: translateY(0px);
    }
}
@keyframes stretch5{
    30%,50%{
        height: 100px;
        transform: translateY(3px);
    }
    70%,100%{
        height: 0px;
        transform: translateY(0px);
    }
}
```

### 2. 果冻效果的按钮

[参考视频](https://www.bilibili.com/video/BV1Fk4y1R77R?t=411)

```html
<body>
    <div class="wrapper">
        <div class="btn">cute</div>
    </div>
</body>
```

```css
body {
    width: 100vh;
    height: 100vh;
    margin: 0px;
    padding: 0px;
}

.wrapper {
    width: 100%;
    height: 100%;
    background-color: rgb(247, 251, 252);
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
}

.btn {
    width: 150px;
    height: 75px;
    color: white;
    text-align: center;
    line-height: 75px;
    background-color: rgb(24, 189, 204);
}

.btn:active {
    cursor: pointer;
    animation: cute 0.5s;
}

@keyframes cute {

    0%,
    100% {
        transform: scale(1, 1);
    }

    25%,
    75% {
        transform: scale(0.9, 1.1);
    }

    50% {
        transform: scale(0.8, 1.2);
    }
}
```

