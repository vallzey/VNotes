##### string
- 可以通过printf输出
```c
string str = "abcd";
printf("%s\n",str.c_str())
```
- It can use operator '+' to add two string variable
```c
stirng str1 = "abc", str2 = "xyz", str3;
str3 = str1 + str2;
```
-Two string type variables can be directly compared using ==, <>, and the comparison rule is alphabet order.
```c
stirng str1 = "abc", str2 = "xyz";
if(str2>str1) printf("OK!\n");
// The result is the "OK!" will be print.
```