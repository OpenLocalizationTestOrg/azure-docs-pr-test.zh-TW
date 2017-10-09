---
title: "aaaAzure AD v2 ASP.NET Web 伺服器快速入門-Config |Microsoft 文件"
description: "使用 OpenID Connect 標準，搭配傳統網頁瀏覽器型應用程式，在 ASP.NET 方案上實作 Microsoft 登入"
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
ms.openlocfilehash: e666be4622ad30aaa1e12e49ae56bbe1e129b2a9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>建立應用程式 (快速)
現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:
1. 註冊您的應用程式，透過 hello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app?appType=serverSideWebApp&appTech=aspNetWebAppOwin&step=configure)
2.  輸入應用程式的名稱和您的電子郵件
3.  請確定已選取 hello 引導式安裝選項
4.  請遵循 hello 指示 tooadd 重新導向 URL tooyour 應用程式

## <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>新增應用程式註冊資訊 tooyour 方案 （進階）
現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:
1. 移 toohello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app)tooregister 應用程式
2. 輸入應用程式的名稱和您的電子郵件 
3.  請確定未引導式的安裝程式的 hello 選項
4.  按一下 `Add Platform`，然後選取 `Web`
5.  返回 tooVisual Studio，在 方案總管 中，選取 hello 專案並查看 hello 屬性 視窗 （如果您沒有看到 屬性 視窗中，按 F4）
6.  也變更啟用 SSL`True`
7.  複製 hello SSL URL，並將此 URL toohello 清單的重新導向 Url 的重新導向 Url 的 hello 註冊入口網站的清單中：<br/><br/>![專案屬性](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
8.  新增中的 hello 下列`web.config`hello hello 區段下方的根資料夾中`configuration\appSettings`:

```xml
<add key="ClientId" value="Enter_the_Application_Id_here" />
<add key="redirectUri" value="Enter_the_Redirect_URL_here" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
<!-- Workaround for Docs conversion bug -->
<ol start="9">
<li>
取代`ClientId`以 hello 您剛登錄的應用程式識別碼
</li>
<li>
取代`redirectUri`以 hello 專案的 SSL URL
</li>
</ol>
<!-- End Docs -->
