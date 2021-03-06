﻿[toc]

# N 皇后问题

## 问题概述

n 个皇后在 n\*n 的棋盘上，能够保证每个皇后在单独的行列一级斜线方向上

解题思路：**回溯法优化查找**

> 回溯算法一种修改过的深度优先查找算法*(广度优先查找)*

```c
/*回溯法 有优化
在到达递归边界前的某层，由于一些事实导致已经不再
需要往任何一个子问题递归，就可以直接返回上一层 */

void Generatep(int index)
{
	//递归边界,生成一个合法方案(回溯算法：相当于看是否递归到叶节点了，找到一个可能解了)
	if (index == n + 1)
	{
		count++;
		for(int k = 1; k <= n; k++)
		{
			printf("%d ",p[k]);
		}
		printf("\n");
		return ;
 	}
	//第x行
	for(int x = 1; x <= n; x++)
	{
		//第x行还没有皇后
		if(hash[x] == false)
		{
			bool flag = true;//表示当前的皇后不会和之前的皇后冲突
			for(int pre = 1; pre < index; pre++)//遍历之前的皇后
			{
				if(abs(index - pre) == abs(x - p[pre]))
				{
					flag = false;
					break ;
				}
			}
		//如果可以把皇后放在第x行
			if(flag)
			{
				//令第index列的皇后的行号为x
				p[index] = x;
				//表示第x行已被占用
				hash[x] = true;
				//递归处理第index+1 列皇后
				Generatep(index+1);
  				//递归完毕后，还原第x行为未占有
				hash[x] = false;
  			}
		}
	}


}
```

### 相关算法回顾

1. 两种搜索算法
2. 解空间树[入门 CSDN](https://blog.csdn.net/gao1440156051/article/details/41721409)
3. 回溯法 [入门 CSDN](https://blog.csdn.net/gao1440156051/article/details/41721409)

   > 回溯法代码大体框架：

```c
    void func(int i)
        {
            if (i == k+1)
            {
                到叶节点了，找到一个可能解了
                验证，做点什么
            }
            for(int t = 一个子问题的各种状态)
            {
                设置字问题i的状态为t
                func(i+1);
            }
        }
//还是那句话,用一个函数表示一个小问题,在函数里面设置各种状态,同时调用下一个子问题的函数,就递归了.
//真正的回溯算法（或者说所有搜索算法）的关键在于剪枝，就是怎么减少搜索可能解的数量
```

### 回溯法思路

本算法的思路是按行来规定皇后位置，第一行放置一个皇后，第二行放置一个皇后， 第 N 行也放置一个皇后… 这样， 可以保证每行都有一个皇后，那么各行的皇后应该放置在那一列呢， 算法通过循环来完成，在循环的过程中， 一旦找到一个合适的列，则该行的皇后位置确定，则继续进行下一行的皇后的位置的确定。由于每一行确定皇后位置的方式相似，所以可以使用递归法。一旦最后 一行的皇后位置确定，则可以得到一组解。找到一组解之后， 之前确定皇后应该放置在哪一列的循环其实才进行了一轮循环的， 算法通过该循环遍历所有的列，以此确定每一行所有可能的列的位置。在从一轮循环进入下一轮循环之前，算法需要清除在上一轮被标记为不可放置皇后的标记，也就是回溯。因为进入下一轮循环之后，同一行的皇后的列的位置会发生了变化，之前被标记为不可放置皇后的列和正反对角线位置都已经失效。

### 流程图

```flow
st=>start: Start
e=>end
op=>operation: My Operation
cond=>condition: Yes or No?

st->op->cond
cond(yes)->e
cond(no)->op
```

以及时序图:

```sequence
Alice->Bob: Hello Bob, how are you?
Note right of Bob: Bob thinks
Bob-->Alice: I am good thanks!
```

> 测试图片

<!-- > ![测试图片](https://cdn.jsdelivr.net/gh/Countra/Picgo_pic/images/测试图片.png) -->

---

![冰菓](https://cdn.jsdelivr.net/gh/Countra/Picgo_pic/images/冰菓.png)

![test](https://cdn.jsdelivr.net/gh/Countra/Picgo_pic/images/test.png)
---

## The end
