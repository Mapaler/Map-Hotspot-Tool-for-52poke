# 神奇宝贝百科地图热点编辑辅助工具
运行环境：此工具为 Adobe Fireworks CS6 的命令脚本。

软件功能：可以在图片内导入和导出 神奇宝贝百科地图热点，方便可视化编辑。

## 背景
玩《晶灿钻石/明亮珍珠》时发现神奥地区地图上没有热点，无法直接点击地图上的位置快速访问我要查看的地点，只能去下面的文字列表框里慢慢查找，非常麻烦。

![双叶真地图](doc/images/双叶镇地图.webp)

后来发现神奥地区的主页面上的地图是有热点的，但是是《白金》的老地图了

![神奥地区热点](doc/images/神奥地区.webp)

于是尝试修改模板字符串`{{神奥地图|Pt}}`内的游戏版本，发现`{{神奥地图|BDSP}}`虽然能显示《晶灿钻石/明亮珍珠》的地图图片，但是热点坐标仍然是白金版本的。

![复刻地图仍用了白金热点](doc/images/复刻地图仍用了白金热点.webp)

于是前往模板源代码查看，发现确实只写了白金的热点数据。要在这种源代码的模式下编辑热点数据也太困难了，所以我决定找一找有没有什么工具可以做。

我印象中网页三剑客里的 Dreamweaver 是可以可视化操作热点的，尝试使用网页内的源代码，确实可以显示出热点的区域。不过自从开始接触 HTML5 的新功能以来，我已经超过 10 年没用过了，现在 Dreamweaver 的界面我已经看不懂了。

![Dreamweaver的界面已经看不懂了](doc/images/Dreamweaver.webp)

但是好在我还有我很熟悉的 Fireworks ，于是我花一个通宵给 Fireworks 写了导入和导出的脚本，这样就可以方便的给新地图图片添加热点了。

## 使用方法
### Fireworks 如何使用命令脚本
#### 单次使用
执行`命令`-`运行脚本`，然后打开需要运行的`.jsf`脚本即可。

![Fireworks单次运行脚本](doc/images/Fireworks单次运行脚本.webp)

#### 加入命令菜单重复使用
将`.jsf`文件放入以下两个目录之一，重启 Fireworks 即可显示在命令菜单里。
* 个人数据目录（对当前用户生效），文件管理器地址栏输入：  
`%AppData%\Adobe\Fireworks CS6\Commands\`
* Fireworks 安装目录（对所有用户生效），默认为：  
`C:\Program Files (x86)\Adobe\Adobe Fireworks CS6\Configuration\Commands\`

![Fireworks运行菜单运行脚本](doc/images/Fireworks运行菜单运行脚本.webp)

### 开始编辑地图热点
#### 导入地图热点
访问地图模板，从模板源代码中获取到形如`rect 23 144 37 150 [[２０１号道路（神奥）]]`这部分的热点坐标值，每行一个。将它们保存到本地的一个文本文件里。

![神奥地图模板](doc/images/Template神奥地图.webp)

由于 Fireworks 的引擎和文档不完善，未能找到如何读取`UTF-8`文件，目前需要使用`ANSI(GBK)`等编码输入数据。

![保存为GBK](doc/images/导入地图热点坐标保存为GBK.webp)

在 Fireworks 内打开地图图片，运行`导入地图热点`功能，选择刚才保存的地图热点坐标列表文件。你将会看到热点添加到了画面上。

![导入热点前](doc/images/导入热点前.webp)
![导入热点后](doc/images/导入热点后.webp)

#### 编辑现有热点/新增热点
指针工具可以移动现有坐标，或编辑多边形坐标的顶点。

![工具-指针](doc/images/工具-指针.webp)

工具栏的 Web 区第一个图标就是热点工具，你可以使用这些工具添加新的热点区域。

![工具-热点](doc/images/工具-热点.webp)

建议在图层里面为热点命名

![工具-热点](doc/images/设定热点元素名.webp)

#### 导出 Wiki 地图热点代码
运行`导出地图热点`功能，选择一个地方填入文件名。（注意需要自己输入完整的文件扩展名）
![导出热点前](doc/images/导出热点前.webp)
![导出热点选文件名](doc/images/导出热点选文件名.webp)

打开导出的文件即可以看到 Wiki 里面使用的代码了。

![导出热点后](doc/images/导出热点后.webp)

**注意**
* 模板里最后一行的`desc none`是干什么用的我不了解，所以需要你自己加上。
* 导出的格式是 UTF-8，但是导入时无法正确读取 UTF-8 编码，是 Fireowrks 引擎不完善导致的，如果需要再次导入请自己转换到 GBK 编码。

### 更多细节
#### 直接导出网页测试
如果你像下图一样完整的填写了`链接`、`替代`，可以直接从 Fireworks 导出一个可以使用的网页进行测试。

![新增热点更名](doc/images/新增热点更名.webp)

点击`文件`-`导出`

![导出网页-1.webp](doc/images/导出网页-1.webp)

选择导出` HTML 和图像`
![导出网页-2.webp](doc/images/导出网页-2.webp)

用浏览器打开刚才导出的网页既可以进行测试

![导出网页-3.webp](doc/images/导出网页-3.webp)

#### 名称判定逻辑情况的说明

因为神奇宝贝百科的热点链接`[[页面名]]`可以额外设定显示名`[[页面名|显示名]]`，对应到 Fireworks 软件内如下 3 处可以设定名称的地点。

![新增热点更名](doc/images/新增热点更名.webp)

上图所示 3 处编辑位置采取如下选择逻辑：

* **页面名**：按`链接`→`元素名`→`替代名`的优先级使用。当没有填写`链接`时，使用`元素名`，没有修改`元素名`时使用`替代名`。
* **显示名**：按`元素名`→`替代名`的优先级使用，如果都不设定，或与页面名相同，则忽略。

因此上图生成的代码为`circle 201 154 12 [[鎧島|铠岛]]`，因为简繁体不一致。

如果不设定`元素名`，就会读取`替代名`，如下图未设定元素名，元素名显示为默认的“热点”。另外下图的链接使用的是浏览器直接复制过来的编码后的 URI，这种 URI 无法在 Wiki 代码内使用，所以我在程序里添加了解码的步骤。

![新增热点更名2](doc/images/新增热点更名2.webp)

因此上图生成的代码为`circle 201 154 12 [[鎧島|假设有个铠岛]]`。

**注意**：虽然我添加了解码的步骤，但是因为 Fireworks 引擎的 BUG，执行解码后程序会直接闪退，记得保存。所以最好还是不要用编码的URL，而是使用原始的汉字 URI。