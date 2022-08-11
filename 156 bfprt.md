无序数组中求第 K 小的数

```java
public static int process1(int[] arr, int index) {
    int L = 0;
    int R = arr.length - 1;
    int pivot = 0;
    int[] range = null;
    while (L < R) {
        pivot = arr[L + (int) (Math.random() * (R - L + 1))];
        range = partition(arr, L, R, pivot);
        if (index < range[0]) {
            R = range[0] - 1;
        } else if (index > range[1]) {
            L = range[1] + 1;
        } else {
            return pivot;
        }
    }
    return arr[L];
}


// 改写快排，时间复杂度为 O(N)
// k >= 1
public static int minKth(int[] arrary, int k) {
    int[] arr = copyArr(arrary);
    return process(arr, 0, arr.length - 1, k - 1);  // 从小到大排序后 k - 1 位置的数为第 k 小的数
}

// arr[L..R] 范围上，排序完后(不是真的去排序)，返回index位置的数
public static int process(int[] arr, int L, int R, int index) {
    if (L == R) return arr[L];  // index 一定在 L…R，如果L=R，那 index 也等于L和R
    int pivot = arr[L + (int) (Math.random() * (R - L + 1))];
    int[] range = partition(arr, L, R, pivot);
    if (index >= range[0] && index <= range[1]) {
        return arr[index];
    } else if (index < range[0]) { // 下面这里只会走一边，时间复杂度为 O(N)，而不是像快排一样为 O(N * logN)
        return process(arr, L, range[0] - 1, index);
    } else {
        return process(arr, range[1] + 1, R, index);
    }
}

public static int[] partition(int[] arr, int L, int R, int pivot) {
    int less = L - 1;
    int more = R + 1;
    int cur = L;
    while (cur < more) {
        if (arr[cur] < pivot) {
            swap(arr, ++less, cur++);
        } else if (arr[cur] > pivot) {
            swap(arr, --more, cur);
        } else {
            cur++;
        }
    }
    return new int[] {less + 1, more - 1};
}

public static void swap(int[] arr, int i, int j) {
    int tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
}

public static int[] copyArr(int[] arrary) {
    int[] arr = new int[arrary.length];
    for (int i = 0; i < arrary.length; i++) {
        arr[i] = arrary[i];
    }
    return arr;
}
```

![1](assets/1.png)

为啥要5个一组，3个或7个不行吗？可以，人家是5个人一起发明的，就是自己想用5个



```java
public static int minKth(int[] arr, int k) {
    return bfprt(arr, 0, arr.length - 1, k - 1);  // 从小到大排序后 k - 1 位置的数为第 k 小的数
}


// ① 五个一组
// ② 小组排序
// ③ 拿出每组中的中位数组成新数组m--- m 规模是原来的 N / 5
// ④ 拿出数组m中的中位数p  --- 求 N / 10 处的数就是它的中位数
// ⑤ 根据 p 去partition
public static int bfprt(int[] arr, int L, int R, int index) {
    if (L == R) return arr[L];
    int pivot = medianOfMedians(arr, L, R);
    int[] range = partition(arr, L, R, pivot);
    if (index >= range[0] && index <= range[1]) {
        return arr[index];
    } else if (index < range[0]) {
        return bfprt(arr, L, range[0] - 1, index);
    } else {
        return bfprt(arr, range[1] + 1, R, index);
    }
}

// L...R
//每五个数一组
//每一个小组内部排好序
//小组的中位数组成新数组
//这个新数组的中位数返回
public static int medianOfMedians(int[] arr, int L, int R) {
    int size = R - L + 1;
    int offset = size % 5 == 0 ? 0 : 1;
    int[] mArr = new int[size / 5 + offset];
    for (int team = 0; team < mArr.length; team++) {
        int teamFirst = L + team * 5;
        mArr[team] = getMedian(arr, teamFirst, Math.min(R, teamFirst + 4));
    }
    return bfprt(mArr, 0, mArr.length - 1, mArr.length / 2);
}

public static int getMedian(int[] arr, int L, int R) {
    insertionSort(arr, L, R); // 就只有5个数，选常数时间最好的
    return arr[(L + R) / 2];
}

public static void insertionSort(int[] arr, int L, int R) {
    for (int i = L + 1; i <= R; i++) {
        for (int j = i; j > L && arr[j - 1] > arr[j]; j--) {
            swap(arr, j - 1, j);
        }
    }
}

public static int[] partition(int[] arr, int L, int R, int pivot) {
    int less = L - 1;
    int more = R + 1;
    int cur = L;
    while (cur < more) {
        if (arr[cur] < pivot) {
            swap(arr, ++less, cur++);
        } else if (arr[cur] > pivot) {
            swap(arr, --more, cur);
        } else {
            cur++;
        }
    }
    return new int[] {less + 1, more - 1};
}

public static void swap(int[] arr, int i, int j) {
    int tmp = arr[i];
    arr[i] = arr[j];
    arr[j] = tmp;
}
```

