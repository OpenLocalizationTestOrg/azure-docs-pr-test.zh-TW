---
title: "Azure AD v2 Windows Desktop 快速入門 - 設定 | Microsoft Docs"
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
ms.openlocfilehash: 1dfaa7ade664e43dcb9aa788b0197ca17e6ec4cc
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
## <a name="create-an-application-express"></a><span data-ttu-id="e0306-104">建立應用程式 (快速)</span><span class="sxs-lookup"><span data-stu-id="e0306-104">Create an application (Express)</span></span>
<span data-ttu-id="e0306-105">現在您需要在「Microsoft 應用程式註冊入口網站」註冊應用程式：</span><span class="sxs-lookup"><span data-stu-id="e0306-105">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="e0306-106">透過 [Microsoft 應用程式註冊入口網站 (英文)](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure) 註冊您的應用程式</span><span class="sxs-lookup"><span data-stu-id="e0306-106">Register your application via the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app?appType=mobileAndDesktopApp&appTech=windowsDesktop&step=configure)</span></span>
2.  <span data-ttu-id="e0306-107">輸入應用程式的名稱和您的電子郵件</span><span class="sxs-lookup"><span data-stu-id="e0306-107">Enter a name for your application and your email</span></span>
3.  <span data-ttu-id="e0306-108">確定已選取 [Guided Setup (引導式設定)] 選項</span><span class="sxs-lookup"><span data-stu-id="e0306-108">Make sure the option for Guided Setup is checked</span></span>
4.  <span data-ttu-id="e0306-109">依照指示取得應用程式識別碼並貼到您的程式碼中</span><span class="sxs-lookup"><span data-stu-id="e0306-109">Follow the instructions to obtain the application ID and paste it into your code</span></span>

### <a name="add-your-application-registration-information-to-your-solution-advanced"></a><span data-ttu-id="e0306-110">將您的應用程式註冊資訊新增到方案 (進階)</span><span class="sxs-lookup"><span data-stu-id="e0306-110">Add your application registration information to your solution (Advanced)</span></span>
<span data-ttu-id="e0306-111">現在您需要在「Microsoft 應用程式註冊入口網站」註冊應用程式：</span><span class="sxs-lookup"><span data-stu-id="e0306-111">Now you need to register your application in the *Microsoft Application Registration Portal*:</span></span>
1. <span data-ttu-id="e0306-112">前往 [Microsoft 應用程式註冊入口網站 (英文)](https://apps.dev.microsoft.com/portal/register-app) 註冊應用程式</span><span class="sxs-lookup"><span data-stu-id="e0306-112">Go to the [Microsoft Application Registration Portal](https://apps.dev.microsoft.com/portal/register-app) to register an application</span></span>
2. <span data-ttu-id="e0306-113">輸入應用程式的名稱和您的電子郵件</span><span class="sxs-lookup"><span data-stu-id="e0306-113">Enter a name for your application and your email</span></span> 
3. <span data-ttu-id="e0306-114">確定已取消選取 [Guided Setup (引導式設定)] 選項</span><span class="sxs-lookup"><span data-stu-id="e0306-114">Make sure the option for Guided Setup is unchecked</span></span>
4. <span data-ttu-id="e0306-115">按一下 `Add Platform`，然後選取 `Native Application` 並按下 [儲存]</span><span class="sxs-lookup"><span data-stu-id="e0306-115">Click `Add Platform`, then select `Native Application` and hit Save</span></span>
5. <span data-ttu-id="e0306-116">複製應用程式識別碼中的 GUID，接著返回 Visual Studio 並開啟 `App.xaml.cs`，然後用您剛註冊的應用程式識別碼取代 `your_client_id_here`：</span><span class="sxs-lookup"><span data-stu-id="e0306-116">Copy the GUID in Application ID, go back to Visual Studio, open `App.xaml.cs` and replace `your_client_id_here` with the Application ID you just registered:</span></span>

```csharp
private static string ClientId = "your_application_id_here";
```
