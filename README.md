# Duet2020-EFI

联想 yoga duet 2020 的黑苹果EFI

目前适配的系统有 macOS 12.7 ，工具和镜像下载 https://www.123pan.com/s/9ZSzVv-fE7Kd.html


安装方法：  参考图文教程 https://apple.sqlsec.com/5-%E5%AE%9E%E6%88%98%E6%BC%94%E7%A4%BA/5-1/

### 一、制作安装优盘
1、找一个16GB的优盘，用管理员身份运行 balenaEtcher 软件，烧录黑果小兵出品的macOS 12.7的安装盘到优盘里。  
2、下载并解压 EFI.zip 压缩包。  
3、用 DiskGenis 软件打开优盘，打开优盘的OPENCORE分区，删除里面的EFI文件夹，再把上面下载解压的EFI文件夹粘贴进来。  

### 二、安装系统
0、按fn+F2选择优盘启动电脑，会看到电脑本身的硬盘，和优盘里的 FirePE 和 Install macOS Monterey。  
1、硬盘划分，以win10+macOS双系统为例，DiskGenis软件，磁盘>快速分区  
分区表类型GPT，分区数目2或3，创建新的ESP分区300MB，创建MSR分区  
个人参考：win10（200G），D盘（100G），macOS（200G）  
2、安装win10LTSC，在winPE里双击win10.iso盘，打开运行安装。不要用win10安装器这类软件安装，不然在bios原生的启动项里会没有win10，每次都要进opencore引导才能启动win10。  
3、安装macOS，优盘启动选择Install macOS Monterey项，进来之后选择“磁盘工具”，把要给苹果系统的分区格式化（抹掉）为APFS格式，取名叫“macOS12”，完成后左上角退出磁盘工具。  
4、然后选择“安装macOS Monterey”，选择刚才格式化好的盘，各种下一步。  
5、安装完成后会重启，然后会出现一个“macOS Installer"的盘，这个其实就是苹果的盘，选这个然后继续等待安装完成。最后安装完自动重启就可以看到“macOS12”这个盘了。  

### 三、复制引导
1、进入优盘里的FirePE系统，打开DiskGenis软件，打开电脑硬盘的EFI分区，删除原来的EFI文件夹，把优盘里EFI分区的EFI文件夹粘贴到电脑硬盘里。  
这样以后启动就不需要进入优盘了。  

### 四、修改系统序列码（可选）
1、苹果电脑有三个序列码，本EFI里预设了一套，但建议不同的电脑用不同的序列码，以免被苹果找麻烦。  
2、安装python3，解压 OCAT.zip 软件并运行，生成三个码，找到硬盘里引导分区的 EFI/OC/config.plist 文件。  
3、查找 SystemSerialNumber、 SystemUUID、 MLB 分别填入。  
