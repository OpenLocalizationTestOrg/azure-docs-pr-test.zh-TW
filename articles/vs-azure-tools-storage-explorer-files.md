---
title: "aaaUsing Azure 檔案儲存體的儲存體總管 （預覽） |Microsoft 文件"
description: "深入了解如何了解如何 toouse 存放裝置總管 （預覽） toowork 與檔案共用和檔案。"
services: storage
documentationcenter: na
author: cawaMS
manager: paulyuk
editor: 
ms.assetid: 
ms.service: storage
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/09/2017
ms.author: cawa
ms.openlocfilehash: 98eb3cde711ae3dbfdb6ffaec23ae24f822370e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="using-storage-explorer-preview-with-azure-file-storage"></a>搭配使用儲存體 Explorer (預覽) 與 Azure 檔案儲存體

Azure 儲存體是一項服務，提供檔案共用中 hello 雲端使用的檔案 hello 標準伺服器訊息區塊 (SMB) 通訊協定。 SMB 2.1 和 SMB 3.0 皆受到支援。 使用 Azure 檔案儲存體，您可以移轉依賴檔案共用 tooAzure 快速且不昂貴的撰寫的舊版應用程式。 您可以使用檔案儲存體 tooexpose 資料公開 toohello 世界中或 toostore 應用程式資料未公開。 在本文中，您將學習如何 toouse 存放裝置總管 （預覽） toowork 與檔案共用和檔案。

## <a name="prerequisites"></a>必要條件

toocomplete hello 本文中的步驟，您將需要下列 hello:

