---
title: "Azure Mobile Apps 中的驗證與授權 | Microsoft Docs"
description: "Azure Mobile Apps 驗證 / 授權功能的概念性參考與概觀"
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
ms.openlocfilehash: 92c9f91807a6b5d4fea6b504256508f805627a16
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="authentication-and-authorization-in-azure-mobile-apps"></a><span data-ttu-id="d2183-103">Azure Mobile Apps 中的驗證與授權</span><span class="sxs-lookup"><span data-stu-id="d2183-103">Authentication and Authorization in Azure Mobile Apps</span></span>
## <a name="what-is-app-service-authentication--authorization"></a><span data-ttu-id="d2183-104">什麼是 App Service 驗證 / 授權？</span><span class="sxs-lookup"><span data-stu-id="d2183-104">What is App Service Authentication / Authorization?</span></span>
> [!NOTE]
> <span data-ttu-id="d2183-105">本主題將移轉至合併的 [App Service 驗證/授權](../app-service/app-service-authentication-overview.md) 主題，其中涵蓋 Web、Mobile 和 API Apps。</span><span class="sxs-lookup"><span data-stu-id="d2183-105">This topic will be migrated to a consolidated [App Service Authentication / Authorization](../app-service/app-service-authentication-overview.md) topic, which covers Web, Mobile, and API Apps.</span></span>
> 
> 

<span data-ttu-id="d2183-106">App Service 驗證 / 授權是一項功能，可讓您的應用程式登入使用者，而不需在 app 後端進行任何程式碼變更。</span><span class="sxs-lookup"><span data-stu-id="d2183-106">App Service Authentication / Authorization is a feature which allows your application to log in users with no code changes required on the app backend.</span></span> <span data-ttu-id="d2183-107">它提供簡單的方法來保護您的應用程式，以及使用每位使用者的資料。</span><span class="sxs-lookup"><span data-stu-id="d2183-107">It provides an easy way to protect your application and work with per-user data.</span></span>

<span data-ttu-id="d2183-108">App Service 會使用同盟身分識別，第 3 方 **身分識別提供者** ("IDP") 會在其中儲存帳戶和驗證使用者，而應用程式會使用這個身分識別，而不是它自己的身分識別。</span><span class="sxs-lookup"><span data-stu-id="d2183-108">App Service uses federated identity, in which a 3rd-party **identity provider** ("IDP") stores accounts and authenticates users, and the application uses this identity instead of its own.</span></span> <span data-ttu-id="d2183-109">App Service 支援五個現成的識別提供者：Azure Active Directory、Facebook、Google、Microsoft 帳戶及 Twitter。</span><span class="sxs-lookup"><span data-stu-id="d2183-109">App Service supports five identity providers out of the box: *Azure Active Directory*, *Facebook*, *Google*, *Microsoft Account*, and *Twitter*.</span></span> <span data-ttu-id="d2183-110">您也可以藉由整合其他身分識別提供者或您自己自訂的身分識別解決方案，針對您的 app 延伸此支援。</span><span class="sxs-lookup"><span data-stu-id="d2183-110">You can also expand this support for your apps by integrating another identity provider or your own custom identity solution.</span></span>

<span data-ttu-id="d2183-111">您的 app 可以利用任意數目的這類身分識別提供者，因此可為您的使用者提供登入選項。</span><span class="sxs-lookup"><span data-stu-id="d2183-111">Your app can leverage any number of these identity providers, so you can provide your end users with options for how they login.</span></span>

<span data-ttu-id="d2183-112">如果您希望立即開始，請參閱下列其中一個教學課程：</span><span class="sxs-lookup"><span data-stu-id="d2183-112">If you wish to get started right away, please see one of the following tutorials:</span></span>

* <span data-ttu-id="d2183-113">[將驗證新增至您的 iOS 應用程式]</span><span class="sxs-lookup"><span data-stu-id="d2183-113">[Add authentication to your iOS app]</span></span>
* <span data-ttu-id="d2183-114">[將驗證新增至 Xamarin.iOS 應用程式]</span><span class="sxs-lookup"><span data-stu-id="d2183-114">[Add authentication to your Xamarin.iOS app]</span></span>
* <span data-ttu-id="d2183-115">[將驗證新增至 Xamarin.Android 應用程式]</span><span class="sxs-lookup"><span data-stu-id="d2183-115">[Add authentication to your Xamarin.Android app]</span></span>
* <span data-ttu-id="d2183-116">[將驗證新增至您的 Windows App]</span><span class="sxs-lookup"><span data-stu-id="d2183-116">[Add Authentication to your Windows app]</span></span>

