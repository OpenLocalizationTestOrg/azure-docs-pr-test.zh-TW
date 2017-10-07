---
title: "aaaHow tooenable 跨應用程式使用 ADAL 的 Android 上的 SSO |Microsoft 文件"
description: "如何 toouse hello 功能 hello 跨應用程式的 ADAL SDK tooenable 單一登入。 "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 3867e15030e5516464e4dbd92ba35894430daf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-android-using-adal"></a>如何 tooenable 跨應用程式使用 ADAL 的 Android 上的 SSO
現在必須由客戶提供單一登入 (SSO)，讓使用者只需要 tooenter 其認證一次，並跨應用程式具有這些認證會自動運作。 在小型螢幕上，通常時間結合其他因素 (2FA)，例如通話或簡訊的程式碼中，輸入使用者名稱和密碼的 hello 難度導致快速不滿，如果使用者有 toodo 這一次以上為您的產品。

此外，如果您套用其他應用程式可能會使用如 Microsoft 帳戶或從 Office365 工作帳戶的身分識別平台時，客戶會預期，提供其所有的應用程式 toouse 那些認證 toobe 無論 hello 廠商。

hello Microsoft 識別身分平台，以及我們 Microsoft 身分識別的 Sdk，運作所有此硬碟的您，並可讓客戶可以發生在您自己的 suite 應用程式，或做為 SSO hello 能力 toodelight 與我們的 broker 功能和驗證器跨應用程式，hello 整個裝置。

本逐步解說會告訴您如何 tooconfigure 我們 SDK 內的應用程式 tooprovide 此權益 tooyour 客戶。

本逐步解說適用於：

* Azure Active Directory
* Azure Active Directory B2C
* Azure Active Directory B2B
* Azure Active Directory 條件式存取

