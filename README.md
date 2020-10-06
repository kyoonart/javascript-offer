---
title: 剑指-offer
date: 2020-02-20 21:11:42
preview: 100
---

flag:  今天起开始也刷剑指offer啦，一步一步来。 

### 二维数组的查找

#### 题目描述

在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

```javascript
//思路：题目不难，而且给出的限制也很小，我一开始试试用了暴力逐步循环发现也能通过，但是这题目设计的初衷不是简单的让你用暴力循环查找出来，而是要注意是有顺序的。所以我们查找的起始点最好从二维数组中的中间的点开始，不过为了方便，我们一般都是选择最左下角的那个点作为起始点，也就是a[array.lenth][0],比它大就往右边走，比它小就往上面走。话不多说，上代码。
function Find(target, array) {
    const n = array.length,
        m = array[0].length;
    let row = n - 1,
        col = 0;
    if (m === 0 && n === 0) {
        return false;
    }
    while (row >= 0 && col <= m - 1) {
        if (array[row][col] > target) {
            row--;
        } else if (array[row][col] < target) {
            col++;
        } else return true;
    }
    return false;
}
```

### 替换空格

#### 题目描述

 请实现一个函数，将一个字符串中的空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。 

```javascript
//思路 :这题比较简单把字符串转换为数组除最后一项，每项后面拼接"%20";最后再转换为字符串
function replaceSpace(str) {
    var arr = str.split(' ');
    var len = arr.length;
    for (let i = 0; i < len - 1; i++) {
        arr[i] = arr[i] + '%20';
    }
    return arr.join('');
}
console.log(replaceSpace('We Are Happy'));
//看了别人的解直接用正则替换比较牛逼 一行代码搞定 学习了
function replaceSpace(str) {
  return str.replace(/\s/g, '%20');
}

```

### 从尾到头打印链表

#### 题目描述

 输入一个链表，按链表从尾到头的顺序返回一个ArrayList。 

```javascript
//使用unshift()或者push()+reverse()
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function printListFromTailToHead(head)
{   
    // write code here
     let  res=[];
     let pNode=head;
    while(pNode!==null){
        res.push(pNode.val);
        pNode=pNode.next
    }
    return res.reverse();
}
--------------------------------------
function printListFromTailToHead(head)
{   
    // write code here
     let  res=[];
     let pNode=head;
    while(pNode!==null){
        res.unshift(pNode.val);
        pNode=pNode.next
    }
    return res;
}
```

### 用两个栈实现队列

#### 题目描述

用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

```javascript
const outStack = [],
    inStack = [];
function push(node) {
    // write code here
    inStack.push(node)
}

function pop() {
    // write code here
    // 出栈为空需要把进栈的数据拿到
    if (!outStack.length) {
        while (inStack.length) {
            outStack.push(inStack.pop())
        }
    }
    return outStack.pop();
}
```

###  旋转数组的最小数字

#### 题目描述

 把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。
输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。
例如数组{3,4,5,1,2}为{1,2,3,4,5}的一个旋转，该数组的最小值为1。
NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。 

```javascript
//暴力解法 直接找最小值
function minNumberInRotateArray(rotateArray) {
    const length = rotateArray.length;
    if (!length) {
        return 0;
    }
    return Math.min.call(Math,...rotateArray);
}
// 二分查找法 
//举几个例子来推导解题细节（请记住题干的数组有序、某个点旋转这两个条件）：
// arr[left] < arr[right]: 直接返回arr[left]。例如：1 2 3 4 5
// arr[left] < arr[mid]: 说明从数组下标范围为[left, right]的元素是递增的，此时最小值只可能出现在[mid + 1, length)范围内。例如:4 5 1 2 3
// arr[mid] < arr[right]: 说明从数组下标范围为[mid, right]的元素是递增的，此时最小值只可能出现在[left, mid] 范围内。注意，这里不能跳过下标mid。例如：3 3 3 4 5
// 其他情况，此时arr[mid] = arr[right] = arr[left]: 移动 left，缩小范围即可。例如：1 1 1 0 
function minNumberInRotateArray(rotateArray) {
    const length = rotateArray.length;
    if (!length) {
        return 0
    }
    let left = 0;
    let right = length - 1;
    while (left < right) {
        let mid = Math.floor((left + right) / 2);
        if (rotateArray[left] < rotateArray[right]) {
            return rotateArray[left];
        }
        if (rotateArray[left] < rotateArray[mid]) {
            left = mid + 1;
        } else if (rotateArray[mid] < rotateArray[right]) {
            right = mid;
        } else {
            left++;
        }
    }

}
```

### 斐波那契数列

```javascript
// 递归就不说了 时间太长了 无法通过
// 采用循环的方式
function Fibonacci(n) {
    let r = 0;
    let sum = 1;
    for (let i = 0; i < n; i++) {
        sum += r;
        r = sum - r;
    }
    return r;
}
```



### 二进制问题

#### 题目描述

 输入一个整数，输出该数二进制表示中1的个数。其中负数用补码表示。 
``` javascript
//  核心代码  n&n-1  一个数 
//  分析一下代码： 这段小小的代码，很是巧妙。
//如果一个整数不为0，那么这个整数至少有一位是1。如果我们把这个整数减1，那么原来处在整数最右边的1就会变为0，原来在1后面的所有的0都会变成1(如果最右边的1后面还有0的话)。其余所有位将不会受到影响。
//举个例子：一个二进制数1100，从右边数起第三位是处于最右边的一个1。减去1后，第三位变成0，它后面的两位0变成了1，而前面的1保持不变，因此得到的结果是1011.我们发现减1的结果是把最右边的一个1开始的所有位都取反了。这个时候如果我们再把原来的整数和减去1之后的结果做与运算，从原来整数最右边一个1那一位开始所有位都会变成0。如1100&1011=1000.也就是说，把一个整数减去1，再和原整数做与运算，会把该整数最右边一个1变成0.那么一个整数的二进制有多少个1，就可以进行多少次这样的操作。
function NumberOf1(n)
{    
    let count =0;
    while(n){
        n=n&(n-1);
        count++;
    }
    return count;
}
```

