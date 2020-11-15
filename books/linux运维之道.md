
### 常见用法
- grep --color doctype ./index.html
- netstat -nlp
- ps -aux
    - ps a 显示现行终端机下的所有程序，包括其他用户的程序
    - ps u 显示当前用户的进程
    - ps x 显示所有程序，不以终端机来区分
    - aux 和ef 是两种显示风格，前者为BSD 格式，后者为标注格式
        - ps -e 所有进程
        - ps -f 全格式
- sed
```sh
sed 's/yes/no/g' test.txt
sed '/static/a ipaddr=192.168.0.1' test.txt
# -f file
sed -f sed.sh test.txt 
```
- awk
```sh
# 是一种编程语言，用于linux/unit 下对文本和数据进行扫描与处理
echo hello the world | awk '{print $1, $2, $3}'
```
- bash 快捷键
```
// 光标移到开头结尾
<C-a> <C-e>
// 删除光标至行首、行尾
<C-u> <C-k>
// 删除光标前后单词
<C-w> <A-d>
```