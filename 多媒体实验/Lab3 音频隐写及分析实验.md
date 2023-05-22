***姓名：李效宇
学号：202228013329004***
# 实验3：音频隐写及分析实验
## 1 选择WAV格式音频
![](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305191528153.png)
## 2 实现LSBR、LSBM 算法
### 2.1 LSBR
```python
import wave  
  
# LSBR算法（WAV）  
def lsbr_wav_hide(audio_path, message, index):  
# 打开WAV文件  
audio = wave.open(audio_path, 'rb')  
# 读取WAV文件的内容  
audio_data = bytearray(list(audio.readframes(audio.getnframes())))  
  
# 将消息转换为二进制字符串  
binary_message = ''.join(format(ord(c), '08b') for c in message)  
  
# 检查消息长度是否超过音频容量  
if len(binary_message) > len(audio_data):  
raise ValueError("消息长度超过音频容量。")  
  
# 将消息隐藏在音频数据中  
for i, bit in enumerate(binary_message):  
audio_data[i] = (audio_data[i] & 254) | int(bit)  
  
# 创建一个新的WAV文件，将隐藏了消息的音频数据写入其中  
new_audio = wave.open(fr"lsbr_encrypted_audio{index}.wav", 'wb')  
new_audio.setparams(audio.getparams())  
new_audio.writeframes(audio_data)  
new_audio.close()  
audio.close()  
  
# LSBR算法（WAV）  
def lsbr_wav_extract(audio_path):  
# 打开WAV文件  
audio = wave.open(audio_path, 'rb')  
# 读取WAV文件的内容  
audio_data = audio.readframes(audio.getnframes())  
  
# 提取隐藏的消息  
binary_message = ''  
for byte in audio_data:  
binary_message += str(byte & 1)  
  
# 将二进制消息转换为字符  
message = ''  
for i in range(0, len(binary_message), 8):  
byte = binary_message[i:i+8]  
message += chr(int(byte, 2))  
  
audio.close()  
message = message.split('!')[0]  
return message  
  
  
# 隐藏消息（WAV）  
for i in range(1, 6):  
message = f"Hello LSBR, put {i} in {i}.wav!"  
lsbr_wav_hide(fr"{i}.wav", message, i)  
  
# 提取消息（WAV）  
for i in range(1, 6):  
extracted_message_wav = lsbr_wav_extract(f"lsbr_encrypted_audio{i}.wav")  
print(f"第{i}个音频文件：" + f"lsbr_encrypted_audio{i}.wav")  
print("提取的WAV消息：", extracted_message_wav)
```

### 2.2 LSBM
```python
import wave  
  
# LSBM算法（WAV）  
def lsbm_wav_hide(audio_path, message, index):  
# 打开WAV文件  
audio = wave.open(audio_path, 'rb')  
# 读取WAV文件的内容  
audio_data = bytearray(list(audio.readframes(audio.getnframes())))  
  
# 将消息转换为二进制字符串  
binary_message = ''.join(format(ord(c), '08b') for c in message)  
  
# 检查消息长度是否超过音频容量  
if len(binary_message) > len(audio_data):  
raise ValueError("消息长度超过音频容量。")  
  
# 将消息隐藏在音频数据中  
for i, bit in enumerate(binary_message):  
audio_data[i] = (audio_data[i] & 254) | int(bit)  
  
# 创建一个新的WAV文件，将隐藏了消息的音频数据写入其中  
new_audio = wave.open(f"lsbm_encrypted_audio{index}.wav", 'wb')  
new_audio.setparams(audio.getparams())  
new_audio.writeframes(audio_data)  
new_audio.close()  
audio.close()  
  
# LSBM算法（WAV）  
def lsbm_wav_extract(audio_path):  
# 打开WAV文件  
audio = wave.open(audio_path, 'rb')  
# 读取WAV文件的内容  
audio_data = bytearray(list(audio.readframes(audio.getnframes())))  
  
# 提取隐藏的消息  
binary_message = ''  
for byte in audio_data:  
binary_message += str(byte & 1)  
  
# 将二进制消息转换为字符  
message = ''  
for i in range(0, len(binary_message), 8):  
byte = binary_message[i:i+8]  
message += chr(int(byte, 2))  
  
audio.close()  
message = message.split('!')[0]  
return message  
  
  
# 隐藏消息（WAV）  
for i in range(1, 6):  
message = f"Hello LBSM, put {i} in {i}.wav!"  
lsbm_wav_hide(fr"{i}.wav", message, i)  
  
# 提取消息（WAV）  
for i in range(1, 6):  
extracted_message_wav = lsbm_wav_extract(f"lsbm_encrypted_audio{i}.wav")  
print(f"第{i}个音频文件：" + f"lsbm_encrypted_audio{i}.wav")  
print("提取的WAV消息：", extracted_message_wav)
```

