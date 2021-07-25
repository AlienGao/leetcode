# 剑指 Offer 09. 用两个栈实现队列
用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

示例 1：

    输入：
    ["CQueue","appendTail","deleteHead","deleteHead"]
    [[],[3],[],[]]
    输出：[null,null,3,-1]

示例 2：

    输入：
    ["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
    [[],[],[5],[2],[],[]]
    输出：[null,-1,null,null,5,2]

提示：

 - 1 <= values <= 10000
 - 最多会对 appendTail、deleteHead 进行 10000 次调用

解答

    var CQueue = function() {
        this.stackA = []
        this.stackB = []
    };
    
    /** 
     * @param {number} value
     * @return {void}
     */
    CQueue.prototype.appendTail = function(value) {
        this.stackA.push(value)
    };
    
    /**
     * @return {number}
     */
    CQueue.prototype.deleteHead = function() {
        // 假如栈B内有数据 先将B内数据移除
        if (this.stackB.length) {
            return this.stackB.pop()
        } else {
            // 否则将A中数据导入B中
            while(this.stackA.length) {
                this.stackB.push(this.stackA.pop())
            }
            // 若B没有数据返回-1
            if (!this.stackB.length) {
                return -1
            } else {
                return this.stackB.pop()
            }
        }
    };
    
    /**
     * Your CQueue object will be instantiated and called as such:
     * var obj = new CQueue()
     * obj.appendTail(value)
     * var param_2 = obj.deleteHead()
     */