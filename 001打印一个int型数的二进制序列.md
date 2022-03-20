打印一个int型数的二进制序列

# 一：

``` java
public static void main(String[] args) {
        print(-1);
    }
    //打印一个int类型数的二进制序列
    public static void print(int num) {
        for (int i = 31; i >= 0; i--) {
            System.out.print((num >> i) & 1);
            if (i % 8 == 0) System.out.print(" ");
        }
    }
```

# 二：

``` java
public static void main(String[] args) {
        print(2);
    }

    public static void print(int n) {
        for (int i = 31; i >= 0; i--) {
            System.out.print((n >> i ) & 1);
            if (i % 8 == 0) {
                System.out.print(" ");
            }
        }
    }
```

# 三：

``` java
public static void main(String[] args) {
        print(2);
    }

    public static void print(int n) {
        for (int i = 31; i >= 0; i--) {
            System.out.print((n >> i ) & 1);
            if (i % 8 == 0) {
                System.out.print(" ");
            }
        }
    }
```

