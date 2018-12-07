# 哼唱识曲文档
## 许烨臻
## [PRD文档链接](https://github.com/Tumaorou/API_ML_AI/blob/master/PRD.md)
------
# 实在细节
## 一、PRD
### PRD1.加值宣言
* 运用**语音识别**提升音乐软件**哼唱识曲**功能的成功率。
### PRD2.核心价值
* 通过用户朗读或唱出少量的歌词（一两句即可），识别出对应的歌曲。
### PRD3.核心价值与用户痛点
* 传统的哼唱识别（网易云音乐、QQ音乐等）通过[**指纹比对**](https://blog.csdn.net/sinat_38682860/article/details/80735513)识别歌曲，依赖用户唱出歌曲的曲调。
* 若用户无法哼唱出曲调（五音不全），传统的哼唱识别又无法识别歌词，成功识别歌曲的成功率低。
* 本产品通过**语音识别**可在用户唱不出曲调，能唱出歌词的情况下提升**哼唱识曲**的成功率。
### PRD4.人工智能概率性与用户痛点
* 可导致识别失败的因素和如何解决
  1. 用户会用外语、方言或者普通话口音重。
    - 百度语音识别可识别多种语言（方言），若能让人工智能分辨语言就能解决。
  2. 用户会念（记）错歌词，如[知乎提问](https://www.zhihu.com/question/297225697/answer/508864493)。
    - 通过**机器学习**提升识别准确度，或依赖现有的语音识别API，实测百度语音识别在用户说：“不愿做努力的人们。”能够把“努力”识别为“奴隶”。
### PRD5.需求列表与人工智能API加值
* 需求列表详情见[PRD文档](https://github.com/Tumaorou/API_ML_AI/blob/master/PRD.md)的Requirements。
* 需求项
  1. 读出歌曲任意歌词识曲
    - 运用**百度语音识别**识别出用户唱出的歌词后，用**网易云API**搜索获取歌曲播放地址。
  2. 读出歌手的名字精准识曲
    - 运用**百度语音识别**识别出用户的语音后，再用**词法分析**将歌词和歌手名分离，最后用**网易云API**可得出精确结果。
  3. 识别普通话以外的歌曲
    - **百度语音识别**支持普通话，英语，粤语，四川话等。 

## 二、原型
### 原型1.交互及界面设计
### 原型2.信息设计
### 原型3.原型文档
### 原型4.口头操作说明

## 三、API 产品使用关键AI或机器学习之API的输出入展示
### API1.使用水平
| 输入 | 输出 | API |
| ------------- | ------------- | ------------- |
| 用户录制的音频 | 识别出的文字 | 百度语音识别 |
| 识别出的文字 | 歌曲ID | 网易云搜索 |
| 歌曲ID | 歌曲音频 | 网易云播放 |

### API2.使用比较分析
### API3.使用后风险报告
### API4.加分项