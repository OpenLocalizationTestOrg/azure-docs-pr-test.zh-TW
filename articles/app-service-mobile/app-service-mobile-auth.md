---
title: "aaaAuthentication 和 Azure 行動應用程式中的授權 |Microsoft 文件"
description: "概念式的參考和概觀 hello 驗證 / 授權功能的 Azure 行動應用程式"
services: app-service\mobile
documentationcenter: 
author: mattchenderson
manager: syntaxc4
editor: 
ms.assetid: a46dbf70-867d-48f6-8885-7f5207ad102e
ms.service: app-service-mobile
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: multiple
ms.topic: article
ms.date: 10/01/2016
ms.author: mahender
ms.openlocfilehash: 5255734481ada11afb65982aebe45c2a349402fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a><span data-ttu-id="dfdd0-103">Azure Mobile Apps 中的驗證與授權</span><span class="sxs-lookup"><span data-stu-id="dfdd0-103">Authentication and Authorization in Azure Mobile Apps</span></span>
## <a name="what-is-app-service-authentication--authorization"></a><span data-ttu-id="dfdd0-104">什麼是 App Service 驗證 / 授權？</span><span class="sxs-lookup"><span data-stu-id="dfdd0-104">What is App Service Authentication / Authorization?</span></span>
> [!NOTE]
> <span data-ttu-id="dfdd0-105">本主題將會移轉的 tooa 合併[應用程式服務驗證 / 授權](../app-service/app-service-authentication-overview.md)主題，其中涵蓋了網頁、 行動裝置版及 API 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-105">This topic will be migrated tooa consolidated [App Service Authentication / Authorization](../app-service/app-service-authentication-overview.md) topic, which covers Web, Mobile, and API Apps.</span></span>
> 
> 

<span data-ttu-id="dfdd0-106">應用程式服務驗證 / 授權是一項功能可讓在使用者的應用程式 toolog hello 應用程式後端上無須任何程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-106">App Service Authentication / Authorization is a feature which allows your application toolog in users with no code changes required on hello app backend.</span></span> <span data-ttu-id="dfdd0-107">提供簡單的方式 tooprotect 應用程式和工作每個使用者資料。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-107">It provides an easy way tooprotect your application and work with per-user data.</span></span>

<span data-ttu-id="dfdd0-108">應用程式服務會在其中使用同盟識別身分，3rd 合作對象**身分識別提供者**""(IDP) 儲存帳戶、 驗證使用者和 hello 應用程式會使用這個身分識別而非其本身。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-108">App Service uses federated identity, in which a 3rd-party **identity provider** ("IDP") stores accounts and authenticates users, and hello application uses this identity instead of its own.</span></span> <span data-ttu-id="dfdd0-109">應用程式服務支援 hello 現成的五個身分識別提供者： *Azure Active Directory*， *Facebook*， *Google*， *Microsoft 帳戶*，和*Twitter*。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-109">App Service supports five identity providers out of hello box: *Azure Active Directory*, *Facebook*, *Google*, *Microsoft Account*, and *Twitter*.</span></span> <span data-ttu-id="dfdd0-110">您也可以藉由整合其他身分識別提供者或您自己自訂的身分識別解決方案，針對您的 app 延伸此支援。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-110">You can also expand this support for your apps by integrating another identity provider or your own custom identity solution.</span></span>

<span data-ttu-id="dfdd0-111">您的 app 可以利用任意數目的這類身分識別提供者，因此可為您的使用者提供登入選項。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-111">Your app can leverage any number of these identity providers, so you can provide your end users with options for how they login.</span></span>

<span data-ttu-id="dfdd0-112">如果您想 tooget 立即開始，請參閱下列教學課程的 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="dfdd0-112">If you wish tooget started right away, please see one of hello following tutorials:</span></span>

* <span data-ttu-id="dfdd0-113">[新增驗證 tooyour iOS 應用程式]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-113">[Add authentication tooyour iOS app]</span></span>
* <span data-ttu-id="dfdd0-114">[新增驗證 tooyour Xamarin.iOS 應用程式]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-114">[Add authentication tooyour Xamarin.iOS app]</span></span>
* <span data-ttu-id="dfdd0-115">[新增驗證 tooyour Xamarin.Android 應用程式]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-115">[Add authentication tooyour Xamarin.Android app]</span></span>
* <span data-ttu-id="dfdd0-116">[新增驗證 tooyour Windows 應用程式]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-116">[Add Authentication tooyour Windows app]</span></span>

