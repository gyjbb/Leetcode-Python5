# Leetcode-Python5
## Hash Table Theory, 242. Valid Anagram, 349. Intersection of Two Arrays, 202. Happy Number

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
[Leetcode Link](https://leetcode.com/problems/valid-anagram/)\
Two strings are made with the same characters, order may be different.\
Use **arrays** to build a hash table here. For a limited number of hash values, use an array. If the number of hash values is too large, use **set**. If you need key value pairs, use **map**.
```python
# Ways 1: use hash table and arrays
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        record = [0] * 26
        for i in s:
            #并不需要记住字符a的ASCII，只要求出一个相对数值就可以了
            record[ord(i) - ord("a")] += 1
        for i in t:
            record[ord(i) - ord("a")] -= 1
        for i in range(26):
            if record[i] != 0:
                #record数组如果有的元素不为零0，说明字符串s和t 一定是谁多了字符或者谁少了字符。
                return False
        return True
```
```python
# Ways 2: use dictionary
class Solution:
    def isAnagram(self, s: str, t: str) -> bool:
        from collections import defaultdict
        
        s_dict = defaultdict(int)
        t_dict = defaultdict(int)
        for x in s:
            s_dict[x] += 1
        
        for x in t:
            t_dict[x] += 1
        return s_dict == t_dict
```
```python
# Ways 3: use Counter function
class Solution(object):
    def isAnagram(self, s: str, t: str) -> bool:
        from collections import Counter
        a_count = Counter(s)
        b_count = Counter(t)
        return a_count == b_count
```


#### 383
#### 49
#### 438

## 349. Intersection of Two Arrays
[Leetcode link](https://leetcode.com/problems/intersection-of-two-arrays/)\
[video link](https://www.bilibili.com/video/BV1ba411S7wu/?spm_id_from=pageDriver&vd_source=63f26efad0d35bcbb0de794512ac21f3)\
We can use **set** to solve this question. Because the integers in the two arrays can be very large, and it's better to use set than array(as in the last question).\
Everytime you need to check if an item appears in a collection of data, can think of using hash table to solve the question.
```python
# Ways 1: use dictionary and set
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
    # 使用哈希表存储一个数组中的所有元素
        table = {}
        for num in nums1:
            table[num] = table.get(num, 0) + 1
        
        # 使用集合存储结果
        res = set()
        for num in nums2:
            if num in table:
                res.add(num)
                del table[num]
        
        return list(res)
```
```python
# Ways 2: use set
class Solution:
    def intersection(self, nums1: List[int], nums2: List[int]) -> List[int]:
        return list(set(nums1) & set(nums2))
```


#### 350


## 202. Happy Number
[Leetcode link](https://leetcode.com/problems/happy-number/)\
[Reading](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0202.%E5%BF%AB%E4%B9%90%E6%95%B0.md)\
A number is happy number if the sum of the squre of all digits finally equals to 1.
```python
# Ways 1: use set
class Solution:
   def isHappy(self, n: int) -> bool:
       record = set()
       while n not in record:
           record.add(n)
           new_num = 0
           n_str = str(n)
           for i in n_str:
               new_num+=int(i)**2
           if new_num==1: return True
           else: n = new_num
       return False
```
```python
# Ways 2: a simpler way to use set
class Solution:
   def isHappy(self, n: int) -> bool:
       seen = set()
       while n != 1:
           n = sum(int(i) ** 2 for i in str(n))
           if n in seen:
               return False
           seen.add(n)
       return True
 ```
 ```python
 # Ways 3: use array
 class Solution:
   def isHappy(self, n: int) -> bool:
       seen = []
       while n != 1:
           n = sum(int(i) ** 2 for i in str(n))
           if n in seen:
               return False
           seen.append(n)
       return True
 ```















