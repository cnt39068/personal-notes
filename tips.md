# 各种技巧
## Windows 10
删除内置应用
系统管理员权限打开PowerShell
```
OneNote：
Get-AppxPackage *OneNote* | Remove-AppxPackage

3D打印：
Get-AppxPackage *3d* | Remove-AppxPackage

Camera相机：
Get-AppxPackage *camera* | Remove-AppxPackage

邮件和日历：
Get-AppxPackage *communi* | Remove-AppxPackage

新闻订阅：
Get-AppxPackage *bing* | Remove-AppxPackage

Groove音乐、电影与电视：
Get-AppxPackage *zune* | Remove-AppxPackage

人脉：
Get-AppxPackage *people* | Remove-AppxPackage

手机伴侣(Phone Companion)：
Get-AppxPackage *phone* | Remove-AppxPackage

照片：
Get-AppxPackage *photo* | Remove-AppxPackage

纸牌游戏：
Get-AppxPackage *solit* | Remove-AppxPackage

录音机：
Get-AppxPackage *soundrec* | Remove-AppxPackage

Xbox：
Get-AppxPackage *xbox* | Remove-AppxPackage
```

需要提醒大家的是，当执行Xbox删除命令后，会跳出一大段错误提示，我们不必理会，实际上Xbox应用已经成功删除了。
 
如果想一次性删除所有预装应用是否可以呢？答案是肯定的！命令如下：
 
    Get-AppxPackage -AllUsers | Remove-AppxPackage
 
注意：当我们新建一个账户后，预装的应用就会被重新安装，不过我们可以通过下面的命令来避免这一情况的发生。
 
    Get-AppXProvisionedPackage -online | Remove-AppxProvisionedPackage –online
 
是不是感觉删除预装程序也是非常简单的呢？如果你也有系统洁癖，那就行动起来吧！

玩转正版Windows10系统，请锁定专注Win10内容阅读体验的Windows10之家！

From <http://www.iwin10.com/jiaocheng/885.html> 

## Linux之自建KMS服务器实现激活Windows 7、8、10等系统
摘要
人人都可搭建自己的KMS服务器来激活 windows 10 8.1 8 7 2008 2012等众多系统版本，这不是什么难事，在Linux上实现照样很简单。
### Linux服务器上自建KMS服务器
```
01  wget https://www.dwhd.org/wp-content/uploads/2015/07/vlmcsd-svn812-2015-08-30-Hotbird64.zip
02  #http://forums.mydigitallife.info/threads/50234-Emulated-KMS-Servers-on-non-Windows-platforms
03  unzip -q vlmcsd-svn812-2015-08-30-Hotbird64.zip -d /usr/local/
04  ln -sv /usr/local/vlmcsd-svn812-2015-08-30-Hotbird64/ /usr/local/KMS
05  echo "export PATH=/usr/local/KMS/binaries/Linux/intel/static:\$PATH" > /etc/profile.d/vlmcs.sh
06  source /etc/profile.d/vlmcs.sh
07  chmod +x /usr/local/KMS/binaries/Linux/intel/static/*
08  echo "vlmcsd-x64-musl-static" >> /etc/rc.local
09  vlmcsd-x64-musl-static
10  #记得防火墙开放TCP的1688端口和关闭SELinux
11  #下面是快速即时生效+永久关闭SELinux的命令
12  sed -i 's/^SELINUX=.*/#&/;s/^SELINUXTYPE=.*/#&/;/SELINUX=.*/a SELINUX=disabled' /etc/sysconfig/selinux && /usr/sbin/setenforce 0
```