## <a name="how-authentication-works"></a><span data-ttu-id="dfdd0-117">驗證的運作方式</span><span class="sxs-lookup"><span data-stu-id="dfdd0-117">How authentication works</span></span>
<span data-ttu-id="dfdd0-118">在使用其中一種 hello 身分識別提供者順序 tooauthenticate，您必須先 tooconfigure hello 身分識別提供者 tooknow 有關您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-118">In order tooauthenticate using one of hello identity providers, you first need tooconfigure hello identity provider tooknow about your application.</span></span> <span data-ttu-id="dfdd0-119">hello 身分識別提供者再將提供您識別碼與回復 toohello 應用程式提供的密碼。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-119">hello identity provider will then provide you with IDs and secrets that you provide back toohello application.</span></span> <span data-ttu-id="dfdd0-120">這樣會完成 hello 信任關係，並讓應用程式服務 toovalidate 身分識別提供 tooit。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-120">This completes hello trust relationship and allows App Service toovalidate identities provided tooit.</span></span>

<span data-ttu-id="dfdd0-121">Hello 下列主題中詳述這些步驟：</span><span class="sxs-lookup"><span data-stu-id="dfdd0-121">These steps are detailed in hello following topics:</span></span>

* <span data-ttu-id="dfdd0-122">[如何 tooconfigure 您的應用程式 toouse Azure Active Directory 登入]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-122">[How tooconfigure your app toouse Azure Active Directory login]</span></span>
* <span data-ttu-id="dfdd0-123">[如何 tooconfigure 應用程式 toouse Facebook 登入]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-123">[How tooconfigure your app toouse Facebook login]</span></span>
* <span data-ttu-id="dfdd0-124">[如何 tooconfigure 應用程式 toouse Google 登入]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-124">[How tooconfigure your app toouse Google login]</span></span>
* <span data-ttu-id="dfdd0-125">[如何 tooconfigure 應用程式 toouse Microsoft 帳戶登入]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-125">[How tooconfigure your app toouse Microsoft Account login]</span></span>
* <span data-ttu-id="dfdd0-126">[如何 tooconfigure 您的應用程式 toouse Twitter 登入]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-126">[How tooconfigure your app toouse Twitter login]</span></span>

<span data-ttu-id="dfdd0-127">一旦所有項目設定 hello 後端上，您可以修改您的用戶端 toolog 中。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-127">Once everything is configured on hello backend, you can modify your client toolog in.</span></span> <span data-ttu-id="dfdd0-128">有以下兩種方法：</span><span class="sxs-lookup"><span data-stu-id="dfdd0-128">There are two approaches here:</span></span>

* <span data-ttu-id="dfdd0-129">使用單行程式碼，讓 hello 行動應用程式登入使用者的用戶端 SDK。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-129">Using a single line of code, let hello Mobile Apps client SDK sign in users.</span></span>
* <span data-ttu-id="dfdd0-130">利用所指定的身分識別提供者 tooestablish 身分發行的 SDK，和便得以存取 tooApp 服務。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-130">Leverage an SDK published by a given identity provider tooestablish identity and then gain access tooApp Service.</span></span>

> [!TIP]
> <span data-ttu-id="dfdd0-131">大部分的應用程式應該使用提供者 SDK tooget 更原生感覺登入體驗和 tooleverage 重新整理支援和其他提供者特有的優點。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-131">Most applications should use a provider SDK tooget a more native-feeling login experience and tooleverage refresh support and other provider-specific benefits.</span></span>
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a><span data-ttu-id="dfdd0-132">不使用提供者 SDK 進行驗證的運作方式</span><span class="sxs-lookup"><span data-stu-id="dfdd0-132">How authentication without a provider SDK works</span></span>
<span data-ttu-id="dfdd0-133">如果您不想 tooset 設定的提供者 SDK，您可以為您允許行動裝置應用程式 tooperform hello 登入。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-133">If you do not wish tooset up a provider SDK, you can allow Mobile Apps tooperform hello login for you.</span></span> <span data-ttu-id="dfdd0-134">hello 行動應用程式用戶端 SDK 將會開啟您選擇且完整的 hello 登入的 web 檢視 toohello 提供者。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-134">hello Mobile Apps client SDK will open a web view toohello provider of your choosing and complete hello sign in.</span></span> <span data-ttu-id="dfdd0-135">有時候在部落格和論壇，您會看到這稱為 tooas hello 「 伺服器流程 」 或 「 伺服器導向流程 」 自 hello server 來管理 hello 登入，且 hello client SDK 永遠不會收到 hello 提供者的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-135">Occasionally on blogs and forums you will see this referred tooas hello "server flow" or "server-directed flow" since hello server is managing hello login, and hello client SDK never receives hello provider token.</span></span>

<span data-ttu-id="dfdd0-136">hello 程式碼需要在每個平台的 hello 驗證教學課程涵蓋此流程 toostart。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-136">hello code needed toostart this flow is covered in hello authentication tutorial for each platform.</span></span> <span data-ttu-id="dfdd0-137">在 hello hello 流程結尾，hello client SDK 有應用程式服務的語彙基元，且 hello 權杖自動附加的 tooall 要求 toohello 後端。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-137">At hello end of hello flow, hello client SDK has an App Service token, and hello token is automatically attached tooall requests toohello backend.</span></span>

