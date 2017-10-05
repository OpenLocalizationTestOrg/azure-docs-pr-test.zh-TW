---
title: "使用入口網站向 Azure AD v2.0 端點註冊應用程式 | Microsoft Docs"
description: "如何向 Microsoft 註冊 app，以使用 v2.0 端點啟用登入及存取 Microsoft 服務"
services: active-directory
documentationcenter: 
author: lnalepa
manager: mbaldwin
editor: 
ms.assetid: bb2f701f-3bc3-4759-94a5-8b9d53a8a0b6
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/01/2017
ms.author: lenalepa
ms.custom: aaddev
ms.openlocfilehash: e6202aa8665c906382666fe08a561421e50e0a8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-register-an-app-with-the-v20-endpoint"></a><span data-ttu-id="02a72-103">如何使用 v2.0 端點註冊 App</span><span class="sxs-lookup"><span data-stu-id="02a72-103">How to register an app with the v2.0 endpoint</span></span>
<span data-ttu-id="02a72-104">若要建置同時接受 MSA 與 Azure AD 登入的應用程式，您必須先向 Microsoft 註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="02a72-104">To build an app that accepts both MSA & Azure AD sign-in, you'll first need to register an app with Microsoft.</span></span>  <span data-ttu-id="02a72-105">您目前無法使用任何現有的 app 搭配 Azure AD 或 MSA - 您需要建立一個全新的 app。</span><span class="sxs-lookup"><span data-stu-id="02a72-105">At this time, you won't be able to use any existing apps you may have with Azure AD or MSA - you'll need to create a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="02a72-106">v2.0 端點並非支援每個 Azure Active Directory 案例和功能。</span><span class="sxs-lookup"><span data-stu-id="02a72-106">Not all Azure Active Directory scenarios & features are supported by the v2.0 endpoint.</span></span>  <span data-ttu-id="02a72-107">若要判斷是否應該使用 v2.0 端點，請閱讀相關的 [v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="02a72-107">To determine if you should use the v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-the-microsoft-app-registration-portal"></a><span data-ttu-id="02a72-108">造訪 Microsoft App 註冊入口網站</span><span class="sxs-lookup"><span data-stu-id="02a72-108">Visit the Microsoft app registration portal</span></span>
<span data-ttu-id="02a72-109">第一件事就是先瀏覽至 [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)。</span><span class="sxs-lookup"><span data-stu-id="02a72-109">First things first - navigate to [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="02a72-110">這是新的 app 註冊入口網站，可供您管理有關 Microsoft app 的所有一切。</span><span class="sxs-lookup"><span data-stu-id="02a72-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="02a72-111">使用個人或公司或學校的 Microsoft 帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="02a72-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="02a72-112">如果您沒有任何帳戶，請註冊新的個人帳戶。</span><span class="sxs-lookup"><span data-stu-id="02a72-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="02a72-113">請繼續進行，這不需要很長的時間 - 我們會在此等候。</span><span class="sxs-lookup"><span data-stu-id="02a72-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="02a72-114">完成了嗎？</span><span class="sxs-lookup"><span data-stu-id="02a72-114">Done?</span></span> <span data-ttu-id="02a72-115">您現在應該看一下您的 Microsoft 應用程式清單，該清單有可能空白。</span><span class="sxs-lookup"><span data-stu-id="02a72-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="02a72-116">讓我們改變這點。</span><span class="sxs-lookup"><span data-stu-id="02a72-116">Let's change that.</span></span>

<span data-ttu-id="02a72-117">按一下 [新增應用程式]，並為它命名。</span><span class="sxs-lookup"><span data-stu-id="02a72-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="02a72-118">入口網站將會指派全域唯一的應用程式識別碼給您的應用程式，以便稍後在您的程式碼中使用。</span><span class="sxs-lookup"><span data-stu-id="02a72-118">The portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="02a72-119">如果您的應用程式包含的伺服器端元件需要用來呼叫 API (例如：Office、Azure 或您自己的 Web API) 的存取權杖，您也會想在此處建立**應用程式密碼**。</span><span class="sxs-lookup"><span data-stu-id="02a72-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want to create an **Application Secret** here as well.</span></span>

<span data-ttu-id="02a72-120">接下來，加入您的 app 將使用的平台。</span><span class="sxs-lookup"><span data-stu-id="02a72-120">Next, add the Platforms that your app will use.</span></span>

* <span data-ttu-id="02a72-121">針對 web 架構的 app，提供可傳送登入訊息的 **重新導向 URI** 。</span><span class="sxs-lookup"><span data-stu-id="02a72-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="02a72-122">針對行動應用程式，複製系統自動為您建立的預設重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="02a72-122">For mobile apps, copy down the default redirect uri automatically created for you.</span></span>

<span data-ttu-id="02a72-123">(選擇性) 您可以在 [設定檔] 區段中自訂登入頁面的外觀及操作方式。</span><span class="sxs-lookup"><span data-stu-id="02a72-123">Optionally, you can customize the look and feel of your sign-in page in the Profile section.</span></span>  <span data-ttu-id="02a72-124">繼續之前，請務必按一下 [儲存]  。</span><span class="sxs-lookup"><span data-stu-id="02a72-124">Make sure to click **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="02a72-125">當您使用 [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList) 建立應用程式時，系統將會在您用來登入入口網站的帳戶的家用租用戶中註冊該應用程式。</span><span class="sxs-lookup"><span data-stu-id="02a72-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), the application will be registered in the home tenant of the account that you use to sign into the portal.</span></span>  <span data-ttu-id="02a72-126">這表示您不能使用個人的 Microsoft 帳戶，在 Azure AD 租用戶中註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="02a72-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="02a72-127">如果您明確地想要在特定的租用戶中註冊應用程式，請使用原本在該租用戶中建立的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="02a72-127">If you explicitly wish to register an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="02a72-128">建置快速啟動應用程式</span><span class="sxs-lookup"><span data-stu-id="02a72-128">Build a quick start app</span></span>
<span data-ttu-id="02a72-129">您現在已有 Microsoft app，您可以完成我們提供的其中一個 v2.0 快速啟動教學課程。</span><span class="sxs-lookup"><span data-stu-id="02a72-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="02a72-130">以下是一些建議：</span><span class="sxs-lookup"><span data-stu-id="02a72-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

