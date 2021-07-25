# 剑指 Offer 50. 第一个只出现一次的字符
在字符串 s 中找出第一个只出现一次的字符。如果没有，返回一个单空格。 s 只包含小写字母。

示例:

    s = "abaccdeff"
    返回 "b"
    
    s = "" 
    返回 " "

限制：

 - 0 <= s 的长度 <= 50000

解答

    /**
     * @param {string} s
     * @return {character}
     */
    var firstUniqChar = function(s) {
        let arr = s.split('')
        let map = new Map()
        for (let i = 0; i < arr.length; i++) {
            // 使用map记录每个字符出现次数
            if (map.has(arr[i])) {
                map.set(arr[i], map.get(arr[i]) + 1)
            } else {
                map.set(arr[i], 1)
            }
        }
        // 筛选出只出现一次的字符
        let result = [...map].filter(([k, v]) => v === 1)
        return result.length > 0 ? result[0][0] : " "
        
        
        let result = []
        for (let i = 0; i < s.length; i++) {
            // 唯一添加进数组
            if (s.indexOf(s[i]) === i) {
                result.push(s[i])
            } else {
            // 重复出现 踢出result数组
                if (result.indexOf(s[i]) > -1) {
                    result.splice(result.indexOf(s[i]), 1)
                }
            }
        }
        return result.length === 0 ? " " : result[0]
    };