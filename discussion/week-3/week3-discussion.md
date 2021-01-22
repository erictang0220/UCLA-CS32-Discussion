# Discussion Session Week 3
By Licheng Guo and Devyan Biswas

## Reverse A Linked List

Example 
<pre>
<b>Input</b>: 1->2->3->4->5->NULL
<b>Output</b>: 5->4->3->2->1->NULL
</pre>

### Solution 1: iteratively

An incorrect implementation. What is wrong?
```c++
class Solution {
public:
1     ListNode* reverseList(ListNode* head) {
2         ListNode *curr = head;
          if (head == nullptr) return nullptr;

3         while (curr->next) {
4             ListNode *next = curr->next;
              // while we are modifying node 2, we are losing access to node 3
5             curr->next->next = curr;
6             curr = next;
7         }
8         
9         return curr;
10    }
};
```

The correct implementation:
```c++
ListNode* reverseList(ListNode* head) {
  ListNode *prev = nullptr;
  ListNode *curr = head;

  while (curr) {
    ListNode *next = curr->next;
    curr->next = prev;
    prev = curr;
    curr = next;
  }

  return prev
}
```

### Solution 2: recursively

How can we use recursion to reverse a linked list?

```c++
ListNode* reverseList(ListNode* head) {
  if (head == nullptr) return nullptr;
  else if (head->next == nullptr) return head;
  else {
    ListNode *new_head_of_sub = reverseList(head->next)
    ListNode *new_tail_of_sub = head->next;

    assert(new_tail_of_sub->next == nullptr)
    new_tail_of_sub->next = head;
    
    head->next = nullptr;

    return new_head_of_sub;
  }
}
```

### Solution 3 Using a stack


```c++
ListNode* reverseList(ListNode* head) {
  if (head == nullptr) return nullptr;

  std::stack<ListNode*> s;
  ListNode *curr = head;
  while (curr) {
    s.push(curr);
    curr = curr->next;
  }

  // reconstruct the linked list in a reversed way
  ListNode *new_head = s.top(); s.pop();
  curr = new_head;

  while (!s.empty()) {
    curr->next = s.top();
    s.pop();
    curr = curr->next;
  }
  curr->next = nullptr;

  return prev;
}
```

## Merge K Sorted Lists (LeetCode 23, Not Discussed)

You are given an array of `k` linked-lists `lists`, each linked-list is sorted in ascending order.

Merge all the linked-lists into one sorted linked-list and return it.

Example 1
<pre>
<b>Input</b>: lists = [[1,4,5],[1,3,4],[2,6]]
<b>Output</b>: [1,1,2,3,4,4,5,6]
</pre>

Example 2
<pre>
<b>Input</b>: lists = []
<b>Output</b>: []
</pre>

Example 2
<pre>
<b>Input</b>: lists = [[]]
<b>Output</b>: []
</pre>

### Situation 1: K == 2

### Situation 2: any K