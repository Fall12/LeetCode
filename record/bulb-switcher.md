# [319. 灯泡开关](https://leetcode-cn.com/problems/bulb-switcher/)
### 题意
初始时有n个灯泡关闭。第1轮，你打开所有的灯泡。第2轮，每两个灯泡你关闭一次。
第3轮，每三个灯泡切换一次开关（如果关闭则开启，如果开启则关闭）。  
第i轮，每i个灯泡切换一次开关。 对于第n轮，你只切换最后一个灯泡的开关。找出n轮后有多少个亮着的灯泡。
### 思路
```
1 2 3 4 5 6 7 8 9 10 11 12  
  2   4   6   8   10    12  
    3     6     9       12  
      4       8         12  
        5         10      
          6             12  
            7 8 9 10 11 12  
``` 
you can find only the square number is light.

### 代码
```cgo
    int bulbSwitch(int n) {
        return sqrt(n);
    }
```
           

