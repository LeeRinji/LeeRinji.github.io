---
title:  文本摘要/关键词TextRank算法视角下的政府工作报告变化
tags: 数据处理
---

## 背景

前段时间某外校同学联系我，问我是否存在“一个可以进行文本分析提取关键词的工具”，同学希望能够利用这种工具对政府工作报告进行词频分析，从而辅助判断其中重点提到了哪些政策内容。

这样的技术当然是存在的，其算法也有着相当的依据。同学希望解决的问题实际上是典型的文本摘要任务，我们是有现成的工具可以进行解决的。（详见[文本摘要/关键词TextRank算法的优化与思考一文](https://github.com/ArtistScript/FastTextRank)）

在完成关键词提取和文本摘要后，出于好奇心理，我简单地统计了2013-2020年间政府工作报告关键词和2005-2012年间政府工作报告关键词的差异，应当说结果非常有趣，不过出于种种原因考虑，我仅将部分结果展示如下：

## 部分结果展示
对2005-2020年共计16年的政府工作报告，我们使用TextRank算法对其完成关键词提取任务，对每年的政府工作报告文本都提取Top15关键词，并以2013年为界限比较前八年（共计120个）和后八年（同样为120个）的关键词差异。

我们枚举后八年出现次数比前八年中更多的关键词如下（相对出现更少的关键词没有列举），第二、四栏是两段时期这一关键词出现的频数差：

|关键词|频数差|关键词|频数差|
创新|5|经济|1
政府|2|有|1
增长|2|推动|2
企业|1|全面|2
基本|1|实现|1
实施|2|保障|1
促进|2|实现|1
完善|1|加快|1
疫情|1|-|-

可以看到，“创新”是这两段时期差异最大的关键词，实际上，这一词汇从来都不是2005-2013年我们对政府工作报告中提取得到的关键词。

另外，“建设”、“改革”、“发展”在2005-2020年间的每一年都在关键词的Top15中。

## 实现代码

代码实现是比较简单的。代码所需要的[数据](https://github.com/LeeRinji/Application_Of_TextRank_Algorithm)我则放在了Github上。总的来说，对本部分提供的代码和数据加以综合应用，能得到比上文展示的结果更多可以挖掘的信息。

在这一Github仓库上也有我所提供的历年来政府工作报告的关键句（每年10句）和关键词（每年15个）的提取结果（Res_10_Sentence.txt, Res_15_Word.txt），以供没有安装FastTextRank（如果numpy版本不对的话，装起来还挺麻烦的）的朋友参考使用。

### 文本摘要提取

```python 
from FastTextRank.FastTextRank4Sentence import FastTextRank4Sentence
import codecs
import datetime
import numpy as np
mod = FastTextRank4Sentence(use_w2v=False,tol=0.0001)
old_time = datetime.datetime.now()
file=open('Res_5_Sentence.txt','w',encoding='UTF-8')
for i in range(43):
    text = codecs.open(str(i + 1) + '.txt', 'r', encoding='UTF-8').read()
    print('摘要'+str(i+1978)+':')
    file.write('摘要'+str(i+1978)+':\n')
    old_time = datetime.datetime.now()
    a=mod.summarize(text, 5)
    for i in a:
        print(i)
        file.write(i+"\n\n")
        print("")
        file.write("\n")
    print("-----------------------------------------------------------------------")
    file.write("-----------------------------------------------------------------------\n")
    print("\n")
    file.write("\n\n\n")
file.close()
```

### 关键词提取

```python
from FastTextRank.FastTextRank4Word import FastTextRank4Word
import datetime
import numpy as np
mod = FastTextRank4Word(tol=0.0001,window=2)
old_time = datetime.datetime.now()
file=open('Res_10_Word.txt','w',encoding='UTF-8')
for i in range(43):
    text = codecs.open(str(i + 1) + '.txt', 'r', encoding='UTF-8').read()
    print('摘要'+str(i+1978)+':')
    file.write('摘要'+str(i+1978)+':\n')
    old_time = datetime.datetime.now()
    a=mod.summarize(text, 15)
    for i in a:
        print(i)
        file.write(i+" ")
        print("")
    print("-----------------------------------------------------------------------")
    file.write("\n-----------------------------------------------------------------------")
    print("\n")
    file.write("\n")
file.close()
```

### 关键词对比

```python
import collections
s = []
f  = open('Res_10_Word.txt','r',encoding='UTF-8') 
res=[[] for i in range(43)]
tmp=0
jl=0
for lines in f:
    tmp=tmp+1
    words=lines.split(' ')
    if tmp%3==2:
        for i in words:
            if i!='\n':
                res[jl].append(i)
        jl=jl+1
before=[]
after=[]
for i in range(27,35):
    for j in res[i]:
        before.append(j)
for i in range(35,43):
    for j in res[i]:
        after.append(j)
bf=collections.Counter(before)
af=collections.Counter(after)
print(bf)
print(af)
print(af-bf)
print(bf-af)
f.close()
```