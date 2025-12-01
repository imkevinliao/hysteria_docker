# hysteria docker
没有找到别人的一键启动方案，有的都是 docker-compose 配置启动，当然他们都配置了SSL，可是我都用docker了，还是嫌麻烦，自签证书也不是不能用，是吧。

我不喜欢用脚本的原因就是容易把服务器搞脏，我甚至不希望在宿主机上留下任何痕迹文件（配置文件）

hysteria 使用 udp 看运营商 和 VPS提供商 是否封禁，建议辅 reality（docker）：https://github.com/imkevinliao/xray_reality_docker
# 使用文档
部署docker（已经准备好了则忽略）
```
curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh
```

部署hysteria (指定端口PORT=XXXX)
```
PORT=12345 && docker run -d --restart=always -p $PORT:443/udp -e PORT="$PORT" --name hysteria kevinstarry/hysteria:latest && sleep 3 && docker exec -it hysteria cat /app/info.txt
```
一键移除
```
docker stop hysteria && docker rm hysteria  && docker rmi kevinstarry/hysteria:latest
```
# 了解更多
hysteria version：v2.6.5

查看链接：docker exec -it hysteria cat /app/info.txt

自签证书设置的 36500 天（没有人真的会用一百年吧）

cert: /app/server.pem

key: /app/server.key

密码证书都是随机自动生成的，V3.0版本增加了二维码，方便直接扫码导入，linux镜像从alpine:latest换成了debian:bookworm-slim。
