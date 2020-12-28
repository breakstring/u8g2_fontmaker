# 前言
这是一个用于生成[u8g2](https://github.com/olikraus/u8g2)字体源代码的一键懒人脚本工具。

在[u8g2的官方字体文件](https://github.com/olikraus/u8g2/wiki/fntlistall)已经提供了大量的英文字体和部分由[larryli](https://github.com/larryli)所提供的部分文泉驿字体。但是在我做一个EPS32驱动的墨水屏设备的小项目中需要使用到[U8g2 for Adafruit GFX](https://github.com/olikraus/U8g2_for_Adafruit_GFX)，但是发现u8g2现有的[文泉驿字体](https://github.com/olikraus/u8g2/wiki/fntgrpwqy)中只提供了最高16点阵的中文字体，无法满足我的需求。所以就开始尝试动手自己制作u8g2中文字体，然后就随手撸了这么个懒人工具出来。

# 参考
- [u8g2关于中文字体的issue](https://github.com/olikraus/u8g2/issues/710)
- [larryli的Wiki](https://github.com/larryli/u8g2_wqy/wiki/CustomFont)

# 使用方法
## 修改参数
在 create.bat 里有几个关键的参数需要注意修改
- FONT_FILE: 即字体文件名（字体文件需要放在 font 目录下）
- FONT_NAME: 字体文件，请使用英文字符，回头生成的源代码里面要用。所以避免那些特殊字符吧。
- FONT_SIZE: 要生成的字体大小，可以是单个，也可以是数组形式（用空格分开就好，例如“16 24 36”）

## 运行
嗯。。。直接执行 create.bat 就好了。遇到字型太大无法生成的字体源码它会跳过，不用管那些错误信息，等到最后运行完就好。

# 源码
根据你的参数配置，每个字体大小会生成一个.c文件和一个.h文件都在 code 目录下。

# 使用
如果您还不会使用 u8g2 的话需要您自行研究一下，我这里就不多赘述了。基本就是引入你要使用的字型头文件，然后用这个字体就好了。。。。
```c
#include "u8g2_fontname_size_number.h"
U8G2_FOR_ADAFRUIT_GFX u8g2Fonts;

void setup(){
  display.init();
  display.setRotation(3);    
  u8g2Fonts.begin(display); 

  u8g2Fonts.setFont(u8g2_fontname_size_number);
  u8g2Fonts.drawUTF8(0, 0, "一些文字");

}

```

# font文件夹中的字体
font文件夹中的字体均下载自[造字工房](https://www.makefont.com/fonts.html)，bdf文件夹中生成的相关bdf字型文件和code文件夹中生成的相关.c/.h源文件仅供用于学习和参考使用。根据其[正版授权](https://www.makefont.com/authorization.html)中提及
```
造字工房所有字库及其单字的著作权均由著作权人和造字工房品牌所属机构所有。个人基于学习、研究或者欣赏目的，或任何基于公益目的，可以免费使用造字工房所有的字库及单字。未经依法授权，任何个人、企业及组织不得将造字工房字库及输出的单字用于任何商业目的或场景。
```
如您需要使用于商业场景，请自行与造字工房取得授权。


# 最后
有空了再写英文的Readme吧。。。估计需要这个工具的也多是中国人