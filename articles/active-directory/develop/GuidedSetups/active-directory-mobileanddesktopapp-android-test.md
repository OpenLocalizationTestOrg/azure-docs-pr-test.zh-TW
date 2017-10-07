---
title: "aaaAzure AD v2 Android 快速入門-測試 |Microsoft 文件"
description: "Android 應用程式如何取得存取權杖，以及如何呼叫 Microsoft 圖形 API，或呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
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
ms.openlocfilehash: 499f32b46fd44cca0e52179bced49b311135d8de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="test-your-code"></a>測試您的程式碼

1. 部署您的程式碼 tooyour 的裝置/模擬器。
2. 當您準備好 tootest，請使用 Microsoft Azure Active Directory （組織帳戶） 或 Microsoft 帳戶 （live.com、 outlook.com） 帳戶 toosign 中。 

![範例螢幕擷取畫面](media/active-directory-mobileanddesktopapp-android-test/mainwindow.png)
<br/><br/>
![登入](media/active-directory-mobileanddesktopapp-android-test/usernameandpassword.png)

### <a name="consent"></a>同意
hello 第一次使用者登入 tooyour 應用程式，他們會看到類似 toohello 下列同意畫面，他們需要其中 tooexplicitly 接受： 

![同意](media/active-directory-mobileanddesktopapp-android-test/androidconsent.png)


### <a name="expected-results"></a>預期的結果
您應該會看到 hello 結果的 Graph API 的呼叫 tooMicrosoft 'me' 的端點使用 tootooobtain hello 使用者設定檔-https://graph.microsoft.com/v1.0/me。 如需一般 Microsoft Graph 端點的清單，請參閱這篇[文章 (英文)](https://developer.microsoft.com/graph/docs#common-microsoft-graph-queries)。

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>與範圍和委派的權限有關的詳細資訊

hello Microsoft Graph API 需要 hello`user.read`範圍 tooread hello 使用者的設定檔。 根據預設值，在我們註冊入口網站上註冊的每個應用程式中都會自動新增此範圍。 Microsoft Graph 的某些其他 API 與您後端伺服器的自訂 API 一樣，需要其他範圍。 例如，針對 Microsoft Graph hello 範圍`Calendars.Read`是必要的 toolist hello 使用者的行事曆。 順序 tooaccess hello 使用者的行事曆應用程式的內容中，您需要 tooadd hello`Calendars.Read`委派權限 toohello 應用程式註冊的資訊，然後再加入 hello`Calendars.Read`範圍 toohello`acquireTokenSilentAsync`呼叫。 隨著您增加 hello 範圍數目，可能會提示 hello 使用者輸入其他的同意授權。

<!--end-collapse-->
