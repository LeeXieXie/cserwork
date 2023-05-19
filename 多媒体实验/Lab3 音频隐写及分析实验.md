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