### 数组奇数前移问题

#### 题目描述

 输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。 

```javascript
function reOrderArray(array)
{
   let l=0,r=0;
   let newarr=[];
   for(let i=0;i<array.length;i++){
       if(array[i]%2!==0){
           r++
       }
   }
   for(let i=0;i<array.length;i++){
       if(array[i]%2===0){
        newarr[r++]=array[i]
       }
       else{
           newarr[l++]=array[i]
       }
   }
   return newarr;
}
```

### 输出链表倒数第K个节点

#### 题目描述

 输入一个链表，输出该链表中倒数第k个结点。 

```javascript
//思路简单 双指针法 用两个指针来跑，两个指针中间相距k-1个节点,第一个指针先跑，跑到了第k个节点时，第二个指针则是第一个节点。
//这时候两个一起跑。当第一个跑到了最后一个节点时，这时候第一个指针则是倒数第k个节点。
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function FindKthToTail(head, k) {
    if (head === null || k <= 0) {
        return null;
    }
    let pNode1 = head;
    let pNode2 = head;
    while (--k) {
        if (pNode2.next !== null) {
            pNode2 = pNode2.next;
        } else {
            return null;
        }
    }
    while (pNode2.next !== null) {
        pNode2 = pNode2.next;
        pNode1 = pNode1.next;
    }
    return pNode1;
}
```

### 反转链表

#### 题目描述

 输入一个链表，反转链表后，输出链表的所有元素。 

```javascript
//原地反转法
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function ReverseList(pHead) {
    // write code here
    let ppre = null;
    let pnext = null;
    while (pHead !== null) {
        pnext = pHead.next;
        pHead.next = ppre;
        ppre = pHead;
        pHead = pnext;
    }
    return ppre;
}
```

