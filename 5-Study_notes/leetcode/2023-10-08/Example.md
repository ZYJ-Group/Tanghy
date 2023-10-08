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
**1. 验证最优解是否正确**  




