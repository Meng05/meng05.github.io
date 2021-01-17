# 遍历文件树修改文件夹名称与权限中遇到的一些问题


#### 背景：

平常用Typora做一些记录，整理的时候发现有很多文件夹权限0o777，导致在Terminal上显示背景很难看，于是打算批量更改一下。结果因为文件名包含空格和其他特殊的字符遇到了一些问题。

最后发现其实简单的办法是直接使用chmod 的-R 参数达成目的, 不过解决问题的过程还是让自己对问题有了更深入的了解。在这里记录下来，或许有遇到类似问题的朋友能看到。

<!--more-->

`man chmod`

>-R  Change the modes of the file hierarchies rooted in the files, instead of just the files themselves.  Beware of unintentionally matching the .. hardlink to the parent directory when using wildcards like ``.*''.


#### 不作重命名的情况下如何操作带有特殊字符的文件？下面的两种方式经测试均可以。



`find . -type d -name '* *'|sed 's/ /\\ /g'|xargs chmod 644`

`find . -type d -name '* *' -exec chmod 755 {} \;`


#### 重命名的尝试：如何遍历整个文件树，对其中的一些文件夹名称做修改？

#### 实验：

手工建立一个文件目录结构如下：嵌套了多层文件夹，文件夹名称上有空格和特殊字符

![Screen Shot 2021-01-17 at 16.53.17](https://tva1.sinaimg.cn/large/008eGmZEly1gmrhz1ntfuj31gk0ouaem.jpg)

下面这些方式经常出现警告，表示在find 某个文件或文件夹时："No sun file or directory",  但是重复执行几次也能完成任务

```sh
find . -type f -print0|xargs -0 rename 's/ /_/g'
find . -type d -name "* *" -exec rename 's/ /#/g' {} \;
find . -type f -name '* *' -execdir mv {} {}_renamed ';'
find . -type d -name '* *' -exec sh -c 'x="{}"; mv "$x" "${x}_test"' \;
```

于是只好换一种方法，写一段Python脚本试一下

```python
import os
import time
import re


fileRoot = os.getcwd()
print(fileRoot)
for (root, dirs,files) in os.walk(fileRoot, topdown=False):
    print('root',root)
    # print('dirs',dirs)
    # print('files',files)
    # os.chmod(root, 0o744)
    newName = re.sub(r'_+test', '', root)
    if (newName != root):
        os.rename(root, newName)
        print(root, newName)
    print('------------------------------')


```

结果也出现类似的错误提示：

>FileNotFoundError: [Errno 2] No such file or directory: '/Users/mengzhao/code/bash-intro/foo/bar/fruit apple 5.assert_______test/apple fuji.asset' -> '/Users/mengzhao/code/bash-intro/foo/bar/fruit apple 5.assert/apple fuji.asset'


最后，发现错误提示的原因有二：

1）os.rename 方法接受的参数要求是绝对路径

2）遍历的顺序有问题


更改后如下：

```python
# 遍历所有子文件，包括名称里包含空格的
# 更改权限

import os
import time
import re

startTime = time.time()

# 需要处理目录的路径
fileRoot = os.getcwd()

def Main():
    for (root, dirNames,fileNames) in os.walk(fileRoot, topdown=False):
        print(root)
        os.chmod(root, 0o744)
        if len(dirNames) != 0:
            print("root:", root)
            print("dirs:",dirNames)
            for dirName in dirNames:
                newdirName = re.sub(r'_', ' ', dirName)
                if newdirName != dirName:
                    print("old name:", dirName)
                    print('🦊 new name:',newdirName)
                    # BUG Fixed: Absolute path!!!
                    os.rename(os.path.join(root,dirName), os.path.join(root,newdirName))
        print('------------------------------')


if __name__ == '__main__':
    Main()
    print('Time total: %.2fs' % (time.time() - startTime))
    print('Current time: %s' % time.strftime('%Y-%m-%d %H:%M:%S', time.localtime(time.time())))
```


测试结果：

- 当参数为topdown=True时，只能完成第一层的文件名更改，之后的更改都失败（没有报错）。

- 当参数topdown=False时，如预期完成所有文件夹名称的更改

- 与-exec 一样，空格不影响结果，不需要额外处理
- 之前的find命令会不会遇到类似的问题？！由于遍历的方式是先序，父文件夹更改了名称，子文件夹的路径没有得到及时更新，因而找不到了。有没有参数可以改变遍历的顺序呢？查看find的文档，果然有一个可以改变遍历顺序的参数-d可以将遍历顺序从pre-order改变为post-order。重新测试：`find . -type d -d -name "*#*" -exec rename 's/#/_/g' {} \;` 之前的问题解决了，但之前的代码还有另一个严重的问题，这行命令可能同时更改父文件夹和子文件夹中的字符，也会导致路径出错。所以还是要把路径和文件夹名称分开来处理。



Folder names in post-order:
![Screen Shot 2021-01-17 at 16.52.57](https://tva1.sinaimg.cn/large/008eGmZEly1gmrhze5a9xj31ka0ogn1s.jpg)



