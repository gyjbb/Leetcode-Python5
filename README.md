# Leetcode-Python5
## Hash Table Theory, 242. Valid Anagram, 349. Intersection of Two Arrays, 202. Happy Number, 1. Two Sum

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

## 1. Two Sum
[Reading](https://github.com/youngyangyang04/leetcode-master/blob/master/problems/0001.%E4%B8%A4%E6%95%B0%E4%B9%8B%E5%92%8C.md)\
In this question, we not only need to find if a number and (target-number) appear in the collection of data, but also need to know the index of the number to return. This is a key-value pair question, and we can use **map** to build the hash table structure.\
Map can be used to quickly search if the key in map appears before, so we use the number as the map's key, and use the index of the number as the map's value.
 ```python
# Ways 1: use set()
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        #创建一个集合来存储我们目前看到的数字
        seen = set()             
        for i, num in enumerate(nums):
            complement = target - num
            if complement in seen:
                return [nums.index(complement), i]
            seen.add(num)
 ```
 ```python
# Ways 2: use disctionary{}
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        records = dict()

        for index, value in enumerate(nums):  
            if target - value in records:   # 遍历当前元素，并在map中寻找是否有匹配的key
                return [records[target- value], index]
            records[value] = index    # 遍历当前元素，并在map中寻找是否有匹配的key
        return []
 ```
 ```python
# Ways 3: use two pointers
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        # 对输入列表进行排序
        nums_sorted = sorted(nums)
        
        # 使用双指针
        left = 0
        right = len(nums_sorted) - 1
        while left < right:
            current_sum = nums_sorted[left] + nums_sorted[right]
            if current_sum == target:
                # 如果和等于目标数，则返回两个数的下标
                left_index = nums.index(nums_sorted[left])
                right_index = nums.index(nums_sorted[right])
                if left_index == right_index:
                    right_index = nums[left_index+1:].index(nums_sorted[right]) + left_index + 1
                return [left_index, right_index]
            elif current_sum < target:
                # 如果总和小于目标，则将左侧指针向右移动
                left += 1
            else:
                # 如果总和大于目标值，则将右指针向左移动
                right -= 1
 ```
 ```python
# Ways 4: brutal
class Solution:
    def twoSum(self, nums: List[int], target: int) -> List[int]:
        for i in range(len(nums)):
            for j in range(i+1, len(nums)):
                if nums[i] + nums[j] == target:
                    return [i,j]

 ```






