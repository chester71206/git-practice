 一開始進去的時候先看到Haha, I am the fake web server. Try to find the real web server!
![image](https://github.com/user-attachments/assets/8420d254-9412-4529-9040-322a164d616b)
然後我就想說開nginx看看，發現無法啟動
![image](https://github.com/user-attachments/assets/bc1f5c34-e3d3-48d9-ae09-29efa92f9695)
因此我去看了nginx的設定檔
發現worker_connections 768;; 多了一個分號
改完之後我就 sudo systemctl restart nginx讓nginx重啟
接下來群組有人提到防火牆的問題
我就去看了防火牆
裡面有一條是1    40 REJECT     6    --  *      *       0.0.0.0/0            0.0.0.0/0            tcp dpt:80 reject-with icmp-port-unreachable
也就是拒絕80端口（HTTP）的TCP流量
因此我用了sudo iptables -D INPUT 1來解決這個問題
我發現問題仍未解決
![image](https://github.com/user-attachments/assets/c17d1d3b-169f-46ed-ad54-a78a10b175d3)
因此可能是有人佔用了80端口，我用了sudo ss -tuln | grep :80這個指令來檢查
![image](https://github.com/user-attachments/assets/7a51ffd0-f2b9-4996-837f-6b9ee1e6745d)
然後我就把他kill掉
接下來我重新curl localhost
發現以下情況
![image](https://github.com/user-attachments/assets/d7c7985b-d820-4b9b-aa8d-ed1d682c8be7)
然後老師上課突然提到說硬碟滿的事情，因此我就檢查容量情況，發現爆滿了，我就把裡面四個大檔案zip起來，解決檔案大小問題
sudo gzip /var/log/system/largefile1
最後我去看了/etc/nginx/sites-enabled的default 發現有權限問題
因此我去更改了我的權限，最後就顯示成功了!
![image](https://github.com/user-attachments/assets/5f977aee-a04d-48ea-a532-094a70700197)
![image](https://github.com/user-attachments/assets/ecf49e64-e894-4fe6-a704-a07897a42b62)


