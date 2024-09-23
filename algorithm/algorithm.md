# algorithm

## 一、位运算的奇巧淫技

基础知识

> 与(&)：都为1结果为1
>
> 或(|)：有一个为1结果为1
>
> 异或(^)：二者不同时结果为1

注：在计算机运算中，应该把运算数都看作二进制数来运算

### 1、找出唯一成对的数

1-1000这1000个数放在含有1001个元素的数组中，只有唯一的一个元素值重复，其他均只出现一次，找出唯一成对的数

解法一：用没有重复数字的1-1000的异或来与数组的每一个元素异或，剩下的结果即为所求

```c
int main(){
    //定义一个整数表示元素个数
    int N=1001;
    //创建一个存放N个元素的数组
    int arr[N];
    //将1-N存到数组中
    for (int i = 0; i < N-1;i++){
        arr[i] = i+1;
    }
    //在数组的最后一位上随机添加一个1-N内的数
    arr[N - 1] = 911;
    //打印查看数组中的元素
    for (int i = 0; i < N;i++){
        printf("%d ", arr[i]);
    }
    printf("\n");
    //记录重复的数
    int x1 = 0;
    //将x1与1-N的每个数进行异或运算
    for (int i = 1; i < N ;i++){
        x1 = (x1 ^ i);
    }
    //将完成与无重复数的1-N进行异或的x1与数组中的每一个元素进行异或运算
    for (int i = 0; i < N ;i++){
        x1 = x1 ^ arr[i];
    }
    //最后的x1即为所求
    printf("%d\n", x1);
}
```

解法二：开辟辅助空间将数组元素作为辅助空间的索引值，遍历辅助空间给每个索引指向的元素的值加1，结果为2的即为重复元素

```c
//不同的解法不再重复书写声明，只写算法相关实现
//开辟辅助空间
int helper[N];
//初始化辅助空间
for (int i = 0; i < N;i++){
    helper[i]=0;
}
//对数组值作为辅助空间索引中的值进行自增操作
for (int i = 0; i < N;i++){
    helper[arr[i]]++;
}
//遍历辅助空间，值为2的索引即为所求结果
for (int i = 0; i < N;i++){
    if(helper[i]==2){
        printf("%d", i);
        break;
}
```

### 2、二进制中1的个数

实现一个函数，输入一个整数，输出该数二进制表示中1的个数

解法一：将1左移至32位上的每个位，每移一次与所求数做与运算，若结果与1左移所求位后的数相等，则这个位上为1

```java
public static void main(String[] args) {
    //创建Scanner对象
    Scanner s=new Scanner(System.in);
    //输入一个N
    int N=s.nextInt();
    //打印N的二进制形式
    System.out.println(Integer.toString(N,2));
    //定义计数器
    int count=0;
    //判断N的每一位与移位后的1与运算的结果是否等于移位后的1，是则计数器自增
    for(int i=0;i<32;i++){
        if((N&(1<<i))==(1<<i)){
             count++;
        }
    }
    //打印计数器结果
    System.out.println(count);
}
```

解法二：将N进行右移然后与1做与运算，结果为1则此时N的最末尾的二进制数为1

```java
for(int i=0;i<32;i++){
    if(((N>>>i)&1)==1){
        count++;
    }
}
```

解法三：将N减一后再与N进行与运算，若末尾为0则要向前面第一个1借位，若为1则直接减，这样每次与运算都会消掉一个末位的1，与运算的次数即为1的个数

```java
while(N!=0){
    N=((N-1)&N);
    count++;
}
```

### 3、将整数的奇偶位互换

```java
public static void main(String[] args) {
    //需要互换的数字
    int a=9;
    int b=SwapOE(a);
    System.out.println(b);
}
//奇偶交换函数
private static int SwapOE(int i) {
    //让i与1010_1010...(8个1010)进行与运算让i的偶数位变为0，这里用十六进制的a代表一个1010，共八个
    int ou=i&0xaaaaaaaa;
    //让i与0101_0101...(8个0101)进行与运算让i的奇数位变为0，这里用十六进制的5代表一个0101，共八个
    int ji=i&0x55555555;
    //让保留奇数位的左移一位，保留偶数位的右移一位，再让两数异或运算，得到的结果即为奇偶交换的结果
    return (ou>>1)^(ji<<1);

    //原理：将数与0xaaaaaaaa进行与运算后偶数位全部为0，奇数位保留原来的数，而与0x55555555进行与运算后偶数位全部为0，
    // 奇数位保留原来的数，在保留奇数位的左移一位，保留偶数位的右移一位后，奇偶将错位，0与任何数进行异或运算都为原本的数，
    // 因此结果为奇偶交换的数
}
```

### 4、0~1间的浮点实数的二进制表示

给一个浮点实数如0.625，类型为double，打印他的二进制表示如0.101，若无法用32位以内的二进制表示则打印“ERROR”

