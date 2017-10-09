# <a name="get-started-using-azure-stream-analytics-real-time-fraud-detection"></a>開始使用 Azure 串流分析：即時詐騙偵測

本教學課程提供端對端實例的方式 toouse Azure Stream Analytics。 您會了解如何： 

* 將串流事件帶入 Azure 事件中樞的執行個體中。 在本教學課程中，您將使用我們提供的應用程式來模擬行動電話中繼資料記錄流。

* 撰寫類似 SQL 的串流分析查詢 tootransform 資料、 彙總資訊或尋求模式。 您會看到 toouse 查詢 tooexamine hello 內送資料流的方式，並尋找可能是詐騙的呼叫。

* 傳送 hello 結果 tooan 輸出接收 （儲存體），您可以分析其他深入資訊。 在此情況下，您將會傳送 hello 可疑呼叫資料 tooAzure Blob 儲存體。

在本教學課程中，我們使用電話資料為基礎的即時詐騙偵測 hello 的範例。 但是，我們將說明 hello 技術也適用於其他類型的詐騙偵測，例如信用卡詐騙或身分識別盜用。 

## <a name="scenario-telecommunications-and-sim-fraud-detection-in-real-time"></a>案例：即時偵測電信與 SIM 詐騙

電信公司有大量的資料都是來電。 hello 公司希望有詐騙 toodetect 呼叫即時，讓他們可以通知客戶即將發生或關閉特定數目的服務。 一種類型的 SIM 詐騙牽涉到多個的 hello 呼叫 hello 周圍的相同身分識別相同時間但在不同地理位置。 toodetect 詐騙，這種 hello 公司需求 tooexamine 傳入電話記錄和尋找特定的模式，在此情況下，對呼叫進行 hello 不同國家/地區中相同的時間。 歸類到此類別的任何電話記錄會寫入 toostorage 進行後續分析。

## <a name="prerequisites"></a>必要條件

在本教學課程中，您會透過用戶端應用程式來產生範例通話中繼資料，以模擬通話資料。 有些 hello 應用程式的 hello 記錄產生看起來像詐騙的呼叫。 

開始之前，請確定您擁有 hello 下列：

