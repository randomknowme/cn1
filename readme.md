https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
# ANSWER


---

Q1. Missing Number
Aim:
Find the missing number from 0..n in an array of size n.

Description:
We XOR all numbers 1..n and all elements of the array. Their XOR gives the missing number.

Full Code:

```py
class Solution:
    def missingNumber(self, nums):
        xor1 = 0
        xor2 = 0
        for i in range(len(nums)):
            xor1 = xor1 ^ (i + 1)
            xor2 = xor2 ^ nums[i]
        return xor1 ^ xor2


if __name__ == "__main__":
    nums = [3, 0, 1]
    print("Missing Number:", Solution().missingNumber(nums))
```

Complexity:
Time: O(n)
Space: O(1)

Output:
Missing Number: 2

---

Q2. Hamming Weight (Number of 1 Bits)
Aim:
Count number of 1s in binary representation of a number.

Description:
Use Brian Kernighan’s method: repeatedly clear the lowest set bit using `n & (n-1)`.

Full Code:

```py
class Solution:
    def hammingWeight(self, n):
        cnt = 0
        while n > 0:
            cnt += 1
            n = n & (n - 1)
        return cnt


if __name__ == "__main__":
    n = 11   # binary 1011
    print("Hamming Weight:", Solution().hammingWeight(n))
```

Complexity:
Time: O(k), where k = number of set bits
Space: O(1)

Output:
Hamming Weight: 3

---

Q3. Middle of the Linked List
Aim:
Find the middle node of a linked list.

Description:
Use slow and fast pointers; when fast reaches end, slow is at the middle.

Full Code:

```py
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def middleNode(self, head):
        slow = head
        fast = head
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
        return slow


if __name__ == "__main__":
    head = ListNode(1, ListNode(2, ListNode(3, ListNode(4, ListNode(5)))))
    mid = Solution().middleNode(head)
    print("Middle Node:", mid.val)
```

Complexity:
Time: O(n)
Space: O(1)

Output:
Middle Node: 3

---

Q4. Linked List Cycle II
Aim:
Detect the node where a cycle begins in a linked list.

Description:
Use Floyd’s cycle detection algorithm (slow and fast pointers).

Full Code:

```py
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def detectCycle(self, head):
        slow = head
        fast = head
        while fast and fast.next:
            fast = fast.next.next
            slow = slow.next
            if slow == fast:
                slow = head
                while slow != fast:
                    slow = slow.next
                    fast = fast.next
                return slow
        return None


if __name__ == "__main__":
    node4 = ListNode(-4)
    node3 = ListNode(0, node4)
    node2 = ListNode(2, node3)
    node1 = ListNode(3, node2)
    node4.next = node2  # create cycle
    cycle_node = Solution().detectCycle(node1)
    print("Cycle starts at:", cycle_node.val if cycle_node else None)
```

Complexity:
Time: O(n)
Space: O(1)

Output:
Cycle starts at: 2

---

Q5. Remove Nth Node From End
Aim:
Remove the nth node from the end of a linked list.

Description:
Advance fast pointer by n, then move both until fast reaches end. Delete slow\.next.

Full Code:

```py
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def removeNthFromEnd(self, head, n):
        if not head or not head.next:
            return None
        slow = head
        fast = head
        for _ in range(n):
            fast = fast.next
        if not fast:
            return head.next
        while fast.next:
            slow = slow.next
            fast = fast.next
        slow.next = slow.next.next
        return head


if __name__ == "__main__":
    head = ListNode(1, ListNode(2, ListNode(3, ListNode(4, ListNode(5)))))
    new_head = Solution().removeNthFromEnd(head, 2)
    curr = new_head
    while curr:
        print(curr.val, end=" -> ")
        curr = curr.next
    print("None")
```

Complexity:
Time: O(n)
Space: O(1)

Output:
1 -> 2 -> 3 -> 5 -> None

---

Q6. Merge Two Sorted Lists
Aim:
Merge two sorted linked lists into a single sorted list.

Description:
Compare nodes one by one using two pointers and a dummy head.

Full Code:

```py
class ListNode:
    def __init__(self, val=0, next=None):
        self.val = val
        self.next = next

class Solution:
    def mergeTwoLists(self, list1, list2):
        ptr1 = list1
        ptr2 = list2
        dummy = ListNode(0)
        curr = dummy
        while ptr1 and ptr2:
            if ptr1.val <= ptr2.val:
                curr.next = ptr1
                ptr1 = ptr1.next
            else:
                curr.next = ptr2
                ptr2 = ptr2.next
            curr = curr.next
        curr.next = ptr1 if ptr1 else ptr2
        return dummy.next


if __name__ == "__main__":
    l1 = ListNode(1, ListNode(2, ListNode(4)))
    l2 = ListNode(1, ListNode(3, ListNode(5)))
    merged = Solution().mergeTwoLists(l1, l2)
    while merged:
        print(merged.val, end=" -> ")
        merged = merged.next
    print("None")
```

