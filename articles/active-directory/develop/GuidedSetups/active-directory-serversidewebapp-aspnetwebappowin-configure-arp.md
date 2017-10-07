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
ms.openlocfilehash: badc47e131290a56a507592f944a0fc7093260a6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="configure-your-aspnet-web-app-with-hello-applications-registration-information"></a>Hello 應用程式的登錄資訊以設定您的 ASP.NET Web 應用程式

在此步驟中，您會設定您的專案 toouse SSL，，，然後使用您的應用程式註冊資訊 hello SSL URL tooconfigure。 在此之後，新增 hello 應用程式 ' 註冊資訊 tooyour 解決方案透過*web.config*。

1.  在方案總管 中，選取 hello 專案並查看 hello`Properties`視窗 （如果您沒有看到 屬性 視窗中，按 F4）
2.  變更`SSL Enabled`太`True`
3.  複製 hello 值從`SSL URL`上方並將它貼在 hello`Redirect URL`欄位 hello 最上層顯示此頁面，然後按一下 *更新*:<br/><br/>![專案屬性](media/active-directory-serversidewebapp-aspnetwebappowin-configure/vsprojectproperties.png)<br />
4.  新增中的 hello 下列`web.config`檔案位於根資料夾下一節, `configuration\appSettings`:

```xml
<add key="ClientId" value="[Enter hello application Id here]" />
<add key="RedirectUri" value="[Enter hello Redirect URL here]" />
<add key="Tenant" value="common" />
<add key="Authority" value="https://login.microsoftonline.com/{0}/v2.0" /> 
```
