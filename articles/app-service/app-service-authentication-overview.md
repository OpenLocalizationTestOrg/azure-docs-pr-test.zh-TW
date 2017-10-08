---
title: "aaaAuthentication 和 Azure App Service 中的授權 |Microsoft 文件"
description: "概念參考和概觀 hello 驗證 / 授權功能的 Azure 應用程式服務"
services: app-service
documentationcenter: 
author: mattchenderson
manager: erikre
editor: 
ms.assetid: b7151b57-09e5-4c77-a10c-375a262f17e5
ms.service: app-service
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 08/29/2016
ms.author: mahender
ms.openlocfilehash: dc2074b16cce47b72b78ea7afeda89dbc4832166
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-app-service"></a>Azure App Service 中的驗證與授權
## <a name="what-is-app-service-authentication--authorization"></a>什麼是 App Service 驗證 / 授權？
應用程式服務驗證 / 授權是使用者在您的應用程式 toosign 提供一個方法，因此 hello 應用程式後端沒有 toochange 程式碼的功能。 提供簡單的方式 tooprotect 應用程式和工作每個使用者資料。

App Service 使用同盟身分識別，由第三方識別提供者儲存帳戶並驗證使用者。 hello 應用程式會依賴 hello 提供者的身分識別資訊，如此 hello 應用程式不需要 toostore 本身的資訊。 應用程式服務支援 hello 現成的五個身分識別提供者： Azure Active Directory、 Facebook、 Google、 Microsoft 帳戶和 Twitter。 您的應用程式可以使用任何數目的這些身分識別提供者 tooprovide 使用者選項的方式登入。 tooexpand hello 內建支援，您可以整合其他身分識別提供者或[自己的自訂身分識別解決方案][custom-auth]。

如果您想 tooget 立即開始，請參閱下列教學課程的 hello 的其中一個：

* [新增驗證 tooyour iOS 應用程式][ iOS] (或[Android]， [Windows]， [Xamarin.iOS]， [Xamarin.Android]， [Xamarin.Forms]，或[Cordova])
* [Azure App Service 中 API Apps 的使用者驗證][apia-user]
* [開始使用 Azure App Service - 第 2 部分][web-getstarted]

## <a name="how-authentication-works-in-app-service"></a>App Service 中驗證的運作方式
在使用其中一種 hello 身分識別提供者順序 tooauthenticate，您必須先 tooconfigure hello 身分識別提供者 tooknow 有關您的應用程式。 識別碼和機密資料，您必須提供 tooApp 服務，然後將提供 hello 身分識別提供者。 如此即完成 hello 信任關係，讓應用程式服務可以驗證使用者的判斷提示，例如驗證語彙基元、 從 hello 身分識別提供者。

在使用這些提供者的其中一個使用者 toosign，hello 使用者必須登入使用者，該提供者的重新導向的 tooan 端點。 如果客戶使用網頁瀏覽器，您可以讓應用程式服務自動直接登入使用者的所有未經驗證的使用者 toohello 端點。 否則，您將需要 toodirect 客戶太`{your App Service base URL}/.auth/login/<provider>`，其中`<provider>`是 hello 下列值之一： aad、 facebook、 google、 microsoft 或 twitter。 在本文稍後各節說明行動和 API 的案例。

