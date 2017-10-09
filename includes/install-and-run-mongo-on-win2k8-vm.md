請遵循這些步驟 tooinstall，並在執行 Windows Server 的虛擬機器上執行 MongoDB。

> [!IMPORTANT]
> MongoDB 安全性功能，例如驗證和 IP 位址繫結，均非預設為已啟用。 部署 MongoDB tooa 生產環境之前，應該啟用安全性功能。  如需詳細資訊，請參閱[安全性和驗證](http://www.mongodb.org/display/DOCS/Security+and+Authentication)。
>
>

1. 您已連接 toohello 虛擬機器使用遠端桌面之後，開啟 Internet Explorer 從 hello**啟動**hello 虛擬機器上的功能表。
2. 選取 hello**工具**hello 右上角的按鈕。  在**網際網路選項**，選取 hello**安全性**索引標籤，然後選取 hello**信任的網站**圖示，最後按一下 hello**網站**按鈕。 新增*https://\*。 mongodb.org* toohello 信任的網站清單。
3. 跳過[下載-MongoDB](https://www.mongodb.com/download-center#community)。
4. 尋找 hello**目前的穩定版本**的**Community 伺服器**，請選取最新 hello **64 位元**hello Windows 資料行中的版本。 下載，然後執行 hello MSI 安裝程式。
5. MongoDB 通常會安裝在 C:\Program Files\MongoDB。 在 hello 桌面搜尋環境變數，並加入 hello MongoDB 二進位檔路徑 toohello 路徑的變數。 例如，您可能會發現在 C:\Program Files\MongoDB\Server\3.4\bin hello 二進位檔在電腦上。
6. 在 hello 資料磁碟中建立 MongoDB 資料和記錄檔目錄 (例如磁碟機**f:**) 在 hello 先前步驟中所建立。 從**啟動**，選取**命令提示字元**tooopen 命令提示字元視窗。  輸入：

        C:\> F:
        F:\> mkdir \MongoData
        F:\> mkdir \MongoLogs
7. toorun hello 資料庫，請執行：

        F:\> C:
        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log

    所有的記錄訊息會導向的 toohello *F:\MongoLogs\mongolog.log*檔為 mongod.exe 伺服器會啟動並 preallocates 日誌檔案。 它可能需要幾分鐘 MongoDB toopreallocate hello 日誌檔案，並開始接聽連接。 hello 命令提示字元會保持專注在此工作上 MongoDB 執行個體正在執行時。
8. toostart hello MongoDB 系統管理命令介面開啟從另一個 [命令] 視窗**啟動**和型別 hello 下列命令：

        C:\> cd \my_mongo_dir\bin  
        C:\my_mongo_dir\bin> mongo  
        >db  
        test
        > db.foo.insert( { a : 1 } )  
        > db.foo.find()  
        { _id : ..., a : 1 }  
        > show dbs  
        ...  
        > show collections  
        ...  
        > help  

    hello 資料庫會建立 hello 插入。
9. 或者，您可以利用服務形式安裝 mongod.exe：

        C:\> mongod --dbpath F:\MongoData\ --logpath F:\MongoLogs\mongolog.log --logappend  --install

    隨即安裝一個名為 MongoDB 的服務，其說明為 "Mongo DB"。 hello`--logpath`選項必須是使用的 toospecify 記錄檔，因為 hello 執行服務沒有命令視窗 toodisplay 輸出。  hello`--logappend`選項會指定 hello 服務重新啟動導致輸出 tooappend toohello 現有記錄檔。  hello`--dbpath`選項會指定 hello hello 資料目錄位置。 如需更多服務相關的命令列選項，請參閱[服務相關的命令列選項][MongoWindowsSvcOptions]。

    toostart hello 服務，執行下列命令：

        C:\> net start MongoDB
10. 現在，MongoDB 已安裝並執行，您需要 tooopen Windows 防火牆中的連接埠，您可以從遠端連接 tooMongoDB。  從 hello**啟動**功能表上，選取**系統管理工具**然後**具有進階安全性的 Windows 防火牆**。
11. a） hello 左窗格中，選取**輸入規則**。  在 hello**動作**窗格右方，hello 選取**新增規則...**.

    ![Windows 防火牆][Image1]

    b） 在 hello**新增輸入規則精靈**，選取**連接埠**，然後按一下**下一步**。

    ![Windows 防火牆][Image2]

    c) 選取 [TCP] 以及 [指定本機連接埠]。  指定 「 27017 」 （hello 預設連接埠接聽 MongoDB） 的連接埠，然後按一下**下一步**。

    ![Windows 防火牆][Image3]

    d） 選取**允許 hello 連線**按一下**下一步**。

    ![Windows 防火牆][Image4]

    e) 再次按 [下一步]。

    ![Windows 防火牆][Image5]

    f） 指定 hello 規則名稱，例如"MongoPort 」，然後按一下**完成**。

    ![Windows 防火牆][Image6]

12. 如果您未設定端點 for MongoDB。 建立 hello 虛擬機器時，您可以立即進行。 您需要 hello 防火牆規則和 hello 端點 toobe 無法 tooconnect tooMongoDB 遠端。

  在 hello Azure 入口網站，按一下 **虛擬機器 （傳統）**，按一下新的虛擬機器 hello 名稱，然後按一下**端點**。

    ![端點][Image7]

13. 按一下 [新增] 。

14. 新增名稱"Mongo"，通訊協定的端點**TCP**，，兩者均**公用**和**私用**連接埠組太"27017 的 」。 開啟此連接埠可讓 MongoDB toobe 遠端存取。

    ![端點][Image9]

> [!NOTE]
> hello 連接埠 27017 是使用 MongoDB hello 預設通訊埠。 您可以變更此預設連接埠指定 hello`--port`啟動 hello mongod.exe 伺服器時的參數。 請確定 toogive hello hello 防火牆中的相同連接埠號碼和 hello hello 上述指示中的"Mongo"端點。
>
>

[MongoDownloads]: http://www.mongodb.org/downloads

[MongoWindowsSvcOptions]: http://www.mongodb.org/display/DOCS/Windows+Service


[Image1]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall1.png
[Image2]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall2.png
[Image3]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall3.png
[Image4]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall4.png
[Image5]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall5.png
[Image6]: ./media/install-and-run-mongo-on-win2k8-vm/WinFirewall6.png
[Image7]: ./media/install-and-run-mongo-on-win2k8-vm/menusendpointadd.png
<!-- Removed 03/08/2017. Not in new portal. -->
<!-- [Image8]: ./media/install-and-run-mongo-on-win2k8-vm/WinVmAddEndpoint2.png
-->
[Image9]: ./media/install-and-run-mongo-on-win2k8-vm/newendpointdetails.png
