# leetcode
## 链表入门题目-两个链表相加
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/cbae74e1-4f93-461d-aaeb-7797f5702806)  


### 笔记
**1. 两个链表相加**  



## 链表入门题目-划分链表
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/72399e5b-29e7-4692-bb9b-ad2b142930ae)  

### 笔记
**1. 划分链表**  
```C++
class Solution {
public:
    ListNode* partition(ListNode* head, int x) {
        if(!head) {
            return head;
        }
        ListNode* small = new ListNode(0);
        ListNode* smallHead = small;
        ListNode* large = new ListNode(0);
        ListNode* largeHead = large;

        while (head != nullptr) {
            if (head->val < x) {
                small->next = head;
                small = small->next;
            } else {
                large->next = head;
                large = large->next;
            }
            head = head->next;
        }

        small->next = largeHead->next;
        large->next = nullptr;
        return smallHead->next;
    }
};
```

