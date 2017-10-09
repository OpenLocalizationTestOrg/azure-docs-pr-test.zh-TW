---
title: "aaa\"上傳檔案至 Media Services 帳戶使用 hello Azure 入口網站 |Microsoft 文件 」"
description: "本教學課程中引導您 hello 步驟的上傳檔案至媒體服務帳戶使用 hello Azure 入口網站"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 3ad3dcea-95be-4711-9aae-a455a32434f6
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/07/2017
ms.author: juliako
ms.openlocfilehash: 4ce1e133c72854532735ba7c72a43c92a75bc240
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-a-media-services-account-using-hello-azure-portal"></a>將檔案上傳到 Media Services 帳戶使用 hello Azure 入口網站
> [!div class="op_single_selector"]
> * [入口網站](media-services-portal-upload-files.md)
> * [.NET](media-services-dotnet-upload-files.md)
> * [REST](media-services-rest-upload-files.md)
> 
> [!NOTE]
> toocomplete 本教學課程中，您需要 Azure 帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。 
> 


在媒體服務中，您會將數位檔案上傳到到資產。 hello 資產可以包含視訊、 音訊、 影像、 縮圖集合、 文字播放軌和隱藏式的字幕檔案 （和 hello 中繼資料，這些檔案的相關。）Hello 檔案上傳，一旦您的內容會安全地儲存在 hello 用於進一步處理和雲端資料流。


## <a name="upload-files"></a>上傳檔案

>[!NOTE]
>沒有支援 Media Services 中的處理限制 toohello 最大檔案大小。 請參閱[這](media-services-quotas-and-limitations.md)hello 檔案大小限制的詳細主題。
>

1. 在 hello [Azure 入口網站](https://portal.azure.com/)，選取您的 Azure Media Services 帳戶。
2. 在 hello**設定**刀鋒視窗中，按一下 **資產**。
   
    ![上傳檔案](./media/media-services-portal-vod-get-started/media-services-upload.png)
3. 按一下 hello**上傳** 按鈕。
   
    hello**上載視訊資產** 視窗隨即出現。
   
   > [!NOTE]
   > 檔案大小不受限。
   > 
   > 
4. 瀏覽您的電腦上的預期 toohello 視訊、 加以選取，並點擊 [確定]。  
   
    hello 上載啟動，而且您可以看見 hello 進度 hello 檔名底下。  

Hello 上傳完成之後，您會看到 hello hello 中所列的新資產**資產**視窗。 

## <a name="next-steps"></a>後續步驟
您現在可以將上傳的資產編碼。 如需詳細資訊，請參閱 [為資產編碼](media-services-portal-encode.md)。

您也可以使用 Azure 函式 tootrigger 抵達 hello 設定容器中的檔案為基礎的編碼工作。 如需詳細資訊，請參閱[此範例](https://azure.microsoft.com/resources/samples/media-services-dotnet-functions-integration/ )。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

