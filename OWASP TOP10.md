# OWASP TOP 10[2017]
#  OWASP基金會

Open Web Application Security Project（或簡稱OWASP）。    
於2004年4月21日在美國成立為非盈利慈善組織，以確保我們在OWASP工作的持續可用性和支持。

# OWASP TOP 10
新版OWASP十大網站安全風險排名出爐，微服務風潮帶來三大新安全風險

OWASP在11月20日公布最新版十大網站資安風險，納入社群建議和實際調查結果後，調整了多項資安風險項目，
各平臺常見的XML外部處理器漏洞，Java平臺、PHP或Node.js等平臺常見的不安全反序列化漏洞，以及紀錄與監控不足風險，則是2017年上榜的網路安全新風險    
文/黃彥棻 | 2017-11-21發表


http://www.gss.com.tw/images/stories/eispage/vol89/pdf/EIS89_P30_-10--OWASP-TOP-10-2017.pdf     
A1 – Injection（注入攻擊）  
A2. Broken Authentication 失效的身份驗證    
A3. Sensitive Data Exposure 敏感資料外漏    
A4. XML External Entities (XXE)外部處理器漏洞   
A5. Broken Access Control 存取控制的破解   
A6. Security Miscon뼿guration 不安全的組態設定   
A7. Cross-Site Scripting   XSS   跨站腳本攻擊   
A8. Insecure Deserialization 不安全的反序列化漏洞    
A9. Using Components with Known Vulnerabilities 使用已知漏洞元件    
A10. Insuffcient Logging & Monitoring 記錄與監控不足    

# A1  - 注射（注入攻擊）
網站應用程式執行來自外部包括資料庫在內的惡意指令，SQL Injection與Command Injection等攻擊包括在內。  
因為駭客必須猜測管理者所撰寫的方式，因此又稱  「駭客的填空遊戲」。  

# 簡述駭客攻擊流程：  

找出未保護變數，作為注入點  
猜測完整Command並嘗試插入  
推測欄位數、Table名稱、SQL版本等資訊  
完整插入完成攻擊程序   
# 防護建議：  

使用Prepared Statements，例如Java PreparedStatement()，.NET SqlCommand(), OleDbCommand()，PHP PDO bindParam()  
使用Stored Procedures  
嚴密的檢查所有輸入值  
使用過濾字串函數過濾非法的字元，例如mysql_real_escape_string、addslashes  
控管錯誤訊息只有管理者可以閱讀  
控管資料庫及網站使用者帳號權限為何  
