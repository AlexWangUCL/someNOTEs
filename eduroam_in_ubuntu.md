作者：尹相楠
链接：https://www.zhihu.com/question/47685853/answer/112112266
来源：知乎

我这里详细展开一下。首先，我们回忆一下在之前的系统上，是如何配置 802.1x 认证的：
1. 点击桌面右上角的网络图标，进入 Edit Connections
2. 弹出一个窗口，点窗口右边的 Add 按钮，出现另一个窗口，窗口上有个下拉菜单，选择 Ethernet，然后点 Create
3. 在新的窗口里，输入最上面的 Connection name，最好不要加空格，比如 Ethernet_connection1，选择 802.1.x Security，勾选 Use 802.1.x security for this connection
4. Authentication 栏选择 Protected EAP (PEAP)
5. 这时候窗口又增加了很多下拉菜单和输入框
- 5.1 Anonymous identity 栏不要输入任何东西
- 5.2 勾选 No CA certificate is required
- 5.3 PEAP version: Automatic
- 5.4 Inner authentication: MSCHAPv2
- 5.5 输入你之前注册的 Username 和 Password，然后点 save save 的时候可能需要你输入系统密码。

做完上面这些步骤，如果在16.04之前的系统上，你就可以连网了，但是由于16.04 系统的 bug，现在你还是上不了网，会不停地弹出窗口让你输入密码。感谢楼上  @我是你的大圣蜀黍 的答案，我们只需要对系统文件做一个小小的改动就好了。
1. `Ctrl+Alt+t` 打开终端
2. `cd /etc/NetworkManager/system-connections`
3. ls 一下，你可以看到之前创建的配置文件（按上面的步骤，这里应该能找到 Ethernet_connection1），我们需要修改这个文件
4. 由于这个目录不在 home 下面，如果要修改，必须有管理员权限: sudo vim Ethernet_connection1，然后输入系统密码，进入到这个文件中
5. 光标跳到 [802-1x] 那个区块，你会注意到 identity=xxx，xxx为你之前配置这个文件时输入的用户名，但是，这个区块中没有你配置网络时输入的密码，所以，在identity这行下面，添加一行：password=xxxxx，xxxxx换成你的密码
6. 保存，退出，关机，开机，然后你就能连网了。