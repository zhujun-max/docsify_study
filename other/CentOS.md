
### 文件与目录操作命令
| 命令	 |  解析 | 
| ----------------- | ------------------------ |
|  cd /home	| 进入 ‘/home’ 目录    |
|  cd ..	|     返回上一级目录    |
|  cd ../..	|     返回上两级目录    |
|  cd -	|     返回上次所在目录    |
|  cp file1 file2	|     将file1复制为file2    |
|  cp -a dir1 dir2	|     复制一个目录    |
|  cp -a /tmp/dir1 .	|     复制一个目录到当前工作目录（.代表当前目录）    |
|  ls	|     查看目录中的文件    |
|  ls -a	|     显示隐藏文件    |
|  ls -l	|     显示详细信息    |
|  ls -lrt	|     按时间显示文件（l表示详细列表，r表示反向排序，t表示按时间排序）    |
|  pwd	|     显示工作路径    |
|  mkdir dir1	|     创建 ‘dir1’ 目录    |
|  mkdir dir1 dir2	|     同时创建两个目录    |
|  mkdir -p /tmp/dir1/dir2	|     创建一个目录树    |
|  mv dir1 dir2	|     移动/重命名一个目录    |
|  rm -f file1	|     删除 ‘file1’    |
|  rm -rf dir1	|     删除 ‘dir1’ 目录及其子目录内容    |

### 文件内容查看命令
| 命令 | 解析 |
| ----------------- | ------------------------ |
| cat file1	|  从第一个字节开始正向查看文件的内容  |
| head -2 file1	|  查看一个文件的前两行  |
| more file1	|  查看一个长文件的内容  |
| tac file1	|  从最后一行开始反向查看一个文件的内容  |
| tail -3 file1	|  查看一个文件的最后三行  |
| vi file	|  打开并浏览文件  |

### 文件内容处理命令
| 命令 | 解析 |
| ----------------- | ------------------------ |
| grep str /tmp/test	|  在文件 ‘/tmp/test’ 中查找 “str”  |
| grep ^str /tmp/test	|  在文件 ‘/tmp/test’ 中查找以 “str” 开始的行  |
| grep [0-9] /tmp/test	|  查找 ‘/tmp/test’ 文件中所有包含数字的行  |
| grep str -r /tmp/*	|  在目录 ‘/tmp’ 及其子目录中查找 “str”  |
| diff file1 file2	|  找出两个文件的不同处  |
| sdiff file1 file2	|  以对比的方式显示两个文件的不同  |
| vi file | i 进入编辑文本模式 <br/>Esc 退出编辑文本模式<br/>:w 保存当前修改 <br/>:q 不保存退出vi <br/>:wq 保存当前修改并退出vi<br/> |

### 查询操作
| 命令 | 解析 |
| ----------------- | ------------------------ |
| find / -name file1	 |    从 ‘/’ 开始进入根文件系统查找文件和目录 |
| find / -user user1	 |    查找属于用户 ‘user1’ 的文件和目录 |
| find /home/user1 -name *.bin	 |    在目录 ‘/ home/user1’ 中查找以 ‘.bin’ 结尾的文件 |
| find /usr/bin -type f -atime +100	 |    查找在过去100天内未被使用过的执行文件 |
| find /usr/bin -type f -mtime -10	 |    查找在10天内被创建或者修改过的文件 |
| locate *.ps	 |    寻找以 ‘.ps’ 结尾的文件，先运行 ‘updatedb’ 命令 |
| find -name ‘*.[ch]’ | xargs grep -E ‘expr’	 |    在当前目录及其子目录所有.c和.h文件中查找 ‘expr’ |
| find -type f -print0 | xargs -r0 grep -F ‘expr’	 |    在当前目录及其子目录的常规文件中查找 ‘expr’ |
| find -maxdepth 1 -type f | xargs grep -F ‘expr’	 |    在当前目录中查找 ‘expr’ |

### 压缩、解压
| 命令 | 解析 |
| ----------------- | ------------------------ |
|  bzip2 file1	  |  压缩 file1 |
|  bunzip2 file1.bz2	  |  解压 file1.bz2 |
|  gzip file1	  |  压缩 file1 |
|  gzip -9 file1	  |  最大程度压缩 file1 |
|  gunzip file1.gz	  |  解压 file1.gz |
|  tar -cvf archive.tar file1	  |  把file1打包成 archive.tar（-c: 建立压缩档案；-v: 显示所有过程；-f: 使用档案名字，是必须的，是最后一个参数） |
|  tar -cvf archive.tar file1 dir1	  |  把 file1，dir1 打包成 archive.tar |
|  tar -tf archive.tar	  |  显示一个包中的内容 |
|  tar -xvf archive.tar	  |  释放一个包 |
|  tar -xvf archive.tar -C /tmp	  |  把压缩包释放到 /tmp目录下 |
|  zip file1.zip file1	  |  创建一个zip格式的压缩包 |
|  zip -r file1.zip file1 dir1	  |  把文件和目录压缩成一个zip格式的压缩包 |
|  unzip file1.zip	  |  解压一个zip格式的压缩包到当前目录 |
|  unzip test.zip -d /tmp/	  |  解压一个zip格式的压缩包到 /tmp 目录 |