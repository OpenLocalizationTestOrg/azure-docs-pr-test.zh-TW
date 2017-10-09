---
title: "aaaCommon FabricClient 擲回例外狀況 |Microsoft 文件"
description: "Hello 常見的例外狀況和錯誤可以在執行應用程式和叢集管理作業時擲回的 hello FabricClient 應用程式開發介面的描述。"
services: service-fabric
documentationcenter: .net
author: rwike77
manager: timlt
editor: 
ms.assetid: bb821313-b221-479f-b08e-36cf07e60a07
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/01/2017
ms.author: ryanwi
ms.openlocfilehash: 55bb556b25150524ebc28756eb1bd3e91dc37853
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="common-exceptions-and-errors-when-working-with-hello-fabricclient-apis"></a>常見的例外狀況和錯誤處理 hello FabricClient Api 時
hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) Api 可讓叢集和應用程式系統管理員 tooperform 系統管理工作 Service Fabric 應用程式、 服務或叢集上的。 例如，應用程式部署、 升級和移除檢查 hello 健全狀況叢集中，或測試服務。 應用程式開發人員 」 和 「 叢集系統管理員可以使用 hello FabricClient Api toodevelop 工具來管理 hello Service Fabric 叢集與應用程式。

使用 FabricClient 可以執行許多不同類型的作業。  每個方法可以擲回例外狀況，因為 tooincorrect 輸入、 執行階段發生錯誤或暫時性的基礎結構問題的錯誤。  請參閱 hello 應用程式開發介面參考文件 toofind 特定的方法所擲回的例外狀況。 不過，許多不同的 [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient) API 可能會擲回一些例外狀況。 hello 下表列出在 hello FabricClient Api 上是常見的 hello 例外狀況。

| 例外狀況 | 擲回時機 |
| --- |:--- |
| [System.Fabric.FabricObjectClosedException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricobjectclosedexception#System_Fabric_FabricObjectClosedException) |hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient)物件處於已關閉狀態。 處置 hello [FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient)物件使用，和具現化新[FabricClient](https://docs.microsoft.com/dotnet/api/system.fabric.fabricclient#System_Fabric_FabricClient)物件。 |
| [System.TimeoutException](https://docs.microsoft.com/dotnet/core/api/system.timeoutexception#System_TimeoutException) |hello 作業已逾時。[OperationTimedOut](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) hello 作業會採用多個 MaxOperationTimeout toocomplete 時，會傳回。 |
| [System.UnauthorizedAccessException](https://docs.microsoft.com/dotnet/core/api/system.unauthorizedaccessexception#System_UnauthorizedAccessException) |hello hello 作業的存取檢查失敗。 傳回 E_ACCESSDENIED。 |
| [System.Fabric.FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException) |執行 hello 作業時發生執行階段錯誤。 任何 hello FabricClient 方法可以可能擲回[FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException)，hello [ErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException_ErrorCode)屬性會指出 hello hello 例外狀況的確切原因。 錯誤代碼定義在 hello [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode)列舉型別。 |
| [System.Fabric.FabricTransientException](https://docs.microsoft.com/dotnet/api/system.fabric.fabrictransientexception#System_Fabric_FabricTransientException) |hello 作業失敗，因為某些種類的 tooa 暫時性的錯誤狀況。 例如，作業可能因暫時無法到達複本的仲裁而失敗。 暫時性例外狀況對應 toofailed 作業可以重試。 |

[FabricException](https://docs.microsoft.com/dotnet/api/system.fabric.fabricexception#System_Fabric_FabricException) 中傳回的一些常見 [FabricErrorCode](https://docs.microsoft.com/dotnet/api/system.fabric.fabricerrorcode#System_Fabric_FabricErrorCode) 錯誤：

| 錯誤 | 條件 |
| --- |:--- |
| CommunicationError |通訊錯誤，造成 hello 作業 toofail，重試 hello 操作。 |
| InvalidCredentialType |hello 認證類型無效。 |
| InvalidX509FindType |hello X509FindType 無效。 |
| InvalidX509StoreLocation |hello X509 存放區位置無效。 |
| InvalidX509StoreName |hello X509 存放區名稱不正確。 |
| InvalidX509Thumbprint |hello X509 憑證指模字串無效。 |
| InvalidProtectionLevel |hello 保護層級無效。 |
| InvalidX509Store |無法開啟 hello X509 憑證存放區。 |
| InvalidSubjectName |hello 主體名稱無效。 |
| InvalidAllowedCommonNameList |hello 通用名稱清單字串的格式不正確。 它應該是以逗號分隔的清單。 |