## 2.3 比较LSBR和LSBM的直方图
绘制直方图源代码：
```python
import wave  
import numpy as np  
import matplotlib.pyplot as plt  
  
# 绘制直方图比较  
for i in range(1, 6):  
# 读取原始音频文件  
audio = wave.open(fr"{i}.wav", 'rb')  
audio_data = audio.readframes(audio.getnframes())  
audio.close()  
audio_data = np.frombuffer(audio_data, dtype=np.uint8)  
  
# 读取LSBR加密后的音频文件  
audio_lsbr = wave.open(fr"lsbr_encrypted_audio{i}.wav", 'rb')  
audio_lsbr_data = audio_lsbr.readframes(audio_lsbr.getnframes())  
audio_lsbr.close()  
audio_lsbr_data = np.frombuffer(audio_lsbr_data, dtype=np.uint8)  
  
# 读取LSBM加密后的音频文件  
audio_lsbm = wave.open(fr"lsbm_encrypted_audio{i}.wav", 'rb')  
audio_lsbm_data = audio_lsbm.readframes(audio_lsbm.getnframes())  
audio_lsbm.close()  
audio_lsbm_data = np.frombuffer(audio_lsbm_data, dtype=np.uint8)  
  
# 绘制直方图  
plt.hist(audio_data, bins=256, density=1, facecolor='blue', alpha=0.5, label=f'Original{i}')  
plt.hist(audio_lsbr_data, bins=256, density=1, facecolor='red', alpha=0.5, label=f'LSBR{i}')  
plt.hist(audio_lsbm_data, bins=256, density=1, facecolor='green', alpha=0.5, label=f'LSBM{i}')  
plt.legend()  
plt.savefig(f"{i}.png")  
plt.show()  
plt.close()
```
1.wav
![1.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305192216778.png)
2.wav
![2.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305192216323.png)
3.wav 
![3.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305192216621.png)
4.wav
![4.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305192217936.png)
5.wav
![5.png](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305192217250.png)
## 3 使用MP3Stego隐写软件
写入信息采用python代码进行批处理
```python
import subprocess  
  
for i in range(1, 6):  
print(f"第{i}个音频文件：" + f"{i}.wav")  
filename = "D:\多媒体实验\Lab3\MP3Stego_1_1_19\hidden_text.txt"  
# 打开文件并读取内容  
with open(filename, "r") as file:  
content = file.read()  
  
# 打印文件内容  
print("将被写入的内容：", content)  
  
command = fr"D:\多媒体实验\Lab3\MP3Stego_1_1_19\Encode.exe -E D:\多媒体实验\Lab3\MP3Stego_1_1_19\hidden_text.txt -P pass D:\多媒体实验\Lab3\{i}.wav D:\多媒体实验\Lab3\{i}_h.wav"  
# 执行命令  
subprocess.run(command, shell=True)  
print(f"第{i}个音频文件加密完成！")
```