### 激活方法
管理员权限运行CDM #:示例激活Windows 10 Professional
```
01  Windows PowerShell
02  版权所有 (C) 2015 Microsoft Corporation。保留所有权利。
03   
04  PS C:\WINDOWS\system32> slmgr.vbs -upk
05  PS C:\WINDOWS\system32> slmgr.vbs -ipk W269N-WFGWX-YVC9B-4J6C9-T83GX
06  PS C:\WINDOWS\system32> slmgr.vbs -skms kms.dwhd.org
07  PS C:\WINDOWS\system32> slmgr.vbs -ato
08  PS C:\WINDOWS\system32> slmgr.vbs -dlv
09  PS C:\WINDOWS\system32>
10   
11  #kms.dwhd.org换成自己对应的服务器IP或者域名
```
下面提供Windows 10 全版本自动KMS激活脚本
下载：[Win10_KMS_Activation.bat | https://www.dwhd.org/20150723_011447.html#button_file]

### 下面提供各种版本的KMS KEY
KEY来源：https://technet.microsoft.com/en-us/library/jj612867.aspx
```
01  OPERATING SYSTEM EDITION                                KMS CLIENT SETUP KEY
02  #############################  Windows 2016 ########################################
03  Windows Server 2016 RTM Datacenter/DatacenterCore        CB7KF-BWN84-R7R2Y-793K2-8XDDG
04  Windows Server 2016 RTM Standard/StandardCore            WC2BQ-8NRM3-FDDYY-2BFGV-KHKQY
05  #############################  Windows  10  ########################################
06  Windows 10 Professional                                    W269N-WFGWX-YVC9B-4J6C9-T83GX
07  Windows 10 Professional N                                MH37W-N47XK-V7XM9-C7227-GCQG9
08  Windows 10 Enterprise                                    NPPR9-FWDCX-D2C8J-H872K-2YT43
09  Windows 10 Enterprise N                                    DPH2V-TTNVB-4X9Q3-TJR4H-KHJW4
10  Windows 10 Education                                    NW6C2-QMPVW-D7KKK-3GKT6-VCFB2
11  Windows 10 Education N                                    2WH4N-8QGBV-H22JP-CT43Q-MDWWJ
12  Windows 10 Enterprise 2015 LTSB                            WNMTR-4C88C-JK8YV-HQ7T2-76DF9
13  Windows 10 Enterprise 2015 LTSB N                        2F77B-TNFGY-69QQF-B8YKP-D69TJ
14   
15  #############################  Windows  8.1 2012R2  #################################
16  Windows 8.1 Professional                                GCRJD-8NW9H-F2CDX-CCM8D-9D6T9
17  Windows 8.1 Professional N                                HMCNV-VVBFX-7HMBH-CTY9B-B4FXY
18  Windows 8.1 Enterprise                                    MHF9N-XY6XB-WVXMC-BTDCT-MKKG7
19  Windows 8.1 Enterprise N                                TT4HM-HN7YT-62K67-RGRQJ-JFFXW
20  Windows Server 2012 R2 Server Standard                    D2N9P-3P6X9-2R39C-7RTCD-MDVJX
21  Windows Server 2012 R2 Datacenter                        W3GGN-FT8W3-Y4M27-J84CP-Q3VJ9
22  Windows Server 2012 R2 Essentials                        KNC87-3J2TX-XB4WP-VCPJV-M4FWM
23   
24  #############################  Windows  8 2012  ######################################
25  Windows 8 Professional                                    NG4HW-VH26C-733KW-K6F98-J8CK4
26  Windows 8 Professional N                                XCVCF-2NXM9-723PB-MHCB7-2RYQQ
27  Windows 8 Enterprise                                    32JNW-9KQ84-P47T8-D8GGY-CWCK7
28  Windows 8 Enterprise N                                    JMNMF-RHW7P-DMY6X-RF3DR-X2BQT
29  Windows Server 2012                                        BN3D2-R7TKB-3YPBD-8DRP2-27GG4
30  Windows Server 2012 N                                    8N2M2-HWPGY-7PGT9-HGDD8-GVGGY
31  Windows Server 2012 Single Language                        2WN2H-YGCQR-KFX6K-CD6TF-84YXQ
32  Windows Server 2012 Country Specific                    4K36P-JN4VD-GDC6V-KDT89-DYFKP
33  Windows Server 2012 Server Standard                        XC9B7-NBPP2-83J2H-RHMBY-92BT4
34  Windows Server 2012 MultiPoint Standard                    HM7DN-YVMH3-46JC3-XYTG7-CYQJJ
35  Windows Server 2012 MultiPoint Premium                    XNH6W-2V9GX-RGJ4K-Y8X6F-QGJ2G
36  Windows Server 2012 Datacenter                            48HP8-DN98B-MYWDG-T2DCC-8W83P
37   
38  #############################  Windows  7 2008R2  ####################################
39  Windows 7 Professional                                    FJ82H-XT6CR-J8D7P-XQJJ2-GPDD4
40  Windows 7 Professional N                                MRPKT-YTG23-K7D7T-X2JMM-QY7MG
41  Windows 7 Professional E                                W82YF-2Q76Y-63HXB-FGJG9-GF7QX
42  Windows 7 Enterprise                                    33PXH-7Y6KF-2VJC9-XBBR8-HVTHH
43  Windows 7 Enterprise N                                    YDRBP-3D83W-TY26F-D46B2-XCKRJ
44  Windows 7 Enterprise E                                    C29WB-22CC8-VJ326-GHFJW-H9DH4
45  Windows Server 2008 R2 Web                                6TPJF-RBVHG-WBW2R-86QPH-6RTM4
46  Windows Server 2008 R2 HPC edition                        TT8MH-CG224-D3D7Q-498W2-9QCTX
47  Windows Server 2008 R2 Standard                            YC6KT-GKW9T-YTKYR-T4X34-R7VHC
48  Windows Server 2008 R2 Enterprise                        489J6-VHDMP-X63PK-3K798-CPX3Y
49  Windows Server 2008 R2 Datacenter                        74YFP-3QFB3-KQT8W-PMXWJ-7M648
50  Windows Server 2008 R2 for Itanium-based Systems        GT63C-RJFQ3-4GMB6-BRFB9-CB83V
51   
52  #############################  Windows  Vista 2008 ####################################
53  Windows Vista Business                                    YFKBB-PQJJV-G996G-VWGXY-2V3X8
54  Windows Vista Business N                                HMBQG-8H2RH-C77VX-27R82-VMQBT
55  Windows Vista Enterprise                                VKK3X-68KWM-X2YGT-QR4M6-4BWMV
56  Windows Vista Enterprise N                                VTC42-BM838-43QHV-84HX6-XJXKV
57  Windows Web Server 2008                                    WYR28-R7TFJ-3X2YQ-YCY4H-M249D
58  Windows Server 2008 Standard                            TM24T-X9RMF-VWXK6-X8JC9-BFGM2
59  Windows Server 2008 Standard without Hyper-V            W7VD6-7JFBR-RX26B-YKQ3Y-6FFFJ
60  Windows Server 2008 Enterprise                            YQGMW-MPWTJ-34KDK-48M3W-X4Q6V
61  Windows Server 2008 Enterprise without Hyper-V            39BXF-X8Q23-P2WWT-38T2F-G3FPG
62  Windows Server 2008 HPC                                    RCTX3-KWVHP-BR6TB-RB6DM-6X7HP
63  Windows Server 2008 Datacenter                            7M67G-PC374-GR742-YH8V4-TCBY3
64  Windows Server 2008 Datacenter without Hyper-V            22XQ2-VRXRG-P8D42-K34TD-G3QQC
65  Windows Server 2008 for Itanium-Based Systems            4DWFP-JF3DJ-B7DTH-78FJB-PDRHK
```

### 人人都可搭建自己手机的 KMS 服务器 激活 windows 10 (含 Mac Linux Win 搭建方法)
TBD