透過網頁瀏覽器來與您的應用程式互動的使用者會設定 Cookie，以便在瀏覽您的應用程式時，能夠維持在已驗證的狀態。 其他的用戶端類型，例如行動裝置、 JSON web 權杖 (JWT)，這應該會看到在 hello`X-ZUMO-AUTH`標頭，將會發出 toohello 用戶端。 hello 行動應用程式用戶端 Sdk 將為您處理這。 或者，Azure Active Directory 識別權杖或存取權杖可能會直接包含在 hello`Authorization`標頭做為[持有人權杖](https://tools.ietf.org/html/rfc6750)。

應用程式服務將會驗證任何 cookie 或您的應用程式發出 tooauthenticate 使用者語彙基元。 toorestrict 可以存取您的應用程式，請參閱 hello[授權](#authorization)本文中稍後的章節。

### <a name="mobile-authentication-with-a-provider-sdk"></a>使用提供者 SDK 的行動驗證
Hello 後端設定的所有項目之後，您可以修改行動用戶端 toosign 入應用程式服務。 有以下兩種方法：

* 使用指定的身分識別提供者發行 tooestablish 身分識別的 SDK 和便得以存取 tooApp 服務。
* 使用單行程式碼，讓該 hello 行動應用程式用戶端 SDK 可以登入使用者。

> [!TIP]
> 大部分的應用程式應該使用提供者 SDK tooget 更一致的經驗使用者登入時，toouse 重新整理支援，以及 tooget 該 hello 提供者會指定其他優點。
> 
> 

當您使用的提供者 SDK，使用者可以登入 tooan 體驗整合更緊密地與 hello 作業系統該 hello 應用程式上執行。 這也會提供權杖提供者以及某些使用者有關 hello 用戶端，以讓您更容易 tooconsume graph Api 和自訂 hello 使用者經驗。 有時候在部落格和論壇，您會看到此參照的 tooas hello 「 用戶端流程 」 或者 「 用戶端導向流程 」 因為 hello 用戶端上的程式碼登入使用者和 hello 用戶端程式碼擁有存取 tooa 提供者的語彙基元。

取得提供者的語彙基元之後，它會需要 toobe 傳送 tooApp 服務進行驗證。 應用程式服務會驗證 hello 語彙基元之後，應用程式服務會建立新的應用程式的服務權杖傳回 toohello 用戶端。 hello 行動應用程式用戶端 SDK helper 方法 toomanage 此交換，而且會自動附加 hello 語彙基元 tooall 要求 toohello 應用程式後端。 如果選擇這樣做的話，開發人員也可以讓參考 toohello 提供者語彙基元。

### <a name="mobile-authentication-without-a-provider-sdk"></a>不使用提供者 SDK 的行動驗證
若不想使用 tooset 設定的提供者 SDK，您可以為您允許在 Azure App Service toosign hello 行動應用程式功能。 hello 行動應用程式用戶端 SDK 將會開啟您所選擇的 toohello web 檢視提供者，並登入 hello 使用者。 有時候在部落格和論壇，您會看到此參照的 tooas hello 「 伺服器流程 」 或 「 伺服器導向流程 」 hello 伺服器負責管理 hello 程序的登入的使用者，因此 hello client SDK 永遠不會收到 hello 提供者的語彙基元。

程式碼的 toostart 此流程包含在 hello 驗證教學課程中的每個平台。 在 hello hello 流程結尾，hello client SDK 有應用程式服務的語彙基元，且 hello 權杖自動附加的 tooall 要求 toohello 應用程式後端。

### <a name="service-to-service-authentication"></a>服務對服務驗證
雖然您可以授與使用者存取 tooyour 應用程式，您也可以信任其他應用程式 toocall 您自己的 API。 例如，您可以讓一個 Web 應用程式呼叫另一個 Web 應用程式中的 API。 在此案例中，您可以使用認證的服務帳戶，而不是使用者認證 tooget 語彙基元。 在 Azure Active Directory 用語中，服務帳戶亦稱為 *服務主體* ，而使用這類帳戶的驗證又稱為「服務對服務案例」。

> [!IMPORTANT]
> 由於行動應用程式是在客戶裝置上執行，因此行動應用程式「不算」是信任的應用程式，不應該使用服務主體流程。 反之，行動應用程式應該使用稍早詳述的使用者流程。
> 
> 

在服務對服務案例下，App Service 可以使用 Azure Active Directory 保護您的應用程式。 hello 呼叫的應用程式只需要 tooprovide 藉由提供 hello 用戶端識別碼和密碼從 Azure Active Directory 用戶端取得 Azure Active Directory 服務主體的授權權杖。 此案例中，使用 ASP.NET 應用程式開發介面應用程式的範例會說明 hello 教學課程中，由[API 應用程式的服務主體驗證][apia-service]。

如果您想 toouse 應用程式服務驗證 toohandle 服務對服務案例，您可以使用用戶端憑證驗證或基本驗證。 在 Azure 中的用戶端憑證的相關資訊，請參閱[如何 tooConfigure TLS 相互驗證 Web 應用程式](../app-service-web/app-service-web-configure-tls-mutual-auth.md)。 如需 ASP.NET 中的基本驗證相關資訊，請參閱 [ASP.NET Web API 2 中的驗證篩選](http://www.asp.net/web-api/overview/security/authentication-filters)。

從應用程式服務的邏輯應用程式 tooan API 應用程式的服務帳戶驗證是特殊案例中詳[使用您裝載邏輯應用程式的 App Service 上的自訂 API](../logic-apps/logic-apps-custom-hosted-api.md)。

## <a name="authorization"></a>App Service 中授權的運作方式
您擁有 hello 要求可以存取您的應用程式的完整控制權。 應用程式服務驗證 / 授權可以設定與任何 hello 下列行為：

* 只有已驗證的要求 tooreach 可讓您的應用程式。
  
    如果瀏覽器接收的匿名要求，應用程式服務會重新導向 tooa hello 身分識別提供者，您可以選擇，讓使用者可以登入頁面。 Hello hello 要求來自於行動裝置，如果傳回的回應是 HTTP *401 未授權*回應。
  
    使用此選項，您不需要 toowrite 任何驗證程式碼在應用程式中。 如果您需要更精細的授權，使用 tooyour 程式碼的相關 hello 使用者資訊。
* 允許所有要求 tooreach 應用程式，但驗證已驗證的要求，並傳遞 hello HTTP 標頭中的驗證資訊。
  
    此選項會延後的授權決策 tooyour 應用程式程式碼。 它提供更有彈性地處理匿名要求，但您有 toowrite 程式碼。
* 允許所有要求 tooreach 應用程式，並在 hello 要求中的驗證資訊採取任何動作。
  
    在此情況下，hello 驗證/授權功能已關閉。 hello 工作的驗證和授權都已完全啟動 tooyour 應用程式程式碼。

hello 先前的行為，皆受 hello**當要求未經驗證的動作 tootake** hello Azure 入口網站中的選項。 如果您選擇 * * 登入的*提供者名稱** *，所有的要求有 toobe 驗證。 **允許要求 （無動作）**會延遲 hello 授權決策 tooyour 程式碼，但它仍然會提供驗證資訊。 如果您想 toohave 您的程式碼處理的所有項目，您可以停用 hello 驗證 / 授權功能。

## <a name="working-with-user-identities-in-your-application"></a>在應用程式中使用您的使用者身分識別
應用程式服務會使用特殊標頭中傳遞某些使用者資訊 tooyour 應用程式。 外部要求會禁止這些標頭，必須由 App Service 驗證/授權設定才會出現。 某些範例標頭包括︰

* X-MS-CLIENT-PRINCIPAL-NAME
* X-MS-CLIENT-PRINCIPAL-ID
* X-MS-TOKEN-FACEBOOK-ACCESS-TOKEN
* X-MS-TOKEN-FACEBOOK-EXPIRES-ON

以任何語言或 framework 撰寫的程式碼可以取得它所需要的 hello 資訊從這些標頭。 針對 ASP.NET 4.6 的應用程式，hello **ClaimsPrincipal**以 hello 適當的值會自動設定。

您的應用程式也可以取得額外的使用者詳細資料，透過 HTTP GET 上 hello`/.auth/me`應用程式的端點。 有效的語彙基元，並包含的 hello 要求會傳回 JSON 裝載 hello 提供者所使用的相關詳細資料，請 hello 基礎提供者的語彙基元和其他使用者資訊。 hello 行動應用程式伺服器的 Sdk 提供 helper 方法 toowork 使用此資料。 如需詳細資訊，請參閱[toouse 如何 hello Azure 行動應用程式 Node.js SDK](../app-service-mobile/app-service-mobile-node-backend-how-to-use-server-sdk.md#howto-tables-getidentity)，和[Azure 行動應用程式使用 hello.NET 後端伺服器 SDK](../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#user-info)。

## <a name="documentation-and-additional-resources"></a>文件和其他資源
### <a name="identity-providers"></a>識別提供者
hello 遵循教學課程顯示如何 tooconfigure App Service toouse 不同的驗證提供者：

* [如何 tooconfigure 您的應用程式 toouse Azure Active Directory 登入][AAD]
* [如何 tooconfigure 應用程式 toouse Facebook 登入][Facebook]
* [如何 tooconfigure 應用程式 toouse Google 登入][Google]
* [如何 tooconfigure 應用程式 toouse Microsoft 帳戶登入][MSA]
* [如何 tooconfigure 您的應用程式 toouse Twitter 登入][Twitter]

如果您不想 toouse 識別系統在這裡，您也可以使用 hello 提供 hello 的[預覽 hello 行動應用程式的.NET server SDK 中的自訂驗證支援][custom-auth]，可以使用在 web 應用程式，行動應用程式或應用程式開發介面應用程式。

### <a name="web-applications"></a>Web 應用程式
hello 遵循教學課程顯示如何 tooadd 驗證 tooa web 應用程式：

* [開始使用 Azure App Service - 第 2 部分][web-getstarted]

### <a name="mobile-applications"></a>行動應用程式
hello 遵循教學課程顯示如何 tooadd 驗證 tooyour 行動用戶端使用 hello 伺服器導向的流程：

* [新增驗證 tooyour iOS 應用程式][iOS]
* [新增驗證 tooyour Android 應用程式][Android]
* [新增驗證 tooyour Windows 應用程式][Windows]
* [新增驗證 tooyour Xamarin.iOS 應用程式][Xamarin.iOS]
* [新增驗證 tooyour Xamarin.Android 應用程式][Xamarin.Android]
* [新增驗證 tooyour Xamarin.Forms 應用程式][Xamarin.Forms]
* [新增驗證 tooyour Cordova 應用程式][Cordova]

使用下列資源，如果您想 toouse hello 用戶端導向流量的 Azure Active Directory 的 hello:

* [使用適用於 iOS 的 hello Active Directory Authentication Library][ADAL-iOS]
* [使用適用於 Android 的 hello Active Directory Authentication Library][ADAL-Android]
* [使用 hello Active Directory 驗證程式庫適用於 Windows 及 Xamarin][ADAL-dotnet]

使用下列資源，如果您想 toouse hello 用戶端導向流程 Facebook 的 hello:

* [使用適用於 iOS 的 hello Facebook SDK](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#facebook-sdk)

使用下列資源，如果您想 toouse hello 用戶端導向流程 Twitter hello:

* [使用 Twitter Fabric for iOS](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#twitter-fabric)

使用下列資源，如果您想 toouse hello 用戶端導向流程 google hello:

* [使用適用於 iOS 的 hello Google 登入 SDK](../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#google-sdk)

### <a name="api-applications"></a>API 應用程式
hello 遵循教學課程顯示如何 tooprotect API 應用程式：

* [Azure App Service 中 API Apps 的使用者驗證][apia-user]
* [Azure App Service 中 API Apps 的服務主體驗證][apia-service]

[apia-user]: ../app-service-api/app-service-api-dotnet-user-principal-auth.md
[apia-service]: ../app-service-api/app-service-api-dotnet-service-principal-auth.md

[web-getstarted]: ../app-service-web/app-service-web-get-started-2.md#authenticate-your-users

[iOS]: ../app-service-mobile/app-service-mobile-ios-get-started-users.md
[Android]: ../app-service-mobile/app-service-mobile-android-get-started-users.md
[Xamarin.iOS]: ../app-service-mobile/app-service-mobile-xamarin-ios-get-started-users.md
[Xamarin.Android]: ../app-service-mobile/app-service-mobile-xamarin-android-get-started-users.md
[Xamarin.Forms]: ../app-service-mobile/app-service-mobile-xamarin-forms-get-started-users.md
[Windows]: ../app-service-mobile/app-service-mobile-windows-store-dotnet-get-started-users.md
[Cordova]: ../app-service-mobile/app-service-mobile-cordova-get-started-users.md

[AAD]: ../app-service-mobile/app-service-mobile-how-to-configure-active-directory-authentication.md
[Facebook]: ../app-service-mobile/app-service-mobile-how-to-configure-facebook-authentication.md
[Google]: ../app-service-mobile/app-service-mobile-how-to-configure-google-authentication.md
[MSA]: ../app-service-mobile/app-service-mobile-how-to-configure-microsoft-authentication.md
[Twitter]: ../app-service-mobile/app-service-mobile-how-to-configure-twitter-authentication.md

[custom-auth]: ../app-service-mobile/app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth

[ADAL-Android]: ../app-service-mobile/app-service-mobile-android-how-to-use-client-library.md#adal
[ADAL-iOS]: ../app-service-mobile/app-service-mobile-ios-how-to-use-client-library.md#adal
[ADAL-dotnet]: ../app-service-mobile/app-service-mobile-dotnet-how-to-use-client-library.md#adal