* 一個 Azure 帳戶。
* hello 呼叫事件產生器應用程式。 您可以取得此下載 hello [TelcoGenerator.zip 檔案](http://download.microsoft.com/download/8/B/D/8BD50991-8D54-4F59-AB83-3354B69C8A7E/TelcoGenerator.zip)從 Microsoft 下載中心 hello。 將此套件解壓縮至電腦上的資料夾。 如果您希望 toosee hello 原始程式碼和偵錯工具中執行的 hello 應用程式，您可以取得 hello 應用程式原始程式碼，從[GitHub](https://aka.ms/azure-stream-analytics-telcogenerator)。 

    >[!NOTE]
    >Windows 可能會封鎖 hello 下載.zip 檔案。 如果您無法將它解壓縮，hello 檔案上按一下滑鼠右鍵，然後選取**屬性**。 如果您看到 hello"這個檔案來自另一部電腦，可能會封鎖的 toohelp 保護您的電腦 」 的訊息、 選取 hello**解除封鎖**選項，然後再按一下**套用**。

如果您想 tooexamine hello hello 串流分析工作結果，您也需要工具來檢視 Azure Blob 儲存體容器的 hello 內容。 如果您使用 Visual Studio，您可以使用 [Azure Tools for Visual Studio](https://docs.microsoft.com/en-us/azure/vs-azure-tools-storage-resources-server-explorer-browse-manage) 或 [Visual Studio Cloud Explorer](https://docs.microsoft.com/en-us/azure/vs-azure-tools-resources-managing-with-cloud-explorer)。 或者，您可以安裝獨立工具，例如 [Azure 儲存體總管](http://storageexplorer.com/)或 [Azure 總管](http://www.cerebrata.com/products/azure-explorer/introduction)。 

## <a name="create-an-azure-event-hubs-tooingest-events"></a>建立 Azure 事件中心 tooingest 事件

tooanalyze 資料流，您*內嵌*到 Azure。 典型 tooingest 資料是 toouse [Azure 事件中心](../event-hubs/event-hubs-what-is-event-hubs.md)，可讓您內嵌的數百萬個每秒的事件，然後處理以及儲存 hello 事件資訊。 此教學課程中，您會建立事件中樞時，而擁有 hello 呼叫事件產生器應用程式傳送呼叫資料 toothat 事件中心。 如需有關事件中心的詳細資訊，請參閱 hello [Azure 服務匯流排文件](https://docs.microsoft.com/en-us/azure/service-bus/)。

>[!NOTE]
>如需此程序更詳細的版本，請參閱[建立事件中樞命名空間，並使用您建立事件中樞 hello Azure 入口網站](../event-hubs/event-hubs-create.md)。 

### <a name="create-a-namespace-and-event-hub"></a>建立命名空間和事件中樞
在此程序，您先建立事件中樞命名空間中，並將事件中樞 toothat namepsace。 事件中樞命名空間用 toologically 群組相關的事件匯流排執行個體。 

1. 登入 hello Azure 入口網站並按一下**新增** > **物聯網** > **事件中心**。 

2. 在 hello**建立命名空間**刀鋒視窗中，輸入命名空間名稱，例如`<yourname>-eh-ns-demo`。 您可以使用任何名稱，如 hello 命名空間，但是 hello 名稱必須是有效的 URL，而且它必須是唯一的 Azure。 
    
3. 選取訂用帳戶並建立或選擇資源群組，然後按一下 [建立]。 

    ![建立事件中樞命名空間](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-namespace-new-portal.png)
 
4. 當部署完成 hello 命名空間時，尋找 hello 事件中樞命名空間清單中的 Azure 資源。 

5. 按一下 hello 新命名空間，然後在 hello 命名空間刀鋒視窗中，按一下 **+&nbsp;事件中心**。 

    ![hello 新增事件中樞按鈕建立新的事件中樞 ](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-button-new-portal.png)    
 
6. 名稱資料行 hello 新的事件中樞`sa-eh-frauddetection-demo`。 您可以使用不同的名稱。 如果您這樣做，請記錄下來，因為您稍後需要 hello 名稱。 您不需要 tooset 任何其他選項 hello 事件中樞現在。

    ![建立新事件中樞的刀鋒視窗](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-eventhub-new-portal.png)
    
 
7. 按一下 [建立] 。
### <a name="grant-access-toohello-event-hub-and-get-a-connection-string"></a>授與存取 toohello 事件中樞，並取得連接字串

處理程序可以傳送資料 tooan 事件中心之前，hello 事件中心必須要有原則，可讓適當的存取權。 hello 存取原則會產生包含授權資訊的連接字串。

1.  在 hello 事件命名空間刀鋒視窗中，按一下 **事件中心**，然後按一下新的事件中樞的 hello 名稱。

2.  在 hello 事件中樞刀鋒視窗中，按一下 **共用存取原則**，然後按一下  **+&nbsp;新增**。

    >[!NOTE]
    >請確定您正在使用 hello 事件中心不 hello 事件中樞命名空間。

3.  新增名為 `sa-policy-manage-demo` 的原則，然後在 [宣告] 中，選取 [管理]。

    ![建立新事件中樞存取原則的刀鋒視窗](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-shared-access-policy-manage-new-portal.png)
 
4.  按一下 [建立] 。

5.  Hello 原則已部署之後，請按一下它在 hello 清單中的共用的存取原則。

6.  尋找 hello 方塊標示為**連接字串-主索引鍵**按一下 hello 複製按鈕下一步 toohello 連接字串。 
    
    ![複製 hello 主要連接字串索引鍵與 hello 存取原則](./media/stream-analytics-real-time-fraud-detection/stream-analytics-shared-access-policy-copy-connection-string-new-portal.png)
 
7.  貼入文字編輯器中的 hello 連接字串。 Hello 下一節中，進行一些稍微修改 tooit 之後，您需要開啟這個連接字串。

    hello 連接字串看起來像這樣：

        Endpoint=sb://YOURNAME-eh-ns-demo.servicebus.windows.net/;SharedAccessKeyName=sa-policy-manage-demo;SharedAccessKey=Gw2NFZwU1Di+rxA2T+6hJYAtFExKRXaC2oSQa0ZsPkI=;EntityPath=sa-eh-frauddetection-demo

    請注意 hello 連接字串包含多個索引鍵-值組，並以分號分隔： `Endpoint`， `SharedAccessKeyName`， `SharedAccessKey`，和`EntityPath`。  

## <a name="configure-and-start-hello-event-generator-application"></a>設定並啟動 hello 事件產生器應用程式

開始 hello TelcoGenerator 應用程式之前，您設定它，讓它會將傳送您剛才建立的呼叫記錄 toohello 事件中心。

### <a name="configure-hello-telcogeneratorapp"></a>設定 hello TelcoGeneratorapp

1.  在您用來複製 hello 連接字串 hello 編輯器中，記下 hello`EntityPath`值，然後再移除 hello`EntityPath`組 （別忘了在它之前的 tooremove hello 分號）。 

2.  在您解壓縮 hello TelcoGenerator.zip 檔案 hello 資料夾中，開啟 hello telcodatagen.exe.config 檔案在編輯器中。 （沒有一個以上的.config 檔案，因此請確定您開啟 hello 右移一個）。

3.  在 hello`<appSettings>`項目，執行這項操作：

    * 設定 hello hello 值`EventHubName`金鑰 toohello 事件中樞名稱 （也就是 toohello 值 hello 實體路徑）。
    * 設定 hello hello 值`Microsoft.ServiceBus.ConnectionString`金鑰 toohello 連接字串。 

    hello`<appSettings>`區段看起來像下列範例中的 hello。 （為了清楚起見，我們包裝 hello 行，而且移除某些字元 hello 授權權杖。）

    ![TelcoGenerator 顯示 hello 事件中樞的名稱和連接字串的應用程式組態檔](./media/stream-analytics-real-time-fraud-detection/stream-analytics-telcogenerator-config-file-app-settings.png)
 
4.  儲存 hello 檔案。 

### <a name="start-hello-app"></a>啟動 hello 應用程式
1.  開啟命令視窗，並變更 toohello hello TelcoGenerator 應用程式解壓縮所在的資料夾。
2.  輸入下列命令的 hello:

        telcodatagen.exe 1000 .2 2

    hello 參數如下： 

    * 每小時的 CDR 數目。 
    * SIM 卡詐騙機率： 頻率，以百分比表示的所有呼叫，該 hello 應用程式應該模擬的詐騙的呼叫。 hello 值.2 表示大約 20%的記錄 hello 呼叫看起來詐騙。
    * 持續時間 (小時)。 hello 的小時數 hello 應用程式應該執行。 您也可以停止 hello 應用程式隨時在 hello 命令列中按下 Ctrl + C。

    幾秒之後，hello 應用程式會啟動 hello 螢幕上顯示通話記錄，因為它會傳送它們 toohello 事件中心。

您將使用此即時詐騙偵測應用程式中的 hello 索引鍵欄位有些 hello 下列：

|**記錄**|**定義**|
|----------|--------------|
|`CallrecTime`|hello hello 呼叫所花費的時間戳記的開始時間。 |
|`SwitchNum`|hello 電話交換機用 tooconnect hello 呼叫。 例如，hello 參數會是代表 hello 國家/地區 （US、 中國、 英國、 德國或澳洲） 的字串。 |
|`CallingNum`|hello hello 呼叫端的電話號碼。 |
|`CallingIMSI`|hello 國際行動用戶識別碼 (IMSI)。 這是 hello hello 呼叫端的唯一識別項。 |
|`CalledNum`|hello hello 呼叫收件者電話號碼。 |
|`CalledIMSI`|國際行動用戶識別碼 (IMSI)。 這是 hello hello 呼叫收件者的唯一識別碼。 |


## <a name="create-a-stream-analytics-job-toomanage-streaming-data"></a>建立串流資料的資料流分析工作 toomanage

既然已取得通話事件的資料流，您可以開始設定串流分析作業。 hello 作業會從您設定的 hello 事件中心讀取資料。 

### <a name="create-hello-job"></a>建立 hello 作業 

1. 在 hello Azure 入口網站，按一下 **新增** > **物聯網** > **資料流分析工作**。

2. 名稱 hello 工作`sa_frauddetection_job_demo`，指定的訂用帳戶、 資源群組和位置。

    它是個不錯的主意 tooplace hello 作業和 hello 事件中樞 hello，以免付出 tootransfer 資料區域之間的最佳效能，所以相同的區域。

    ![建立新的串流分析作業](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-job-new-portal.png)

3. 按一下 [建立] 。

    建立 hello 工作，而 hello 入口網站會顯示工作詳細資料。 執行任何動作正在執行，不過，您有 tooconfigure hello 工作，才能啟動。

### <a name="configure-job-input"></a>設定作業輸入

1. 在 hello 儀表板或 hello**所有資源**刀鋒視窗中，尋找並選取 hello`sa_frauddetection_job_demo`資料流分析工作。 
2. 在 hello**作業拓撲**區段 hello 資料流分析工作刀鋒視窗中，按一下 hello**輸入**方塊。

    ![在拓撲 hello 串流分析工作刀鋒視窗中的輸入的方塊](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-input-box-new-portal.png)
 
3. 按一下 **+&nbsp;新增**然後填入 hello 刀鋒視窗包含下列值：

    * **輸入的別名**： 使用 hello 名稱`CallStream`。 如果使用不同的名稱，請記下來，因為稍後需要用到。
    * **來源類型**：選取 [資料流]。 (**參考資料**參考 toostatic 查閱資料，您將不會在本教學課程中使用。)
    * **來源**：選取 [事件中樞]。
    * **匯入選項**：選取 [使用目前訂用帳戶的事件中樞]。 
    * **服務匯流排命名空間**： 選取 hello 事件中樞命名空間您稍早建立 (`<yourname>-eh-ns-demo`)。
    * **事件中心**: hello 選取您稍早建立的事件中心 (`sa-eh-frauddetection-demo`)。
    * **事件中樞原則名稱**： 選取您稍早建立的 hello 存取原則 (`sa-policy-manage-demo`)。

    ![建立串流分析作業的新輸入](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sa-input-new-portal.png)

4. 按一下 [建立] 。

## <a name="create-queries-tootransform-real-time-data"></a>建立查詢 tootransform 即時資料

此時，您必須設定 tooread 內送資料流資料流分析工作。 hello 下一個步驟是 toocreate 分析即時 hello 資料的轉換。 做法是建立查詢。 串流分析支援用來說明轉換的簡單、宣告式查詢模型，以供即時處理。 hello 查詢使用具有某些延伸模組特定 toostream 分析類似 SQL 的語言。 

非常簡單的查詢可能會直接讀取所有 hello 內送資料。 不過，您通常會建立查詢的特定資料或 hello 資料中關聯性的查詢。 在本節中的 hello 教學課程，您會建立並測試數個查詢 toolearn 在其中您可以將分析的輸入資料流轉換的數種方法。 

您在此處建立 hello 查詢將只會顯示 hello 已轉換的資料 toohello 螢幕。 在更新版本的區段中，您需要設定的輸出來源，以及寫入 hello 已轉換的資料 toothat 接收器的查詢。

toolearn 進一步了解 hello 語言，請參閱 hello [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/dn834998.aspx)。

### <a name="get-sample-data-for-testing-queries"></a>取得範例資料來測試查詢

hello TelcoGenerator 應用程式正在呼叫記錄 toohello 事件中樞與串流分析工作會從 hello 事件中樞設定的 tooread。 您可以使用查詢 tootest hello 作業 toomake 確定正確讀取。 太測試查詢 hello Azure 主控台中，您需要範例資料。 這個逐步解說中，您將範例資料擷取 hello 事件中心傳入的 hello 資料流。

1. 請確定該 hello TelcoGenerator 應用程式正在執行，而且會產生記錄呼叫。
2. 在 hello 入口網站中，傳回 toohello 串流分析工作刀鋒視窗。 (如果您關閉 hello 刀鋒視窗中，搜尋`sa_frauddetection_job_demo`在 hello**所有資源**刀鋒視窗。)
3. 按一下 hello**查詢**方塊。 Azure 會列出 hello 輸入及輸出，已設定為 hello 工作，並可讓您建立查詢，可讓您轉換 hello 輸入資料流傳送 toohello 輸出。
4. 在 hello**查詢**刀鋒視窗中，按一下 下一步 toohello 的 hello 點`CallStream`輸入，然後選取 **範例從輸入資料**。

    ![功能表選項 toouse 的範例資料 hello 串流分析工作項目，如 「 範例資料從輸入 」 選取](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-sample-data-from-input.png)

    這會開啟可讓您指定以 tooread hello 多久輸入資料流定義多少範例資料 tooget 刀鋒視窗。

5. 設定**分鐘**too3，然後按一下**確定**。 
    
    ![取樣 hello 輸入資料流，與 「 3 分鐘 」，選取選項。](./media/stream-analytics-real-time-fraud-detection/stream-analytics-input-create-sample-data.png)

    Azure 範例 3 分鐘 hello 輸入資料流中的資料量與 hello 範例資料已就緒時通知您。 (這需要等一下。) 

hello 範例資料會暫時存放，可同時有 hello 查詢視窗中開啟。 如果您關閉 hello 查詢視窗中，會捨棄 hello 範例資料，而且必須 toocreate 一組新的範例資料。 

或者，您可以取得中有範例資料的.json 檔案[從 GitHub](https://github.com/Azure/azure-stream-analytics/blob/master/Sample%20Data/telco.json)，然後將該.json 檔案 toouse 上傳為範例資料以供 hello`CallStream`輸入。 

### <a name="test-using-a-pass-through-query"></a>使用傳遞查詢來測試

如果您想 tooarchive 每個事件，您可以使用傳遞查詢 tooread hello 事件的 hello 承載中的所有 hello 欄位。

1. 在 hello 查詢視窗中，輸入以下查詢：

        SELECT 
            *
        FROM 
            CallStream

    >[!NOTE]
    >如同 SQL，關鍵字不區分大小寫，空白字元也不重要。

    在此查詢中，`CallStream`是 hello 別名，指定當您建立 hello 輸入。 如果您使用不同的別名，請改為使用該名稱。

2. 按一下 [ **測試**]。

    hello 資料流分析工作會針對 hello 取樣資料執行 hello 查詢，並在 hello hello 視窗底部顯示 hello 輸出。 這會告訴您正確設定 hello 事件中樞與 hello 串流分析工作。 (如所述，稍後您將建立的輸出接收該 hello 查詢可以將資料寫入。)

    ![串流分析作業輸出，顯示已產生 73 筆記錄](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output.png)

    hello 的記錄，您會看到的確切數目將取決於在 3 分鐘範例中所擷取的記錄數目。
 
### <a name="reduce-hello-number-of-fields-using-a-column-projection"></a>減少 hello 使用資料行投射的欄位數目

在許多情況下，您分析不需要從 hello 輸入資料流的所有 hello 資料行。 您可以使用較少的欄位比查詢傳回的 hello 傳遞查詢 tooproject。

1. 變更 hello 編輯器 toohello 後面的程式碼中的 hello 查詢：

        SELECT CallRecTime, SwitchNum, CallingIMSI, CallingNum, CalledNum 
        FROM 
            CallStream

2. 再按一次 [測試]。 

    ![投影的串流分析作業輸出，顯示已產生 25 筆記錄](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-projection.png)
 
### <a name="count-incoming-calls-by-region-tumbling-window-with-aggregation"></a>各區域的來電計數：含彙總的輪轉視窗

假設您想要的連入呼叫每個區域的 toocount hello 數字。 在資料流處理資料，當您想 tooperform 彙總函式，例如計算，您需要 toosegment hello 資料流到暫時的單位 （因為 hello 資料流本身是有效的無止盡的）。 做法是使用串流分析[視窗函式](stream-analytics-window-functions.md)。 您接著可以使用該視窗內 hello 資料，做為一個單位。

在這個轉換過程中，您需要有一連串不重疊的時態性視窗，每個視窗會有一組特定的資料讓您分組和彙總。 這種類型的視窗是參照的 tooas*輪轉視窗*。 在 hello 輪轉視窗中，您可以取得 hello 分組的連入呼叫計數`SwitchNum`，代表 hello hello 呼叫起源所在的國家/地區。 

1. 變更 hello 編輯器 toohello 後面的程式碼中的 hello 查詢：

        SELECT 
            System.Timestamp as WindowEnd, SwitchNum, COUNT(*) as CallCount 
        FROM
            CallStream TIMESTAMP BY CallRecTime 
        GROUP BY TUMBLINGWINDOW(s, 5), SwitchNum

    此查詢會使用 hello`Timestamp By`關鍵字 hello`FROM`子句 toospecify hello 中的哪一個時間戳記欄位輸入資料流 toouse toodefine hello 輪轉視窗。 在此情況下，hello 視窗分成 hello 資料區段的 hello`CallRecTime`欄位中每一筆記錄。 （如果未不指定任何欄位，則 hello 視窗化作業會使用每個事件抵達 hello 事件中心的 hello 時間。 請參閱[串流分析查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)中的＜抵達時間與應用時間的比較＞。 

    hello 投影包含`System.Timestamp`，它會傳回每個視窗的 hello 結束的時間戳記。 

    您想 toouse 輪轉視窗 toospecify，使用 hello [TUMBLINGWINDOW](https://msdn.microsoft.com/library/dn835055.aspx)函式在 hello`GROUP BY `子句。 在 hello 函式，您可以指定時間單位 （從微秒 tooa 每天） 和視窗大小 （單位數量）。 在此範例中，hello 輪轉視窗組成 5 秒的間隔，以便每隔 5 秒的價值的呼叫會取得依國家/地區的計數。

2. 再按一次 [測試]。 在 hello 結果中，請注意下的該 hello 時間戳記**WindowEnd**在 5 秒為增量單位。

    ![彙總的串流分析作業輸出，顯示已產生 13 筆記錄](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-aggregation.png)
 
### <a name="detect-sim-fraud-using-a-self-join"></a>使用自我聯結來偵測 SIM 詐騙

針對此範例中，我們可以考慮詐騙使用量 toobe 呼叫源自 hello 相同使用者但在不同的另一個 5 秒內的位置。 例如，hello 相同的使用者無法合法撥打電話，從 hello 美國和澳大利亞 hello 在相同的時間。 

toocheck 在這些情況下的，您可以使用自我聯結的資料流資料 toojoin hello 資料流 tooitself 根據 hello hello`CallRecTime`值。 然後您可以查看呼叫記錄在 hello`CallingIMSI`值 (hello 起始數字) 是 hello 相同，但 hello `SwitchNum` （國家/地區） 的值不是 hello 相同。

當您使用資料流資料使用聯結時，hello 聯結必須提供遠比對資料列的 hello 一些限制，可以及時區隔。 （如前文所述，hello 串流資料是有效的無止盡）。指定 hello hello 關聯性的時間範圍內 hello`ON`使用 hello 的 hello 聯結子句`DATEDIFF`函式。 在此情況下，hello 聯結根據在 5 秒的間隔呼叫資料。

1. 變更 hello 編輯器 toohello 後面的程式碼中的 hello 查詢： 

        SELECT  System.Timestamp as Time, 
            CS1.CallingIMSI, 
            CS1.CallingNum as CallingNum1, 
            CS2.CallingNum as CallingNum2, 
            CS1.SwitchNum as Switch1, 
            CS2.SwitchNum as Switch2 
        FROM CallStream CS1 TIMESTAMP BY CallRecTime 
            JOIN CallStream CS2 TIMESTAMP BY CallRecTime 
            ON CS1.CallingIMSI = CS2.CallingIMSI 
            AND DATEDIFF(ss, CS1, CS2) BETWEEN 1 AND 5 
        WHERE CS1.SwitchNum != CS2.SwitchNum

    此查詢就像除了 hello 任何 SQL 聯結`DATEDIFF`hello 聯結中的函式。 這是版本`DATEDIFF`特定 tooStreaming 分析，而且它必須出現在 hello`ON...BETWEEN`子句。 hello 參數為時間單位 （在此範例中為秒） 和 hello 別名的 hello hello 聯結兩個來源。 (這點不同於 hello 標準 SQL`DATEDIFF`函式。) 

    hello`WHERE`子句包含 hello 詐騙呼叫加上旗標的 hello 條件： hello 原始參數不是 hello 相同。 

2. 再按一次 [測試]。 

    ![自我聯結的串流分析作業輸出，顯示已產生 6 筆記錄](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-sample-output-self-join.png)

3. 按一下 [儲存] 。 這可以節省 hello 自我聯結查詢 hello 串流分析工作的一部分。 （它不會儲存 hello 範例資料）。

    ![儲存串流分析作業](./media/stream-analytics-real-time-fraud-detection/stream-analytics-query-editor-save-button-new-portal.png)

## <a name="create-an-output-sink-toostore-transformed-data"></a>建立輸出接收 toostore 轉換資料

您已定義的事件資料流、 事件中樞輸入的 tooingest 事件，以及查詢 tooperform 轉換 hello 資料流上。 hello 最後一個步驟是 toodefine 為 hello 工作的輸出來源 — 也就是將 toowrite hello 轉換資料流。 

您可以使用許多資源作為輸出接收，例如 SQL Server 資料庫、資料表儲存體、Data Lake 儲存體、Power BI，甚至是另一個事件中樞。 此教學課程中，您會將寫入 hello 資料流 tooAzure Blob 儲存體，這是典型的選擇，來收集事件資訊，以便稍後進行分析，因為它適用於非結構化的資料。

如果您已有 blob 儲存體帳戶，則可直接使用。 此教學課程中，我們將為您示範如何 toocreate 新的儲存體帳戶只針對本教學課程。

### <a name="create-an-azure-blob-storage-account"></a>建立 Azure Blob 儲存體帳戶

1. 在 hello Azure 入口網站，會傳回 toohello 串流分析工作刀鋒視窗。 (如果您關閉 hello 刀鋒視窗中，搜尋`sa_frauddetection_job_demo`在 hello**所有資源**刀鋒視窗。)
2. 在 hello**作業拓撲**區段中，按一下 hello**輸出**方塊。 
3. 在 hello**輸出**刀鋒視窗中，按一下 **+&nbsp;新增**然後填入 hello 刀鋒視窗包含下列值：

    * **輸出別名**： 使用 hello 名稱`CallStream-FraudulentCalls`。 
    * **接收器**：選取 [Blob 儲存體]。
    * **匯入選項**：選取 [使用來自目前訂用帳戶的 Blob 儲存體]。
    * **儲存體帳戶**。 選取 [建立新儲存體帳戶]。
    * **儲存體帳戶** (第二個方塊)。 輸入 `YOURNAMEsademo`，其中 `YOURNAME` 是您的名稱或另一個唯一字串。 hello 名稱可以使用小寫字母和數字，而且它必須是唯一整個 Azure。 
    * **容器**。 輸入 `sa-fraudulentcalls-demo`。
    hello 儲存體帳戶名稱及容器名稱是使用同時 tooprovide hello blob 儲存體，像這樣的 URI: 

    `http://yournamesademo.blob.core.windows.net/sa-fraudulentcalls-demo/...`
    
    ![串流分析作業的 [新輸出] 刀鋒視窗](./media/stream-analytics-real-time-fraud-detection/stream-analytics-create-output-blob-storage-new-console.png)
    
4. 按一下 [建立] 。 

    Azure 會建立 hello 儲存體帳戶，並會自動產生索引鍵。 

5. 關閉 hello**輸出**刀鋒視窗。 

## <a name="start-hello-streaming-analytics-job"></a>啟動 hello 串流分析工作

hello 工作現在已設定。 您所指定的輸入 （hello 事件中心）、 (hello 查詢詐騙呼叫的 toolook，) 的轉換和輸出 （blob 儲存）。 您現在可以啟動 hello 作業。 

1. 請確定 hello TelcoGenerator 應用程式正在執行。

2. 在 hello 作業刀鋒視窗中，按一下 **啟動**。

    ![啟動 hello 資料流分析工作](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-output.png)

3. 在 hello**開始工作**刀鋒視窗中的，對於作業輸出開始時間，請選取**現在**。 

4. 按一下 [啟動] 。 

    ![「 啟動工作 」 刀鋒視窗中的 hello 資料流分析工作](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-start-job-blade.png)

    Azure 通知您，當 hello 作業已啟動，而且 hello 作業刀鋒視窗中，在 hello 狀態會顯示為**執行**。

    ![串流分析作業狀態，顯示「執行中」](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-running-status.png)
    

## <a name="examine-hello-transformed-data"></a>檢查 hello 轉換資料

您現在已完成串流分析作業。 hello 作業是檢查通話中繼資料的資料流、 尋找即時詐騙撥打電話，以及撰寫這些詐騙呼叫 toostorage 的相關資訊。 

toocomplete 本教學課程中，您可能會想 toolook hello hello 串流分析工作所擷取的資料。 hello 資料寫入 Blob 儲存體 tooAzure 區塊 （chunk） （檔案）。 您可以使用任何可讀取 Azure Blob 儲存體的工具。 Hello 必要條件 > 一節所述，您可以在 Visual Studio 中，使用 Azure 擴充功能，或者您可以使用這類工具[Azure 儲存體總管](http://storageexplorer.com/)或[Azure 總管](http://www.cerebrata.com/products/azure-explorer/introduction)。 

當您檢查 hello blob 儲存體中的檔案內容時，您會看到類似下列 hello:

![Azure blob 儲存體與串流分析輸出](./media/stream-analytics-real-time-fraud-detection/stream-analytics-sa-job-blob-storage-view.png)
 

## <a name="clean-up-resources"></a>清除資源

我們有其他發行項，繼續進行 hello 詐騙偵測案例，並使用您已建立本教學課程中的 hello 資源。 如果您想 toocontinue，請參閱底下的 hello 建議**後續步驟**更新版本。

不過，如果您完成時，您不需要您已建立 hello 資源，您可以刪除它們，讓您不會產生不必要的 Azure 費用。 在此情況下，我們建議您不要 hello 遵循：

1. 停止 hello 串流分析工作。 在 hello**作業**刀鋒視窗中，按一下 **停止**hello 頂端。
2. 停止 hello 電信公司產生器應用程式。 在 hello 命令視窗，在您啟動 hello 應用程式，請按 Ctrl + C。
3. 如果您建立的新 blob 儲存體帳戶只用於本教學課程，請刪除它。 
4. 刪除 hello 串流分析工作。
5. 刪除 hello 事件中樞。
6. 刪除 hello 事件中樞命名空間。

## <a name="get-support"></a>取得支援

如需進一步的協助，請參閱我們的 [Azure Stream Analytics 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)。

## <a name="next-steps"></a>後續步驟

您可以繼續本教學課程以 hello 下列文章：

* [串流分析及 Power BI：適用於串流資料的即時分析儀表板](stream-analytics-power-bi-dashboard.md)。 本文章將示範如何 toosend hello 電信公司輸出的 hello 資料流分析作業 tooPower BI 即時的視覺效果和分析。
* [如何從 Azure Redis 快取 Azure 函式的使用中的 Azure Stream Analytics toostore 資料](stream-analytics-functions-redis.md)。 本文將說明如何 toouse Azure 函式 toowrite 詐騙呼叫 tooan Azure Redis 快取透過服務匯流排佇列。

如需串流分析在整體上的詳細資訊，請參閱下列文章：

* [簡介 tooAzure 資料流分析](stream-analytics-introduction.md)
* [調整 Azure Stream Analytics 工作](stream-analytics-scale-jobs.md)
* [Azure Stream Analytics 查詢語言參考](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [Azure 串流分析管理 REST API 參考](https://msdn.microsoft.com/library/azure/dn835031.aspx)
