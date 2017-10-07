---
title: "aaaAzure AD v2 iOS 入門-測試 |Microsoft 文件"
description: "iOS (Swift) 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
services: active-directory
documentationcenter: dev-center-name
author: andretms
manager: mbaldwin
editor: 
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 05/09/2017
ms.author: andret
ms.openlocfilehash: 98c73eddabf9664feb19ac6878e9d7315b9aa79b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="test-querying-hello-microsoft-graph-api-from-your-ios-application"></a>測試查詢 hello Microsoft Graph API 從 iOS 應用程式

按`Command`  +  `R` toorun hello 模擬器中的 hello 程式碼。

![範例螢幕擷取畫面](media/active-directory-mobileanddesktopapp-ios-test/iostestscreenshot.png)

當您準備好 tootest 時，點選*' 呼叫 Microsoft Graph API'*而且您將會提示的 tootype，您的使用者名稱和密碼。

### <a name="consent"></a>同意
hello 第一次您登入 tooyour 應用程式，您會看到類似 toohello 下列同意畫面，您需要在 tooexplicitly 接受：

![同意畫面](media/active-directory-mobileanddesktopapp-ios-test/iosconsentscreen.png)

### <a name="expected-results"></a>預期的結果
您應該會看到在 hello hello Microsoft Graph API 呼叫所傳回的使用者設定檔資訊*記錄*> 一節。

<!--start-collapse-->
### <a name="more-information-about-scopes-and-delegated-permissions"></a>與範圍和委派的權限有關的詳細資訊

hello Microsoft Graph API 需要 hello`user.read`範圍 tooread hello 使用者的設定檔。 根據預設值，在我們註冊入口網站上註冊的每個應用程式中都會自動新增此範圍。 Microsoft Graph 的某些其他 API 與您後端伺服器的自訂 API 一樣，需要其他範圍。 例如，針對 Microsoft Graph hello 範圍`Calendars.Read`是必要的 toolist hello 使用者的行事曆。 順序 tooaccess hello 使用者的行事曆應用程式的內容中，您需要 tooadd hello`Calendars.Read`委派權限 toohello 應用程式註冊的資訊，然後再加入 hello`Calendars.Read`範圍 toohello`acquireTokenSilent`呼叫。 隨著您增加 hello 範圍數目，可能會提示 hello 使用者輸入其他的同意授權。

<!--end-collapse-->



