# leetcode
## 时间复杂度和空间复杂度
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/1ee46368-5159-4b77-8244-5f185aba2869)  
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/cd46f995-04bd-4679-acff-48b1841c247c)  
### 笔记  

**1. 常数操作**  
位运算，算术运算，寻址运算，哈希。  

**2. 时间复杂度**  
例：选择排序。  

遍历 | 次数 | 作用
--- | --- | ---
0 - N-1 | N | 把min放到[0]
1 - N-1 | N-1 | 把min放到[1]
2 - N-1 | N-2 | 把min放到[2]
3 - N-1 | N-3 | 把min放到[3]  

总和（等差数列）：[N + (N-1) + …… + 2 + 1 = n/2*(2*a1+(n-1)*d) = an^2 + bn + c ---- O(n^2)  
同理，冒泡排序，插入排序都是O(n^2)时间复杂度。  
但是，在严格固定流程的算法，一定强调最差情况！比如插入排序。 

**3. 空间复杂度**  
需要注意的是，动态数组的空间复杂度在进行动态扩展时可能存在摊销的情况。当数组需要扩展时，可能会分配新的内存空间，并将原来的元素复制到新的内存空间中。这个操作的时间复杂度是O(n)，但由于不是每次都需要扩展，而是摊销到多次插入操作中，因此平均情况下每次插入的空间复杂度仍然是O(1)。
什么叫最优解，先满足时间复杂度最优，然后尽量少用空间的解。  

**4. 判断时间复杂度**
- 不要用代码结构来判断时间复杂度。  
``` C++
// 例：
for(){
  for(){
    }
  }
// 并不表示这个的时间复杂度就为O(n^2)
```
```java
	// 只用一个循环完成冒泡排序
	// 但这是时间复杂度O(N^2)的！
	public static void bubbleSort(int[] arr) {
		if (arr == null || arr.length < 2) {
			return;
		}
		int n = arr.length;
		int end = n - 1, i = 0;
		while (end > 0) {
			if (arr[i] > arr[i + 1]) {
				swap(arr, i, i + 1);
			}
			if (i < end - 1) {
				i++;
			} else {
				end--;
				i = 0;
			}
		}
	}
```

```java
//N/1 + N/2 + N/3 + … + N/N，这个流程的时间复杂度是O(N * logN)，著名的调和级数
		for (int i = 1; i <= N; i++) {
			for (int j = i; j <= N; j += i) {
				// 这两个嵌套for循环的流程，时间复杂度为O(N * logN)
				// 1/1 + 1/2 + 1/3 + 1/4 + 1/5 + ... + 1/n，也叫"调和级数"，收敛于O(logN)
				// 所以如果一个流程的表达式 : n/1 + n/2 + n/3 + ... + n/n
				// 那么这个流程时间复杂度O(N * logN)
			}
		}
```

**5. 常见复杂度**  
O(1) O(logN) O(N) O(N*logN) O(N^2) … O(N^k) O(2^N) … O(k^N) … O(N!)  


## 二分搜索
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/05d0685e-5a61-4ace-a7b6-c095343f964c)


## 算法和数据结构简介  
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/5b6e1a1c-3de1-4d99-9da6-ba9dc7227a90)   
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/ba0f07f1-d7a5-484c-b3c4-dba826f11114)  


**1. 数据结构分类**    
宏观上说，只有连接结构和跳转结构。  
连接结构类似于数组，是在一个连续的空间内。  
跳跃结构类似于，链表，在一个内容中，第一位数据存储该字节的值，第二位数据存储下一个字节的地址。同样的类似于二叉树，可能第一位数据记录该字节的值，第二位和第三位数据分别记录其左孩子和右孩子的地址。
