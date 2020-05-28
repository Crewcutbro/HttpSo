## AndServer+Service 打造 Android 服务器调用 so 文件
#### 参考：https://mp.weixin.qq.com/s/Do4rGrMNFGx5HqFKM9vA1g 
#### 代码：https://github.com/NightTeam/HttpSo 
##### 在此基础上实现调用抖音libcms.so和秒拍的libte.so
---
#### 2020.5.9
#### 调用秒拍7.2.70 libte.so的Decode方法解密response
#### 调用10.9.0抖音libcms.so生成0404开头x-gorgon
#### 我的用法： https://github.com/heyaug/sign-algorithms

##### 抖音
```python
# 完整
data={"url":url,"headers":headers}
gorgon=requests.post("http://127.0.0.1:8887/url",data=str(data)).text

# 简单
gorgon=requests.post("http://127.0.0.1:8887/url",data=url).text
ks=str(int(rticket/1000))

headers.update({"X-Gorgon":gorgon})
headers.update({"X-Khronos":ks})
requests.get(url,headers=headers).json()
```
##### 秒拍
```python
r=requests.get(url=url,headers=headers)
data=base64.b64encode(r.content).decode()
result=requests.post(url="http://127.0.0.1:8887/decode",data=data)
```