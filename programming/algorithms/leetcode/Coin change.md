# Coin change

URL: https://leetcode.com/problems/coin-change/submissions/

Categories:
1. [[Dynamic programming]]

Insights:
1. We know we can use a coin if `target` - `coin value` is `>=` 0.
2. If we use a coin in reaching a given amount, the total number of coins used to reach the amount is 1 + `numberOfCoins(targetAmount - currentCoinVal)`.
3. Since we know the number of coins to reach 0 is 0, we can build up from there, memoizing the number of coins needed to reach every integer from 1 to the target amount.

Notes:
What tripped me up about this problem was the need to iterate over and memoize possible *amounts*.  I thought I needed to explicitly track the number of times I used a given coin, starting at the max possible and decrementing.  Instead, use the minimum number of coins required to reach smaller amounts to figure out the number of coins needed to reach the current amount.

Solution:
```javascript
var coinChange = function(coins, amount) {
	const idx = Array(amount + 1).fill(amount + 1);
	idx[0] = 0;
    
    for(let currAmt = 1; currAmt < idx.length; currAmt++){
        for(let j = 0; j < coins.length; j++){
            const coinVal = coins[j];
            
            if(coinVal > currAmt) continue;
            
            idx[currAmt] = Math.min(idx[currAmt], 1 + idx[currAmt - coinVal]);
        }
    }
    
    return idx[amount] > amount ? -1 : idx[amount];
};
```