# 121. Best Time to Buy and Sell Stock

## Problem Statement

You are given an array `prices` where `prices[i]` represents the price of a stock on the `i-th` day.

You want to maximize your profit by choosing:
- One day to buy the stock.
- A future day to sell the stock.

Return the maximum profit you can achieve. If no profit is possible, return `0`.

---

## Example 1

Input:
prices = [7,1,5,3,6,4]

Output:
5

Explanation:
Buy at price 1 and sell at price 6.
Profit = 6 - 1 = 5

---

## Example 2

Input:
prices = [7,6,4,3,1]

Output:
0

Explanation:
No profitable transaction is possible.

---

## Approach

Maintain:
- `minPrice` = Minimum stock price seen so far.
- `maxProfit` = Maximum profit obtained so far.

For each price:
1. Update the minimum buying price.
2. Calculate profit if sold today.
3. Update the maximum profit.

This guarantees buying before selling and finds the answer in a single traversal.

---

## Algorithm

1. Initialize `minPrice = prices[0]` and `maxProfit = 0`.
2. Traverse the array from index 1.
3. If current price is less than `minPrice`, update `minPrice`.
4. Otherwise:
   - Calculate `profit = prices[i] - minPrice`.
   - Update `maxProfit`.
5. Return `maxProfit`.

---

## Java Solution

```java
class Solution {
    public int maxProfit(int[] prices) {
        int minPrice = prices[0];
        int maxProfit = 0;

        for (int i = 1; i < prices.length; i++) {
            if (prices[i] < minPrice) {
                minPrice = prices[i];
            } else {
                maxProfit = Math.max(maxProfit, prices[i] - minPrice);
            }
        }

        return maxProfit;
    }
}
```

---

## Dry Run

Input:
prices = [7,1,5,3,6,4]

| Day | Price | Min Price | Profit | Max Profit |
|-----|--------|-----------|--------|-----------|
| 0 | 7 | 7 | 0 | 0 |
| 1 | 1 | 1 | 0 | 0 |
| 2 | 5 | 1 | 4 | 4 |
| 3 | 3 | 1 | 2 | 4 |
| 4 | 6 | 1 | 5 | 5 |
| 5 | 4 | 1 | 3 | 5 |

Final Answer: 5

---

## Complexity Analysis

- Time Complexity: O(n)
- Space Complexity: O(1)

---

## Key Insight

Keep track of the lowest stock price seen so far and calculate the profit for each day. This allows us to find the maximum profit in a single pass instead of checking all possible buy-sell pairs.
