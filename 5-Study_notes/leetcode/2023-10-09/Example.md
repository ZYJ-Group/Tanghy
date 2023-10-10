# leetcode
## 单双链表及其反转-堆栈诠释
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/da60afd8-1179-4206-a254-4f104ad8db09)  



### 笔记  
**1. 按值传递、按引用传递**  
```java
	// int、long、byte、short
	// char、float、double、boolean
	// 还有String
	// 都是按值传递
	int a = 10;
	f(a);
	System.out.println(a);

	public static void f(int a) {
		a = 0;
	}
//在这个代码里面，f(a)在调用的过程中，实际上是创建了一个新的a',a'的值等于a，所以修改a'的值并不会改变a的值。
```

```java
// 其他类型按引用传递
// 比如下面的Number是自定义的类
	Number b = new Number(5);
	g1(b);
	System.out.println(b.val);
	g2(b);
	System.out.println(b.val);

	// 比如下面的一维数组
	int[] c = { 1, 2, 3, 4 };
	g3(c);
	System.out.println(c[0]);
	g4(c);
	System.out.println(c[0]);


	public static class Number {
		public int val;

		public Number(int v) {
			val = v;
		}
	}

	public static void g1(Number b) {
		b = null;
	}

	public static void g2(Number b) {
		b.val = 6;
	}

	public static void g3(int[] c) {
		c = null;
	}

	public static void g4(int[] c) {
		c[0] = 100;
	}
//在这个代码中，当g(b)调用b的时候，实际上也是创建了一个新的b'，但是b'和b指向同一个内存的值，所以当b'设置为null的时候，对b不会有影响，但是如果b'.val进行了修改，实际上是修改了同时指向的内存的值，所以b对应的值也会发生变化。
```
**2. 单链表、双链表的定义**  
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/c6700cbe-da93-498d-9524-ca01c879d2b4)  
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/45ce8140-9173-4190-8f27-d890cb1eb775)  
```c++
// 单链表
Node{
	int val;
	Node next;
}
```
```c++
// 双链表
Node{
	int val;
	Node next;
	Node last;
}
```
**3. 链表反转**  
```C++
//单链表反转
//https://leetcode.cn/problems/reverse-linked-list/solutions/
class Solution {
public:
    ListNode* reverseList(ListNode* head){
    ListNode* pre = nullptr;
    ListNode* cur = head;
    while(cur) {
        ListNode* next = cur->next;
        cur->next = pre;
        pre = cur;
        cur = next;
    }
    return pre;
    }
};
```
```C++
//双链表反转
class Solution {
public:
    ListNode* reverseDoubleList(ListNode* head){
    ListNode* pre = nullptr;
    ListNode* cur = head;
    while(cur) {
        ListNode* next = cur->next;
        cur->next = pre;
        cur->last = next;
        pre = cur;
        cur = next;
    }
    return pre;
    }
};
```
## 链表入门题目-合并两个有序链表  
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/f4c86c2b-587f-49a5-8017-37d54d3bd41c)  

**1. 合并两个有序链表**    
```C++
//https://leetcode.cn/problems/merge-two-sorted-lists/

```

