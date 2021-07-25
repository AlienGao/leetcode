# 剑指 Offer 05. 替换空格
请实现一个函数，把字符串 s 中的每个空格替换成"%20"。

示例 1：

    输入：s = "We are happy."
    输出："We%20are%20happy."

限制：

 - 0 <= s 的长度 <= 10000

解答

    /**
     * @param {string} s
     * @return {string}
     */
    var replaceSpace = function(s) {
        s = s.split('')
        let oldLength = s.length
        let spaceCount = 0
        for (let i = 0; i < oldLength; i++) {
            if (s[i] === " ") {
                spaceCount++
            }
        }
        // 增加数组长度 每个空格增加两位长度
        s.length += spaceCount * 2
        for (let i = s.length - 1, j = oldLength - 1; j >= 0; i--, j--) {
            // 遇到空格 替换
            if (s[j] === " ") {
                s[i] = "0"
                s[i-1] = "2"
                s[i-2] = "%"
                i = i - 2
            } else {
                s[i] = s[j]
            }
        }
        return s.join('')
    };


