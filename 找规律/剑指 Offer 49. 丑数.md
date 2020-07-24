移动零

# 题目描述
我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

## 示例1
```
输入: n = 10
输出: 12
解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。
```

## 方法：  
这道题的目的是找出序号n和对应的丑数之间的规律，分析丑数的排列，有一个特点是，任意一个丑数都是由小于它的某一个丑数*2，*3或者*5得到的  
现在假设有3个数组，分别是：   
A：{1*2，2*2，3*2，4*2，5*2，6*2，8*2，10*2......}  
B：{1*3，2*3，3*3，4*3，5*3，6*3，8*3，10*3......}
C：{1*5，2*5，3*5，4*5，5*5，6*5，8*5，10*5......}
  
那么所有丑数的排列，必定就是上面3个数组的合并结果然后去重得到的，那么这不就转换成了三个有序数组的无重复元素合并的问题了
  
合并有序数组的一个比较好的方法，就是每个数组都对应一个指针，然后比较这些指针所指的数中哪个最小，就将这个数放到结果数组中，然后该指针向后挪一位


## 代码一：时间慢

```python
class Solution:
  def nthUglyNumber(n) :
      i,j,k = 0,0,0
      temp = [1]
      count = 1
      while count<n:
          m = min(temp[i]*2,temp[j]*3,temp[k]*5)
          if m not in temp:
              temp.append(m)
              count+=1
          if m==temp[i]*2:i+=1
          elif m ==temp[j]*3:j+=1
          else: k+=1
      return temp[n-1]
```
## 代码二：改进去重方式

```python
class Solution:
  def nthUglyNumber(n) :
      i,j,k = 0,0,0
      temp = [1]
      while len(temp)<n:
          m = min(temp[i]*2,temp[j]*3,temp[k]*5)
          if m==temp[i]*2:i+=1
          if m ==temp[j]*3:j+=1
          if m==temp[k]*5:k+=1
          temp.append(m)
      return temp[n-1]
```