- [下載並安裝儲存體 Explorer (預覽)](http://www.storageexplorer.com/)

- [連接 tooa Azure 儲存體帳戶或服務](https://docs.microsoft.com//azure/vs-azure-tools-storage-manage-with-storage-explorer#connect-to-a-storage-account-or-service)

## <a name="create-a-file-share"></a>建立檔案共用

所有檔案必須都位於檔案共用，這是檔案的邏輯群組。 帳戶可以包含無限數量的檔案共用，每個共用可以儲存無限數量的檔案。

hello 下列步驟說明如何 toocreate 檔案共用儲存體總管 （預覽） 內。

1. 開啟儲存體 Explorer (預覽)。

2. Hello 左窗格中，展開要在其中 toocreate hello 檔案共用的 hello 儲存體帳戶

3. 以滑鼠右鍵按一下**檔案共用**，和-hello 操作功能表： 從選取**建立檔案共用**。

    ![建立檔案共用](media/vs-azure-tools-storage-explorer-files/image1.png)

4. 文字會出現一個方塊下方 hello**檔案共用**資料夾。 輸入 hello 檔案共用的名稱。 請參閱 hello[共用命名規則](https://docs.microsoft.com//azure/storage/storage-dotnet-how-to-use-blobs#create-a-container)一節，以清單規則以及限制命名的檔案共用。

    ![命名 hello 共用](media/vs-azure-tools-storage-explorer-files/image2.png)

5. 按**Enter**時完成的 toocreate hello 檔案共用或**Esc** toocancel。 一旦已成功建立 hello 檔案共用，它就會顯示在 hello**檔案共用**hello 資料夾選取儲存體帳戶。

    ![hello 新的共用](media/vs-azure-tools-storage-explorer-files/image3.png)

## <a name="view-a-file-shares-contents"></a>檢視檔案共用的內容

檔案共用包含檔案和資料夾 (也包含檔案)。

hello 下列步驟說明如何 tooview hello 檔案內容的共用存放裝置總管 （預覽） 中: +

1. 開啟儲存體 Explorer (預覽)。

2. Hello 左窗格中，展開包含您想 tooview hello 檔案共用的 hello 儲存體帳戶。

3. 展開 hello 儲存體帳戶的**檔案共用**。

4. 以滑鼠右鍵按一下 hello 檔案共用您想 tooview，和-hello 操作功能表： 從選取**開啟**。 您也可以按兩下您想 tooview hello 檔案共用。

    ![開啟共用](media/vs-azure-tools-storage-explorer-files/image4.png)

5. hello 主窗格會顯示 hello 檔案共用的內容。
    
    ![hello 共用的內容](media/vs-azure-tools-storage-explorer-files/image5.png)

## <a name="delete-a-file-share"></a>刪除檔案共用

檔案共用可以輕鬆地建立並視需要刪除。 (toosee toodelete 個別檔案，請參閱 toohello 區段中，如何[管理檔案共用中的檔案](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container)。)

hello 下列步驟說明如何 toodelete 檔案共用儲存體總管 （預覽） 中所示：

1. 開啟儲存體 Explorer (預覽)。

2. Hello 左窗格中，展開包含您想 tooview hello 檔案共用的 hello 儲存體帳戶。

3. 展開 hello 儲存體帳戶的**檔案共用**。

4. 以滑鼠右鍵按一下 hello 檔案共用您想 toodelete，和-hello 操作功能表： 從選取**刪除**。 您也可以按**刪除**toodelete hello 目前選取的檔案共用。

    ![刪除](media/vs-azure-tools-storage-explorer-files/image6.png)

5. 選取**是**toohello 確認對話方塊。
    
    ![確認對話方塊](media/vs-azure-tools-storage-explorer-files/image7.png)

## <a name="copy-a-file-share"></a>複製檔案共用

儲存體總管 （預覽） 可讓您 toocopy 檔案共用 toohello 剪貼簿，然後將該檔案共用貼到另一個儲存體帳戶。 (toosee toocopy 個別檔案，請參閱 toohello 區段中，如何[管理檔案共用中的檔案](https://docs.microsoft.com//azure/vs-azure-tools-storage-explorer-blobs#managing-blobs-in-a-blob-container)。)

hello 下列步驟說明從一個儲存體帳戶 tooanother toocopy 檔案共用的方式。

1. 開啟儲存體 Explorer (預覽)。

2. Hello 左窗格中，展開包含您想 toocopy hello 檔案共用的 hello 儲存體帳戶。

3. 展開 hello 儲存體帳戶的**檔案共用**。

4. 以滑鼠右鍵按一下 hello 檔案共用您想 toocopy，和-hello 操作功能表： 從選取**複製的檔案共用**。

    ![複製檔案共用](media/vs-azure-tools-storage-explorer-files/image8.png)

5. 以滑鼠右鍵按一下 hello 所需"target"儲存體帳戶所在 toopaste hello 檔案共用，再-hello 操作功能表： 從選取**貼上檔案共用**。

    ![貼上檔案共用](media/vs-azure-tools-storage-explorer-files/image9.png)

## <a name="get-hello-sas-for-a-file-share"></a>取得檔案共用中的 hello SAS

A[共用的存取簽章 (SAS)](https://docs.microsoft.com//azure/storage/storage-dotnet-shared-access-signature-part-1)提供儲存體帳戶中的委派的存取 tooresources。 這表示您可以授與用戶端在指定期間內的時間與一組指定的權限，在儲存體帳戶的權限 tooobjects 限制而不需要 tooshare 帳戶存取金鑰。

hello 下列步驟說明如何 toocreate SAS，使檔案共用: +

1. 開啟儲存體 Explorer (預覽)。

2. Hello 左窗格中，展開包含您想 tooget SAS hello 檔案共用的 hello 儲存體帳戶。

3. 展開 hello 儲存體帳戶的**檔案共用**。

4. Hello 所需的檔案共用，以滑鼠右鍵按一下和-hello 操作功能表： 從選取**取得共用存取簽章**。

    ![取得共用存取簽章](media/vs-azure-tools-storage-explorer-files/image10.png)

5. 在 [hello**共用存取簽章**] 對話方塊中，指定 hello 原則、 開始和到期日期、 時間區域，然後存取您想要用於 hello 資源層級。

    ![SAS 對話方塊](media/vs-azure-tools-storage-explorer-files/image11.png)

6. 當您完成指定的 hello SAS 選項，選取**建立**。

7. 第二個**共用存取簽章**清單 hello 以及 hello URL 的檔案共用，您可以使用 tooaccess QueryStrings hello 儲存體資源，就會顯示對話方塊。 選取**複製**想 toocopy toohello 剪貼簿的 下一步 toohello URL。
    
    ![第二個 SAS 對話方塊](media/vs-azure-tools-storage-explorer-files/image12.png)

8. 完成時，選取 [關閉] 。

## <a name="manage-access-policies-for-a-file-share"></a>管理檔案共用的存取原則

hello 下列步驟說明如何 toomanage （新增與移除） 存取檔案共用的原則: +。 hello 存取原則用來建立 SAS Url，透過該人員可以定義的時間期間使用 tooaccess hello 儲存體檔案資源。

1. 開啟儲存體 Explorer (預覽)。

2. Hello 左窗格中，展開包含 hello 檔案共用您想 toomanage 的存取原則的 hello 儲存體帳戶。

3. 展開 hello 儲存體帳戶的**檔案共用**。

4. 選取 hello 所需的檔案共用，以及-hello 操作功能表： 從選取**管理存取原則**。

    ![管理存取原則內容功能表](media/vs-azure-tools-storage-explorer-files/image13.png)

5. hello**存取原則** 對話方塊會列出任何已建立 hello 選取的檔案共用的存取原則。
    
    ![存取原則](media/vs-azure-tools-storage-explorer-files/image14.png)

6. 遵循下列步驟，視 hello 存取原則的管理工作而定：
    
    - **新增新的存取原則** -選取 [新增]。 一旦產生，hello**存取原則**對話方塊會顯示 hello 新加入的存取原則 （使用預設設定）。

    - **編輯存取原則** - 進行任何所需的編輯，然後選取 [儲存]。

    - **移除存取原則**-選取**移除**想 tooremove 的下一個 toohello 存取原則。

7. 建立新的 SAS URL，使用 hello 您稍早建立的存取原則：
    
    ![取得 SAS](media/vs-azure-tools-storage-explorer-files/image15.png)
    
    ![SAS 名稱和屬性](media/vs-azure-tools-storage-explorer-files/image16.png)

## <a name="managing-files-in-a-file-share"></a>檔案共用中的管理檔案

一旦您已建立的檔案共用，您可以上傳檔案 toothat 檔案共用、 下載檔案 tooyour 本機電腦、 開啟本機電腦，以及執行更多檔案。

hello 下列步驟說明如何 toomanage hello 檔案 （和資料夾） 內的檔案共用。

1.  開啟儲存體 Explorer (預覽)。

2.  Hello 左窗格中，展開包含您想 toomanage hello 檔案共用的 hello 儲存體帳戶。

3.  展開 hello 儲存體帳戶的**檔案共用**。

4.  按兩下您想 tooview hello 檔案共用。

5.  hello 主窗格會顯示 hello 檔案共用的內容。

    ![hello 共用的內容](media/vs-azure-tools-storage-explorer-files/image17.png)

6.  hello 主窗格會顯示 hello 檔案共用的內容。

7.  請遵循這些步驟視 hello 工作想 tooperform:

    - **上傳檔案 tooa 檔案共用**

        a.  Hello 主窗格的工具列上，選取**上傳**，然後**上載檔案**從 hello 下拉式選單。

        ![上傳檔案](media/vs-azure-tools-storage-explorer-files/image18.png)
        
        b. 在 hello**將檔案上傳**對話方塊中，選取 hello 省略符號 (**...**) 在 hello hello 右邊的按鈕**檔案**文字方塊想 tooupload tooselect hello 檔案。

        ![新增檔案](media/vs-azure-tools-storage-explorer-files/image19.png)

        c. 選取 [上傳] 。

    - **上傳資料夾 tooa 檔案共用**
        
        a. Hello 主窗格的工具列上，選取**上傳**，然後**上傳資料夾**從 hello 下拉式選單。

        ![上傳資料夾功能表](media/vs-azure-tools-storage-explorer-files/image20.png)

        b. 在 hello**上傳資料夾**對話方塊中，選取 hello 省略符號 (**...**) 在 hello hello 右邊的按鈕**資料夾**文字方塊 tooselect hello 資料夾想 tooupload 其內容。

        c. 選擇性地指定所選的資料夾的內容將會上傳到哪個 hello 的目標資料夾。 如果 hello 目標資料夾不存在，則會建立。

        d. 選取 [上傳] 。

    - **下載檔案 tooyour 本機電腦**
        
        a. 選取您想 toodownload hello 檔案。
        
        b. 在 hello 主窗格的工具列上，選取 **下載**。
        
        c. 在 [hello **toosave hello 下載檔案的位置指定**] 對話方塊中，指定您希望 hello 檔案下載，hello 位置，然後 hello 想 toogive 名稱它。

        d. 選取 [ **儲存**]。

    - **在您的本機電腦上開啟檔案**
        
        a.  選取您想 tooopen hello 檔案。
        
        b.  在 hello 主窗格的工具列上，選取 **開啟**。
        
        c.  hello 檔案會下載，並使用 hello 與 hello 檔案基礎的檔案類型相關聯的應用程式開啟。

    - **複製檔案 toohello 剪貼簿**

        a. 選取您想 toocopy hello 檔案。

        b. 在 hello 主窗格的工具列上，選取 **複製**。

        c. 在 hello 左窗格中，瀏覽 tooanother 檔案共用，然後按兩下該 tooview hello 主窗格中。

        d. 在 hello 主窗格的工具列上，選取 **貼上**toocreate hello 檔案的副本。

    - **刪除檔案**

        a. 選取您想 toodelete hello 檔案。

        b. 在 hello 主窗格的工具列上，選取 **刪除**。

        c. 選取**是**toohello 確認對話方塊。

## <a name="next-steps"></a>後續步驟

- 檢視 hello[最新的存放裝置總管 （預覽） 版本資訊和視訊](http://www.storageexplorer.com/)。

- 了解如何太[建立應用程式使用 Azure blob、 資料表、 佇列和檔案](https://azure.microsoft.com/documentation/services/storage/)。
