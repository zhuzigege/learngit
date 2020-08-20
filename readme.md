## 目录
1. 介绍
2. 各模块功能说明

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
 针对存在分表情况的数据入库，目前暴力从各分表获取数据并load到hive  
 usage：import_mysql.sh [task_name] [task_date]  
 说明：config_import_muysql文件夹包含当前所有mysql入库任务参数，task_name参数与该文件夹的文件是对应的。  
 - sqoop_import_hue.sh  
    封装采用sqoop import入库的方法，入库更高效稳定  
     usage：sqoop_import.sh [task_name] [task_date]  
     
2. ck入库
 - 基于python读取ck服务接口的方式（比较耗时，已经停止）
 - 采用基于Flink的方案  
 usage：import_ck_flink.sh [task_name] [task_date]  
 说明：目前CK入库的任务参数存放在mysql中的flink_job_ods_param中
 
3. hive计算
 - 基于hue的HIVE Server2 Action  
    只需配置要运行的hql脚本，具体配置参考Hue上已配置的任务  
 - hive_excute_hue.sh  
 使用shell封装对hive-sql的执行，该封装能自动检查当前hive任务的依赖，并能使用使用各种时间参数（hue上每个时间参数都需要配置）  
 usage：hive_excute_hue.sh [task_name] [task_date]  
 说明：hql脚本都在hql文件夹内，task_name与文件夹内的文件对应；  
 关于使用时间参数：传入task_date，脚本默认可以使用对应task_date的相对日期参数，具体参考脚本和param/param_date_day.param文件  
 
4. mysql出库  
 - sqoop_export.sh
 usage：sqoop_export.sh [task_name] [task_date]  
 
 
5. 日志告警  
- 日志工具  
task_log.sh：
- task_monitor.sh 每小时短信发送当天的任务的运行情况
- task_monitor_realtime.sh 






