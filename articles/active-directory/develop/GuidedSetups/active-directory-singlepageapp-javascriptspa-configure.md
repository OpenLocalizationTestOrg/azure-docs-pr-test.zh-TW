---
title: "aaaAzure AD v2 JS SPA 引導式安裝-設定 |Microsoft 文件"
description: "JavaScript SPA 應用程式如何呼叫需要來自 Azure Active Directory v2 端點之存取權杖的 API"
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
ms.date: 06/01/2017
ms.author: andret
ms.openlocfilehash: 1b93298d4bd4e17dd261dbb75502a122c30aac97
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="register-your-application"></a>註冊您的應用程式

有多個方式 toocreate 應用程式，請選取其中一個：

### <a name="option-1-register-your-application-express-mode"></a>選項 1：註冊您的應用程式 (快速模式)
現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:

1.  註冊您的應用程式，透過 hello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app?appType=singlePageApp&appTech=javascriptSpa&step=configure)
2.  輸入應用程式的名稱和您的電子郵件
3.  請確定 hello 選項*引導式安裝*會檢查
4.  遵循 hello 指示 tooobtain hello 應用程式識別碼，並將它貼到您的程式碼

### <a name="option-2-register-your-application-advanced-mode"></a>選項 2：註冊您的應用程式 (進階模式)

1. 移 toohello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app)tooregister 應用程式
2. 輸入應用程式的名稱和您的電子郵件 
3. 請確定 hello 選項*引導式安裝*未選取
4.  按一下 `Add Platform`，然後選取 `Web`
5. 新增 hello`Redirect URL`對應 toohello 應用程式的 URL，根據您的 web 伺服器。 請參閱 hello 下列各節以指示 tooset / 取得 Visual Studio 和 Python 中的 hello 重新導向 URL。
6. 按一下 [儲存] 

> #### <a name="visual-studio-instructions-for-obtaining-redirect-url"></a>取得重新導向 URL 的 Visual Studio 指示
> 請依照下列 hello 指示 tooobtain 重新導向 URL:
> 1.    在*方案總管 中*選取 hello 專案，看看 hello`Properties`視窗 (如果您沒有看到 屬性 視窗，請按`F4`)
> 2.    複製 hello 值從`URL`toohello 剪貼簿：<br/> ![專案屬性](media/active-directory-singlepageapp-javascriptspa-configure/vs-project-properties-screenshot.png)<br />
> 3.    切換後 toohello*應用程式註冊入口網站*貼上為 hello 值`Redirect URL`，按一下 [儲存]

<p/>

> #### <a name="setting-redirect-url-for-python"></a>設定 Python 的重新導向 URL
> 對於 Python，您可以設定 hello web 伺服器連接埠，透過命令列。 此 「 引導式的安裝程式會使用 hello 連接埠 8080 的參考，但覺得可用 toouse 任何其他可用的通訊埠。 在任何情況下，請遵循以下 tooset hello 應用程式註冊資訊的重新導向 URL 設定的 hello 指示：<br/>
> - 切換後 toohello*應用程式註冊入口網站*並設定`http://localhost:8080/`為`Redirect URL`，或使用`http://localhost:[port]/`如果您使用自訂的 TCP 連接埠 (其中*[port]*為 hello 自訂 TCP 通訊埠數字），按一下 [儲存]


#### <a name="configure-your-javascript-spa"></a>設定您的 JavaScript SPA

1.  建立名為`msalconfig.js`包含 hello 應用程式註冊資訊。 如果您使用 Visual Studio 中，選取 hello 專案 （專案根資料夾） 上按一下滑鼠右鍵，然後選取： `Add`  >  `New Item`  >  `JavaScript File`。 將它命名為 `msalconfig.js`
2.  新增下列程式碼 tooyour hello`msalconfig.js`檔案：

```javascript
var msalconfig = {
    clientID: "Enter_the_Application_Id_here",
    redirectUri: location.origin
};
```
<ol start="3">
<li>
取代<code>Enter_the_Application_Id_here</code>以 hello 您剛登錄的應用程式識別碼
</li>
</ol>
