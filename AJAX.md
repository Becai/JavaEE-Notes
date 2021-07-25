# AJAX

**什么是AJAX ？**

Asynchronous JavaScript And XML —— 异步的JavaScript和XML

AJAX不是一个技术，是多个技术联合实现的产物

**异步和同步有什么区别 ？**

A线程和B线程，并发执行，谁也不等谁，这就是异步

A线程和B线程，在A线程执行的时候B线程需要等待，或者B线程执行的时候A线程需要等待，这就是同步

举个例子：普通B/S模式（同步）AJAX技术（异步）

同步：提交请求$\rightarrow$等待服务器处理$\rightarrow$处理完毕返回这个期间客户端浏览器不能干任何事

异步：请求通过事件触发$\rightarrow$服务器处理（这是浏览器仍然可以作其他事情）$\rightarrow$处理完毕

**传统的请求（form表单action/a标签href）和AJAX请求有什么区别 ？**

传统的请求，都是同步的；AJAX请求，可以做到异步

**AJAX主要解决的问题：**

- 页面的局部刷新（需要前端手动实现）
- 异步请求，提高用户体验

## 传统请求的缺点

**当浏览器采用的是传统请求的时候，请求只要一发送，整个浏览器窗口锁定，无法点击其它按钮，并且浏览器会将窗口当中的数据全部清除，跳转新的页面**

- 每次请求，页面全部刷新
- 多线程同步请求

## AJAX请求

AJAX发送请求全靠浏览器内置的XMLHttpRequest对象。使用这个对象可以在浏览器中单独启动一个浏览器线程，通过浏览器线程发送请求，达到异步效果。

**使用AJAX请求的四个步骤**

1. 创建AJAX核心对象XMLHttpRequest（浏览器内置的，可以直接使用）

   ```javascript
   if (window.XMLHttpRequest) {
       var xhr = new XMLHttpRequest();
   } else {
       // 不支持XMLHttpRequest对象，IE5和IE6不支持，它只支持ActiveXObject对象来发送ajax请求
       var xhr = new ActiveXObject("Microsoft.XMLHTTP");
   }
   ```

2. 注册回调函数

   ```javascript
   // 程序执行到这里的时候，后面的回调函数并不会执行，只是将回调函数注册给xhr对象
   // 等xhr对象的readyState发生改变时，后面的回调函数就会执行
   /*
   * XMLHttpRequest对象在请求和响应的过程当中，该对象的readyState状态从0-4
   * 0：请求未初始化
   * 1：服务器连接已建立
   * 2：请求已接收
   * 3：请求处理中
   * 4：请求已完成，且响应已就绪
   */
   xhr.onreadystatechange = function() {
       // xhr对象的readyState的值发生改变的时候，回调一次
       if (readyState == 4) { // 服务器响应结束
           if (xhr.status == 200) { // 服务器正常响应结束
               // 在浏览器端使用xhr对象接收服务器端的响应回来的文本
               var res = xhr.responseText;
               // 通过HTML显示
           } else {
               // 错误处理
           }
       }
   }
   ```

3. 开启浏览器与服务器之间的通道

   ```javascript
   // method：GET/POST 请求方式
   // url：请求路径
   // asyn：true/false（true表示支持异步，false表示支持同步）
   xhr.open(method,url,asyn)
   ```

4. 发送AJAX请求

   ```javascript
   // 发送AJAX请求
   // POST请求提交数据在send方法当中提交
   xhr.send()
   ```

**默认请求类型：**

Content-Type: application/x-www-form-urlencoded; charset=UTF-8

此格式为表单提交格式，数据为key1=value1&key2=value2的格式

