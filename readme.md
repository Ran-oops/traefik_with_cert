
本项目是使用mkcert+trafic+fastapi+docker compose实现https安全访问

0. 创建证书
    ```txt
    # mkcert installation is here: https://github.com/FiloSottile/mkcert
    scoop bucket add extras
    scoop install mkcert
    mkcert -key-file certs/key.pem -cert-file certs/cert.pem m.local *.m.local
    mkcert -install
    ```
    [参考链接一](https://github.com/pplmx/LearningDocker/tree/main/compose/traefik/self-signed)
    [参考链接二](https://github.com/FiloSottile/mkcert)

1. 方法一：在本地起项目(此时不是https访问)：
    ```txt
    pip install fastapi
    uvicorn main:app --reload
    ```
    可以在浏览器输入：` http://127.0.0.1:8000 `


2. 方法二：使用docker container 启动项目(此时不是https访问)：
    ```txt
    docker build -t fastapidemo .
    docker run -d -p 8080:8080 fastapidemo
    ```
    可以在浏览器输入：` http://127.0.0.1:8080 `

3. 方法三： 使用docker compose启动项目(https安全访问)
    ```txt
   docker compose up -d
    ```

4. 在hosts里面添加域名映射
    ```txt
    127.0.0.1 fastapi.m.local
    127.0.0.1 traefik.m.local
    ```
    这样就可以在浏览器里面输入`fastapi.m.local`

4. 其他一些常用的docker 命令
    ```shell
    docker compose -p jenkins down
    docker compose -p jenkins down -v
    docker compose -p portainer down -v
    docker compose -p sonar down -v
    docker container prune -f
    docker container ls -a
    docker compose ls（列出起起来的compose.yml）
    docker compose up -d
    docker logs -f relaxed_williams(查看relaxed_williams这个容器的日志)
    docker compose logs -f(查看compose.yml里面所有容器的日志)
    docker compose restart
    docker kill busy_greider(杀掉容器）
    ```




