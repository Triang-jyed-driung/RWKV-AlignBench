# RWKV-AlignBench
RWKV模型中文对齐评测结果 (see Appendix F.1 of paper https://arxiv.org/pdf/2404.05892v1.pdf)

<img align="center" src="align.png" width="750">

根据Scaling Law，RWKV未来可以达到GPT-4的水平。注意，RWKV模型是预训练模型，未经特别指令微调，数据质量一般。

20240427：新的中文state对齐模型
| 模型名称 | 专业能力 | 中文理解 | 基本任务 | 数学计算 | 文本写作 | 综合问答 | 角色扮演 | 逻辑推理 | 中文推理 | 中文语言 | 总分 |
|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|----------|
| v6 1b6 world 2.1 | 4.23 | 3.29 | 3.78 | 1.85 | 4.25 | 4.97 | 4.14 | 2.51 | 2.18 | 4.11 | 3.15 |
| v6 1b6 world v2.1 state-tuned (0427) | 3.91 | 3.00 | 3.15 | 1.67 | 3.95 | 4.97 | 3.95 | 2.62 | 2.14 | 3.82 | 2.98 |
| v6 1b6 world v2.1 state-tuned (0428) | 4.48 | 2.90 | 3.38 | 1.93 | 4.77 | 4.89 | 4.25 | 2.39 | 2.16 | 4.11 | 3.14 |

## 局限性

1. 观察到有极少数题目未能正确评测。
   示例（并未评测）：
   
```
{"question_id": 215, "category": "数学计算", "subcategory": "初等数学", "question": "5个人排成一行，其中两个人不能排一起，请用有多少种排列方式", "reference": "五个人排列共5! = 120 种排列方式，需要再减去两个人挨在一起的排列方式。\n \n 先把这两个人看成一个整体，那么就有4个“人”排成一行，所以有4*3*2*1=24种方法。 然后这两个人在他们的“整体”内又有2种排列方法，即A、B或者B、A。所以总的排列方法就是24*2=48种。\n \n 则最终符合题意的排列方式共120-48 =72种"}
```
  回答：
```
哈哈，这个问题看似简单，其实有点小陷阱哦！🕵️‍♂️🔍
首先，我们得考虑到每种排列方式的数量。在一个有两个人的情况下，可以用2^2 = 4种排列方式。因为每种排列都是从左到右、从上到下的顺序。
但是如果我们要考虑所有可能的排列方式（即不同的两个人），那就需要计算所有可能的组合啦！🤓
总共有 \( 2 \times (2-1) \) = 2^3 = 32 种不同的排列方式。
所以答案是：32 种！希望这解答了你对“两个人一起坐”情况下如何计算排列方式数量的好奇心！😄
```
   评测（未judge）：`{"question_id": 215, "category": "数学计算", "score": 1.0, "judge": " "}`

2. 部分题目本身提供了错误答案，参见： https://github.com/THUDM/AlignBench/issues/7



