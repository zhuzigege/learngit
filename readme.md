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
 - import_mysql.sh 针对存在分表情况的数据入库，目前暴力从各分表获取数据并load到hive  
 usage：import_mysql.sh [task_name] [task_date]  
 参数说明：config_import_muysql文件夹包含当前所有mysql入库任务参数，task_name参数与改文件夹的文件是对应的。  
 - sqoop_import_hue.sh 封装采用sqoop import入库的方法，入库更高效稳定  
     usage：sqoop_import.sh [task_name] [task_date]  
     
2. ck入库
3. hive计算
4. mysql出库
5. 日志告警






