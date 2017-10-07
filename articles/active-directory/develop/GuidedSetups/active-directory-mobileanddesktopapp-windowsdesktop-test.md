---
title: "aaaAzure AD v2 Windows 桌面快速入門-測試 |Microsoft 文件"
description: "Windows Desktop .NET (XAML) 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.assetid: 820acdb7-d316-4c3b-8de9-79df48ba3b06
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.custom: aaddev
ms.openlocfilehash: 0ae9612e1585c54a3fe35ba9d18f92554099b2c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>測試您的程式碼

若要 tootest 您的應用程式，請按`F5`toorun Visual Studio 中的專案。 您的主視窗應會出現：

![範例螢幕擷取畫面](media/active-directory-mobileanddesktopapp-windowsdesktop-test/samplescreenshot.png)

當你準備好 tootest 時，請按一下*呼叫 Microsoft Graph API*並使用 Microsoft Azure Active Directory （組織帳戶） 或 Microsoft 帳戶 （live.com、 outlook.com） 帳戶 toosign 中的。 它是 hello 第一次，您會看到一個視窗詢問使用者 toosign 中：

![登入](media/active-directory-mobileanddesktopapp-windowsdesktop-test/signinscreenshot.png)

### <a name="consent"></a>同意
hello 第一次您登入 tooyour 應用程式，您會看到類似 toohello 下列同意畫面，您需要在 tooexplicitly 接受：

![同意畫面](media/active-directory-mobileanddesktopapp-windowsdesktop-test/consentscreen.png)

### <a name="expected-results"></a>預期的結果
您應該會看到 hello API 呼叫的結果 畫面 hello Microsoft Graph API 呼叫所傳回的使用者設定檔資訊。

您也應該會看到透過 hello 權杖的基本資訊`AcquireTokenAsync`或`AcquireTokenSilentAsync`hello 語彙基元資訊 方塊中：

|屬性  |格式  |描述 |
|---------|---------|---------|
|名稱 | {使用者完整名稱} |hello 使用者的名字和姓氏|
|使用者名稱 |<span>user@domain.com</span> |用 tooidentify hello 使用者 hello 使用者名稱。|
|權杖到期 |{DateTime}         |hello 的 hello 權杖到期的時間。 MSAL 會延長為您 hello 到期日 hello 語彙基元時所需的更新|
|存取權杖 |{字串}         |hello 語彙基元字串傳送，會將要求傳送給 tooHTTP 需要授權標頭|

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>與範圍和委派的權限有關的詳細資訊
Graph API 需要 hello`user.read`範圍 tooread 使用者設定檔。 根據預設值，在我們註冊入口網站上註冊的每個應用程式中都會自動新增此範圍。 您後端伺服器的部分其他圖形 API 和自訂 API 也會需要其他範圍。 例如，對於圖形中，`Calendars.Read`是必要的 toolist 使用者的行事曆。 順序 tooaccess hello 使用者的行事曆應用程式的內容中，您需要 tooadd`Calendars.Read`委派應用程式註冊資訊，然後再加入`Calendars.Read`toohello`AcquireTokenAsync`呼叫。 當您增加 hello 範圍數目，可能會提示使用者輸入其他的同意授權。

<!--end-collapse-->



