# qinglong-jdc-mulit-node
青龙2.8&amp;JDC多节点集成环境

# docker-compose.yaml 添加容器节点
```shell
crazyrico-ql-jdc-node3:
    container_name: crazyrico-ql-jdc-node3
    build:
      context: ./
      dockerfile: ./ql-jdc/Dockerfile
    environment:
      TZ: Asia/Shanghai
    ports:
    - "5777:5700"
    expose:
    - "5701"
    volumes:
    - ./node3/config:/ql/config
    - ./node3/log:/ql/log
    - ./node3/db:/ql/db
    - ./node3/scripts:/ql/scripts
    - ./node3/jbot:/ql/jbot
    - ./node3/jdc:/ql/jdc
    restart: always
```

# 配置节点连接
进入pubic目录 修改config.js节点url
```script
let publicnodeinfo = [
	{ "name":"京东节点1", "url":"node1" },
	{ "name":"京东节点2", "url":"node2" },
	{ "name":"京东节点3", "url":"node3" }
]
```

# nginx 配置添加节点代理
```shell
location /node3 {
    proxy_set_header Host $host;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header   X-Real-IP $remote_addr;
    proxy_pass http://crazyrico-ql-jdc-node3:5701/;
    client_max_body_size  10M;
}
```

# 启动容器
```shell
$ docker-compose up &
```
![pic.png](pic.png)

# 停止容器
```shell
$ docker-compose down
```

![mulit-node.png](mulit-node.png)
