---
title: "aaaAzure AD v2 Windows 桌面快速入門-Config |Microsoft 文件"
description: "Windows Desktop .NET (XAML) 應用程式可取得存取權杖，以及呼叫受 Azure Active Directory v2 端點保護之 API 的方法。 | Microsoft Azure | Microsoft Azure"
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
ms.openlocfilehash: 39c257e3e0cb09491f6fe005877601bd46824d12
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
## <a name="create-an-application-express"></a>建立應用程式 (快速)
現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:
1. 註冊您的應用程式，透過 hello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)
2.  輸入應用程式的名稱和您的電子郵件
3.  請確定已選取 hello 引導式安裝選項
4.  遵循 hello 指示 tooobtain hello 應用程式識別碼，並將它貼到您的程式碼

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a>新增應用程式註冊資訊 tooyour 方案 （進階）
現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:
1. 移 toohello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app)tooregister 應用程式
2. 輸入應用程式的名稱和您的電子郵件 
3. 請確定未引導式的安裝程式的 hello 選項
4. 按一下 `Add Platform`，然後選取 `Native Application` 並按下 [儲存]
5. 複製應用程式識別碼中的 hello GUID，請回到 tooVisual Studio 中，開啟`App.xaml.cs`和取代`your_client_id_here`以 hello 您剛登錄的應用程式識別碼：

```csharp
private static string ClientId = "your_application_id_here";
```
