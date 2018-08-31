## 系统学习Linux Command Line Learning
左键复制，中键粘贴
cd -; cd ~username
>file　清空文件
cmdline ＆>file = cmdline > file 2>&1
echo $((2**3)) = 8 幂运算
touch {1..5}.txt
printenv查看有效变量
echo $(cal) 和　echo "$(cal)"的不同在于双引号之中的空白字符将会保留，不加双引号，其中的空白字符只保留一个．
shell命令行的快捷高级操作：
1. ctrl+t exchange
2. ctrl+f forward移动
3. ctrl+b backward移动
4. ctrl+k 光标后全部删除
5. ctrl+u 光标前全部删除
6. alt+d 删除当前光标后的词
7. alt+backspace 删除当前光标前的词
8. ctrl+y 粘贴刚才删除的
9. ctrl+p,ctrl+n 向上历史命令，向下历史命令
