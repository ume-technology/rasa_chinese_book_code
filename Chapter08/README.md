### Rasa 版本和项目依赖以及训练模型
```shell script
    Rasa 3.0.X
    Rasa 3.3.0
    pip install --no-deps -r ../full_requirements.txt
    - 安装 redis
    - 安装 docker：基于docker安装redis；https://www.docker.com/ 
    - 拉取 redis 的 docker 镜像：docker pull redis:6.2.5
    - 运行 redis：docker run --rm -p 6379:6379 --name docker-redis redis:6.2.5
    - 训练 Rasa 模型：rasa train
```

### 运行SDK微服务
```shell script
    - 为了和多 worker 模式下的 Rasa 服务器比较性能，使用 CUDA_VISIBLE_DEVICES=-1 设置；将模型加载到 CPU 上（而不是 GPU）：CUDA_VISIBLE_DEVICES=-1 rasa run --endpoints ./endpoints_default.yml
    - 运行动作服务器: rasa run actions
    - 以多worker的形式运行 Rasa：
      - rasa服务器：CUDA_VISIBLE_DEVICES=-1 SANIC_WORKERS=5 rasa run
      - action服务器：ACTION_SERVER_SANIC_WORKERS=5 rasa run actions
```

### JMeter 测试
```shell script 
    测试文件是 RasaPerformance.jmx (软件 Apache JMeter 5.4.1);默认模式的性能如下图：
```
![](media/SingleWorkerGraphResults.png)
多 woker 模式下的性能：
![](media/MultipleWorkerTestResults.png)
