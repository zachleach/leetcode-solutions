## 200. Number of Islands
https://leetcode.com/problems/number-of-islands/description/

```py
class Solution:
	def numIslands(self, grid):
		count = 0
		h, w = len(grid), len(grid[0])
		for y in range(h):
			for x in range(w):
				if grid[y][x] == '1':
					self.dfs(grid, y, x)
					count += 1

		return count

	def dfs(self, grid, y, x):
		if y < 0 or y > len(grid) - 1:
			return
		if x < 0 or x > len(grid[0]) - 1:
			return
		if grid[y][x] != '1':
			return

		grid[y][x] = '#'
		self.dfs(grid, y + 1, x)
		self.dfs(grid, y - 1, x)
		self.dfs(grid, y, x + 1)
		self.dfs(grid, y, x - 1)
```

## 150. evaluate reverse polish notation
https://leetcode.com/problems/evaluate-reverse-polish-notation/description/

```py
class Solution:
	def evalRPN(self, tokens):
		op_map = {
			'+': operator.add,
			'-': operator.sub,
			'*': operator.mul,
			'/': lambda a, b: math.trunc(a / b)
		}

		stack = []
		for token in tokens:
			if token in op_map:
				func = op_map[token]
				a, b = stack.pop(-2), stack.pop(-1)
				stack.append(func(a, b))
			else:
				stack.append(int(token))

		return stack[-1]
```

## 424. Longest Repeating Character Replacement
https://leetcode.com/problems/longest-repeating-character-replacement/description/

```py
class Solution:
	def characterReplacement(self, arr, k):
		freq = defaultdict(int)
		best, l, n = 0, 0, len(arr)

		for r in range(n):
			freq[arr[r]] += 1
			most_freq = max(freq, key=lambda x: freq[x])
			amt_most_freq = freq[most_freq]

			if (r - l + 1) - amt_most_freq > k:
				freq[arr[l]] -= 1
				l += 1
			
			best = max(best, r - l + 1)
		
		return best
```

## 3. Longest Substring Without Repeating Characters
https://leetcode.com/problems/longest-substring-without-repeating-characters/description/

```py
class Solution:
	def lengthOfLongestSubstring(self, arr):
		n, l, best, window = len(arr), 0, 0, set()
		for r in range(n):
			while arr[r] in window:
				window.remove(arr[l])
				l += 1

			window.add(arr[r])
			best = max(best, len(window))

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

		total, l = 0, 0
		for r in range(n):
			total += arr[r]
			if total < 0:
				l = r + 1
				total = 0

		return -1 if sum(arr) < 0 else l
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
		arr.sort()
		n, result = len(arr), set()

		for i in range(n):
			l, r = i + 1, n - 1
			while l < r:
				total = arr[i] + arr[l] + arr[r]
				if total < 0: l += 1
				if total > 0: r -= 1
				if total == 0:
					result.add((arr[i], arr[l], arr[r]))
					l += 1

		return list(result)
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

## 167. Two Sum II - Input Array Is Sorted
https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/

```py
class Solution:
	def twoSum(self, arr, target):
		n = len(arr)
		l, r = 0, n - 1
		while l < r:
			if arr[l] + arr[r] < target:
				l += 1
			elif arr[l] + arr[r] > target:
				r -= 1
			else:
				return [l + 1, r + 1]
```
