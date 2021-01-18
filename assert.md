# assert.h

## 1. 断言 <assert.h>
> The header<assert.h> defines theassertandstatic_assert macros and refers to another macro:

```C
NODEBUG
```

头文件<assert.h>定义assert 和 static_assert，并且定义了另一个宏: NDEBUG

> which is not defined by<assert.h>. If NDEBUG is defined as a macro name at the point in the source file where<assert.h>is included, the assert macro is defined simply as

如果在源文件中NDEBUG不是由<assert.h>定义的宏, 那包含<assert.h>的时候，assert会被定义为:

```C
#define assert(ignore) ((void)0)
```

> The assert macro is redefined according to the current state of NDEBUG each time that <assert.h>is included.

每次包含<assert.h>时，都会根据NDEBUG的当前状态重新定义assert宏。

## 2.

> The assert macro shall be implemented as a macro, not as an actual function. If the macro definition is suppressed in order to access an actual function, the behavior is undefined.

assert实现要是个宏，而不是一个函数,如果为了访问实际函数而取消宏定义，这种行为是没定义的哦。

## 3. static_assert宏
static_assert扩展自  _Static_assert

### 译者补充
> _Static_assert是c11新增的关键字，在C11里面，它接收一个表达式参数，一个错误消息，如果表达式是false (应当说是0), 则编译时期输出错误消息

### 4. 返回值
> 这玩意儿没返回值

## 总结
> The assert macro puts diagnostic tests into programs; it expands to a void expression.  When it is executed, if expression (which shall have a scalar type) is false (that is, compares equal to 0),the assert macro writes information about the particular call that failed (including the text of the argument, the name of the source file, the source line number, and the name of the enclosing function— the latter are respectively the values of the preprocessing macros __FILE__ and __LINE__ and of the identifier __func__ ) on the standard error stream in an implementation-defined format.201)It then calls the abort function.

assert宏将会把需要进行判断的表达式放到程序中，这个表达式会展开成一个void的表达式, 当它被执行的时候，如果为false, assert就会打印特定的信息, 包括参数的相关内容，在啥文件，哪行儿，哪个函数，然后调用abort函数