---
title: "使用資料流分析的 IoT 解決方案 aaaBuild |Microsoft 文件"
description: "快速入門教學課程中的 hello 的收費站案例的資料流分析 IoT 解決方案"
keywords: "iot 解決方案, 視窗函數"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: a473ea0a-3eaa-4e5b-aaa1-fec7e9069f20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: e37fc5b56c4ffc4a2d7b820afe0c17631e577ea0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="build-an-iot-solution-by-using-stream-analytics"></a>利用串流分析來建置 IoT 解決方案
## <a name="introduction"></a>簡介
在此教學課程中，您將學習如何 toouse Azure Stream Analytics tooget 即時深入資訊從您的資料。 開發人員可以輕鬆地結合資料的流，例如按一下資料流、 記錄檔，以及裝置產生的事件，歷程記錄或參考資料 tooderive 商業見解。 以完全受管理、 即時資料流計算服務裝載於 Microsoft Azure，Azure Stream Analytics 提供內建的恢復功能、 低延遲度及延展性 tooget 啟動及執行以分鐘為單位。

完成本教學課程之後，您將能夠：

* 熟悉 hello Azure Stream Analytics 入口網站。
* 設定及部署串流工作。
* 表達真實問題和解決使用 hello Stream Analytics 查詢語言。
* 有自信地使用串流分析來為客戶開發串流解決方案。
* 使用 hello 監視和記錄經驗 tootroubleshoot 問題。

## <a name="prerequisites"></a>必要條件
您將需要 hello 必要條件 toocomplete 遵循本教學課程：

