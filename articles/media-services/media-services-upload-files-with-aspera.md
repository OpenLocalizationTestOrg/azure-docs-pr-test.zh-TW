---
title: "Azure 媒體服務帳戶使用 Aspera aaaUpload 檔案 |Microsoft 文件"
description: "本教學課程會引導您完成 hello 步驟將檔案上傳至儲存體帳戶使用 hello Media Services 帳戶有關聯的 * * Aspera 伺服器上指定 * * Azure 上的服務。"
services: media-services
documentationcenter: 
author: johndeu
manager: cfowler
editor: 
ms.assetid: 8812623a-b425-4a0f-9e05-0ee6c839b6f9
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 04/17/2017
ms.author: juliako
ms.openlocfilehash: 7213f016cc1b7f262b14db7b39b478a03970d1c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-aspera-server-on-demand-service-on-azure"></a>將檔案上傳到 Media Services 帳戶在 Azure 上使用 hello 隨選 Aspera 伺服器服務

## <a name="overview"></a>概觀

**Aspera** 是高速檔案傳輸軟體。 適用於 Azure 的 **Aspera Server On Demand** 可讓大型檔案直接高速上傳和下載到 Azure Blob 物件儲存體。 如需有關資訊**Aspera 隨選**，請參閱 hello [Aspera 雲端](http://cloud.asperasoft.com/)站台。 
  
**隨選 Aspera 伺服器**Azure 是可以從 hello 購買[Azure marketplace](https://azure.microsoft.com/en-us/marketplace/)。 在順序 toocomplete 購買**隨選 Aspera 伺服器**azure，請登入 Azure Marketplace 與您的 Windows Live id。

本教學課程會引導您完成 hello 步驟將檔案上傳至儲存體帳戶與使用 hello Media Services 帳戶相關聯之**隨選 Aspera 伺服器**Azure 上的服務。 

您可以找到範例顯示如何 toouse Azure 函式與 Aspera 以及 Media Services[這裡](https://github.com/Azure-Samples/media-services-dotnet-functions-integration/tree/master/103-aspera-ingest)。

>[!NOTE]
>沒有與 Azure Media Services 處理媒體處理器 (Mp) 支援的限制 toohello 最大檔案大小。 請參閱[這](media-services-quotas-and-limitations.md)hello 檔案大小限制的詳細主題。
>

## <a name="prerequisites"></a>必要條件 

toocomplete 本教學課程中，您需要：

* Windows Live ID
* [Azure 帳戶](https://azure.microsoft.com)。 如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。 
* [Azure 媒體服務帳戶](media-services-portal-create-account.md)。

## <a name="purchase-aspera-on-demand-for-azure"></a>購買適用於 Azure 的 Aspera On Demand

一旦您登入 Azure Marketplace，遵循這些基本步驟 toocomplete Aspera 隨選 azure 的購買。

1. 搜尋 Aspera，並選取「Server On Demand」。

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera001.png)

2. 檢閱 hello 訂用帳戶的計劃，然後按一下 登入 '

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera002.png)

3. 填寫 hello 規格需要訂用帳戶上的伺服器。

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera003.png)

4. 按一下 hello**定價層**hello sub 面板中選取您想要每月的磁碟區。 在 hello**計劃的詳細資料**面板中，選取**確定**。 然後，在 hello**選擇定價層**] 面板中，按一下 [**選取**。

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera004.png)

5. 按一下**法律條款**tooview 並接受 hello sub 面板中的 hello 法律條款。 一旦您已檢閱 hello 法律條款，按一下 **購買**。

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera005.png)

6. 按一下完成 hello 購買**建立**。

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera006.png)

7. hello Azure 儀表板會宣布，它會佈建 hello 服務。  它使用佈建完成後，您可以透過搜尋 hello hello 服務名稱的資源中尋找 hello 新訂用帳戶。 一旦找到 hello 服務，在其上按兩下 toolaunch hello 服務管理入口網站。

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera007.png)

8. 啟動 hello Aspera 管理入口網站。 一旦找到新 Aspera 服務，您可以獲得存取 toohello 管理入口網站中，按一下 hello 服務。  新的面板就會啟動。 從內該新面板中，您需要在 hello tooclick**資源名稱**的新服務。  在下列螢幕擷取畫面的 hello，hello 資源名稱會是 'AsperaTransferDemo'。 一旦您按一下 hello 資源名稱，就會啟動另一個面板。 在該新推出的面板中，您會看到 [管理] 連結。 按一下 [管理] 5d 連結 toolaunch hello Aspera 管理入口網站上 hello。

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera008.png)

9. Hello 上的 管理連結上，您會得到 toohello 註冊頁面上，都需要 tooaccess hello 服務。

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera009.png)

10. 此時，您應該有存取 toohello Aspera 服務管理入口網站中，其中建立便捷鍵，請下載 Aspera 用戶端和授權、 檢視使用量並了解 hello 應用程式開發介面。

    hello 下列螢幕擷取畫面顯示 hello 存取建立。 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera010.png)

    hello 下列螢幕擷取畫面顯示 hello 使用方式報告 hello 入口網站中的介面。 

   ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera011.png)

## <a name="upload-files-with-aspera"></a>透過 Aspera 上傳檔案

1. 下載並安裝 hello Aspera 用戶端軟體：
    
    * [瀏覽器外掛程式](http://downloads.asperasoft.com/connect2/)
    * [豐富型用戶端](http://downloads.asperasoft.com/en/downloads/2)

2. 進行第一次傳送。 在訂單 toouse hello Aspera 用戶端 tootransfer 以 hello Aspera 傳輸服務，您會需要 toocomplete hello 下列： 

    1. 建立使用 hello Aspera 入口網站的存取金鑰。  
    2. 下載、 安裝和授權 hello Aspera 用戶端 （hello Aspera 入口網站中可以找到軟體）。  

    >[!NOTE]
    >請閱讀 hello Aspera 用戶端指南以取得組態資訊。
    
    3. 擷取儲存體帳戶使用 hello Azure Media 帳戶有關聯的某些資訊[Azure 入口網站](https://portal.azure.com/)。 具體而言，名稱和金鑰，以及 hello 儲存體 blob 容器名稱中 toowhich 想 tooplace 您的內容。 

        * tooget hello 儲存資訊從 hello 入口網站： 找不到儲存體帳戶，請按一下 hello 存取金鑰，然後複製 hello 名稱和 hello 帳戶金鑰。
        * tooget hello 容器名稱： 尋找您的儲存體帳戶，請選取**Blob**，選取您想要 tooupload hello 內容 hello 容器 hello 名稱。 

    以下是 hello Aspera 用戶端 hello 螢幕擷取畫面**連線管理員**您必須在其中指定 hello 'Azure' 的儲存類型和認證，以及 hello blob 容器。

    ![Aspera](./media/media-services-upload-files-with-aspera/media-services-upload-files-with-aspera012.png)

## <a name="resources"></a>資源

這篇文章中提及 hello 下列資源。 

* [Connect 瀏覽器外掛程式](http://downloads.asperasoft.com/connect2/)
* [Connect 指南](http://downloads.asperasoft.com/en/documentation/8)
* [Aspera 用戶端](http://downloads.asperasoft.com/en/downloads/2)
* [用戶端指南](http://downloads.asperasoft.com/en/documentation/2)

## <a name="next-steps"></a>後續步驟

您現在可以[從儲存體帳戶將 Blob 複製到 AMS 帳戶](media-services-copying-existing-blob.md#copy-blobs-from-a-storage-account-into-an-ams-account)。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

