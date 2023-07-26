## debounce 防抖

**某函数在某段时间内，无论触发了多少次回调，都只执行最后一次。**
防抖实现原理就是利用定时器，函数第一次执行时设定一个定时器，并且通过闭包缓存起来，之后调用时发现已经设定过定时器就清空之前的定时器，并重新设定一个新的定时器，如果存在没有被清空的定时器，当定时器计时结束后触发函数执行。

使用场景：
搜索框输入查询，按钮提交事件

    `function debounce(fn, delay) {
      // 利用闭包保存定时器
      let timer = null;
      return function() {
        let context = this;
        let arg = arguments;
        // 在规定时间内再次触发会先清除定时器后再重设定时器
        clearTimeout(timer)
        // 重新设置一个新的延时器
        timer = setTimeout(() => {
          fn.apply(context, arg)
        }, delay);
      }
    }

    function fn() {
      console.log('防抖');
      }
      addEventListener('scroll',debounce(fn, 1000))
    `
