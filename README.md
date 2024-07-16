
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

```py
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

## 128. Longest Consecutive Sequence
https://leetcode.com/problems/longest-consecutive-sequence/description/

```py
class Solution:
	def longestConsecutive(self, arr):
		num_set = set(arr)
		best = 0
		for x in num_set:
			if x - 1 not in num_set:
				y = x
				while y in num_set:
					y += 1

				best = max(best, y - x)

		return best
```

## 134. Gas Station
https://leetcode.com/problems/gas-station/description/

```py
class Solution:
	def canCompleteCircuit(self, gas, cost):
		n = len(gas)
		arr = [gas[i] - cost[i] for i in range(n)]

		total = 0
		l, r = 0, 0
		while r < n:
			total += arr[r]
			r += 1

			if total < 0:
				l = r		#	reset the window
				total = 0	#	reset the total

		return l if sum(arr) >= 0 else -1
```


## 39. Combination Sum
https://leetcode.com/problems/combination-sum/description/

```py
class Solution:
	def combinationSum(self, candidates, target):
		result = []
		self.dfs(candidates, result, target, [])

		return result

	def dfs(self, candidates, result, target, combination):
		if sum(combination) > target:
			return
		if sum(combination) == target:
			result += [combination]
			return
		n = len(candidates)
		for i in range(n):
			num = candidates[i]
			self.dfs(candidates[i:], result, target, combination + [num])
```

## 238. Product of Array Except Self
https://leetcode.com/problems/product-of-array-except-self/description/

```py
class Solution:
	def productExceptSelf(self, arr):
		n = len(arr)
		L = [1 for i in range(n)]
		R = [1 for i in range(n)]

		pl, pr = 1, 1
		for i in range(n):
			L[i] *= pl
			pl *= arr[i]
		for i in range(n):
			R[~i] *= pr
			pr *= arr[~i]

		result = [L[i] * R[i] for i in range(n)]
		return result
```

## 15. 3Sum
https://leetcode.com/problems/3sum/description/
```py
class Solution:
	def threeSum(self, arr):
		result = []
		n = len(arr)
		arr.sort()

		for i in range(n):
			#	avoid duplicates (a[i], ?, ?)
			if i > 0 and arr[i - 1] == arr[i]:
				continue

			l, r = i + 1, n - 1
			while l < r:
				tsum = arr[i] + arr[l] + arr[r]
				if (tsum < 0):
					l = l + 1
				elif (tsum > 0):
					r = r - 1
				else:
					result += [(arr[i], arr[l], arr[r])]
					l, r = l + 1, r - 1

					#	avoid duplicates (a[i], a[l], ?)
					while l < n and arr[l - 1] == arr[l]:
						l = l + 1

		return result
```

## 57. Insert Interval
https://leetcode.com/problems/insert-interval/description/

```py
class Solution:
	def insert(self, intervals, newInterval):
		x, y = newInterval
		left, needs_merging, right = [], [], []
        
		for [a, b] in intervals:
			if (b < x):
				left += [[a, b]]
			if (a > y):
				right += [[a, b]]
			if not (b < x or a > y):
				needs_merging += [[a, b]]

		l, r = x, y
		for [a, b] in needs_merging:
			l = min(l, a)
			r = max(r, b)

		return left + [[l, r]] + right
```
