---
title: "aaaRetry 邏輯 hello Media Services SDK for.NET |Microsoft 文件"
description: "hello 主題概要說明的重試邏輯中 hello Media Services SDK for.NET。"
author: Juliako
manager: cfowler
editor: 
services: media-services
documentationcenter: 
ms.assetid: 527b61a6-c862-4bd8-bcbc-b9aea1ffdee3
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: juliako
ms.openlocfilehash: 18d0a9d68e55a48bc769fb6ae5711ddba78ed8e6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="retry-logic-in-hello-media-services-sdk-for-net"></a>.NET 的重試 hello Media Services SDK 中的邏輯
當使用 Microsoft Azure 服務時，可能會發生暫時性錯誤。 如果發生暫時性錯誤，在大部分情況下，在少數的重試後 hello 作業會成功。 hello Media Services SDK for.NET 實作 hello 重試邏輯 toohandle 暫時性錯誤例外狀況和 web 要求、 執行查詢，儲存變更，以及儲存體作業所造成的錯誤相關聯。  根據預設，hello Media Services SDK for.NET 會重新擲回 hello 例外狀況 tooyour 應用程式之前執行四次重試。 您的應用程式中的 hello 程式碼再必須正確處理這個例外狀況。  

 hello 下面是簡短的 Web 要求、 儲存體、 查詢和 SaveChanges 原則指導方針：  

* hello 存放裝置原則適用於 blob 儲存體作業 （上傳或下載 asset 檔案）。  
* hello Web 要求的原則適用於一般 web 要求 （例如，用於取得驗證權杖和解決 hello 使用者叢集端點）。  
* hello 查詢原則用於查詢其餘部分 (例如，mediaContext.Assets.Where(...)) 實體。  
* hello SaveChanges 原則用來進行變更 （例如，建立更新實體，服務函式呼叫作業的實體） 的 hello 服務內的資料。  
  
  本主題列出例外狀況類型，並會由 hello Media Services SDK for.NET 的錯誤碼重試邏輯。  

## <a name="exception-types"></a>例外狀況類型
hello 下表描述該 hello Media Services SDK for.NET 的控制代碼的例外狀況或不會進行某些作業可能會造成暫時性錯誤處理。  

| 例外狀況 | Web 要求 | 儲存體 | 查詢 | SaveChanges |
| --- | --- | --- | --- | --- |
| WebException<br/>如需詳細資訊，請參閱 hello [WebException 狀態碼](media-services-retry-logic-in-dotnet-sdk.md#WebExceptionStatus)> 一節。 |是 |是 |是 |是 |
| DataServiceClientException<br/> 如需詳細資訊，請參閱 [HTTP 錯誤狀態碼](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode)。 |否 |是 |是 |是 |
| DataServiceQueryException<br/> 如需詳細資訊，請參閱 [HTTP 錯誤狀態碼](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode)。 |否 |是 |是 |是 |
| DataServiceRequestException<br/> 如需詳細資訊，請參閱 [HTTP 錯誤狀態碼](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode)。 |否 |是 |是 |是 |
| DataServiceTransportException |否 |否 |是 |是 |
| TimeoutException |是 |是 |是 |否 |
| SocketException |是 |是 |是 |是 |
| StorageException |否 |是 |否 |否 |
| IOException |否 |是 |否 |否 |

### <a name="WebExceptionStatus"></a> WebException 狀態碼
hello 下表顯示代碼 hello 重試邏輯如何實作 WebException 錯誤。 hello [WebExceptionStatus](http://msdn.microsoft.com/library/system.net.webexceptionstatus.aspx)列舉型別定義 hello 的狀態碼。  

| 狀態 | Web 要求 | 儲存體 | 查詢 | SaveChanges |
| --- | --- | --- | --- | --- |
| ConnectFailure |是 |是 |是 |是 |
| NameResolutionFailure |是 |是 |是 |是 |
| ProxyNameResolutionFailure |是 |是 |是 |是 |
| SendFailure |是 |是 |是 |是 |
| PipelineFailure |是 |是 |是 |否 |
| ConnectionClosed |是 |是 |是 |否 |
| KeepAliveFailure |是 |是 |是 |否 |
| UnknownError |是 |是 |是 |否 |
| ReceiveFailure |是 |是 |是 |否 |
| RequestCanceled |是 |是 |是 |否 |
| 逾時 |是 |是 |是 |否 |
| ProtocolError <br/>ProtocolError hello 重試受到 hello HTTP 狀態碼處理。 如需詳細資訊，請參閱 [HTTP 錯誤狀態碼](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode)。 |是 |是 |是 |是 |

### <a name="HTTPStatusCode"></a> HTTP 錯誤狀態碼
當查詢與 SaveChanges 作業擲回傳回 DataServiceClientException、 DataServiceQueryException 或 DataServiceQueryException 時，hello HTTP 錯誤狀態碼會傳回在 hello StatusCode 屬性。  hello 下表顯示的錯誤碼實作 hello 重試邏輯。  

| 狀態 | Web 要求 | 儲存體 | 查詢 | SaveChanges |
| --- | --- | --- | --- | --- |
| 401 |否 |是 |否 |否 |
| 403 |否 |是<br/>處理重試等待較久。 |否 |否 |
| 408 |是 |是 |是 |是 |
| 429 |是 |是 |是 |是 |
| 500 |是 |是 |是 |否 |
| 502 |是 |是 |是 |否 |
| 503 |是 |是 |是 |是 |
| 504 |是 |是 |是 |否 |

如果您想 tootake 查看 hello 實際實作 hello Media Services SDK for.NET 重試邏輯，請參閱[azure-sdk--媒體-服務的](https://github.com/Azure/azure-sdk-for-media-services/tree/dev/src/net/Client/TransientFaultHandling)。

## <a name="next-steps"></a>後續步驟
[!INCLUDE [media-services-learning-paths-include](../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>提供意見反應
[!INCLUDE [media-services-user-voice-include](../../includes/media-services-user-voice-include.md)]

