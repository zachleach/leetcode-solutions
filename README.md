
## 3. Longest Substring Without Repeating Characters
https://leetcode.com/problems/longest-substring-without-repeating-characters/description/

```py
class Solution:
	def lengthOfLongestSubstring(self, arr):
		l, r = 0, 0
		best = 0
		seen = set()
		n = len(arr)
		while r < n:
			if arr[r] not in seen:
				seen.add(arr[r])
				best = max(best, len(seen))
				r += 1
				continue

			seen.remove(arr[l])
			l += 1

		return best
```
