---
title: "aaaRegister hello Azure AD v2.0 端點使用 hello 入口網站的應用程式 |Microsoft 文件"
description: "Tooregister 應用程式，但 Microsoft 來啟用登入及存取 Microsoft 服務使用 hello v2.0 端點"
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
ms.openlocfilehash: c56c98906656062435516e820cb318a04c03149c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooregister-an-app-with-hello-v20-endpoint"></a><span data-ttu-id="250aa-103">如何 tooregister 與 hello v2.0 端點的應用程式</span><span class="sxs-lookup"><span data-stu-id="250aa-103">How tooregister an app with hello v2.0 endpoint</span></span>
<span data-ttu-id="250aa-104">toobuild 接受 MSA 與 Azure AD 的應用程式登入時，您必須先 tooregister 與 Microsoft 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="250aa-104">toobuild an app that accepts both MSA & Azure AD sign-in, you'll first need tooregister an app with Microsoft.</span></span>  <span data-ttu-id="250aa-105">此時，您將不會是能 toouse 任何現有的應用程式，您可能必須向 Azure AD 或 MSA-您將需要 toocreate 新品牌。</span><span class="sxs-lookup"><span data-stu-id="250aa-105">At this time, you won't be able toouse any existing apps you may have with Azure AD or MSA - you'll need toocreate a brand new one.</span></span>

> [!NOTE]
> <span data-ttu-id="250aa-106">並非所有的 Azure Active Directory 案例和功能都受到 hello v2.0 端點。</span><span class="sxs-lookup"><span data-stu-id="250aa-106">Not all Azure Active Directory scenarios & features are supported by hello v2.0 endpoint.</span></span>  <span data-ttu-id="250aa-107">toodetermine 如果應該使用 hello v2.0 端點，閱讀有關[v2.0 限制](active-directory-v2-limitations.md)。</span><span class="sxs-lookup"><span data-stu-id="250aa-107">toodetermine if you should use hello v2.0 endpoint, read about [v2.0 limitations](active-directory-v2-limitations.md).</span></span>
> 
> 

## <a name="visit-hello-microsoft-app-registration-portal"></a><span data-ttu-id="250aa-108">請瀏覽 hello Microsoft 應用程式註冊入口網站</span><span class="sxs-lookup"><span data-stu-id="250aa-108">Visit hello Microsoft app registration portal</span></span>
<span data-ttu-id="250aa-109">首要之務先瀏覽過[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)。</span><span class="sxs-lookup"><span data-stu-id="250aa-109">First things first - navigate too[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList).</span></span>  <span data-ttu-id="250aa-110">這是新的 app 註冊入口網站，可供您管理有關 Microsoft app 的所有一切。</span><span class="sxs-lookup"><span data-stu-id="250aa-110">This is a new app registration portal where you can manage your Microsoft apps.</span></span>

<span data-ttu-id="250aa-111">使用個人或公司或學校的 Microsoft 帳戶進行登入。</span><span class="sxs-lookup"><span data-stu-id="250aa-111">Sign in with either a personal or work or school Microsoft account.</span></span>  <span data-ttu-id="250aa-112">如果您沒有任何帳戶，請註冊新的個人帳戶。</span><span class="sxs-lookup"><span data-stu-id="250aa-112">If you don't have either, sign up for a new personal account.</span></span> <span data-ttu-id="250aa-113">請繼續進行，這不需要很長的時間 - 我們會在此等候。</span><span class="sxs-lookup"><span data-stu-id="250aa-113">Go ahead, it won't take long - we'll wait here.</span></span>

<span data-ttu-id="250aa-114">完成了嗎？</span><span class="sxs-lookup"><span data-stu-id="250aa-114">Done?</span></span> <span data-ttu-id="250aa-115">您現在應該看一下您的 Microsoft 應用程式清單，該清單有可能空白。</span><span class="sxs-lookup"><span data-stu-id="250aa-115">You should now be looking at your list of Microsoft apps, which is probably empty.</span></span>  <span data-ttu-id="250aa-116">讓我們改變這點。</span><span class="sxs-lookup"><span data-stu-id="250aa-116">Let's change that.</span></span>