Complexity:
Time: O(m+n)
Space: O(1)

Output:
1 -> 1 -> 2 -> 3 -> 4 -> 5 -> None

---

Q7. Daily Temperatures
Aim:
Find how many days you must wait for a warmer temperature.

Description:
Use a stack to track indices of decreasing temperatures, traverse from right to left.

Full Code:

```py
class Solution:
    def dailyTemperatures(self, temp):
        st = []
        n = len(temp)
        res = [0] * n
        for i in range(n - 1, -1, -1):
            while st and temp[i] >= temp[st[-1]]:
                st.pop()
            res[i] = 0 if not st else st[-1] - i
            st.append(i)
        return res


if __name__ == "__main__":
    temps = [73, 74, 75, 71, 69, 72, 76, 73]
    print("Result:", Solution().dailyTemperatures(temps))
```

Complexity:
Time: O(n)
Space: O(n)

Output:
Result: \[1, 1, 4, 2, 1, 1, 0, 0]

---

Q8. Find Median from Data Stream
Aim:
Design a structure to add numbers and find median dynamically.

Description:
Use two heaps: max-heap (left) for smaller half, min-heap (right) for larger half. Balance them.

Full Code:

```py
import heapq

class MedianFinder:
    def __init__(self):
        self.left = []   # max-heap (store negatives)
        self.right = []  # min-heap

    def addNum(self, num):
        heapq.heappush(self.left, -num)
        if self.left and self.right and -self.left[0] > self.right[0]:
            ele = -heapq.heappop(self.left)
            heapq.heappush(self.right, ele)
        if len(self.left) > len(self.right) + 1:
            ele = -heapq.heappop(self.left)
            heapq.heappush(self.right, ele)
        if len(self.right) > len(self.left) + 1:
            ele = heapq.heappop(self.right)
            heapq.heappush(self.left, -ele)

    def findMedian(self):
        if len(self.right) == len(self.left):
            return (-self.left[0] + self.right[0]) / 2
        elif len(self.left) > len(self.right):
            return -self.left[0]
        else:
            return self.right[0]


if __name__ == "__main__":
    mf = MedianFinder()
    mf.addNum(1)
    mf.addNum(2)
    print("Median:", mf.findMedian())
    mf.addNum(3)
    print("Median:", mf.findMedian())
```

Complexity:
Time: O(log n) per insertion, O(1) for median
Space: O(n)

Output:
Median: 1.5
Median: 2

---

Q9. Longest Substring Without Repeating Characters
Aim:
Find the length of the longest substring without repeating characters.

Description:
Use sliding window with a set to track characters. Move left pointer when duplicate found.

Full Code:

```py
class Solution:
    def lengthOfLongestSubstring(self, s: str) -> int:
        seen = set()
        l = 0
        maxlen = 0
        for r in range(len(s)):
            while s[r] in seen:
                seen.remove(s[l])
                l += 1
            seen.add(s[r])
            maxlen = max(maxlen, r - l + 1)
        return maxlen


if __name__ == "__main__":
    s = "abcabcbb"
    print("Length of Longest Substring:", Solution().lengthOfLongestSubstring(s))
```

Complexity:
Time: O(n)
Space: O(n)

Output:
Length of Longest Substring: 3

---

Q10. Spiral Matrix
Aim:
Return elements of a matrix in spiral order.

Description:
Use boundaries (top, bottom, left, right) and traverse in 4 directions until all elements are covered.

Full Code:

```py
class Solution:
    def spiralOrder(self, matrix):
        n = len(matrix)
        m = len(matrix[0])
        top, bottom, left, right = 0, n - 1, 0, m - 1
        ans = []
        while left <= right and top <= bottom:
            for i in range(left, right + 1):
                ans.append(matrix[top][i])
            top += 1
            for i in range(top, bottom + 1):
                ans.append(matrix[i][right])
            right -= 1
            if top <= bottom:
                for i in range(right, left - 1, -1):
                    ans.append(matrix[bottom][i])
                bottom -= 1
            if left <= right:
                for i in range(bottom, top - 1, -1):
                    ans.append(matrix[i][left])
                left += 1
        return ans


if __name__ == "__main__":
    mat = [[1,2,3],[4,5,6],[7,8,9]]
    print("Spiral Order:", Solution().spiralOrder(mat))
```

Complexity:
Time: O(m × n)
Space: O(1)

Output:
Spiral Order: \[1, 2, 3, 6, 9, 8, 7, 4, 5]

---

Q11. Container With Most Water
Aim:
Find two lines that form a container holding the most water.

Description:
Use two pointers at both ends, calculate area, and move inward from shorter line.

Full Code:

```py
class Solution:
    def maxArea(self, height):
        l, r = 0, len(height) - 1
        maxarea = 0
        while l < r:
            area = min(height[l], height[r]) * (r - l)
            maxarea = max(maxarea, area)
            if height[l] < height[r]:
                l += 1
            else:
                r -= 1
        return maxarea


if __name__ == "__main__":
    h = [1,8,6,2,5,4,8,3,7]
    print("Max Area:", Solution().maxArea(h))
```

