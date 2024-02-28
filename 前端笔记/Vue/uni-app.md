## 生命周期

### 应用生命周期

| 函数名            | 说明                                                    |
| ----------------- | ------------------------------------------------------- |
| onLaunch          | 当 uni-app 初始化完成时触发（全局只触发一次）           |
| onShow            | 当 uni-app 启动，或从后台进入前台显示                   |
| onHide            | 当 uni-app 从前台进入后台                               |
| onError           | 当 uni-app 报错时触发                                   |
| onUniNViewMessage | 对 nvue 页面发送的数据进行监听，可参考 nvue 向 vue 通讯 |

### 页面生命周期

| 函数名                              | 说明                                                                                                                                                                                                                                                                                 |
| ----------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| onLoad                              | 监听页面加载，其参数为上个页面传递的数据，参数类型为 Object（用于页面传参），参考示例                                                                                                                                                                                                |
| onShow                              | 监听页面显示。页面每次出现在屏幕上都触发，包括从下级页面点返回露出当前页面                                                                                                                                                                                                           |
| onReady                             | 监听页面初次渲染完成。注意如果渲染速度快，会在页面进入动画完成前触发                                                                                                                                                                                                                 |
| onHide                              | 监听页面隐藏                                                                                                                                                                                                                                                                         |
| onUnload                            | 监听页面卸载                                                                                                                                                                                                                                                                         |
| onResize                            | 监听窗口尺寸变化                                                                                                                                                                                                                                                                     |
| onPullDownRefresh                   | 监听用户下拉动作，一般用于下拉刷新，参考示例                                                                                                                                                                                                                                         |
| onReachBottom                       | 页面滚动到底部的事件（不是 scroll-view 滚到底），常用于下拉下一页数据。具体见下方注意事项                                                                                                                                                                                            |
| onTabItemTap                        | 点击 tab 时触发，参数为 Object，具体见下方注意事项                                                                                                                                                                                                                                   |
| onShareAppMessage                   | 用户点击右上角分享                                                                                                                                                                                                                                                                   |
| onPageScroll                        | 监听页面滚动，参数为 Object                                                                                                                                                                                                                                                          |
| onNavigationBarButtonTap            | 监听原生标题栏按钮点击事件，参数为 Object                                                                                                                                                                                                                                            |
| onBackPress                         | 监听页面返回，返回 event = {from\:backbutton、 navigateBack} ，backbutton 表示来源是左上角返回按钮或 android 返回键；navigateBack 表示来源是 uni.navigateBack ；详细说明及使用：onBackPress 详解。支付宝小程序只有真机能触发，只能监听非 navigateBack 引起的返回，不可阻止默认行为。 |
| onNavigationBarSearchInputChanged   | 监听原生标题栏搜索输入框输入内容变化事件                                                                                                                                                                                                                                             |
| onNavigationBarSearchInputConfirmed | 监听原生标题栏搜索输入框搜索事件，用户点击软键盘上的“搜索”按钮时触发。                                                                                                                                                                                                               |
| onNavigationBarSearchInputClicked   | 监听原生标题栏搜索输入框点击事件                                                                                                                                                                                                                                                     |

### 组件生命周期

| 函数名            | 说明        |
| ----------------- | ----------- |
| onLaunch          | row 1 col 2 |
| onShow            | row 1 col 2 |
| onHide            | row 1 col 2 |
| onError           | row 1 col 2 |
| onUniNViewMessage | row 1 col 2 |

## 页面通讯
