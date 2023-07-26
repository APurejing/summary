## throttle 节流

**函数在 n 秒内只执行一次**实现原理就是通过一个布尔类型变量来判断是否可执行回调，当变量为 true 时，生成一个定时器，同时将变量取反通过闭包保存起来，当定时器执行完回调后，再将变量变为 true，在变量为期 false 间，调用节流函数不会生成定时器。

使用场景：mousemove

    `
    function throttle(fn, delay) {
     // 记录上一次函数触发的时间
     let lastTime = Date.now();
     return function() {
      let context = this;
      // 记录当前函数触发的时间
      var nowTime = Date.now()
      // 当前时间减去上一次执行时间大于这个时间间隔才让他触发这个函数
      if (nowTime - lastTime >= delay) {
       // 绑定this 指向
       fn.apply(context, arg);
       // 同步时间
       lastTime = Date.now();
       }
      }
     }

    function fn() {
     console.log('节流');
     }

    addEventListener('scroll',throttle(fn, 1000))
    `
