"# My first git" 
H Company Using Git by Proxy 

- 第一步解决网络代理的问题 
  - git proxy
  - git config --local -l 
  - git config --local http
- 因为H公司的代理。。 需要使用cntlm 来进行代理转换
  - cntlm 内网代理外网说明
    - D:\>net start cntlm
      服务无法启动---Windows 下计算机管理中的系统日志-应用程序日志，网上搜索，应该是cntlm 使用的非默认安装路径导致的，需要同步修改注册表信息
    - HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\cntlm\Parameters 下的AppArgs -f 修改为：-f -c "/cygdrive/D/_WorkEnv/Cntlm/cntlm.ini"
    - net start cntlm | net stop cntlm 
  - Cntlm Config Information
    公司的不同的代理对于 NTLM的支持不一样
  - 执行命令：cntlm -v -c cntlm.ini -M http://www.baidu.com
  - 前提：对安装路径下的cntlm.ini 文件进行配置，不需要的删除如password 
  - 然后将生成的Profile 中如下：
    ----------------------------[ Profile  1 ]---------- 
    Auth    NTLM 
    PassNT
    PassLM 
  - 然后需要将生成的相关信息放入cntlm.ini 下的 PassNTLMv2下
    测试IE下的代理指向 127.0.0.1 3128 (port 在ini文件中指定)

解决使用GIT通过Proxy

git config --global -l 全局的变量配置

git config --local http.proxy http://username:password@proxy:port

git config --local https.proxy  http://username:password@proxy:port

git config --local http.sslVerify false (关闭SSL验证)

然后使用git config --local -l 查看相关git 配置 

git clone https://github.com/wwdgd1983/StackEdit.git
