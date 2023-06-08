# 如何建立 prebid docker 環境
1. 建立image
```
docker build -t mctw_prebid:latest .
```

2. clone prebid
```
git clone https://github.com/mimicex/pyhon-prebid-docker.git
```

3. run container
 ```
docker run -it \
--name mctw_prebid \
-p 9002:9002 \
-d mctw_prebid:latest start
 ```
