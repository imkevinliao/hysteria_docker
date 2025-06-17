# hysteria docker
起初是打算看看有没有人有现成的方案，结果没找到。找到的是 docker compose 方式启动的，好处就是自己编辑，但是我都用docker了，我就是想要一键完成那咋办？

# 使用文档
一键部署
```
PORT=12345 && docker run -d --restart=always -p $PORT:443/udp -e PORT="$PORT" --name hysteria kevinstarry/hysteria:latest  && sleep 3 && docker exec -it hysteria cat /app/info.txt
```
不想使用默认端口？自行修改 PORT=12345 改成你服务器暴露的端口，直接启动


一键移除
```
docker stop hysteria && docker rm hysteria  && docker rmi kevinstarry/hysteria:latest
```
