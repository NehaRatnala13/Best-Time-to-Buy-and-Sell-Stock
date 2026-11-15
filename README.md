# 121. Best Time to Buy and Sell Stock

- **Difficulty:** Easy
- **Topics:** Array, Dynamic Programming, Greedy
- **Problem Link:** [LeetCode 121](https://leetcode.com)

---

## 📝 Problem Description

You are given an array `prices` where `prices[i]` is the price of a given stock on the \(i^{th}\) day.

You want to maximize your profit by choosing a **single day** to buy one stock and choosing a **different day in the future** to sell that stock.

Return *the maximum profit you can achieve from this transaction*. If you cannot achieve any profit, return `0`.

### Examples

**Example 1:**
```text
Input: prices = [7,1,5,3,6,4]
Output: 5
Explanation: Buy on day 2 (price = 1) and sell on day 5 (price = 6), profit = 6-1 = 5.
Note that buying on day 2 and selling on day 1 is not allowed because you must buy before you sell.
```

**Example 2:**
```text
Input: prices = [7,6,4,3,1]
Output: 0
Explanation: In this case, no transactions are done and the max profit = 0.
```

### Constraints
- 1 ≤ prices.length ≤ 10⁵
- \(0 \le \text{prices}[i] \le 10^4\)

---

## 💡 Approach & Intuition

To maximize profit, we need to find the largest difference between a selling price and a buying price that comes **before** it. 

Instead of checking every possible pair of days (which would take O(n²) time), we can solve this in a single pass:
1. Track the **minimum price** seen so far (`min_price`).
2. For each day's price, calculate the potential profit if we sold today (`price - min_price`).
3. Update `max_profit` if today's potential profit is higher than our previous best.
4. Update `min_price` if today's price is lower than the lowest price seen so far.

---

## 📊 Complexity Analysis

- **Time Complexity:** \(\mathcal{O}(n)\), where n is the length of the `prices` array. We only iterate through the array once.
- **Space Complexity:** \(\mathcal{O}(1)\), as we only use two variables (`min_price` and `max_profit`) regardless of the input size.

---

## 💻 Solutions

### Python
```python
class Solution:
    def maxProfit(self, prices: list[int]) -> int:
        min_price = float('inf')
        max_profit = 0
        
        for price in prices:
            if price < min_price:
                min_price = price
            elif price - min_price > max_profit:
                max_profit = price - min_price
                
        return max_profit
```


```
