函数f()能等概率产生一个1\~5的数，利用f()写一个能随机产生0~7的数

``` java
//函数f()能等概率产生一个1~5的数，利用f()写一个能随机产生0~7的数，
    // 又怎样通过写出的方法等概率产生0~6的数，又怎么等概率得到1~7的数呢
    //又怎么通过上面的思想 由等概率产生3~19的函数g()等概率得到20~56的数呢？
    public static void main(String[] args) {

    }

    public static int f() {
        return (int) (Math.random() * 5) + 1;
    }

    public static int f1() {
        int a = 0;
        do {
            a = f();
        } while (a == 3);
        //经过上面这层循环，a将会等概率等于1/2/4/5，然后下面将等概率返回0/1
        return a < 3 ? 0 : 1;
    }

    //等概率产生0~7的数
    public static int f2() {
        return (f1() << 2) + (f1() << 1) + f1();  //等概率产生000~111的数，即0~7的数。
    }

    //等概率产生0~6的数
    public static int f3() {
        int a = 0;
        do {
            a = f2();
        } while (a == 7);
        return a;
    }

    //等概率得到1~7的数
    public static int f4() {
        return f3() + 1;
    }

    //等概率等到3~19
    public static int g() {
        return (int) (Math.random() * 17) + 3;
    }

    //按上面的思想通过g()产生一个等概率产生0或1的数
    public static int g1() {
        int a = 0;
        do {
            a = g();
        } while (a == 11);
        return a < 11 ? 0 : 1;
    }

    //一个等概率产生0~63的函数
    public static int g2() {
        return (g1() << 5) + (g1() << 4) + (g1() << 3) 
                + (g1() << 2) + (g1() << 1) + g1();
    }

    //等概率得到20~56的数
    public static int g3() {
        int a = 0;
        do {
            a = g2() + 10;
        } while (a > 56);
        return a;
    }
```

# 二：

``` java
//通过等概率等到6~18的函数f()写一个等概率等到3~25的函数
    public int f() {
        return (int) (Math.random() * 13) + 6;
    }
    
    public int f1() {
        int a = 0;
        do {
            a = f();
        } while (a == 12);
        return a < 12 ? 0 : 1;
    }
    
    public int f2() {
        return (f1() << 4) + (f1() << 3) + (f1() << 2) + (f1() << 1) + f1();
    }
    
    public int f3() {
        int a = 0;
        do {
            a = f2() + 3;
        } while (a >25);
        return a;
    }
```

