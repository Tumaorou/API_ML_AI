# 哼唱识曲文档
## 许烨臻
## 清单
* [初版PRD文档链接](https://github.com/Tumaorou/API_ML_AI/blob/master/PRD.md)
* [产品原型展示页面](https://tumaorou.github.io/API_ML_AI/#g=1&p=%E9%A6%96%E9%A1%B5)
* [Axure原型文件下载](https://github.com/Tumaorou/API_ML_AI/blob/gh-pages/rp/%E5%93%BC%E5%94%B1%E8%AF%86%E6%9B%B2.rp?raw=true)
* [jupyter代码展示](https://github.com/Tumaorou/API_ML_AI/blob/master/API_ML_AI.ipynb)
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
* [搜狗语音识别产品与竞品准确率对比评估报告](https://max.book118.com/html/2017/0528/109819187.shtm)中显示，**百度语音识别**的准确率可排实验对象的前三，至于为什么不用排名第一的讯飞，详情见**API2.使用比较分析**和**API3.使用后风险报告**
* 百度官方宣称
  > 百度语音识别为开发者提供业界优质且免费的语音服务，通过场景识别优化，为车载导航，智能家居和社交聊天等行业提供语音解决方案，`准确率达到90%`以上，让您的应用绘“声”绘色
* __可导致识别失败的因素和如何解决__
  1. 用户会用外语、方言或者普通话口音重。
      - 百度语音识别可识别多种语言（方言），若能让人工智能分辨语言就能解决。
  2. 用户会念（记）错歌词，如[知乎提问](https://www.zhihu.com/question/297225697/answer/508864493)。
      - 通过**机器学习**提升识别准确度，或依赖现有的语音识别API，实测百度语音识别在用户说：“不愿做努力的人们。”能够把“努力”识别为“奴隶”。
### PRD5.需求列表与人工智能API加值
| **Title**   |    **User story**   |  **Importance**|     **Notes**    |
| ------------- | ------------- |------------- |------------- |
| 读出歌曲任意歌词识曲 | 用户读出歌曲的一两句歌词，当然读的越多越好 | 非常重要 | 产品改进的核心功能 |
| 直接读出歌名识曲 | 用户在哼唱识曲中直接读出歌名，识别出歌曲 | 不重要 | 音乐软件通常自带搜索，用户知道了歌名再哼唱识曲显得多此一举，但加上并不会增加用户的操作 |
| 读出歌手的名字精准识曲 | 用户在录音中读出歌手的名字，返回的结果是该歌手的该首歌 | 重要 | 大部分歌曲有不止一个歌手的版本 |
| 识别普通话以外的歌曲 | 识别外语歌和方言歌 | 非常重要 | |

* **需求项**
  1. 读出歌曲任意歌词识曲
      - 运用**百度语音识别**识别出用户唱出的歌词后，用**网易云API**搜索获取歌曲播放地址。
  2. 读出歌手的名字精准识曲
      - 运用**百度语音识别**识别出用户的语音后，再用**词法分析**将歌词和歌手名分离，最后用**网易云API**可得出精确结果。
  3. 识别普通话以外的歌曲
      - **百度语音识别**支持普通话，英语，粤语，四川话等。 

## 二、原型
### 原型1.交互及界面设计
* 可进入[产品原型展示页面](https://tumaorou.github.io/API_ML_AI/#g=1&p=%E9%A6%96%E9%A1%B5)体验交互
1. 首页，用户可在此页面进行录音。

	<img src="https://raw.githubusercontent.com/Tumaorou/API_ML_AI/master/img/%E9%A6%96%E9%A1%B5.PNG" alt="首页" width="35%">
	
2. 识别成功/识别失败，识别成功进入成功页面显示识别出的歌曲，识别失败则列出最有可能的三首歌。

	<img src="https://raw.githubusercontent.com/Tumaorou/API_ML_AI/master/img/%E8%AF%86%E5%88%AB%E6%88%90%E5%8A%9F.PNG" alt="识别成功" width="35%"><img src="https://raw.githubusercontent.com/Tumaorou/API_ML_AI/master/img/%E8%AF%86%E5%88%AB%E5%A4%B1%E8%B4%A5.PNG" alt="识别失败" width="35%" align="right">

3. 播放，在成功或失败页面点击歌曲进入播放页面

	<img src="https://raw.githubusercontent.com/Tumaorou/API_ML_AI/master/img/%E6%92%AD%E6%94%BE.PNG" alt="播放" width="35%">

### 原型2.信息设计
### 原型3.原型文档
* [产品原型展示页面](https://tumaorou.github.io/API_ML_AI/#g=1&p=%E9%A6%96%E9%A1%B5)
* [Axure原型文件下载](https://github.com/Tumaorou/API_ML_AI/blob/gh-pages/rp/%E5%93%BC%E5%94%B1%E8%AF%86%E6%9B%B2.rp?raw=true)
### 原型4.口头操作说明

## 三、API 产品使用关键AI或机器学习之API的输出入展示
### API1.使用水平
* [jupyter代码展示](https://github.com/Tumaorou/API_ML_AI/blob/master/API_ML_AI.ipynb)
* API运作流程图

	<img src="https://raw.githubusercontent.com/Tumaorou/API_ML_AI/master/img/API%E8%BF%90%E4%BD%9C%E6%B5%81%E7%A8%8B%E5%9B%BE.jpg" alt="API运作流程图" width="80%">

| 输入 | 输出 | API |
| ------------- | ------------- | ------------- |
| 用户录制的音频 | 识别出的文字 | 百度语音识别 |
| 用户录制的音频 | 歌曲名称 | 讯飞听歌识曲 |
| 识别出的文字 | 歌曲ID | 网易云搜索 |
| 歌曲ID | 歌曲音频 | 网易云播放 |

### API2.使用比较分析
### API3.使用后风险报告
### API4.加分项
