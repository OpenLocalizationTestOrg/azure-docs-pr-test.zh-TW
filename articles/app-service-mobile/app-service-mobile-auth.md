---
title: "aaaAuthentication 和 Azure 行動應用程式中的授權 |Microsoft 文件"
description: "概念式的參考和概觀 hello 驗證 / 授權功能的 Azure 行動應用程式"
services: app-service\mobile
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: a46dbf70-867d-48f6-8885-7f5207ad102e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5255734481ada11afb65982aebe45c2a349402fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a>Azure Mobile Apps 中的驗證與授權
## <a name="what-is-app-service-authentication--authorization"></a>什麼是 App Service 驗證 / 授權？
> [!NOTE]
> 本主題將會移轉的 tooa 合併[應用程式服務驗證 / 授權](../app-service/app-service-authentication-overview.md)主題，其中涵蓋了網頁、 行動裝置版及 API 應用程式。
> 
> 

應用程式服務驗證 / 授權是一項功能可讓在使用者的應用程式 toolog hello 應用程式後端上無須任何程式碼變更。 提供簡單的方式 tooprotect 應用程式和工作每個使用者資料。

應用程式服務會在其中使用同盟識別身分，3rd 合作對象**身分識別提供者**""(IDP) 儲存帳戶、 驗證使用者和 hello 應用程式會使用這個身分識別而非其本身。 應用程式服務支援 hello 現成的五個身分識別提供者： *Azure Active Directory*， *Facebook*， *Google*， *Microsoft 帳戶*，和*Twitter*。 您也可以藉由整合其他身分識別提供者或您自己自訂的身分識別解決方案，針對您的 app 延伸此支援。

您的 app 可以利用任意數目的這類身分識別提供者，因此可為您的使用者提供登入選項。

如果您想 tooget 立即開始，請參閱下列教學課程的 hello 的其中一個：

* [新增驗證 tooyour iOS 應用程式]
* [新增驗證 tooyour Xamarin.iOS 應用程式]
* [新增驗證 tooyour Xamarin.Android 應用程式]
* [新增驗證 tooyour Windows 應用程式]

## <a name="how-authentication-works"></a>驗證的運作方式
在使用其中一種 hello 身分識別提供者順序 tooauthenticate，您必須先 tooconfigure hello 身分識別提供者 tooknow 有關您的應用程式。 hello 身分識別提供者再將提供您識別碼與回復 toohello 應用程式提供的密碼。 這樣會完成 hello 信任關係，並讓應用程式服務 toovalidate 身分識別提供 tooit。

Hello 下列主題中詳述這些步驟：

* [如何 tooconfigure 您的應用程式 toouse Azure Active Directory 登入]
* [如何 tooconfigure 應用程式 toouse Facebook 登入]
* [如何 tooconfigure 應用程式 toouse Google 登入]
* [如何 tooconfigure 應用程式 toouse Microsoft 帳戶登入]
* [如何 tooconfigure 您的應用程式 toouse Twitter 登入]

一旦所有項目設定 hello 後端上，您可以修改您的用戶端 toolog 中。 有以下兩種方法：

* 使用單行程式碼，讓 hello 行動應用程式登入使用者的用戶端 SDK。
* 利用所指定的身分識別提供者 tooestablish 身分發行的 SDK，和便得以存取 tooApp 服務。

> [!TIP]
> 大部分的應用程式應該使用提供者 SDK tooget 更原生感覺登入體驗和 tooleverage 重新整理支援和其他提供者特有的優點。
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a>不使用提供者 SDK 進行驗證的運作方式
如果您不想 tooset 設定的提供者 SDK，您可以為您允許行動裝置應用程式 tooperform hello 登入。 hello 行動應用程式用戶端 SDK 將會開啟您選擇且完整的 hello 登入的 web 檢視 toohello 提供者。 有時候在部落格和論壇，您會看到這稱為 tooas hello 「 伺服器流程 」 或 「 伺服器導向流程 」 自 hello server 來管理 hello 登入，且 hello client SDK 永遠不會收到 hello 提供者的語彙基元。

hello 程式碼需要在每個平台的 hello 驗證教學課程涵蓋此流程 toostart。 在 hello hello 流程結尾，hello client SDK 有應用程式服務的語彙基元，且 hello 權杖自動附加的 tooall 要求 toohello 後端。