## <a name="how-authentication-works"></a><span data-ttu-id="d2183-117">驗證的運作方式</span><span class="sxs-lookup"><span data-stu-id="d2183-117">How authentication works</span></span>
<span data-ttu-id="d2183-118">若要使用其中一個身分識別提供者進行驗證，您首先需要設定身分識別提供者來了解您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2183-118">In order to authenticate using one of the identity providers, you first need to configure the identity provider to know about your application.</span></span> <span data-ttu-id="d2183-119">身分識別提供者接著將為您提供識別碼和密碼，您需要將這兩者再次提供給應用程式。</span><span class="sxs-lookup"><span data-stu-id="d2183-119">The identity provider will then provide you with IDs and secrets that you provide back to the application.</span></span> <span data-ttu-id="d2183-120">這會完成的信任關係，並讓 App Service 能夠驗證其所提供的身分識別。</span><span class="sxs-lookup"><span data-stu-id="d2183-120">This completes the trust relationship and allows App Service to validate identities provided to it.</span></span>

<span data-ttu-id="d2183-121">這些步驟將於下列主題中詳細說明：</span><span class="sxs-lookup"><span data-stu-id="d2183-121">These steps are detailed in the following topics:</span></span>

* <span data-ttu-id="d2183-122">[如何設定您的 App 以使用 Azure Active Directory 登入]</span><span class="sxs-lookup"><span data-stu-id="d2183-122">[How to configure your app to use Azure Active Directory login]</span></span>
* <span data-ttu-id="d2183-123">[如何設定 App 以使用 Facebook 登入]</span><span class="sxs-lookup"><span data-stu-id="d2183-123">[How to configure your app to use Facebook login]</span></span>
* <span data-ttu-id="d2183-124">[如何設定 App 以使用 Google 登入]</span><span class="sxs-lookup"><span data-stu-id="d2183-124">[How to configure your app to use Google login]</span></span>
* <span data-ttu-id="d2183-125">[如何設定 App 以使用 Microsoft 帳戶登入]</span><span class="sxs-lookup"><span data-stu-id="d2183-125">[How to configure your app to use Microsoft Account login]</span></span>
* <span data-ttu-id="d2183-126">[如何設定 App 以使用 Twitter 登入]</span><span class="sxs-lookup"><span data-stu-id="d2183-126">[How to configure your app to use Twitter login]</span></span>

<span data-ttu-id="d2183-127">在後端將一切設定就緒之後，您就可以修改用來登入的用戶端。</span><span class="sxs-lookup"><span data-stu-id="d2183-127">Once everything is configured on the backend, you can modify your client to log in.</span></span> <span data-ttu-id="d2183-128">有以下兩種方法：</span><span class="sxs-lookup"><span data-stu-id="d2183-128">There are two approaches here:</span></span>

* <span data-ttu-id="d2183-129">使用單一行程式碼，讓 Mobile Apps 用戶端 SDK 登入使用者。</span><span class="sxs-lookup"><span data-stu-id="d2183-129">Using a single line of code, let the Mobile Apps client SDK sign in users.</span></span>
* <span data-ttu-id="d2183-130">利用指定的身分識別提供者發佈的 SDK 來建立身分識別，然後取得 App Service 的存取權。</span><span class="sxs-lookup"><span data-stu-id="d2183-130">Leverage an SDK published by a given identity provider to establish identity and then gain access to App Service.</span></span>

> [!TIP]
> <span data-ttu-id="d2183-131">大部分的應用程式都應該使用提供者 SDK 來獲得更自然的登入體驗，以及利用重新整理支援和其他提供者專屬的權益。</span><span class="sxs-lookup"><span data-stu-id="d2183-131">Most applications should use a provider SDK to get a more native-feeling login experience and to leverage refresh support and other provider-specific benefits.</span></span>
> 
> 

