# 剑指 Offer 49. 丑数
我们把只包含质因子 2、3 和 5 的数称作丑数（Ugly Number）。求按从小到大的顺序的第 n 个丑数。

示例:

    输入: n = 10
    输出: 12
    解释: 1, 2, 3, 4, 5, 6, 8, 9, 10, 12 是前 10 个丑数。

说明:  

 - 1 是丑数。
 - n 不超过1690。
 
解答

    /**
     * @param {number} n
     * @return {number}
     */
    var nthUglyNumber = function(n) {
        let dp = new Array(n + 1).fill(0)
        dp[1] = 1
        let p2 = 1, p3 = 1, p5 = 1
        for (let i = 2; i <= n; i++) {
            let num2 = dp[p2] * 2, num3 = dp[p3] * 3, num5 = dp[p5] * 5
            dp[i] = Math.min(Math.min(num2, num3), num5)
            if (dp[i] === num2) {
                p2++
            }
            if (dp[i] === num3) {
                p3++
            }
            if (dp[i] === num5) {
                p5++
            }
        }
        return dp[n]
    };