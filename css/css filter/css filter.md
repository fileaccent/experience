现在规范中支持的效果有：

grayscale 灰度          值为0-1之间的小数 
sepia 褐色　　　　　　   值为0-1之间的小数
saturate 饱和度　　　　  值为num
hue-rotate 色相旋转　　  值为angle
invert 反色　　　　　　   值为0-1之间的小数
opacity 透明度　　　　　  值为0-1之间的小数
brightness 亮度　　　　   值为0-1之间的小数
contrast 对比度　　　　   值为num
blur 模糊　　　　　　     值为length
drop-shadow 阴影

用法是标准的CSS写法，如：

-webkit-filter: blur(2px);

测试浏览器为chrom浏览器44.0版本，示例图片中上方为原图，下方为加fifter效果后的图片。

grayscale灰度
　　如果使用该效果参数里没值的话将会以100%来渲染，取值0-1之间为不同的灰度。下面实例为100%的渲染：-webkit-filter:grayscale(1) ;



sepia
　　褐色，就是美图秀秀里有个怀旧功能的那种效果，取值也是0-1，-webkit-filter:sepia(1) ;



saturate饱和度
　　该属性改变图片的饱和度，取值范围为数字即可，默认值100%，示例为800%：-webkit-saturate(6) ;



hue-rotate色相旋转
　　hue-rotate用来改变图片的色相，默认值为0deg，取值为angle，示例：-webkit-filter:hue-rotate(180deg) 



invert反色
　　invert的效果就和照片底片有点相似，示例：-webkit-filter:invert(1) 



opacity透明度
　　这个属性经常遇到，示例：-webkit-filter:opacity(0.3)

 

brightness亮度
　　改变图片的亮度，默认值为100%，示例：-webkit-filter:brightness(0.5) 



contrast对比度
　　这个属性取值和饱和度saturate类似，示例500%：-webkit-filter:contrast(5) 



blur模糊
　　这个属性改变图片的清晰度，默认值为0，示例：-webkit-filter:blur(1px) 



drop-shadow阴影
　　这个类似于box-shadow，给图片加阴影，示例：-webkit-filter:drop-shadow(10px 10px 10px #000)



当然，添加多个属性也是可以的，示例：-webkit-filter:saturate(10) hue-rotate(500deg) grayscale(0.3) sepia(0.7) contrast(2.5) invert(0.2) brightness(1.2);

就先这么多了，ie低版本的滤镜效果下次再讨论。