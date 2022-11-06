![题目](https://upload-images.jianshu.io/upload_images/16630052-1a2bc613e4f42428.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

# 面试便当`python`
解1：一种面试过程比较不容易写头晕的写法
#### Python3
```Python
# Definition for singly-linked list.
# class ListNode:
#     def __init__(self, val=0, next=None):
#         self.val = val
#         self.next = next
class Solution:
    def addTwoNumbers(self, l1: Optional[ListNode], l2: Optional[ListNode]) -> Optional[ListNode]:
        holder = ListNode()
        cur = holder
        carry = 0
        while l1 or l2 or carry:
            l1v = l1.val if l1 else 0
            l2v = l2.val if l2 else 0
            val = (l1v + l2v + carry) % 10
            carry = (l1v + l2v + carry) // 10
            cur.next = ListNode(val)
            cur = cur.next
            l1 = l1.next if l1 else l1
            l2 = l2.next if l2 else l2
        return holder.next
```
> - 时间复杂度：O(n)
> - 空间复杂度：O(n)
---
# 其他语言版本`Java/Golang/C++`
#### Java
```java
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        ListNode holder = new ListNode();
        ListNode cur = holder;
        int carry = 0;
        while (l1 != null || l2 != null || carry > 0) {
            int l1v = l1 == null ? 0 : l1.val;
            int l2v = l2 == null ? 0 : l2.val;

            int val = (l1v + l2v + carry) % 10;
            carry = (l1v + l2v + carry) / 10;
            cur.next = new ListNode(val);
            cur = cur.next;

            l1 = l1 == null ? l1 : l1.next;
            l2 = l2 == null ? l2 : l2.next;
        }
        return holder.next;
    }
}
```
#### Golang
```go
/**
 * Definition for singly-linked list.
 * type ListNode struct {
 *     Val int
 *     Next *ListNode
 * }
 */
func addTwoNumbers(l1 *ListNode, l2 *ListNode) *ListNode {
	holder := &ListNode{}
	cur := holder
	carry := 0

	for l1 != nil || l2 != nil || carry > 0 {
		l1v := 0
		if l1 != nil {
			l1v = l1.Val
		}
		l2v := 0
		if l2 != nil {
			l2v = l2.Val
		}

		val := (carry + l1v + l2v) % 10
		carry = (carry + l1v + l2v) / 10
		cur.Next = &ListNode{Val: val}
		cur = cur.Next

		if l1 != nil {
			l1 = l1.Next
		}
		if l2 != nil {
			l2 = l2.Next
		}
	}
	return holder.Next
}
```
> go没有三元运算符，有点显长
#### C++
```cpp
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode() : val(0), next(nullptr) {}
 *     ListNode(int x) : val(x), next(nullptr) {}
 *     ListNode(int x, ListNode *next) : val(x), next(next) {}
 * };
 */
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        auto holder = new ListNode();
        auto cur = holder;
        int carry = 0;

        while (l1 != NULL || l2 != NULL || carry > 0) {
            auto l1v = l1 != NULL ? l1->val : 0;
            auto l2v = l2 != NULL ? l2->val : 0;

            auto value = (l1v + l2v + carry) % 10;
            carry = (l1v + l2v + carry) / 10;
            cur->next = new ListNode(value);
            cur = cur->next;

            l1 = l1 != NULL ? l1->next : l1;
            l2 = l2 != NULL ? l2->next : l2;
        }    

        return holder->next;
    }
};
```