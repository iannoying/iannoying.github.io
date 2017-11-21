---
layout: post
title: Spark based python/scala in jupyter notebook 
---

1. 安装 jupyter

   ```
   pip install --upgrade pip
   pip install jupyter
   ```

2. 配置文件

   - 生成配置文件

     ```
     jupyter notebook --generate-config
     ```

     生成的配置文件为  ~/.jupyter/jupyter_notebook_config.py

   - 编辑配置文件，加入

     ```
     c.NotebookApp.ip = '*'  # * 替换成服务器的 ip 地址
     c.NotebookApp.open_browser = False
     ```

   - 当然也可以加入密码，打开 notebook 时要求输入密码；

     打开 ipython

     ```
     In [1]: from notebook.auth import passwd
     In [2]: passwd()
     Enter password:
     Verify password:
     Out[2]: 'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed'
     ```

     在 ~/.jupyter/jupyter_notebook_config.py 中加入一行

     ```
     c.NotebookApp.password = u'sha1:67c9e60bb8b6:9ffede0825894254b2e042ea597d771089e11aed'
     ```

3. pyspark

   - 在 ~/.bashrc 加入以下内容，并使配置生效

     ```
     export PYSPARK_DRIVER_PYTHON=jupyter 
     export PYSPARK_DRIVER_PYTHON_OPTS="notebook"
     ```

     执行 pyspark 后即可

4. ```
   pip install toree   # 安装toree包
   jupyter toree install --spark_home=$SPARK_HOME  # 用户jupyter配置Apache Toree
   jupyter toree install --spark_home=$SPARK_HOME --interpreters=Scala,PySpark,SparkR,SQL
   jupyter toree install --interpreters=PySpark
   or
   jupyter toree install --spark_home=$SPARK_HOME --interpreters=PySpark
   ```

5. 最后执行 jupyter notebook 即可

