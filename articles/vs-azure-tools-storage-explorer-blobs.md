---
title: "aaaManage Azure Blob 儲存體資源，使用儲存體總管 （預覽） |Microsoft 文件"
description: "使用儲存體 Explorer 來管理 Azure Blob 容器和 Blob (預覽)"
services: storage
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 2f09e545-ec94-4d89-b96c-14783cc9d7a9
ms.service: storage
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: 503dd061b205875da127378ab48e8d465800fc09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-azure-blob-storage-resources-with-storage-explorer-preview"></a>使用儲存體 Explorer 來管理 Azure Blob 儲存體資源 (預覽)
## <a name="overview"></a>概觀
[Azure Blob 儲存體](storage/blobs/storage-dotnet-how-to-use-blobs.md)是用來儲存大量非結構化資料，例如文字或二進位資料，可以在 hello world，透過 HTTP 或 HTTPS 從任何地方存取服務。
您可以使用 Blob 儲存體 tooexpose 資料公開 toohello 世界中或 toostore 應用程式資料未公開。 在本文中，您將學習如何將存放裝置總管 （預覽） toowork toouse blob 容器和 blob。

## <a name="prerequisites"></a>必要條件
toocomplete hello 本文中的步驟，您將需要下列 hello:

* [下載並安裝儲存體 Explorer (預覽)](http://www.storageexplorer.com)
* [連接 tooa Azure 儲存體帳戶或服務](vs-azure-tools-storage-manage-with-storage-explorer.md#connect-to-a-storage-account-or-service)

## <a name="create-a-blob-container"></a>建立 Blob 容器
所有 blob 必須都位於 blob 容器，這是 blob 的邏輯群組。 帳戶可以包含無限數量的容器，每個容器可以儲存無限數量的 blob。

hello 下列步驟說明如何 toocreate 存放裝置總管 （預覽） 中的 blob 容器。

1. 開啟儲存體 Explorer (預覽)。
2. Hello 左窗格中，展開要在其中 toocreate hello blob 容器的 hello 儲存體帳戶。
3. 以滑鼠右鍵按一下**Blob 容器**，和-hello 操作功能表： 從選取**建立 Blob 容器**。

   ![建立 Blob 容器內容功能表][0]
4. 文字會出現一個方塊下方 hello **Blob 容器**資料夾。 輸入您的 blob 容器的 hello 名稱。 請參閱 hello[容器命名規則](storage/blobs/storage-dotnet-how-to-use-blobs.md#create-a-container)一節，以清單規則以及限制命名 blob 容器。

   ![建立 Blob 容器文字方塊][1]
5. 按**Enter**完成 toocreate hello blob 容器，或**Esc** toocancel。 一旦已成功建立 hello blob 容器，它就會顯示在 hello **Blob 容器**hello 資料夾選取儲存體帳戶。

   ![Blob 容器已建立][2]

## <a name="view-a-blob-containers-contents"></a>檢視 blob 容器的內容
Blob 容器包含 blob 和資料夾 (也包含 blob)。

hello 下列步驟說明如何在儲存體總管 （預覽） 中的 blob 容器 tooview hello 內容：

1. 開啟儲存體 Explorer (預覽)。
2. Hello 左窗格中，展開包含您想 tooview hello blob 容器的 hello 儲存體帳戶。
3. 展開 hello 儲存體帳戶的**Blob 容器**。
4. 以滑鼠右鍵按一下 hello blob 容器 tooview，並為 hello 操作功能表： 從選取**開啟 Blob 容器編輯器**。
   您也可以按兩下您想 tooview hello blob 容器。

   ![開啟 blob 容器編輯器內容功能表][19]
5. hello 主窗格會顯示 hello blob 容器的內容。

   ![Blob 容器編輯器][3]

## <a name="delete-a-blob-container"></a>刪除 Blob 容器
Blob 容器可以輕鬆地建立並視需要刪除。 (toosee toodelete 個別的 blob，請參閱 toohello 區段[管理 blob 容器中的 blob](#managing-blobs-in-a-blob-container)。)

hello 下列步驟說明如何 toodelete blob 容器中儲存體總管 （預覽）：

1. 開啟儲存體 Explorer (預覽)。
2. Hello 左窗格中，展開包含您想 tooview hello blob 容器的 hello 儲存體帳戶。
3. 展開 hello 儲存體帳戶的**Blob 容器**。
4. 以滑鼠右鍵按一下 hello blob 容器 toodelete，並為 hello 操作功能表： 從選取**刪除**。
   您也可以按**刪除**toodelete hello 目前選取的 blob 容器。

   ![刪除 Blob 容器內容功能表][4]
5. 選取**是**toohello 確認對話方塊。

   ![刪除 Blob 容器確認][5]

## <a name="copy-a-blob-container"></a>複製 Blob 容器
儲存體總管 （預覽） 可讓您 toocopy blob 容器 toohello 剪貼簿，然後到另一個儲存體帳戶 blob 容器的貼。 (toosee toocopy 個別的 blob，請參閱 toohello 區段[管理 blob 容器中的 blob](#managing-blobs-in-a-blob-container)。)

hello 下列步驟說明如何從一個儲存體 blob 容器 toocopy 帳戶 tooanother。

1. 開啟儲存體 Explorer (預覽)。
2. Hello 左窗格中，展開包含您想 toocopy hello blob 容器的 hello 儲存體帳戶。
3. 展開 hello 儲存體帳戶的**Blob 容器**。
4. 以滑鼠右鍵按一下 hello blob 容器 toocopy，並為 hello 操作功能表： 從選取**複製 Blob 容器**。

   ![複製 Blob 容器內容功能表][6]
5. 以滑鼠右鍵按一下 hello 所需"target"儲存體帳戶所在 toopaste hello blob 容器，再-hello 操作功能表： 從選取**貼上的 Blob 容器**。

   ![貼上 Blob 容器內容功能表][7]

## <a name="get-hello-sas-for-a-blob-container"></a>取得 blob 容器的 SAS hello
A[共用的存取簽章 (SAS)](storage/common/storage-dotnet-shared-access-signature-part-1.md)提供儲存體帳戶中的委派的存取 tooresources。
這表示您可以授與用戶端限制在指定期間內的時間與一組指定的權限，在儲存體帳戶的權限 tooobjects，而不需要共用您的帳戶存取金鑰。

hello 下列步驟說明如何 toocreate blob 容器的 SAS:

1. 開啟儲存體 Explorer (預覽)。
2. Hello 左窗格中，展開包含您想 tooget SAS hello blob 容器的 hello 儲存體帳戶。
3. 展開 hello 儲存體帳戶的**Blob 容器**。
4. Hello 所需的 blob 容器，以滑鼠右鍵按一下和-hello 操作功能表： 從選取**取得共用存取簽章**。

   ![取得 SAS 內容功能表][8]
5. 在 [hello**共用存取簽章**] 對話方塊中，指定 hello 原則、 開始和到期日期、 時間區域，然後存取您想要用於 hello 資源層級。

   ![取得 SAS 選項][9]
6. 當您完成指定的 hello SAS 選項，選取**建立**。
7. 第二個**共用存取簽章**清單 hello blob 容器以及 hello URL，您可以使用 tooaccess QueryStrings hello 儲存體資源，就會顯示對話方塊。
   選取**複製**想 toocopy toohello 剪貼簿的 下一步 toohello URL。

   ![複製 SAS URL][10]
8. 完成時，選取 [關閉] 。

## <a name="manage-access-policies-for-a-blob-container"></a>管理 blob 容器的存取原則
hello 下列步驟說明如何 toomanage （新增與移除） 存取的 blob 容器的原則：

1. 開啟儲存體 Explorer (預覽)。
2. Hello 左窗格中，展開包含您想 toomanage 其存取原則的 hello blob 容器的 hello 儲存體帳戶。
3. 展開 hello 儲存體帳戶的**Blob 容器**。
4. 選取 hello 所需的 blob 容器，以及-hello 操作功能表： 從選取**管理存取原則**。

   ![管理存取原則內容功能表][11]
5. hello**存取原則** 對話方塊會列出任何已建立 hello 選的 blob 容器的存取原則。

   ![存取原則選項][12]        
6. 遵循下列步驟，視 hello 存取原則的管理工作而定：

   * **新增新的存取原則** -選取 [新增]。 一旦產生，hello**存取原則**對話方塊會顯示 hello 新加入的存取原則 （使用預設設定）。
   * **編輯存取原則** -進行任何所需的編輯，然後選取 [儲存]。
   * **移除存取原則**-選取**移除**想 tooremove 的下一個 toohello 存取原則。

## <a name="set-hello-public-access-level-for-a-blob-container"></a>Blob 容器設定 hello 公用存取層級
根據預設，每個 blob 容器設定太 「 沒有公用存取 」。

hello 下列步驟說明如何 toospecify 公用存取層級的 blob 容器。

1. 開啟儲存體 Explorer (預覽)。
2. Hello 左窗格中，展開包含您想 toomanage 其存取原則的 hello blob 容器的 hello 儲存體帳戶。
3. 展開 hello 儲存體帳戶的**Blob 容器**。
4. 選取 hello 所需的 blob 容器，以及-hello 操作功能表： 從選取**設定公用存取層級**。

   ![設定公用存取層級內容功能表][13]
5. 在 [hello**設定容器的公用存取層級**] 對話方塊中，指定所需的 hello 存取層級。

   ![設定公用存取層級選項][14]
6. 選取 [套用] 。

## <a name="managing-blobs-in-a-blob-container"></a>管理 blob 容器中的 blob
建立 blob 容器之後，您可以上傳 blob toothat blob 容器下載 blob tooyour 本機電腦、 開啟本機電腦，以及執行更多的 blob。

hello 下列步驟說明 toomanage 如何 hello blob （和資料夾） 內的 blob 容器。

1. 開啟儲存體 Explorer (預覽)。
2. Hello 左窗格中，展開包含您想 toomanage hello blob 容器的 hello 儲存體帳戶。
3. 展開 hello 儲存體帳戶的**Blob 容器**。
4. 按兩下您想 tooview hello blob 容器。
5. hello 主窗格會顯示 hello blob 容器的內容。

   ![檢視 Blob 容器][3]
6. hello 主窗格會顯示 hello blob 容器的內容。
7. 請遵循這些步驟視 hello 工作想 tooperform:

   * **上傳檔案 tooa blob 容器**

     1. Hello 主窗格的工具列上，選取**上傳**，然後**上載檔案**從 hello 下拉式選單。

        ![上傳檔案功能表][15]
     2. 在 hello**將檔案上傳**對話方塊中，選取 hello 省略符號 (**...**) 在 hello hello 右邊的按鈕**檔案**文字方塊想 tooupload tooselect hello 檔案。

        ![上傳檔案選項][16]
     3. 指定 hello 類型**Blob 類型**。 hello 文章[開始使用適用於.NET 的 Azure Blob 儲存體使用](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts)說明 hello 差異 hello 各種 blob 類型。
     4. 選擇性地指定 hello 選取的檔案將會上傳到其中的目標資料夾。 如果 hello 目標資料夾不存在，則會建立。
     5. 選取 [上傳] 。
   * **上傳資料夾 tooa blob 容器**

     1. Hello 主窗格的工具列上，選取**上傳**，然後**上傳資料夾**從 hello 下拉式選單。

        ![上傳資料夾功能表][17]
     2. 在 hello**上傳資料夾**對話方塊中，選取 hello 省略符號 (**...**) 在 hello hello 右邊的按鈕**資料夾**文字方塊 tooselect hello 資料夾想 tooupload 其內容。

        ![上傳資料夾選項][18]
     3. 指定 hello 類型**Blob 類型**。 hello 文章[開始使用適用於.NET 的 Azure Blob 儲存體使用](storage/blobs/storage-dotnet-how-to-use-blobs.md#blob-service-concepts)說明 hello 差異 hello 各種 blob 類型。
     4. 選擇性地指定所選的資料夾的內容將會上傳到哪個 hello 的目標資料夾。 如果 hello 目標資料夾不存在，則會建立。
     5. 選取 [上傳] 。
   * **下載 blob tooyour 本機電腦**

     1. 選取您想 toodownload hello blob。
     2. 在 hello 主窗格的工具列上，選取 **下載**。
     3. 在 [hello **toosave hello 下載 blob 的位置指定**] 對話方塊中，指定您要下載，hello blob 的 hello 位置和 hello 想 toogive 名稱它。  
     4. 選取 [ **儲存**]。
   * **在您的本機電腦上開啟 blob**

     1. 選取您想 tooopen hello blob。
     2. 在 hello 主窗格的工具列上，選取 **開啟**。
     3. hello blob 會下載，並使用 hello 與 hello blob 的基礎檔案類型相關聯的應用程式開啟。
   * **複製 blob toohello 剪貼簿**

     1. 選取您想 toocopy hello blob。
     2. 在 hello 主窗格的工具列上，選取 **複製**。
     3. 在 hello 左窗格中，瀏覽 tooanother blob 容器，然後按兩下該 tooview hello 主窗格中。
     4. 在 hello 主窗格的工具列上，選取 **貼上**toocreate hello blob 的複本。
   * **刪除 Blob**

     1. 選取您想 toodelete hello blob。
     2. 在 hello 主窗格的工具列上，選取 **刪除**。
     3. 選取**是**toohello 確認對話方塊。

## <a name="next-steps"></a>後續步驟
* 檢視 hello[最新的存放裝置總管 （預覽） 版本資訊和視訊](http://www.storageexplorer.com)。
* 了解如何太[建立應用程式使用 Azure blob、 資料表、 佇列和檔案](https://azure.microsoft.com/documentation/services/storage/)。

[0]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-create-context-menu.png
[1]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create.png
[2]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-create-done.png
[3]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-editor.png
[4]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-context-menu.png
[5]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-delete-confirmation.png
[6]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-copy-context-menu.png
[7]: ./media/vs-azure-tools-storage-explorer-blobs/blob-containers-paste-context-menu.png
[8]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-context-menu.png
[9]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-options.png
[10]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-get-sas-urls.png
[11]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-context-menu.png
[12]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-manage-access-policies-options.png
[13]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-context-menu.png
[14]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-set-public-access-level-options.png
[15]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-menu.png
[16]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-files-options.png
[17]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-menu.png
[18]: ./media/vs-azure-tools-storage-explorer-blobs/blob-upload-folder-options.png
[19]: ./media/vs-azure-tools-storage-explorer-blobs/blob-container-open-editor-context-menu.png