### <a name="how-authentication-without-a-provider-sdk-works"></a><span data-ttu-id="d2183-132">不使用提供者 SDK 進行驗證的運作方式</span><span class="sxs-lookup"><span data-stu-id="d2183-132">How authentication without a provider SDK works</span></span>
<span data-ttu-id="d2183-133">如果您不想設定提供者 SDK，則可允許 Mobile Apps 來為您執行登入。</span><span class="sxs-lookup"><span data-stu-id="d2183-133">If you do not wish to set up a provider SDK, you can allow Mobile Apps to perform the login for you.</span></span> <span data-ttu-id="d2183-134">Mobile Apps 用戶端 SDK 將為您選擇的提供者開啟網頁檢視，然後完成登入。</span><span class="sxs-lookup"><span data-stu-id="d2183-134">The Mobile Apps client SDK will open a web view to the provider of your choosing and complete the sign in.</span></span> <span data-ttu-id="d2183-135">您有時會在部落格和論壇上看到這稱為「伺服器流程」或「伺服器導向流程」。因為伺服器正在管理登入，而用戶端 SDK 永遠都不會收到提供者權杖。</span><span class="sxs-lookup"><span data-stu-id="d2183-135">Occasionally on blogs and forums you will see this referred to as the "server flow" or "server-directed flow" since the server is managing the login, and the client SDK never receives the provider token.</span></span>

<span data-ttu-id="d2183-136">啟動此流程所需的程式碼會包含於適用於每個平台的驗證教學課程中。</span><span class="sxs-lookup"><span data-stu-id="d2183-136">The code needed to start this flow is covered in the authentication tutorial for each platform.</span></span> <span data-ttu-id="d2183-137">在流程結束時，用戶端 SDK 會擁有一個 App Service 權杖，而該權杖會自動附加至對後端的所有要求。</span><span class="sxs-lookup"><span data-stu-id="d2183-137">At the end of the flow, the client SDK has an App Service token, and the token is automatically attached to all requests to the backend.</span></span>

### <a name="how-authentication-with-a-provider-sdk-works"></a><span data-ttu-id="d2183-138">使用提供者 SDK 進行驗證的運作方式</span><span class="sxs-lookup"><span data-stu-id="d2183-138">How authentication with a provider SDK works</span></span>
<span data-ttu-id="d2183-139">使用提供者 SDK 可讓登入體驗與 app 執行所在的平台作業系統更緊密地進行互動。</span><span class="sxs-lookup"><span data-stu-id="d2183-139">Working with a provider SDK allows the log-in experience to interact more tightly with the platform OS the app is running on.</span></span> <span data-ttu-id="d2183-140">這也會提供您一個提供者權杖以及用戶端上的一些使用者資訊，讓它更容易取用圖表 API 和自訂使用者體驗。</span><span class="sxs-lookup"><span data-stu-id="d2183-140">This also gives you a provider token and some user information on the client, which makes it much easier to consume graph APIs and customize the user experience.</span></span> <span data-ttu-id="d2183-141">您有時會在部落格和論壇上看到這稱為「用戶端流程」或「用戶端導向的流程」，因為用戶端上的程式碼正在處理登入，而且用戶端程式碼可以存取提供者權杖。</span><span class="sxs-lookup"><span data-stu-id="d2183-141">Occasionally on blogs and forums you will see this referred to as the "client flow" or "client-directed flow" since code on the client is handling the login, and the client code has access to a provider token.</span></span>

<span data-ttu-id="d2183-142">一旦取得提供者權杖之後，它需要傳送給 App Service 以進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d2183-142">Once a provider token is obtained, it needs to be sent to App Service for validation.</span></span> <span data-ttu-id="d2183-143">在流程結束時，用戶端 SDK 會擁有一個 App Service 權杖，而該權杖會自動附加至對後端的所有要求。</span><span class="sxs-lookup"><span data-stu-id="d2183-143">At the end of the flow, the client SDK has an App Service token, and the token is automatically attached to all requests to the backend.</span></span> <span data-ttu-id="d2183-144">如果開發人員選擇這樣做，他們也可以保留對提供者權杖的參考。</span><span class="sxs-lookup"><span data-stu-id="d2183-144">The developer can also keep a reference to the provider token if they so choose.</span></span>

## <a name="how-authorization-works"></a><span data-ttu-id="d2183-145">授權的運作方式</span><span class="sxs-lookup"><span data-stu-id="d2183-145">How authorization works</span></span>
<span data-ttu-id="d2183-146">App Service 驗證 / 授權會公開 **未驗證要求時要採取的動作**的數個選項。</span><span class="sxs-lookup"><span data-stu-id="d2183-146">App Service Authentication / Authorization exposes several choices for **Action to take when request is not authenticated**.</span></span> <span data-ttu-id="d2183-147">在您的程式碼收到指定的要求之前，您可以進行 App Service 檢查來查看是否會驗證要求，如果沒有，請加以拒絕，並先嘗試讓使用者登入，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="d2183-147">Before your code receives a given request, you can have App Service check to see if the request is authenticated and if not, reject it and attempt to have the user log in before trying again.</span></span>

