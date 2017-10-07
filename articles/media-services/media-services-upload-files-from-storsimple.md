---
title: "從 Azure StorSimple 的 Azure Media Services 帳戶將 aaaUpload 檔案 |Microsoft 文件"
description: "本文提供 Azure StorSimple Data Manager 的簡短概述。 hello 發行項也會連結 tootutorials，教您如何從 StorSimple tooextract 資料並將它上傳為資產 tooan Azure Media Services 帳戶。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 1dd09328-262b-43ef-8099-73241b49a925
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 03/27/2017
ms.author: juliako
ms.openlocfilehash: 7e9712aa480106bbd5fcc63eaecf0418b24a8bef
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-into-an-azure-media-services-account-from-azure-storsimple"></a>從 Azure StorSimple 將檔案上傳至 Azure 媒體服務帳戶

本文提供 Azure StorSimple Data Manager 的簡短概述。 hello 發行項也會連結 tootutorials，教您如何從 StorSimple tooextract 資料並將此資料上傳為資產 tooan Azure 媒體服務 (AMS) 帳戶。

> 
> [!NOTE]
> Azure StorSimple Data Manager 目前處於私人預覽階段。 
> 

## <a name="overview"></a>概觀

在媒體服務中，您會將數位檔案上傳到到資產。 hello 資產可以包含視訊、 音訊、 影像、 縮圖集合、 文字播放軌和隱藏式的字幕檔案 （和 hello 中繼資料，這些檔案的相關。）Hello 檔案上傳，一旦您的內容會安全地儲存在 hello 用於進一步處理和雲端資料流。

[Azure StorSimple](https://docs.microsoft.com/azure/storsimple/) hello 的延伸模組在內部部署方案並自動層 hello 在內部部署儲存體和雲端存放裝置之間的資料，使用雲端儲存體。 hello StorSimple 裝置 dedupes，並將您的資料壓縮再將它傳送 toohello 雲端進行傳送大型檔案 toohello 雲端非常有效率。 hello [StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md)服務提供 Api，可讓您 tooextract 資料從 StorSimple，並加以呈現為 AMS 資產。

## <a name="get-started"></a>開始使用

1. [建立 Media Services 帳戶](media-services-portal-create-account.md)要 tootransfer hello 資產。
2. 註冊資料管理員預覽 hello 中所述[StorSimple Data Manager](../storsimple/storsimple-data-manager-overview.md)發行項。
3. 建立 StorSimple Data Manager 帳戶。
4. 建立資料轉換作業，以在執行時從 StorSimple 裝置擷取資料並將它傳輸到 AMS 帳戶中做為資產。 

    Hello 作業啟動時執行，則會建立儲存體佇列。 此佇列中會填入已轉換的 blob 備妥時的相關訊息。 hello 這個佇列名稱是 hello 與 hello hello 工作定義名稱相同。 您可以使用這個佇列 toodetermine 時資產是準備以及您想要的媒體服務作業 toorun 呼叫它。 例如，您可以使用這個佇列 tootrigger hello 必要的媒體服務程式碼中擁有 Azure 函式。

## <a name="see-also"></a>另請參閱

[使用 hello.Net SDK tootrigger hello 資料管理員中的工作](../storsimple/storsimple-data-manager-dotnet-jobs.md)

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>後續步驟

您現在可以將上傳的資產編碼。 如需詳細資訊，請參閱 [為資產編碼](media-services-portal-encode.md)。
