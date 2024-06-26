### 题目描述

这是 LeetCode 上的 **[剑指 Offer II 009. 乘积小于 K 的子数组](https://leetcode.cn/problems/ZVAVXX/solution/by-ac_oier-lop5/)** ，难度为 **中等**。

Tag : 「滑动窗口」、「双指针」



给你一个整数数组 `nums` 和一个整数 $k$ ，请你返回子数组内所有元素的乘积严格小于 $k$ 的连续子数组的数目。

示例 1：
```
输入：nums = [10,5,2,6], k = 100

输出：8

解释：8 个乘积小于 100 的子数组分别为：[10]、[5]、[2],、[6]、[10,5]、[5,2]、[2,6]、[5,2,6]。
需要注意的是 [10,5,2] 并不是乘积小于 100 的子数组。
```
示例 2：
```
输入：nums = [1,2,3], k = 0

输出：0
```

提示: 
* $1 <= nums.length <= 3 \times 10^4$
* $1 <= nums[i] <= 1000$
* $0 <= k <= 10^6$

---

### 滑动窗口

利用 $1 <= nums[i] <= 1000$，我们可以从前往后处理所有的 $nums[i]$，使用一个变量 $cur$ 记录当前窗口的乘积，使用两个变量 $j$ 和 $i$ 分别代表当前窗口的左右端点。

当 $cur >= k$ 时，我们考虑将左端点 $j$ 右移，同时消除原来左端点元素 $nums[j]$ 对 $cur$ 的贡献，直到 $cur >= k$ 不再满足，这样我们就可以得到每个右端点 $nums[i]$ 的最远左端点 $nums[j]$，从而得知以 $nums[i]$ 为结尾的合法子数组个数为 $i - j + 1$。

Java 代码：
```Java 
class Solution {
    public int numSubarrayProductLessThanK(int[] nums, int k) {
        int n = nums.length, ans = 0;
        if (k <= 1) return 0;
        for (int i = 0, j = 0, cur = 1; i < n; i++) {
            cur *= nums[i];
            while (cur >= k) cur /= nums[j++];
            ans += i - j + 1;
        }
        return ans;
    }
}
```
TypeScript 代码：
```TypeScript
function numSubarrayProductLessThanK(nums: number[], k: number): number {
    let n = nums.length, ans = 0
    if (k <= 1) return 0
    for (let i = 0, j = 0, cur = 1; i < n; i++) {
        cur *= nums[i]
        while (cur >= k) cur /= nums[j++]
        ans += i - j + 1
    }
    return ans
};
```
* 时间复杂度：$O(n)$
* 空间复杂度：$O(1)$

---

### 最后

这是我们「刷穿 LeetCode」系列文章的第 `剑指 Offer II 009` 篇，系列开始于 2021/01/01，截止于起始日 LeetCode 上共有 1916 道题目，部分是有锁题，我们将先把所有不带锁的题目刷完。

在这个系列文章里面，除了讲解解题思路以外，还会尽可能给出最为简洁的代码。如果涉及通解还会相应的代码模板。

为了方便各位同学能够电脑上进行调试和提交代码，我建立了相关的仓库：https://github.com/SharingSource/LogicStack-LeetCode 。

在仓库地址里，你可以看到系列文章的题解链接、系列文章的相应代码、LeetCode 原题链接和其他优选题解。

