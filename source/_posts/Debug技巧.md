## 常见的bug类型

1. 语法错误

   SyntaxError：语法

   AttributeError：属性

   KeyError：关键字

   NameError：变量名

   ValueError：值

   IndexError：索引

   ZeroDivisionError：除数为0

2. 运行错误

   1. print法（开发过程中）：对折调试

   2. logging模块（重要位置）：debug、info、warning、error、critical

   3. pdb法：python -m pbd test.py

      ​			   python.set_trace（）

      ​							l	：打印代码

      ​							pp：打印值

      

   4. 调试工具

   5. reload（）

      ​	import机制

      ​	