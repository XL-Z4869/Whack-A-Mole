# Whack-A-Mole
打地鼠游戏
效果：https://xl-z4869.github.io/Whack-A-Mole/
### 一、知识点
#### 1.Math.random()
#### 2.setTimeout()计数器
### 二、主要步骤
#### 1.获取元素
* 获取元素
* 定义分数为0
* 定义一个值，作为要出现的地鼠
* 定义一个timeup作为计时器开关
```
const holes = document.querySelectorAll('.hole');
const scoreBoard = document.querySelector('.score');
const moles = document.querySelectorAll('.mole');
let score = 0
let timeUp = false
let lastHole
```
#### 2.定义一个函数，随机产生一个数字
```
function randomTime(min, max) {
    return Math.round(Math.random() * (max - min) + min)
}
```
#### 3.定义一个函数，随机出现地鼠
```
function randomHole(holes) {
    const holeId = Math.floor(Math.random() * holes.length)
    const hole = holes[holeId]
    if (hole === lastHole) {
        console.log("是同一只地鼠");
        return randomHole(holes)
    }
    lastHole = hole
    return hole
}
```
#### 4.定义一个函数
* 获得随机的时间、地鼠
* 对样式进行操作，让地鼠出现
* 制作一个计时器
```
function peep() {
    const time = randomTime(200, 1000)
    const hole = randomHole(holes)
    hole.classList.add('up')
    setTimeout(() => {
        hole.classList.remove('up')
        if (!timeUp) peep()
    }, time)
}
```
#### 5.添加鼠标点击事件
```
function startGame() {
    console.log(123);
    scoreBoard.textContent = 0
    score = 0
    timeUp = false
    peep()
    setTimeout(() => timeUp = true, 10000)
}
```
#### 6.给地鼠添加点击事件
```
function scoreHandler(e) {
    if (!e.isTrusted) return;
    score++
    scoreBoard.textContent = score
    this.parentNode.classList.remove('up')
}
moles.forEach((mole) => mole.addEventListener('click', scoreHandler))
```
