## 1. Instance 的 Public IP
- **Public IP**: `52.63.69.186`

---

## 2. 什麼是 Instance Type?
- **解釋**: 指的是你創建雲端實例（instance）之後所選擇的硬體規格，如 CPU、記憶體等。規格越高、性能越好，價格也越貴。

---

## 3. 什麼是 Nginx？有哪些用途與特性？
- **解釋**: 
  - Nginx 最主要是一個 Web Server，主要用來處理 HTTP 請求，回應對應的靜態或動態內容。
  - 也可以作為一個 **Reverse Proxy（反向代理伺服器）**，將 client 的請求轉發到後端伺服器（如 Node.js 的 Express 伺服器），再將後端回應結果傳回 client。
  - Nginx 還支援負載均衡、高效靜態資源處理等功能。

---

## 4. PM2 套件是什麼？有什麼用處？
- **解釋**: 
  - PM2 是一個為 Node.js 設計的 **Process Manager**。
  - 可以在背景執行程式，當程式崩潰時自動重啟，確保應用穩定運行。
  - 支援日誌管理，所有問題或輸出都可以在日誌檔案中查到，方便調試和追蹤。

---

## 5. 步驟 9 中提到的 Proxy 是什麼意思？為什麼要透過 Nginx 來 Proxy 到 Express 開發的 Web Server?
- **解釋**: 
  - `Proxy` 是一個中間層，在 server 和 client 之間轉發請求。
  - 分為 **Forward Proxy** 和 **Reverse Proxy**：
    - **Forward Proxy（正向代理）**：代表客戶端發出請求，幫助客戶端訪問受限資源。
    - **Reverse Proxy（反向代理）**：站在伺服器這端接受外部請求，再將這些請求轉發到後端伺服器。
  - Nginx 作為一個 **Reverse Proxy**，可以隱藏後端伺服器的真實 IP，增強安全性，並分擔流量。

---

## 6. Nginx 設定檔範例
```nginx
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
```

## 7. Security Group 是什麼？用途為何？有什麼設定原則嗎？

- **Security Group** 是一種雲端防火牆，控制網路流量的進出，例如限制只有特定 IP 才可以進入。
- **Security Group 的設定原則**：
  - **最小權限原則**：若是只提供 HTTP 服務，就應該將其他的端口關閉。

## 8. 什麼是 sudo？為什麼有的時候需要加上 sudo，有時候不用？

- 需要系統級別的操作就需要 `sudo`，例如安裝軟體或牽涉系統資源管理的操作。
- 但是如果是編輯文件、執行 Python 程式碼這樣的操作，則不需要 `sudo`。

## 9. Nginx 的 Log 檔案在哪裡？你怎麼找到的？怎麼看 Nginx 的 Log？

- **Log 檔案位置**：`/var/log/nginx/`
  - 包括：
    - `access.log`：用於流量分析和網站使用情況的監控。
    - `error.log`：記錄伺服器錯誤。

- **在這個網站找到的**：[Nginx 日誌管理 - CSDN](https://blog.csdn.net/qq_35393472/article/details/136719093)

- **查看 Nginx Log 的方法**：
  - 使用 `vim` 編輯器查看：
    ```bash
    vim access.log
    vim error.log
    ```
  - 查看近期log：
    ```bash
    tail access.log
    ```
  - 查看整個log：
    ```bash
    cat access.log
    ```
  - 查找特定 IP 或日期的log：
    ```bash
    grep "IP" access.log
    grep "日期" access.log
    ```
