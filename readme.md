## 目录
1. 介绍
2. 各模块功能说明
3. 部署

## <a name="module">一、介绍</a>
1. 应用于推荐场景的数据仓库建设项目，包含各类任务的抽象封装，以及具体任务的参数配置（主要存储在mysql表中和以config开头的文件夹中）。
2. 项目包含日志、依赖、任务监控模块，能对任务的运行情况进行监控和管理。
3. 作业类型：
 - mysql入库
 - ck入库
 - hive计算
 - mysql 出库

## <a name="module">二、各模块功能</a>
1. mysql入库  
 - import_mysql.sh  
 usage：import_mysql.sh [task_name] [task_date]  
 针对存在分表情况的数据入库，目前暴力从各分表获取数据并load到hive。config_import_muysql文件夹包含当前所有mysql入库任务参数，task_name参数与该文件夹内的文件是对应的。  
 - sqoop_import_hue.sh  
     usage：sqoop_import.sh [task_name] [task_date]  
     封装采用sqoop import入库的方法，入库高效稳定  
     
2. ck入库
 - 基于python读取ck服务接口的方式（比较耗时，已经停止，目前备份到bak文件夹）
 - import_ck_flink.sh  
 usage： [task_name] [task_date]  
 采用基于Flink的方案。目前CK入库的任务参数存放在mysql中的flink_job_ods_param中
 
3. hive计算
 - 基于hue的HIVE Server2 Action  
    只需配置要运行的hql脚本，具体配置参考Hue上已配置的任务  
 - hive_excute_hue.sh   
 usage：hive_excute_hue.sh [task_name] [task_date]  
 使用shell封装对hive-sql的执行，该封装能自动检查当前hive任务的依赖，并能使用使用各种时间参数（hue上每个时间参数都需要配置）。hql脚本都在hql文件夹内，task_name与文件夹内的文件对应。    
 关于使用时间参数：传入task_date，脚本默认可以使用对应task_date的相对日期参数，具体参考脚本和param/param_date_day.param文件  
 
4. mysql出库  
 - sqoop_export.sh  
 usage：sqoop_export.sh [task_name] [task_date]  
 
 
5. 日志告警  
- task_log.sh   
日志工具，以上各类型任务都使用task_log来汇报记录任务的执行情况，任务状态有：init、waitting、running、success、fail
- task_monitor.sh  
每小时短信发送当天的任务的运行情况（当有任务失败时）
- task_monitor_realtime.sh   
短信告警近10分钟内失败、等待超时、运行超时的任务
- hive_control.sh
在hue上配置hive任务，用于检查依赖的任务是否执行成功


## <a name="module">三、部署</a>
- crontab：mysql入库、ck入库
- hue：hive计算、mysql出库
    具体任务的配置方法请参考hue上的任务






