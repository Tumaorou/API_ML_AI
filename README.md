# 哼唱识曲文档
## 许烨臻
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
* [《搜狗语音识别产品与竞品准确率对比评估报告》](https://max.book118.com/html/2017/0528/109819187.shtm)中显示，**百度语音识别**的准确率可排实验对象的前三，至于为什么不用排名第一的讯飞，详情见**API2.使用比较分析**和**API3.使用后风险报告**
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
* API运作流程图

	<img src="https://raw.githubusercontent.com/Tumaorou/API_ML_AI/master/img/API%E8%BF%90%E4%BD%9C%E6%B5%81%E7%A8%8B%E5%9B%BE.jpg" alt="API运作流程图" width="80%">

### 原型3.原型文档
* [产品原型展示页面](https://tumaorou.github.io/API_ML_AI/#g=1&p=%E9%A6%96%E9%A1%B5)
* [Axure原型文件下载](https://github.com/Tumaorou/API_ML_AI/blob/gh-pages/rp/%E5%93%BC%E5%94%B1%E8%AF%86%E6%9B%B2.rp?raw=true)
### 原型4.口头操作说明

## 三、API 产品使用关键AI或机器学习之API的输出入展示
### API1.使用水平
* [jupyter代码文件](https://github.com/Tumaorou/API_ML_AI/blob/master/API_ML_AI.ipynb)，展示了最基本的百度语音识别，科大讯飞语音听写和歌曲识别，以及网易云搜索等API的调用及简单的使用。
* [API运作流程图](https://raw.githubusercontent.com/Tumaorou/API_ML_AI/master/img/API%E8%BF%90%E4%BD%9C%E6%B5%81%E7%A8%8B%E5%9B%BE.jpg)

| 输入 | 输出 | API |
| ------------- | ------------- | ------------- |
| 用户录制的音频 | 识别出的文字 | 百度语音识别 |
| 用户录制的音频 | 歌曲名称 | 讯飞听歌识曲 |
| 识别出的文字 | 歌曲ID | 网易云搜索 |
| 歌曲ID | 歌曲音频 | 网易云播放 |

### API2.使用比较分析
* [jupyter代码展示](https://github.com/Tumaorou/API_ML_AI/blob/master/API_ML_AI.ipynb)（一手证据，API实际使用）
* [《使用比较分析文档》](https://github.com/Tumaorou/API_ML_AI/blob/master/API_compare.md)
* 通过比较使用方便程度，性价比，使用限制等方面分析得出使用百度语音识别，科大讯飞歌曲识别，网易云搜索等API。
### API3.使用后风险报告
#### 前景报告
* [**《2018年中国人工智能行业市场前景研究报告》**](http://www.askci.com/news/finance/20180330/151540120775_2.shtml)

| 类别 | 现在发展程度 | 未来前景 |
| --- | --- | --- |
| 语音识别 | 人工智能领域的一个重要分支 | 是目前主流研究的方向 |
| 歌曲识别 | 一种特殊的语音识别 | 实际应用广 |

* 综上所述，在语音识别以及它的实际应用上，占了目前人工智能市场的较大比重，发展前景良好。
#### 未来使用策略
| 产品 | 市场竞争程度 | 输入输出限制 | 价格 | 能否自己开发 |
| --- | --- | --- | --- | --- |
| 百度语音识别 | 非常强，有科大讯飞，三角兽等多家竞争对手 | 调用量无限制（QPS限制100） | 可免费使用 | 开发难度大，而且不成熟，尽量使用API |
| 讯飞歌曲识别 | 歌曲识别的接口很多，但开放使用的只找到讯飞一家 | 每日500次限额/只能设置5个IP地址进行调用 | 可免费使用 | 指纹比对的代码难度不大，但要依赖庞大的**数据库** |
| 网易云搜索 | 无官方API，只有民间的 | 无限制 | 完全免费 | 需要庞大的**数据库** |

* 综上所述，在数据库足够庞大的情况下，歌曲识别和音乐搜索可以自己开发代替API（[指纹比对教程](https://blog.csdn.net/sinat_38682860/article/details/80735513)），语音识别依然会用第三方API。
### API4.加分项

## 清单
* [初版PRD文档链接](https://github.com/Tumaorou/API_ML_AI/blob/master/PRD.md)
* [《搜狗语音识别产品与竞品准确率对比评估报告》](https://max.book118.com/html/2017/0528/109819187.shtm)
* [产品原型展示页面](https://tumaorou.github.io/API_ML_AI/#g=1&p=%E9%A6%96%E9%A1%B5)
* [Axure原型文件下载](https://github.com/Tumaorou/API_ML_AI/blob/gh-pages/rp/%E5%93%BC%E5%94%B1%E8%AF%86%E6%9B%B2.rp?raw=true)
* [jupyter代码展示](https://github.com/Tumaorou/API_ML_AI/blob/master/API_ML_AI.ipynb)
* [API运作流程图](https://raw.githubusercontent.com/Tumaorou/API_ML_AI/master/img/API%E8%BF%90%E4%BD%9C%E6%B5%81%E7%A8%8B%E5%9B%BE.jpg)
* [《使用比较分析文档》](https://github.com/Tumaorou/API_ML_AI/blob/master/API_compare.md)
* [《2018年中国人工智能行业市场前景研究报告》](http://www.askci.com/news/finance/20180330/151540120775_2.shtml)
* [指纹比对教程](https://blog.csdn.net/sinat_38682860/article/details/80735513)
