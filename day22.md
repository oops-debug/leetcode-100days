### 1.两数之和
思路：
寻找两个数字，使它们相加等于 target
固定当前数字 a，另一个数字必须是 target - a
问题转化成：如何快速判断 target - a 是否出现过
如果每次都重新遍历数组去找，还是 O(n²)
所以需要一个支持“快速查询某个值是否存在”的数据结构
哈希表可以做到平均 O(1) 查询
遍历数组时，把已经见过的数字存进哈希表
对当前 a，先查 target - a 是否已经在哈希表里
如果在，就找到答案；不在，就把当前 a 存进去
```python
class Solution:
    def twoSum(self, nums: list[int], target: int) -> list[int]:
        idx = {}
        for j,x in enumerate(nums):
            if target - x in idx:
                return [idx[target-x],j]
            idx[x] = j
```

### 49.字母异位词分组
```python
class Solution:
    def groupAnagrams(self, strs: list[str]) -> list[list[str]]:
        d = defaultdict(list)# 每个人都有一本自己的“词典”
        for s in strs:
            sorted_s = ''.join(sorted(s))# 无论你的身份如何，你始终是你自己
            d[sorted_s].append(s)# 而这些身份又构成了你
        return list(d.values())
```
发现新题材，力扣小说体