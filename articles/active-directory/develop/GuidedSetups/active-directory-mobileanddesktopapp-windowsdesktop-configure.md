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
## <a name="create-an-application-express"></a><span data-ttu-id="839f1-104">建立應用程式 (快速)</span><span class="sxs-lookup"><span data-stu-id="839f1-104">Create an application (Express)</span></span>
<span data-ttu-id="839f1-105">現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:</span><span class="sxs-lookup"><span data-stu-id="839f1-105">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="839f1-106">註冊您的應用程式，透過 hello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span><span class="sxs-lookup"><span data-stu-id="839f1-106">Register your application via hello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="839f1-107">輸入應用程式的名稱和您的電子郵件</span><span class="sxs-lookup"><span data-stu-id="839f1-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="839f1-108">請確定已選取 hello 引導式安裝選項</span><span class="sxs-lookup"><span data-stu-id="839f1-108">Make sure hello option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="839f1-109">遵循 hello 指示 tooobtain hello 應用程式識別碼，並將它貼到您的程式碼</span><span class="sxs-lookup"><span data-stu-id="839f1-109">Follow hello instructions tooobtain hello application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-tooyour-solution-advanced"></a><span data-ttu-id="839f1-110">新增應用程式註冊資訊 tooyour 方案 （進階）</span><span class="sxs-lookup"><span data-stu-id="839f1-110">Add your application registration information tooyour solution (Advanced)</span></span>
<span data-ttu-id="839f1-111">現在您需要在應用程式中 hello tooregister *Microsoft 應用程式註冊入口網站*:</span><span class="sxs-lookup"><span data-stu-id="839f1-111">Now you need tooregister your application in hello *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="839f1-112">移 toohello [Microsoft 應用程式註冊入口網站](https://apps.dev.microsoft.com/portal/register-app)tooregister 應用程式</span><span class="sxs-lookup"><span data-stu-id="839f1-112">Go toohello [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) tooregister an application</span></span>
2. <span data-ttu-id="839f1-113">輸入應用程式的名稱和您的電子郵件</span><span class="sxs-lookup"><span data-stu-id="839f1-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="839f1-114">請確定未引導式的安裝程式的 hello 選項</span><span class="sxs-lookup"><span data-stu-id="839f1-114">Make sure hello option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="839f1-115">按一下 `Add Platform`，然後選取 `Native Application` 並按下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="839f1-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="839f1-116">複製應用程式識別碼中的 hello GUID，請回到 tooVisual Studio 中，開啟`App.xaml.cs`和取代`your_client_id_here`以 hello 您剛登錄的應用程式識別碼：</span><span class="sxs-lookup"><span data-stu-id="839f1-116">Copy hello GUID in Application ID, go back tooVisual Studio, open `App.xaml.cs` and replace `your_client_id_here` with hello Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
