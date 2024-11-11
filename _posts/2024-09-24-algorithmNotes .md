---
layout: post
title: 'Algorithm Notes'
date: 2024-09-24
author: Liyang
cover: 'https://images.unsplash.com/photo-1653629154302-8687b83825e2'
cover_author: 'rogov'
cover_author_link: 'https://unsplash.com/@rogovca'
tags: 
- Java 
- Algorithm
- Notes 
pin: true
---

Hi guys, these are my notes on learning some Algorithms.

This note is used  both to record algorithms learning and to practice English writing.

But I am not good at writing, there may be many grammar errors. Please forgive and correct me.

E-mail : bryceyangli@gmail.com

Thanks.

**Contents:**



#### 0 - 65535

题目来源/Source of Questions：LeetCode-001 两数之和/Two Sum

解题思路/Ideas：

​	December 07,2024：**1、**双循环暴力求解；2、进阶“时间复杂度为 O(n)”

算法 或 数据结构/Algorithm or Data Structure：

​	**HashMap**：数据以“键值对<key,value>”的方式存储，插入的**键-key**数据是无序的，不能重复的，无索引的；

```java
//这个题目中，我们使用数组中的值作为键，数组下标作为值；
Map<Integer,Integer> hashmap = new HashMap<>();
for(int i = 0; i < nums.length; i++){
    //如果HashMap中包含目标值作为的键；则反回HashMap目标值作为键所对应的值和当前i作为结果
	if(hashmap.containsKey(target - nums[i])){
		return new int[]{hashmap.get(target-nums[i]),i};
    }
    //否则，将数组中的值作为键，数组下标作为值存入HashMap中；
    hashmap.put(nums[i],i);
}
```

#### 1 - 65535

题目来源/Source of Questions：回文数/Palindrome Number

解题思路/Ideas：

​	December 07,2024 ：**1、**将数字转换为String类型，然后用StringBuffer倒置，与原来字符串进行匹配，true则为回文数，false则不是，同时避免的整数溢出的问题；**2、**进阶“你能不将整数转为字符串来解决这个问题吗？” 取余然后翻转，要考虑如何避免溢出；

算法 或 数据结构/Algorithm or Data Structure：

​	回文数：后半部分翻转后和前半部分相等；考虑如何只翻转一半；

```java
String str1 = String.valueOf(x);
StringBuffer stringBuffer = new StringBuffer(str1);
stringBuffer.reverse();
String str2 = stringBuffer.toString();
return str1.equals(str2)?true:fa
```



​	

​	

