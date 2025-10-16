https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
# ANSWER



---

## 🧩 **U1 – Reverse Linked List**

**Aim**
Reverse a singly linked list.

**Description – 3m**
Uses recursion to reverse the linked list — the tail becomes the new head.

**Example – 2m**
Input: `[1, 2, 3, 4, 5]`
Output: `[5, 4, 3, 2, 1]`

**Program – 5m**

```python
class ListNode:
    def __init__(self, val=0, nxt=None):
        self.val = val
        self.next = nxt

def reverseList(head):
    if not head or not head.next:
        return head
    newHead = reverseList(head.next)
    head.next.next = head
    head.next = None
    return newHead

# Simplified main
a = ListNode(1, ListNode(2, ListNode(3, ListNode(4, ListNode(5)))))
res = reverseList(a)
out = []
while res:
    out.append(res.val)
    res = res.next
print(out)
```

**Expected Output**
`[5, 4, 3, 2, 1]`

**Actual Output – 2m**
`[5, 4, 3, 2, 1]`

---

## 🧩 **U1 – Remove Nth Node From End**

**Aim**
Remove the nth node from the end of a linked list.

**Description – 3m**
Move one pointer `n` steps ahead, then move both until the first reaches the end; remove the node.

**Example – 2m**
Input: `[1,2,3,4,5], n=2`
Output: `[1,2,3,5]`

**Program – 5m**

```python
class ListNode:
    def __init__(self, val=0, nxt=None):
        self.val = val
        self.next = nxt

def removeNthFromEnd(head, n):
    if not head or not head.next:
        return None
    slow = fast = head
    for _ in range(n):
        fast = fast.next
    if not fast:
        return head.next
    while fast.next:
        slow = slow.next
        fast = fast.next
    slow.next = slow.next.next
    return head

# Main simplified
a = ListNode(1, ListNode(2, ListNode(3, ListNode(4, ListNode(5)))))
res = removeNthFromEnd(a, 2)
out = []
while res:
    out.append(res.val)
    res = res.next
print(out)
```

**Expected Output**
`[1, 2, 3, 5]`

**Actual Output – 2m**
`[1, 2, 3, 5]`

---

## 🧩 **U2 – Top K Frequent Elements**

**Aim**
Return the `k` most frequent elements from an array.

**Description – 3m**
Count frequencies and bucket them; collect top `k` elements from highest frequencies.

**Example – 2m**
Input: `[1,1,1,2,2,3], k=2`
Output: `[1,2]`

**Program – 5m**

```python
def topKFrequent(nums, k):
    freq = {}
    for num in nums:
        freq[num] = freq.get(num, 0) + 1

    bucket = [[] for _ in range(len(nums)+1)]
    for key, val in freq.items():
        bucket[val].append(key)

    res = []
    for i in range(len(bucket)-1, 0, -1):
        for val in bucket[i]:
            res.append(val)
            if len(res) == k:
                return res

print(topKFrequent([1,1,1,2,2,3], 2))
```

**Expected Output**
`[1, 2]`

**Actual Output – 2m**
`[1, 2]`

---

## 🧩 **U2 – Product of Array Except Self**

**Aim**
Return an array where each element is product of all others except itself.

**Description – 3m**
Use prefix and postfix multiplication to avoid division and keep O(1) extra space.

**Example – 2m**
Input: `[1,2,3,4]`
Output: `[24,12,8,6]`

**Program – 5m**

```python
def productExceptSelf(nums):
    n = len(nums)
    res = [1] * n

    prefix = 1
    for i in range(n):
        res[i] = prefix
        prefix *= nums[i]

    postfix = 1
    for i in range(n-1, -1, -1):
        res[i] *= postfix
        postfix *= nums[i]

    return res

print(productExceptSelf([1,2,3,4]))
```

**Expected Output**
`[24, 12, 8, 6]`

**Actual Output – 2m**
`[24, 12, 8, 6]`

---

## 🧩 **U3 – Common Elements Between Two Arrays**

**Aim**
Count how many elements of each array appear in the other.

**Description – 3m**
Use sets for fast membership checks;
count common elements individually for each list.

**Example – 2m**
`nums1=[1,2,2,3], nums2=[2,2,4]` → `[2,2]`

**Program – 5m**

```python
def findIntersectionValues(nums1, nums2):
    set1, set2 = set(nums1), set(nums2)
    c1 = sum(1 for x in nums1 if x in set2)
    c2 = sum(1 for x in nums2 if x in set1)
    return [c1, c2]

print(findIntersectionValues([1,2,2,3], [2,2,4]))
```

**Expected Output**
`[2, 2]`

**Actual Output – 2m**
`[2, 2]`

---

## 🧩 **U3 – Ugly Number**

**Aim**
Check if the number’s only prime factors are 2, 3, and 5.

**Description – 3m**
Keep dividing the number by 2, 3, 5 while divisible.
If final value equals 1 → it’s ugly.

**Example – 2m**
6 → True
14 → False

**Program – 5m**

```python
def isUgly(n):
    if n <= 0: return False
    for p in [2, 3, 5]:
        while n % p == 0:
            n //= p
    return n == 1

print(isUgly(6))
print(isUgly(14))
```

**Expected Output**

```
True
False
```

**Actual Output – 2m**

```
True
False
```

---

## 🧩 **U4 – Best Time to Buy Stocks**

**Aim**
Maximize profit with one buy and one sell.

**Description  3m**
Track the minimum price seen so far and update the maximum profit as the difference between current price and the minimum.

**Example 2m**
Input: `[7,1,5,3,6,4]` → Output: `5`

**Program 5m**