![见图](https://uploadfiles.nowcoder.com/images/20190905/1922887_1567665291938_48FCB8FBA07B019F0D00D01B6282CEC6)

### 合并两个递增链表

#### 题目描述

 输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则 

```javascript
//设置一个“哨兵节点”叫 preHead，这会让代码写起来非常“清爽”。整体流程如下：
//如果 pHead1 和 pHead2，均没遍历完：
//如果 pHead1.val <= pHead2.val，那么当前 node 的 next 指向 pHead1。并且移动 pHead1 指针。
//否则，当前 node 的 next 指向 pHead2，移动 pHead2 指针。
//移动 node 指针
//继续循环
//否则，结束循环：
//如果 pHead1 未遍历完，node 的 next 指向 pHead1
//如果 pHead2 未遍历玩，node 的 next 指向 pHead2
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function Merge(pHead1, pHead2) {
    if (pHead1 === null) return pHead2;
    if (pHead2 === null) return pHead1;
    let preHead = new ListNode(-1);
    let node = preHead;
    while (pHead2 && pHead1) {
        if (pHead1.val < pHead2.val) {
            node.next = pHead1;
            pHead1 = pHead1.next;
        } else {
            node.next = pHead2;
            pHead2 = pHead2.next;
        }
        node = node.next;
    }
    if (pHead1) {
        node.next = pHead1;
    } else if (pHead2) {
        node.next = pHead2;
    }

    return preHead.next;
} 
看了下题解   发现别人用递归实现的很厉害 代码量更少
// 重点抓住这两个链表都是单调递增的，因此我们只需要不断地比较他们的头结点就行，明显这是个重复的过程。
/* function ListNode(x){
 this.val = x;
 this.next = null;
 }*/
function Merge(pHead1, pHead2) {
  let pMergeHead = null;
  // write code here
  if (pHead1 === null) return pHead2;
  if (pHead2 === null) return pHead1;
  if (pHead1.val < pHead2.val) {
    pMergeHead = pHead1;
    pMergeHead.next = Merge(pHead1.next, pHead2);
  } else {
    pMergeHead = pHead2;
    pMergeHead.next = Merge(pHead1, pHead2.next);
  }
  return pMergeHead;
}
// 解法三 借助一个额外指针
var mergeTwoLists = function(l1, l2) {
    let head = new ListNode(0);
    let cur = head;
    while (l1 && l2) {
        if (l1.val <= l2.val) {
            cur.next = l1;
            l1 = l1.next;
        } else {
            cur.next = l2;
            l2 = l2.next;
        }
        cur = cur.next
    }
    cur.next = l1 ? l1 : l2;
    return head.next;
};

```

 ![](https://images2017.cnblogs.com/blog/1130568/201710/1130568-20171023110623504-438636512.jpg)

### 包含main函数的栈

#### 题目描述

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

注意：保证测试中不会当栈为空的时候，对栈调用pop()或者min()或者top()方法。

```javascript
借用辅助栈
// 剑指offer里面推荐的思路就是增加了一个辅助栈，每次压入数据栈时，把当前栈里面最小的值压入辅助栈当中。这样辅助栈的栈顶数据一直是数据栈中最小的值。
//比如，data中依次入栈,  5, 4, 3, 8, 10, 11, 12, 1
 //则min依次入栈，   5, 4, 3, 3,  3,  3,  3, 1

var stack = [];
var minStack = [];
var temp = null;

function push(node) {
    // write code here
    if (temp !== null) {
        if (node < temp) {
            temp = node;
        }
        stack.push(node);
        minStack.push(temp);
    } else {
        temp = node;
        minStack.push(temp);
        stack.push(node)
    }
}

function pop() {
    // write code here
    stack.pop();
    minStack.pop();

}

function top() {
    // write code here
    return stack[stack.length-1]
}

function min() {
    // write code here
    return minStack[minStack.length-1]
}
```

### 栈的压入顺序弹出顺序

#### 题目描述

 输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的） 

```javascript
【思路】借用一个辅助的栈，遍历压栈顺序，先讲第一个放入栈中，这里是1，然后判断栈顶元素是不是出栈顺序的第一个元素，这里是4，很显然1≠4，所以我们继续压栈，直到相等以后开始出栈，出栈一个元素，则将出栈顺序向后移动一位，直到不相等，这样循环等压栈顺序遍历完成，如果辅助栈还不为空，说明弹出序列不是该栈的弹出顺序。

举例：

入栈1,2,3,4,5

出栈4,5,3,2,1

首先1入辅助栈，此时栈顶1≠4，继续入栈2

此时栈顶2≠4，继续入栈3

此时栈顶3≠4，继续入栈4

此时栈顶4＝4，出栈4，弹出序列向后一位，此时为5，,辅助栈里面是1,2,3

此时栈顶3≠5，继续入栈5
此时栈顶5=5，出栈5,弹出序列向后一位，此时为3，,辅助栈里面是1,2,3
依次执行，最后辅助栈为空。如果不为空说明弹出序列不是该栈的弹出顺序
….
function IsPopOrder(pushV, popV)
{
    // write code here
    var stack = [];
    var index = 0;
    for(let i = 0;i<pushV.length;i++){
        stack.push(pushV[i]);
        while(stack.length&&popV[index]==stack[stack.length-1]){
            stack.pop();
            index++;
        }
    }
    return stack.length==0;
}

```



###  从上往下遍历二叉树

#### 题目描述

 从上往下打印出二叉树的每个节点，同层节点从左至右打印。 

```javascript
//从下打印就是按层次打印，其实也就是树的广度遍历。
//一般来说树的广度遍历用队列，利用先进先出的特点来保存之前节点，并操作之前的节点。
function PrintFromTopToBottom(root) {
    const queue = [],
        res = [];
    if (root === null) {
        return res;
    }
    queue.push(root);
    while (queue.length) {
        const pRoot = queue.shift();
        if (pRoot.left !== null) {
            queue.push(pRoot.left);
        }
        if (pRoot.right !== null) {
            queue.push(pRoot.right);
        }
        res.push(pRoot.val);
    }
    return res;
}
```

### 树的子结构

#### 题目描述

 输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构） 

```javascript
// Step1.在树A中找到和B的根结点的值一样的结点R；
// Step2.判断树A中以R为根结点的子树是不是包含和树B一样的结点。
function HasSubtree(pRoot1, pRoot2) {
    let res = false;
    //当Tree1或者Tree2都为零的时候，才进行比较。否则直接返回false
    if (pRoot1 === null || pRoot2 === null) return false;
    //如果找到了对应Tree2的根节点的点
    if (pRoot1.val === pRoot2.val)
    //以这个根节点为为起点判断是否包含Tree2
        res = doesTree1HasTree2(pRoot1, pRoot2);
    if (!res)
    //如果找不到，那么就再去root的左儿子当作起点，去判断时候包含Tree2
        res = HasSubtree(pRoot1.left, pRoot2);
    if (!res)
    //如果找不到，那么就再去root的右儿子当作起点，去判断时候包含Tree2
        res = HasSubtree(pRoot1.right, pRoot2);
    //返回结果
    return res;
}

function doesTree1HasTree2(pRoot1, pRoot2) {
    //如果Tree2已经遍历完了都能对应的上，返回true
    if (pRoot2 === null) return true;
    //如果Tree2还没有遍历完，Tree1却遍历完了。返回false
    if (pRoot1 === null) return false;
    //如果其中有一个点没有对应上，返回false
    if (pRoot1.val !== pRoot2.val) return false;
    //如果根节点对应的上，那么就分别去子节点里面匹配
    return doesTree1HasTree2(pRoot1.left, pRoot2.left) && doesTree1HasTree2(pRoot1.right, pRoot2.right);
}
```

###  数值的整次方 

#### 题目描述

给定一个 double 类型的浮点数 base 和 int 类型的整数 exponent。求 base 的 exponent 次方。保证 base 和 exponent 不同时为 0

① 傻瓜解法

```javascript
function Power(base, exponent) {
    return Math.pow(base, exponent);
}
```

② 暴力解法

```javascript
function Power(base, exponent) {
    if (exponent === 0) {
        return 1;
    }
    if (exponent === 1) {
        return base;
    }
    const isNegative = exponent < 0; // 是否是负指数
    const absExponent = Math.abs(exponent);
    let result = base;
    for (let i = 1; i < absExponent; ++i) {
        result = result * base;
    }
 
    return isNegative ? 1 / result : result;
}
```

③ 推荐解法

看大佬的解法tql

 为了理解，假设 base=3，exponent= 5。那么 5 的二进制是：101。所以，3 的 5 次方可以写成下图的格式： ![](https://uploadfiles.nowcoder.com/files/20200101/305674089_1577878980758_006tNbRwgy1gahan3575dj30o203ggq6.jpg)

可以看到，对 base 进行自乘，导致 base 的指数每次都扩大 2 倍。与 exponent 的二进制相对应。

以上图为例，整个算法的流程如下：

+  结果值 result 初始为 1 
+  base 初始为 3，此时 exponent 的二进制最右位为 1，更新结果为：base * result
+  exponent 右移一位。base 进行累乘，base 更新为 3 的 2 次方。由于 exponent 的二进制最右位为 0，不更新结果 
+  exponent 右移一位。base 进行累乘，base 更新为 3 的 4 次方。此时 exponent 的二进制最右位为 1，更新结果为：base * result 
+ over 

```javascript
function Power(base, exponent) {
    if (exponent === 0) {
        return 1;
    }
    if (exponent === 1) {
        return base;
    }

    const isNegative = exponent < 0; // 是否是负指数
    let absExponent = Math.abs(exponent);
    let result = 1;
    while (absExponent) {
        // 如果exponent最右位是1，将当前base累乘到result
        if (absExponent & 1) {
            result = result * base;
        }

        base = base * base; // base自乘法
        absExponent = Math.floor(absExponent / 2); // exponent右移1位
    }

    return isNegative ? 1 / result : result;
}
```

### 二叉树的镜像

#### 题目描述

 操作给定的二叉树，将其变换为源二叉树的镜像。 就是镜子里面的倒像一样嘿嘿

```javascript
递归   交换
function Mirror(root) {
        // write code here
        if (root === null) return null;
        if (root.left == null && root.right == null) return null
        var trmp = root.right;
        root.right = root.left;
        root.left = temp;
        if (root.left)
            Mirror(root.left);
        if (root.right)
            Mirror(root.right);
    }
```

### 二叉树的后续遍历

####  题目描述

 输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则输出Yes,否则输出No。假设输入的数组的任意两个数字都互不相同。 `

```javascript
//1.后续遍历我们可以知道，最右边的是根节点r。
//2.通过根节点r我们可以判断左子树和右子树。
//3.判断左子树中的每个值是否小于r,右子树的每个值是否大于r.
//4.对左、右子树递归判断。
function VerifySquenceOfBST(sequence) {
    if (!sequence.length) return false;
    return judge(sequence, 0, sequence.length - 1)
}

function judge(a, l, r) {
    if (l >= r) return true;
    let i = r;
    while (a[i - 1] > a[r] && i > l) i--;
    for (let j = i - 1; j >= l; j--) {
        if (a[j] > a[r]) return false
    }
    return judge(a, l, i - 1) && judge(a, i, r - 1)
}
```

### 重建二叉树

#### 题目描述

 输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。 



```javascript
 假设有二叉树如下： 
     1     
   / \
  2   3
 / \
4   5
它的前序遍历的顺序是：1 2 4 5 3。中序遍历的顺序是：4 2 5 1 3
因为前序遍历的第一个元素就是当前二叉树的根节点。那么，这个值就可以将中序遍历分成 2 个部分。在以上面的例子，中序遍历就被分成了 4 2 5 和 3 两个部分。4 2 5就是左子树，3就是右子树。
最后，根据左右子树，继续递归即可。
code:
/**
 * @param {TreeNode} pre
 * @param {TreeNode} vin
 * @return {TreeNode}
 */
function reConstructBinaryTree(pre, vin) {
    if (!pre.length || !vin.length) {
        return null;
    }
    const rootVal = pre[0];
    const node = new TreeNode(rootVal);
 
    let i = 0; // i有两个含义，一个是根节点在中序遍历结果中的下标，另一个是当前左子树的节点个数
    for (; i < vin.length; ++i) {
        if (vin[i] === rootVal) {
            break;
        }
    }
 
    node.left = reConstructBinaryTree(pre.slice(1, i + 1), vin.slice(0, i));
    node.right = reConstructBinaryTree(pre.slice(i + 1), vin.slice(i + 1));
    return node;
}
```

### 二叉树的中和为某一值的路径

#### 题目描述

 输入一颗二叉树和一个整数，打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径 

```javascript
function FindPath(root, expectNumber) {
    let list = [];
    let listAll = [];
    return findpath(root, expectNumber, list, listAll);
}

function findpath(root, expectNumber, list, listAll) {
    if (root === null) { return listAll }
    list.push(root.val);
    const x = expectNumber - root.val
    if (root.left == null && root.right == null && x === 0) {
        listAll.push(Array.of(...list));
    }
    findpath(root.left, x, list, listAll)
    findpath(root.right, x, list, listAll)
    list.pop()
    return listAll
}
```

### 数组中出现次数超过一半的数字

#### 题目描述

 数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。 

```javascript
//把数组转换为字符串然后使用一个对象把各个数字出现的次数存起来 在遍历整个对象就可以找出某个数字的最大出现次数 
function MoreThanHalfNum_Solution(numbers) {
    var str = numbers.join('');
    var obj = {};
    for (var i = 0; i < str.length; i++) {
        var char = str.charAt(i);
        if (obj[char]) {
            obj[char]++
        } else {
            obj[char] = 1
        }
    }
    let max = 0;
    var k = '';
    for (var key in obj) {
        // console.log(key);
        if (obj[key] > max) {
            max = obj[key]
            k = key;
        }
    }
    return (max > str.length / 2) ? k - 0 : 0
}
```

### 最小的K个数

#### 题目描述

 输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。 

```javascript
//  我使用了最简单的方法 通过 哈哈  看了题解 红黑树 堆栈 太难了 但是我的复杂度有点高 其实还可以通过冒泡排序巧妙利用每次把最小的数放到前面直到K就不排了 返回  今天太晚了 下次贴上代码
function GetLeastNumbers_Solution(input, k) {
    // write code here
    if (input.length == 0 || k == 0 || input.length < k) {
        return [];
    }
    input.sort((a, b) => {
        return a - b
    })
    return input.slice(0, k)
}
```

### 连续子数组的最大和

#### 题目描述

 HZ偶尔会拿些专业问题来忽悠那些非计算机专业的同学。今天测试组开完会后,他又发话了:在古老的一维模式识别中,常常需要计算连续子向量的最大和,当向量全为正数的时候,问题很好解决。但是,如果向量中包含负数,是否应该包含某个负数,并期望旁边的正数会弥补它呢？例如:{6,-3,-2,7,-15,1,2,2},连续子向量的最大和为8(从第0个开始,到第3个为止)。给一个数组，返回它的最大连续子序列的和，你会不会被他忽悠住？(子向量的长度至少是1) 

```javascript
function FindGreatestSumOfSubArray(array) {
    if (array.length < 0)
        return 0;
    var sum = array[0],
        tempsum = array[0];
    for (var i = 1; i < array.length; i++) {
        tempsum = tempsum < 0 ? array[i] : tempsum + array[i];
        sum = tempsum > sum ? tempsum : sum;
    }
    return sum;
}

```

### 丑数

#### 题目描述

 把只包含质因子2、3和5的数称作丑数（Ugly Number）。例如6、8都是丑数，但14不是，因为它包含质因子7。 习惯上我们把1当做是第一个丑数。求按从小到大的顺序的第N个丑数。 

```javascript
丑数能够分解成2^x3^y5^z,
所以只需要把得到的丑数不断地乘以2、3、5之后并放入他们应该放置的位置即可，
而此题的难点就在于如何有序的放在合适的位置。
1乘以 （2、3、5）=2、3、5；2乘以（2、3、5）=4、6、10；3乘以（2、3、5）=6,9,15；5乘以（2、3、5）=10、15、25；
从这里我们可以看到如果不加策略地添加丑数是会有重复并且无序，
而在2x，3y，5z中，如果x=y=z那么最小丑数一定是乘以2的，但关键是有可能存在x》y》z的情况，所以我们要维持三个指针来记录当前乘以2、乘以3、乘以5的最小值，然后当其被选为新的最小值后，要把相应的指针+1；因为这个指针会逐渐遍历整个数组，因此最终数组中的每一个值都会被乘以2、乘以3、乘以5，也就是实现了我们最开始的想法，只不过不是同时成乘以2、3、5，而是在需要的时候乘以2、3、5.
function GetUglyNumberSolution(index) {
    if (index < 7) return index;
    const res = [];
    res[0] = 1;
    let t2 = 0,
        t3 = 0,
        t5 = 0;
    for (let i = 1; i < index; i++) {
        res[i] = Math.min(res[t2] * 2, res[t3] * 3, res[t5] * 5);
        if (res[i] === res[t2] * 2) { t2++ };
        if (res[i] === res[t3] * 3) { t3++ };
        if (res[i] === res[t5] * 5) { t5++ };
    }
    return res[index - 1];
}
//  这题太有难度了吧 看题解基本都是这个解法 233
```

### 第一个只出现一次的字符

#### 题目描述

 在一个字符串(0<=字符串长度<=10000，全部由字母组成)中找到第一个只出现一次的字符,并返回它的位置, 如果没有则返回 -1（需要区分大小写）. 

```javascript
// 记住和字符串遍历有关的都可以转换为一个对象 让对象来记录各个字符出现的次数
function FirstNotRepeatingChar(str) {
    // write code here
    if (str.length < 1 || str.length > 10000)
        return -1;
    const map = {};
    for (let i = 0; i < str.length; i++) {
        if (!map[str[i]]) {
            map[str[i]] = 1
        } else {
            map[str[i]]++
        }
    }
    for (let i = 0; i < str.length; i++) {
        if (map[str[i]] === 1) {
            return i
        }
    }
    return -1;
}
```

### 两个链表第一个公共的节点

#### 题目描述

 输入两个链表，找出它们的第一个公共结点。（注意因为传入数据是链表，所以错误测试数据的提示是用其他方式显示的，保证传入数据是正确的） 

```javascript
看下面的链表例子：
0-1-2-3-4-5-null
a-b-4-5-null
代码的ifelse语句，对于某个指针p1来说，其实就是让它跑了连接好的的链表，长度就变成一样了。
如果有公共结点，那么指针一起走到末尾的部分，也就一定会重叠。看看下面指针的路径吧。
p1： 0-1-2-3-4-5-null(此时遇到ifelse)-a-b-4-5-null
p2: a-b-4-5-null(此时遇到ifelse)0-1-2-3-4-5-null
因此，两个指针所要遍历的链表就长度一样了！
如果两个链表存在公共结点，那么p1就是该结点，如果不存在那么p1将会是nul
function FindFirstCommonNode(pHead1, pHead2) {
    // write code here
    if (pHead1 == null || pHead2 == null) return null;
    let p1 = pHead1,
        p2 = pHead2;
    while (p1 != p2) {
        p1 = p1.next;
        p2 = p2.next;
        if (p1 != p2) {
            if (p1 == null) p1 = pHead2;
            if (p2 == null) p2 = pHead1
        }
    }
    return p1;
}
下面的这个是大佬写的 更清晰明了   只不过js版本的运行超时了 java版本的就可以  反正这题最重要的就是找到两个链表的相同的其实位置
function FindFirstCommonNode(pHead1, pHead2) {
    // write code here
    if (pHead1 == null || pHead2 == null) return null;
    let p1 = pHead1,
        p2 = pHead2;
    while (p1 != p2) {
        p1 = p1 == null ? pHead2 : p1.next;
        p2 = p2 == null ? pHead2 : p2.next
    }
    return p1;
}
```

### 查找一个排序数组中一个数出现的次数

#### 题目描述

 统计一个数字在排序数组中出现的次数。 

``` javascript
乍一看这样太简单了 233 只是自己用了最暴力的方法
function GetNumberOfK(data, k) {
     write code here
     if (data.length < 1 || k < 1) return 0;
     let count = 0;
     for (let i = 0; i < data.length; i++) {
         if (data[i] === k) {
            count++;
         }
     }
     return count;
}
这个方法很巧妙 
return data.join('').split(k).length - 1;
 下面的大佬的二分查找法
 function GetNumberOfK(data, k) {
  if (getEnd(data, k) === -1 && getBegin(data, k) === -1) return 0;
  return getEnd(data, k) - getBegin(data, k) + 1;
}
function getBegin(data, k) {
  let [left, right] = [0, data.length - 1];
  let mid = left + right >> 1;
  while (left <= right) {
    if (data[mid] > k) {
      right = mid - 1;
    } else if (data[mid] < k) {
      left = mid + 1;
    } else if (mid - 1 >= 0 && data[mid - 1] === k) {
      right = mid - 1;
    } else return mid;
    mid = left + right >> 1;
  }
  return -1;
}
function getEnd(data, k) {
  let [left, right] = [0, data.length - 1];
  let mid = left + right >> 1;
  while (left <= right) {
    if (data[mid] > k) {
      right = mid - 1;
    } else if (data[mid] < k) {
      left = mid + 1;
    } else if (mid + 1 < data.length && data[mid + 1] === k) {
      left = mid + 1;
    } else return mid;
    mid = left + right >> 1;
  }
  return -1;
}
头看晕了
```

### 二叉树的深度

#### 题目描述

 输入一棵二叉树，求该树的深度。从根结点到叶结点依次经过的结点（含根、叶结点）形成树的一条路径，最长路径的长度为树的深度。 

```javascript
var maxDepth = function(root) {
        if (!root) return 0;
        return Math.max(maxDepth(root.left), maxDepth(root.right)) + 1
    }
    // 对于该递归函数可以这样理解：一旦没有找到节点就会返回 0，
    //每弹出一次递归函数就会加一，树有三层就会得到3
```

### 平衡二叉树

#### 题目描述

判断一棵树是否是平衡二叉树

```javascript
首先得知道什么的平衡二叉树 
平衡二叉树定义：它是一棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。
思路：根据定义，我们只需要后序遍历此树，从树的叶子节点开始计算高度，只要有一个子树不满足定义就返回-1，如果满足继续向上计算高度。
function IsBalanced_Solution(pRoot) {
  if (pRoot == null) return true;
  let leftLen = TreeDepth(pRoot.left);
  let rightLen = TreeDepth(pRoot.right);
  return Math.abs(rightLen - leftLen) <= 1 && IsBalanced_Solution(pRoot.left) && IsBalanced_Solution(pRoot.right);
}
function TreeDepth(pRoot) {
  if (pRoot == null) return 0;
  let leftLen = TreeDepth(pRoot.left);
  let rightLen = TreeDepth(pRoot.right);
  return Math.max(leftLen, rightLen) + 1;
}
这个解法有重复节点遍历 了，影响效率
第二种方法参考大佬的解法 代码很优美
改进办法就是在求高度的同时判断是否平衡，如果不平衡就返回-1，否则返回树的高度。
并且当左子树高度为-1时，就没必要去求右子树的高度了，可以直接一路返回到最上层了
function treeDep(root) {
    if (!root) return 0;
    let left = treeDep(root.left);
    if (left === -1) return -1;
    let right = treeDep(root.right);
    if (right === -1) return -1;
    return Math.abs(left - right) > 1 ? -1 : Math.max(left, right) + 1
}

function IsBalanced_Solution(pRoot) {
    return treeDep(pRoot) !== -1
}
```

### 数组中只出现一次的数组

#### 题目描述

 一个整型数组里除了两个数字之外，其他的数字都出现了两次。请写程序找出这两个只出现一次的数字。 

```javascript
 第一种  简单
function FindNumsAppearOnce(array) {
  const res = [];
  for (let i = 0; i < array.length; i++) {
    if (array.indexOf(array[i]) === array.lastIndexOf(array[i])) {
      res.push(array[i]);
    }
  }
  return res;
}

// 第二种 也挺简单
function FindNumsAppearOnce2(array) {
  const map = {},
    res = [];
  for (let i = 0; i < array.length; i++) {
    if (!map[array[i]]) {
      map[array[i]] = 1;
    } else {
      map[array[i]]++;
    }
  }
  for (let i = 0; i < array.length; i++) {
    if (map[array[i]] === 1) {
      res.push(array[i]);
    }
  }
  return res;
}
```

###  和为S的正数序列

#### 题目描述

 小明很喜欢数学,有一天他在做数学作业时,要求计算出9~16的和,他马上就写出了正确答案是100。但是他并不满足于此,他在想究竟有多少种连续的正数序列的和为100(至少包括两个数)。没多久,他就得到另一组连续正数和为100的序列:18,19,20,21,22。现在把问题交给你,你能不能也很快的找出所有和为S的连续正数序列? Good Luck! 

#### 输出描述

输出所有和为S的连续正数序列。序列内按照从小至大的顺序，序列间按照开始数字从小到大的顺序

```javascript
我想用暴力方法 但是无奈没写出来
思路：
因为要求连续的数列和，所以这是一个等差数列，并且我们想到用双指针来做，slow，high。
1.等差数列：current（当前值）=(high-slow+1)(high+slow)/2
2.初始化slow=1和high=2.(因为考虑要覆盖到所有情况，所以赋值为两个较小的数)
3.只要满足slow<high,循环就可进行。
4.不断地比较current和slow
4.1.current==slow,即slow和high之间的数满足序列要求，所以遍历slow和high之间的所有数，存入一个数组。*之后slow++**（因为要求的所有的连续正数序列，所以要不断的右移）
4.2.current<slow,则表明当前值小于sum，需要high++，
4.3.current>slow,则表明当前值大于sum，需要减小当前值，即slow--；
function FindContinuousSequence(sum)
{
    // write code here
    var result = [];
    var slow = 1;var high = 2;
    while(slow<high){
        current = (high-slow+1)*(high+slow)/2;
        if(current==sum){
            var list = [];
            for(let i =slow;i<=high;i++){
                list.push(i);
            }
            result.push(list);
            slow++;
        }else if(current<sum){
            high++;
        }else{
            slow++
        }
    }
    return result;
}
```

### 和为s的两个数

#### 题目描述

 输入一个递增排序的数组和一个数字S，在数组中查找两个数，使得他们的和正好是S，如果有多对数字的和等于S，输出两个数的乘积最小的。 

```javascript
双指针  其次是两个数字相隔越远  积越小
function FindNumbersWithSum(array, sum) {
    if (array.length < 2) return [];
    let left = 0,
        right = array.length - 1;
    const res = [];
    while (left < right) {
        if (array[left] + array[right] < sum) {
            left++;
        } else if (array[left] + array[right] > sum) {
            right--;
        } else {
            res.push(array[left], array[right]);
            break;
        }
    }
    return res;
}
```

### 左旋转字符串

#### 题目描述

 汇编语言中有一种移位指令叫做循环左移（ROL），现在有个简单的任务，就是用字符串模拟这个指令的运算结果。对于一个给定的字符序列S，请你把其循环左移K位后的序列输出。例如，字符序列S=”abcXYZdef”,要求输出循环左移3位后的结果，即“XYZdefabc”。是不是很简单？OK，搞定它！ 

```javascript
hhhhh  终于遇到简单的题目了  还有个反转字符串也简单 一行代码搞定 这里就不写了
字符串截取  slice  substring 
function LeftRotateString(str, n)
{
    // write code here
 if (str === null || str.length === 0) return '';
  return str.slice(n,str.length) + str.slice(0, n);
}
```

### 1+2+3+4+...

#### 题目描述

 求1+2+3+...+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C） 

```javascript
function Sum_Solution(n)
{
    // write code here
    return ( Math.pow(n,2)+n)/2
}
hhh 简单 公式法 递归法都可以

function Sum_Solution(n)
{
    // write code here
    return n&& Sum_Solution(n-1)+n
}
```

### 字符串转换为整数

#### 题目描述

 将一个字符串转换成一个整数，要求不能使用字符串转换整数的库函数。 数值为0或者字符串不是一个合法的数值则返回0 

输入描述 ：输入一个字符串,包括数字字母符号,可以为空

输出描述：如果是合法的数值表达则返回该数字，否则返回0

```javascript
不太会 看了题解 这神奇操作牛
function StrToInt(str) {
  let res = 0,
    flag = 1;
    res=res,split('')
  const n = str.length;
  if (!n) return 0;
  if (str[0] === '-') {
    flag = -1;
  }
  for (let i = str[0] === '+' || str[0] === '-' ? 1 : 0; i < n; i++) {
    if (!(str[i] >= '0' && str[i] <= '9')) return 0;
    res = (res << 1) + (res << 3) + (str[i] - '0');    这个题最迷幻的就是这里了 其实这个等价与     res=res*10+ (str[i] - '0')  这样看就明白多了
  }
  return res * flag;
}
```

### 构建乘积数组

#### 题目描述

 给定一个数组A[0,1,...,n-1],请构建一个数组B[0,1,...,n-1],其中B中的元素B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]。不能使用除法。（注意：规定B[0] = A[1] * A[2] * ... * A[n-1]，B[n-1] = A[0] * A[1] * ... * A[n-2];） 

```javascript
一开始没有看清楚题意 耽误了好久  借助一个数组 B 本来还可以用空间来换取时间复杂度 下面这个改进一点
function multiply(array) {
  const B = [],
    len = array.length;
  B[0] = 1;
  // 计算前i - 1个元素的乘积
  for (let i = 1; i < len; i++) {
    B[i] = array[i - 1] * B[i - 1];
  }
  let tmp = 1;
  // 计算后N - i个元素的乘积并连接
  for (let i = len - 2; i >= 0; i--) {
    tmp *= array[i + 1];
    B[i] *= tmp;
  }
  return B;
}
```

### 表示数值的字符串

#### 题目描述

 请实现一个函数用来判断字符串是否表示数值（包括整数和小数）。例如，字符串"+100","5e2","-123","3.1416"和"-1E-16"都表示数值。 但是"12e","1a3.14","1.2.3","+-5"和"12e+4.3"都不是。 

```javascript
function isNumeric(s)
{
    // write code here
    var reg = /^[\+-]?\d*\.?\d+(e[\+-]?\d+)?$/i;
    return reg.test(s);

} 
自己暴力的方法还是失败了 看了题解 这正则太厉害了 看来得好好学习一下正则了
```

### 链表的环入口节点

#### 题目描述

 给一个链表，若其中包含环，请找出该链表的环的入口结点，否则，输出null。 

```javascript
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
// 、对于问题链表环入口，使用追赶的方法，设定两个指针slow、fast，从头节点开始，
//每次分别前进1步、2步。如存在环，则两者相遇；如不存在环，fast遇到NULL退出。
function EntryNodeOfLoop(pHead) {
    // write code here
    let slow = pHead;
    let fast = pHead
    while (fast !== null && fast.next !== null) {
        slow = slow.next;
        fast = fast.next.next;
        if (fast === slow) {
            //相遇
            let p = pHead;
            while (p !== slow) {
                p = p.next;
                slow = slow.next;
            }
            return p;
        }
    }
    return null;

}
```

### 删除链表的重复节点值

#### 题目描述

 在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。 例如，链表1->2->3->3->4->4->5 处理后为 1->2->5 

```javascript
其实这道题目本身不难  一开始就想到用指针遍历找到相同节点然后用第一个节点连接到下个相同节点的后面这样相当于跳过了中间相同的节点 但是考虑周全 
导致最后也没写出来
下面是参考牛客的  思路差不多
1.因为链表是单向的，如果是第一个、第二个节点就重复的话，删除就比较麻烦。因此我们可以额外添加头节点来解决
2.因为重复的节点不一定是重复两个，可能重复很多个，需要循环处理下。
/*function ListNode(x){
    this.val = x;
    this.next = null;
}*/
function deleteDuplication(pHead)
{ 
    if (pHead === null || pHead.next === null) {
    return pHead;
  }
    // write code here
    const Head = new ListNode(0); // 重要，方便处理第一个、第二个节点就是相同的情况。
  Head.next = pHead;
  let pre = Head;
  let cur = Head.next;
  while (cur !== null) {
    if (cur.next !== null && cur.val === cur.next.val) {
      // 找到最后的一个相同节点,因为相同节点可能重复多个
      while (cur.next !== null && cur.val === cur.next.val) {
        cur = cur.next;
      }
      pre.next = cur.next;
      cur = cur.next;
    } else {
      pre = pre.next;
      cur = cur.next;
    }
  }
    return Head.next;
}
```

### 二叉树的下一个节点

#### 题目描述

给定一个二叉树和其中的一个结点，请找出中序遍历顺序的下一个结点并且返回。注意，树中的结点不仅包含左右子结点，同时包含指向父结点

```javascript
这个题目分析过程有点耗费时间 中序遍历 左根右  需要分两种情况 此节点的下一个节点是否有右子树 然后根据这两种情况来分析 
需要注意的是 =>树中的结点不仅包含左右子结点，同时包含指向父结点的指针。
// 有右子树，下一结点是右子树中的最左结点，例如 B，下一结点是 H
// 无右子树，且结点是该结点父结点的左子树，则下一结点是该结点的父结点
// 无右子树，且结点是该结点父结点的右子树，则我们一直沿着父结点追朔，直到找到某个结点是其父结点的左子树，如果存在这样的结点，那么这个结点的父结点就是我们要找的下一结点。
/*function TreeLinkNode(x){
    this.val = x;
    this.left = null;
    this.right = null;
    this.next = null;
}*/
function GetNext(pNode) {
    // write code here
    if (pNode == null) {
        return null
    } //第一种情况
    if (pNode.right !== null) {
        pNode = pNode.right;
        while (pNode.left !== null) {
            pNode = pNode.left
        }
        return pNode
    }
    while (pNode.next !== null) {
        // 第2种
        if (pNode === pNode.next.left) {
            return pNode.next;
        }
        pNode = pNode.next;
    }
    return null;
}
```

### 二叉树的镜像

#### 题目描述

 请实现一个函数，用来判断一颗二叉树是不是对称的。注意，如果一个二叉树同此二叉树的镜像是同样的，定义其为对称的。 

```javascript
 理解题意 理解题意 理解题意 画图 画图 画图 ！！！
如果我们拥有一颗对称二叉树，他只需要满足，每个节点的左子树和右子树都是镜像。
所以解题思路分四步：
我们检测根节点是不是为null，如果是，则他肯定是对称的，直接返回true。
我们新建一个method check，用来检测当前的左子树和右子树是不是镜像。我们从根节点往下一路检测。
举个例子，首先我们检测根节点的左孩子和右孩子，如果两个都是null，说明他是镜像。但是如果有一个不为null或者他们的值不相等，则此时我们就可以判断已经是不对称的了。如果此时还是对称的而且左孩子和右孩子都分别还有各自的孩子，我们就继续检测。这时，我们需要判断，左孩子的左子树和右孩子的右子树是否镜像，及左孩子的右子树和右孩子的左子树是否镜像。
如此进入下一次循环，直到我们接触到叶节点还是镜像return true或者我们任意时刻发现不是镜像return false 为止。
function isSymmetrical(pRoot) {
    if (pRoot == null) return true;
    return check(pRoot.left, pRoot.right)
}

function check(left, right) {
    if (left == null && right == null)  { 
        return true ;
    } 
    else if ((left == null && right !== null) || (left !== null && right == null) || (left.val !== right.val)) {
        return false;
    }
    return check(left.left, right.right) && check(left.right, right.left)
}
```

### leetcode 841

有 N 个房间，开始时你位于 0 号房间。每个房间有不同的号码：0，1，2，...，N-1，并且房间里可能有一些钥匙能使你进入下一个房间。在形式上，对于每个房间 i 都有一个钥匙列表 rooms[i]，每个钥匙 rooms[i][j] 由 [0,1，...，N-1] 中的一个整数表示，其中 N = rooms.length。 钥匙 rooms[i][j] = v 可以打开编号为 v 的房间。最初，除 0 号房间外的其余所有房间都被锁住。你可以自由地在房间之间来回走动。如果能进入每个房间返回 true，否则返回 false。

示例 1：输入: [[1],[2],[3],[]]
输出: true
解释:  
我们从 0 号房间开始，拿到钥匙 1。
之后我们去 1 号房间，拿到钥匙 2。
然后我们去 2 号房间，拿到钥匙 3。
最后我们去了 3 号房间。
由于我们能够进入每个房间，我们返回 true。
示例 2：

输入：[[1,3],[3,0,1],[2],[0]]
输出：false
解释：我们不能进入 2 号房间。

来源：力扣（LeetCode）
链接：https://leetcode-cn.com/problems/keys-and-rooms
著作权归领扣网络所有。商业转载请联系官方授权，非商业转载请注明出处。

```javascript
/*
 * @lc app=leetcode.cn id=841 lang=javascript
 *
 * [841] 钥匙和房间
 */
// 解题思路:
//     只要以此用手里的钥匙打开对应的房门， 将房门内新的钥匙取出放入手里钥匙这个数组， 直到手里没有新钥匙循环结束.
// 最后判断钥匙数量和房间数量是否相等就可以得出结果. **
//     这里要注意房门内可能取得几条同样的钥匙， 需要将得到的数组去重.

// @lc code=start
/**
 * @param {number[][]} rooms
 * @return {boolean}
 */
var canVisitAllRooms = function(rooms) {
    let n = 0;
    let key = [0];
    while (key.length > n) {
        key = key.concat([...new Set(rooms[key[n]].filter((item) => !key.includes(item)))])
        n++
    }
    return key.length === rooms.length
};
// @lc code=end
```



