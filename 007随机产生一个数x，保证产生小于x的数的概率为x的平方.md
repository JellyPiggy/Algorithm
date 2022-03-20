随机产生一个数x，保证产生小于x的数的概率为x的平方

Math.rand()随机产生0-x的数的概率为x

# 一：

``` java
	public static void main(String[] args) {
        //测试下面的方法产生在0-x数的概率为x的平方
        int testTimes = 100000;
        int count = 0;
        double x = 0.9;
        for (int i = 0; i < testTimes; i++) {
            if (xPower2() < x) {
                count++;
            }
        }
        System.out.println(count/(double)testTimes);
        System.out.println(Math.pow(x, 2));
    }
	
    public static double xPower2() {
        return Math.max(Math.random() , Math.random());
    }
```

# 二：

``` java
class PreSum {
    private int[] preSum;
    public PreSum(int[] arr) {
        preSum = new int[arr.length];
        preSum[0] = arr[0];
        for (int i = 1; i < arr.length; i++) {
            preSum[i]  = arr[i] + preSum[i - 1]; 
        }
    }
    public int rangSum(int left, int right) {
        return left == 0 ? preSum[right] : preSum[right] - preSum[left - 1];
    }
}
```

