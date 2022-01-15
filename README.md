#### Vim 配置

### 源码安装 Vim

- 若系统未安装Python,则可先从源码安装Python3

  1. 下载Python3源码包,如[Python-3.8.12.tar.xz](https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tar.xz)  
     `wget https://www.python.org/ftp/python/3.8.12/Python-3.8.12.tar.xz`

  2. 解压源码包  
     `tar -xJvf Python-3.8.12.tar.xz`

  3. 安装编译依赖  
     `yum-builddep python3`
     > <small>若报"yum-builddep"命令未找到,则先安装yum-utils</small>  

  4. 进入解压后的目录,执行  
     `./configure --prefix=/usr/local/Python-3.8.12 --enable-optimizations`

  5. 编译安装,执行  
     `make -j $(nproc) && make install`
     > <small>若报"make: *** [profile-opt] Error 2",则可删除configure时的--enable-optimizations参数再执行</small>  

  6. 验证是否安装成功,执行:  
     `python3.8`  
     > <small>若未进入交互界面,可能为系统中已存在其他版本的Python3,可手动将本次安装的Python的可执行目录添加至环境变量中</small>  
     > <small>执行 `echo PATH=$PATH:/usr/local/Python-3.8.12/bin`</small>

  > <small>[参考文档: https://devguide.python.org/setup/#build-dependencies]</small>


- 源码安装 Vim

  1. 从github上克隆vim仓库:  
     `git clone https://github.com/vim/vim`

  2. 进入克隆后的vim目录并更新到最新版本  
     `git pull`

  3. 安装编译依赖  
     `yum-builddep vim`

  4. 设置编译参数并执行  
     ```Shell
     ./configure \
     --with-features=huge \
     --enable-multibyte \
     --enable-luainterp=yes \
     --enable-perlinterp=yes \
     --enable-python3interp=dynamic \ 
     --enable-tclinterp=yes \
     --enable-rubyinterp=yes \
     --enable-cscope \
     --with-tclsh=tclsh \
     --with-ruby-command=ruby \
     --with-python3-config-dir=/usr/local/lib/python3.8/config-3.8-x86_64-linux-gnu \
     --with-python3-command=python3.8 \
     --enable-gui=auto \
     --enable-gtk2-check \
     --enable-fontset \
     --enable-largefile \
     --disable-netbeans \
     --with-compiledby="guanvix@gmail.com" \
     --prefix=/usr/local/vim \
     --enable-fail-if-missing \
     
     #参数说明
     --with-features=huge           # 支持最大特性 
     --enable-multibyte             # 打开多字节支持,可以在Vim中输入中文
     --enable-luainterp=yes         # 打开对lua编写的插件支持 
     --enable-perlinterp=yes        # 打开对perl编写的插件支持
     --enable-python3interp=dynamic # 打开对Python3编写的插件支持,指定dynamic参数则动态支持 
     --enable-tclinterp=yes         # 打开对tcl编写的插件支持
     --enable-rubyinterp=yes        # 打开对ruby编写的插件支持
     --enable-cscope                # 打开对cscope的支持
     --with-tclsh=tclsh             # 指定tcl命令为tclsh 
     --with-ruby-command=ruby       # 指定ruby命令为ruby 
     --with-python3-config-dir      # 指定python3路径,可通过whereis python3.8查询
     --with-python3-command         # 指定python命令,如有多个python版本可依据自身需要而定
     --enable-gui=auto              # 据可用的GUI库自动构建
     --enable-gtk2-check            # 如果自动选择GUI,请检查GTK default=yes
     --enable-fontset               # 包括X fontset输出支持
     --enable-largefile             # 提供对大文件的支持
     --disable-netbeans             # 禁用NetBeans集成支持
     --with-compiledby              # 编译者
     --prefix                       # 安装位置
     --enable-fail-if-missing       # 如果依赖于其他特性,则失败

     ```

  5. 验证是否安装成功   
     `vim --version`


  > <small>[参考文档: https://www.jianshu.com/p/aa5ea81bbc72]</small>  
  > <small>可通过 `./configure --help` 查看参数详细的情况</small>