```python
def maxProfit(prices):
    mini = prices[0]
    maxProfit = 0
    for i in range(1, len(prices)):
        maxProfit = max(maxProfit, prices[i] - mini)
        mini = min(mini, prices[i])
    return maxProfit

print(maxProfit([7,1,5,3,6,4]))
```

**Expected output**
`5`

**Actual output 2m**
`5`

---

## 🧩 **U4 – Longest Repeating Character Replacement**

**Aim**
Find the length of the longest substring where you can replace at most `k` characters to make all characters the same.

**Description  3m**
Use a sliding window that tracks character frequencies and the maximum character frequency in the window. If window size minus max frequency > k, shrink from left.

**Example 2m**
Input: `s = "AABABBA", k = 1` → Output: `4`

**Program 5m**

```python
def characterReplacement(s, k):
    freq = [0] * 26
    maxLen = 0
    maxFreq = 0
    n = len(s)
    r, l = 0, 0
    while r < n:
        freq[ord(s[r]) - ord('A')] += 1
        maxFreq = max(maxFreq, freq[ord(s[r]) - ord('A')])
        while (r - l + 1) - maxFreq > k:
            freq[ord(s[l]) - ord('A')] -= 1
            l += 1
        maxLen = max(maxLen, r - l + 1)
        r += 1
    return maxLen

print(characterReplacement("AABABBA", 1))
```

**Expected output**
`4`

**Actual output 2m**
`4`

---

## 🧩 **U4 – Longest Substring Without Repeating Characters**

**Aim**
Return the length of the longest substring with all unique characters.

**Description  3m**
Maintain a sliding window using a set; expand right pointer and remove from set when duplicates encountered, updating maximum length.

**Example 2m**
Input: `s = "abcabcbb"` → Output: `3`

**Program 5m**

```python
def lengthOfLongestSubstring(s):
    seen = set()
    l = r = 0
    maxLen = 0
    while r < len(s):
        while s[r] in seen:
            seen.remove(s[l])
            l += 1
        seen.add(s[r])
        maxLen = max(maxLen, r - l + 1)
        r += 1
    return maxLen

print(lengthOfLongestSubstring("abcabcbb"))
```

**Expected output**
`3`

**Actual output 2m**
`3`

---

## 🧩 **U4 – Minimum Window Substring**

**Aim**
Find the smallest substring in `s` that contains all characters of `t`.

**Description  3m**
Use a frequency array for `t`, expand right to include characters, and shrink left while all required characters are included to find minimum window.

**Example 2m**
Input: `s = "ADOBECODEBANC", t = "ABC"` → Output: `"BANC"`

**Program 5m**

```python
def minWindow(s, t):
    freq = [0] * 256
    n = len(s)
    m = len(t)
    minLen = n + 1
    for ch in t:
        freq[ord(ch)] += 1
    c = l = r = 0
    sIdx = -1
    while r < n:
        if freq[ord(s[r])] > 0:
            c += 1
        freq[ord(s[r])] -= 1
        while c == m:
            if r - l + 1 < minLen:
                minLen = r - l + 1
                sIdx = l
            freq[ord(s[l])] += 1
            if freq[ord(s[l])] > 0:
                c -= 1
            l += 1
        r += 1
    return s[sIdx:sIdx+minLen] if sIdx != -1 else ""

print(minWindow("ADOBECODEBANC", "ABC"))
```

**Expected output**
`BANC`

**Actual output 2m**
`BANC`

---

## 🧩 **U4 – Birthday Paradox**

**Aim**
Compute probability that at least two people share a birthday in a group of `n`.

**Description  3m**
Compute the complement: probability that all birthdays are unique is product_{i=0..n-1} (365 - i)/365. Return `1 - product`.

**Example 2m**
Input: `n = 23` → Output: approximately `0.507297`

**Program 5m**

```python
def birthdayProbability(n):
    if n > 365:
        return 1.0
    prob = 1.0
    for i in range(n):
        prob *= (365.0 - i) / 365.0
    return 1 - prob

print("{:.6f}".format(birthdayProbability(23)))
```

**Expected output**
Approximately: `0.507297`

**Actual output 2m**
`0.507297`

---

## 🧩 **U5 – Find Minimum in Rotated Sorted Array**

**Aim**
Find the minimum element in a rotated sorted array (no duplicates).

**Description  3m**
Binary-search style: if subarray is already sorted, the leftmost is min; otherwise locate the unsorted half containing the minimum.

**Example 2m**
Input: `[3,4,5,1,2]` → Output: `1`

**Program 5m**

```python
def findMin(nums):
    low = 0
    high = len(nums) - 1
    ans = 6e3
    while low <= high:
        mid = (low + high) // 2
        if nums[low] <= nums[high]:
            return min(nums[low], ans)
        if nums[low] <= nums[mid]:
            ans = min(ans, nums[low])
            low = mid + 1
        elif nums[mid] <= nums[high]:
            ans = min(ans, nums[mid])
            high = mid - 1
    return -1

print(findMin([3,4,5,1,2]))
```

**Expected output**
`1`

**Actual output 2m**
`1`

---

## 🧩 **U5 – Binary Search**

**Aim**
Return index of `target` in sorted array `nums`, or `-1` if not present.

**Description  3m**
Standard iterative binary search updating `low`/`high` based on comparisons.

**Example 2m**
Input: `nums = [-1,0,3,5,9,12], target = 9` → Output: `4`

**Program 5m**

```python
def search(nums, target):
    low, high = 0, len(nums) - 1
    while low <= high:
        mid = (low + high) // 2
        if nums[mid] == target:
            return mid
        if nums[mid] > target:
            high = mid - 1
        else:
            low = mid + 1
    return -1

print(search([-1,0,3,5,9,12], 9))
```

**Expected output**
`4`

**Actual output 2m**
`4`



# END
https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
