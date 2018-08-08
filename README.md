# G-Reader
机器阅读理解(Machine Reading Comprehension)是指让机器阅读文本，然后回答和阅读内容相关的问题。“[2018机器阅读理解技术竞赛](http://mrc2018.cipsc.org.cn/)”由中国中文信息学会、中国计算机学会和百度公司联手举办，使用了百度提供的面向真实应用场景的大规模中文阅读理解数据集。

国内外1000多支队伍中BLEU-4评分排名第6， ROUGE-L评分排名第14。（未ensemble，未嵌入训练好的词向量，无dropout）


# 模型架构
针对一个问题，文档集里有多答案的情况非常普遍，我们认为‘一边提高某个答案作为答案的概率，另一边又降低其它答案作为答案的概率’是不合理的。

因此我们的模型采用先从每篇文章中独立抽取候选答案，再从候选答案集中抽取最佳答案的结构，以解决多答案致使神经网络难以学习的问题。架构的具体实现中，我们通过BiDAF+ Passage Self-Matching从单篇文章中抽取答案，构成候选答案集，再使用em和xgboost决策树从候选答案集中抽取最佳答案。

![image1](https://github.com/freefuiiismyname/G-Reader/blob/master/G-Reader-master/images-folder/1.png)
# 即模型分为以下两部分：
1、候选答案抽取层——BiDAF+Passage Self-Matching

2、答案选择层——em算法、xgboost 
# 关于数据
移步[比赛官网](http://mrc2018.cipsc.org.cn/)的数据下载页面，来自百度知道和搜索的真实场景数据集共包含30万问题，其中包括27万的训练集，1万开发集和2万测试集，分为4个部分供参赛用户下载。

Em算法部分包含了百度知道集的tfidf模型文件，只需下载百度知道的数据文件便可用java运行，暂未做python实现。它在整个模型（Bidaf抽取答案、xgboost决策答案）作为特征扩充，交互答案之间的信息。
# 算法效果
最终效果：

![image3](https://github.com/freefuiiismyname/G-Reader/blob/master/G-Reader-master/images-folder/3.png)

无监督EM算法效果：
![image2](https://github.com/freefuiiismyname/G-Reader/blob/master/G-Reader-master/images-folder/2.jpg)
# 致谢
本模型由华南理工大学的G-scuter团队完成。
致谢广州极天信息技术股份有限公司、华南理工大学软件学院。