执行结果如下：
```bash
第1个音频文件：1.wav
将被写入的内容： Hello MP3Stego

MP3StegoEncoder 1.1.19
See README file for copyright info
Microsoft RIFF, WAVE audio, PCM, stereo 44100Hz 16bit, Length:  0: 0:40
MPEG-I layer III, stereo  Psychoacoustic Model: AT&T
Bitrate=128 kbps  De-emphasis: none  CRC: off  
Encoding "D:\��ý��ʵ��\Lab3\1.wav" to "D:\��ý��ʵ��\Lab3\1_h.wav"
Hiding "D:\��ý��ʵ��\Lab3\MP3Stego_1_1_19\hidden_text.txt"
[Frame   1531 of   1531] (100.00%) Finished in  0: 0: 0
第1个音频文件加密完成！
第2个音频文件：2.wav
将被写入的内容： Hello MP3Stego

MP3StegoEncoder 1.1.19
See README file for copyright info
Microsoft RIFF, WAVE audio, PCM, stereo 44100Hz 16bit, Length:  0: 0:40
MPEG-I layer III, stereo  Psychoacoustic Model: AT&T
Bitrate=128 kbps  De-emphasis: none  CRC: off  
Encoding "D:\��ý��ʵ��\Lab3\2.wav" to "D:\��ý��ʵ��\Lab3\2_h.wav"
Hiding "D:\��ý��ʵ��\Lab3\MP3Stego_1_1_19\hidden_text.txt"
[Frame   1531 of   1531] (100.00%) Finished in  0: 0: 0
第2个音频文件加密完成！
第3个音频文件：3.wav
将被写入的内容： Hello MP3Stego

MP3StegoEncoder 1.1.19
See README file for copyright info
Microsoft RIFF, WAVE audio, PCM, stereo 44100Hz 16bit, Length:  0: 0:40
MPEG-I layer III, stereo  Psychoacoustic Model: AT&T
Bitrate=128 kbps  De-emphasis: none  CRC: off  
Encoding "D:\��ý��ʵ��\Lab3\3.wav" to "D:\��ý��ʵ��\Lab3\3_h.wav"
Hiding "D:\��ý��ʵ��\Lab3\MP3Stego_1_1_19\hidden_text.txt"
[Frame   1531 of   1531] (100.00%) Finished in  0: 0: 0
第3个音频文件加密完成！
第4个音频文件：4.wav
将被写入的内容： Hello MP3Stego

MP3StegoEncoder 1.1.19
See README file for copyright info
Microsoft RIFF, WAVE audio, PCM, stereo 44100Hz 16bit, Length:  0: 0:40
MPEG-I layer III, stereo  Psychoacoustic Model: AT&T
Bitrate=128 kbps  De-emphasis: none  CRC: off  
Encoding "D:\��ý��ʵ��\Lab3\4.wav" to "D:\��ý��ʵ��\Lab3\4_h.wav"
Hiding "D:\��ý��ʵ��\Lab3\MP3Stego_1_1_19\hidden_text.txt"
[Frame   1531 of   1531] (100.00%) Finished in  0: 0: 0
第4个音频文件加密完成！
第5个音频文件：5.wav
将被写入的内容： Hello MP3Stego

MP3StegoEncoder 1.1.19
See README file for copyright info
Microsoft RIFF, WAVE audio, PCM, stereo 44100Hz 16bit, Length:  0: 0:40
MPEG-I layer III, stereo  Psychoacoustic Model: AT&T
Bitrate=128 kbps  De-emphasis: none  CRC: off  
Encoding "D:\��ý��ʵ��\Lab3\5.wav" to "D:\��ý��ʵ��\Lab3\5_h.wav"
Hiding "D:\��ý��ʵ��\Lab3\MP3Stego_1_1_19\hidden_text.txt"
[Frame   1531 of   1531] (100.00%) Finished in  0: 0: 0
第5个音频文件加密完成！

```


## 4  比较嵌入消息、提取消息的内容
### 4.1 提取消息
#### LSBR
```bash
第1个音频文件：lsbr_encrypted_audio1.wav
提取的WAV消息： Hello LSBR, put 1 in 1.wav
第2个音频文件：lsbr_encrypted_audio2.wav
提取的WAV消息： Hello LSBR, put 2 in 2.wav
第3个音频文件：lsbr_encrypted_audio3.wav
提取的WAV消息： Hello LSBR, put 3 in 3.wav
第4个音频文件：lsbr_encrypted_audio4.wav
提取的WAV消息： Hello LSBR, put 4 in 4.wav
第5个音频文件：lsbr_encrypted_audio5.wav
提取的WAV消息： Hello LSBR, put 5 in 5.wav
```
#### LSBM
```bash
第1个音频文件：lsbm_encrypted_audio1.wav
提取的WAV消息： Hello LBSM, put 1 in 1.wav
第2个音频文件：lsbm_encrypted_audio2.wav
提取的WAV消息： Hello LBSM, put 2 in 2.wav
第3个音频文件：lsbm_encrypted_audio3.wav
提取的WAV消息： Hello LBSM, put 3 in 3.wav
第4个音频文件：lsbm_encrypted_audio4.wav
提取的WAV消息： Hello LBSM, put 4 in 4.wav
第5个音频文件：lsbm_encrypted_audio5.wav
提取的WAV消息： Hello LBSM, put 5 in 5.wav
```

