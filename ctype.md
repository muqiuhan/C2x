# 7.4 ctype.h
> TITLE : 字符处理
> TIME : 2021/1/23
> VERSION : 0.0.1
> AUTHOR : Muqiu-Han

> 1. The header <ctype.h> declares several functions useful for classifying and mapping characters.
> In all cases the argument is an int, the value of which shall be representable as an unsigned char or shall equal the value of the macro EOF.
> If the argument has any other value, the behavior is undefined.

1. 头文件ctype.h中声明了几个用于分类和映射字符的函数.
   不管在什么情况下，参数都是一个int型，它的值应该可以用unsigned char表示，或者等于宏EOF的值
   如果参数还有其他的值, 那么这种情况是未定义的(不合法)
   
> 2. The behavior of these functions is affected by the current locale. Those functions that have locale-specific aspects only when not in the "C" locale are noted below.

2. 这些函数的所作所为取决于当前的本地环境, 只有当那些特定的功能方面不是下面提到的“C”语言环境。

__译者注:__ 一下的 “特定区域” 为某个国家的特定语言环境

> 3. The term printing character refers to a member of a locale-specific set of characters, each of which occupies one printing position on a display device;
> the term control character refers to a member of a locale-specific set of characters that are not printing characters
> All letters and digits are printing characters.

3. 术语 "可打印字符" 是指特定区域的字符串中的其中一个，每个字符在显示设备上占据一个位置;
   术语 "控制字符" 是指一组特殊的字符拥有特殊的功能，使用其并不会打印字符
   所有的字母和数字都属于 "可打印字符"

## 7.4.1 关于字符类的函数
> 1. The functions in this subclause return nonzero (true) if and only if the value of the argument c conforms to that in the description of the function.
（在以下函数中）仅当参数c的值与函数描述中的值一致时，该子句中的函数才返回非零(true)。

__译者注: __ 以下函数都来自ctype.h

### 7.4.1.1 函数 isalnum
```C
int isalnum(int c);
```
> The isalnum function tests for any character for which isalpha or isdigit is true.
isalnum函数将测试isalpha或isdigit为true的任何字符。

### 7.4.1.2 函数isalpha
```
int isalpha(int c);
```
> The isalpha function tests for any character for which isupper or islower is true, or any character that is one of a locale-specific set of alphabetic characters for which none of iscntrl, isdigit, ispunct, or isspace is true.

isalpha函数会先将参数传给isupper和islower, 只要其中一个函数的返回值是true, 那么isalpha函数的返回值就是true, 
或者说任何字符，是特定于语言环境设置的一组字母字符，只要isalpha为真, 那么iscntrl、isdigit、ispunct或isspace都不为真。

### 7.4.1.3 函数isblank
```
int isblank(int c);
```
> The isblank function tests for any character that is a standard blank character or is one of a locale-specific set of characters for which isspace is true and that is used to separate words within a line of text. 
> The standard blank characters are the following: space ( ’ ’ ), and horizontal tab ( ’\t’ ). In the "C" locale, isblank returns true only for the standard blank characters.

isblank函数将测试标准空白字符或isspace函数测试为真, 且用于分隔一行文本中的单词的特定于区域的字符集中的任何字符. 标准的空白字符有空格，tab.
在C语言中， isblank只当字符是标准空白的时候返回true.

### 7.4.1.4 函数iscntrl
```
int iscntrl(int c);
```
> The iscntrl function tests for any control character.

iscntrl测试字符是否是控制字符

### 7.4.1.5 函数isdigit
```
int isdigit(int c);
```
> The isdigit function tests for any decimal-digit character (as defined in 5.2.1).

isdigit函数测试字符是否是十进制数字

### 7.4.1.5 函数isgraph
```
int isgraph(int c);
```
> The isgraph function tests for any printing character except space ( ’ ’ ).

isgraph函数测试字符是否是可以打印的，但是除了空格之外

### 7.4.1.7 函数islower
```
int islower(int c);
```

> The islower function tests for any character that is a lowercase letter or is one of a locale-specific set of characters for which none of iscntrl, isdigit, ispunct, or isspace is true.
> In the "C" locale, islower returns true only for the lowercase letters (as defined in 5.2.1).

islower函数将测试字符是否是小写字母或者是iscntrl、isdigit、ispunct或isspace测试为false的特定于区域设置的字符集中的一个字符。

### 7.4.1.8 函数isprint
```
int isprint(int c);
```
> The isprint function tests for any printing character including space ( ’ ’ ).

isprint函数测试字符是否是可以打印的，并且包括了空格

### 7.4.1.9 函数ispunct
```
int ispunct(int c);
```
> The ispunct function tests for any printing character that is one of a locale-specific set of punctuation characters for which neither isspace nor isalnum is true.
> In the "C" locale, ispunct returns true for every printing character for which neither isspace nor isalnum is true.

ispunct函数测试字符是否是可打印的， 并且这些字符是特定于区域设置的字符集中的一个标点符号，通过isspace和isalnum的测试都是false。
在c语言中， ispunct只有当参数是任何可打印字符并且通过isspace和isalnum的测试都是false的时候才返回true

### 7.4.1.10 函数isspace
```
int isspace(int c);
```
> The isspace function tests for any character that is a standard white-space character or is one of a locale-specific set of characters for which isalnum is false.
> The standard white-space characters are the following: space ( ’ ’ ), form feed ( ’\f’ ), new-line ( ’\n’ ), carriage return ( ’\r’ ), horizontal tab ( ’\t’ ), and vertical tab ( ’\v’ ).
> In the "C" locale, isspace returns true only for the standard white-space characters.

isspace函数测试字符是否是空白的，或者是特定区域设置中的空白，并且isalnum测试为false的.
标准的空白字符应该是: 空格， \f \n \r \t \v
在c语言中，isspace只要当参数是标准空白字符的时候才会返回true

### 7.4.1.11 函数isupper
```
int isupper(int c);
```
> The isupper function tests for any character that is an uppercase letter or is one of a locale-specific
> set of characters for which none of iscntrl, isdigit, ispunct, or isspace is true. In the "C" locale,
> isupper returns true only for the uppercase letters (as defined in 5.2.1).

isupper函数测试字符是否是大写的，或者是特定区域设置中的字符， 并且这个字符在iscntrl isdigit isspace的测试中都是false的，
在c语言中， isupper只有当参数是大写字母的时候才会返回true

### 7.4.1.12 isxdigit函数
```
int isxdigit(int c);
```
> The isxdigit function tests for any hexadecimal-digit character (as defined in 6.4.4.1).
isxdigit函数判断字符是否是十六进制的

## 7.4.2 字符大小写转换函数

### tolower函数
```
int tolower(int c);
```
> The tolower function converts an uppercase letter to a corresponding lowercase letter.

tolower函数会把大写字母转换成对应的小写字母

#### 返回值
> If the argument is a character for which isupper is true and there are one or more corresponding characters, as specified by the current locale, for which islower is true, the tolower function returns one of the corresponding characters (always the same one for any given locale); otherwise, the argument is returned unchanged.

如果参数通过isupper测试为true, 并有一个或多个由当前语言环境指定的通过islower测试为true的对应字符， 则tolower函数将返回其中一个对应字符（对于任何给定的语言环境，总是相同的字符）；否则，参数将原封不动地返回。

### 7.4.4.2 toupper函数
和上面的相反
