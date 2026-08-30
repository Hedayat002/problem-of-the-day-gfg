### 1. Brute Force

```python
class Solution:
    def getMarks(self, l, r, rank):
        marks = []

        for i in range(len(l)):
            for x in range(l[i], r[i] + 1):
                marks.append(x)

        ans = []

        for x in rank:
            ans.append(marks[x - 1])

        return ans
```

**TC:** O(total number of valid marks + q)
**SC:** O(total number of valid marks)

---

### 2. Better — Prefix + Sorted Queries

```python
class Solution:
    def getMarks(self, l, r, rank):
        n = len(l)

        prefix = [0] * n
        prefix[0] = r[0] - l[0] + 1

        for i in range(1, n):
            prefix[i] = prefix[i - 1] + (r[i] - l[i] + 1)

        queries = sorted((x, i) for i, x in enumerate(rank))
        ans = [0] * len(rank)

        interval = 0

        for x, original_index in queries:
            while prefix[interval] < x:
                interval += 1

            before = 0 if interval == 0 else prefix[interval - 1]
            ans[original_index] = l[interval] + (x - before - 1)

        return ans
```

**TC:** O(n + q log q)
**SC:** O(n + q)

---

### 3. Optimal — Prefix + Binary Search

```python
class Solution:
    def findInterval(self, prefix, rank):
        low = 0
        high = len(prefix) - 1

        while low < high:
            mid = low + (high - low) // 2

            if prefix[mid] < rank:
                low = mid + 1
            else:
                high = mid

        return low

    def getMarks(self, l, r, rank):
        n = len(l)

        prefix = [0] * n
        prefix[0] = r[0] - l[0] + 1

        for i in range(1, n):
            prefix[i] = prefix[i - 1] + (r[i] - l[i] + 1)

        ans = []

        for x in rank:
            idx = self.findInterval(prefix, x)

            before = 0 if idx == 0 else prefix[idx - 1]

            ans.append(l[idx] + (x - before - 1))

        return ans
```

**TC:** O(n + q log n)
**SC:** O(n)