#### MP3Stego
提取消息代码
```python
import subprocess  
  
for i in range(1, 6):  
print(f"第{i}个音频文件：" + f"{i}_h.wav")  
command = fr"D:\多媒体实验\Lab3\MP3Stego_1_1_19\Decode.exe -X -P pass D:\多媒体实验\Lab3\{i}_h.wav D:\多媒体实验\Lab3\{i}_h.wav.pcm"  
# 执行命令  
print(command)  
subprocess.run(command, shell=True)  
print(f"第{i}个音频文件解密完成！")  
filename = fr"D:\多媒体实验\Lab3\{i}_h.wav.txt"  
# 打开文件并读取内容  
with open(filename, "r") as file:  
content = file.read()  
  
print("提取的消息：", content)  
print()
```

```bash
第1个音频文件：1_h.wav
D:\多媒体实验\Lab3\MP3Stego_1_1_19\Decode.exe -X -P pass D:\多媒体实验\Lab3\1_h.wav D:\多媒体实验\Lab3\1_h.wav.pcm
Input file = 'D:\��ý��ʵ��\Lab3\1_h.wav'  output file = 'D:\��ý��ʵ��\Lab3\1_h.wav.pcm'
Will attempt to extract hidden information. Output: D:\��ý��ʵ��\Lab3\1_h.wav.txt
the bit stream file D:\��ý��ʵ��\Lab3\1_h.wav is a BINARY file
HDR: s=FFF, id=1, l=3, ep=off, br=9, sf=0, pd=1, pr=0, m=0, js=0, c=0, o=0, e=0
alg.=MPEG-1, layer=III, tot bitrate=128, sfrq=44.1
mode=stereo, sblim=32, jsbd=32, ch=2
MP3StegoEncoder 1.1.19
See README file for copyright info
[Frame 1531]Avg slots/frame = 417.688; b/smp = 2.90; br = 127.917 kbps
Decoding of "D:\��ý��ʵ��\Lab3\1_h.wav" is finished
The decoded PCM output file name is "D:\��ý��ʵ��\Lab3\1_h.wav.pcm"
第1个音频文件解密完成！
提取的消息： Hello MP3Stego


第2个音频文件：2_h.wav
D:\多媒体实验\Lab3\MP3Stego_1_1_19\Decode.exe -X -P pass D:\多媒体实验\Lab3\2_h.wav D:\多媒体实验\Lab3\2_h.wav.pcm
Input file = 'D:\��ý��ʵ��\Lab3\2_h.wav'  output file = 'D:\��ý��ʵ��\Lab3\2_h.wav.pcm'
Will attempt to extract hidden information. Output: D:\��ý��ʵ��\Lab3\2_h.wav.txt
the bit stream file D:\��ý��ʵ��\Lab3\2_h.wav is a BINARY file
HDR: s=FFF, id=1, l=3, ep=off, br=9, sf=0, pd=1, pr=0, m=0, js=0, c=0, o=0, e=0
alg.=MPEG-1, layer=III, tot bitrate=128, sfrq=44.1
mode=stereo, sblim=32, jsbd=32, ch=2
MP3StegoEncoder 1.1.19
See README file for copyright info
[Frame 1531]Avg slots/frame = 417.688; b/smp = 2.90; br = 127.917 kbps
Decoding of "D:\��ý��ʵ��\Lab3\2_h.wav" is finished
The decoded PCM output file name is "D:\��ý��ʵ��\Lab3\2_h.wav.pcm"
第2个音频文件解密完成！
提取的消息： Hello MP3Stego


第3个音频文件：3_h.wav
D:\多媒体实验\Lab3\MP3Stego_1_1_19\Decode.exe -X -P pass D:\多媒体实验\Lab3\3_h.wav D:\多媒体实验\Lab3\3_h.wav.pcm
MP3StegoEncoder 1.1.19
See README file for copyright info
[Frame   50]Input file = 'D:\��ý��ʵ��\Lab3\3_h.wav'  output file = 'D:\��ý��ʵ��\Lab3\3_h.wav.pcm'
Will attempt to extract hidden information. Output: D:\��ý��ʵ��\Lab3\3_h.wav.txt
the bit stream file D:\��ý��ʵ��\Lab3\3_h.wav is a BINARY file
HDR: s=FFF, id=1, l=3, ep=off, br=9, sf=0, pd=1, pr=0, m=0, js=0, c=0, o=0, e=0
alg.=MPEG-1, layer=III, tot bitrate=128, sfrq=44.1
mode=stereo, sblim=32, jsbd=32, ch=2
[Frame 1531]Avg slots/frame = 417.688; b/smp = 2.90; br = 127.917 kbps
Decoding of "D:\��ý��ʵ��\Lab3\3_h.wav" is finished
The decoded PCM output file name is "D:\��ý��ʵ��\Lab3\3_h.wav.pcm"
第3个音频文件解密完成！
提取的消息： Hello MP3Stego


第4个音频文件：4_h.wav
D:\多媒体实验\Lab3\MP3Stego_1_1_19\Decode.exe -X -P pass D:\多媒体实验\Lab3\4_h.wav D:\多媒体实验\Lab3\4_h.wav.pcm
MP3StegoEncoder 1.1.19
See README file for copyright info
[Frame   48]Input file = 'D:\��ý��ʵ��\Lab3\4_h.wav'  output file = 'D:\��ý��ʵ��\Lab3\4_h.wav.pcm'
Will attempt to extract hidden information. Output: D:\��ý��ʵ��\Lab3\4_h.wav.txt
the bit stream file D:\��ý��ʵ��\Lab3\4_h.wav is a BINARY file
HDR: s=FFF, id=1, l=3, ep=off, br=9, sf=0, pd=1, pr=0, m=0, js=0, c=0, o=0, e=0
alg.=MPEG-1, layer=III, tot bitrate=128, sfrq=44.1
mode=stereo, sblim=32, jsbd=32, ch=2
[Frame 1531]Avg slots/frame = 417.688; b/smp = 2.90; br = 127.917 kbps
Decoding of "D:\��ý��ʵ��\Lab3\4_h.wav" is finished
The decoded PCM output file name is "D:\��ý��ʵ��\Lab3\4_h.wav.pcm"
第4个音频文件解密完成！
提取的消息： Hello MP3Stego


第5个音频文件：5_h.wav
D:\多媒体实验\Lab3\MP3Stego_1_1_19\Decode.exe -X -P pass D:\多媒体实验\Lab3\5_h.wav D:\多媒体实验\Lab3\5_h.wav.pcm
MP3StegoEncoder 1.1.19
See README file for copyright info
[Frame   49]Input file = 'D:\��ý��ʵ��\Lab3\5_h.wav'  output file = 'D:\��ý��ʵ��\Lab3\5_h.wav.pcm'
Will attempt to extract hidden information. Output: D:\��ý��ʵ��\Lab3\5_h.wav.txt
the bit stream file D:\��ý��ʵ��\Lab3\5_h.wav is a BINARY file
HDR: s=FFF, id=1, l=3, ep=off, br=9, sf=0, pd=1, pr=0, m=0, js=0, c=0, o=0, e=0
alg.=MPEG-1, layer=III, tot bitrate=128, sfrq=44.1
mode=stereo, sblim=32, jsbd=32, ch=2
[Frame 1531]Avg slots/frame = 417.688; b/smp = 2.90; br = 127.917 kbps
Decoding of "D:\��ý��ʵ��\Lab3\5_h.wav" is finished
The decoded PCM output file name is "D:\��ý��ʵ��\Lab3\5_h.wav.pcm"
第5个音频文件解密完成！
提取的消息： Hello MP3Stego
```

**经过对比可知与我们写入的信息一致！**


![](https://wanwurong.oss-cn-beijing.aliyuncs.com/picgo/202305230004206.png)