上述的 hello 文件假設您知道如何太[佈建 Azure Active Directory 的 hello 舊版入口網站中的應用程式](active-directory-how-to-integrate.md)hello 與整合您的應用程式和[Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a>在 hello Microsoft 識別身分平台中的 SSO 概念
### <a name="microsoft-identity-brokers"></a>Microsoft 身分識別代理人
Microsoft 提供應用程式的每個行動平台，允許不同廠商的應用程式間 hello 橋接的認證，並允許特殊的增強功能需要單一的安全位置，從哪裡 toovalidate 認證。 我們稱它們為 **訊息代理程式**。 IOS 和 Android 上提供這些項目透過可下載的應用程式的客戶獨立安裝或由負責管理其員工的部分或全部 hello 裝置的公司可以推送 toohello 裝置。 這些代理程式只用於某些應用程式或根據 IT 系統管理員想要的 hello 整個裝置支援管理安全性。 在 Windows 中，這項功能是由 toohello 作業系統，技術上來說稱為 hello Web 驗證代理人內建帳戶選擇器提供的。

如需詳細資訊，我們使用這些仲介和如何您的客戶可能會看到它們在其登入資料流程中為 hello Microsoft 身分識別平台上讀取。

### <a name="patterns-for-logging-in-on-mobile-devices"></a>在行動裝置上登入的模式
在裝置上的存取 toocredentials 遵循 hello Microsoft 識別身分平台中的兩個基本模式：

* 非訊息代理程式協助登入
* 訊息代理程式協助登入

#### <a name="non-broker-assisted-logins"></a>非訊息代理程式協助登入
非 broker 協助登入是內嵌於 hello 應用程式，就可能發生，在該應用程式的 hello 裝置上使用本機儲存體 hello 登入體驗。 這個儲存體可能會跨應用程式共用但 hello 認證緊密繫結的 toohello 應用程式或套件的應用程式使用該認證。 最有可能遭遇這許多行動應用程式中輸入使用者名稱和密碼 hello 應用程式本身內時。

這些登入具有下列優點 hello:

* 使用者經驗完全內含 hello 應用程式。
* 認證可 hello 所簽署的應用程式之間共用相同的憑證，提供單一登入體驗 tooyour 套應用程式。
* 控制項周圍的登入的 hello 經驗提供 toohello 應用程式之前和之後登入。

這些登入有下列缺點 hello:

* 使用者無法跨所有使用 Microsoft 身分識別的應用程式體驗單一登入，只會跨應用程式已設定的那些 Microsoft 身分識別。
* 您的應用程式不能與更進階的商業功能，例如條件式存取或使用 hello InTune 套件的產品。
* 您的應用程式無法針對商務使用者支援以憑證為基礎的驗證。

以下是與您的應用程式 tooenable SSO 的 hello 共用存放裝置 hello Microsoft 識別 Sdk 的運作方式的表示法：

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a>訊息代理程式協助登入
Broker 輔助登入係指 hello broker 應用程式內發生，並且套用 hello Microsoft 識別身分平台中 hello 裝置上所有應用程式使用 hello 儲存和安全性的 hello broker tooshare 認證登入體驗。 這表示您的應用程式依賴中的 hello broker toosign 使用者。 IOS 和 Android 上是在透過可下載的應用程式提供這些 broker 客戶獨立安裝或由負責管理其使用者的 hello 裝置的公司可以推送 toohello 裝置。 這種類型的應用程式的範例是在 iOS 上的 hello Microsoft 驗證器應用程式。 在 Windows 中 toohello 作業系統，技術上來說稱為 hello Web 驗證代理人內建帳戶選擇器會提供此功能。
hello 體驗會依平台而有所不同，有時可能干擾 toousers 如果未正確管理。 如果您已安裝的 hello Facebook 應用程式，並從另一個應用程式中使用 Facebook Connect，您已使用此模式可能是最熟悉。 hello Microsoft 身分識別平台使用 hello 相同的模式。

適用於 iOS 這會導致 tooa 「 過渡 」 動畫的應用程式傳送 toohello 背景 hello Microsoft 驗證器應用程式時出現的 hello 使用者 tooselect toohello 前景他們想 toosign 中使用哪一個帳戶。  

Android 和 Windows hello 帳戶選擇器會顯示在您的應用程式也就是比較不會干擾 toohello 使用者之上。

#### <a name="how-hello-broker-gets-invoked"></a>Hello broker 取得叫用的方式
如果在 hello 裝置，例如 hello Microsoft 驗證器應用程式，hello Microsoft 識別 Sdk 會自動安裝相容的 broker hello 當使用者表示他們想在使用中的任何帳戶 toolog 叫用 hello broker，為您的工作hello Microsoft 身分識別平台。 這個帳戶可以是個人的 Microsoft 帳戶、工作或學校帳戶，或您提供的帳戶，以及在 Azure 中使用 B2C 和 B2B 產品的主機。 
 
 #### <a name="how-we-ensure-hello-application-is-valid"></a>我們如何確保 hello 應用程式無效
 
 我們提供協助的 broker 登入中的重要 toohello 安全性 hello 需要 tooensure hello 識別的應用程式呼叫 hello 代理人。 IOS 和 Android 都不會強制執行唯一的識別項僅適用於特定應用程式，讓惡意應用程式可能會 「 詐騙 」 合法應用程式的識別項和接收 hello 語彙基元適用於 hello 合法的應用程式。 tooensure 我們一律會與 hello 右應用程式在執行階段通訊，我們會要求 hello 開發人員 tooprovide 自訂 redirectURI 向 Microsoft 註冊他們的應用程式時。 **以下將詳細討論開發人員應該如何製作此重新導向 URI。** 這個自訂的 redirectURI 包含 hello hello 應用程式的憑證指紋，並確保 toobe 唯一 toohello 應用程式的 hello Google Play 商店。 當應用程式呼叫 hello broker hello broker 詢問 hello Android 作業系統 tooprovide hello 與憑證指紋該呼叫的 hello broker。 hello broker 提供此憑證指紋 tooMicrosoft hello 呼叫 tooour 身分識別系統中。 如果在註冊期間，hello hello 應用程式的憑證指紋不符合 hello 憑證指紋的憑證提供 toous hello 開發人員，我們將會拒絕存取 toohello 語彙基元的 hello 資源 hello 應用程式要求。 此檢查可確保只有 hello 開發人員所註冊的 hello 應用程式接收權杖。

**hello 開發人員有 hello 選擇的如果呼叫 hello broker hello Microsoft Identity SDK，或使用 hello 非 broker 協助的流程。** 不過 hello 開發人員所選擇不 toouse hello broker 輔助流程失去使用 SSO 認證的 hello 優點 hello 使用者可能已經加入 hello 裝置上，並防止他們從 Microsoft 的商務功能搭配使用的應用程式提供例如條件式存取、 Intune 管理功能，以及使用憑證式驗證其客戶。

這些登入具有下列優點 hello:

* 使用者體驗 SSO hello 廠商無論其所有應用程式。
* 您的應用程式可以使用更進階的商業功能，例如條件式存取，或使用 hello InTune 套件的產品。
* 您的應用程式可針對商務使用者支援以憑證為基礎的驗證。
* 更安全登入體驗 hello 的 hello 應用程式和 hello 使用者的身分識別會驗證 hello broker 的應用程式與其他安全性演算法和加密。

這些登入有下列缺點 hello:

* 在 iOS 中已超出您的應用程式體驗轉換 hello 使用者時選擇的認證。
* 遺失 hello 能力 toomanage hello 登入，為您應用程式中的客戶體驗。

以下是如何 hello hello Microsoft 識別 Sdk 使用 broker 應用程式 tooenable SSO 的表示法：

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+

```

此背景資訊為利器您應該要能夠 toobetter 了解和使用 hello Microsoft 識別身分平台和 Sdk 的應用程式中實作 SSO。

## <a name="enabling-cross-app-sso-using-adal"></a>使用 ADAL 啟用跨應用程式的 SSO
我們在此使用 ADAL 的 Android SDK hello 至：

* 開啟應用程式套件的非訊息代理程式協助 SSO
* 開啟訊息代理程式協助 SSO 的支援

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a>開啟非訊息代理程式協助 SSO 的 SSO
非 broker 跨應用程式的協助 sso hello Microsoft 識別 Sdk 許多 SSO hello 複雜度為您管理。 這包括尋找 hello 快取中的 hello 正確的使用者和維護您 tooquery 已登入的使用者清單。

跨應用程式，您擁有需要遵循 toodo hello tooenable SSO:

1. 請確定所有您的應用程式使用者 hello 相同的用戶端 ID 或應用程式 id。
2. 請確定您的應用程式有相同 SharedUserID 設定的 hello。
3. 確保所有相同的簽章憑證，從 Google Play hello 儲存，以便您可以使用共用儲存體您的應用程式共用 hello。

#### <a name="step-1-using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a>步驟 1： 使用 hello 相同的用戶端識別碼 / 應用程式 ID 的所有 hello 您的應用程式套件中的應用程式
為了讓 hello Microsoft 身分識別平台 tooknow 跨應用程式允許 tooshare 語彙基元，每個應用程式需要 tooshare hello 相同的用戶端 ID 或應用程式 id。 這是 hello tooyou hello 入口網站中註冊您的第一個應用程式時提供的唯一識別碼。

您可能想知道識別不同的應用程式的方式 toohello Microsoft 的身分識別服務，如果它使用 hello 相同應用程式識別碼。 hello 回應是以 hello**重新導向 Uri**。 每個應用程式可以有多個重新導向 Uri hello 登入入口網站中註冊。 組件中的每個應用程式將會有不同的重新導向 URI。 其外觀的範例如下：

App1 重新導向 URI： `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`

App2 重新導向 URI： `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`

App3 重新導向 URI： `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`

....

這些之下巢狀 hello 相同的用戶端識別碼 / 應用程式識別碼和查閱根據的 hello 重新導向的 URI 傳回 toous SDK 組態中。

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


*請注意，hello 這些重新導向 Uri 的格式說明如下。除非您希望 toosupport hello broker，您便可以使用任何重新導向 URI，在此情況下它們必須看起來像上述 hello*

#### <a name="step-2-configuring-shared-storage-in-android"></a>步驟 2︰在 Android 中設定共用儲存體
設定 hello`SharedUserID`已超出本文件 hello 範圍，但是可以透過讀取 hello hello Google Android 文件取得[資訊清單](http://developer.android.com/guide/topics/manifest/manifest-element.html)。 您必須決定 sharedUserID 的名稱，並且跨所有的應用程式使用該名稱。

一旦您擁有 hello`SharedUserID`在所有的應用程式中，您是準備 toouse SSO。

> [!WARNING]
> 當您跨應用程式共用儲存體的任何應用程式可以刪除使用者或更糟的是整個應用程式中刪除所有 hello 語彙基元。 這是特別而言，如果您擁有 hello 語彙基元 toodo 背景工作所依賴的應用程式。 共用儲存體表示，您必須非常小心移除所有作業，透過 hello Microsoft 識別 Sdk 中。
> 
> 

就這麼簡單！ hello Microsoft Identity SDK 現在會跨所有應用程式共用認證。 hello 使用者清單也會在應用程式執行個體之間共用。

### <a name="turning-on-sso-for-broker-assisted-sso"></a>開啟訊息代理程式協助 SSO 的 SSO
hello hello 裝置上安裝任何 broker 應用程式 toouse 能力**預設關閉**。 若要 toouse 您的應用程式使用 hello broker，您必須執行一些額外的設定並新增一些程式碼 tooyour 應用程式。

hello 步驟 toofollow 如下：

1. 啟用您的應用程式程式碼呼叫 toohello MS SDK 中的 broker 模式
2. 建立新的重新導向 URI，並提供該 tooboth hello 應用程式和應用程式註冊
3. 設定 hello hello Android 資訊清單中的正確權限

#### <a name="step-1-enable-broker-mode-in-your-application"></a>步驟 1︰在應用程式中啟用訊息代理程式模式
您的應用程式 toouse hello broker hello 能力時，會開啟您建立 hello 「 設定 」 或驗證執行個體的初始設定。 您可以設定程式碼中的 ApplicationSettings 類型就可以辦到︰

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a>步驟 2︰利用 URL 配置建立新的重新導向 URI
中，我們一律會傳回 hello 認證權杖 toohello 正確的應用程式的順序 tooensure，我們需要確定我們回撥 tooyour hello Android 作業系統的方式的應用程式可以驗證 toomake。 Android 作業系統 hello 使用 hello Google Play 商店中的 hello hello 憑證雜湊。 這樣就不會讓惡意應用程式假冒。 因此，我們會利用這以及 hello 我們 broker 應用程式 tooensure hello 權杖會傳回 toohello 正確的應用程式的 URI。 我們需要您 tooestablish 此唯一的重新導向 URI，在您的應用程式和設定為重新導向 URI 的我們的開發人員入口網站。

Hello 的適當的格式必須為您重新導向 URI:

`msauth://packagename/Base64UrlencodedSignature`

例如：msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D

此重新導向 URI 必須指定在您的應用程式註冊使用 hello toobe [Azure 入口網站](https://portal.azure.com/)。 如需 Azure AD 應用程式註冊的詳細資訊，請參閱 [與 Azure Active Directory 整合](active-directory-how-to-integrate.md)。

#### <a name="step-3-set-up-hello-correct-permissions-in-your-application"></a>步驟 3： 設定您的應用程式中的 hello 正確權限
我們 broker 的應用程式在 Android 中跨應用程式使用 hello 的 hello Android OS toomanage 認證的帳戶管理員功能。 在 Android 中的順序 toouse hello broker 您應用程式資訊清單必須有權限 toouse AccountManager 帳戶。 這在 hello 中詳細討論[Google 文件的帳戶管理員](http://developer.android.com/reference/android/accounts/AccountManager.html)

特別是以下這些權限︰

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a>您已設定 SSO！
現在 hello Microsoft Identity SDK 會自動同時在您的應用程式之間共用的認證並叫用 hello broker 是否出現在其裝置上。

