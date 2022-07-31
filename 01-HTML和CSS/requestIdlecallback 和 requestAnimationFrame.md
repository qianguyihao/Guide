

## requestIdlecallback：由 React fiber引起的关注

- 组建树转换为链表，可分段宣染

- 渲染时可以暂停，去执行其他高优任务，空闲时再继续宣染。
- 如何判断空闲? 通过 requestIdleCallback



## RAF：requestAnimationFrame

- 要想动画流畅，更新频率需要60帧/s，即16.67ms更新一次视图。

- setTimeout 要手动控制频率；而 通过RAF，浏览器会自动控制。

- 页面在后台或隐藏 iframe 中，setTimeout 依然执行，而RAF 会暂停。

## requestIdlecallback和requestAnimationFrame区别

- requestIdlecallback的优先级低，空闲时才会执行。
- requestAnimationFrame的优先级高，每次渲染完成后都会执行。

### 追问：它们是宏任务还是微任务？

都是宏任务。要等DOM渲染完成后才会执行，肯定是宏任务。