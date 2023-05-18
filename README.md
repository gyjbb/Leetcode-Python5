# Leetcode-Python5
## Hash Table Theory, 242. Valid Anagram

May 17, 2023  4h

The fifth day, will start learning Hash Table!!! Yeah, keep going!!!

## Hash Table Theory
[Reading link](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/%E5%93%88%E5%B8%8C%E8%A1%A8%E7%90%86%E8%AE%BA%E5%9F%BA%E7%A1%80.md)\
When to use hash table?\
When we need to quickly judge if an element exists in a set.\
There are 3 data type that can work with hash table: array, set, map.\
总结一下，当我们遇到了要快速判断一个元素是否出现集合里的时候，就要考虑哈希法。\
但是哈希法也是牺牲了空间换取了时间，因为我们要使用额外的数组，set或者是map来存放数据，才能实现快速的查找。

## 242. Valid Anagram
Two strings are made with the same charaters, order may be different.\
Use arrays to build hash table.
