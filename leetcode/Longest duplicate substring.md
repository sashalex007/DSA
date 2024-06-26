  
**Link:** https://leetcode.com/problems/longest-duplicate-substring/  
#### Solution:  
  
**Topics**: [binary search](binary%20search.md), [rabin-karp](rabin-karp.md)  
  
**Intuition**  
 Very tricky problem. Binary search is used because if there exists a duplicate substring of length n, then there is guaranteed to be a duplicate substring of length n-1. The idea is to perform binary search with a sliding window to check if there exists a duplicate substring.  
  
The optimal solution requires the rabin-karp algorithm because a simple sliding window and set requires slicing the string, and slicing is o(length) time complexity. Rabin-karp allows us to slice and hash a substring in O(1) time.   
  
Rabin-karp is pretty complicated to code by hand, but python provides a very nice class `memoryview` that allows for O(1) slicing! The reason being is that when you slice the `memoryview` object, it does not create a new object, only a reference to the underlying data.  
  
**Implementation**  
```python  
def longest_dup(s):  
	def has_dup(length):  
		has = set()  
		l = 0  
		for r in range(length, len(s)+1):  
			curr = s_data[l:r]  
			if curr in has:  
				return s[l:r]  
			has.add(curr)  
			l += 1  
		return ''  
  
	s_data = memoryview(s.encode()) #remember this!  
	res = ''  
	l = 1  
	r = len(s)-1  
	while l <= r:  
		mid = (l + r) // 2  
		dup = has_dup(mid)  
		if len(dup):  
			l = mid + 1  
			res = dup if len(dup) > len(res) else res  
		else:  
			r = mid - 1  
	return res  
	  
#time: o(nlogn)  
#memory: o(n)  
```  
  
**Visual**   
![Open Leetcode.jpeg](./_pics/Open%20Leetcode.jpeg)  
  
#review   
#hard   
  