### <a name="how-authentication-with-a-provider-sdk-works"></a><span data-ttu-id="dfdd0-138">使用提供者 SDK 進行驗證的運作方式</span><span class="sxs-lookup"><span data-stu-id="dfdd0-138">How authentication with a provider SDK works</span></span>
<span data-ttu-id="dfdd0-139">使用提供者 SDK 可讓 hello 登入經驗 toointeract 更緊密地與 hello 平台執行作業系統 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-139">Working with a provider SDK allows hello log-in experience toointeract more tightly with hello platform OS hello app is running on.</span></span> <span data-ttu-id="dfdd0-140">這也會提供權杖提供者以及某些使用者有關 hello 用戶端，以讓您更容易 tooconsume graph Api 和自訂 hello 使用者經驗。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-140">This also gives you a provider token and some user information on hello client, which makes it much easier tooconsume graph APIs and customize hello user experience.</span></span> <span data-ttu-id="dfdd0-141">偶爾部落格和論壇上您會看到此參照的 tooas hello 「 用戶端流程 」 或 「 用戶端導向流程 」 之後的程式碼 hello 用戶端上處理 hello 登入，而且 hello 用戶端程式碼具有存取 tooa 提供者的語彙基元。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-141">Occasionally on blogs and forums you will see this referred tooas hello "client flow" or "client-directed flow" since code on hello client is handling hello login, and hello client code has access tooa provider token.</span></span>

<span data-ttu-id="dfdd0-142">一旦取得提供者的語彙基元時，它就會需要 toobe 傳送 tooApp 服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-142">Once a provider token is obtained, it needs toobe sent tooApp Service for validation.</span></span> <span data-ttu-id="dfdd0-143">在 hello hello 流程結尾，hello client SDK 有應用程式服務的語彙基元，且 hello 權杖自動附加的 tooall 要求 toohello 後端。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-143">At hello end of hello flow, hello client SDK has an App Service token, and hello token is automatically attached tooall requests toohello backend.</span></span> <span data-ttu-id="dfdd0-144">如果選擇這樣做的話，hello 開發人員也可以讓參考 toohello 提供者語彙基元。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-144">hello developer can also keep a reference toohello provider token if they so choose.</span></span>

## <a name="how-authorization-works"></a><span data-ttu-id="dfdd0-145">授權的運作方式</span><span class="sxs-lookup"><span data-stu-id="dfdd0-145">How authorization works</span></span>
<span data-ttu-id="dfdd0-146">應用程式服務驗證 / 授權會公開數個選項的**當要求未經驗證的動作 tootake**。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-146">App Service Authentication / Authorization exposes several choices for **Action tootake when request is not authenticated**.</span></span> <span data-ttu-id="dfdd0-147">您的程式碼會接收指定的要求之前，您可以有應用程式服務的核取 toosee 如果 hello 要求驗證而且如果沒有，請予以拒絕並嘗試 toohave hello 使用者登入後再重試。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-147">Before your code receives a given request, you can have App Service check toosee if hello request is authenticated and if not, reject it and attempt toohave hello user log in before trying again.</span></span>

<span data-ttu-id="dfdd0-148">其中一個選項是 toohave 未經驗證的要求重新導向 tooone hello 身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-148">One option is toohave unauthenticated requests redirect tooone of hello identity providers.</span></span> <span data-ttu-id="dfdd0-149">在 web 瀏覽器中，這實際上會需要 hello 使用者 tooa 新頁面。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-149">In a web browser, this would actually take hello user tooa new page.</span></span> <span data-ttu-id="dfdd0-150">不過，如此一來，您的行動用戶端就無法重新導向，而且未經驗證的回應將會收到 HTTP「401 未經授權」回應。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-150">However, your mobile client cannot be redirected in this way, and unauthenticated responses will receive an HTTP *401 Unauthorized* response.</span></span> <span data-ttu-id="dfdd0-151">根據這點，可讓您的用戶端 hello 第一個要求應該一律 toohello 登入端點，且則您可以讓其他應用程式開發介面呼叫 tooany。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-151">Given this, hello first request your client makes should always be toohello login endpoint, and then you can make calls tooany other APIs.</span></span> <span data-ttu-id="dfdd0-152">如果您嘗試 toocall 另一個應用程式開發介面登入之前，您的用戶端會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-152">If you attempt toocall another API before logging in, your client will receive an error.</span></span>

