# 剑指 Offer 12. 矩阵中的路径
给定一个 m x n 二维字符网格 board 和一个字符串单词 word 。如果 word 存在于网格中，返回 true ；否则，返回 false 。
单词必须按照字母顺序，通过相邻的单元格内的字母构成，其中“相邻”单元格是那些水平相邻或垂直相邻的单元格。同一个单元格内的字母不允许被重复使用。
例如，在下面的 3×4 的矩阵中包含单词 "ABCCED"（单词中的字母已标出）。

示例 1：

    输入：board = [["A","B","C","E"],["S","F","C","S"],["A","D","E","E"]], word = "ABCCED"
    输出：true

示例 2：

    输入：board = [["a","b"],["c","d"]], word = "abcd"
    输出：false

 

提示：

 - 1 <= board.length <= 200
 - 1 <= board[i].length <= 200
 - board 和 word 仅由大小写英文字母组成
 
解答

    /**
     * @param {character[][]} board
     * @param {string} word
     * @return {boolean}
     */
    var exist = function(board, word) {
        if (board.length * board[0].length < word.length) return false;
        let result = []
        for (let i = 0; i < board.length; i++) {
            for (let j = 0; j < board[0].length; j++) {
                if (board[i][j] === word[0]) {
                    result.push([i,j])
                }
            }
        }
        
        function dfs(i, j, l) {
            if (i < 0 || j < 0 || i > board.length -1 || j > board[0].length - 1 || board[i][j] !== word[l]) return false
            // 防止往回找匹配字母
            let code = board[i][j]
            board[i][j] = '-'
            l += 1
            if (l === word.length) return true
            let res = dfs(i-1, j, l) || dfs(i+1, j, l) || dfs(i, j-1, l) || dfs(i, j+1, l)
            board[i][j] = code
            return res
            
        }
        for (let i = 0; i < result.length; i++) {
            let l = 0
            if (dfs(result[i][0], result[i][1], l)) return true
        }
        return false
    };