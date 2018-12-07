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


# A2. Broken Authentication 失效的身份驗證   

網站應用程式中自行撰寫的身分驗證相關功能有缺陷。例如，登入時無加密、SESSION無控管、Cookie未保護、密碼強度過弱等等。  

# 例如：    
應用程式SESSION Timeout沒有設定。使用者在使用公用電腦登入後卻沒有登出，只是關閉視窗。攻擊者在經過一段時間之後使用同一台電腦，卻可以直接登入。   
 
網站並沒有使用SSL / TLS加密，使用者在使用一般網路或者無線網路時，被攻擊者使用Sniffer竊聽取得User ID、密碼、SESSION ID等，進一步登入該帳號。  
這些都是身分驗證功能缺失的例子。    
  
# 管理者必須做以下的檢查：    

所有的密碼、Session ID、以及其他資訊都有透過加密傳輸嗎？    
憑證都有經過加密或hash保護嗎？    
驗證資訊能被猜測到或被其他弱點修改嗎？    
Session ID是否在URL中暴露出來？    
Session ID是否有Timeout機制？    
# 防護建議：  
使用完善的COOKIE / SESSION保護機制  
不允許外部SESSION  
登入及修改資訊頁面使用SSL加密  
設定完善的Timeout機制  
驗證密碼強度及密碼更換機制  

# A3. Sensitive Data Exposure 敏感資料外漏  
不少網路應用程式對於金融資訊、健康資料及個人資料的保護不足，若遭當駭客取得，就可以進行信用卡詐欺、身份竊取或是其他的犯罪行為等。  
# 保護措施  
不使用或傳送時的資料必須加密  
或者是瀏覽器瀏覽時，也必須要特別注意

# A4. XML External Entities (XXE)外部處理器漏洞  
XML 是一個純文件型態的檔案格式，目的就是將 data 以簡單的格式儲存，方便 data 在不同平台間傳遞、儲存、共享等。  
XML 檔案有兩個特徵：DTD 及 XML Schema，在此特別介紹所謂的 DTD，Document Type Definition，文件類型定義，用來宣告網頁的文件類型。  
會發生 XXE 主要是因為 parser 沒有禁止使用外部實體，意思是我們可以自行定義一個實體名稱，並在實體內容中定義要伺服器做的行為，因此注入點通常是可以輸入 XML 的位置。  
# 由上述可見  
XXE Injection 並不是一個結果，可以說它是一個成因，因為網站含有 XXE 風險，會造成如洩漏敏感資訊、RCE、SSRF、DoS 等結果。  
# 預防 XXE   
完整的禁止使用外部實體，parser 就不會處理攻擊者自行宣告之 entity，即可防止 XXE Injection 的發生。   
PHP 為例，在程式碼中加入  libxml_disable_entity_loader(true);  即可防止 parser 處理外部實體。 
# A5. Broken Access Control 存取控制的破解   
管理者設定好的控制方式被破解了，使得原本不應該被存取的資源被未受權存取了。    
# 在OWASP的解說中也提到，最常發生的幾個狀況:  

不安全的識別(Insecure Id’s ) – 如教室的門窗都鎖好了，進入門只有一個辦法”刷卡”(Id)，因為這唯一的辦法，當別人撿到你的卡就能進到教室裡了。又或者厲害的人拿自已的卡片猜出能進入的卡號，如學號之類的，輸入卡片後也能進入。  
強制頁面流灠(Forced Browsing Past Access Control Checks) – 這就跟上面的例子一樣，明明大家都從門進出，就有人不理門那個鎖，直接去看窗戶上的每個鎖(每個網頁頁面)，看哪一個鎖沒有上，就能進入。  
路徑跨越(Path Traversal )- 這個方法蠻妙的，只要看到教室有人，不用進去，直接跟他講”請幫我拿第二排第三個座位裡的皮夾”，當他說沒有時，就說”第二排第四個”(不斷試路徑)不斷的嘗試一直到真的找到有皮夾的位置。  
檔案權限(File Permissions)-裡論上每個人都有自已的座位，抽屜裡的東西也只有自已能放能拿。但…這只發生在你正坐在座位前面，大家才會這麼守規矩，當你不在座位時，就是把抽屜的權限放出來，讓大家隨意使用。  
流灠器快取(Client Side Caching)-在電腦教室上課每個人都會分配到一台電腦，理論上這台電腦只有你會用，但當你要開GMail時確發現眼前的畫面是別人的信箱，這是因為…前一位同學沒有登出XD  
# 問題是，當我們碰上這些問題的時候這麼解? 怎麼防護呢?

很妙的事，當放在網路上時，我們的警覺好像就會自然的消失，在日常生活反而比較知道怎麼一回事，下面是我們建議的解法:  

不安全的識別(Insecure Id’s ) – 當卡片中的ID可能被偽冒，那我們就加強防偽，如不要用學號、不要用流水號，以不可預測的亂數來當ID。但…別人拿到卡片還是可以進去!!那就讓驗證不只有ID，還要如指紋、密碼等多因素驗證。  
強制頁面流灠(Forced Browsing Past Access Control Checks) –這個真的沒有捷徑，離開教室前要了解到底有多少個窗戶，每個鎖都要上鎖。如果是網頁，往往是邏輯問題，確認需授權的網頁都有確認身份的函數判斷後才能使用，但問題時常在不知道有哪些網頁沒有判斷到，可以透過掃描、滲透服務來協助驗證。  
路徑跨越(Path Traversal )- 這個解法就是要讓每個同學知道，有人要問你教室裡有沒有東西的時候，不要理他、不要幫他找東西，要對的人(身份證證過的人)才幫他找東西。  
檔案權限(File Permissions)-原理很簡單，當你離開座位時，請清空抽屜中的貴重物品，隨身攜帶(確保該有權限的資源一直有權限管制)，所以定時去檢視哪些資源權限沒有設定好，最常以資安技術服務搭配驗證。  
流灠器快取(Client Side Caching)-解法就是要按”登出”，或必免在公用場所使用私資資源。 
A6. Security Miscon뼿guration 不安全的組態設定   