### <a name="how-authentication-with-a-provider-sdk-works"></a>使用提供者 SDK 進行驗證的運作方式
使用提供者 SDK 可讓 hello 登入經驗 toointeract 更緊密地與 hello 平台執行作業系統 hello 應用程式。 這也會提供權杖提供者以及某些使用者有關 hello 用戶端，以讓您更容易 tooconsume graph Api 和自訂 hello 使用者經驗。 偶爾部落格和論壇上您會看到此參照的 tooas hello 「 用戶端流程 」 或 「 用戶端導向流程 」 之後的程式碼 hello 用戶端上處理 hello 登入，而且 hello 用戶端程式碼具有存取 tooa 提供者的語彙基元。

一旦取得提供者的語彙基元時，它就會需要 toobe 傳送 tooApp 服務進行驗證。 在 hello hello 流程結尾，hello client SDK 有應用程式服務的語彙基元，且 hello 權杖自動附加的 tooall 要求 toohello 後端。 如果選擇這樣做的話，hello 開發人員也可以讓參考 toohello 提供者語彙基元。

## <a name="how-authorization-works"></a>授權的運作方式
應用程式服務驗證 / 授權會公開數個選項的**當要求未經驗證的動作 tootake**。 您的程式碼會接收指定的要求之前，您可以有應用程式服務的核取 toosee 如果 hello 要求驗證而且如果沒有，請予以拒絕並嘗試 toohave hello 使用者登入後再重試。

其中一個選項是 toohave 未經驗證的要求重新導向 tooone hello 身分識別提供者。 在 web 瀏覽器中，這實際上會需要 hello 使用者 tooa 新頁面。 不過，如此一來，您的行動用戶端就無法重新導向，而且未經驗證的回應將會收到 HTTP「401 未經授權」回應。 根據這點，可讓您的用戶端 hello 第一個要求應該一律 toohello 登入端點，且則您可以讓其他應用程式開發介面呼叫 tooany。 如果您嘗試 toocall 另一個應用程式開發介面登入之前，您的用戶端會收到錯誤。

如果您想 toohave 更細微控制哪些端點透過要求驗證，您也可以選擇 「 採取任何動作 （允許要求） 」 的未經驗證的要求。 在此情況下，才會延期驗證的所有決策 tooyour 應用程式程式碼。 這也可讓您根據自訂授權規則 tooallow 存取 toospecific 使用者。

## <a name="documentation"></a>文件
hello 遵循教學課程顯示如何 tooadd 驗證 tooyour 行動用戶端使用應用程式服務：

* [新增驗證 tooyour iOS 應用程式]
* [新增驗證 tooyour Xamarin.iOS 應用程式]
* [新增驗證 tooyour Xamarin.Android 應用程式]
* [新增驗證 tooyour Windows 應用程式]

hello 遵循教學課程顯示如何 tooconfigure App Service tooleverage 不同的驗證提供者：

* [如何 tooconfigure 您的應用程式 toouse Azure Active Directory 登入]
* [如何 tooconfigure 應用程式 toouse Facebook 登入]
* [如何 tooconfigure 應用程式 toouse Google 登入]
* [如何 tooconfigure 應用程式 toouse Microsoft 帳戶登入]
* [如何 tooconfigure 您的應用程式 toouse Twitter 登入]

如果您想 toouse 識別系統以外在這裡，您也可以利用 hello 提供 hello 的[預覽 hello.NET server SDK 中的自訂驗證支援](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth)。

[新增驗證 tooyour iOS 應用程式]: app-service-mobile-ios-get-started-users.md
[新增驗證 tooyour Xamarin.iOS 應用程式]: app-service-mobile-xamarin-ios-get-started-users.md
[新增驗證 tooyour Xamarin.Android 應用程式]: app-service-mobile-xamarin-android-get-started-users.md
[新增驗證 tooyour Windows 應用程式]: app-service-mobile-windows-store-dotnet-get-started-users.md

[如何 tooconfigure 您的應用程式 toouse Azure Active Directory 登入]: app-service-mobile-how-to-configure-active-directory-authentication.md
[如何 tooconfigure 應用程式 toouse Facebook 登入]: app-service-mobile-how-to-configure-facebook-authentication.md
[如何 tooconfigure 應用程式 toouse Google 登入]: app-service-mobile-how-to-configure-google-authentication.md
[如何 tooconfigure 應用程式 toouse Microsoft 帳戶登入]: app-service-mobile-how-to-configure-microsoft-authentication.md
[如何 tooconfigure 您的應用程式 toouse Twitter 登入]: app-service-mobile-how-to-configure-twitter-authentication.md
