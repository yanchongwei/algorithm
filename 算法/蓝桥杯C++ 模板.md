## 📜 蓝桥杯冲刺专用 C++ 精炼模板合集

（建议打印出来或每天手写一遍）

### ✅ 快速幂

```
cppCopy codelong long qpow(long long a, long long b, long long mod) {
    long long res = 1;
    a %= mod;
    while (b) {
        if (b & 1) res = res * a % mod;
        a = a * a % mod;
        b >>= 1;
    }
    return res;
}
```

### ✅ 欧几里得算法 GCD

```
cpp


Copy code
int gcd(int a, int b) { return b == 0 ? a : gcd(b, a % b); }
```

### ✅ 组合数（预处理阶乘版）

```
cppCopy codeconst int N = 1e5 + 10, MOD = 1e9 + 7;
long long fac[N], inv[N];
long long qpow(long long a, long long b) {...}  // 上面快速幂模板
void init() {
    fac[0] = inv[0] = 1;
    for (int i = 1; i < N; i++) {
        fac[i] = fac[i - 1] * i % MOD;
        inv[i] = qpow(fac[i], MOD - 2, MOD);
    }
}
long long C(int n, int m) {
    if (m > n) return 0;
    return fac[n] * inv[m] % MOD * inv[n - m] % MOD;
}
```

### ✅ DFS（经典八皇后/排列模板）

```
cppCopy codevoid dfs(int step) {
    if (step == n + 1) {
        // 记录结果
        return;
    }
    for (int i = 1; i <= n; i++) {
        if (!vis[i]) {
            vis[i] = true;
            a[step] = i;
            dfs(step + 1);
            vis[i] = false;
        }
    }
}
```

### ✅ 背包DP（0/1 背包模板）

```
cppCopy codefor (int i = 1; i <= n; i++) 
    for (int j = V; j >= v[i]; j--) 
        dp[j] = max(dp[j], dp[j - v[i]] + w[i]);
```

### ✅ 二分模板

```
cppCopy codeint l = 0, r = n - 1;
while (l <= r) {
    int mid = l + r >> 1;
    if (check(mid)) r = mid - 1;
    else l = mid + 1;
}
```

### ✅ 字符串 KMP

```
cppCopy codevoid getNext(string s) {
    int n = s.size();
    next[0] = -1;
    for (int i = 1, j = -1; i < n; i++) {
        while (j != -1 && s[i] != s[j + 1]) j = next[j];
        if (s[i] == s[j + 1]) j++;
        next[i] = j;
    }
}
```

# 自己总结的

## 删除链表元素递归表示

```cpp
class Solution {
public:
    ListNode* removeElements(ListNode* head, int val) {
        // 基础情况：空链表
        if (head == nullptr) {
            return nullptr;
        }

        // 递归处理
        if (head->val == val) {
            ListNode* newHead = removeElements(head->next, val);
            delete head;
            return newHead;
        } else {
            head->next = removeElements(head->next, val);
            return head;
        }
    }
};
```

