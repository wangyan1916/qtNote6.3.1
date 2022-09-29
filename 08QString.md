16位 QChar

隐式共享（copy-on-write）



`append()`

`prepend()`

`count()`



### 初始化

```c++
QString str1 = "asd";
char a[] = "asd";
QString str2(a);
```

### 访问

`str[num]`

`str.at()` at是只读，效率更高

`str.right(5)`

`str.left(6)`

`str.mid(4, 5)`



### 使用

#### 用实际值代替特定控制字符

```c++
QString s1 = "那里有%1朵花";
int n = 12;
int m = 4;
s1.arg(n); //arg 是实参，用实际值代替特定控制字符

QString s1 = "那里有%1朵花和%2棵树";
s1.arg(n).arg(m);
```

#### 比较

```c++
QString::compare(a, b);
QString::compare(a, b, QT::CaseInsensitive); //忽略大小写

```

#### 类型转换

#### 字符串对齐

`leftJustified`

`rightJustified`

#### 格式转换

