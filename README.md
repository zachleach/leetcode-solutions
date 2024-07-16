
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

## 347. Top K Frequent Elements
https://leetcode.com/problems/top-k-frequent-elements/description/

```
class Solution:
	def topKFrequent(self, arr, k):
		table = defaultdict(int)
		for num in arr:
			table[num] += 1

		keys = sorted(table, key=lambda x: table[x], reverse=True)

		return [keys[i] for i in range(k)]
```

## 49. Group Anagrams
https://leetcode.com/problems/group-anagrams/description/

```py
class Solution:
	def groupAnagrams(self, strs):
		table = defaultdict(list)
		for s in strs:
			key = ''.join(sorted(s))
			table[key] += [s]

		return table.values()
```
