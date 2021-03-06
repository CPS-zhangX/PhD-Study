# This is a note for CSCE531 Project 1b

Implement a calculator in Haskell as described in Section 2.6 [R].

Implement a calculator in Java as described in Section 2.7 [R]. Please use BNFC and Java under Ubuntu
for this. 

<b>[R]</b>Aarne Ranta [R]. Implementing Programming Languages: An Introduction to Compilers and Interpreters. College Publications, 2012. ISBN: 978-1-84890-064-6.

<b>所有的代码都在Calculator路径下</b>

Reference:

[R]

http://www.cse.chalmers.se/edu/year/2011/course/TIN321/lectures/bnfc-tutorial.html#toc6

https://github.com/BNFC/bnfc/tree/master/document/tutorial
## Haskell
在包含calc.cf文件的文件夹下执行： (这一步就是project1a)

bnfc -m Calc.cf

make

之后测试得到的抽象语法等信息，现在我们要做的就是将这些抽象的信息转化为计算器的计算结果。在于Test.hs所在的文件夹中新建两个文件：

Interpreter.hs

Calculator.hs
### Interpreter.hs
代码如下：
```
module Interpreter where
  
import AbsCalc
  
interpret :: Exp -> Integer
interpret x = case x of
    EAdd exp0 exp  -> interpret exp0 + interpret exp
    ESub exp0 exp  -> interpret exp0 - interpret exp
    EMul exp0 exp  -> interpret exp0 * interpret exp
    EDiv exp0 exp  -> interpret exp0 `div` interpret exp
    EInt n  -> n

```
### Calculator.hs
代码如下：
```
module Main where
  
import LexCalc
import ParCalc
import AbsCalc
import Interpreter
  
import ErrM
  
main = do
    interact calc
    putStrLn ""
  
calc s = 
    let Ok e = pExp (myLexer s) 
    in show (interpret e)
```

之后编译Calculator.hs即可：

ghc --make Calculator.hs
### 测试
#### 命令行输入参数
```
echo "1 + 2 * 3" | ./Calculator
```
#### 文件读入参数
```
./Calculator < ex1.calc
```
其中ex1文件中的内容为：

(123 + 47 - 6) * 222 / 4
## Java
在包含calc.cf文件的文件夹下执行： (这一步就是project1a)

bnfc -m -java Calc.cf

make

之后进去生成的Calc/Absyn文件夹，修改EInt.java, EAdd.java, EMul.java, EDiv.java, ESub.java, Exp.java文件：修改方式为在每个文件里面的类中添加一个eval()方法。
### Exp.java
添加一行
```
public abstract Integer eval() ;
```

### EInt.java
添加
```
public Integer eval() {return integer_ ;}
```

### EDiv.java
添加
```
public Integer eval() {return exp_1.eval() / exp_2.eval() ;}
```

### EAdd.java
添加
```
public Integer eval() {return exp_1.eval() + exp_2.eval() ;}
```

### ESub.java
添加
```
public Integer eval() {return exp_1.eval() - exp_2.eval() ;}
```

### EMul.java
添加
```
public Integer eval() {return exp_1.eval() * exp_2.eval() ;}
```

接下来复制Calc文件夹中的Test.java文件，重命名为Calculator.java。将里面的Test类更换为：
```
public class Calculator {
  public static void main(String args[]) throws Exception
  {
    Yylex l = new Yylex(System.in) ;
    parser p = new parser(l) ;
    Calc.Absyn.Exp parse_tree = p.pExp() ;
    System.out.println(parse_tree.eval());
  }
}
```
执行javac Calc/Calculator.java即可

### 测试
#### 命令行输入参数
```
echo "1 + 2 * 3" | java Calc/Calculator
```
#### 文件读入参数
```
java Calc/Calculator < ex1.calc
```
其中ex1文件中的内容为：

(123 + 47 - 6) * 222 / 4