<span data-ttu-id="250aa-117">按一下 [新增應用程式]，並為它命名。</span><span class="sxs-lookup"><span data-stu-id="250aa-117">Click **Add an app**, and give it a name.</span></span>  <span data-ttu-id="250aa-118">hello 入口網站將會指派全域唯一的應用程式識別碼，稍後在程式碼中，您將使用您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="250aa-118">hello portal will assign your app a globally unique  Application Id that you'll use later in your code.</span></span>  <span data-ttu-id="250aa-119">如果您的應用程式包含伺服器端元件，需要存取權杖呼叫應用程式開發介面 (認為： Office、 Azure 或您自己的 web 應用程式開發介面)，您會想 toocreate**應用程式密碼**也這裡。</span><span class="sxs-lookup"><span data-stu-id="250aa-119">If your app includes a server-side component that needs access tokens for calling APIs (think: Office, Azure, or your own web API), you'll want toocreate an **Application Secret** here as well.</span></span>

<span data-ttu-id="250aa-120">接下來，新增 hello 將使用您的應用程式平台。</span><span class="sxs-lookup"><span data-stu-id="250aa-120">Next, add hello Platforms that your app will use.</span></span>

* <span data-ttu-id="250aa-121">針對 web 架構的 app，提供可傳送登入訊息的 **重新導向 URI** 。</span><span class="sxs-lookup"><span data-stu-id="250aa-121">For web based apps, provide a **Redirect URI** where sign-in messages can be sent.</span></span>
* <span data-ttu-id="250aa-122">行動裝置應用程式，向下 hello 預設複製重新導向自動為您建立的 uri。</span><span class="sxs-lookup"><span data-stu-id="250aa-122">For mobile apps, copy down hello default redirect uri automatically created for you.</span></span>

<span data-ttu-id="250aa-123">（選擇性） 您可以自訂您的登入頁面 hello 設定檔 > 一節中的 hello 外觀與風格。</span><span class="sxs-lookup"><span data-stu-id="250aa-123">Optionally, you can customize hello look and feel of your sign-in page in hello Profile section.</span></span>  <span data-ttu-id="250aa-124">請確定 tooclick**儲存**在繼續之前。</span><span class="sxs-lookup"><span data-stu-id="250aa-124">Make sure tooclick **Save** before moving on.</span></span>

> [!NOTE]
> <span data-ttu-id="250aa-125">當您建立應用程式使用[https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList)，hello 應用程式將在 hello hello 帳戶，您會使用 toosign hello 入口網站的主要租用戶中登錄。</span><span class="sxs-lookup"><span data-stu-id="250aa-125">When you create an application using [https://apps.dev.microsoft.com/?deeplink=/appList](https://apps.dev.microsoft.com/?referrer=https://azure.microsoft.com/documentation/articles&deeplink=/appList), hello application will be registered in hello home tenant of hello account that you use toosign into hello portal.</span></span>  <span data-ttu-id="250aa-126">這表示您不能使用個人的 Microsoft 帳戶，在 Azure AD 租用戶中註冊應用程式。</span><span class="sxs-lookup"><span data-stu-id="250aa-126">This means that you can not register an application in your Azure AD tenant using a personal Microsoft account.</span></span>  <span data-ttu-id="250aa-127">如果您明確地想 tooregister 應用程式特定的租用戶中，使用原先建立該租用戶中的帳戶登入。</span><span class="sxs-lookup"><span data-stu-id="250aa-127">If you explicitly wish tooregister an application in a particular tenant, sign in with an account originally created in that tenant.</span></span>
> 
> 

## <a name="build-a-quick-start-app"></a><span data-ttu-id="250aa-128">建置快速啟動應用程式</span><span class="sxs-lookup"><span data-stu-id="250aa-128">Build a quick start app</span></span>
<span data-ttu-id="250aa-129">您現在已有 Microsoft app，您可以完成我們提供的其中一個 v2.0 快速啟動教學課程。</span><span class="sxs-lookup"><span data-stu-id="250aa-129">Now that you have a Microsoft app, you can complete one of our v2.0 quick start tutorials.</span></span>  <span data-ttu-id="250aa-130">以下是一些建議：</span><span class="sxs-lookup"><span data-stu-id="250aa-130">Here are a few recommendations:</span></span>

[!INCLUDE [active-directory-v2-quickstart-table](../../../includes/active-directory-v2-quickstart-table.md)]