Complexity:
Time: O(n)
Space: O(1)

Output:
Max Area: 49

---

Q12. 3Sum
Aim:
Find all unique triplets in array that sum to zero.

Description:
Sort array, fix one element, then use two-pointer approach to find pairs.

Full Code:

```py
class Solution:
    def threeSum(self, nums):
        nums.sort()
        res = []
        n = len(nums)
        for i in range(n):
            if i > 0 and nums[i] == nums[i-1]:
                continue
            l, r = i + 1, n - 1
            while l < r:
                total = nums[i] + nums[l] + nums[r]
                if total < 0:
                    l += 1
                elif total > 0:
                    r -= 1
                else:
                    res.append([nums[i], nums[l], nums[r]])
                    l += 1
                    while l < r and nums[l] == nums[l-1]:
                        l += 1
        return res


if __name__ == "__main__":
    nums = [-1,0,1,2,-1,-4]
    print("Triplets:", Solution().threeSum(nums))
```

Complexity:
Time: O(n²)
Space: O(1) (excluding output)

Output:
Triplets: \[\[-1, -1, 2], \[-1, 0, 1]]

---

Q13. Remove Duplicates from Sorted Array
Aim:
Remove duplicates in-place such that each unique element appears once.

Description:
Use two pointers. One iterates through array, the other tracks unique elements.

Full Code:

```py
class Solution:
    def removeDuplicates(self, nums):
        if not nums:
            return 0
        i = 0
        for j in range(1, len(nums)):
            if nums[j] != nums[i]:
                i += 1
                nums[i] = nums[j]
        return i + 1


if __name__ == "__main__":
    arr = [0,0,1,1,1,2,2,3,3,4]
    k = Solution().removeDuplicates(arr)
    print("Unique count:", k)
    print("Modified array:", arr[:k])
```

Complexity:
Time: O(n)
Space: O(1)

Output:
Unique count: 5
Modified array: \[0, 1, 2, 3, 4]

---

Q14. Rotate Image
Aim:
Rotate an n×n matrix by 90 degrees (clockwise).

Description:
First transpose matrix, then reverse each row.

Full Code:

```py
class Solution:
    def rotate(self, matrix):
        n = len(matrix)
        # Transpose
        for i in range(n):
            for j in range(i, n):
                matrix[i][j], matrix[j][i] = matrix[j][i], matrix[i][j]
        # Reverse each row
        for row in matrix:
            row.reverse()
        return matrix


if __name__ == "__main__":
    mat = [[1,2,3],[4,5,6],[7,8,9]]
    print("Rotated Matrix:", Solution().rotate(mat))
```

Complexity:
Time: O(n²)
Space: O(1)

Output:
Rotated Matrix: \[\[7, 4, 1], \[8, 5, 2], \[9, 6, 3]]

---

Q15. Word Search
Aim:
Determine if a word exists in a 2D board of characters.

Description:
Use DFS with backtracking, exploring up, down, left, right while marking visited.

Full Code:

```py
class Solution:
    def exist(self, board, word):
        n, m = len(board), len(board[0])

        def dfs(i, j, idx):
            if idx == len(word):
                return True
            if i < 0 or j < 0 or i >= n or j >= m or board[i][j] != word[idx]:
                return False
            temp = board[i][j]
            board[i][j] = "#"
            found = (dfs(i+1,j,idx+1) or dfs(i-1,j,idx+1) or
                     dfs(i,j+1,idx+1) or dfs(i,j-1,idx+1))
            board[i][j] = temp
            return found

        for i in range(n):
            for j in range(m):
                if dfs(i, j, 0):
                    return True
        return False


if __name__ == "__main__":
    board = [
        ["A","B","C","E"],
        ["S","F","C","S"],
        ["A","D","E","E"]
    ]
    word = "ABCCED"
    print("Exists:", Solution().exist(board, word))
```

Complexity:
Time: O(n × m × 4^L), where L = length of word
Space: O(L) recursion stack

Output:
Exists: True

---

Q16. Largest Rectangle in Histogram
Aim:
Find the largest rectangle area in a histogram.

Description:
Use stack to maintain increasing bars, calculate area when popping.

Full Code:

```py
class Solution:
    def largestRectangleArea(self, heights):
        st = []
        maxarea = 0
        heights.append(0)
        for i, h in enumerate(heights):
            while st and heights[st[-1]] > h:
                height = heights[st.pop()]
                width = i if not st else i - st[-1] - 1
                maxarea = max(maxarea, height * width)
            st.append(i)
        return maxarea


if __name__ == "__main__":
    heights = [2,1,5,6,2,3]
    print("Largest Rectangle Area:", Solution().largestRectangleArea(heights))
```

Complexity:
Time: O(n)
Space: O(n)

Output:
Largest Rectangle Area: 10

---


# END
https://github.com/randomknowme/cn1

https://github.com/randomknowme/cn2

https://github.com/randomknowme/cn3
