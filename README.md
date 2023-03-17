# 日本语能力测试（JLPT）抢座脚本

这个脚本会调用网站原本的一些方法来实现ajax请求，但去除了ui的各种操作，以便更快的轮询和发起请求。

如果这个脚本有帮到你的话，麻烦给个star吧。

**一緒に散歩しましょう**

---

## 脚本界面

![截图](screenshot/ui-1.png)

- 报考的等级
    - 字面意思

- 改座模式
    - 用于订座成功之后进行改座。
    - 订座成功后有且仅有一次改座机会。
    - 改座失败不影响当前订座。
    - 目标考场不要包含已报考场。

- 快速抢座考场
    - 填写考点代号，用英文逗号分隔，例如：`1020101,1020103,1020105`。
    - 因为在人多的时候，查询接口会卡。而第一天往往所有考场都是有座位的，所以可以跳过查询直接订座。
    - 可以在这里填写考场，会自动卡时间，2点开始，按照顺序尝试直接订座。
    - 注意每次订座都需要消耗验证码。

- 目标考场
    - 填写考点代号，用英文逗号分隔，例如：`1020101,1020103,1020105`。
    - 会通过接口去查询哪个有空座，然后按照列表的优先顺序选择有空座的考场。

- 开始/停止按钮
    - 字面意思

- 验证码显示和输入
    - **每次订座请求都会消耗掉验证码，一旦订座失败，会立刻请求新的验证码。请注意迅速输入，以免因此耽误时间。**
    - 不用关心大小写。
    - 在输入框按回车提交。
    - 如果看不清，不输入或输入小于4个字符，回车提交，都会请求新的验证码。
    - 这里刷出验证码之后，不要在原来的界面上刷新验证码。

- 日志显示
    - 显示过程中的日志。
    - 如果觉得窗口小，console控制台也会有一样的输出。
    
- 参数的保存
    - 界面上的参数修改之后，会自动保存到localStorage。

## 使用方法

- 浏览器打开 <https://jlpt.neea.cn/index.do>，登录帐号。

- F12打开控制台，会因为无限循环的debugger而进入断点调试。取消断点（Deactivate breakpoints），然后恢复运行（Resume script execution）。
    ![截图](screenshot/debug.png)

- 来到Console界面，将`jlpt.js`所有代码粘贴进去，回车，界面上出现窗口。

- 调整参数，点击开始。

- 刚运行或者验证码错误/过期之类的，会自动获取一个新的验证码，显示在窗口里。输入验证码答案后，程序继续运行。
![截图](screenshot/ui-2.png)

- 程序循环查询考场信息，找到符合目标条件的有座位考场，会立刻发起订座的请求。
![截图](screenshot/ui-3.png)
![截图](screenshot/success.jpg)

## 注意事项

- 最好在14:00之前几分钟，登录账号，运行脚本。以防14:00左右卡顿导致登录困难。但不要太早登录，否则会超时掉出来重新登录。

- 脚本运行时，页面最好不要操作，以免导致验证码失效。（实际上只需要登录即可，甚至不需要进入到选座界面）

- 报名第一天，因为人多，且座位肯定是有的，可以先尝试快速抢座。

- 第一波没抢到，后续报名日，每天会释放前一天没付款的座位。相对人少，且不确定哪个考场会有座位释放，所以不建议再使用快速抢座，并且最好在目标考场里多给几个周边的备选考场。（不要纠结一定要某个考场，有的时候真的就全定完了，不会释放了）

- 建议提前演练一下，一方面脚本可能有问题，或者网站更新导致功能不可用。

- 如果遇到订座请求（book.do）报400，可能需要注销一下重新登录才能好。