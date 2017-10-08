---
title: "媒體服務錯誤碼 aaaAzure |Microsoft 文件"
description: "hello 主題提供 Azure Media Services 錯誤碼的概觀。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: d3a62a64-7608-4b17-8667-479b26ba0d6c
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: juliako
ms.openlocfilehash: de1ffd6dee8901a3051eb5032536c3669482d6b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-media-services-error-codes"></a>Azure 媒體服務錯誤代碼
使用 Microsoft Azure 媒體服務時，可能會從根據問題，例如驗證權杖過期 Media Services 中不支援的 tooactions hello 服務收到 HTTP 錯誤碼。 hello 以下是一份**HTTP 錯誤碼**，可能會傳回由 Media Services 和 hello 可能會導致它們。  

## <a name="400-bad-request"></a>400 不正確的要求
hello 要求包含無效的資訊，但遭到拒絕，因為下列原因 hello 的 tooone:

* 指定了不支援的 API 版本。 Hello 最新版本，請參閱[Media Services REST API 開發的安裝程式](media-services-rest-how-to-use.md)。
* 未指定的媒體服務的 hello API 版本。 如需如何 toospecify hello API 版本資訊，請參閱[媒體服務作業的 REST API 參考](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)。
  
  > [!NOTE]
  > 如果您使用 hello.NET 或 Java Sdk tooconnect tooMedia hello API 版本的服務會為您指定每當您再試一次，並執行某些動作，對媒體服務。
  > 
  > 
