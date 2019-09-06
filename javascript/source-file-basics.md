## 源文件基础要素

### 文件名
文件名必须全部是小写的，可以带有下划线和中划线，但是不能带有其他的标点符号。遵循项目使用的惯例，文件名的后缀必须是`.js`。

### 文件编码：UTF-8
源文件必须使用UTF-8编码。

### 特殊字符

#### 空白字符
除了换行符，ASCII码水平空格符(0x20)是唯一可以出现在源代码任何地方的字符。这意味着：
- 其他空白字符在string字面量中是转义的
- Tab制表符不能用来缩进

#### 特殊转义字符
对于拥有转义含义的字符(`\', \", \\, \b, \f, \n, \r, \t, \v`)，应该直接使用该转义字符而不是使用相应的数字转义(eg `\x0a, \u000a, or \u{a}`)。永远不要使用八进制数字转义。

#### 非ASCII字符
剩下的非ASCII字符，使用Unicode字符（e.g. ∞）或者等价的十六进制、Unicode转义字符（e.g. \u221e）都可以，这取决于哪一种使代码更好读懂。

> 提示：在使用Unicode转义字符、Unicode字符的情况下，注释会非常有用。

| 例子                                       | 讨论                     |
| ---------------------------------------- | ---------------------- |
| `const units = 'μs';`                    | 最佳：即使没有注释也很清楚。         |
| `const units = '\u03bcs'; // 'μs'`       | 允许：但是没有理由这样做。          |
| `const units = '\u03bcs'; // Greek letter mu, 's'` | 允许：但是很笨拙，容易犯错。         |
| `const units = '\u03bcs';`               | 不好：代码阅读者根本不知道这是什么。     |
| `return '\ufeff' + content; // byte order mark` | 良好：使用非打印字符的转义，需要的时候注释。 |

> 提示：永远不要因为出于对某些程序不能正确的处理非ASCII字符的恐惧而让你的代码变得不可读。如果那些程序真的不能处理，那么这些程序就不是完整的，它们必须被修复。
