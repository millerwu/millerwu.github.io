---
title: Efficient Integer To String
date: 2017-09-18 20:50:17
tags:
---

# Integer Converve to String

注意点   

- 写c++ 模板函数，可以涵盖使用 int， short， long， long long 类型的各个类型
- 注意char 数值的大小
- 考虑负数case

在muduo 库中看到一种很好的写法，记录下来


```
char digits[] = "9876543210123456789";
int zero = 9;

template <typename T>
int IntToString(char buf[], T t)
{
  int64_t num = static_cast<int64_t>(t);
  int size = 0;
  int i = 0;

  do {
    int index = static_cast<char>(num % 10);
    num = num/10;
    buf[i++] = digits[zero+index];
    size++;
  } while (num != 0);

  if (t < 0)  {
    buf[i++] = '-';
  }
  buf[i] = '\0';
  std::reverse(&buf[0], &buf[i]);

  return size;
}
```
自己在用普通模式写的情况下，因为负数的case，会导致代码逻辑写的比较复杂；使用这个方案，代码清晰，高效
