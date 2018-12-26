# 使用对比分析
## 语音识别
### 产品对比
* 开发文档
  * 百度语音识别：https://ai.baidu.com/docs#/ASR-API/top
  * 科大讯飞语音听写：https://doc.xfyun.cn/rest_api/%E8%AF%AD%E9%9F%B3%E5%90%AC%E5%86%99.html

| 对比项\产品 | 百度语音识别 | 科大讯飞语音听写 |
| --- | --- | --- |
| 费用 | 可免费使用 | 可免费使用 |
| 限额 | 无调用量限制 | 每日500次限额 |
| 准确率（两者对比） | 低 | 高 |
| 方言或其它语音支持度（两者对比） | 少 | 多 |
| 有无SDK | 有 | 无 |
| 有无自定义词条 | 有 | 无 |
| 其它限制 | 无 | 只可设置5个IP地址使用 |

### 代码展示
```
# 百度语音识别
def speech_recognition(filePath):
    APP_ID = ''
    API_KEY = ''
    SECRET_KEY = ''

    client = AipSpeech(APP_ID, API_KEY, SECRET_KEY)
    
    with open(filePath, 'rb') as fp:
        return client.asr(fp.read(), 'wav', 16000, {'dev_pid': 1536,})
```
```
# 科大讯飞语音听写
def speech_recognition():
    f = open("myrecord.wav", 'rb')
    file_content = f.read()
    base64_audio = base64.b64encode(file_content)
    body = urllib.parse.urlencode({'audio': base64_audio})
 
    url = 'http://api.xfyun.cn/v1/service/v1/iat'
    api_key = ''
    param = {"engine_type": "sms16k", "aue": "raw"}
 
    x_appid = ''
    x_param = base64.b64encode(json.dumps(param).replace(' ', '').encode('utf-8'))
    x_param = str(x_param, 'utf-8')
 
    x_time = int(int(round(time.time() * 1000)) / 1000)
    x_checksum = hashlib.md5((api_key + str(x_time) + x_param).encode('utf-8')).hexdigest()
    x_header = {'X-Appid': x_appid,
                'X-CurTime': x_time,
                'X-Param': x_param,
                'X-CheckSum': x_checksum}

    req = urllib.request.Request(url = url, data = body.encode('utf-8'), headers = x_header, method = 'POST')
    result = urllib.request.urlopen(req)
    result = result.read().decode('utf-8')
    return result
```

* 由上可得，科大讯飞和百度语音识别均可免费使用
* 科大讯飞的产品成熟度要优于百度。
* 使用方便程度百度提供SDK，在代码复杂程度上要优于科大讯飞。
* 百度的使用限制要优于科大讯飞，讯飞只可设置5个IP地址，而且设置后5分钟才能生效，免费版使用并不方便。
* 值得注意的细节是，科大讯飞返回的识别结果中包含**标点符号**，而百度则没有，对于歌词搜索来说，有标点符号并不是好事。
* 故选择**百度语音识别**。

## 歌曲识别
* 目前市面上支持歌曲识别的API并不多，能找到的只有**科大讯飞的歌曲识别**，仅此一家。
* 科大讯飞歌曲识别开发文档：https://doc.xfyun.cn/rest_api/%E6%AD%8C%E6%9B%B2%E8%AF%86%E5%88%AB.html
* 虽然科大讯飞的产品有诸多限制，但无其它竞品。

### 代码展示
```
def song_recognition(filePath):
    url = ''
    api_key = ''
    param = {"engine_type": "afs", "aue": "raw", "sample_rate": "16000"}
 
    x_appid = '5c0b2a6f'
    x_param = base64.b64encode(json.dumps(param).replace(' ', '').encode('utf-8'))

    x_param = str(x_param, 'utf-8')
 
    x_time = int(int(round(time.time() * 1000)) / 1000)
    x_checksum = hashlib.md5((api_key + str(x_time) + x_param).encode('utf-8')).hexdigest()
    x_header = {'X-Appid': x_appid,
                'X-CurTime': str(x_time),
                'X-Param': x_param,
                'X-CheckSum': x_checksum}

    with open(filePath, 'rb') as file:
        r = requests.post(url = url, data = file.read(), headers = x_header)
    return json.loads(r.content.decode('utf-8'))
```

## 歌曲搜索
* API提供网易云音乐和QQ音乐两家的歌曲下载，由于不是官方API，所以选择相对使用人数较多的**网易云搜索**。
* 开发文档：https://www.bzqll.com/2018/10/39.html
### 代码展示
```
def search_song(wd):
    payload = {'key': '579621905', 's': wd, 'limit': 5}
    r = requests.get('https://api.bzqll.com/music/netease/search', params=payload)
    return r.json()

def download_song(search_result):
    url = 'https://api.bzqll.com/music/netease/url?key=579621905&br=128000'+'&id='+search_result['data'][0]['id']
    r = requests.get(url) 
    with open("song\%s.mp3"%search_result['data'][0]['name'], "wb") as code:
        code.write(r.content)
```