```java
public static void main(String[] args) {
    //定义一个浮点实数
    double num=0.625;
    //用字符串容器存放转换的二进制数
    StringBuilder sb=new StringBuilder("0.");
    while(num>0){
        //原浮点数乘2
        double b=num*2;
        //乘2后大于1
        if(b>=1){
            sb.append("1");
            num=b-1;
        }else{//乘2后下于1
            sb.append("0");
            //转变为乘2后的数
            num=b;
        }
        //若0.后的位数大于32则输出ERROR
        if(sb.length()>34){
            System.out.println("ERROR");
            return;
        }
    }
    //输入2二进制形式的数
    System.out.println(sb.toString());
}
//原理：整形通过除二来求二进制数，浮点数则通过乘2来求二进制数，当浮点数乘2后大于1，则其二进制数后补一个1，然后将成2后的数减一，若乘2后小于1，则补0，循环上述步骤，直指原浮点数为0为止
```

### 5、出现k次与出现1次

数组中只有一个数出现了1次，其他的数都出现了k次，请输出只出现出现了1次的数

```java
public static void main(String[] args) {
    //存数数组
    int[] arr={2,2,2,9,7,7,7,3,3,3,6,6,6,0,0,0};
    //数组长度
    int len=arr.length;
    //存放数组中每个数字的k进制字符数组
    char[][] kRadix=new char[len][];
    //数组中的数重复出现k次
    int k=3;
    //记录下面转换的三进制数中长度最长是多少，例如9为100，有3位，以此确定要做多少列的求和
    int maxlen=0;
    //转成k进制字符数组
    for (int i = 0; i < len; i++) {
        //将每个数组的数转换为k进制字符串并翻转，然后转换为字符数组，翻转是为了让低位对其，后面好做不进位加法
        kRadix[i]=new StringBuilder(Integer.toString(arr[i],k)).reverse().toString().toCharArray();
        if(kRadix[i].length>maxlen)
            //求三进制数中最长有几位
            maxlen=kRadix[i].length;
    }
    //存放三进制数中每一列数的和
    int[] resArr=new int[maxlen];
    //遍历每一行，每一行就代表一个数组中的一个数字
    for (int i = 0; i < len; i++) {
        //每一列就是这个数字在这一行上三进制的数值
        for (int j = 0; j < maxlen; j++) {
            //做不进位加法(这里只是做每一列数的相加，不进位的结果在后面通过求余求得)
            if(j>=kRadix[i].length)//如果j超出了三进制的位数，则加0
                resArr[j]+=0;
            else
                resArr[j]+=(kRadix[i][j]-'0');//j为三进制数的第几个位，其中存放所有三进制数的相同位的和,减'0'是将char类型数转换为int型来做加法
        }
    }
    //记录最终结果
    int res=0;
    //扫描存放三进制数和的数组
    for (int i = 0; i < maxlen; i++) {
        res+=(resArr[i]%k)*(int)(Math.pow(k,i));//(resArr[i]%k)的结果就是此位上三进制数的数字，在这里通过求余完成不进位处理，即余数就是每列相加的数的不进位的结果
        // Math.pow(k,i)表示求k的i次方，就是三进制转十进制的过程，其实本质就是将这个只出现了一次的数的三进制转换为十进制
    }
    System.out.println(res);//打印结果
}

//原理：k个相同的k进制数做不进位加法结果为0(因为是不进位，因此表现为k进制数的同位的每一列数相加)，这样将所给数转换为k进制数后再做不进位加法，有k个相同的数相加结果为0，只剩下一个单着的数
// 代码将所给数组中的每个数转换成k进制数，再通过翻转使每个三进制数的低位对其，然后将所有三进制数上同一位的数加起来，最后%k再乘权重转换为十进制数
```

## 二、查找排序

### 1、递归进行插入排序

```java
public static void insertSort(int[] arr,int k){
    //出口
    if(k==0){
        return;
    }
    //对前k-1个元素排序
    insertSort(arr,k-1);
    //把位置k的元素插入到前面的部分
    int x=arr[k];
    int index=k-1;
    while(index>-1&&x<arr[index]){
        arr[index+1]=arr[index];
        index--;
    }
    arr[index+1]=x;
}
```









## 小题基础练习

### 1、找出落单的那个数

对所有数进行异或操作，成对的会被消掉，最后保留的就是答案

### 2、整数是不是2的整数次方

这个数的二进制只有1个1，其他位上都是0，则为2的整数次方

```java
public static void main(String[] args) {
    int N=256;
    boolean flag;
    if(((N-1)&N)==0){
        flag=true;
    }else{
        flag=false;
    }
    System.out.println(flag);
}
```

### 3、用递归求阶乘

```java
static int f(int n){
    if(n==1)
        return 1;
    return n*f(n-1);
}
```

### 4、递归打印i到j

````java
public static void Print(int i,int j){
    if(i>j)
        return;
    System.out.print(i+" ");
    Print(i+1,j);

}
````

### 5、递归求数组的和

```java
public static int AddArr(int[] arr,int begin){
    if(begin==arr.length-1){
        return arr[begin];
    }
    return arr[begin]+AddArr(arr,begin+1);
}
```

### 6、递归翻转字符串

```java
public static String reverse(String src,int end){
    if(end==0)
        return ""+src.charAt(0);
    return src.charAt(end)+reverse(src,end-1);
}
```

### 7、求第n个斐波那契数

```java
public static int Fib(int n){
    if(n==1||n==2)
        return 1;
    return Fib(n-1)+Fib(n-2);
}
```

### 8、递归求最大公约数

```java
public static int gcd(int m,int n){
    if(n==0)
        return m;
    return gcd(n,m%n);
}
//辗转相除法
```

