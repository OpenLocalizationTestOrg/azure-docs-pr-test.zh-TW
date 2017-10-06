---
title: "aaaPublish 原生用戶端應用程式的 Azure AD |Microsoft 文件"
description: "涵蓋如何與 Azure AD 應用程式 Proxy 連接器 tooprovide 安全遠端存取 tooyour tooenable 原生用戶端應用程式 toocommunicate 內部部署應用程式。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: f0cae145-e346-4126-948f-3f699747b96e
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: kgremban
ms.reviewer: harshja
ms.custom: it-pro
ms.openlocfilehash: 0ed2be217bf992f034d8321d5e66569b4cace24f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-native-client-apps-toointeract-with-proxy-applications"></a>如何使用應用程式 proxy tooenable 原生用戶端應用程式 toointeract

加法 tooweb 應用程式中，Azure Active Directory 應用程式 Proxy 也可以使用的 toopublish 原生用戶端應用程式。 原生用戶端應用程式與 Web 應用程式不同，因為這種應用程式會安裝在裝置上，而 Web 應用程式則是透過瀏覽器存取。 

應用程式 Proxy 藉由接受在標準授權 HTTP 標頭中傳送的 Azure AD 發行權杖，來支援原生用戶端應用程式。

![使用者、Azure Active Directory 和已發佈應用程式之間的關係](./media/active-directory-application-proxy-native-client/richclientflow.png)

使用 hello Azure AD 驗證程式庫，它會負責驗證並支援許多用戶端環境、 toopublish 原生應用程式。 應用程式 Proxy 納入 hello [tooWeb API 的原生應用程式案例](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)。 這篇文章會引導您 hello 四個步驟 toopublish hello Azure AD 驗證程式庫與應用程式 Proxy 的原生應用程式。 

## <a name="step-1-publish-your-application"></a>步驟 1：發佈您的應用程式
發行應用程式 proxy，如同任何其他應用程式，並指派使用者 tooaccess 您的應用程式。 如需詳細資訊，請參閱[使用應用程式 Proxy 發佈應用程式](active-directory-application-proxy-publish.md)。

## <a name="step-2-configure-your-application"></a>步驟 2：設定您的應用程式
以下列方式設定原生應用程式：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。
2. 瀏覽過**Azure Active Directory** > **應用程式註冊**。
3. 選取 [新增應用程式註冊]。
4. 指定應用程式的名稱，選取**原生**hello 應用程式類型，並提供您的應用程式中的 hello 重新導向 URI。 

   ![建立新的應用程式註冊](./media/active-directory-application-proxy-native-client/create.png)
5. 選取 [ **建立**]。

如需建立新應用程式註冊的詳細資訊，請參閱[整合應用程式與 Azure Active Directory](.//develop/active-directory-integrating-applications.md)。


## <a name="step-3-grant-access-tooother-applications"></a>步驟 3： 授與存取 tooother 應用程式
啟用 hello 原生應用程式公開的 toobe tooother 應用程式目錄中：

1. 仍在**應用程式註冊**，選取 hello 您剛才建立的新原生應用程式。
2. 選取 [必要權限]。
3. 選取 [新增] 。
4. 開啟 hello 第一個步驟中，**選取應用程式開發介面**。
5. 使用 hello 搜尋列 toofind hello 應用程式 Proxy 應用程式發佈 hello 第一個區段中。 選擇該應用程式，然後按一下 [選取]。 

   ![搜尋 hello proxy 應用程式](./media/active-directory-application-proxy-native-client/select_api.png)
6. 開啟 hello 第二個步驟中，**選取權限**。
7. 使用 hello 核取方塊 toogrant 原生應用程式存取 tooyour proxy 應用程式，然後按一下**選取**。

   ![授與存取 tooproxy 應用程式](./media/active-directory-application-proxy-native-client/select_perms.png)
8. 選取 [完成] 。


## <a name="step-4-edit-hello-active-directory-authentication-library"></a>步驟 4： 編輯 hello Active Directory Authentication Library
編輯下列文字的 hello Active Directory 驗證程式庫 (ADAL) tooinclude hello hello 驗證內容中的 hello 原生應用程式程式碼：

```
// Acquire Access Token from AAD for Proxy Application
AuthenticationContext authContext = new AuthenticationContext("https://login.microsoftonline.com/<Tenant ID>");
AuthenticationResult result = authContext.AcquireToken("< External Url of Proxy App >",
        "<App ID of hello Native app>",
        new Uri("<Redirect Uri of hello Native App>"),
        PromptBehavior.Never);

//Use hello Access Token tooaccess hello Proxy Application
HttpClient httpClient = new HttpClient();
httpClient.DefaultRequestHeaders.Authorization = new AuthenticationHeaderValue("Bearer", result.AccessToken);
HttpResponseMessage response = await httpClient.GetAsync("< Proxy App API Url >");
```

hello 變數 hello 範例程式碼中的應該被取代，如下所示：

* **租用戶識別碼**可以在 hello Azure 入口網站中找到。 瀏覽過**Azure Active Directory** > **屬性**和複製 hello 目錄識別碼。 
* **外部 URL**是 hello 前端在 hello Proxy 應用程式中所輸入的 URL。 這個值 toofind，瀏覽 toohello**應用程式 proxy** hello proxy 應用程式的區段。
* **應用程式識別碼**hello 的原生應用程式可以找到上 hello**屬性**hello 原生應用程式頁面。
* **重新導向的 hello 原生應用程式 URI**可以找到上 hello**重新導向 Uri** hello 原生應用程式頁面。


## <a name="see-also"></a>另請參閱

如需 hello 原生應用程式流程的詳細資訊，請參閱[原生應用程式 tooweb 應用程式開發介面](develop/active-directory-authentication-scenarios.md#native-application-to-web-api)

如 hello 最新消息和更新，請參閱 hello[應用程式 Proxy 部落格](http://blogs.technet.com/b/applicationproxyblog/)