<span data-ttu-id="dfdd0-153">如果您想 toohave 更細微控制哪些端點透過要求驗證，您也可以選擇 「 採取任何動作 （允許要求） 」 的未經驗證的要求。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-153">If you wish toohave more granular control over which endpoints require authentication, you can also pick "No action (allow request)" for unauthenticated requests.</span></span> <span data-ttu-id="dfdd0-154">在此情況下，才會延期驗證的所有決策 tooyour 應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-154">In this case, all authentication decisions are deferred tooyour application code.</span></span> <span data-ttu-id="dfdd0-155">這也可讓您根據自訂授權規則 tooallow 存取 toospecific 使用者。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-155">This also allows you tooallow access toospecific users based on custom authorization rules.</span></span>

## <a name="documentation"></a><span data-ttu-id="dfdd0-156">文件</span><span class="sxs-lookup"><span data-stu-id="dfdd0-156">Documentation</span></span>
<span data-ttu-id="dfdd0-157">hello 遵循教學課程顯示如何 tooadd 驗證 tooyour 行動用戶端使用應用程式服務：</span><span class="sxs-lookup"><span data-stu-id="dfdd0-157">hello following tutorials show how tooadd authentication tooyour mobile clients using App Service:</span></span>

* <span data-ttu-id="dfdd0-158">[新增驗證 tooyour iOS 應用程式]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-158">[Add authentication tooyour iOS app]</span></span>
* <span data-ttu-id="dfdd0-159">[新增驗證 tooyour Xamarin.iOS 應用程式]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-159">[Add authentication tooyour Xamarin.iOS app]</span></span>
* <span data-ttu-id="dfdd0-160">[新增驗證 tooyour Xamarin.Android 應用程式]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-160">[Add authentication tooyour Xamarin.Android app]</span></span>
* <span data-ttu-id="dfdd0-161">[新增驗證 tooyour Windows 應用程式]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-161">[Add Authentication tooyour Windows app]</span></span>

<span data-ttu-id="dfdd0-162">hello 遵循教學課程顯示如何 tooconfigure App Service tooleverage 不同的驗證提供者：</span><span class="sxs-lookup"><span data-stu-id="dfdd0-162">hello following tutorials show how tooconfigure App Service tooleverage different authentication providers:</span></span>

* <span data-ttu-id="dfdd0-163">[如何 tooconfigure 您的應用程式 toouse Azure Active Directory 登入]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-163">[How tooconfigure your app toouse Azure Active Directory login]</span></span>
* <span data-ttu-id="dfdd0-164">[如何 tooconfigure 應用程式 toouse Facebook 登入]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-164">[How tooconfigure your app toouse Facebook login]</span></span>
* <span data-ttu-id="dfdd0-165">[如何 tooconfigure 應用程式 toouse Google 登入]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-165">[How tooconfigure your app toouse Google login]</span></span>
* <span data-ttu-id="dfdd0-166">[如何 tooconfigure 應用程式 toouse Microsoft 帳戶登入]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-166">[How tooconfigure your app toouse Microsoft Account login]</span></span>
* <span data-ttu-id="dfdd0-167">[如何 tooconfigure 您的應用程式 toouse Twitter 登入]</span><span class="sxs-lookup"><span data-stu-id="dfdd0-167">[How tooconfigure your app toouse Twitter login]</span></span>

<span data-ttu-id="dfdd0-168">如果您想 toouse 識別系統以外在這裡，您也可以利用 hello 提供 hello 的[預覽 hello.NET server SDK 中的自訂驗證支援](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth)。</span><span class="sxs-lookup"><span data-stu-id="dfdd0-168">If you wish toouse an identity system other than hello ones provided here, you can also leverage hello [preview custom authentication support in hello .NET server SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth).</span></span>

[新增驗證 tooyour iOS 應用程式]: app-service-mobile-ios-get-started-users.md
[新增驗證 tooyour Xamarin.iOS 應用程式]: app-service-mobile-xamarin-ios-get-started-users.md
[新增驗證 tooyour Xamarin.Android 應用程式]: app-service-mobile-xamarin-android-get-started-users.md
[新增驗證 tooyour Windows 應用程式]: app-service-mobile-windows-store-dotnet-get-started-users.md

[如何 tooconfigure 您的應用程式 toouse Azure Active Directory 登入]: app-service-mobile-how-to-configure-active-directory-authentication.md
[如何 tooconfigure 應用程式 toouse Facebook 登入]: app-service-mobile-how-to-configure-facebook-authentication.md
[如何 tooconfigure 應用程式 toouse Google 登入]: app-service-mobile-how-to-configure-google-authentication.md
[如何 tooconfigure 應用程式 toouse Microsoft 帳戶登入]: app-service-mobile-how-to-configure-microsoft-authentication.md
[如何 tooconfigure 您的應用程式 toouse Twitter 登入]: app-service-mobile-how-to-configure-twitter-authentication.md
