 1. instance 的 public IP: 52.63.69.186
 2. 什麼是 instance type? : 指的是在 AWS EC2 中你配置什麼樣的規格
 3. 什麼是 Nginx？有哪些用途與特性？ : Nginx最主要是一個Web Server 處理HTTP請求，回應對應的內容。 也可以當作一種Reverse Proxy(反向代理伺服器) 將 client 的請求送到後端 並把回應結果傳回client
 4. pm2 套件是什麼？有什麼用處？ : PM2是為node js設計的 process manager
 5. 步驟 9 中提到的 proxy 是什麼意思？為什麼要透過 Nginx 來 proxy 到 Express 開發的 Web Server? : proxy是一個中間人，在server和client之間轉發請求，分為Forward Proxy和Reverse Proxy，Forward Proxy代表客戶端發出請求，Reverse Proxy則是站在伺服器這端接受外面的請求



6. 在 readme 中提供步驟 9 的 Nginx 設定檔:
server {
    listen 80;

    server_name your-domain-or-public-ip;

    location / {
        proxy_pass http://localhost:3000;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}









11. https://tw.alphacamp.co/blog/nginx
    https://medium.com/learn-or-die/%E5%A5%BD-pm2-%E4%B8%8D%E7%94%A8%E5%97%8E-fc7434cc8821
    
  
