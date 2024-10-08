# 121. Best Time to Buy and Sell Stock

Say you have an array for which the ith element is the price of a given stock on day i. If you were only permitted to complete at most one transaction (i.e., buy one and sell one share of the stock), design an algorithm to find the maximum profit. Not that you cannot sell a stock before you buy one.

## Solution (use two-pointer)

```python
def maxProfit(self, prices: list[int]) -> int:
    l, r = 0, 1 # left = buy, right = sell
    maxProfit = 0

    while r < len(prices):
        if prices[l] < prices[r]:
            profit = prices[r] - prices[l]
            maxProfit = max(maxProfit, profit)
        else:
            l = r
        r += 1
    return maxProfit
```