<span data-ttu-id="d2183-148">其中一個選項是讓未經驗證的要求重新導向至其中一個身分識別提供者。</span><span class="sxs-lookup"><span data-stu-id="d2183-148">One option is to have unauthenticated requests redirect to one of the identity providers.</span></span> <span data-ttu-id="d2183-149">在 Web 瀏覽器中，這實際上會將使用者帶到新頁面。</span><span class="sxs-lookup"><span data-stu-id="d2183-149">In a web browser, this would actually take the user to a new page.</span></span> <span data-ttu-id="d2183-150">不過，如此一來，您的行動用戶端就無法重新導向，而且未經驗證的回應將會收到 HTTP「401 未經授權」回應。</span><span class="sxs-lookup"><span data-stu-id="d2183-150">However, your mobile client cannot be redirected in this way, and unauthenticated responses will receive an HTTP *401 Unauthorized* response.</span></span> <span data-ttu-id="d2183-151">考慮到這一點，您的用戶端所提出的第一個要求應一律為登入端點，而您接著可對任何其他 API 進行呼叫。</span><span class="sxs-lookup"><span data-stu-id="d2183-151">Given this, the first request your client makes should always be to the login endpoint, and then you can make calls to any other APIs.</span></span> <span data-ttu-id="d2183-152">如果您嘗試在登入之前呼叫另一個 API，您的用戶端將會收到錯誤。</span><span class="sxs-lookup"><span data-stu-id="d2183-152">If you attempt to call another API before logging in, your client will receive an error.</span></span>

<span data-ttu-id="d2183-153">如果您想要更細微地控制哪些端點需要驗證，您也可以針對未經驗證的要求挑選「沒有動作 (允許要求)」。</span><span class="sxs-lookup"><span data-stu-id="d2183-153">If you wish to have more granular control over which endpoints require authentication, you can also pick "No action (allow request)" for unauthenticated requests.</span></span> <span data-ttu-id="d2183-154">在此情況下，所有驗證決策都會延後至您的應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="d2183-154">In this case, all authentication decisions are deferred to your application code.</span></span> <span data-ttu-id="d2183-155">這也可以讓您根據自訂的授權規則來允許存取特定的使用者。</span><span class="sxs-lookup"><span data-stu-id="d2183-155">This also allows you to allow access to specific users based on custom authorization rules.</span></span>

## <a name="documentation"></a><span data-ttu-id="d2183-156">文件</span><span class="sxs-lookup"><span data-stu-id="d2183-156">Documentation</span></span>
<span data-ttu-id="d2183-157">下列教學課程示範如何使用 App Service，將驗證新增至您的行動用戶端：</span><span class="sxs-lookup"><span data-stu-id="d2183-157">The following tutorials show how to add authentication to your mobile clients using App Service:</span></span>

* <span data-ttu-id="d2183-158">[將驗證新增至您的 iOS 應用程式]</span><span class="sxs-lookup"><span data-stu-id="d2183-158">[Add authentication to your iOS app]</span></span>
* <span data-ttu-id="d2183-159">[將驗證新增至 Xamarin.iOS 應用程式]</span><span class="sxs-lookup"><span data-stu-id="d2183-159">[Add authentication to your Xamarin.iOS app]</span></span>
* <span data-ttu-id="d2183-160">[將驗證新增至 Xamarin.Android 應用程式]</span><span class="sxs-lookup"><span data-stu-id="d2183-160">[Add authentication to your Xamarin.Android app]</span></span>
* <span data-ttu-id="d2183-161">[將驗證新增至您的 Windows App]</span><span class="sxs-lookup"><span data-stu-id="d2183-161">[Add Authentication to your Windows app]</span></span>

<span data-ttu-id="d2183-162">下列教學課程示範如何設定 App Service 來運用不同的驗證提供者：</span><span class="sxs-lookup"><span data-stu-id="d2183-162">The following tutorials show how to configure App Service to leverage different authentication providers:</span></span>

