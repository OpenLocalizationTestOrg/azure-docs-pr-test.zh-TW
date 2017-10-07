---
title: "行動應用程式和行動服務中的 aaaClient 和伺服器 SDK 版本設定 |Microsoft 文件"
description: "列出適用於行動服務和 Azure Mobile Apps 的用戶端 SDK 和與伺服器 SDK 版本的相容性"
services: app-service\mobile
documentationcenter: 
author: ggailey777
manager: syntaxc4
editor: 
ms.assetid: 35b19672-c9d6-49b5-b405-a6dcd1107cd5
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: mobile-multiple
ms.devlang: dotnet
ms.topic: article
ms.date: 10/01/2016
ms.author: glenga
ms.openlocfilehash: 5874b7455ea407ca8c77fb1bd03d97d0767ebb47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="client-and-server-versioning-in-mobile-apps-and-mobile-services"></a>Mobile Apps 和行動服務中的用戶端和伺服器版本控制
hello 最新版本的 Azure Mobile Services 為 hello**行動應用程式**Azure 應用程式服務的功能。

hello 行動裝置應用程式用戶端和伺服器 Sdk 原本根據行動服務中的項目，但是可以*不*彼此相容。
也就是說，您必須使用 Mobile Apps 用戶端 SDK 搭配 Mobile Apps 伺服器 SDK，「行動服務」也是類似作法。 透過 hello 用戶端和伺服器 Sdk，所使用的特殊標頭值強制執行這項契約`ZUMO-API-VERSION`。

注意： 這份文件是指的每當 tooa*行動服務*後端，就不一定需要 toobe 裝載於行動服務。 它現在可能 toomigrate App Service 上的行動服務 toorun 不需要變更任何程式碼，但 hello 服務仍會在使用*行動服務*SDK 版本。

深入了解 toolearn 移轉 tooApp 服務不需要變更任何程式碼，請參閱 hello 文章[移轉應用程式服務的行動服務 tooAzure]。

## <a name="header-specification"></a>標頭規格
hello 金鑰`ZUMO-API-VERSION`可能 hello HTTP 標頭或 hello 查詢字串中指定。 hello 值為 hello 格式的版本字串**x.y.z**。

例如：

GET https://service.azurewebsites.net/tables/TodoItem

HEADERS: ZUMO-API-VERSION: 2.0.0

POST https://service.azurewebsites.net/tables/TodoItem?ZUMO-API-VERSION=2.0.0

## <a name="opting-out-of-version-checking"></a>選擇不進行版本檢查
您可以選擇退出版本檢查設定的值**true** hello 應用程式設定**MS_SkipVersionCheck**。 在 web.config 中或在 hello hello Azure 入口網站應用程式設定 區段中，請指定這個選項。

> [!NOTE]
> 有一些行動服務和行動應用程式，特別是在離線同步處理、 驗證和推播通知的 hello 區域之間的行為變更。 您應該只選擇退出，這些行為的變更不會中斷您的應用程式功能完整的測試 tooensure 後進行檢查的版本。
>
>

## <a name="summary-of-compatibility-for-all-versions"></a>所有版本的相容性摘要
hello 下圖顯示 hello 所有用戶端和伺服器型別之間的相容性。 後端會被分類為任一行動**服務**或行動裝置版**應用程式**hello server SDK，它會使用為基礎。

|  | **行動服務** Node.js 或 .NET | **Mobile Apps** Node.js 或 .NET |
| --- | --- | --- |
| [行動服務用戶端] |確定 |錯誤\* |
| [Mobile Apps 用戶端] |錯誤\* |確定 |

\*這可以藉由指定 **MS_SkipVersionCheck** 來控制。

<!-- IMPORTANT!  hello anchors for Mobile Services and Mobile Apps MUST be 1.0.0 and 2.0.0 respectively, since there is an exception error message that uses those anchors. -->

<!-- NOTE: hello fwlink toothis document is http://go.microsoft.com/fwlink/?LinkID=690568 -->

## <a name="1.0.0"></a>行動服務用戶端和伺服器
hello 表中的 hello 用戶端 Sdk 可與相容**行動服務**。