* hello 最新版本的[Azure PowerShell](/powershell/azure/overview)
* Visual Studio 2017，2015 中，或使用可用的 hello [Visual Studio Community](https://www.visualstudio.com/products/visual-studio-community-vs.aspx)
* [Azure 訂用帳戶](https://azure.microsoft.com/pricing/free-trial/)
* Hello 電腦上的系統管理權限
* 下載[TollApp.zip](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip)從 Microsoft 下載中心 hello
* 選擇性： Hello TollApp 事件產生器中的原始程式碼[GitHub](https://aka.ms/azure-stream-analytics-toll-source)

## <a name="scenario-introduction-hello-toll"></a>案例簡介：收費站，你好！
收費站是常見的設施。 您會遇到這些許多 expressways、 橋接器和通道 hello 世界各地。 每個收費站都有多個收費亭。 在手動攤位，您可以停止 toopay hello 付費 tooan 服務員。 在自動化攤位，每個亭上方的感應器會掃描您傳送嗨收費亭為貼附 toohello 擋風玻璃上的汽車的 RFID 卡。 它是簡單 toovisualize hello 經過通過這些收費站的車輛的可執行有趣作業的事件資料流。

![收費亭中車輛的圖片](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image1.jpg)

## <a name="incoming-data"></a>傳入的資料
本教學課程搭配兩個資料串流來教學。 感應器安裝在 hello 進入與離開 hello 付費電台產生 hello 第一個資料流。 hello 第二個資料流是擁有車輛註冊資料的靜態查閱資料集。

### <a name="entry-data-stream"></a>入口資料流
hello 項目資料流在進入收費站包含汽車的相關資訊。

| TollID | EntryTime | LicensePlate | State | Make | 模型 | VehicleType | VehicleWeight | Toll | Tag |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| 1 |2014-09-10 12:01:00.000 |JNB 7001 |NY |Honda |CRV |1 |0 |7 | |
| 1 |2014-09-10 12:02:00.000 |YXZ 1001 |NY |Toyota |Camry |1 |0 |4 |123456789 |
| 3 |2014-09-10 12:02:00.000 |ABC 1004 |CT |Ford |Taurus |1 |0 |5 |456789123 |
| 2 |2014-09-10 12:03:00.000 |XYZ 1003 |CT |Toyota |Corolla |1 |0 |4 | |
| 1 |2014-09-10 12:03:00.000 |BNJ 1007 |NY |Honda |CRV |1 |0 |5 |789123456 |
| 2 |2014-09-10 12:05:00.000 |CDE 1007 |NJ |Toyota |4x4 |1 |0 |6 |321987654 |

以下是簡短 hello 資料行的描述：

| 資料欄 | 說明 |
| --- | --- |
| TollID |可唯一識別收費亭 hello 收費亭識別碼 |
| EntryTime |hello 日期和時間-utc 時區 hello vehicle toohello 收費亭的項目 |
| LicensePlate |hello 與車牌號碼的一種載具，hello |
| State |美國的某個洲 |
| Make |hello 汽車的 hello 製造商 |
| 模型 |hello 汽車 hello 型號號碼 |
| VehicleType |1 代表載客車或 2 代表商用車 |
| WeightType |車輛的重量，單位為噸；0 代表客車 |
| Toll |以 usd 計算 hello 付費值 |
| Tag |hello E-tag 上自動執行付款; hello 汽車空白 hello 付款已手動完成 |

### <a name="exit-data-stream"></a>出口資料流
hello 結束資料流包含離開 hello 收費站的汽車相關資訊。

| **TollId** | **ExitTime** | **LicensePlate** |
| --- | --- | --- |
| 1 |2014-09-10T12:03:00.0000000Z |JNB 7001 |
| 1 |2014-09-10T12:03:00.0000000Z |YXZ 1001 |
| 3 |2014-09-10T12:04:00.0000000Z |ABC 1004 |
| 2 |2014-09-10T12:07:00.0000000Z |XYZ 1003 |
| 1 |2014-09-10T12:08:00.0000000Z |BNJ 1007 |
| 2 |2014-09-10T12:07:00.0000000Z |CDE 1007 |

以下是簡短 hello 資料行的描述：

| 資料欄 | 說明 |
| --- | --- |
| TollID |可唯一識別收費亭 hello 收費亭識別碼 |
| ExitTime |hello 日期和時間-utc 時區的收費亭的 hello 汽車結束 |
| LicensePlate |hello 與車牌號碼的一種載具，hello |

### <a name="commercial-vehicle-registration-data"></a>商用車的登記資料
hello 教學課程使用靜態的商用車輛註冊資料庫快照集。

| LicensePlate | RegistrationId | 已過期 |
| --- | --- | --- |
| SVT 6023 |285429838 |1 |
| XLZ 3463 |362715656 |0 |
| BAC 1005 |876133137 |1 |
| RIV 8632 |992711956 |0 |
| SNY 7188 |592133890 |0 |
| ELH 9896 |678427724 |1 |

以下是簡短 hello 資料行的描述：

| 資料欄 | 說明 |
| --- | --- |
| LicensePlate |hello 與車牌號碼的一種載具，hello |
| RegistrationId |hello 車輛註冊識別碼 |
| 已過期 |hello hello vehicle 登錄狀態： 0，如果車輛註冊為作用中，1，表示註冊已過期 |

## <a name="set-up-hello-environment-for-azure-stream-analytics"></a>設定 Azure Stream Analytics hello 環境
toocomplete 本教學課程中，您需要 Microsoft Azure 訂用帳戶。 Microsoft 能讓您免費試用 Microsoft Azure 服務。

如果您沒有 Azure 帳戶，您可以 [要求獲得免費試用版](http://azure.microsoft.com/pricing/free-trial/)。

> [!NOTE]
> toosign 註冊免費試用版，您需要的行動裝置，可以接收文字訊息和有效的信用卡。
> 
> 

請務必 toofollow hello 步驟 hello 「 清除您的 Azure 帳戶 」 一節中的這篇文章的 hello 結尾，如此您就可以進行 hello 充分利用 Azure 信用額度。

## <a name="provision-azure-resources-required-for-hello-tutorial"></a>佈建 Azure hello 教學課程所需的資源
本教學課程需要兩個事件中樞 tooreceive*項目*和*結束*資料流。 Azure SQL Database 輸出 hello hello 資料流分析工作的結果。 Azure 儲存體會儲存車輛登記的相關參考資料。

您可以使用 hello Setup.ps1 指令碼在 hello TollApp 資料夾 GitHub toocreate 上所有必要的資源。 在 hello 感興趣的時間，我們建議您執行。 如果您想要深入了解如何 tooconfigure hello Azure 入口網站中的這些資源，請參閱 toolearn toohello < 在 Azure 入口網站中設定資源教學課程 > 的附錄。

下載並儲存 hello 支援[TollApp](https://github.com/Azure/azure-stream-analytics/blob/master/Samples/TollApp/TollApp.zip)資料夾和檔案。

請*以系統管理員的身分*開啟 [Microsoft Azure PowerShell]。 如果您還沒有 Azure PowerShell，請依照下列中的 hello 指示[安裝和設定 Azure PowerShell](/powershell/azure/overview) tooinstall 它。

因為 Windows 會自動封鎖.ps1、.dll 和.exe 檔案，然後再執行 hello 指令碼需要 tooset hello 執行原則。 請確定 hello Azure PowerShell 視窗執行*身為系統管理員*。 請執行 **Set-ExecutionPolicy unrestricted**。 在出現提示時按下 Y 鍵 。

!["Set-ExecutionPolicy unrestricted" 正在 Azure PowerShell 視窗中執行的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image2.png)

執行**Get-executionpolicy** toomake 確定 hello 命令處理。

!["Get-ExecutionPolicy" 正在 Azure PowerShell 視窗中執行的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image3.png)

移 toohello 目錄具有 hello 指令碼和產生器應用程式。

![「 Cd.\TollApp\TollApp"hello Azure PowerShell 視窗中執行的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image4.png)

型別**。\\Setup.ps1** tooset 註冊 Azure 帳戶、 建立和設定所有必要的資源，並開始 toogenerate 事件。 hello 指令碼隨機挑選區域 toocreate 您的資源。 tooexplicitly 指定地區，您可以傳遞 hello **-位置**參數如 hello 下列範例所示：

**.\\Setup.ps1 -location “Central US”**

![Hello Azure 登入頁面的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image5.png)

hello 指令碼會開啟 hello**登入**Microsoft azure 的頁面。 請輸入您的帳戶認證。

> [!NOTE]
> 如果您的帳戶有存取 toomultiple 訂閱，您會想 toouse hello 教學課程的問的 tooenter hello 訂用帳戶名稱。
> 
> 

hello 指令碼可能需要幾分鐘的時間 toorun。 完成之後，hello 輸出看起來應該像下列螢幕擷取畫面的 hello。

![在 hello Azure PowerShell 視窗中的 hello 指令碼的輸出的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image6.PNG)

您也會看到類似下列螢幕擷取畫面的 toohello 另一個視窗。 此應用程式傳送事件 tooAzure 事件中心，也就必要的 toorun hello 教學課程。 因此，請勿停止 hello 應用程式或關閉此視窗，直到您完成 hello 教學課程。

![「正在傳送事件中樞資料」的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image7.png)

您應該能夠 toosee 資源在 Azure 入口網站現在。 跳過<https://portal.azure.com>，並以您的帳戶認證登入。 請注意，目前有些功能會利用 hello 傳統入口網站。 將會清楚指出這些步驟。

### <a name="azure-event-hubs"></a>Azure 事件中心
在 hello Azure 入口網站，按一下 **更多服務**上 hello hello 左的管理 窗格的底部。 型別**事件中心**在 hello 提供欄位，然後按一下**事件中心**。 這會啟動新的瀏覽器視窗 toodisplay hello **SERVICE BUS**  區域中 hello**傳統入口網站**。 您可以在這裡看到 hello hello Setup.ps1 指令碼所建立的事件中樞。

![服務匯流排](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image8.png)

按一下它的開頭 hello *tolldata*。 按一下 hello**事件中心** 索引標籤。您會在這個命名空間中看到 2 個已建立的事件中樞，分別名為 *entry* 和 *exit*。

![Hello 傳統入口網站中的 [事件中樞] 索引標籤](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image9.png)

### <a name="azure-storage-container"></a>Azure 儲存體容器
1. 返回您的瀏覽器開啟 tooAzure 入口網站中的 toohello 索引標籤。 按一下**儲存體**上 hello hello Azure 入口網站 toosee hello Azure 儲存體容器 hello 教學課程中所使用的左方。
   
    ![儲存體功能表項目](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image11.png)
2. 按一下 hello 開頭的其中一個*tolldata*。 按一下 hello**容器** 索引標籤 toosee hello 建立容器。
   
    ![在 hello Azure 入口網站中 容器 索引標籤](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image10.png)
3. 按一下 hello **tolldata**容器 toosee hello 上傳內含車輛註冊資料的 JSON 檔案。
   
    ![Hello 容器中的 hello registration.json 檔案的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image12.png)

### <a name="azure-sql-database"></a>Azure SQL Database
1. 請返回 toohello Azure 入口網站開啟 hello 瀏覽器中的 hello 第一個索引標籤。 按一下**SQL 資料庫**上的 hello Azure 入口網站 toosee hello SQL database，將用於 hello 教學課程中，按一下左方的 hello **tolldatadb**。
   
    ![Hello 建立 SQL database 的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15.png)
2. 複製 hello 伺服器名稱沒有 hello 連接埠號碼 (*servername*。.database.windows.net，例如)。
    ![Hello 建立 SQL 資料庫 db 的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image15a.png)

## <a name="connect-toohello-database-from-visual-studio"></a>從 Visual Studio 中連接 toohello 資料庫
您可以使用 Visual Studio tooaccess 查詢結果 hello 輸出資料庫中。

從 Visual Studio 中連接 toohello SQL database （hello 目的地）：

1. 開啟 Visual Studio 中，然後再按一下**工具** > **連接 tooDatabase**。
2. 如果畫面出現提示，請按一下 [Microsoft SQL Server]  來做為資料來源。
   
    ![[變更資料來源] 對話方塊](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image16.png)
3. 在 hello**伺服器名稱**欄位中，貼上從 hello Azure 入口網站複製 hello 前一節中的 hello 名稱 (也就是*servername*。.database.windows.net)。
4. 按一下 [使用 SQL Server 驗證] 。
5. 輸入**tolladmin**在 hello**使用者名**欄位和**123toll ！** 在 hello**密碼**欄位。
6. 按一下**選取或輸入資料庫名稱**，然後選取**TollDataDB** hello 資料庫。
   
    ![[新增連線] 對話方塊](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image17.jpg)
7. 按一下 [確定] 。
8. 開啟 [伺服器總管]。
   
    ![Server Explorer](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image18.png)
9. 請參閱 hello TollDataDB 資料庫中的四個資料表。
   
    ![Hello TollDataDB 資料庫中的資料表](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image19.jpg)

## <a name="event-generator-tollapp-sample-project"></a>事件產生器：TollApp 範例專案
自動 hello PowerShell 指令碼會使用 hello TollApp 範例應用程式以開始 toosend 事件。 您不需要任何額外的步驟 tooperform。

不過，如果您有興趣實作詳細資料，您可以找到 hello hello TollApp 應用程式原始碼 GitHub 中[範例/TollApp](https://aka.ms/azure-stream-analytics-toll-source)。

![Visual Studio 中所顯示範例程式碼的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image20.png)

## <a name="create-a-stream-analytics-job"></a>建立串流分析工作
1. 在 hello Azure 入口網站，按一下 hello hello 頁面 toocreate hello 左上角中的綠色加號新的資料流分析工作。 選取 智慧 + 分析，然後按一下串流分析作業。
   
    ![New button](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image21.png)
2. 提供作業名稱、 驗證 hello 訂用帳戶均正確無誤，然後建立新的資源群組在 hello 與 hello 事件中樞的儲存體相同區域 （預設值為美國中南部 hello 指令碼）。
3. 按一下**Pin toodashboard**然後**建立**hello hello 頁底端。
   
    ![[建立串流分析工作] 選項](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image22.png)

## <a name="define-input-sources"></a>定義輸入來源
1. hello 作業會建立和開啟 hello 作業頁面。 或者，您可以按一下 hello hello 入口網站儀表板上建立分析工作。

2. 按一下 hello**輸入**toodefine hello 來源資料 索引標籤。
   
    ![hello 輸入 索引標籤](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image24.png)
3. 按一下 [加入輸入] 。
   
    ![hello 新增輸入選項](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image25.png)
4. 輸入 **EntryStream** 做為 [輸入別名]。
5. [來源類型] 是 [資料流]
6. [來源] 是 [事件中樞]。
7. **服務匯流排命名空間**應該的 hello hello TollData 其中一個下拉式清單。
8. **事件中樞名稱**應該設定太**項目**。
9. **事件中樞原則名稱*是**RootManageSharedAccessKey** (hello 預設值)。
10. 選取 [JSON] 做為 [事件序列化格式]，並選取 [UTF8] 做為 [編碼] 格式。
   
    您的設定將看起來會像是：
   
    ![[事件中樞] 設定](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image28.png)

10. 按一下**建立**底部 hello hello 頁 toofinish hello 精靈。
    
    既然您已建立 hello 項目資料流，您將遵循 hello 相同步驟 toocreate hello 結束資料流。 在下列螢幕擷取畫面的 hello 上是確定 tooenter 值。
    
    ![Hello 結束資料流設定](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image31.png)
    
    您已經定義了兩個輸入串流：
    
    ![在 hello Azure 入口網站中定義輸入資料流](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image32.png)
    
    接下來，您將加入包含汽車註冊資料的 hello blob 檔案的參考資料輸入。
11. 按一下**新增**，然後遵循相同程序的 hello 資料流輸入，但選取的 hello**參考資料**而不是**資料流**和 hello**輸入別名**是**註冊**。

12. 按一下開頭為 **tolldata** 的儲存體帳戶。 hello 容器名稱應該是**tolldata**，和 hello**路徑模式**應該**registration.json**。 這個檔案名稱會區分大小寫，且應該是**小寫**。
    
    ![[部落格儲存體] 設定](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image34.png)
13. 按一下**建立**toofinish hello 精靈。

現在，所有輸入都已經定義了。

## <a name="define-output"></a>定義輸出
1. 在 hello 資料流分析作業概觀窗格中，選取 **輸出**。
   
    ![hello 輸出 索引標籤和 加入輸出 選項](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image37.png)
2. 按一下 [新增] 。
3. 設定 hello**輸出別名**too'output' 然後**Sink**太**SQL database**。
3. 選取在 hello hello 文章的 「 從 Visual Studio 連接 tooDatabase 」 一節中的 hello 所使用的伺服器名稱。 hello 資料庫名稱是**TollDataDB**。
4. 輸入**tolladmin**在 hello **USERNAME**  欄位中， **123toll ！** 在 [hello**密碼**] 欄位中，和**TollDataRefJoin**在 hello**資料表**欄位。
   
    ![SQL Database 設定](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image38.png)
5. 按一下 [建立] 。

## <a name="azure-stream-analytics-query"></a>Azure 串流分析查詢
hello**查詢** 索引標籤包含轉換 hello 內送資料的 SQL 查詢。

![查詢加入 toohello 查詢索引標籤](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image39.png)

本教學課程中嘗試的 tooanswer tootoll 資料以及建構資料流分析查詢，其相關的數個商務問題可在 Azure Stream Analytics tooprovide 相關的回應。

在您開始第一個資料流分析工作之前，請讓我們來探索少數的案例和 hello 的查詢語法。

## <a name="introduction-tooazure-stream-analytics-query-language"></a>簡介 tooAzure 串流分析查詢語言
- - -
例如，假設您需要輸入收費亭的車輛 toocount hello 數目。 因為這是連續的資料流的事件，您有 toodefine 」 期間的時間。 」 讓我們來修改 hello 問題 toobe 「 多少車輛輸入收費亭每隔三分鐘？ 」。 這是通常參照的 tooas hello 輪轉計數。

讓我們看看 hello Azure 串流分析查詢，此問題的答案：

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*) AS Count
    FROM EntryStream TIMESTAMP BY EntryTime
    GROUP BY TUMBLINGWINDOW(minute, 3), TollId

如您所見，Azure 串流分析會使用類似 SQL 的查詢語言加入幾個擴充功能 toospecify 時間相關的層面 hello 查詢。

如需詳細資訊，閱讀[時間管理](https://msdn.microsoft.com/library/azure/mt582045.aspx)和[Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx)從 MSDN 的 hello 查詢中使用的建構。

## <a name="testing-azure-stream-analytics-queries"></a>測試 Azure 串流分析查詢
既然您已經撰寫第一個 Azure 資料流分析查詢，它是時間 tootest 它藉由使用範例資料檔案位於下列路徑的 hello 中您 TollApp 資料夾中：

**..\\TollApp\\TollApp\\Data**

此資料夾包含下列檔案的 hello:

* Entry.json
* Exit.json
* registration.json

## <a name="question-1-number-of-vehicles-entering-a-toll-booth"></a>問題 1：進入某個收費亭的車輛數目
1. 開啟 hello Azure 入口網站，並移 tooyour 建立 Azure 資料流分析工作。 按一下 hello**查詢**索引標籤，然後貼上查詢 hello 前一節。

2. toovalidate 這項查詢針對取樣資料，hello EntryStream 輸入，按一下 上傳 hello 資料...hello 符號，然後選取**從檔案的範例資料上傳**。

    ![Hello Entry.json 檔案的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image41.png)
3. 在您本機電腦，並按一下上顯示選取的 hello 檔案 (Entry.json) hello 窗格中**確定**。 hello**測試**圖示現在會在照亮，並能按。
   
    ![Hello Entry.json 檔案的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image42.png)
3. 驗證 hello 查詢的 hello 輸出如預期般：
   
    ![Hello 測試的結果](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image43.png)

## <a name="question-2-report-total-time-for-each-car-toopass-through-hello-toll-booth"></a>問題 2： 報告之每個透過 hello 收費亭的車輛 toopass 時間總計
hello 透過 hello 收費站的汽車 toopass 所需的平均時間有助於 hello 程序和 hello 客戶經驗 tooassess hello 效率。

toofind hello 總時間，您需要 toojoin hello EntryTime 資料流與 hello ExitTime 資料流。 您會加入 hello TollId 且 LicencePlate 資料行上的資料流。 hello**聯結**運算子則需要一個 toospecify 時態彈性以描述 hello 差異 hello 加入事件可接受的時間。 您將使用**DATEDIFF**函式 toospecify 事件應該彼此不超過 15 分鐘。 您也會套用 hello **DATEDIFF**函式 tooexit 和 toocompute hello 實際的時間花在 hello 的汽車時間的項目付費站台。 請注意 hello 用途的 hello 差異**DATEDIFF**使用中時**選取**陳述式而非**聯結**條件。

    SELECT EntryStream.TollId, EntryStream.EntryTime, ExitStream.ExitTime, EntryStream.LicensePlate, DATEDIFF (minute , EntryStream.EntryTime, ExitStream.ExitTime) AS DurationInMinutes
    FROM EntryStream TIMESTAMP BY EntryTime
    JOIN ExitStream TIMESTAMP BY ExitTime
    ON (EntryStream.TollId= ExitStream.TollId AND EntryStream.LicensePlate = ExitStream.LicensePlate)
    AND DATEDIFF (minute, EntryStream, ExitStream ) BETWEEN 0 AND 15

1. tootest 此查詢中，更新 hello 查詢上 hello**查詢**hello 作業。 加入 hello 測試檔案，如**ExitStream**一樣**EntryStream**輸入上方。
   
2. 按一下 [ **測試**]。

3. 選取 [hello] 核取方塊 tootest hello 查詢和檢視表 hello 輸出：
   
    ![Hello 測試的輸出](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image45.png)

## <a name="question-3-report-all-commercial-vehicles-with-expired-registration"></a>問題 3：回報所有車輛登記已過期的商用車
Azure Stream Analytics 可以暫時資料資料流使用資料 toojoin 靜態快照的集。 toodemonstrate 這項功能，使用 hello 遵循範例問題。

如果與 hello 通行費管理公司註冊商用車輛，它可以通過 hello 收費亭不需停車檢查。 您將使用商用車輛註冊查閱資料表 tooidentify 所有註冊過期的商用車輛。

```
SELECT EntryStream.EntryTime, EntryStream.LicensePlate, EntryStream.TollId, Registration.RegistrationId
FROM EntryStream TIMESTAMP BY EntryTime
JOIN Registration
ON EntryStream.LicensePlate = Registration.LicensePlate
WHERE Registration.Expired = '1'
```

tootest 使用參考資料的查詢，您會需要 toodefine 輸入來源 hello 參考資料，您已經完成。

tootest 此查詢中，貼上 hello 查詢貼入 hello**查詢**索引標籤上，按一下 **測試**，並指定 hello 兩個輸入的來源並 hello 註冊範例資料，然後按一下**測試**。  
   
![Hello 測試的輸出](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image46.png)

## <a name="start-hello-stream-analytics-job"></a>啟動 hello 資料流分析工作
現在它是時間 toofinish hello 設定和開始 hello 作業。 問題 3，會產生相符項目 hello hello 的結構描述的輸出儲存 hello 查詢**TollDataRefJoin**輸出資料表。

移 toohello 作業**儀表板**，然後按一下**啟動**。

![Hello 作業儀表板中的 hello 開始 按鈕的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image48.png)

在 hello 開啟對話方塊，變更 hello**開始輸出**時間太**自訂時間**。 變更 hello 小時 tooone 小時 hello 目前時間之前。 這項變更可確保您在 hello 教學課程的 hello 開頭開始 toogenerate hello 事件之後處理的 hello 事件中心的所有事件。 現在按一下 hello**啟動**按鈕 toostart hello 作業。

![自訂時間的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image49.png)

開始 hello 工作可能需要幾分鐘的時間。 您可以在資料流分析的 hello 最上層頁面上查看 hello 狀態。

![Hello hello 工作狀態的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image50.png)

## <a name="check-results-in-visual-studio"></a>在 Visual Studio 中查看結果
1. 開啟 Visual Studio 伺服器總管 中，並以滑鼠右鍵按一下 hello **TollDataRefJoin**資料表。
2. 按一下**顯示資料表資料**toosee hello 輸出的工作。
   
    ![伺服器總管中 [顯示資料表資料] 的選取項目](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image51.jpg)

## <a name="scale-out-azure-stream-analytics-jobs"></a>相應放大 Azure 串流分析工作
Azure Stream Analytics 設計 tooelastically 調整，好讓它可以處理大量資料。 hello Azure Stream Analytics 查詢就可以使用**PARTITION BY**子句 tootell hello 系統，此步驟會向外延展。**PartitionId**在於 hello 系統的特殊資料行加入 toomatch hello 資料分割識別碼 hello 輸入 （事件中心）。

    SELECT TollId, System.Timestamp AS WindowEnd, COUNT(*)AS Count
    FROM EntryStream TIMESTAMP BY EntryTime PARTITION BY PartitionId
    GROUP BY TUMBLINGWINDOW(minute,3), TollId, PartitionId

1. 停止 hello 目前的工作，在 hello 更新 hello 查詢**查詢**索引標籤，然後開啟 hello**設定**齒輪 hello 作業儀表板中。 按一下 [調整] 。
   
    **串流單位**定義可以收到 hello 數量 hello 工作的運算能力。
2. 變更 hello 下拉式清單從 6 1。
   
    ![選取 6 個串流處理單位的螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/image52.png)
3. 移 toohello**輸出**索引標籤，然後變更 hello hello SQL 資料表名稱太**TollDataTumblingCountPartitioned**。

如果您啟動 hello 作業現在，Azure Stream Analytics 中可以將工作分散到運算資源就愈，達到更佳的輸送量。 請注意該 hello TollApp 應用程式也會傳送事件的 TollId 來分割。

## <a name="monitor"></a>監視
hello**監視器**區域包含正在執行工作的 hello 相關統計資料。 第一次設定時所需的 hello toouse hello 儲存體帳戶相同的區域 （例如 hello 這份文件其餘部分的名稱付費電話）。   

![監視螢幕擷取畫面](media/stream-analytics-build-an-iot-solution-using-stream-analytics/monitoring.png)

您可以存取**活動記錄**從 hello 作業儀表板**設定**以及區域。


## <a name="conclusion"></a>結論
本教學課程會引進 toohello Azure Stream Analytics 服務。 它所示範的 tooconfigure 輸入和輸出 hello 資料流分析工作。 Hello 教學課程使用 hello 付費資料案例，說明常見的 hello 空間中的資料移動，以及如何解決使用簡單的類似 SQL 的查詢，在 Azure Stream Analytics 中發生的問題。 hello 教學課程所述使用暫存資料的 SQL 延伸模組建構。 它示範了如何 toojoin 資料流，tooenrich hello 資料流與靜態參考資料，以及如何 tooscale 出查詢 tooachieve 更高的輸送量。

雖然本教學課程提供了詳盡的簡介，但也絕對不算是完整的說明。 您可以找到多個查詢模式使用在 hello SAQL 語言[查詢常見的資料流分析使用模式的範例](stream-analytics-stream-analytics-query-patterns.md)。
請參閱 toohello[線上文件](https://azure.microsoft.com/documentation/services/stream-analytics/)toolearn 深入了解 Azure Stream Analytics。

## <a name="clean-up-your-azure-account"></a>清理您的 Azure 帳戶
1. 停止 hello hello Azure 入口網站中的資料流分析工作。
   
    hello Setup.ps1 指令碼會建立兩個事件中心 」 和 「 SQL 資料庫。 下列指示說明清除資源在 hello hello 教學課程結尾處的 hello。
2. 在 PowerShell 視窗中，輸入**。\\Cleanup.ps1** toostart hello 指令碼，以刪除 hello 教學課程中使用的資源。
   
   > [!NOTE]
   > Hello 名稱所識別的資源。 請確認您在確認刪除之前，已仔細檢閱每個項目。
   > 
   > 


