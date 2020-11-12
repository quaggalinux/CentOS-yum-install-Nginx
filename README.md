# CentOS-yum-install-Nginx
CentOS7或8用标准yum方式安装Nginx最新版   
      
好多玩家喜欢CentOS,说是喜欢它的稳定,但是不得不承认CentOS安装大部分的流行软件都不是那么顺畅,如果使用系统的yum方式安装,要么不是最新版,又或者干脆就没有     
           
这不,有玩家要在CentOS上安装Nginx,玩玩这个高性能,多功能的web服务器,发现用标准yum方式安装,结果是令人惊叹的,在CentOS 7上yum安装的版本是1.16,在CentOS 8上yum安装的版本居然是1.14,不知为什么倒回去了,有些玩家会发现即使用1.16版,使用一些高级功能都会出现各种问题,在其他linux发行版上一般都会标准安装出1.18版的Nginx,这个1.18版本就解决了好些问题            
          
那些个玩家们肯定是钻研好学的,找度娘叉半天,都是个怎么在CentOS上编译调试最新版Nginx的教程,草泥马...有这本事,早就不找度娘,自撸去了       
      
有没有使用标准yum方式在CentOS7或8上几键安装最新版Nginx的方法呢? 小白,对,说的就是你 o(≧v≦)o      
      
怎么又是我 ( ´•︵•` )  ,好吧,梳碧湖的砍柴人掏出了缺口柴刀            
        
首先转用root用户更新系统及安装编辑软件          
         
$su          
#yum -y update               
#yum -y install make        
#yum -y install curl           
#yum -y install wget             
#yum -y install nano             
          
然后安装为“红帽系”的操作系统提供额外的软件包命令,确保可以安装一个额外的软件包        
         
#yum -y install epel-release         
        
安装一个额外的软件包做验证,如果下面的安装命令找不到程序包,不知什么原因,恭喜你的系统中奖了,一定要重装系统!!!        
       
#yum -y install htop       
         
如果上面的包能够安装就继续下面命令           
      
安装 yum-utils       
       
#yum -y install yum-utils         
      
新建nginx的repo源       
        
#touch /etc/yum.repos.d/nginx.repo      
       
编辑nginx.repo 文件          
         
#nano /etc/yum.repos.d/nginx.repo       
        
------CentOS 7需要在文件里面写入以下内容,如果文件原来有内容需要全部删除内容再把下面内容粘贴进去       
       
[nginx-stable]          
name=nginx stable repo        
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/       
gpgcheck=1        
enabled=1         
gpgkey=https://nginx.org/keys/nginx_signing.key       
       
[nginx-mainline]          
name=nginx mainline repo       
baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/       
gpgcheck=1         
enabled=0       
gpgkey=https://nginx.org/keys/nginx_signing.key         
       
保存并退出         
         
------CentOS 8需要在文件里面写入以下内容,比CentOS 7多一些,没有这些多出的内容,CentOS 8仍然会安装回1.14版,如果文件原来有内容需要全部删除内容再把下面内容粘贴进去      
    
[nginx-stable]          
name=nginx stable repo       
baseurl=http://nginx.org/packages/centos/$releasever/$basearch/         
gpgcheck=1        
enabled=1         
gpgkey=https://nginx.org/keys/nginx_signing.key         
module_hotfixes=true          
       
[nginx-mainline]        
name=nginx mainline repo       
baseurl=http://nginx.org/packages/mainline/centos/$releasever/$basearch/       
gpgcheck=1         
enabled=0       
gpgkey=https://nginx.org/keys/nginx_signing.key         
module_hotfixes=true         
       
保存并退出         
       
安装nginx       
     
#yum -y install nginx        
       
安装完成后检查Nginx的版本是否1.18或更高       
        
#nginx -v         
     


