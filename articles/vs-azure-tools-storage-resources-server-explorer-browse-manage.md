---
title: "aaaBrowsing 和管理存放裝置資源，使用伺服器總管 |Microsoft 文件"
description: "使用伺服器總管瀏覽和管理儲存體資源"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 658dc064-4a4e-414b-ae5a-a977a34c930d
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/24/2017
ms.author: kraigb
ms.openlocfilehash: f5b456b812f2ad8103c50538d532a57397bcccbb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="browsing-and-managing-storage-resources-with-server-explorer"></a>使用伺服器總管瀏覽和管理儲存體資源
[!INCLUDE [storage-try-azure-tools](../includes/storage-try-azure-tools.md)]

## <a name="overview"></a>概觀
如果您已安裝 hello Azure Tools for Microsoft Visual Studio，您可以檢視 blob、 佇列和資料表資料儲存體帳戶從 azure。 在伺服器總管 中的 hello Azure 儲存體節點顯示您的本機儲存體模擬器帳戶和其他 Azure 儲存體帳戶中的資料。

tooview 在 Visual Studio 伺服器總管 hello 功能表列上，選擇**檢視**，**伺服器總管**。 hello 存放裝置 節點會顯示所有的 hello 存在每個 Azure 訂用帳戶/憑證您已經連接到下的儲存體帳戶。 如果儲存體帳戶未出現，您可以將它加入 hello 指示[本主題稍後](#add-storage-accounts-by-using-server-explorer)。

您也可以從 Azure SDK 2.7 開始，使用新 Cloud Explorer tooview hello 和管理您的 Azure 資源。 如需詳細資訊，請參閱 [使用雲端總管管理 Azure 資源](vs-azure-tools-resources-managing-with-cloud-explorer.md) 。

## <a name="view-and-manage-storage-resources-in-visual-studio"></a>檢視和管理 Visual Studio 中的儲存體資源
[伺服器總管] 會自動在您的儲存體模擬器帳戶中顯示 blob、佇列和資料表的清單。 伺服器總管中列出 hello 儲存體模擬器帳戶下 hello 儲存節點做 hello**開發**節點。

toosee hello 儲存體模擬器帳戶的資源中，展開 hello**開發**節點。 當您展開 hello 如果尚未開啟 hello 儲存體模擬器**開發** 節點，就會自動開始。 這可能需要數秒鐘的時間。 Hello 儲存體模擬器啟動時，您可以繼續 toowork Visual Studio 的其他區域中。

tooview 資源儲存體帳戶中，展開 [伺服器總管] 中的 hello 儲存體帳戶的節點。 此時會出現下列子節點的 hello:

* Blob
* 佇列
* 資料表

## <a name="work-with-blob-resources"></a>使用 Blob 資源
hello Blob 節點顯示 hello 選取儲存體帳戶的容器清單。 Blob 容器包含 blob 檔案，您可以將這些 blob 組織成資料夾和子資料夾。 請參閱[如何從.NET 的 Blob 儲存體 toouse](storage/blobs/storage-dotnet-how-to-use-blobs.md)如需詳細資訊。

### <a name="toocreate-a-blob-container"></a>toocreate blob 容器
1. 開啟 hello hello 的捷徑功能表**Blob** ] 節點，然後選擇 [**建立 Blob 容器**。
2. 在 hello**建立 Blob 容器**對話方塊方塊中，輸入 hello hello 新容器名稱。  
3. 按**ENTER**上鍵盤，或者您可以按一下或點選 hello 名稱欄位 toosave hello blob 容器之外。
   
   > [!NOTE]
   > hello blob 容器名稱必須以數字 (0-9) 或小寫字母 (a-z) 開頭。
   > 
   > 

### <a name="toodelete-a-blob-container"></a>toodelete blob 容器
* 開啟 hello hello blob 容器，您想 tooremove，然後選擇捷徑功能表**刪除**。

### <a name="toodisplay-a-list-of-hello-items-contained-in-a-blob-container"></a>toodisplay hello 項目清單所包含的 blob 容器中
* 開啟 hello 清單中的 hello blob 容器名稱的捷徑功能表，然後選擇**開啟**。
  
    當您檢視 blob 容器的 hello 內容時，它會出現稱為 hello blob 容器檢視的索引標籤中。
  
    ![VST_SE_BlobDesigner](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC749016.png)
  
    您可以執行下列 blob 上的作業使用 hello 按鈕 hello hello blob 容器檢視右上角中的 hello:
  
  * 輸入篩選值並加以套用
  * 重新整理 hello hello 容器中的 blob 清單
  * 上傳檔案
  * 刪除 Blob
    
    > [!NOTE]
    > 從 blob 容器中刪除檔案並不會刪除 hello 基礎檔案。它只會移除它從 hello blob 容器。
    > 
    > 
  * 開啟 blob
  * 儲存 blob toohello 本機電腦

### <a name="toocreate-a-folder-or-subfolder-in-a-blob-container"></a>toocreate 資料夾或子資料夾中的 blob 容器
1. 選擇在 Cloud Explorer 中的 hello blob 容器。 在 hello 容器視窗中，選擇 hello**上傳 Blob**  按鈕。
   
    ![將檔案上傳至 blob 資料夾](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766037.png)
2. 在 hello**上傳新的檔案**對話方塊方塊中，選擇 hello**瀏覽**按鈕 toospecify hello 檔案您想 tooupload，，然後輸入 hello 中的 資料夾名稱**資料夾 （選擇性）**方塊.
   
    您可以將遵循的容器資料夾中的子資料夾 hello 相同程序。 如果您未指定資料夾名稱，將會 hello 檔案上傳 toohello hello blob 容器的頂部層級。 hello 檔案會出現在 hello hello 容器中指定的資料夾。
   
    ![資料夾加入 tooa blob 容器](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766038.png)
3. 按兩下 [hello] 資料夾，或按下 ENTER toosee hello 內容 hello 資料夾。 當您準備 hello 容器資料夾中時，您可以瀏覽的 hello 容器後 toohello 根選擇 hello**開啟上層目錄**（向上箭頭） 按鈕。

### <a name="toodelete-a-container-folder"></a>toodelete 容器資料夾
* 刪除所有 hello 資料夾中的 hello 檔案
  
  > [!NOTE]
  > Blob 容器中的資料夾是虛擬資料夾，因為您無法建立空的資料夾，也可以刪除資料夾 toodelete 其檔案內容。 您有 toodelete hello 整個資料夾 toodelete hello 資料夾內容。
  > 
  > 

### <a name="toofilter-blobs-in-a-container"></a>toofilter blob 容器中
您可以篩選會顯示藉由指定通用的前置詞的 hello blob。

例如，如果您輸入 hello 前置詞`hello`在 hello 篩選] 文字方塊，然後選擇 [hello **Execute** (**！**)按鈕，以 'hello' 開頭的 blob 會出現。

![VST_SE_FilterBlobs](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC519076.png)

> [!NOTE]
> hello 篩選欄位會區分大小寫，且不支援使用萬用字元進行篩選。 Blob 只可以利用前置詞篩選。 如果您使用分隔符號 tooorganize blob 以虛擬階層 hello 前置詞可能包含分隔符號。 例如，篩選 hello 前置詞 HelloFabric/會傳回所有以該字串開頭的 blob。
> 
> 

### <a name="toodownload-blob-data"></a>toodownload blob 資料
* 在**Cloud Explorer**，開啟一個或多個 blob 的 hello 捷徑功能表，然後選擇**開啟**，或選擇 hello blob 名稱，然後選擇 hello**開啟**按鈕，或按兩下hello blob 名稱。
  
    hello blob 下載進度會顯示在 hello **Azure 活動記錄檔**視窗。
  
    hello blob 會在 hello 該檔案類型的預設編輯器中開啟。 Hello 作業系統辨識出 hello 檔案類型，若 hello 檔案會開啟在本機安裝的應用程式。否則，系統會提示您 toochoose 適合 hello blob hello 檔案類型的應用程式。 hello 下載 blob 時所建立的本機檔案會標示為唯讀。
  
    Blob 資料是在本機快取和 blob 的上次修改的時間 hello Blob 服務在經過 hello。 如果 hello blob 已更新上次下載之後，它將會再次下載。否則，會從 hello 本機磁碟載入 hello blob。 根據預設，blob 是下載的 tooa 暫存目錄。 blob 名稱 toodownload blob tooa 特定目錄中，開啟 hello hello 選取捷徑功能表，然後選擇 **存**。 當您以這種方式儲存 blob 時，hello blob 檔案尚未開啟，並建立 hello 本機檔案具有讀寫屬性。

### <a name="tooupload-blobs"></a>tooupload blob
* 選擇 hello**上傳 Blob**按鈕 hello 容器開啟以供在 hello blob 容器檢視中檢視時。
  
    您可以選擇其中一個或多個檔案 tooupload，而且您可以上傳任何類型的檔案。 hello **Azure 活動記錄檔**顯示 hello 的 hello 上傳進度。 如需有關如何 toowork blob 資料，請參閱[toouse hello.net 的 Azure Blob 儲存體服務的方式](http://go.microsoft.com/fwlink/p/?LinkId=267911)。

### <a name="tooview-logs-transferred-tooblobs"></a>傳輸 tooblobs tooview 記錄檔。
* 如果您從 Azure 應用程式使用 Azure 診斷 toolog 資料，並且已傳輸記錄檔 tooyour 儲存體帳戶，您會看到由 Azure 為這些記錄建立的容器。 在伺服器總管中檢視這些記錄檔是您的應用程式輕鬆 tooidentify 問題，特別是當它已部署的 tooAzure。 如需 Azure 診斷的詳細資訊，請參閱 [使用 Azure 診斷收集記錄資料](https://msdn.microsoft.com/library/azure/gg433048.aspx)。

### <a name="tooget-hello-url-for-a-blob"></a>blob 的 tooget hello URL
* 開啟 hello blob 的捷徑功能表，然後選擇**複製 URL**。

### <a name="tooedit-a-blob"></a>tooedit blob
* 選取 hello blob，然後選擇 [hello**開啟 Blob** ] 按鈕。
  
    hello 檔案下載的 tooa 暫存位置，並開啟 hello 本機電腦上。 您必須再次上傳 hello blob 進行變更之後。

## <a name="work-with-queue-resources"></a>使用佇列資源
儲存體服務佇列裝載於 Azure 儲存體帳戶，您可以使用這些 tooallow 您雲端服務的角色有 toocommunicate 與彼此、 與其他服務的訊息傳遞機制。 您可以透過雲端服務，並透過外部用戶端的 web 服務以程式設計方式存取 hello 佇列。 您也可以使用 Visual Studio 中的伺服器總管 來直接存取 hello 佇列。

當您開發使用佇列的雲端服務時，您可能會想 toouse Visual Studio toocreate 佇列，並使用它們以互動方式在您開發並測試您的程式碼。

在伺服器總管 中，您可以檢視儲存體帳戶中的 hello 佇列、 建立和刪除佇列、 開啟佇列 tooview 其訊息，並加入訊息 tooa 佇列。 當您開啟佇列進行檢視時，您可以檢視個別的 hello 訊息，以及您可以執行下列動作 hello 佇列上，使用 hello 按鈕 hello 左上角中的 hello:

* 重新整理 hello 佇列的 hello 檢視
* 新增訊息 toohello 佇列
* 清除佇列 hello 最上層訊息
* 清除 hello 整個佇列

hello 下列影像顯示包含兩個訊息的佇列。

![檢視佇列](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC651470.png)

如需有關儲存體服務佇列，請參閱[How to： 使用 hello 佇列儲存體服務](http://go.microsoft.com/fwlink/?LinkID=264702)。 如需 hello web 服務的儲存體服務佇列，請參閱[佇列服務概念](http://go.microsoft.com/fwlink/?LinkId=264788)。 如需 toosend 訊息 tooa 儲存體服務佇列使用 Visual Studio 的如何資訊，請參閱[傳送訊息 tooa 儲存體服務佇列](https://msdn.microsoft.com/library/azure/jj649344.aspx)。

> [!NOTE]
> 儲存體服務佇列與服務匯流排佇列不同。 如需服務匯流排佇列的詳細資訊，請參閱服務匯流排佇列、主題和訂用帳戶。
> 
> 

## <a name="work-with-table-resources"></a>使用資料表資源
hello Azure 資料表儲存體服務儲存大量結構化資料。 hello 服務是可接受的 NoSQL 資料存放區驗證呼叫從內部和外部 hello Azure 雲端。 Azure 資料表很適合儲存結構化、非關聯式資料。

### <a name="toocreate-a-table"></a>toocreate 資料表
1. 在 Cloud Explorer 中選取 hello**資料表**節點 hello 儲存體帳戶，，然後選擇  **Create Table**。
2. 在 hello **Create Table**對話方塊方塊中，輸入 hello 資料表的名稱。

### <a name="tooview-table-data"></a>tooview 資料表資料
1. 在 Cloud Explorer 中開啟 hello **Azure**節點，然後再開啟 hello**儲存體**節點。
2. 開啟 hello 的儲存體帳戶節點您感興趣，，，然後開啟 hello**資料表**節點 toosee hello 儲存體帳戶的表格清單。
3. 開啟 hello 資料表的捷徑功能表，然後選擇**檢視資料表**。
   
    ![方案總管中的 Azure 資料表](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744165.png)

hello 表格被依照 （顯示為資料列） 的實體和屬性 （資料行中顯示）。 例如，下列圖例 hello 顯示 hello 中列出實體**資料表設計工具**:

### <a name="tooedit-table-data"></a>tooedit 資料表資料
1. 在 hello**資料表設計工具**，開啟 hello 實體 （單一資料列） 或屬性 （單一儲存格） 的捷徑功能表，然後選擇**編輯**。
   
    ![新增或編輯資料表實體](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC656238.png)
   
    單一資料表中的實體不是必要的 toohave hello 相同設定的屬性 （資料行）。 請注意 hello 遵循上檢視及編輯資料表資料的限制。
   
   * 您無法檢視或編輯二進位資料 (位元組類型)，但您可以將其儲存在資料表中。
   * 您無法編輯 hello **PartitionKey**或**RowKey**值，因為在 Azure 中的資料表儲存體不支援這項操作。
   * 您無法建立名為 Timestamp 的屬性，Azure 儲存體服務會使用該名稱的屬性。
   * 如果您輸入的日期時間值，您必須依照您的電腦的適當 toohello 地區和語言設定的格式 (例如，MM/DD/YYYY hh: mm: [AM |PM] 美國地區英文)。

### <a name="tooadd-entities"></a>tooadd 實體
1. 在 [hello**資料表設計工具**，選擇 hello**加入實體**] 按鈕。
   
    ![新增實體](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655336.png)
2. 在 hello**加入實體**對話方塊方塊中，輸入 hello hello 值**PartitionKey**和**RowKey**屬性。
   
    ![新增實體對話方塊](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655335.png)
   
    請仔細輸入 hello 值，因為您無法在關閉 hello 對話方塊中，除非您刪除 hello 實體，並將它重新加入之後變更它們。

### <a name="toofilter-entities"></a>toofilter 實體
您可以自訂 hello 出現在資料表中，如果您使用 hello 查詢產生器的實體集。

1. tooopen hello 查詢產生器中，開啟任一表格進行檢視。
2. 選擇 hello hello 資料表檢視的工具列上的查詢產生器 按鈕。
   
    hello**查詢產生器** 對話方塊隨即出現。 hello 如下圖所顯示的查詢正在建立 hello 查詢產生器中。
   
    ![查詢產生器](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC652231.png)
3. 當您完成建立 hello 查詢，關閉 [hello] 對話方塊。 hello 產生的文字格式的 hello 查詢會顯示在文字方塊中，為 WCF Data Services 篩選器。
4. toorun hello 查詢中，選擇 hello 綠色的三角形圖示。
   
    您也可以篩選出現在 hello 中的實體資料**資料表設計工具**如果您直接在 hello 篩選欄位中輸入 WCF Data Services 篩選條件字串。 這類字串類似 tooa SQL WHERE 子句，但會以 HTTP 要求傳送 toohello 伺服器。 如需如何 tooconstruct 篩選字串資訊，請參閱[hello 資料表設計工具建構篩選字串](https://msdn.microsoft.com/library/azure/ff683669.aspx)。
   
    hello 下圖顯示有效的篩選字串的範例：
   
    ![VST_SE_TableFilter](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC655337.png)

### <a name="refresh-storage-data"></a>重新整理儲存體資料
當伺服器總管 連接 tooor 取得資料時從儲存體帳戶時，就可能會在 hello 作業 toocomplete tooa 分鐘。 如果它無法連接，hello 作業可能會逾時。擷取資料時，您可以繼續在 Visual Studio 的其他部分 toowork。 如果費時太久，toocancel hello 作業選擇 hello**停止重新整理**hello 伺服器總管 工具列上的按鈕。

#### <a name="toorefresh-blob-container-data"></a>toorefresh blob 容器資料
* 選取 hello **Blob**下方的節點**儲存體**選擇 hello**重新整理**hello 伺服器總管 工具列上的按鈕。
* toorefresh hello 的 blob 清單，會顯示選擇 hello **Execute**  按鈕。

#### <a name="toorefresh-table-data"></a>toorefresh 資料表資料
* 選取 hello**資料表**下方的節點**儲存體**選擇 hello**重新整理** 按鈕。
* 實體的 toorefresh hello 清單，會顯示在 hello**資料表設計工具**，選擇 hello **Execute**按鈕 hello**資料表設計工具**。

#### <a name="toorefresh-queue-data"></a>toorefresh 佇列資料
* 選取 hello**佇列** 節點，然後選擇 hello**重新整理** 按鈕。

#### <a name="toorefresh-all-items-in-a-storage-account"></a>toorefresh 儲存體帳戶中的所有項目
* 選擇 hello 帳戶名稱，然後選擇 [hello**重新整理**hello 工具列上的伺服器總管] 按鈕。

### <a name="add-storage-accounts-by-using-server-explorer"></a>使用 [伺服器總管] 新增儲存體帳戶
有兩種方式 tooadd 儲存體帳戶使用 [伺服器總管]。 您可以在您的 Azure 訂用帳戶中建立新的儲存體帳戶，或者您可以附加現有的儲存體帳戶。

#### <a name="toocreate-a-new-storage-account-by-using-server-explorer"></a>toocreate 新的儲存體帳戶，使用伺服器總管
1. 在伺服器總管 中，開啟 hello hello 存放裝置 節點的捷徑功能表，然後選擇建立儲存體帳戶。
   
    ![建立新的 Azure 儲存體帳戶](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC744166.png)
2. 選取或輸入下列資訊在 hello hello 新儲存體帳戶的 hello**建立儲存體帳戶** 對話方塊。
   
   * hello Azure 訂用帳戶 toowhich 想 tooadd hello 儲存體帳戶。
   * 您要新增儲存體帳戶 hello toouse hello 名稱。
   * hello 地區或同質群組 （例如美國西部或東亞）。
   * hello 類型的複寫想 toouse hello 儲存體帳戶，例如 異地備援。
3. 選擇 [建立] 。
   
    hello 新儲存體帳戶會出現在 hello**儲存體**方案總管 中的清單。

#### <a name="tooattach-an-existing-storage-account-by-using-server-explorer"></a>tooattach 現有的儲存體帳戶使用伺服器總管
1. 在 [伺服器總管] 中，開啟 hello hello Azure 儲存體] 節點的捷徑功能表，然後選擇 [**附加外部儲存體**。
   
    ![新增現有的儲存體帳戶](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766039.png)
2. 選取或輸入下列資訊在 hello hello 新儲存體帳戶的 hello**建立儲存體帳戶** 對話方塊。
   
   * hello hello 想 tooattach 現有儲存體帳戶名稱。 您可以輸入的名稱，或從 hello 清單中選取。
   * hello hello 索引鍵選取儲存體帳戶。 當您選取儲存體帳戶時，通常會提供這個值給您。 如果您希望 Visual Studio tooremember hello 儲存體帳戶金鑰，請選取 hello 記住帳戶金鑰 方塊。
   * hello 通訊協定 toouse tooconnect toohello 儲存體帳戶，例如 HTTP、 HTTPS 或自訂端點。 請參閱[如何 tooConfigure 連接字串](https://msdn.microsoft.com/library/azure/ee758697.aspx)如需有關自訂端點。

### <a name="tooview-hello-secondary-endpoints"></a>tooview hello 次要端點
* 如果您建立儲存體帳戶使用 hello**讀取存取異地備援**複寫選項，您可以檢視其次要端點。 開啟 hello hello 帳戶名稱的捷徑功能表，然後選擇**屬性**。
  
    ![儲存體次要端點](./media/vs-azure-tools-storage-resources-server-explorer-browse-manage/IC766040.png)

### <a name="tooremove-a-storage-account-from-server-explorer"></a>tooremove 儲存體帳戶，從 伺服器總管
* 在 伺服器總管 中，開啟 hello hello 帳戶名稱的捷徑功能表，然後選擇 **刪除**。 如果您刪除儲存體帳戶，也會移除該帳戶的所有已儲存金鑰資訊。
  
  > [!NOTE]
  > 如果您從 [伺服器總管] 刪除儲存體帳戶，它不會影響您的儲存體帳戶或任何內含的資料只會從伺服器總管移除 hello 參考。 toopermanently 刪除儲存體帳戶，請使用 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。
  > 
  > 

## <a name="next-steps"></a>後續步驟
toolearn 進一步了解如何使用 Azure 儲存體服務，請參閱[存取 hello Azure 儲存體服務](https://msdn.microsoft.com/library/azure/ee405490.aspx)。

