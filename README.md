# hdmagic
Tool that help you with manage your database

截止目前，安装、备份、恢复、同步、ddl备份恢复等已经全面支持GP6版本！！！！！！    

！！！【在5.20.0和5.20.1版本上暂时无法使用gpmcbackup命令，因为存在Utility模式COPY问题，BUG】！！！ 
【目前已经修改代码，不带条件可以使用】
【最新的版本不能直接替换以前的版本，因为日志文件格式发生了变化】
Master的备份目录下的last_stat.tag文件需要为每一行追加;.gz

使用备份恢复命令，请将  
gpddlbackup  
gpddlrestore  
gpmcbackup  
gpmcrestore  
四个文件直接拷贝到$GPHOME/bin/目录下，修改owner为gpadmin和mod为755：  
[gpadmin@mdw ~]$ cd $GPHOME/bin  
[gpadmin@mdw bin]$ chown gpadmin. gp{mc,ddl}*  
[gpadmin@mdw bin]$ chmod 755 gp{mc,ddl}*  
使用说明可以参考命令的help信息和word文档  
gpddlbackup已经经过较大范围验证，欢迎试用  

！！！【不能使用gpdbtransfer以5.20.0和5.20.1作为源端，因为存在Utility模式COPY问题，BUG】！！！ 
【目前已经修改代码，不带条件可以使用】
使用跨集群数据传输命令，请将  
gpdbtransfer  
文件直接拷贝到$GPHOME/bin/目录下，修改owner为gpadmin和mod为755：  
[gpadmin@mdw ~]$ cd $GPHOME/bin  
[gpadmin@mdw bin]$ chown gpadmin. gpdbtransfer  
[gpadmin@mdw bin]$ chmod 755 gpdbtransfer  
使用说明可以参考命令的help信息或readme目录中查看  

gpdbcluster命令目前已经经过全面重构、逻辑上更加清晰和严谨、欢迎试用    
#建议慎重用于生产环境    
#目前已经强化了Standby激活的逻辑，如果无法判断Master的状态就不切换，    
#因为，如果gpactivatestandby命令本身也无法判断Master状态的话，    
#可能会出现Master和Standby都活着的冲突状态，
#目前进行了进一步强化，常规的Master状态判断使用pg_sleep进行长时间保持，    
#如果第一次检测到异常，将会马上再进行3次简单测试，只有4次都异常才认为Master访问异常，   
#这一机制的完善主要用于避免可能出现检测SQL被误杀的情况，    
#对于出现连接数超过限制的情况，将认为数据库状态是正常的，不会予以切换


    
