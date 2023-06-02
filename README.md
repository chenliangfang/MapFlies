# MapFlies-使用文档
# MapFiles使用文档——信托经理批量生成合同小工具

## 0. 前言

> 目前头部信托公司 ***私行类代销业务*** 明显上升，私行类业务多为***系列化*** 项目，***标准化程度非常高***，但是标注化项目承做过程中存在最大的问题便是合同内部和合同之间的***一致性问题***和一致性问题。同时理财子债券业务的申赎需求也非常大，人工处理申赎单的工作压力也非常大。

为响应**标准化** 业务导向，优化项目承做流程，提高项目承做效率，增加项目经理承做项目容量，开发MapFiles工具。

---

> Map为Python的一个函数，主要用于批量处理变量使用，所以MapFiles的意思就是批量处理文件的意思。

## 1. 功能介绍

MapFiles 是实现项目台账到项目文件的批量转化功能。其中，项目台账是以excel格式的展示，项目文件可以是word、excel的格式文件。

1. 项目台账格式；

    项目台账的第一行必须为变量名，所谓变量值，之后每一行为每一个项目的标量值。

    ![](https://secure2.wostatic.cn/static/eKokBDtAvfqFGJqLNZ3Hmq/微信图片_20200822001538.png?auth_key=1685681739-61dtMDw5Dk5kFhV1yQLWfa-0-aee7e71c5b39f4915917d886366b4612)

    
2. 文件模板展示

![](https://secure2.wostatic.cn/static/crLpGtoTCBc8VZKcuuzcWK/word.png?auth_key=1685681739-oqYSgdmX5ECJGRbueD2HEn-0-cddadb604a03c63081ffd5f6b65dc901)

MapFiles 即实现excel形式项目台账至项目文件之间的一一映射，可实现包括项目合同、PMS项目审批内容、预成立通知、交易指令、对方先用印承诺函等等一些类word和excel文件的一键生成，尤其是系列系列化项目非常有帮助。

## 2. 软件界面介绍和详细使用教程

1. 软件界面展示

![](https://secure2.wostatic.cn/static/9zYf6shwspk8qoBN5mVEZK/image.png?auth_key=1685681739-rhr3oDuN4oKGxLZJAXD2sm-0-c678b9a38c04391f9f79618f006211e4)

- **Template：**用于选择已经制作好的word（必须为.docx格式）或者excel模板；
- **Save Path：**用于选择文件保存的路径；
- **Data Path：**即项目台账的选择；
- **Sheet：**输入数据源选择的项目台账的sheet号码，第一个sheet，则输入值为1，以此类推；
- **Row：**输入数据源选择的项目台账的sheet行号，比如第2行即为2，1-10表示第1行至第10行，1,3,5表述第1,3,5行；
- **Names：**即生成文件文件名字前缀，用以标注项目的名字，后续开发考虑加入文件铭前缀直接管理项目台账中某一个或者两个变量；
- **MapFiles：**即自动化生成文件；
- **MapPdf：**自动生产word + 对应的PDF文件，生产PDF文件速度一般较慢；

完成上述的一些列选择后，即可生自动化生成文件了。

2. 效果展示

![生成的文件列表](https://secure2.wostatic.cn/static/fVsyGGuWRhZRMbZyDVUPad/image.png?auth_key=1685681739-eeHM7D51rsxggpXFD1vtZh-0-90cd948d86e8490369b1f634544dbd1c)

![](https://secure2.wostatic.cn/static/qRWwr6nxmUSwjPC1D2K8mH/image.png?auth_key=1685681739-o9pbr7GXJhfuHQ121wwJFg-0-27ee29bea642c95811afa1e534669674)

![](https://secure2.wostatic.cn/static/sJbzLCshdgaXy8d4dbrxg3/image.png?auth_key=1685681739-d9nTAg7xVAjtihZZ5FDHfX-0-f6ce9503dae4141c25225247d521b069)

上述标注红色框的都是自动替换的地方，而这些也是替地方都是只需要我们一次性在项目台账中输入一次，就可以完成要素在项目***全项目周期的重复使用，减少一致性等问题，提高项目承做效率。***

## 4. 使用建议

- **数字问题：**数据大于3的数字，系统会自动使用千分位以及保留2位小数的形式展示在最后的文件中，小于等于3的数字，系统自动使用4位置有效数字形式展示在最后的文件中；如果想展示数字本来的样子，建议在台账中以【数字形式】展示，eg：【365】。
- **项目合同生成时，部分要素未定确定如何解决?**

    比如专户账号未确定，则变量值以{{变量名}}命名，待变量确定后，以生成的文件作为模板再生成一次即可。
- **日期数据如何避免入坑**：最佳方式以【2020年8月17日】的形式输入变量名，以可以以 '2020年8月17日，其中' 使得日期数据被识别未字符串。

## 5.  高级语法（学会使用会很香）

> 上述基础用法只能在非常标准的项目中使用或者系列项目中使用，并不能有效的解决多数的问题，使用效果欠佳。**我们的合同模版往往需要不同的情况判断后选择不同的表述**，所以需要使用高级用法，目前华润信托TOF项目支持模板按照自动化生产合同。

### 模板语法：

```Python
{%r if qk1 == "Y" %}
采用的表述{{项目简称}}
{%r elif qk1 == "N" %}
采用的表述
{%r endif %}
```

## 6. 现在链接以及权限申请

- 下载链接【请使用最新的下载链接】

链接：[https://pan.baidu.com/s/1nACa37gLoqSfYhI6QDdhAQ?pwd=cpxk](https://pan.baidu.com/s/1nACa37gLoqSfYhI6QDdhAQ?pwd=cpxk)
提取码：cpxk

- 使用方法
    1. 解压压缩包
    2. 将如下exe文件发送桌面快捷方式

    ![](https://secure2.wostatic.cn/static/2aGRCcAUDTMn6ZSPAjpcDB/image.png?auth_key=1685681739-gTJCoACP943CizSYcua9UE-0-ef8cb811ad0a19209db41bd1c4ef8483)

    1. 点击exe文件运行
- 权限申请

运行程序后，会自动生成macs.txt文件，查阅macs文件中的mac地址后填写到以下的seatable中

[https://cloud.seatable.cn/dtable/links/ee53cb4649c140409530](https://cloud.seatable.cn/dtable/links/ee53cb4649c140409530)。

![](https://secure2.wostatic.cn/static/6k3N6jDtQkFwdbk2vCyHVq/image.png?auth_key=1685681739-aP4wvGAcnbS52PyLjg9o5N-0-bf65ba12b97288af7d4ffe5109200a9a)
