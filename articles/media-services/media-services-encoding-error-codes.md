---
title: "aaaAzure Media Services 編碼錯誤碼 |Microsoft 文件"
description: "本主題列出以防 hello 編碼工作執行期間發生錯誤，可能會傳回的錯誤碼..."
services: media-services
documentationcenter: 
author: juliako
manager: cfowler
editor: 
ms.assetid: ce4e939f-5aee-41f9-859d-e4429815e9f2
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/09/2017
ms.author: juliako
ms.openlocfilehash: b69b6abee797c40c9b8b8f23bf2398273c170e7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="encoding-error-codes"></a>編碼錯誤碼

hello 下表列出可能會傳回，以防 hello 編碼工作執行期間發生錯誤的錯誤碼。  tooget 錯誤詳細資料，您的.NET 程式碼，使用 hello [ErrorDetails](http://msdn.microsoft.com/library/microsoft.windowsazure.mediaservices.client.errordetail.aspx)類別。 tooget 錯誤詳細資料，您的其餘程式碼中使用 hello [ErrorDetail](https://msdn.microsoft.com/library/jj853026.aspx) REST API。

| ErrorDetail.Code | 導致發生錯誤的可能原因 |
| --- | --- |
| 不明 |執行 hello 工作時發生未知的錯誤 |
| ErrorDownloadingInputAssetMalformedContent |涵蓋下載輸入資產中之錯誤 (例如無效的檔案名稱、長度為零檔案、錯誤格式等等) 的錯誤類別。 |
| ErrorDownloadingInputAssetServiceFailure |涵蓋 hello 服務端的網路或存放裝置錯誤的範例下載時的問題的錯誤分類。 |
| ErrorParsingConfiguration |錯誤分類其中工作<see cref="MediaTask.PrivateData"/>（組態） 無效，例如 hello 組態並不是有效的系統預設值或包含無效的 XML。 |
| ErrorExecutingTaskMalformedContent |Hello hello 問題輸入媒體檔案造成失敗的 hello 工作執行期間發生的錯誤分類。 |
| ErrorExecutingTaskUnsupportedFormat |分類的錯誤，其中 hello 媒體處理器無法處理提供 hello 檔案-媒體格式不受支援，或者不符合 hello 組態。 例如，嘗試 tooproduce 具有唯一的視訊資產的僅限音訊輸出 |
| ErrorProcessingTask |在 hello 的不相關的 toocontent hello 工作處理期間所遇到 hello 媒體處理器的其他錯誤分類。 |
| ErrorUploadingOutputAsset |上傳 hello 輸出資產時的錯誤分類 |
| ErrorCancelingTask |分類的錯誤 toocover 失敗時嘗試 toocancel hello 工作 |
| TransientError |問題分類的錯誤 toocover 暫時性 （例如。 Azure 儲存體發生暫時性網路問題) |

從 hello tooget 說明**Media Services**小組，請開啟[支援票證](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。

## <a name="media-services-learning-paths"></a>媒體服務學習路徑
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

## <a name="related-articles"></a>相關文章
* [透過自訂 Media Encoder Standard 預設值來執行進階編碼工作](media-services-custom-mes-presets-with-dotnet.md)
* [配額和限制](media-services-quotas-and-limitations.md)

<!--Reference links in article-->
[1]: http://azure.microsoft.com/pricing/details/media-services/
