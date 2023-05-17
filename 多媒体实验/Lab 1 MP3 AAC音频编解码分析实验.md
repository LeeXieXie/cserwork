# 实验1 ： MP3/AAC音频编解码分析实验
## 1 选择WAV格式音频
![image.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305152133953.png)
## 2 用MP3 编码进行压缩
我采用的是WinLame（Windows端软件），下载链接：[winLAME, free CD ripper and MP3 encoder using LAME](https://winlame.sourceforge.io/)
![image.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305152135366.png)

### 2.1 比特率设置
### 2.1.1 320kbps
![image.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305152135513.png)
![image.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305152135710.png)
![image.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305152143681.png)
### 2.1.1 128kbps
![image.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305152148479.png)
### 2.1.3 96kbps
![image.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305152148251.png)
## 2.2 分析压缩前后，比特率、压缩比、文件大小的关系
分析python代码
```
import os  
def get_file_size(file_path):  
# 获取文件大小（字节数）  
return os.stat(file_path).st_size  
def analyze_compression(input_file, output_file):  
# 获取压缩前文件大小  
original_size = get_file_size(input_file)  
  
# 获取压缩后文件大小  
compressed_size = get_file_size(output_file)  
  
# 计算压缩比  
compression_ratio = original_size / compressed_size  
  
# 打印结果  
print("原始文件大小->", input_file,":", original_size, "字节")  
print("压缩后文件大小->", output_file,":", compressed_size, "字节")  
print("压缩比->", compression_ratio)  
  
  
for i in range(1, 11):  
print(f"第 {i} 个音频文件：")  
  
input_file = f"D:\多媒体实验\Lab1\wav\{i}.wav" # 原始 WAV 文件路径  
  
# 320kbps 压缩  
print("MP3-320kbps")  
output_file = f"D:\多媒体实验\Lab1\wav\MP3_320kbps\{i}_320.mp3" # 压缩后 MP3 文件路径  
analyze_compression(input_file, output_file)  
print("AAC-320kbps")  
output_file = f"D:\多媒体实验\Lab1\wav\AAC_320kbps\{i}_320.aac" # 压缩后 MP3 文件路径  
analyze_compression(input_file, output_file)  
  
# 128kbps 压缩  
print("MP3-128kbps")  
output_file = f"D:\多媒体实验\Lab1\wav\MP3_128kbps\{i}_128.mp3" # 压缩后 MP3 文件路径  
analyze_compression(input_file, output_file)  
print("AAC-128kbps")  
output_file = f"D:\多媒体实验\Lab1\wav\AAC_128kbps\{i}_128.aac" # 压缩后 MP3 文件路径  
analyze_compression(input_file, output_file)  
  
# 96kbps 压缩  
print("MP3-96kbps")  
output_file = f"D:\多媒体实验\Lab1\wav\MP3_96kbps\{i}_96.mp3" # 压缩后 MP3 文件路径  
analyze_compression(input_file, output_file)  
print("AAC-96kbps")  
output_file = f"D:\多媒体实验\Lab1\wav\AAC_96kbps\{i}_96.aac" # 压缩后 MP3 文件路径  
analyze_compression(input_file, output_file)  
  
print() # 打印空行分隔不同音频文件的输出
```


```
第 1 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\1.wav : 960044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\1_320.mp3 : 392378 字节  
压缩比-> 2.4467324875502703  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\1.wav : 960044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\1_320.aac : 287364 字节  
压缩比-> 3.3408638521178715  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\1.wav : 960044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\1_128.mp3 : 191066 字节  
压缩比-> 5.024672102833576  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\1.wav : 960044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\1_128.aac : 164279 字节  
压缩比-> 5.843984928079669  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\1.wav : 960044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\1_96.mp3 : 144986 字节  
压缩比-> 6.621632433476336  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\1.wav : 960044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\1_96.aac : 123911 字节  
压缩比-> 7.747851280354448  
  
第 2 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\2.wav : 99244 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\2_320.mp3 : 44414 字节  
压缩比-> 2.2345206466429506  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\2.wav : 99244 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\2_320.aac : 46436 字节  
压缩比-> 2.13722112154363  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\2.wav : 99244 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\2_128.mp3 : 44486 字节  
压缩比-> 2.230904104662141  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\2.wav : 99244 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\2_128.aac : 42168 字节  
压缩比-> 2.35353822804022  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\2.wav : 99244 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\2_96.mp3 : 37574 字节  
压缩比-> 2.641294512162666  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\2.wav : 99244 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\2_96.aac : 33126 字节  
压缩比-> 2.995954839099197  
  
第 3 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\3.wav : 48198 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\3_320.mp3 : 23354 字节  
压缩比-> 2.0638006337244157  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\3.wav : 48198 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\3_320.aac : 22420 字节  
压缩比-> 2.149776984834969  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\3.wav : 48198 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\3_128.mp3 : 23426 字节  
压缩比-> 2.0574575258260053  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\3.wav : 48198 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\3_128.aac : 21243 字节  
压缩比-> 2.2688885750600196  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\3.wav : 48198 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\3_96.mp3 : 23498 字节  
压缩比-> 2.0511532896416718  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\3.wav : 48198 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\3_96.aac : 20550 字节  
压缩比-> 2.3454014598540147  
  
第 4 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\4.wav : 679450 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\4_320.mp3 : 286130 字节  
压缩比-> 2.374619928004753  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\4.wav : 679450 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\4_320.aac : 224499 字节  
压缩比-> 3.026516821901211  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\4.wav : 679450 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\4_128.mp3 : 112408 字节  
压缩比-> 6.04449861219842  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\4.wav : 679450 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\4_128.aac : 120114 字节  
压缩比-> 5.656709459346954  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\4.wav : 679450 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\4_96.mp3 : 82734 字节  
压缩比-> 8.212464041385646  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\4.wav : 679450 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\4_96.aac : 91820 字节  
压缩比-> 7.399803964277935  
  
第 5 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\5.wav : 70700 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\5_320.mp3 : 32858 字节  
压缩比-> 2.151682999573924  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\5.wav : 70700 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\5_320.aac : 36739 字节  
压缩比-> 1.9243855303628297  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\5.wav : 70700 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\5_128.mp3 : 32786 字节  
压缩比-> 2.1564082230220216  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\5.wav : 70700 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\5_128.aac : 35045 字节  
压缩比-> 2.0174061920388073  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\5.wav : 70700 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\5_96.mp3 : 32786 字节  
压缩比-> 2.1564082230220216  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\5.wav : 70700 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\5_96.aac : 33939 字节  
压缩比-> 2.083149179410118  
  
第 6 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\6.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\6_320.mp3 : 35810 字节  
压缩比-> 2.1744764032393187  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\6.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\6_320.aac : 41215 字节  
压缩比-> 1.8893121436370253  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\6.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\6_128.mp3 : 35594 字节  
压缩比-> 2.1876720795639715  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\6.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\6_128.aac : 39483 字节  
压缩比-> 1.9721905630271257  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\6.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\6_96.mp3 : 35594 字节  
压缩比-> 2.1876720795639715  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\6.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\6_96.aac : 38347 字节  
压缩比-> 2.030615171982163  
  
第 7 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\7.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\7_320.mp3 : 35522 字节  
压缩比-> 2.192106300320928  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\7.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\7_320.aac : 40119 字节  
压缩比-> 1.94092574590593  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\7.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\7_128.mp3 : 35378 字节  
压缩比-> 2.2010288880094975  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\7.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\7_128.aac : 38441 字节  
压缩比-> 2.025649696938165  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\7.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\7_96.mp3 : 35378 字节  
压缩比-> 2.2010288880094975  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\7.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\7_96.aac : 37450 字节  
压缩比-> 2.079252336448598  
  
第 8 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\8.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\8_320.mp3 : 35954 字节  
压缩比-> 2.1657673694164767  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\8.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\8_320.aac : 39741 字节  
压缩比-> 1.9593870310258927  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\8.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\8_128.mp3 : 35810 字节  
压缩比-> 2.1744764032393187  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\8.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\8_128.aac : 38020 字节  
压缩比-> 2.048079957916886  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\8.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\8_96.mp3 : 35810 字节  
压缩比-> 2.1744764032393187  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\8.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\8_96.aac : 36971 字节  
压缩比-> 2.1061913391577183  
  
第 9 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\9.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\9_320.mp3 : 1117385 字节  
压缩比-> 2.368068302330889  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\9.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\9_320.aac : 1294607 字节  
压缩比-> 2.043897491671218  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\9.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\9_128.mp3 : 928859 字节  
压缩比-> 2.8487036245544264  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\9.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\9_128.aac : 985409 字节  
压缩比-> 2.6852241049148122  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\9.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\9_96.mp3 : 705397 字节  
压缩比-> 3.7511415557480396  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\9.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\9_96.aac : 745063 字节  
压缩比-> 3.551436589925953  
  
第 10 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\10.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\10_320.mp3 : 1093818 字节  
压缩比-> 2.419089830300836  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\10.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\10_320.aac : 904314 字节  
压缩比-> 2.926023482993739  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\10.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\10_128.mp3 : 887606 字节  
压缩比-> 2.9811019754260335  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\10.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\10_128.aac : 863178 字节  
压缩比-> 3.0654673775281576  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\10.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\10_96.mp3 : 656250 字节  
压缩比-> 4.032067047619048  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\10.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\10_96.aac : 711422 字节  
压缩比-> 3.7193733114803873
```

## 3 使用AAC进行压缩
我采用的是FAAC，[FAAC Freeware AAC Codec](https://faac.sourceforge.net/)
对于wav的处理我写了一个bat脚本进行批处理
```
@echo off
chcp 65001 > nul
setlocal

set "input_dir=D:\多媒体实验\Lab1\wav"
set "output_dir=D:\多媒体实验\Lab1\wav"

for /L %%i in (1,1,10) do (
    echo 转码文件 %%i.wav ...
	.\faac.exe -b 320 "%input_dir%\%%i.wav" -o "%output_dir%\%%i_320.aac"
	.\faac.exe -b 128 "%input_dir%\%%i.wav" -o "%output_dir%\%%i_128.aac"	
	.\faac.exe -b 96 "%input_dir%\%%i.wav" -o "%output_dir%\%%i_96.aac"
)

echo 转码完成！

endlocal

```
### 3.1 分析压缩前后，比特率、压缩比、文件大小的关系

```
第 1 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\1.wav : 960044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\1_320.mp3 : 392378 字节  
压缩比-> 2.4467324875502703  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\1.wav : 960044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\1_320.aac : 287364 字节  
压缩比-> 3.3408638521178715  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\1.wav : 960044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\1_128.mp3 : 191066 字节  
压缩比-> 5.024672102833576  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\1.wav : 960044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\1_128.aac : 164279 字节  
压缩比-> 5.843984928079669  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\1.wav : 960044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\1_96.mp3 : 144986 字节  
压缩比-> 6.621632433476336  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\1.wav : 960044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\1_96.aac : 123911 字节  
压缩比-> 7.747851280354448  
  
第 2 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\2.wav : 99244 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\2_320.mp3 : 44414 字节  
压缩比-> 2.2345206466429506  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\2.wav : 99244 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\2_320.aac : 46436 字节  
压缩比-> 2.13722112154363  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\2.wav : 99244 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\2_128.mp3 : 44486 字节  
压缩比-> 2.230904104662141  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\2.wav : 99244 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\2_128.aac : 42168 字节  
压缩比-> 2.35353822804022  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\2.wav : 99244 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\2_96.mp3 : 37574 字节  
压缩比-> 2.641294512162666  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\2.wav : 99244 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\2_96.aac : 33126 字节  
压缩比-> 2.995954839099197  
  
第 3 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\3.wav : 48198 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\3_320.mp3 : 23354 字节  
压缩比-> 2.0638006337244157  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\3.wav : 48198 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\3_320.aac : 22420 字节  
压缩比-> 2.149776984834969  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\3.wav : 48198 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\3_128.mp3 : 23426 字节  
压缩比-> 2.0574575258260053  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\3.wav : 48198 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\3_128.aac : 21243 字节  
压缩比-> 2.2688885750600196  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\3.wav : 48198 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\3_96.mp3 : 23498 字节  
压缩比-> 2.0511532896416718  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\3.wav : 48198 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\3_96.aac : 20550 字节  
压缩比-> 2.3454014598540147  
  
第 4 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\4.wav : 679450 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\4_320.mp3 : 286130 字节  
压缩比-> 2.374619928004753  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\4.wav : 679450 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\4_320.aac : 224499 字节  
压缩比-> 3.026516821901211  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\4.wav : 679450 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\4_128.mp3 : 112408 字节  
压缩比-> 6.04449861219842  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\4.wav : 679450 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\4_128.aac : 120114 字节  
压缩比-> 5.656709459346954  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\4.wav : 679450 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\4_96.mp3 : 82734 字节  
压缩比-> 8.212464041385646  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\4.wav : 679450 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\4_96.aac : 91820 字节  
压缩比-> 7.399803964277935  
  
第 5 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\5.wav : 70700 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\5_320.mp3 : 32858 字节  
压缩比-> 2.151682999573924  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\5.wav : 70700 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\5_320.aac : 36739 字节  
压缩比-> 1.9243855303628297  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\5.wav : 70700 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\5_128.mp3 : 32786 字节  
压缩比-> 2.1564082230220216  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\5.wav : 70700 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\5_128.aac : 35045 字节  
压缩比-> 2.0174061920388073  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\5.wav : 70700 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\5_96.mp3 : 32786 字节  
压缩比-> 2.1564082230220216  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\5.wav : 70700 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\5_96.aac : 33939 字节  
压缩比-> 2.083149179410118  
  
第 6 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\6.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\6_320.mp3 : 35810 字节  
压缩比-> 2.1744764032393187  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\6.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\6_320.aac : 41215 字节  
压缩比-> 1.8893121436370253  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\6.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\6_128.mp3 : 35594 字节  
压缩比-> 2.1876720795639715  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\6.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\6_128.aac : 39483 字节  
压缩比-> 1.9721905630271257  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\6.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\6_96.mp3 : 35594 字节  
压缩比-> 2.1876720795639715  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\6.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\6_96.aac : 38347 字节  
压缩比-> 2.030615171982163  
  
第 7 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\7.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\7_320.mp3 : 35522 字节  
压缩比-> 2.192106300320928  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\7.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\7_320.aac : 40119 字节  
压缩比-> 1.94092574590593  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\7.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\7_128.mp3 : 35378 字节  
压缩比-> 2.2010288880094975  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\7.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\7_128.aac : 38441 字节  
压缩比-> 2.025649696938165  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\7.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\7_96.mp3 : 35378 字节  
压缩比-> 2.2010288880094975  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\7.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\7_96.aac : 37450 字节  
压缩比-> 2.079252336448598  
  
第 8 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\8.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\8_320.mp3 : 35954 字节  
压缩比-> 2.1657673694164767  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\8.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\8_320.aac : 39741 字节  
压缩比-> 1.9593870310258927  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\8.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\8_128.mp3 : 35810 字节  
压缩比-> 2.1744764032393187  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\8.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\8_128.aac : 38020 字节  
压缩比-> 2.048079957916886  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\8.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\8_96.mp3 : 35810 字节  
压缩比-> 2.1744764032393187  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\8.wav : 77868 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\8_96.aac : 36971 字节  
压缩比-> 2.1061913391577183  
  
第 9 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\9.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\9_320.mp3 : 1117385 字节  
压缩比-> 2.368068302330889  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\9.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\9_320.aac : 1294607 字节  
压缩比-> 2.043897491671218  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\9.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\9_128.mp3 : 928859 字节  
压缩比-> 2.8487036245544264  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\9.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\9_128.aac : 985409 字节  
压缩比-> 2.6852241049148122  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\9.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\9_96.mp3 : 705397 字节  
压缩比-> 3.7511415557480396  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\9.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\9_96.aac : 745063 字节  
压缩比-> 3.551436589925953  
  
第 10 个音频文件：  
MP3-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\10.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_320kbps\10_320.mp3 : 1093818 字节  
压缩比-> 2.419089830300836  
AAC-320kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\10.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_320kbps\10_320.aac : 904314 字节  
压缩比-> 2.926023482993739  
MP3-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\10.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_128kbps\10_128.mp3 : 887606 字节  
压缩比-> 2.9811019754260335  
AAC-128kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\10.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_128kbps\10_128.aac : 863178 字节  
压缩比-> 3.0654673775281576  
MP3-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\10.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\MP3_96kbps\10_96.mp3 : 656250 字节  
压缩比-> 4.032067047619048  
AAC-96kbps  
原始文件大小-> D:\多媒体实验\Lab1\wav\10.wav : 2646044 字节  
压缩后文件大小-> D:\多媒体实验\Lab1\wav\AAC_96kbps\10_96.aac : 711422 字节  
压缩比-> 3.7193733114803873
```
## 4 解码MP3和AAC
我采用python的库来进行解码，pydub库将MP3和AAC解码为WAV,代码如下：
```python
import os  
from pydub import AudioSegment  
  
def decode_mp3_to_wav(mp3_file, wav_file):  
# 将MP3文件解码为WAV文件  
audio = AudioSegment.from_mp3(mp3_file)  
audio.export(wav_file, format='wav')  
  
def decode_aac_to_wav(aac_file, wav_file):  
# 将AAC文件解码为WAV文件  
audio = AudioSegment.from_file(aac_file, format='aac')  
audio.export(wav_file, format='wav')  
def decode(rate):  
  
for i in range(1, 11):  
print(f"第 {i} 个音频文件：")  
  
output_dir_mp3 = fr"D:\多媒体实验\Lab1\wav\decode\MP3_{rate}kbps" # 目标目录路径  
if not os.path.exists(output_dir_mp3):  
os.makedirs(output_dir_mp3)  
output_file = os.path.join(output_dir_mp3, f"{i}_{rate}.wav") # 压缩后 MP3 文件路径  
mp3_file = f"D:\多媒体实验\Lab1\wav\MP3_{rate}kbps\{i}_{rate}.mp3" # MP3文件路径  
print(f"MP3-{rate}kbps->", mp3_file)  
decode_mp3_to_wav(mp3_file, output_file)  
print("MP3解码完成！")  
  
output_dir_aac = fr"D:\多媒体实验\Lab1\wav\decode\AAC_{rate}kbps" # 目标目录路径  
if not os.path.exists(output_dir_aac):  
os.makedirs(output_dir_aac)  
output_file = os.path.join(output_dir_aac, f"{i}_{rate}.wav") # 压缩后 MP3 文件路径  
aac_file = f"D:\多媒体实验\Lab1\wav\AAC_{rate}kbps\{i}_{rate}.aac" # AAC文件路径  
print(f"AAC-{rate}kbps->", aac_file)  
decode_aac_to_wav(aac_file, output_file)  
print("AAC解码完成！")  
  
print("MP3解码：320kbps")  
decode(320)  
print("MP3解码：320kbps finish！")  
print("MP3解码：128kbps")  
decode(128)  
print("MP3解码：128kbps finish！")  
print("MP3解码：96kbps")  
decode(96)  
print("MP3解码：96kbps finish！")
```

```txt
MP3解码：320kbps  
第 1 个音频文件：  
MP3-320kbps-> D:\多媒体实验\Lab1\wav\MP3_320kbps\1_320.mp3  
MP3解码完成！  
AAC-320kbps-> D:\多媒体实验\Lab1\wav\AAC_320kbps\1_320.aac  
AAC解码完成！  
第 2 个音频文件：  
MP3-320kbps-> D:\多媒体实验\Lab1\wav\MP3_320kbps\2_320.mp3  
MP3解码完成！  
AAC-320kbps-> D:\多媒体实验\Lab1\wav\AAC_320kbps\2_320.aac  
AAC解码完成！  
第 3 个音频文件：  
MP3-320kbps-> D:\多媒体实验\Lab1\wav\MP3_320kbps\3_320.mp3  
MP3解码完成！  
AAC-320kbps-> D:\多媒体实验\Lab1\wav\AAC_320kbps\3_320.aac  
AAC解码完成！  
第 4 个音频文件：  
MP3-320kbps-> D:\多媒体实验\Lab1\wav\MP3_320kbps\4_320.mp3  
MP3解码完成！  
AAC-320kbps-> D:\多媒体实验\Lab1\wav\AAC_320kbps\4_320.aac  
AAC解码完成！  
第 5 个音频文件：  
MP3-320kbps-> D:\多媒体实验\Lab1\wav\MP3_320kbps\5_320.mp3  
MP3解码完成！  
AAC-320kbps-> D:\多媒体实验\Lab1\wav\AAC_320kbps\5_320.aac  
AAC解码完成！  
第 6 个音频文件：  
MP3-320kbps-> D:\多媒体实验\Lab1\wav\MP3_320kbps\6_320.mp3  
MP3解码完成！  
AAC-320kbps-> D:\多媒体实验\Lab1\wav\AAC_320kbps\6_320.aac  
AAC解码完成！  
第 7 个音频文件：  
MP3-320kbps-> D:\多媒体实验\Lab1\wav\MP3_320kbps\7_320.mp3  
MP3解码完成！  
AAC-320kbps-> D:\多媒体实验\Lab1\wav\AAC_320kbps\7_320.aac  
AAC解码完成！  
第 8 个音频文件：  
MP3-320kbps-> D:\多媒体实验\Lab1\wav\MP3_320kbps\8_320.mp3  
MP3解码完成！  
AAC-320kbps-> D:\多媒体实验\Lab1\wav\AAC_320kbps\8_320.aac  
AAC解码完成！  
第 9 个音频文件：  
MP3-320kbps-> D:\多媒体实验\Lab1\wav\MP3_320kbps\9_320.mp3  
MP3解码完成！  
AAC-320kbps-> D:\多媒体实验\Lab1\wav\AAC_320kbps\9_320.aac  
AAC解码完成！  
第 10 个音频文件：  
MP3-320kbps-> D:\多媒体实验\Lab1\wav\MP3_320kbps\10_320.mp3  
MP3解码完成！  
AAC-320kbps-> D:\多媒体实验\Lab1\wav\AAC_320kbps\10_320.aac  
AAC解码完成！  
MP3解码：320kbps finish！  
MP3解码：128kbps  
第 1 个音频文件：  
MP3-128kbps-> D:\多媒体实验\Lab1\wav\MP3_128kbps\1_128.mp3  
MP3解码完成！  
AAC-128kbps-> D:\多媒体实验\Lab1\wav\AAC_128kbps\1_128.aac  
AAC解码完成！  
第 2 个音频文件：  
MP3-128kbps-> D:\多媒体实验\Lab1\wav\MP3_128kbps\2_128.mp3  
MP3解码完成！  
AAC-128kbps-> D:\多媒体实验\Lab1\wav\AAC_128kbps\2_128.aac  
AAC解码完成！  
第 3 个音频文件：  
MP3-128kbps-> D:\多媒体实验\Lab1\wav\MP3_128kbps\3_128.mp3  
MP3解码完成！  
AAC-128kbps-> D:\多媒体实验\Lab1\wav\AAC_128kbps\3_128.aac  
AAC解码完成！  
第 4 个音频文件：  
MP3-128kbps-> D:\多媒体实验\Lab1\wav\MP3_128kbps\4_128.mp3  
MP3解码完成！  
AAC-128kbps-> D:\多媒体实验\Lab1\wav\AAC_128kbps\4_128.aac  
AAC解码完成！  
第 5 个音频文件：  
MP3-128kbps-> D:\多媒体实验\Lab1\wav\MP3_128kbps\5_128.mp3  
MP3解码完成！  
AAC-128kbps-> D:\多媒体实验\Lab1\wav\AAC_128kbps\5_128.aac  
AAC解码完成！  
第 6 个音频文件：  
MP3-128kbps-> D:\多媒体实验\Lab1\wav\MP3_128kbps\6_128.mp3  
MP3解码完成！  
AAC-128kbps-> D:\多媒体实验\Lab1\wav\AAC_128kbps\6_128.aac  
AAC解码完成！  
第 7 个音频文件：  
MP3-128kbps-> D:\多媒体实验\Lab1\wav\MP3_128kbps\7_128.mp3  
MP3解码完成！  
AAC-128kbps-> D:\多媒体实验\Lab1\wav\AAC_128kbps\7_128.aac  
AAC解码完成！  
第 8 个音频文件：  
MP3-128kbps-> D:\多媒体实验\Lab1\wav\MP3_128kbps\8_128.mp3  
MP3解码完成！  
AAC-128kbps-> D:\多媒体实验\Lab1\wav\AAC_128kbps\8_128.aac  
AAC解码完成！  
第 9 个音频文件：  
MP3-128kbps-> D:\多媒体实验\Lab1\wav\MP3_128kbps\9_128.mp3  
MP3解码完成！  
AAC-128kbps-> D:\多媒体实验\Lab1\wav\AAC_128kbps\9_128.aac  
AAC解码完成！  
第 10 个音频文件：  
MP3-128kbps-> D:\多媒体实验\Lab1\wav\MP3_128kbps\10_128.mp3  
MP3解码完成！  
AAC-128kbps-> D:\多媒体实验\Lab1\wav\AAC_128kbps\10_128.aac  
AAC解码完成！  
MP3解码：128kbps finish！  
MP3解码：96kbps  
第 1 个音频文件：  
MP3-96kbps-> D:\多媒体实验\Lab1\wav\MP3_96kbps\1_96.mp3  
MP3解码完成！  
AAC-96kbps-> D:\多媒体实验\Lab1\wav\AAC_96kbps\1_96.aac  
AAC解码完成！  
第 2 个音频文件：  
MP3-96kbps-> D:\多媒体实验\Lab1\wav\MP3_96kbps\2_96.mp3  
MP3解码完成！  
AAC-96kbps-> D:\多媒体实验\Lab1\wav\AAC_96kbps\2_96.aac  
AAC解码完成！  
第 3 个音频文件：  
MP3-96kbps-> D:\多媒体实验\Lab1\wav\MP3_96kbps\3_96.mp3  
MP3解码完成！  
AAC-96kbps-> D:\多媒体实验\Lab1\wav\AAC_96kbps\3_96.aac  
AAC解码完成！  
第 4 个音频文件：  
MP3-96kbps-> D:\多媒体实验\Lab1\wav\MP3_96kbps\4_96.mp3  
MP3解码完成！  
AAC-96kbps-> D:\多媒体实验\Lab1\wav\AAC_96kbps\4_96.aac  
AAC解码完成！  
第 5 个音频文件：  
MP3-96kbps-> D:\多媒体实验\Lab1\wav\MP3_96kbps\5_96.mp3  
MP3解码完成！  
AAC-96kbps-> D:\多媒体实验\Lab1\wav\AAC_96kbps\5_96.aac  
AAC解码完成！  
第 6 个音频文件：  
MP3-96kbps-> D:\多媒体实验\Lab1\wav\MP3_96kbps\6_96.mp3  
MP3解码完成！  
AAC-96kbps-> D:\多媒体实验\Lab1\wav\AAC_96kbps\6_96.aac  
AAC解码完成！  
第 7 个音频文件：  
MP3-96kbps-> D:\多媒体实验\Lab1\wav\MP3_96kbps\7_96.mp3  
MP3解码完成！  
AAC-96kbps-> D:\多媒体实验\Lab1\wav\AAC_96kbps\7_96.aac  
AAC解码完成！  
第 8 个音频文件：  
MP3-96kbps-> D:\多媒体实验\Lab1\wav\MP3_96kbps\8_96.mp3  
MP3解码完成！  
AAC-96kbps-> D:\多媒体实验\Lab1\wav\AAC_96kbps\8_96.aac  
AAC解码完成！  
第 9 个音频文件：  
MP3-96kbps-> D:\多媒体实验\Lab1\wav\MP3_96kbps\9_96.mp3  
MP3解码完成！  
AAC-96kbps-> D:\多媒体实验\Lab1\wav\AAC_96kbps\9_96.aac  
AAC解码完成！  
第 10 个音频文件：  
MP3-96kbps-> D:\多媒体实验\Lab1\wav\MP3_96kbps\10_96.mp3  
MP3解码完成！  
AAC-96kbps-> D:\多媒体实验\Lab1\wav\AAC_96kbps\10_96.aac  
AAC解码完成！  
MP3解码：96kbps finish！
```

## 5 比较解码后音频的质量
采用python代码
```python
import pesq  
  
def calculate_audio_quality(reference_file, degraded_file, rate):  
# 计算音频质量得分  
quality_score = pesq.pesq(reference_file, degraded_file, 'wb', rate)  
return quality_score  
  
def score(rate):  
for i in range(1, 11):  
print(f"第 {i} 个音频文件：")  
  
reference_file = f"D:\多媒体实验\Lab1\wav\{i}.wav" # 原始音频文件路径  
decode_mp3_file = f"D:\多媒体实验\Lab1\wav\decode\MP3_{rate}kbps\{i}_{rate}.wav" # 使用MP3解码后的音频文件路径  
decode_aac_file = f"D:\多媒体实验\Lab1\wav\decode\AAC_{rate}kbps\{i}_{rate}.wav" # 使用AAC解码后的音频文件路径  
  
  
mp3_quality = calculate_audio_quality(reference_file, decode_mp3_file, rate)  
aac_quality = calculate_audio_quality(reference_file, decode_aac_file, rate)  
  
print(f"Decode_MP3_{rate}音频质量得分：", mp3_quality)  
print(f"Decode_AAC_{rate}音频质量得分：", aac_quality)  
  
score(320)  
score(128)  
score(96)
```