* <span data-ttu-id="d2183-163">[如何設定您的 App 以使用 Azure Active Directory 登入]</span><span class="sxs-lookup"><span data-stu-id="d2183-163">[How to configure your app to use Azure Active Directory login]</span></span>
* <span data-ttu-id="d2183-164">[如何設定 App 以使用 Facebook 登入]</span><span class="sxs-lookup"><span data-stu-id="d2183-164">[How to configure your app to use Facebook login]</span></span>
* <span data-ttu-id="d2183-165">[如何設定 App 以使用 Google 登入]</span><span class="sxs-lookup"><span data-stu-id="d2183-165">[How to configure your app to use Google login]</span></span>
* <span data-ttu-id="d2183-166">[如何設定 App 以使用 Microsoft 帳戶登入]</span><span class="sxs-lookup"><span data-stu-id="d2183-166">[How to configure your app to use Microsoft Account login]</span></span>
* <span data-ttu-id="d2183-167">[如何設定 App 以使用 Twitter 登入]</span><span class="sxs-lookup"><span data-stu-id="d2183-167">[How to configure your app to use Twitter login]</span></span>

<span data-ttu-id="d2183-168">如果您想要使用此處提供之身分識別系統以外的身分識別系統，也可以利用 [預覽 .NET 伺服器 SDK 中的自訂驗證支援](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth)。</span><span class="sxs-lookup"><span data-stu-id="d2183-168">If you wish to use an identity system other than the ones provided here, you can also leverage the [preview custom authentication support in the .NET server SDK](app-service-mobile-dotnet-backend-how-to-use-server-sdk.md#custom-auth).</span></span>

<span data-ttu-id="d2183-169">[將驗證新增至您的 iOS 應用程式]: app-service-mobile-ios-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="d2183-169">[Add authentication to your iOS app]: app-service-mobile-ios-get-started-users.md</span></span>
<span data-ttu-id="d2183-170">[將驗證新增至 Xamarin.iOS 應用程式]: app-service-mobile-xamarin-ios-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="d2183-170">[Add authentication to your Xamarin.iOS app]: app-service-mobile-xamarin-ios-get-started-users.md</span></span>
<span data-ttu-id="d2183-171">[將驗證新增至 Xamarin.Android 應用程式]: app-service-mobile-xamarin-android-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="d2183-171">[Add authentication to your Xamarin.Android app]: app-service-mobile-xamarin-android-get-started-users.md</span></span>
<span data-ttu-id="d2183-172">[將驗證新增至您的 Windows App]: app-service-mobile-windows-store-dotnet-get-started-users.md</span><span class="sxs-lookup"><span data-stu-id="d2183-172">[Add Authentication to your Windows app]: app-service-mobile-windows-store-dotnet-get-started-users.md</span></span>

<span data-ttu-id="d2183-173">[如何設定您的 App 以使用 Azure Active Directory 登入]: app-service-mobile-how-to-configure-active-directory-authentication.md</span><span class="sxs-lookup"><span data-stu-id="d2183-173">[How to configure your app to use Azure Active Directory login]: app-service-mobile-how-to-configure-active-directory-authentication.md</span></span>
<span data-ttu-id="d2183-174">[如何設定 App 以使用 Facebook 登入]: app-service-mobile-how-to-configure-facebook-authentication.md</span><span class="sxs-lookup"><span data-stu-id="d2183-174">[How to configure your app to use Facebook login]: app-service-mobile-how-to-configure-facebook-authentication.md</span></span>
<span data-ttu-id="d2183-175">[如何設定 App 以使用 Google 登入]: app-service-mobile-how-to-configure-google-authentication.md</span><span class="sxs-lookup"><span data-stu-id="d2183-175">[How to configure your app to use Google login]: app-service-mobile-how-to-configure-google-authentication.md</span></span>
<span data-ttu-id="d2183-176">[如何設定 App 以使用 Microsoft 帳戶登入]: app-service-mobile-how-to-configure-microsoft-authentication.md</span><span class="sxs-lookup"><span data-stu-id="d2183-176">[How to configure your app to use Microsoft Account login]: app-service-mobile-how-to-configure-microsoft-authentication.md</span></span>
<span data-ttu-id="d2183-177">[如何設定 App 以使用 Twitter 登入]: app-service-mobile-how-to-configure-twitter-authentication.md</span><span class="sxs-lookup"><span data-stu-id="d2183-177">[How to configure your app to use Twitter login]: app-service-mobile-how-to-configure-twitter-authentication.md</span></span>