* 已指定未定義的屬性。 hello 屬性名稱已在 hello 錯誤訊息。 只能指定屬於指定實體的屬性。 請參閱 [Azure 媒體服務 REST API 參考](https://docs.microsoft.com/rest/api/media/operations/azure-media-services-rest-api-reference)，以取得實體及其屬性的清單。
* 已指定無效的屬性值。 hello 屬性名稱已在 hello 錯誤訊息。 請參閱 hello 前一個連結的有效屬性類型和其值。
* 遺漏必要的屬性值。
* 部分指定 hello URL 包含不正確的值。
* 嘗試進行 tooupdate WriteOnce 屬性。
* 嘗試進行 toocreate 具有未指定，或無法判斷主要 AssetFile 的輸入的資產的工作。
* 嘗試進行 tooupdate SAS 定位器。 僅能建立或刪除 SAS 定位器。 可以更新串流定位器。 如需詳細資訊，請參閱[定位器](https://docs.microsoft.com/rest/api/media/operations/locator)。
* 不支援的作業或查詢已提交。

## <a name="401-unauthorized"></a>401 未經授權
（之前會授權它），無法驗證 hello 要求到期 tooone 的 hello 下列原因：

* 遺失驗證標頭。
* 不正確的驗證標頭值。
  * hello token 已過期。 
  * hello token 包含無效的簽章。

## <a name="403-forbidden"></a>403 禁止
不允許到期 hello 要求 tooone 的 hello 下列原因：

* 找不到 hello Media Services 帳戶，或已刪除。
* hello Media Services 帳戶已停用，且 hello 要求類型不是 HTTP GET。 服務作業也會傳回 403 回應。
* hello 驗證權杖不含 hello 使用者認證資訊： AccountName 及/或訂用帳戶 Id。 Hello Azure 管理入口網站中，媒體服務帳戶，您可以在 hello Media Services UI 延伸模組中找到這項資訊。
* 無法存取 hello 的資源。
  
  * 嘗試進行 toouse 不適用於您的 Media Services 帳戶 mediaprocessor 」 轉換。
  * 已嘗試的 tooupdate JobTemplate 定義由 Media Services。
  * 嘗試進行 toooverwrite 某些其他媒體服務帳戶的定位器。
  * 嘗試進行 toooverwrite 某些其他媒體服務帳戶的 ContentKey。
* 無法建立 hello 資源，因為 tooa hello Media Services 帳戶已達到的服務配額。 如需有關 hello 服務配額的詳細資訊，請參閱[配額和限制](media-services-quotas-and-limitations.md)。

## <a name="404-not-found"></a>404 找不到
在資源上不允許 hello 要求到期 tooone 的 hello 下列原因：

* 嘗試進行 tooupdate 實體不存在。
* 嘗試進行 toodelete 實體不存在。
* 嘗試進行 toocreate 連結 tooan 實體不存在的實體。
* 嘗試進行 tooGET 實體不存在。
* 嘗試進行 toospecify 未與 hello Media Services 帳戶相關聯的儲存體帳戶。  

## <a name="409-conflict"></a>409 衝突
不允許到期 hello 要求 tooone 的 hello 下列原因：

* 一個以上的 AssetFile 有 hello hello 資產內指定的名稱。
* 已嘗試第二個 toocreate 主要 AssetFile hello 資產中的。
* 已嘗試 toocreate hello 與 ContentKey 指定已在使用中的識別碼。
* 已嘗試 toocreate 以 hello 的定位器指定已在使用中的識別碼。
* 一個以上的 IngestManifestFile 有 hello hello IngestManifest 中指定的名稱。
* 嘗試進行第二個儲存體加密 ContentKey toohello toolink 儲存體加密資產。
* 已嘗試 toolink hello 相同 ContentKey toohello 資產。
* 已嘗試的 toocreate 與 hello 資產相關聯的定位器 tooan 資產的儲存體容器遺漏或已不存在。
* 嘗試進行 toocreate 定位器 tooan 已經有使用中的 5 定位器的資產。 （azure 儲存體會強制執行上一個儲存體容器的五個共用的存取原則的 hello 的限制）。
* 連結的資產 tooan IngestManifestAsset 的儲存體帳戶不是 hello 父系 IngestManifest hello 相同 hello 儲存體帳戶使用。  

## <a name="500-internal-server-error"></a>500 內部伺服器錯誤
Hello hello 要求處理期間 Media Services 會遇到錯誤，阻礙 hello 處理無法繼續。 這可能是因下列原因 hello 的 tooone:

* 建立資產或作業就會失敗，因為暫時無法使用 hello Media Services 帳戶的服務配額資訊。
* 建立資產或 IngestManifest blob 儲存體容器就會失敗，因為暫時無法使用 hello 帳戶的儲存體帳戶資訊。
* 其他未預期的錯誤。

## <a name="503-service-unavailable"></a>503 服務無法使用
目前無法 tooreceive 要求 hello 伺服器。 這個錯誤可能是過多要求 toohello 服務所造成。 媒體服務節流機制會限制應用程式而言過多要求 toohello 服務 hello 資源使用的狀況。

> [!NOTE]
> 核取 hello 錯誤訊息和錯誤程式碼字串 tooget 所得的 hello 原因的相關資訊的詳細 hello 503 錯誤。 此錯誤不一定表示節流。
> 
> 

可能的狀態描述為︰

* 「伺服器忙碌中。 先前執行此類型的要求超過 {0} 秒。」
* 「伺服器忙碌中。 每秒可以節流超過 {0} 個要求。」
* 「伺服器忙碌中。 {1} 秒內可以節流超過 {0} 個要求。」

toohandle 這個錯誤，建議使用指數型撤退重試邏輯。 這表示在連續錯誤回應的重試之間使用越來越久的等候。  如需詳細資訊，請參閱[暫時性錯誤處理應用程式區塊](https://msdn.microsoft.com/library/hh680905.aspx)。

> [!NOTE]
> 如果您使用[Azure Media Services SDK for.Net](https://github.com/Azure/azure-sdk-for-media-services/tree/master)，已由 hello SDK 實作 hello 503 錯誤的 hello 重試邏輯。  
> 
> 

## <a name="see-also"></a>另請參閱
[媒體服務管理錯誤代碼](http://msdn.microsoft.com/library/windowsazure/dn167016.aspx)

## <a name="next-steps"></a>後續步驟
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

