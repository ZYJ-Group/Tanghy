# leetcode
## 对数器-验证的重要手段
![image](https://github.com/ZYJ-Group/Tanghy/assets/94824386/70012ef8-1039-4d0c-8f94-d7b95d9b5362)  

### 笔记
**1. 验证最优解是否正确**  
输入 | 输出 | 功能  
--- | --- | --- 
暴力解 | ans1 | 判断是否一样
最优解 | ans2 | 同上

使用随机数据，可以控制数据的长度，数据值的范围，运行次数。

``` C++
int main(){
  // 随机数组最大长度
  int N = 200;
  // 随机数组每个值，在1-V之间等概率随机
  int V = 1000;
  // testTimes ： 测试次数
  int testTimes = 50000;
  cout << "测试开始" << endl;

  for (int i = 0; i < testTimes; i++) {
    // 随机得到一个长度，长度在[0-N-1]
    int n = rand() % N;
    // 得到随机数组
    int *arr = new int[n];
    for (int j = 0; j < n; j++) {
      // rand() -> int -> [0 , RAND_MAX]范围内的整数，等概率！
      arr[j] = rand() % V + 1;
    }

    int *arr1 = new int[n];
    int *arr2 = new int[n];
    int *arr3 = new int[n];

    // 复制数组
    for (int j = 0; j < n; j++) {
      arr1[j] = arr[j];
      arr2[j] = arr[j];
      arr3[j] = arr[j];

    // 排序
    selectionSort(arr1, n);
    bubbleSort(arr2, n);
    insertionSort(arr3, n);

    // 验证排序结果
    for (int j = 1; j < n; j++) {
      if (!is_sorted(arr1, arr1 + n) || !is_sorted(arr2, arr2 + n) || !is_sorted(arr3, arr3 + n)) {
        cout << "出错了！" << endl;
        break;
      }
        delete[] arr;
        delete[] arr1;
        delete[] arr2;
        delete[] arr3;
    }

    cout << "测试结束" << endl;

    return 0;
}    
```
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


