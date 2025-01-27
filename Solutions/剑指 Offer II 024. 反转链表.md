## [剑指 Offer II 024. 反转链表](https://leetcode-cn.com/problems/UHnkqh/)

- 标签：递归、链表
- 难度：简单

## 题目大意

给定一个单链表的头节点 `head`。

要求将其进行反转，并返回反转后的链表的头节点。

## 解题思路

### 1. 迭代

顺序遍历当前节点，将当前节点的前后指针进行交换。也就是将当前节点的 next 指针指向前一个节点，由于当前节点没有引用前一个节点，所以更改指向之前必须先把前一个节点保存下来。并且由于更改之后，当前节点的后一个节点失去了引用，所以更改指向前，还要将当前节点的后一个节点保存下来。

所以指针更替顺序为：

1. 保存前一个节点 prev；
2. 遍历到当前节点 curr；
3. 保存当前节点 curr 的后一个节点 next；
4. 当前节点的 next 指针指向前一个节点；
5. 前一个节点 prev 移动到当前节点（保存前一个节点）；
6. 当前节点继续向后遍历到 next 位置（遍历当前节点）。
7. 继续执行 3、4、5、6。

上述步骤执行到第 4 步时，当前节点 curr 和 next 就完成了反转，此时 next 指向了 curr，继续向下执行，就会不断的进行反转。最后返回新的头节点。

### 2. 递归

假设链表为 $n_1 → n_2 → … → n_{k-1} → n_k → n_{k+1} → … → n_{m-1} → n_m → ∅$ 。

从末尾开始反转，先反转 $n_{m-1} → n_m → ∅$ ，则反转顺序为：

1. $n_{n-1}$ 的  next 的 next （即 $n_m$）指向 $n_{m-1}$
2. 再将 $n_{m-1}$ 的 next 指向 $∅$。
3. 返回新的头节点 $n_m$。

这样就变成了 $∅ ← n_{m-1} ← n_m$，就完成了末尾的反转。

然后我们是从 head 位置开始进行递归遍历，逆序对链表末尾进行反转。

## 代码

1. 迭代

```Python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        prev = None
        curr = head
        while curr != None:
            next = curr.next
            curr.next = prev
            prev = curr
            curr = next
        return prev
```

2. 递归

```Python
class Solution:
    def reverseList(self, head: ListNode) -> ListNode:
        if head == None or head.next == None:
            return head

        newHead = self.reverseList(head.next)
        head.next.next = head
        head.next = None
        return newHead
```



