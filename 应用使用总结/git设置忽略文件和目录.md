# git设置忽略文件和目录
### 1.登录git bash命令端进入本地git库目录
```bash
$ cd /d/ZGLDoingGitRepository/DoingGit/
```

### 2.创建.gitignore

```bash
$ notepad++ .gitignore
```

注[^notePad++]

### 3.修改文件，添加忽略正则
```bash
# 忽略*.o和*.a文件
 *.[oa]

# 忽略*.b和*.B文件，my.b除外
*.[bB]
!my.b

# 忽略dbg文件和dbg目录
dbg

# 只忽略dbg目录，不忽略dbg文件
dbg/

# 只忽略dbg文件，不忽略dbg目录
dbg
!dbg/

# 只忽略当前目录下的dbg文件和目录，子目录的dbg不在忽略范围内
/dbg

# 以'#'开始的行，被视为注释.
 * ？：代表任意的一个字符
    * ＊：代表任意数目的字符
    * {!ab}：必须不是此类型
    * {ab,bb,cx}：代表ab,bb,cx中任一类型即可
    * [abc]：代表a,b,c中任一字符即可
    * [ ^abc]：代表必须不是a,b,c中任一字符
```
#### 4.提交本地版本库，推送到远程项目，方便协作，项目管理



---

[^notePad++]: 在win10环境变量Path中配置`D:\Program Files (x86)\Notepad++`,即可使用NotePad++编辑。

