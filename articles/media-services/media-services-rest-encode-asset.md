---
title: "aaaHow tooencode 使用標準的媒體編碼器 Azure 資產 |Microsoft 文件"
description: "了解如何 toouse 媒體編碼器標準 tooencode 媒體內容上 Azure Media Services。 程式碼範例會使用 REST API。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.assetid: 2a7273c6-8a22-4f82-9bfe-4509ff32d4a4
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: juliako
ms.openlocfilehash: b766bafded7ee98eda3e6ef149c31d5d8fe406fc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooencode-an-asset-by-using-media-encoder-standard"></a>如何使用媒體編碼器標準資產 tooencode
> [!div class="op_single_selector"]
> * [.NET](media-services-dotnet-encode-with-media-encoder-standard.md)
> * [REST](media-services-rest-encode-asset.md)
> * [入口網站](media-services-portal-encode.md)
>
>

## <a name="overview"></a>概觀
toodeliver hello 網際網路上的數位視訊，您必須壓縮 hello 媒體。 數位視訊檔案很大，而且可能會太大 toodeliver 透過 hello 網際網路，或基於您的客戶裝置 toodisplay 正確。 編碼是壓縮視訊和音訊，使您的客戶可以檢視您的媒體 hello 程序。

編碼工作是在 Azure Media Services hello 大多數處理作業。 您從一個編碼 tooanother 建立編碼工作 tooconvert 媒體檔案。 當編碼時，您可以使用 hello Media Services 內建編碼器 （媒體編碼器標準）。 您也可以使用媒體服務合作夥伴所提供的編碼器。 第三方編碼器皆可透過 hello Azure Marketplace。 您可以指定 hello 的編碼工作，使用針對您的編碼器定義的預設的字串，或使用預設的組態檔的詳細資料。 toosee hello 類型的預設值可供使用，請參閱[的媒體編碼器標準工作預設](http://msdn.microsoft.com/library/mt269960)。

每個工作可以有一個或更多的工作，根據 hello 類型處理您想 tooaccomplish。 透過 hello REST API，您可以建立工作和其相關的工作中有兩種：

* 工作可以透過工作項目上的 hello 工作導覽屬性的內嵌定義。
* 使用 OData 批次處理。

我們建議您一律將原始程式檔編碼成彈性位元速率 MP4 集，並使用，以轉換 hello 集 toohello 所需的格式[動態封裝](media-services-dynamic-packaging-overview.md)。

如果輸出資產是儲存體加密，您必須設定 hello 資產傳遞原則。 如需詳細資訊，請參閱[設定資產傳遞原則](media-services-rest-configure-asset-delivery-policy.md)。

## <a name="considerations"></a>考量

在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。 如需詳細資訊，請參閱 [媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。

您可以啟動參考媒體處理器之前，請確認您擁有 hello 正確的媒體處理器的識別碼。 如需詳細資訊，請參閱[取得媒體處理器](media-services-rest-get-media-processor.md)。

## <a name="connect-toomedia-services"></a>TooMedia 服務連接

如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。 

>[!NOTE]
>已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。 您必須進行的後續呼叫 toohello 新的 URI。

## <a name="create-a-job-with-a-single-encoding-task"></a>建立具有單一編碼工作的工作
> [!NOTE]
> 當您使用以 hello 媒體服務 REST API 時，hello 適用下列考量：
>
> 在媒體服務中存取實體時，您必須在 HTTP 要求中設定特定的標頭欄位和值。 如需詳細資訊，請參閱[媒體服務 REST API 開發設定](media-services-rest-how-to-use.md)。
>
> 已成功連接之後 toohttps://media.windows.net，您會收到指定另一個媒體服務 URI 的 301 重新導向。 您必須進行的後續呼叫 toohello 新的 URI。 如需有關如何 tooconnect toohello AMS API，請參閱詳細[存取 hello Azure 媒體服務 API 與 Azure AD 驗證](media-services-use-aad-auth-to-access-ams-api.md)。
>
> 當使用 JSON，並指定 toouse hello **__metadata**關鍵字 hello 要求 (例如，tooreferences 連結物件)，您必須設定 hello**接受**標頭太[詳細資訊 JSON 格式](http://www.odata.org/documentation/odata-version-3-0/json-verbose-format/)： 接受： 應用程式/json; odata = 詳細資訊。
>
>

hello 下列範例會示範如何 toocreate 和 post 作業的一項工作設定 tooencode 視訊在特定的解析度與品質。 透過媒體編碼器標準進行編碼時，您可以使用 [這裡](http://msdn.microsoft.com/library/mt269960)指定的工作組態預設。

要求：

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net

    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3Aaab7f15b-3136-4ddf-9962-e9ecb28fb9d2')"}}],  "Tasks" : [{"Configuration" : "Adaptive Streaming", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",  "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"}]}

回應：

    HTTP/1.1 201 Created

    . . .

### <a name="set-hello-output-assets-name"></a>設定 hello 輸出資產的名稱
hello 下列範例顯示如何 tooset hello assetName 屬性：

    { "TaskBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"CustomOutputAssetName\">JobOutputAsset(0)</outputAsset></taskBody>"}

## <a name="considerations"></a>考量
* TaskBody 屬性必須使用常值的輸入或輸出資產 hello 工作所使用 XML toodefine hello 數目。 hello 工作主題包含 XML hello XML 結構描述定義。
* 在 hello TaskBody 定義中，每個內部值<inputAsset>和<outputAsset>必須設定為 JobInputAsset(value) 或 JobOutputAsset(value)。
* 每個工作可以有多個輸出資產。 一個 JobOutputAsset(x) 只能使用一次做為工作中的工作輸出。
* 您可以指定 JobInputAsset 或 JobOutputAsset 做為工作的輸入資產。
* 工作不能形成循環。
* 您傳遞 tooJobInputAsset 或 JobOutputAsset 的 hello value 參數代表資產 hello 索引值。 hello 實際的資產會定義在 hello Inputmediaasset 與 Outputmediaasset 導覽屬性上 hello 工作實體定義。
* 因為 Media Services 內建於 OData v3，hello 個別資產 hello Inputmediaasset 與 Outputmediaasset 導覽屬性集合會透過參考"__metadata: uri"名稱 / 值組。
* Inputmediaasset 對應 tooone 或您建立 Media Services 中的多個資產。 Outputmediaasset 由 hello 系統建立。 它們不會參考現有的資產。
* Outputmediaasset 可以使用 hello assetName 屬性命名。 如果這個屬性不存在，則 hello OutputMediaAsset hello 名稱是 hello 任何 hello 內部文字值<outputAsset>項目是與 hello 作業名稱值或 （在 hello hello Name 屬性不定義所在的情況下） 的 hello 作業識別碼值的尾碼。 例如，如果您設定 assetName 的值太 「 範例 」，然後 hello OutputMediaAsset Name 屬性設定太"Sample。" 不過，如果您未設定 assetName 的值，但是未設定 hello 工作名稱太"NewJob，"然後 hello OutputMediaAsset Name 將是"JobOutputAsset （值） _NewJob"。

## <a name="create-a-job-with-chained-tasks"></a>建立具有鏈結工作的工作
在許多應用程式案例中，開發人員會想 toocreate 一連串的處理工作。 在媒體服務中，您可以建立一連串的鏈結工作。 每一項工作會執行不同的處理步驟，而且可以使用不同的媒體處理器。 hello 鏈結工作可以遞交資產，從一個工作 tooanother，hello 資產上執行一連串的工作。 不過，執行作業中的 hello 工作就不需要的 toobe 序列中。 當您建立鏈結的工作時，hello 鏈結**ITask**物件都會建立單一**IJob**物件。

> [!NOTE]
> 目前有每個工作裡 30 個工作的限制。 如果您需要 toochain 30 個以上的工作，建立多個作業 toocontain hello 工作。
>
>

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Name":"NewTestJob",
       "InputMediaAssets":[  
          {  
             "__metadata":{  
                "uri":"https://testrest.cloudapp.net/api/Assets('nb%3Acid%3AUUID%3A910ffdc1-2e25-4b17-8a42-61ffd4b8914c')"
             }
          }
       ],
       "Tasks":[  
          {  
             "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody>"
          },
          {  
             "Configuration":"H264 Smooth Streaming 720p",
             "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
             "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-16\"?><taskBody><inputAsset>JobOutputAsset(0)</inputAsset><outputAsset>JobOutputAsset(1)</outputAsset></taskBody>"
          }
       ]
    }


### <a name="considerations"></a>考量
tooenable 鏈結工作：

* 一個作業至少必須有 2 個工作。
* 必須有至少一個工作的輸入是 hello hello 工作中另一項工作的輸出。

## <a name="use-odata-batch-processing"></a>使用 OData 批次處理
hello 下列範例顯示如何 toouse OData 批次處理 toocreate 工作和工作。 如需批次處理的資訊，請參閱 [開放式資料通訊協定 (OData) 批次處理](http://www.odata.org/documentation/odata-version-3-0/batch-processing/)。

    POST https://media.windows.net/api/$batch HTTP/1.1
    DataServiceVersion: 1.0;NetFx
    MaxDataServiceVersion: 3.0;NetFx
    Content-Type: multipart/mixed; boundary=batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Accept: multipart/mixed
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000
    Host: media.windows.net


    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e
    Content-Type: multipart/mixed; boundary=changeset_122fb0a4-cd80-4958-820f-346309967e4d

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/Jobs HTTP/1.1
    Content-ID: 1
    Content-Type: application/json
    Accept: application/json
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {"Name" : "NewTestJob", "InputMediaAssets@odata.bind":["https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A2a22445d-1500-80c6-4b34-f1e5190d33c6')"]}

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d
    Content-Type: application/http
    Content-Transfer-Encoding: binary

    POST https://media.windows.net/api/$1/Tasks HTTP/1.1
    Content-ID: 2
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    Accept-Charset: UTF-8
    Authorization: Bearer <token>
    x-ms-version: 2.11
    x-ms-client-request-id: 00000000-0000-0000-0000-000000000000

    {  
       "Configuration":"H264 Adaptive Bitrate MP4 Set 720p",
       "MediaProcessorId":"nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56",
       "TaskBody":"<?xml version=\"1.0\" encoding=\"utf-8\"?><taskBody><inputAsset>JobInputAsset(0)</inputAsset><outputAsset assetName=\"Custom output name\">JobOutputAsset(0)</outputAsset></taskBody>"
    }

    --changeset_122fb0a4-cd80-4958-820f-346309967e4d--
    --batch_a01a5ec4-ba0f-4536-84b5-66c5a5a6d34e--



## <a name="create-a-job-by-using-a-jobtemplate"></a>使用 JobTemplate 建立作業
當您使用一組常用的工作，則使用 JobTemplate toospecify hello 預設的工作預設設定或工作的 tooset hello 順序來處理多個資產。

下列範例中的 hello 顯示 toocreate 是 TaskTemplate 使用 JobTemplate 定義內嵌的方式。 hello TaskTemplate 使用 hello 媒體編碼器標準為 hello MediaProcessor tooencode hello 資產檔案。 但是，也可以使用其他 MediaProcessor。

    POST https://media.windows.net/API/JobTemplates HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewJobTemplate25", "JobTemplateBody" : "<?xml version=\"1.0\" encoding=\"utf-8\"?><jobTemplate><taskBody taskTemplateId=\"nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789\"><inputAsset>JobInputAsset(0)</inputAsset><outputAsset>JobOutputAsset(0)</outputAsset></taskBody></jobTemplate>", "TaskTemplates" : [{"Id" : "nb:ttid:UUID:071370A3-E63E-4E81-A099-AD66BCAC3789", "Configuration" : "H264 Smooth Streaming 720p", "MediaProcessorId" : "nb:mpid:UUID:ff4df607-d419-42f0-bc17-a481b1331e56", "Name" : "SampleTaskTemplate2", "NumberofInputAssets" : 1, "NumberofOutputAssets" : 1}] }


> [!NOTE]
> 不同於其他媒體服務實體，您必須為每個 TaskTemplate 定義新的 GUID 識別碼，並將它放在 hello taskTemplateId 與 Id 屬性中，要求主體中。 hello 內容識別配置必須依照 hello 配置識別 Azure 媒體服務實體中所述。 而且，不能更新 JobTemplate。 相反地，您必須使用更新後的變更建立一個新的 JobTemplate。
>
>

如果成功，則會傳回下列回應 hello:

    HTTP/1.1 201 Created

    . . .


下列範例會示範如何 hello toocreate 參考 JobTemplate 識別碼的工作：

    POST https://media.windows.net/API/Jobs HTTP/1.1
    Content-Type: application/json;odata=verbose
    Accept: application/json;odata=verbose
    DataServiceVersion: 3.0
    MaxDataServiceVersion: 3.0
    x-ms-version: 2.11
    Authorization: Bearer <token value>
    Host: media.windows.net


    {"Name" : "NewTestJob", "InputMediaAssets" : [{"__metadata" : {"uri" : "https://media.windows.net/api/Assets('nb%3Acid%3AUUID%3A3f1fe4a2-68f5-4190-9557-cd45beccef92')"}}], "TemplateId" : "nb:jtid:UUID:15e6e5e6-ac85-084e-9dc2-db3645fbf0aa"}


如果成功，則會傳回下列回應 hello:

    HTTP/1.1 201 Created

    . . .



## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="next-steps"></a>後續步驟
您現在知道如何 toocreate 作業 tooencode 資產，請參閱[toocheck 如何工作進度與 Media Services](media-services-rest-check-job-progress.md)。

## <a name="see-also"></a>另請參閱
[取得媒體處理器](media-services-rest-get-media-processor.md)
