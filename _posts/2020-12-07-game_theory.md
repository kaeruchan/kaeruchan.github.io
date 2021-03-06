---
title: 浅谈博弈论（Game theory）
author: Kaeruchan
date: 2020-12-07 09:44:00 +0900
categories: [Security, Game theory]
tags: [Game theory]
math: true
---

# 前言

博弈论英文叫“game theory”，目前属于经济学一个分支。
收到世人瞩目的原因是因为这个单独的学科，适用于任何
明显有竞争对抗成分在里面的场景。
我第一次接触到这块也是因为参与了安全性问题的探讨而
学习到这部分知识。

这个理论专门研究多个个体之间对抗行为（竞争行为）。
所以某些叫法也有叫“对策论 or 赛局理论”。

---

# 博弈论的起源

在开始，我们先聊一下"博弈论"的发展史。

要开始这个话题，约翰·冯·诺伊曼（John von Neumann）
是个怎么样都绕不过去的人物。

![约翰·冯·诺伊曼](https://imgur.com/nrwodGm.jpg)

此人是个**超级跨界牛人**，
就算用了那么夸张的称呼，
依然不足以体现这个人的牛逼之处——
他同时在“数学，物理学，经济学，计算机”等
多个领域作出了划时代的贡献，并且留下了一大堆以他命名的东西。
比如：程序员都应该听说过的“冯诺伊曼体系”，
数学领域的“冯诺伊曼代数、冯诺伊曼便历定理…”，
物理领域的“冯诺伊曼量子测量，冯诺伊曼熵，冯诺伊曼方程…”。
另外还有很多东西，
虽然不是以他的名字命名，也是他先发现的，
比如：量子力学的公理化表述，
希尔伯特第五问题，
连续几何（其空间维数不是整数），
蒙特卡洛仿真方法，
归并排序算法…

1944年，他与奥斯卡·摩根斯坦（Oskar Morgenstern）
合作发表了《[博弈论与经济行为](https://press.princeton.edu/books/paperback/9780691130613/theory-of-games-and-economic-behavior)》
（英语“Theory of Games and Economic Behavior”），
一举奠定博弈论体系的基础，
所以他也被称作“博弈论之父”。

这个《博弈论与经济行为》一开始是以论文形式写成，
长达1200页，基本上是冯·诺曼依一个人的手笔。
有些朋友会误会——那为什么摩根斯坦能当第二作者啊？
这里面大致有2个原因：
其一，摩根斯坦本人非常看好“博弈领域的研究”，
他认为：该领域的研究可以为一切经济学理论建立正确的基础。
当他解释了大牛知乎，就一直劝说大牛写该领域的论文；
其二，当大牛完成上千页的论文之后，
摩根斯坦为这篇论文补了一个非常有煽动性的"绪论"，
是的这篇论文一发表就在数学界和经济学界产生轰动效果。
所以把摩根斯坦列为第二作者，也算说得过去。

另外，这本《博弈论与经济行为》的某些思想，
源自冯·诺伊曼在1928年发表的论文
《On the Theory of Parlor Games》。
因此有些学者认为1928年才是真正意义上的博弈论诞生之年。

---

# 博弈的类型

“博弈的类型”是博弈论的基本概念，先来聊这个。

---

## 合作博弈（cooperative game） VS 非合作博弈（non-cooperative game）

无论是“合作博弈”or“非合作博弈”，在博弈过程中都可能会出现“合作的”现象。差别在于——<br>
对于“合作博弈”，存在某种【外部约束力】，使得“背叛”的行为会受到这种外部约束力的惩罚。<br>
对于“非合作博弈”，【没有】上述这种“外部约束力”，对“背叛”的惩罚只能依靠博弈过程的其他参与者。

距离：商业活动中有“合同法”，就相当于上述所说的【外部约束力】。
通常所说的“博弈”大都指“【非】合作博弈”。大多数博弈论的研究也是针对后者（非合作），本文大部分内容也是针对后者。

---

## 同时博弈（simultaneous game） VS 顺序博弈（sequential game）

### 同时博弈（静态博弈）

“同时博弈”有时也称作“静态博弈”，指的是博弈的【任何一个】参与者在选择自己的行为之前，
并【不】知道其他参与者的行为信息。

举例：“石头/剪刀/布”

### 顺序博弈（动态博弈）

“顺序博弈”有时也称作“动态博弈”。
在这类博弈中，参与者的动作有【时间上的先后】，
并且后一个执行动作的博弈者可以看到其他博弈者之前的动作，然后根据别人的动作，思考自己的行为。

举例：绝大部分棋牌类游戏都属于这种。

---

## 零和博弈（zero-sum game） VS 非零和博弈（non-zero-sum game）

### 零和博弈

“零和博弈”这个名称具有误导性，使得很多人以为各方的收益总和为零。
“零和博弈”指的是——在博弈结束之后，参与各方的利益总和为【常量】
（可以是零，也可以是“正值”或“负值”）。
举例：大多数棋类游戏属于这种；“石头/剪刀/布”也属于这种。

### 非零和博弈（变和博弈）

“非零和博弈”指的是——在博弈结束之后，参与各方的利益总和为【变量】。所以这类博弈有时候称为【变和博弈】。
对于这类博弈，在某些情况下可能会让参与各方的利益总和【变大】，从而使得各方存在【合作】的可能性。
举例：在“非零和博弈”中，最有名的应该就是“囚徒困境”（*Prisoner's Dilemma*）了。
这个“困境”非常有名，这里就不详细解释啦。不太了解的同学，先看俺加注的维基百科链接。因为后续的讨论中，会多次提及这个模型。

---

## 非重复博弈（non-repeated game） VS 重复博弈（repeated game）

“非重复博弈”有时也称作“单次博弈”；相应的，“重复博弈”也被称作“多次博弈”。

以“囚徒困境”为例。如果困境中的两个嫌疑人只被抓进去一次，那就是“单次博弈”；如果被抓进去不止一次，就是“多次博弈”。

“重复博弈”还可以进一步细分为“有限重复博弈”（finite repeated game）与“无限重复博弈”（infinite repeated game）。

这2个术语容易产生歧义。更严谨的说法是：

“有限重复博弈”——重复次数【确定】的博弈

“无限重复博弈”——重复次数【不确定】的博弈

---

# 收益矩阵 VS 决策树

## 概述

这两个指标都是为了更为直观的描述博弈过程，并帮你看清各方利弊的得失。

“收益矩阵”通常用来描述“静态博弈”（同时博弈）；由于“动态博弈”（顺序博弈）的场景较为复杂，通常【不用】“收益矩阵”描述。

“决策树”既可以用作描述“静态博弈”，也可以用来描述“动态博弈”。

顺便提醒一下：

在某些书籍/文章中，把“收益矩阵”称为“普通形式”（normal-form），把“决策树”称为“扩展形式”（extensive-form）。

---

## 收益矩阵（payoff matrix）

上一个小节说了：“收益矩阵”通常用来描述【静态博弈】。而且一般是用来描述【双人】的静态博弈。
更多人的静态博弈，虽说也可以用“收益矩阵”来描述，但是画起来会麻烦很多。
在本文的后续部分，
凡提及“收益矩阵”都是指“双人静态博弈”。
通常的惯例是把自己这方的策略写在表格【左边】，
把对方的策略写在表格【上边】。
下面以“石头/剪刀/布”为例，收益矩阵的表述可以为下图：

<center>
	<table border>
		<tbody>
			<tr>
				<td></td>
				<td>石头</td>
				<td>剪刀</td>
				<td>布</td>
			</tr>
			<tr>
				<td>石头</td>
				<td>0</td>
				<td>1</td>
				<td>-1</td>
			</tr>
			<tr>
				<td>剪刀</td>
				<td>-1</td>
				<td>0</td>
				<td>1</td>
			</tr>
			<tr>
				<td>布</td>
				<td>1</td>
				<td>-1</td>
				<td>0</td>
			</tr>
		</tbody>
	</table>
</center>


在上述矩阵中，`1`代表赢，`-1`代表输，`0`代表平手。

---

## 决策树（decision tree）

![Decision tree](/assets/img/posts/decision_tree.jpg)

同样是以石头剪刀布为例，表示一个简单的决策树。
两个博弈者分别为1和2，可选策略都有（`石头`，`剪刀`，`布`）。

如上图所示，1先执行某个动作，然后由2执行对应的动作，再然后博弈结束。

---

# 策略 & 策略集合

## 决策选项（move） VS 策略（strategy）

某些资料把“move”翻译成“移动”，这种叫法较难理解，在这里，我称之为“决策选项”。

很多人混淆了“策略”和“决策选项”。

以下棋为例，完成一局游戏你需要有多个步骤。对每个步骤，你都有 **N** 个决策选项（走什么棋子，到哪里）。
而“策略”指的是——从第一步到最后一步所有决策选项的【总和】。
你可以把“策略”通俗理解为某种【算法 or 指导思想】，
它指导你从第一步走到最后一步。

## 策略集合（strategy set）

所有可能的策略，构成了“策略集合”。
以“石头/剪刀/布”为例，其“策略集合”只包含3个策略。

## 有限策略集合 VS 无限策略集合

### 有限策略集合

“石头/剪刀/布”就是经典的“有限策略集合”（该集合只有3个元素）。

### 无限策略集合

为了说明这种集合，举个“分蛋糕博弈”的例子。

所谓的“分蛋糕博弈”很简单——这是双人博弈，其中一人先把蛋糕分为两块（可以随便分），然后另一个人先挑选其中一块。

对于“负责分蛋糕”的人而言，其策略集合是无穷大（纯小数有无穷多个）。

## 关于“有限/无限”的反直觉

很多人凭直觉会认为：具有“无限策略集合”的博弈比“有限策略集合”的博弈更复杂。其实不然！

围棋虽然很复杂，但其“策略集合”依然是有限滴（只不过，要想描述这个集合，需要存储的信息量会超出整个宇宙的承受能力）。

作为对比，“分蛋糕博弈”比“围棋”简单多了（两者的复杂性相差 N 个数量级），但“分蛋糕博弈”反而具有【无限】的策略集合。

---

# 纯策略 VS 混合策略

## 纯策略（pure strategy）

在实际博弈时，如果你总是【固定选择】“策略集合”中的某【一个】策略，这种情况称之为“纯策略”。

以“石头/剪刀/布”为例：如果你每次总是出“石头”，这就是【纯策略】。

## 混合策略（mixed strategy）

如果你在博弈时，总是【随机选择】“策略集合”中的某【几个】策略，这种情况称之为“混合策略”。

以“石头/剪刀/布”为例：如果你一半概率出“石头”一半概率出“剪刀”，这就是【混合策略】。

## 完全混合策略（totally mixed strategy）

如果某个“混合策略”包含了“策略集合”中的【每一个】元素，称之为“完全混合策略”。

上一个小节的举例（一半概率出“石头”一半概率出“剪刀”）属于“混合策略”，但【不是】“完全混合策略”。

作为对比，如果你1/4概率出“石头”，1/4概率出“剪刀”，1/2概率出“布”——这就是“完全混合策略”。

---

# 支配策略（优势策略）

## 策略之间的【支配性】

假设你有两个策略 A ＆ B。
如果在【任何】情况下，A 都比 B 更优，
称作“A 支配 B”（A dominates B）或者“B 被 A 支配”（B is dominated by A）。

## 支配策略（dominant strategy）

“支配策略”又称“优势策略”。如果某个策略能够支配【所有】其它策略，那么它就是“支配策略/优势策略”。

通俗地说，不论你的对手采用何种策略，你的“支配策略”总是比你的其它策略有更好的结果。

在后面的某个小节，俺会举个很简单的例子，帮你理解“支配策略”这个概念。

## 强支配策略（strictly dominant strategy） VS 弱支配策略（weakly dominant strategy）

有时候会把“支配策略”进一步细分为“强支配”＆“弱支配”。

对于前者，它在任何情况下都比其它策略更好；对于后者，它在某些情况下比其它策略更好，某些情况下与其它策略一样好。

## 支配策略 VS 制胜策略（winning strategy）

有些人会把“支配策略”与“制胜策略”搞混淆。

“制胜策略”也称“必胜策略”，它通常只用于“零和博弈”，指的是——只要你采用这个策略（不论对方如何应对），你总是赢。

“制胜策略”肯定是“支配策略”（最起码是“弱支配策略”）；但“支配策略”不一定是“制胜策略”。

## 实例：（二战中）新几内亚的航路作战

这是一个很经典的博弈论案例，很多博弈论的科普读物都引用了此案例。

话说太平洋战场上，美日双方对新几内亚岛展开争夺战。美方通过截获的情报得知日方有一支补给船队要开往该岛。
日军补给船队有两条路线可走（北线 or 南线），两条路线都耗时3天。在南线，这3天都是晴天；
在北线有2天是晴天，1天是阴雨（阴雨天会影响美军轰炸）。

美方空军将领手头只有一个飞行队，需要决策：把这个飞行队派到哪一边执行轰炸任务？
如果押宝的方向错误，重新部署又会浪费掉1天时间。

对这个博弈过程，美方的收益矩阵参见下述表格。
表格中的数字表示“可用来轰炸的天数”（对美军而言，这个数字越大越好）。
<center>
	<table border>
		<tr>
			<td></td>
			<td colspan="3">日方</td>
		</tr>
		<tr>
			<td rowspan="3">美方</td>
			<td></td>
			<td>北线</td>
			<td>南线</td>
		</tr>
		<tr>
			<td>北线</td>
			<td>2</td>
			<td>2</td>
		</tr>
		<tr>
			<td>南线</td>
			<td>1</td>
			<td>3</td>
		</tr>
	</table>
</center>

从上述收益矩阵来看，美军应该选哪个策略，不那么明显。但如果【换位思考】，看日军的策略，就非常明显啦。
<center>
	<table border>
		<tr>
			<td></td>
			<td colspan="3">日方</td>
		</tr>
		<tr>
			<td rowspan="3">美方</td>
			<td></td>
			<td>北线</td>
			<td>南线</td>
		</tr>
		<tr>
			<td>北线</td>
			<td>2,-2</td>
			<td>2,-2</td>
		</tr>
		<tr>
			<td>南线</td>
			<td>1,-1</td>
			<td>3,-3</td>
		</tr>
	</table>
</center>

第2个表格补充了日方的收益（以逗号分隔）。由于日方是遭受轰炸，其收益以“负数”表示。

从日方的角度（表格的【纵向】角度）来看，走北线是其【支配策略】——
不论美方如何选择，日方走北线的收益都不比南线差。对应到刚才介绍的概念，日方的这个“支配策略”属于“弱支配策略”。

知道日军必定走北线之后，美军就很容易选定自己的策略了。

## 如何发现“支配策略”？

一个比较简单的做法是：逐步删除【被】支配的策略（英文叫做“Iterated Elimination of Strictly Dominated Strategies”，简称 IESDS）。

下面这张GIF，演示了逐步删除的过程。最后剩下的那个单元格，也就是该博弈的“纳什均衡点”（关于“纳什均衡”，后面有个章节会专门细聊）。

![IESDS](/assets/img/posts/IESDS.gif)

## “支配策略”的【罕见性】

一般来说，只有极其简单的博弈才存在“支配策略”。只要博弈再稍微复杂那么一丁点，“支配策略”可能就不存在了。

举个栗子：哪怕像“石头/剪刀/布”这么简单的游戏，就已经不存在“支配策略”了。

## “支配策略”的【乏味性】

当某个博弈存在“支配策略”，这个博弈通常就显得索然无味。
反过来想，你就能理解——为啥绝大部分棋牌类游戏都【没有】“支配策略”。

---

# 最小最大定理

## 概述

这个东西的定义英文叫做“Minimax”，比较绕口的陈述是：最小化最大损失。
更通俗的表述是：在最坏的情况下最小化损失。

这个定理以及算法最早在冯·诺伊曼的
《[博弈论与经济行为](https://press.princeton.edu/books/paperback/9780691130613/theory-of-games-and-economic-behavior)》
中提出。
本文开头介绍过——此书是博弈论的奠基性著作。

## 举例：静态博弈

假设你是A（你有三个策略：A1、A2、A3），你的对手是B（也有三个策略：B1、B2、B3）。
以下是针对A（你）的收益矩阵：
<center>
	<table border>
		<tbody>
			<tr>
				<td></td>
				<td>B1</td>
				<td>B2</td>
				<td>B3</td>
			</tr>
			<tr>
				<td>A1</td>
				<td>+3</td>
				<td>-2</td>
				<td>+4</td>
			</tr>
			<tr>
				<td>A2</td>
				<td>-1</td>
				<td>0</td>
				<td>+2</td>
			</tr>
			<tr>
				<td>A3</td>
				<td>-4</td>
				<td>-3</td>
				<td>+1</td>
			</tr>
		</tbody>
	</table>
</center>

针对上述收益矩阵，基于 Minimax 算法，你应该选择 A2 策略——此时你的最坏情况是
`-1`。

## 举例：动态博弈——切蛋糕博弈

前面章节已经简单介绍过“分蛋糕博弈”。
这是一个非常简单的动态博弈（步骤很少）。

当双方都是足够理性，选蛋糕的人肯定会选大的那块。
切蛋糕的人基于“最小最大原则”，
应该在最坏情况下最小化自己的损失，
所以他/她应该把蛋糕切成同等大小。

# 反向归纳法

## 概念

该方法英文称之为
“backward induction”。
其精髓是【正向展望，反向推理】。

首先，你需要思考自己的每个决策，以及对方在应对你的决策时，会采用何种决策（这个思维过程类似于【决策树的展开】）。

这个展开过程要一直推演到【最后一步】（也就是决策树的叶子节点）。
此时你就可以看清双方在最后一步各自的最优选择；
然后再反向回推到第一步。

## 局限性

当你要用“反向归纳”进行展望与推理，前提是——你要获得充分的信息；或者说，如果某个博弈者所知的信息不够充分，就【无法】运用该方法。

## 重复博弈中的“囚徒困境”

前面提到的“囚徒困境”属于【单次】静态博弈。如果把这个局面改为【多次】，并且两个囚徒足够理性且相互认识，并且两人也都知道自己处于【多次】博弈的场景，那么就有可能达成合作。

### 无限重复博弈（次数不确定）

在这个博弈场景中，由于两个囚徒都知道未来还会有多次类似的博弈局面，所以他们在第一次被抓的时候，就会选择合作（双方都抵赖），并且未来也会每次都选择合作。

他们之所以选择合作，是为了给将来博弈中的合作建立基础。

### 有限重复博弈（次数确定）
　　假设次数确定为【10次】。这种情况下，是否还可能达成合作捏？很多同学凭直觉认为：还是可以合作。其实不然！

对于有限重复的情形，就需要用到本章节的“反向归纳法”了。

先分析【最后一次】（第10次）博弈的情形。因为不再有后续的博弈，此时的局面等价于【单次】博弈（单次囚徒困境）——也就是说，双方会选择背叛。

如果两人都足够理性，当他们在进行第9次博弈的时候，就应该能想到——下一次博弈是最后一次，不会有合作。既然如此，那么本次博弈，当然也没必要合作了（请注意：合作是为了下次能继续合作）。

上述反推可以一直持续到第一次。所以，如果双方都足够理性，在第一次就会选择互相背叛。

## 海盗博弈（海盗分金问题）

上述例子太简单啦，再来个稍微复杂的例子。

### 博弈场景描述

5个海盗抢了100个金币，讨论如何分赃。

这5个海盗有等级高低（不妨假设 A＞B＞C＞D＞E）。
先由等级最高的海盗提出分赃方案，然后投票。
如果半数以上（含半数）同意，就按这个方案分，游戏结束；
如果同意的不到半数，把提出方案的海盗扔进海里喂鲨鱼，然后由次一等级的海盗提出新的方案；以此类推。

每个海盗的特点是：足够理性（追求个人利益最大化）并且知道别人也足够理性；足够残忍（在个人利益等同的情况下，倾向于把更多同伴扔进海里）。

现在，请你思考一下最终的结局（需要用到本章节所说的“反向归纳法”）。

### 博弈策略分析

为了进行反向推理，假设最后只剩下2个海盗（D ＆ E）。
此时的投票肯定过半（D 肯定投票赞同自己的方案）。
在这种局面下，D 可以采用最极端的方案——自己全拿100个金币，E 则一个也拿不到。

现在回推一步。
当只剩下3个海盗（C、D、E），
由 C 提出方案。
他只需要分1个金币给 E，
E 就会投票支持（否则的话，等到由 D 来提方案，E 啥也拿不到）。
所以在 C 的方案中，他自己拿99个金币，E 拿1个金币。

再往前一步。
只剩下4个海盗（B、C、D、E），B 提方案，他当然也能想到刚才那些推理。
他只需给 D 1个金币，D 就会支持他（如果等到 C 来提方案，D 啥也拿不到）。
所以 B 提出的方案是 `B：99，C：0，D：1，E：0`，同样能得到半数支持。

基于上述分析，再看 A 的方案，就很显然了——`A：98，B：0，C：1，D：0，E：1`

有些同学可能会觉得：A 还可以提出另一个等价方案 `A：98，B：0，C：0，D：1，E：1`（把 C ＆ D 交换）。

其实这个方案【不】等价。如果是后面这个方案，D 会投反对票，于是 A 去喂鲨鱼，由 B 来提方案，D 还是可以拿到1个金币。虽然两种方案，D 都是拿1个金币。但基于规则中提到的【残忍性】，D 会对 A 的方案投反对票。

### 海盗分金的推广

如果你凭直觉认为：总是最先提出方案的海盗占最大利益，那你就犯了直觉谬误啦。

这个博弈游戏还可以推广到更多海盗。当海盗数量达到某个临界点之后，第一个提出方案的海盗必死无疑（必定被丢进海里喂鲨鱼）。


# 纳什均衡

前面喷了好多口水，终于要聊到大名鼎鼎的“[纳什均衡](https://zh.wikipedia.org/wiki/%E7%BA%B3%E4%BB%80%E5%9D%87%E8%A1%A1)”（Nash equilibrium）啦。

美国数学家纳什在1951年发表了一篇小论文（篇幅很短），名叫
《非合作博弈》[^1]，
其中提出了“纳什均衡”的概念并给出了相应的数学证明（该证明基于“不动点定理”）。

![约翰·福布斯·纳什](https://imgur.com/Aj9hZIK.jpg)

<center>
(
	<a href="https://zh.wikipedia.org/wiki/%E7%BA%A6%E7%BF%B0%C2%B7%E7%A6%8F%E5%B8%83%E6%96%AF%C2%B7%E7%BA%B3%E4%BB%80">
	约翰·福布斯·纳什
</a>
)
</center>

## 概念

所谓的“纳什均衡”，通俗地说是指——在多人的“非合作博弈”中，如果每个博弈者都无法【单方面】改善自己的境地，此时的局面称作“纳什均衡”。

冯·诺伊曼已经在《博弈论与经济行为》一书中证明了：零和博弈必定存在这样的均衡点。

纳什的贡献在于——他从“零和博弈”推广到“非零和博弈”，并证明了：这样的均衡点依然存在。

这里有几个定语需要注意：

其一，“纳什均衡”的前提是【非合作博弈】。不要望文生义，把“非合作博弈”误解为“没有合作的博弈”。请参见本文开头章节对“博弈类型”的解释。

其二，【单方面】指的是——在其他博弈者都没有改变策略的情况下，自己改变策略。


## “纳什均衡”的【稳定性】

当博弈的局面处于“纳什均衡”，此时的系统是【稳定】的——
如果每个博弈者都足够理性，他们都【不愿意】主动改变当前的策略。

## 实例：囚徒困境

几乎每一个讲“纳什均衡”的资料（书/文章）都会拿“囚徒困境”来举例。

以下是“囚徒困境”的收益矩阵（被判刑的年数以负数表示，零表示立即释放）：
<center>
	<table border>
		<tbody>
			<tr>
				<td></td>
				<td colspan="3">囚犯 B</td>
			</tr>
			<tr>
				<td rowspan="3">囚犯 A</td>
				<td></td>
				<td class="background:#C0C0C0">坦白</td>
				<td class="background:#C0C0C0">抵赖</td>
			</tr>
			<tr>
				<td class="background:#C0C0C0">坦白</td>
				<td>-2,-2</td>
				<td>0,-5</td>
			</tr>
			<tr>
				<td class="background:#C0C0C0">抵赖</td>
				<td>-5,0</td>
				<td>-1,-1</td>
			</tr>
		</tbody>
	</table>
</center>

基于上述矩阵，“双方都坦白”的局面是“纳什均衡点”（表格中着色的格子）——在这个均衡局面下，任何一个囚犯【单方面】改变策略，只会让自己更不利。

作为对比，“双方都抵赖”虽然是双赢的局面，但这个局面是【不】稳定滴。因为在这个局面下，任何一个囚犯都有动机去改变策略，从而让自己的获益更多。

## 实例：石头/剪刀/布

对这个游戏，有一个稳定的【混合策略】——其中每个策略各占1/3的权重（以相等的概率随机使用这3个策略）。

当双方都采用这个混合策略，此时博弈处于“纳什均衡”。

对于“石头/剪刀/布”而言，这是【唯一】的“纳什均衡点”。不信的话，你可以试着考虑其它各种局面，会发现其它的局面都不稳定，（只要双方足够理性）最终都会演化到上述的均衡点。

## 对“纳什均衡”的【误解】

**误解1**：把“纳什均衡”误解为“各方利益总和最大化”。

实际情况是：“纳什均衡”与利益最大化没啥关系。甚至可能出现相反的情况——当局面处于“纳什均衡”时，对博弈的各方都不利。

典型的例子参见“囚徒困境”——均衡的时候，反而是【双输】的局面。

<br/>

**误解2**：认为“纳什均衡点”是唯一的。

实际情况是：对某些博弈，可以有【多个】“纳什均衡点”（下面聊“三党博弈”会提及）

## “纳什均衡”的【局限性】

**局限性1**
纳什的证明是【非建设性】滴。也就是说，他只是证明了这个均衡点必定存在，但【没有】给出“如何找到均衡点”的方法论。

那么，如何找到均衡点捏？

进入21世纪之后，数学家已经证明：即使对于某些比较简单的博弈，找到纳什均衡点所消耗的计算量也会超出整个宇宙的承受力。

从这些数学家的成果中，你会再次感受到“复杂系统”的魅力与挑战——即使是一些看似简单的系统，其【复杂性】也已经远远超出人们的想象。

<br/>

**局限性2**
对于任何一个稍微复杂点的博弈，要想达到“纳什均衡点”，需要依赖于非常非常多的约束条件；在现实生活中，不太可能达到。

为何大多数地缘政治，会以两个大党作为均衡存在，而不是三个？

这里的三个党也就是“三党博弈”。
“三党博弈”确实有可能达成均衡（而且均衡点还不止一个），
但每一个均衡点要依赖的约束条件太多了。
这么多约束条件同时满足，概率本来就很低（趋向于零）。
即使真的出现了，这种局面也很容易被干扰（只要某个约束条件不再满足，局面就被破坏了）。作为对比，“两党博弈”就更容易演变到“纳什均衡点”，也更容易长期维持。

如果连“三个实体的博弈”都如此难达成均衡。你可以粗略想象一下：在更复杂的博弈中，达成“纳什均衡”的可行性有多么低。

# 博弈中的【信息】因素

聊完“均衡”，重要的概念基本上讲差不多了。下面开始聊博弈中涉及的一些因素，首先是“信息”因素。

## “perfect information” VS “imperfect information”

这两个概念通常针对“顺序博弈”（动态博弈）而言。

在博弈过程中，如果每个参与者在做每个决策时，都能知道已经发生的每个事件的信息，称作“perfect information”；反之则是“imperfect information”。

<br/>

**“perfect information”举例：**
大部分棋类游戏（围棋、象棋、跳棋...）属于这类。

<br/>

**“imperfect information”举例：**
某些军棋游戏只能看到己方的棋子，
属于这类；
大部分扑克游戏（比如：桥牌、拱猪...）
也是这类。

## “complete information” VS “incomplete information”

在博弈论的讨论中，很多人混淆了“perfect information”与“complete information”。

“complete VS incomplete”的讨论主要针对【博弈者】。如果每个博弈者的特征都是公开的（每个人都知道其他人的特征），则称为“complete”；反之是“incomplete”。

【博弈者的特征】是啥捏？通俗地说包括：博弈目标、效用函数、等等。

“博弈目标”比较好理解，“效用函数”指的是——为达到不同级别的目标愿意付出多大代价。

“核战略博弈”就是典型的“incomplete information”类型的博弈，因为博弈的各方【无法】精确评估其它国家领导人的“战争意志”。

<br/>

**“complete information”举例：**
几乎有所有的【棋牌类游戏】都属于“complete information”——双方的目标是公开且固定的（比如象棋的目标是干掉对方的王），而且也不用考虑“效用函数”之类的概念。

**“incomplete information”举例：**
除了刚才所说的“核战略博弈”，【拍卖】也属于这类博弈——有些人是真的买家，有些人只是为了抬价；即使是真正的买家，各自的底线也不公开。


## 贝叶斯博弈（Bayesian game）＆ 贝叶斯纳什均衡（Bayesian Nash equilibrium）

对于“incomplete information”的博弈，由于每个博弈者【无法】精确掌握其它博弈者的特征。对这类博弈，需要引入【贝叶斯定理】（[Bayes' rule](https://en.wikipedia.org/wiki/Bayes%27_theorem)）进行概率分析，从而猜测其它对手的特征。所以这类博弈也称作“贝叶斯博弈”。

“贝叶斯定理”是概率论的重要工具。要对它展开讨论，至少又是一个长篇博文。暂且打住。

对于“贝叶斯博弈”，其纳什均衡称之为“贝叶斯纳什均衡”，英文简称 BNE（Bayesian Nash equilibrium）。

# 结尾

由于本文定位于【基础性扫盲】，只能蜻蜓点水，简单聊聊。
这里面的很多话题，假如要深入细谈，可以再写出好几篇博文。
当然今后根据研究方向不同，涉及到这块的部分会单独整理出来并加以科普。




[^1]: J. Nash, "Non-cooperative games", *The Annuals of Mathematics*, vol. 54, no. 2, pp. 286-295, Oct. 1950.