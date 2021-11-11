---
layout: post
title: IC_EDA环境搭建
date: 2021-11-11 10:30:00
tags: 
- IC验证
- 环境搭建
published: true
---

### 环境搭建介绍

<blockquote data-tool="科技兽" style="border-top: none;border-right: none;border-bottom: none;font-size: 0.9em;background: url(https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20210519013028.png) 10px 10px / 40px no-repeat rgb(31,79,137);overflow: auto;color: inherit;border-left: 0px;padding: 1.2em 2em;margin-bottom: 2em;margin-top: 2em;text-align: center;border-radius: 10px;"><p style="font-family: Optima-Regular, Optima, PingFangSC-light, PingFangTC-light, &quot;PingFang SC&quot;, Cambria, Cochin, Georgia, Times, &quot;Times New Roman&quot;, serif;text-align: justify;line-height: 26px;margin-top: 1em;margin-bottom: 0.3em;font-size: 14px;color: rgb(255, 255, 38);"><strong style="color: #fc8705;">使用工具</strong><br  />Vmware Workstation 16 Pro , Centos7</p></blockquote>

<blockquote data-tool="科技兽" style="border-top: none;border-right: none;border-bottom: none;font-size: 0.9em;background: url(https://figurebed-iseex.oss-cn-hangzhou.aliyuncs.com/img/20210519013028.png) 10px 10px / 40px no-repeat rgb(31,79,137);overflow: auto;color: inherit;border-left: 0px;padding: 1.2em 2em;margin-bottom: 2em;margin-top: 2em;text-align: center;border-radius: 10px;"><p style="font-family: Optima-Regular, Optima, PingFangSC-light, PingFangTC-light, &quot;PingFang SC&quot;, Cambria, Cochin, Georgia, Times, &quot;Times New Roman&quot;, serif;text-align: justify;line-height: 26px;margin-top: 1em;margin-bottom: 0.3em;font-size: 14px;color: rgb(255, 255, 38);"><strong style="color: #fc8705;">安装软件</strong><br  />vcs, verdi, virtuoso, vivado, dc以及一些工艺库</p></blockquote>

### Vmware

安装时选择**移动**

用户/root密码：**2020**

### Terminal

```shell
open环境文件
la
g .bashrc (tab自动补齐) --linux gvim -->环境配置

source .bashrc --source环境才起作用
```

切换VCS版本  --MX(verilog&VHDL) / VO(verilog)

> HOME路径也要修改 -- shift+* -->即修改掉代码前的注释

#### 内容展示

```shell
ls
.. --上一个目录
ll
cd cadence/

..
cd IC_lib --gtkwave不兼容

..
cd synopsys --未破解
ll 
# 安装程序,安装需要的工具
cd SynopsysInstaller_v5.0/
./setup.sh

cd vcs-mx
ll

cd Xilinx/
ll
cd vivado_lib/ --编译库
```

#### 实际操作

```shell
# 接上述代码
..
..
cd ICer/
ls
rm .rf test test1/
ls 
# 建立文件夹
mkdir test
ls
cd test/

# verdi
verdi -- open verdi --会生成一些临时文件
ls
ll

# DC --综合
dc --进入dc_shell命令行
exit

# 结合项目
操作目录 ICer
la

# cadence会和synopsys冲突
g .bashrc
添加source命令
source .cadence_bashrc -- 切换cedence
source .bashrc
cd test/
virtuoso&

cd ~  --切换回来
g .bashrc
source .bashrc

..
cd ic_prjs/
ll

cd heart/
cd sim/
g Makefile
make clean
ls
make vcs
make verdi

# 打开了verdi
选信号 ctrl+w 看波形

..
cd breath_led/
ll
cd verification/
ls
g Makefile
make vcs
make verdi
# 打开了verdi 左键选信号，中间拖

make clean
ls
..
cd fpga/
cd constraint/
..
cd libs/
..
cd script/
..
cd work/
make clean
ls
g Makefile
make built

#open new tab
ctrl+shift+t
ls --验证环境
cd ic_prjs/
cd iic_slave/
ls
source bashrc.env
ls
cd verification/
cd regress_fun/
g Makefile 
make abc --abc is case , 进行仿真，有点像UVM
cd VCS_SLV_test/
open_verdi --加载波形文件
make open --启动vivado    
```

