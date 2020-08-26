# Java 基本控制语句

## 读写语句

```java
ch = (char) System.in.read();  // 从键盘读取一个字符

System.out.print("ch is:" + ch);
System.out.println("ch is:" + ch);  // 带换行输出
```

## if 语句

```java
if (condituion) {
    statement sequence;
}
else if (condituion) {
    statement sequence;
}
else {
    statement sequence;
}
```

## switch 语句

```java
switch (condituion) {
    case cxonstant1:
        statement sequence;
        break;
    case cxonstant2:
        statement sequence;
        break;
    ...
    default:
        statement sequence;
}
```

case 语句可以为空：

```java
switch (condituion) {
    case cxonstant1:
    case cxonstant2:
        statement sequence;
        break;
    ...
    default:
        statement sequence;
}
```

case 语句可以嵌套：

```java
switch (ch1) {
    case 'A':
        statement sequence;
        switch (ch2) {
            case 'A':
                statement sequence;
                break;
            case 'B':
                statement sequence;
                break;
            ...
        }
    case 'B':
        statement sequence;
        break;
    ...
    default:
        statement sequence;
}
```

## for 循环

```java
for (initialization; condition; iteration) {
    // int i = 0 如果声明在循环外则循环结束后变量依然存在，
    // 否则变量结束i即无法访问
    statement;
}
```

> for 循环可没有循环体或者循环条件(一个至三个)

## for-each 循环



## while 循环

```java
while (condition) {
    statement;
}
```

## do-while 循环

```java
do {
} while (condition);
```

示例程序：

```java
// Guess the letter game, 4th version.
class Guess4 {
  public static void main(String args[])
    throws java.io.IOException {

    char ch, ignore, answer = 'K';

    do {
      System.out.println("I'm thinking of a letter between A and Z.");
      System.out.print("Can you guess it: ");

      // read a character
      ch = (char) System.in.read();

      // discard any other characters in the input buffer
      // **保证每行只读取第一个字符**
      do {
        ignore = (char) System.in.read();
      } while(ignore != '\n');

      if(ch == answer) System.out.println("** Right **");
      else {
        System.out.print("...Sorry, you're ");
        if(ch < answer) System.out.println("too low");
        else System.out.println("too high");
        System.out.println("Try again!\n");
      }
    } while(answer != ch);
  }
}
```

## break 语句

break 语句只能跳出所在那层循环。

### break 作为 goto 语句使用

示例程序1：

```java
// Using break with a  label.
class Break4 {  
  public static void main(String args[]) {  
    int i;

    for(i=1; i<4; i++) {
one:  {
two:    {
three:    {
            System.out.println("\ni is " + i);
            if(i==1) break one;
            if(i==2) break two;
            if(i==3) break three;

            // this is never reached
            System.out.println("won't print");
          }
          System.out.println("After block three.");
        }
        System.out.println("After block two.");
      }
      System.out.println("After block one.");
    }
    System.out.println("After for.");

  }  
}
```

```bash

```

示例程序2：

```java
// Another example of using break with a label.
class Break5 {  
  public static void main(String args[]) {  

done:
    for(int i=0; i<10; i++) {
      for(int j=0; j<10; j++) {
        for(int k=0; k<10; k++) {
          System.out.println(k + " ");
          if(k == 5) break done; // jump to done
        }
        System.out.println("After k loop"); // won't execute
      }
      System.out.println("After j loop"); // won't execute
    }
    System.out.println("After i loop");  
  }  
}
```

```bash

```

示例程序3：

```java
// Where you put a label is important.
class Break6 {  
  public static void main(String args[]) {  
    int x=0, y=0;

// here, put label before for statement.
stop1: for(x=0; x < 5; x++) {
         for(y = 0; y < 5; y++) {
           if(y == 2) break stop1;
           System.out.println("x and y: " + x + " " + y);  
         }
       }

       System.out.println();

// now, put label immediately before {
      for(x=0; x < 5; x++)
stop2: {
         for(y = 0; y < 5; y++) {
           if(y == 2) break stop2;
           System.out.println("x and y: " + x + " " + y);  
         }
       }

  }  
}
```

```bash

```

注意：不能使控制权转移到任何不包括break语句的代码块标记处。

```java
// This program contains an error.
class BreakErr {
  public static void main(String args[]) {

    one: for(int i=0; i<3; i++) {
      System.out.print("Pass " + i + ": ");
    }

    for(int j=0; j<100; j++) {
      if(j == 10) break one; // WRONG，one和break不在一个循环
      System.out.print(j + " ");

  }
}
```

## continue 语句

跳过当前循环剩下的部分，继续下一次循环。

```java
// Use continue.
class ContDemo {
  public static void main(String args[]) {
    int i;

    // print even number between 0 and 100
    for(i = 0; i<=100; i++) {  
      if((i%2) != 0) continue; // iterate
      System.out.println(i);
    }
  }
}
```

### 指定标记

```java
// Use continue with a label.
class ContToLabel {
  public static void main(String args[]) {

outerloop:
    for(int i=1; i < 10; i++) {
      System.out.print("\nOuter loop pass " + i + ", Inner loop: ");
      for(int j = 1; j < 10; j++) {
        if(j == 5) continue outerloop; // continue outer loop
        System.out.print(j);
      }
    }
  }
}
```
