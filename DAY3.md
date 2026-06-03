class Solution(object):
    def maxDistance(self, arrays):
        """
        :type arrays: List[List[int]]
        :rtype: int
        """
        ans = 0
        mn, mx = float('inf'), float('-inf')
        for array in arrays:
            ans = max(ans,array[-1] - mn, mx - array[0])                      
            mn = min(mn,array[0])
            mx = max(mx,array[-1])
        return ans