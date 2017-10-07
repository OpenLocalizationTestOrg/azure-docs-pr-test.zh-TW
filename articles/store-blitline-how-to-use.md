---
title: "映像處理的 aaaHow toouse Blitline Azure 功能指南"
description: "了解 toouse hello Blitline 服務 tooprocess 映像，在 Azure 應用程式的方式。"
services: 
documentationcenter: .net
author: blitline-dev
manager: jason@blitline.com
editor: jason@blitline.com
ms.assetid: 6c711248-0e52-4895-ba9e-8395628de924
ms.service: multiple
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/09/2014
ms.author: support@blitline.com
ms.openlocfilehash: 328fd177e25f45f29f8ad8e142d02b46017a858e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toouse-blitline-with-azure-and-azure-storage"></a>如何使用 Azure 和 Azure 儲存體 Blitline toouse
本指南將說明如何 tooaccess Blitline 服務和 toosubmit 作業 tooBlitline 的方式。

## <a name="what-is-blitline"></a>什麼是 Blitline？
Blitline 是以雲端為基礎的影像，處理服務，可提供企業層級的映像處理 hello 價格它需要成本 toobuild 一部分在它自己。

hello 事實是該映像處理已完成一再重複，通常從針對每個網站的 hello 地面重建。 我們了解這個情況，那是因為我們已經建立了上百萬次。 有一天，我們決定或許是替所有人執行此動作的時候了。 我們已經知道如何 toodo toodo 它快速並有效率地與儲存每個人都適用於 hello 同時它。

如需詳細資訊，請參閱 [http://www.blitline.com](http://www.blitline.com)(英文)。

## <a name="what-blitline-is-not"></a>Blitline 不是什麼...
tooclarify 什麼 Blitline 是很有用，它是通常更容易 tooidentify Blitline 無法達成的目標之前繼續進行後續步驟。

* Blitline 沒有 HTML widget tooupload 映像。 您必須提供的映像可公開或以供 Blitline tooreach 限制權限。
* Blitline 不會執行即時影像處理，如 Aviary.com
* Blitline 不接受映像上傳，您無法直接發送映像 tooBlitline。 您必須將其推送 tooAzure 儲存體或 Blitline 支援其他位置，然後告訴 Blitline toogo 哪裡取得它們。
* Blitline 可大量平行處理，但無法執行任何同步處理。 這表示您必須提供 postback_url 給我們，我們會在處理完成時通知您。

## <a name="create-a-blitline-account"></a>建立 Blitline 帳戶
[!INCLUDE [blitline-signup](../includes/blitline-signup.md)]

## <a name="how-toocreate-a-blitline-job"></a>如何 toocreate Blitline 工作
Blitline 會使用您想要在影像上的 tootake JSON toodefine hello 動作。 此 JSON 是由幾個簡單欄位組合而成。

hello 最簡單的範例如下所示：

        json : '{
       "application_id": "MY_APP_ID",
       "src" : "http://cdn.blitline.com/filters/boys.jpeg",
       "functions" : [ {
           "name": "resize_to_fit",
           "params" : { "width": 240, "height": 140 },
           "save" : { "image_identifier" : "external_sample_1" }
       } ]
    }'

這裡我們有會"src 」 映像的 JSON"...boys.jpeg 」 再調整大小的影像 too240x140。

您可以在找到 hello 應用程式識別碼是您**連接資訊**或**管理**在 Azure 上的索引標籤。 它是您的秘密識別碼，可讓您在 Blitline 的 toorun 作業。

[儲存] 參數的 hello 識別您希望我們已經處理它，一旦 tooput hello 映像的相關資訊。 在這個簡單的案例中，我們尚未定義一個位置。 如果沒有定義位置，Blitline 會將它儲存在本機 (並暫時地) 的唯一雲端位置。 您將無法從 hello JSON 的位置時請 hello Blitline Blitline 傳回的 tooget。 hello 「 映像 」 識別項需要並傳回 tooyou tooidentify 這個特定儲存映像時。

您可以找到更多資訊 hello*函式*我們這裡支援： <http://www.blitline.com/docs/functions>

您也可以尋找文件中的有關 hello 這裡工作選項： <http://www.blitline.com/docs/api>

一旦您的 JSON 時只需 toodo **POST**它太`http://api.blitline.com/job`

您將取回如下所示的 JSON：

    {
     "results":
         {"images":
            [{
              "image_identifier":"external_sample_1",
              "s3_url":"https://s3.amazonaws.com/dev.blitline/2011110722/YOUR_APP_ID/CK3f0xBF_2bV6wf7gEZE8w.jpg"
            }],
          "job_id":"4eb8c9f72a50ee2a9900002f"
         }
    }


這會告訴您，Blitline 已收到您的要求、 將它已將其放在處理佇列中，而 hello 映像完成後將會位於： **https://s3.amazonaws.com/dev.blitline/2011110722/YOUR\_應用程式\_識別碼/CK3f0xBF_2bV6wf7gEZE8w.jpg**

## <a name="how-toosave-an-image-tooyour-azure-storage-account"></a>如何 toosave 映像 tooyour Azure 儲存體帳戶
如果您有 Azure 儲存體帳戶，您輕鬆地插入您的 Azure 容器有 Blitline 發送 hello 處理影像。 藉由新增 「 azure_destination 」 您定義 hello 位置和要 Blitline toopush 權限。

下列是一個範例：

    job : '{
      "application_id": "YOUR_APP_ID",
      "src" : "http://www.google.com/logos/2011/houdini11-hp.jpg",
         "functions" : [{
         "name": "blur",
         "save" : {
             "image_identifier" : "YOUR_IMAGE_IDENTIFIER",
             "azure_destination" : {
                 "account_name" : "YOUR_AZURE_CONTAINER_NAME",
                 "shared_access_signature" : "SAS_THAT_GIVES_BLITLINE_PERMISSION_TO_WRITE_THIS_OBJECT_TO_CONTAINER",
               }
           }
         }]
       }'


填入與您自己的 hello CAPITALIZED 值，您可以送出此 JSON toohttp://api.blitline.com/job 並 hello"src 」 映像將使用模糊篩選處理然後推送至 tooyou Azure 的目的地。

### <a name="please-note"></a>請注意：
hello SAS 必須包含 hello 整個 SAS url，包括 hello hello 目的地檔案的檔案名稱。

範例：

    http://blitline.blob.core.windows.net/sample/image.jpg?sr=b&sv=2012-02-12&st=2013-04-12T03%3A18%3A30Z&se=2013-04-12T04%3A18%3A30Z&sp=w&sig=Bte2hkkbwTT2sqlkkKLop2asByrE0sIfeesOwj7jNA5o%3D


您也可以讀取 hello 的 Blitline 的 Azure 儲存體文件的最新版本[這裡](http://www.blitline.com/docs/azure_storage)。

## <a name="next-steps"></a>後續步驟
請造訪 blitline.com tooread 有關我們其他所有功能：

* Blitline API 端點文件 <http://www.blitline.com/docs/api>
* Blitline API 函式 <http://www.blitline.com/docs/functions>
* Blitline API 範例 <http://www.blitline.com/docs/examples>
* 協力廠商 Nuget 程式庫 <http://nuget.org/packages/Blitline.Net>

