# hysteria docker
没有找到别人的一键启动方案，有的都是 docker-compose 配置后启动。

我都用 docker 了，还要搞这么多那还是用别人的脚本叭。

我不喜欢用脚本的原因就是容易把服务器搞脏，而docker可以保证你在科学上网同时，完全不影响服务器使用。

hysteria 使用 udp 看运营商 和 VPS提供商 是否封禁，建议辅 reality（docker）：https://github.com/imkevinliao/xray_reality_docker
# 使用文档
部署docker（已经准备好了则忽略）
```
curl -fsSL get.docker.com -o get-docker.sh && sh get-docker.sh
```

部署hysteria （不想使用默认端口？自行修改 PORT=12346 改成你服务器暴露的端口）
```
PORT=12346 && docker run -d --restart=always -p $PORT:443/udp -e PORT="$PORT" --name hysteria kevinstarry/hysteria:latest  && sleep 3 && docker exec -it hysteria cat /app/info.txt
```

一键移除
```
docker stop hysteria && docker rm hysteria  && docker rmi kevinstarry/hysteria:latest
```
# 了解更多
hysteria version：v2.6.2

查看链接（自动获取ipv4然后生成链接）：docker exec -it hysteria cat /app/info.txt

自签证书设置的 36500 天（没有人真的会用十年吧）

cert: /app/server.pem

key: /app/server.key

密码证书都是自动生成的，本来想弄成密码可以指定的，但是感觉还是随机生成好，懒人不想思考
