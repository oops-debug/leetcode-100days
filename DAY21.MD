### 84.柱状图中最大的矩形
思考：分析问题-以当前为标准遍历左右比现在矮的（o(n2)有没有重复性动作）-右端的情况扫不到-定右端，遇到右端降低就来结算左边比他高的
```python
class Solution:
    def largestRectangleArea(self, heights: List[int]) -> int:
        # 保证最后一个也可以被遍历到
        heights.append(-1)
        st = [-1]
        ans = 0
        for right, h in enumerate(heights):
            while len(st)>1 and heights[st[-1]]>=h:
                i = st.pop()# 当前
                left = st[-1]# 左侧比当前矮的最近的
                ans = max(ans, heights[i]*(right-left-1))
            st.append(right)# 单调递增栈
        return ans
```