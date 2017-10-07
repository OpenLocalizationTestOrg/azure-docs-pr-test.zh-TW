---
title: "aaa tooget 媒體處理器執行個體使用 REST 的方式 |Microsoft 文件"
description: "了解 toocreate 媒體處理器元件 tooencode 」，將格式轉換、 加密或解密媒體內容，Azure 媒體服務的方式。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: f9ff1997-0da6-4528-aaed-792837e5be41
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: 9f423648ab73c90405c64895ce0f5b6a457862e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooget-a-media-processor-instance"></a>如何 tooget 媒體處理器執行個體
> [!div class="op_single_selector"]
> * [.NET](media-services-get-media-processor.md)
> * [REST](media-services-rest-get-media-processor.md)
> 
> 

## <a name="overview"></a>Overview
在媒體服務中，媒體處理器是可處理特定處理工作的元件，例如編碼、格式轉換、加密或解密媒體內容。 通常當您建立工作 tooencode 建立媒體處理器、 加密，或將媒體內容的 hello 格式轉換。

## <a name="azure-media-processors"></a>Azure 媒體處理器 

hello 下列主題提供媒體處理器的清單：

* [編碼媒體處理器](scenarios-and-availability.md#encoding-media-processors)
* [分析媒體處理器](scenarios-and-availability.md#analytics-media-processors)

>[!NOTE]
>在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。 如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。

## <a name="connect-toomedia-services"></a>TooMedia 服務連接

如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。 

>[!NOTE]
>已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。 您必須進行的後續呼叫 toohello 新的 URI。

## <a name="get-a-media-processor"></a>取得媒體處理器

下列 REST 呼叫的 hello 顯示 tooget 媒體處理器執行個體之名稱的方式 (在此情況下，**媒體編碼器標準**)。 

要求：

    GET https://media.windows.net/api/MediaProcessors()?$filter=Name%20eq%20'Media%20Encoder%20Standard' HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Accept: application/json
    Accept-Charset: UTF-8
    User-Agent: Microsoft ADO.NET Data Services
    Authorization: Bearer <token>
    x-ms-version: 2.11
    Host: media.windows.net

回應：

    . . .

    {  
       "odata.metadata":"https://media.windows.net/api/$metadata#MediaProcessors",
       "value":[  
          {  
             "Id":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "Description":"Media Encoder Standard",
             "Name":"Media Encoder Standard",
             "Sku":"",
             "Vendor":"Microsoft",
             "Version":"1.1"
          }
       ]
    }


## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>後續步驟
您現在知道如何 tooget 媒體處理器執行個體中，移 toohello[如何 tooEncode 資產](media-services-rest-get-started.md)這會顯示如何 toouse 會 hello 媒體編碼器標準 tooencode 資產的主題。

