# leetcode
## 时间复杂度和空间复杂度
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/1ee46368-5159-4b77-8244-5f185aba2869)  


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

## 二分搜索
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/05d0685e-5a61-4ace-a7b6-c095343f964c)

### 笔记
**1. 在有序数组中确定num存在还是不存在**  
```C++
bool right(vector<int>& sortedArr, int num) {
  for (int cur : sortedArr) {
    if (cur == num) {
      return true;
    }
  }
  return false;
}

//保证arr有序，才能用这个方法
bool exist(vector<int>& arr, int num) {
  if (arr.empty()) {
    return false;
  }
  int l = 0; r = arr.size() - 1, m = 0;
  while (l <= r) {
    m = (l + r) /2;
    if (arr[m] == num) {
      return true;
    } else if(arr[m] > num) {
      r = m - 1;
    } else {
      l = m + 1;
    }
  }
  return false;
}

int main() {
  int N = 100;
  int V = 1000;
  int testTime = 50000;
  cout << "测试开始" << endl;
  for (int i = 0; i < testTime; i++) {
    int n = rand() % N;
    vector<int> arr;
    for (int j = 0; j < n; j++) {
      arr.push_back(rand() % V + 1);
    }
    sort(arr.begin(), arr.end());
    int num = rand() % V;
    if (right(arr, num) != exist(arr, num)) {
      cout << "出错了！" << endl;
    }
  }
  cout << "测试结束" << endl;
  return 0;
}
```

**2. 在有序数组中找>=num的最左位置**  
``` C++
bool left(vector<int>& arr, int num) {
  if (arr.empty()) {
    return false;
  }
  int l = 0, r = arr.size() - 1, m = 0;
  int ans = -1;
  while (l <= r) {
    m = (l + r) / 2;
    if (arr[m] >= num) {
      ans = m;
      r = m - 1;
      } else {
        l = m + 1;
      }
  }
  return ans;
}
```
**3. 二分搜索不一定发生在有序数组上（比如寻找峰值问题）**  
```C++
// 峰值元素是指其值严格大于左右相邻值的元素
// 给你一个整数数组 nums，已知任何两个相邻的值都不相等
// 找到峰值元素并返回其索引
// 数组可能包含多个峰值，在这种情况下，返回 任何一个峰值 所在位置即可。
// 你可以假设 nums[-1] = nums[n] = 无穷小
// 你必须实现时间复杂度为 O(log n) 的算法来解决此问题。
#include <vector>

class Solution {
public:
    int findPeakElement(std::vector<int>& nums) {
        if (nums.empty()) {
            return -1;  // 返回一个特殊值表示没有找到峰值
        }

        int l = 0, r = nums.size() - 1, m = -1;
        int n = nums.size();

        // 处理特殊情况，数组长度为1时，直接返回0
        if (n == 1) {
            return 0;
        }

        while (l <= r) {
            m = l + (r - l) / 2;

            // 检查是否是峰值
            if ((m == 0 || nums[m] > nums[m - 1]) && (m == n - 1 || nums[m] > nums[m + 1])) {
                return m;
            }

            // 如果右侧元素大于当前元素，则峰值一定在右侧
            if (m < n - 1 && nums[m] < nums[m + 1]) {
                l = m + 1;
            } else {
                // 否则，峰值一定在左侧
                r = m - 1;
            }
        }

        return -1;  // 如果数组中没有峰值，返回一个特殊值表示未找到
    }
};
```
[链接](https://leetcode.cn/problems/find-peak-element/submissions/)  

**ps.小细节**  
1. 在计算 m 的时候，可以采取 m = (l + r) / 2 的方式， 但是可能会存在溢出的可能性。比如l为15亿，r为16亿，此时l + r会超出int的数值范围。可替代的方式有：m = l + (r - l) / 2 和 m = l + ((r - l) >> 1)。  


