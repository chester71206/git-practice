 1. instance 的 public IP: 52.63.69.186
 2. 什麼是 instance type? : 指的是你創建instance之後配置什麼樣的規格，規格越好價格越貴。
 3. 什麼是 Nginx？有哪些用途與特性？ : Nginx最主要是一個Web Server 處理HTTP請求，回應對應的內容。 也可以當作一種Reverse Proxy(反向代理伺服器) 將 client 的請求送到後端 並把回應結果傳回client
 4. pm2 套件是什麼？有什麼用處？ : PM2是為node js設計的 process manager，可以在背景執行程式，當程式崩潰或壞掉的時候也會自動重啟，並且所有問題或輸出都可以在log檔查到，方便debug
 5. 步驟 9 中提到的 proxy 是什麼意思？為什麼要透過 Nginx 來 proxy 到 Express 開發的 Web Server? : proxy是一個中間人，在server和client之間轉發請求，分為Forward Proxy和Reverse Proxy，Forward Proxy代表客戶端發出請求，Reverse Proxy則是站在伺服器這端接受外面的請求，再將這些請求傳到後端。Nginx是一個Reverse Proxy，若是透過Reverse Proxy的方式，可以隱藏後端伺服器的真實 IP ，真強安全性

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
7.Security Group 是什麼？用途為何？有什麼設定原則嗎？: Security Group是一種雲端防火牆，控制網路流量的進出，比方說特定 IP才可以進入
Security Group 的設定原則:最小權限原則，若是只提供http服務，就應該將其他的端口關閉

8.什麼是 sudo? 為什麼有的時候需要加上 sudo，有時候不用？ : 需要系統級別的操作就需要sudo，例如安裝軟體，或是牽涉系統資源管理的時候，但如果是編輯文件、跑python程式碼就不用

9.Nginx 的 Log 檔案在哪裡？你怎麼找到的？怎麼看 Nginx 的 Log？ :  Log檔在 /var/log/nginx/  ，可以用tail(顯示最後幾個log) 或是cat(整個) 或是grep(找特定的字串或時間)
10.無
11. https://tw.alphacamp.co/blog/nginx
    https://medium.com/learn-or-die/%E5%A5%BD-pm2-%E4%B8%8D%E7%94%A8%E5%97%8E-fc7434cc8821
    
  