注意： hello 行動服務用戶端 Sdk*不*傳送的標頭值`ZUMO-API-VERSION`。 如果 hello 服務收到此標頭或查詢字串值，也將會傳回錯誤，除非您明確選擇逾時 （如上所述）。

### <a name="MobileServicesClients"></a>行動「服務」用戶端 SDK
| 用戶端平台 | 版本 | 版本標頭值 |
| --- | --- | --- |
| 受管理的用戶端 (Windows、Xamarin) |[1.3.2](https://www.nuget.org/packages/WindowsAzure.MobileServices/1.3.2) |n/a |
| iOS |[2.2.2](http://aka.ms/gc6fex) |n/a |
| Android |[2.0.3](https://go.microsoft.com/fwLink/?LinkID=280126) |n/a |
| HTML |[1.2.7](http://ajax.aspnetcdn.com/ajax/mobileservices/MobileServices.Web-1.2.7.min.js) |n/a |

### <a name="mobile-services-server-sdks"></a>行動「服務」  伺服器 SDK
| 伺服器平台 | 版本 | 接受的版本標頭 |
| --- | --- | --- |
| .NET |[WindowsAzure.MobileServices.Backend.* 版本 1.0.x](https://www.nuget.org/packages/WindowsAzure.MobileServices.Backend/) |* * 沒有版本標頭 * * |
| Node.js |(敬請期待) |**無版本標頭** |

<!-- TODO: add Node npm version -->

### <a name="behavior-of-mobile-services-backends"></a>行動服務後端的行為
| ZUMO-API-VERSION | MS_SkipVersionCheck 的值 | Response |
| --- | --- | --- |
| 未指定 |任意 |200 - 確定 |
| 任何值 |True |200 - 確定 |
| 任何值 |False/未指定 |400 - 不正確的要求 |

## <a name="2.0.0"></a>Azure Mobile Apps 用戶端和伺服器
### <a name="MobileAppsClients"></a> Mobile Apps 用戶端 SDK
版本檢查起 hello 遵循 hello client SDK 版本所導入的**Azure 行動應用程式**:

| 用戶端平台 | 版本 | 版本標頭值 |
| --- | --- | --- |
| 受管理的用戶端 (Windows、Xamarin) |[2.0.0](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Client/2.0.0) |2.0.0 |
| iOS |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=529823) |2.0.0 |
| Android |[3.0.0](http://go.microsoft.com/fwlink/?LinkID=717033&clcid=0x409) |3.0.0 |

<!-- TODO: add HTML version when released -->

### <a name="mobile-apps-server-sdks"></a>Mobile「Apps」  伺服器 SDK
下列伺服器 SDK 版本包含版本檢查：

| 伺服器平台 | SDK | 接受的版本標頭 |
| --- | --- | --- |
| .NET |[Microsoft.Azure.Mobile.Server](https://www.nuget.org/packages/Microsoft.Azure.Mobile.Server/) |2.0.0 |
| Node.js |[azure-mobile-apps)](https://www.npmjs.com/package/azure-mobile-apps) |2.0.0 |

### <a name="behavior-of-mobile-apps-backends"></a>Mobile Apps 後端的行為
| ZUMO-API-VERSION | MS_SkipVersionCheck 的值 | Response |
| --- | --- | --- |
| x.y.z 或 Null |True |200 - 確定 |
| Null |False/未指定 |400 - 不正確的要求 |
| 1.x.y |False/未指定 |400 - 不正確的要求 |
| 2.0.0-2.x.y |False/未指定 |200 - 確定 |
| 3.0.0-3.x.y |False/未指定 |400 - 不正確的要求 |

## <a name="next-steps"></a>後續步驟
* [移轉應用程式服務的行動服務 tooAzure]

[行動服務用戶端]: #MobileServicesClients
[Mobile Apps 用戶端]: #MobileAppsClients


[Mobile App Server SDK]: http://www.nuget.org/packages/microsoft.azure.mobile.server
[移轉應用程式服務的行動服務 tooAzure]: app-service-mobile-migrating-from-mobile-services.md
