# CRLF

> CR ： Carriage Return ，对应 ASCII 中转义字符 `\r` ，表示回车。
>
> LF ： Line Feed ， 对应 ASCII 中转义字符 `\n` ，表示换行。
>
> CRLF ： Carriage Return & Line Feed ，对应 ASCII 中转义字符 `\r\n` ，表示回车并换行。

Windows 系统采用两个字符 `CRLF` 来进行换行。

而 Unix / Linux / macOS 系统采用单个字符 `LF` 来进行换行。

据野史记载，在很久以前的机械打字机时代， `CR` 和 `LF` 分别具有不同的作用： `LF` 会将打印纸张上移一行位置，但是保持当前打字的水平位置不变。 `CR` 则会将打字机上的滚动托架滚回到打印纸张的最左侧，但是保持当前打字的垂直位置不变，即还是在同一行。当 `CR` 和 `LF` 组合使用时，则会将打印纸张上移一行，且下一个打字位置将回到该行的最左侧，也就是我们今天所理解的换行操作。

随着时间的推移，机械打字机渐渐地退出了历史舞台，当初的纸张变成了今天的显示器，打字机的按键也演变为了如今的键盘。在操作系统出现的年代，受限于内存和软盘空间的不足，一些操作系统的设计者决定采用单个字符来表示换行符，如 Unix 的 `LF` 、 Macintosh 的 `CR` 。他们的意图都是为了进行换行操作，所以才有这样字符上的不同。