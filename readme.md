# 2025 新春版：一个近乎完美的 Konva 手写板诞生记

基于 Konva 开发的可直接用于各类项目的 Web 手写板组件。

包含 4 套代码：

1. React18/19 (javascript)
2. React18/19 (typescript)
3. Vue3 (javascript)
4. Vue3 (typescript)

## 目录结构说明

dist 目录为 build 后的代码，可自行下载体验最终效果。

zip 压缩包为项目源码。

🔑🔑💖💖 解压密码，见配套教程原文。 💖💖🔑🔑

## 教程原文

📚📚 本项目有详细的讲解教程，原文请关注我的微信公众号【卧梅又闻花】📚📚

[《2025 新春版：一个近乎完美的 Konva 手写板诞生记（Vue版）》](https://mp.weixin.qq.com/s/cowD80tN0OkbTRyNXUb4bQ)

[《2025 新春版：一个近乎完美的 Konva 手写板诞生记（React版）》](https://mp.weixin.qq.com/s/1xy10ZFPtU0cyVQi-AmRbw)

## 教程目录

```
1 开发及测试环境
2 核心点及解决方案
• 2.1 识别鼠标、手指、触控笔
• 2.2 高强度单点笔划操作时可能误识别为多点触控
• 2.3 双指缩放和移动
• 2.4 自适应外层容器尺寸
• 2.5 双指接触和抬起的瞬间导致误触笔划
• 2.6 笔划过多导致的卡顿
• 2.7 其他性能优化Tips
• 2.8 iPad与HUAWEI MatePad体验差异
• 2.9 Debug信息输出
3 项目源码
推荐阅读
ZIP项目源码解压密码
```

## API 说明

> drawStage组件（画布Stage）的宽高无需设置，根据“引入组件的外部容器尺寸”及“加载的底板图片尺寸”自动适配，类似自动实现CSS的background-size: contain的填充效果。因此，只需自行做好外层容器的适配即可。

| 属性                 | 说明                                                                                                 | 类型                           | 默认值                                  |
| :----------------- | :---------------------------------------------------------------------------------------------------- | :--------------------------- | :-------------------------------------- |
| imageSrc           | 【必填】底板图片。支持URL或base64，URL不能跨域        | string                       |                                         |
| tool               | 【必填】工具。pen=笔、eraser=橡皮         | string           |            |
| allowedPointerType | 允许的触控方式。mouse=鼠标，touch=手指，pen=触控笔      | object       | { mouse: true, touch: true, pen: true } |
| initialData        | 初始笔划数据        | string                       | null                                    |
| borderWidth        | 画布边框宽度        | number                       | 1                                       |
| borderColor        | 画布边框颜色        | string                       | #000000                                 |
| maxScale           | 最大缩放比例        | number                       | 3                                       |
| stageOriginalWidth | Stage原始宽度（参考系）。用于当Stage器尺寸大小发生变化时，笔划的粗细以stageOriginalWidth为参考进行比例缩放。例如，设置stageOriginalWidth=900，strokeWidth=9时，当画布尺寸宽度自动调整为1000时，笔划粗细也会相应自动调整为10，确保笔划粗细与画布尺寸相对不变。默认为auto，实际作用是将当前画布的宽度作为stageOriginalWidth，auto适用于首次加载画布的尺寸是固定值（以移动端为例，无论横屏还是竖屏，初次加载时，都需要将画布尺寸设置为固定值）。总之，为了保证在画布尺寸自适应变化时，笔划粗细和画布尺寸的比例相对不变，需要借助stageOriginalWidth给strokeWidth一个参考系。 | number \|\| string           | auto                                    |
| strokeColor        | 笔划颜色           | string                       | #000000                                 |
| strokeWidth        | 笔划粗细           | number                       | 5                                       |
| strokeTension      | 笔划平滑度（0-1），对所有笔划生效            | number                        | 0.5                                     |
| strokeCap          | 笔划线段两端的样式。round=圆形，square=方形、butt=无，对所有笔划生效           | string                       | round                   |
| strokeJoin         | 笔划多条线段的链接样式。round=圆形，miter=尖角、bevel=斜切，对所有笔划生效      | string                       | round                    |
| maxRealRenderLines | 最大实时渲染的笔划数量（建议20，尽量不超过100，越大越卡顿）                     | number                       | 20                      |
| maxUndoLines       | 最大可撤销的笔划数量（建议10，必须小于maxRealRenderLines）                   | number                       | 10                       |
| enableDebug        | 显示调试信息                                                             | boolean                      | false                  |
| eraserHintColor    | 橡皮擦提示色                                                             | string                       | #b5f5ec                  |
| eraserHintWidth    | 橡皮擦粗细                                                              | number                       | 20                     |
| eraserTension      | 橡皮擦平滑度（0-1），对所有橡皮擦笔划生效                                     | number                       | 0.5                      |
| eraserCap          | 橡皮擦线段两端的样式。round=圆形，square=方形、butt=无，对所有橡皮擦笔划生效     | string                       | round                    |
| eraserJoin         | 橡皮擦多条线段的链接样式。round=圆形，miter=尖角、bevel=斜切，对所有橡皮擦笔划生效   | string                       | round                    |
| onImageLoadFailed  | 事件回调：底板图片加载失败                                                | function                     |         null           |
| onImageLoadSucceed | 事件回调：底板图片加载成功                                               | function                     |           null           |
| onLinesChanged     | 事件回调：笔划发生改变                                                  | function                     |          null             |
| onUndoFinished     | 事件回调：撤销完成，返回剩余可撤销的次数                                   | function(number: resetCount) |       null               |


## 更新日志
### 1.1.0 （2025-09-12）
更新全部依赖至当前最新版本：
```
@eslint/js                    ^9.20.0  →   ^9.35.0
@types/react                  ^19.0.8  →  ^19.1.12
@types/react-dom              ^19.0.3  →   ^19.1.9
@vitejs/plugin-react           ^4.3.4  →    ^5.0.2
antd                          ^5.24.0  →   ^5.27.3
eslint                        ^9.20.1  →   ^9.35.0
eslint-plugin-react           ^7.37.4  →   ^7.37.5
eslint-plugin-react-hooks      ^5.1.0  →    ^5.2.0
eslint-plugin-react-refresh   ^0.4.19  →   ^0.4.20
globals                      ^15.15.0  →   ^16.4.0
konva                         ^9.3.18  →   ^10.0.2
less                           ^4.2.2  →    ^4.4.1
react                         ^19.0.0  →   ^19.1.1
react-dom                     ^19.0.0  →   ^19.1.1
react-konva                   ^19.0.2  →  ^19.0.10
sass                          ^1.85.0  →   ^1.92.1
vite                           ^6.1.0  →    ^7.1.5
```
无业务代码更新。
