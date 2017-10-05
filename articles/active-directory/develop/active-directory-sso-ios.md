---
title: "如何使用 ADAL 在 iOS 上啟用跨應用程式的 SSO | Microsoft Docs"
description: "如何使用 ADAL SDK 的功能來啟用跨應用程式的單一登入。 "
services: active-directory
documentationcenter: 
author: brandwe
manager: mbaldwin
editor: 
ms.assetid: d042d6da-7503-4e20-bb55-06917de01fcd
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: ios
ms.devlang: objective-c
ms.topic: article
ms.date: 04/07/2017
ms.author: brandwe
ms.custom: aaddev
ms.openlocfilehash: 73b8ed7e6a153a0790f7eae9bd51bb2e554ae72e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-enable-cross-app-sso-on-ios-using-adal"></a><span data-ttu-id="29d6c-103">如何使用 ADAL 在 iOS 上啟用跨應用程式的 SSO</span><span class="sxs-lookup"><span data-stu-id="29d6c-103">How to enable cross-app SSO on iOS using ADAL</span></span>
<span data-ttu-id="29d6c-104">提供單一登入 (SSO)，讓使用者只需要輸入一次認證，就可以讓認證自動跨應用程式運作，這是客戶目前的期待。</span><span class="sxs-lookup"><span data-stu-id="29d6c-104">Providing Single Sign-On (SSO) so that users only need to enter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="29d6c-105">在小型螢幕上輸入其使用者名稱和密碼的困難，通常伴隨著其他因素 (2FA)，例如撥打電話或簡訊傳送程式碼，如果使用者必須對您的產品執行這個動作多次，會容易讓使用者不滿。</span><span class="sxs-lookup"><span data-stu-id="29d6c-105">The difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has to do this more than one time for your product.</span></span>

<span data-ttu-id="29d6c-106">此外，如果您套用其他應用程式可能使用的身分識別平台 (例如 Microsoft 帳戶或來自 Office365 的工作帳戶)，客戶會預期這些認證可以跨所有應用程式使用，而無論是什麼廠商。</span><span class="sxs-lookup"><span data-stu-id="29d6c-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials to be available to use across all their applications no matter the vendor.</span></span>

<span data-ttu-id="29d6c-107">Microsoft 身分識別平台以及我們的 Microsoft 身分識別 SDK 會為您執行這整個繁重的工作，讓您能夠在整個裝置上使用您自己的應用程式套件中的 SSO，或利用我們的訊息代理程式功能和 Authenticator 應用程式，來符合客戶的期待。</span><span class="sxs-lookup"><span data-stu-id="29d6c-107">The Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you the ability to delight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across the entire device.</span></span>

<span data-ttu-id="29d6c-108">本逐步解說會告訴您如何在應用程式中設定我們的 SDK 以提供這個優勢給客戶。</span><span class="sxs-lookup"><span data-stu-id="29d6c-108">This walkthrough will tell you how to configure our SDK within your application to provide this benefit to your customers.</span></span>

<span data-ttu-id="29d6c-109">本逐步解說適用於：</span><span class="sxs-lookup"><span data-stu-id="29d6c-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="29d6c-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="29d6c-110">Azure Active Directory</span></span>
* <span data-ttu-id="29d6c-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="29d6c-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="29d6c-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="29d6c-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="29d6c-113">Azure Active Directory 條件式存取</span><span class="sxs-lookup"><span data-stu-id="29d6c-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="29d6c-114">下列文件假設您知道如何[在 Azure Active Directory 的舊版入口網站中佈建應用程式](active-directory-how-to-integrate.md)，並且已將您的應用程式與 [Microsoft Identity iOS SDK (英文)](https://github.com/AzureAD/azure-activedirectory-library-for-objc) 整合。</span><span class="sxs-lookup"><span data-stu-id="29d6c-114">The document preceding assumes you know how to [provision applications in the legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with the [Microsoft Identity iOS SDK](https://github.com/AzureAD/azure-activedirectory-library-for-objc).</span></span>

## <a name="sso-concepts-in-the-microsoft-identity-platform"></a><span data-ttu-id="29d6c-115">Microsoft 身分識別平台中的 SSO 概念</span><span class="sxs-lookup"><span data-stu-id="29d6c-115">SSO Concepts in the Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="29d6c-116">Microsoft 身分識別代理人</span><span class="sxs-lookup"><span data-stu-id="29d6c-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="29d6c-117">Microsoft 為每個行動平台提供應用程式，允許跨不同廠商的應用程式橋接認證，並允許需要單一安全地方來驗證認證的特殊增強功能。</span><span class="sxs-lookup"><span data-stu-id="29d6c-117">Microsoft provides applications for every mobile platform that allow for the bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where to validate credentials.</span></span> <span data-ttu-id="29d6c-118">我們稱它們為 **訊息代理程式**。</span><span class="sxs-lookup"><span data-stu-id="29d6c-118">We call these **brokers**.</span></span> <span data-ttu-id="29d6c-119">在 iOS 和 Android 上，會透過可下載的應用程式提供這些訊息代理程式，客戶可以獨立安裝它們，或可由為員工管理部分或全部裝置的公司推送至裝置。</span><span class="sxs-lookup"><span data-stu-id="29d6c-119">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages some or all of the device for their employee.</span></span> <span data-ttu-id="29d6c-120">這些訊息代理程式支援只管理某些應用程式或整個裝置的安全性，取決於 IT 系統管理員的需求。</span><span class="sxs-lookup"><span data-stu-id="29d6c-120">These brokers support managing security just for some applications or the entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="29d6c-121">在 Windows 中，內建於作業系統的帳戶選擇器會提供此功能，在技術上稱為 Web 驗證訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-121">In Windows, this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>

<span data-ttu-id="29d6c-122">如需如何使用這些訊息代理程式，以及客戶如何在其 Microsoft 身分識別平台的登入流程中看見它們的詳細資訊，請繼續閱讀。</span><span class="sxs-lookup"><span data-stu-id="29d6c-122">For more information on how we use these brokers and how your customers might see them in their login flow for the Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="29d6c-123">在行動裝置上登入的模式</span><span class="sxs-lookup"><span data-stu-id="29d6c-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="29d6c-124">如需在裝置上存取認證，請遵循 Microsoft 身分識別平台的兩個基本模式︰</span><span class="sxs-lookup"><span data-stu-id="29d6c-124">Access to credentials on devices follow two basic patterns for the Microsoft Identity platform:</span></span>

* <span data-ttu-id="29d6c-125">非訊息代理程式協助登入</span><span class="sxs-lookup"><span data-stu-id="29d6c-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="29d6c-126">訊息代理程式協助登入</span><span class="sxs-lookup"><span data-stu-id="29d6c-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="29d6c-127">非訊息代理程式協助登入</span><span class="sxs-lookup"><span data-stu-id="29d6c-127">Non-broker assisted logins</span></span>
<span data-ttu-id="29d6c-128">非訊息代理程式協助登入是在應用程式內發生的登入體驗，並且使用該應用程式之裝置上的本機儲存體。</span><span class="sxs-lookup"><span data-stu-id="29d6c-128">Non-broker assisted logins are login experiences that happen inline with the application and use the local storage on the device for that application.</span></span> <span data-ttu-id="29d6c-129">儲存體可能會跨應用程式共用，但認證會緊密繫結至使用該認證的應用程式或應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="29d6c-129">This storage may be shared across applications but the credentials are tightly bound to the app or suite of apps using that credential.</span></span> <span data-ttu-id="29d6c-130">當您在應用程式本身內部輸入使用者名稱和密碼時，最可能已在許多行動應用程式中經歷此體驗。</span><span class="sxs-lookup"><span data-stu-id="29d6c-130">You've most likely experienced this in many mobile applications when you enter a username and password within the application itself.</span></span>

<span data-ttu-id="29d6c-131">這些登入具備下列優點︰</span><span class="sxs-lookup"><span data-stu-id="29d6c-131">These logins have the following benefits:</span></span>

* <span data-ttu-id="29d6c-132">使用者體驗完全存在於應用程式內部。</span><span class="sxs-lookup"><span data-stu-id="29d6c-132">User experience exists entirely within the application.</span></span>
* <span data-ttu-id="29d6c-133">認證可以跨由相同憑證登入的應用程式共用，提供單一登入體驗給您的應用程式套件。</span><span class="sxs-lookup"><span data-stu-id="29d6c-133">Credentials can be shared across applications that are signed by the same certificate, providing a single sign-on experience to your suite of applications.</span></span>
* <span data-ttu-id="29d6c-134">在登入前後，會提供登入體驗的控制項給應用程式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-134">Control around the experience of logging in is provided to the application before and after sign-in.</span></span>

<span data-ttu-id="29d6c-135">這些登入具備下列缺點︰</span><span class="sxs-lookup"><span data-stu-id="29d6c-135">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="29d6c-136">使用者無法跨所有使用 Microsoft 身分識別的應用程式體驗單一登入，只會跨應用程式已設定的那些 Microsoft 身分識別。</span><span class="sxs-lookup"><span data-stu-id="29d6c-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="29d6c-137">您的應用程式無法搭配更進階的商務功能使用，例如條件式存取，或使用產品的 InTune 套件。</span><span class="sxs-lookup"><span data-stu-id="29d6c-137">Your application cannot be used with more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="29d6c-138">您的應用程式無法針對商務使用者支援以憑證為基礎的驗證。</span><span class="sxs-lookup"><span data-stu-id="29d6c-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="29d6c-139">以下說明 Microsoft Identity SDK 如何使用應用程式的共用儲存體來啟用 SSO：</span><span class="sxs-lookup"><span data-stu-id="29d6c-139">Here is a representation of how the Microsoft Identity SDKs work with the shared storage of your applications to enable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| ADAL SDK  |  |  ADAL SDK  |  |  ADAK SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="29d6c-140">訊息代理程式協助登入</span><span class="sxs-lookup"><span data-stu-id="29d6c-140">Broker assisted logins</span></span>
<span data-ttu-id="29d6c-141">訊息代理程式協助登入是在訊息代理程式應用程式中發生的登入體驗，並且使用訊息代理程式的儲存體和安全性，跨套用 Microsoft 身分識別平台之裝置上的所有應用程式共用認證。</span><span class="sxs-lookup"><span data-stu-id="29d6c-141">Broker-assisted logins are login experiences that occur within the broker application and use the storage and security of the broker to share credentials across all applications on the device that apply the Microsoft Identity platform.</span></span> <span data-ttu-id="29d6c-142">這表示您的應用程式依賴訊息代理程式來讓使用者登入。</span><span class="sxs-lookup"><span data-stu-id="29d6c-142">This means that your applications rely on the broker to sign users in.</span></span> <span data-ttu-id="29d6c-143">在 iOS 和 Android 上，會透過可下載的應用程式提供這些訊息代理程式，客戶可以獨立安裝它們，或可由為使用者管理裝置的公司推送至裝置。</span><span class="sxs-lookup"><span data-stu-id="29d6c-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed to the device by a company who manages the device for their user.</span></span> <span data-ttu-id="29d6c-144">此類型應用程式的範例為 iOS 上的 Microsoft Authenticator 應用程式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-144">An example of this type of application is the Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="29d6c-145">在 Windows 中，內建於作業系統的帳戶選擇器會提供此功能，在技術上稱為 Web 驗證訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-145">In Windows this functionality is provided by an account chooser built in to the operating system, known technically as the Web Authentication Broker.</span></span>
<span data-ttu-id="29d6c-146">體驗會依平台而有所不同，如果未正確管理，有時可能會干擾使用者。</span><span class="sxs-lookup"><span data-stu-id="29d6c-146">The experience varies by platform and can sometimes be disruptive to users if not managed correctly.</span></span> <span data-ttu-id="29d6c-147">如果您已安裝 Facebook 應用程式，並在另一個應用程式中使用 Facebook Connect，您可能最熟悉這種模式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-147">You're probably most familiar with this pattern if you have the Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="29d6c-148">Microsoft 身分識別平台會使用相同的模式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-148">The Microsoft Identity platform uses the same pattern.</span></span>

<span data-ttu-id="29d6c-149">對於 iOS 而言，這會前往「轉換」動畫，您的應用程式已在其中傳送到背景工作，而 Microsoft Authenticator 應用程式則來到前景讓使用者選取他們想要登入的帳戶。</span><span class="sxs-lookup"><span data-stu-id="29d6c-149">For iOS this leads to a "transition" animation where your application is sent to the background while the Microsoft Authenticator applications comes to the foreground for the user to select which account they would like to sign in with.</span></span>  

<span data-ttu-id="29d6c-150">對於 Android 和 Windows 而言，帳戶選擇器會顯在比較不干擾使用者的應用程式頂端。</span><span class="sxs-lookup"><span data-stu-id="29d6c-150">For Android and Windows the account chooser is displayed on top of your application which is less disruptive to the user.</span></span>

#### <a name="how-the-broker-gets-invoked"></a><span data-ttu-id="29d6c-151">如何叫用訊息代理程式</span><span class="sxs-lookup"><span data-stu-id="29d6c-151">How the broker gets invoked</span></span>
<span data-ttu-id="29d6c-152">如果在裝置上安裝相容的訊息代理程式，例如 Microsoft Authenticator 應用程式，當使用者指出他們想要使用 Microsoft 身分識別平台的任何帳戶登入時，Microsoft 身分識別 SDK 會自動為您叫用訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-152">If a compatible broker is installed on the device, like the Microsoft Authenticator application, the Microsoft Identity SDKs will automatically do the work of invoking the broker for you when a user indicates they wish to log in using any account from the Microsoft Identity platform.</span></span> <span data-ttu-id="29d6c-153">這個帳戶可以是個人的 Microsoft 帳戶、工作或學校帳戶，或您提供的帳戶，以及在 Azure 中使用 B2C 和 B2B 產品的主機。</span><span class="sxs-lookup"><span data-stu-id="29d6c-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 

 #### <a name="how-we-ensure-the-application-is-valid"></a><span data-ttu-id="29d6c-154">我們如何確保應用程式有效</span><span class="sxs-lookup"><span data-stu-id="29d6c-154">How we ensure the application is valid</span></span>
 
 <span data-ttu-id="29d6c-155">需要確保應用程式的身分識別會呼叫訊息代理程式，對於我們在訊息代理程式協助登入中所提供的安全性而言相當重要。</span><span class="sxs-lookup"><span data-stu-id="29d6c-155">The need to ensure the identity of an application call the broker is crucial to the security we provide in broker assisted logins.</span></span> <span data-ttu-id="29d6c-156">IOS 和 Android 都不會強制執行僅對特定應用程式有效的唯一識別碼，因此，惡意應用程式可能會「詐騙」合法應用程式的識別碼，並接收適用於合法應用程式的權杖。</span><span class="sxs-lookup"><span data-stu-id="29d6c-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive the tokens meant for the legitimate application.</span></span> <span data-ttu-id="29d6c-157">若要確定我們一律會在執行階段與正確的應用程式進行通訊，我們會要求開發人員在向 Microsoft 註冊應用程式時提供自訂的 redirectURI。</span><span class="sxs-lookup"><span data-stu-id="29d6c-157">To ensure we are always communicating with the right application at runtime, we ask the developer to provide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="29d6c-158">**以下將詳細討論開發人員應該如何製作此重新導向 URI。**</span><span class="sxs-lookup"><span data-stu-id="29d6c-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="29d6c-159">此自訂的 redirectURI 包含應用程式的搭售識別碼，並透過 Apple App Store 確保它對應用程式而言是唯一的。</span><span class="sxs-lookup"><span data-stu-id="29d6c-159">This custom redirectURI contains the Bundle ID of the application and is ensured to be unique to the application by the Apple App Store.</span></span> <span data-ttu-id="29d6c-160">當應用程式呼叫訊息代理程式時，訊息代理程式會要求 iOS 作業系統搭配呼叫訊息代理程式的配套識別碼來提供它。</span><span class="sxs-lookup"><span data-stu-id="29d6c-160">When an application calls the broker, the broker asks the iOS operating system to provide it with the Bundle ID that called the broker.</span></span> <span data-ttu-id="29d6c-161">訊息代理程式會在對我們身分識別系統的呼叫中將此配套識別碼提供給 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="29d6c-161">The broker provides this Bundle ID to Microsoft in the call to our identity system.</span></span> <span data-ttu-id="29d6c-162">如果應用程式的配套識別碼不符合開發人員在註冊期間提供給我們的配套識別碼，我們將會拒絕存取應用程式所要求之資源的權杖。</span><span class="sxs-lookup"><span data-stu-id="29d6c-162">If the Bundle ID of the application does not match the Bundle ID provided to us by the developer during registration, we will deny access to the tokens for the resource the application is requesting.</span></span> <span data-ttu-id="29d6c-163">這項檢查可確保只有開發人員所註冊的應用程式能夠接收權杖。</span><span class="sxs-lookup"><span data-stu-id="29d6c-163">This check ensures that only the application registered by the developer receives tokens.</span></span>

<span data-ttu-id="29d6c-164">**如果 Microsoft Identity SDK 呼叫訊息代理程式或使用非訊息代理程式協助流程，開發人員就有這個選項。**</span><span class="sxs-lookup"><span data-stu-id="29d6c-164">**The developer has the choice of if the Microsoft Identity SDK calls the broker or uses the non-broker assisted flow.**</span></span> <span data-ttu-id="29d6c-165">不過，如果開發人員選擇不使用訊息代理程式協助流程，他們會失去使用 SSO 認證的優點，使用者可能已在裝置上新增這些認證，並防止 Microsoft 提供給客戶的商務功能使用其應用程式，例如條件式存取、Intune 管理功能和以憑證為基礎的驗證。</span><span class="sxs-lookup"><span data-stu-id="29d6c-165">However if the developer chooses not to use the broker-assisted flow they lose the benefit of using SSO credentials that the user may have already added on the device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="29d6c-166">這些登入具備下列優點︰</span><span class="sxs-lookup"><span data-stu-id="29d6c-166">These logins have the following benefits:</span></span>

* <span data-ttu-id="29d6c-167">無論廠商為何，使用者都可以跨所有應用程式體驗 SSO。</span><span class="sxs-lookup"><span data-stu-id="29d6c-167">User experiences SSO across all their applications no matter the vendor.</span></span>
* <span data-ttu-id="29d6c-168">您的應用程式可以使用更進階的商務功能，例如條件式存取，或使用產品的 InTune 套件。</span><span class="sxs-lookup"><span data-stu-id="29d6c-168">Your application can use more advanced business features such as Conditional Access or use the InTune suite of products.</span></span>
* <span data-ttu-id="29d6c-169">您的應用程式可針對商務使用者支援以憑證為基礎的驗證。</span><span class="sxs-lookup"><span data-stu-id="29d6c-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="29d6c-170">由訊息代理程式利用額外的安全性演算法和加密來驗證應用程式和使用者身分識別，可享有更多安全的登入體驗。</span><span class="sxs-lookup"><span data-stu-id="29d6c-170">Much more secure sign-in experience as the identity of the application and the user are verified by the broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="29d6c-171">這些登入具備下列缺點︰</span><span class="sxs-lookup"><span data-stu-id="29d6c-171">These logins have the following drawbacks:</span></span>

* <span data-ttu-id="29d6c-172">在 iOS 中，使用者可在選擇認證時轉換出您的應用程式體驗。</span><span class="sxs-lookup"><span data-stu-id="29d6c-172">In iOS the user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="29d6c-173">喪失在應用程式內為客戶管理登入體驗的功能。</span><span class="sxs-lookup"><span data-stu-id="29d6c-173">Loss of the ability to manage the login experience for your customers within your application.</span></span>

<span data-ttu-id="29d6c-174">以下說明 Microsoft Identity SDK 如何使用訊息代理程式應用程式來啟用 SSO：</span><span class="sxs-lookup"><span data-stu-id="29d6c-174">Here is a representation of how the Microsoft Identity SDKs work with the broker applications to enable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
| Azure SDK  | | Azure SDK  |   | Azure SDK   |
+-----+------+-+-----+------+-  +-------+-----+
      |              |                  |
      |       +------v------+           |
      |       |             |           |
      |       | Microsoft   |           |
      +-------> Broker      |^----------+
              | Application
              |             |
              +-------------+
              |             |
              |   Broker    |
              |   Storage   |
              |             |
              +-------------+
```

<span data-ttu-id="29d6c-175">有了這個背景資訊，您應該能夠使用 Microsoft 身分識別平台和 SDK 在應用程式內進一步了解和實作 SSO。</span><span class="sxs-lookup"><span data-stu-id="29d6c-175">Armed with this background information you should be able to better understand and implement SSO within your application using the Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="29d6c-176">使用 ADAL 啟用跨應用程式的 SSO</span><span class="sxs-lookup"><span data-stu-id="29d6c-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="29d6c-177">我們會在此處使用 ADAL iOS SDK 執行以下動作：</span><span class="sxs-lookup"><span data-stu-id="29d6c-177">Here we use the ADAL iOS SDK to:</span></span>

* <span data-ttu-id="29d6c-178">開啟應用程式套件的非訊息代理程式協助 SSO</span><span class="sxs-lookup"><span data-stu-id="29d6c-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="29d6c-179">開啟訊息代理程式協助 SSO 的支援</span><span class="sxs-lookup"><span data-stu-id="29d6c-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="29d6c-180">開啟非訊息代理程式協助 SSO 的 SSO</span><span class="sxs-lookup"><span data-stu-id="29d6c-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="29d6c-181">對於跨應用程式的非訊息代理程式協助 SSO，Microsoft Identity SDK 會為您管理 SSO 的大部分複雜內容。</span><span class="sxs-lookup"><span data-stu-id="29d6c-181">For non-broker assisted SSO across applications the Microsoft Identity SDKs manage much of the complexity of SSO for you.</span></span> <span data-ttu-id="29d6c-182">這包括在快取中尋找適當的使用者，以及維護登入使用者的清單以便您查詢。</span><span class="sxs-lookup"><span data-stu-id="29d6c-182">This includes finding the right user in the cache and maintaining a list of logged in users for you to query.</span></span>

<span data-ttu-id="29d6c-183">若要跨您擁有的應用程式啟用 SSO，您需要執行下列動作︰</span><span class="sxs-lookup"><span data-stu-id="29d6c-183">To enable SSO across applications you own you need to do the following:</span></span>

1. <span data-ttu-id="29d6c-184">請確定您所有的應用程式使用相同的用戶端識別碼或應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="29d6c-184">Ensure all your applications user the same Client ID or Application ID.</span></span>
2. <span data-ttu-id="29d6c-185">請確定您所有的應用程式共用來自 Apple 的相同簽署憑證，以便您可以共用金鑰鏈</span><span class="sxs-lookup"><span data-stu-id="29d6c-185">Ensure that all of your applications share the same signing certificate from Apple so that you can share keychains</span></span>
3. <span data-ttu-id="29d6c-186">要求每個應用程式的相同金鑰鏈權利。</span><span class="sxs-lookup"><span data-stu-id="29d6c-186">Request the same keychain entitlement for each of your applications.</span></span>
4. <span data-ttu-id="29d6c-187">告知 Microsoft Identity SDK 您想要我們使用的共用金鑰鏈。</span><span class="sxs-lookup"><span data-stu-id="29d6c-187">Tell the Microsoft Identity SDKs about the shared keychain you want us to use.</span></span>

#### <a name="using-the-same-client-id--application-id-for-all-the-applications-in-your-suite-of-apps"></a><span data-ttu-id="29d6c-188">將相同的用戶端識別碼 / 應用程式識別碼使用於應用程式套件中的所有應用程式</span><span class="sxs-lookup"><span data-stu-id="29d6c-188">Using the same Client ID / Application ID for all the applications in your suite of apps</span></span>
<span data-ttu-id="29d6c-189">為了讓 Microsoft 身分識別平台知道它可以跨應用程式共用權杖，您的每個應用程式必須共用相同的用戶端識別碼或應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="29d6c-189">In order for the Microsoft Identity platform to know that it's allowed to share tokens across your applications, each of your applications will need to share the same Client ID or Application ID.</span></span> <span data-ttu-id="29d6c-190">這是您在入口網站中註冊第一個應用程式時提供給您的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="29d6c-190">This is the unique identifier that was provided to you when you registered your first application in the portal.</span></span>

<span data-ttu-id="29d6c-191">如果 Microsoft 識別服務使用相同的應用程式識別碼，您可能想知道如何識別它的不同應用程式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-191">You may be wondering how you will identify different apps to the Microsoft Identity service if it uses the same Application ID.</span></span> <span data-ttu-id="29d6c-192">答案是使用 **重新導向 URI**。</span><span class="sxs-lookup"><span data-stu-id="29d6c-192">The answer is with the **Redirect URIs**.</span></span> <span data-ttu-id="29d6c-193">每個應用程式可以在上架的入口網站中註冊多個重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="29d6c-193">Each application can have multiple Redirect URIs registered in the onboarding portal.</span></span> <span data-ttu-id="29d6c-194">組件中的每個應用程式將會有不同的重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="29d6c-194">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="29d6c-195">其外觀的範例如下：</span><span class="sxs-lookup"><span data-stu-id="29d6c-195">An example of how this looks is below:</span></span>

<span data-ttu-id="29d6c-196">App1 重新導向 URI： `x-msauth-mytestiosapp://com.myapp.mytestapp`</span><span class="sxs-lookup"><span data-stu-id="29d6c-196">App1 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp`</span></span>

<span data-ttu-id="29d6c-197">App2 重新導向 URI： `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span><span class="sxs-lookup"><span data-stu-id="29d6c-197">App2 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp2`</span></span>

<span data-ttu-id="29d6c-198">App3 重新導向 URI： `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span><span class="sxs-lookup"><span data-stu-id="29d6c-198">App3 Redirect URI: `x-msauth-mytestiosapp://com.myapp.mytestapp3`</span></span>

<span data-ttu-id="29d6c-199">....</span><span class="sxs-lookup"><span data-stu-id="29d6c-199">....</span></span>

<span data-ttu-id="29d6c-200">它們在相同的用戶端識別碼 / 應用程式識別碼之下是巢狀的，並且可根據您在 SDK 組態中傳回給我們的重新導向 URI 查看。</span><span class="sxs-lookup"><span data-stu-id="29d6c-200">These are nested under the same client ID / application ID and looked up based on the redirect URI you return to us in your SDK configuration.</span></span>

```
+-------------------+
|                   |
|  Client ID        |
+---------+---------+
          |
          |           +-----------------------------------+
          |           |  App 1 Redirect URI               |
          +----------^+                                   |
          |           +-----------------------------------+
          |
          |           +-----------------------------------+
          +----------^+  App 2 Redirect URI               |
          |           |                                   |
          |           +-----------------------------------+
          |
          +----------^+-----------------------------------+
                      |  App 3 Redirect URI               |
                      |                                   |
                      +-----------------------------------+

```


<span data-ttu-id="29d6c-201">請注意，以下將說明這些重新導向 URI 的格式。您可以使用任何重新導向 URI，除非您想要支援訊息代理程式，在此情況下，它們的外觀必須如上所示</span><span class="sxs-lookup"><span data-stu-id="29d6c-201">*Note that the format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish to support the broker, in which case they must look something like the above*</span></span>

#### <a name="create-keychain-sharing-between-applications"></a><span data-ttu-id="29d6c-202">建立應用程式之間共用的金鑰鏈</span><span class="sxs-lookup"><span data-stu-id="29d6c-202">Create keychain sharing between applications</span></span>
<span data-ttu-id="29d6c-203">啟用金鑰鏈共用已超出本文範圍，包含在 Apple 的 [新增功能](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html)文件中。</span><span class="sxs-lookup"><span data-stu-id="29d6c-203">Enabling keychain sharing is beyond the scope of this document and covered by Apple in their document [Adding Capabilities](https://developer.apple.com/library/ios/documentation/IDEs/Conceptual/AppDistributionGuide/AddingCapabilities/AddingCapabilities.html).</span></span> <span data-ttu-id="29d6c-204">您必須決定金鑰鍊的名稱，並且跨所有應用程式新增該功能。</span><span class="sxs-lookup"><span data-stu-id="29d6c-204">What is important is that you decide what you want your keychain to be called and add that capability across all your applications.</span></span>

<span data-ttu-id="29d6c-205">當您確實已正確設定權利時，您應該會在標題為 `entitlements.plist` 的專案目錄中看到檔案，其中包含的項目外觀如下︰</span><span class="sxs-lookup"><span data-stu-id="29d6c-205">When you do have entitlements set up correctly you should see a file in your project directory entitled `entitlements.plist` that contains something that looks like the following:</span></span>

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE plist PUBLIC "-//Apple//DTD PLIST 1.0//EN" "http://www.apple.com/DTDs/PropertyList-1.0.dtd">
<plist version="1.0">
<dict>
    <key>keychain-access-groups</key>
    <array>
        <string>$(AppIdentifierPrefix)com.myapp.mytestapp</string>
        <string>$(AppIdentifierPrefix)com.myapp.mycache</string>
    </array>
</dict>
</plist>
```

<span data-ttu-id="29d6c-206">一旦您在每個應用程式中啟用金鑰鍊權利，而且您已準備好使用 SSO，請在使用下列設定的 `ADAuthenticationSettings` 中使用下列設定告訴 Microsoft Identity SDK 關於金鑰鍊的資訊：</span><span class="sxs-lookup"><span data-stu-id="29d6c-206">Once you have the keychain entitlement enabled in each of your applications, and you are ready to use SSO, tell the Microsoft Identity SDK about your keychain by using the following setting in your `ADAuthenticationSettings` with the following setting:</span></span>

```
defaultKeychainSharingGroup=@"com.myapp.mycache";
```

> [!WARNING]
> <span data-ttu-id="29d6c-207">當您跨應用程式共用金鑰鍊時，任何應用程式都可以刪除使用者，更糟的是可以跨應用程式刪除所有權杖。</span><span class="sxs-lookup"><span data-stu-id="29d6c-207">When you share a keychain across your applications any application can delete users or worse delete all the tokens across your application.</span></span> <span data-ttu-id="29d6c-208">如果您的應用程式依賴這些權杖來執行背景工作，這樣會造成可怕的災難。</span><span class="sxs-lookup"><span data-stu-id="29d6c-208">This is particularly disastrous if you have applications that rely on the tokens to do background work.</span></span> <span data-ttu-id="29d6c-209">共用金鑰鏈表示您在整個 Microsoft Identity SDK 必須非常小心進行任何移除作業。</span><span class="sxs-lookup"><span data-stu-id="29d6c-209">Sharing a keychain means that you must be very careful in any and all remove operations through the Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="29d6c-210">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="29d6c-210">That's it!</span></span> <span data-ttu-id="29d6c-211">Microsoft Identity SDK 現在會跨所有應用程式共用認證。</span><span class="sxs-lookup"><span data-stu-id="29d6c-211">The Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="29d6c-212">使用者清單也會跨應用程式執行個體共用。</span><span class="sxs-lookup"><span data-stu-id="29d6c-212">The user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="29d6c-213">開啟訊息代理程式協助 SSO 的 SSO</span><span class="sxs-lookup"><span data-stu-id="29d6c-213">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="29d6c-214">應用程式使用任何已安裝在裝置上之訊息代理程式的功能 **預設為關閉**。</span><span class="sxs-lookup"><span data-stu-id="29d6c-214">The ability for an application to use any broker that is installed on the device is **turned off by default**.</span></span> <span data-ttu-id="29d6c-215">若要搭配使用應用程式與訊息代理程式，您必須執行一些額外的設定，並將一些程式碼新增至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-215">In order to use your application with the broker you must do some additional configuration and add some code to your application.</span></span>

<span data-ttu-id="29d6c-216">要遵循的步驟如下：</span><span class="sxs-lookup"><span data-stu-id="29d6c-216">The steps to follow are:</span></span>

1. <span data-ttu-id="29d6c-217">在應用程式程式碼呼叫 MS SDK 時啟用訊息代理程式模式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-217">Enable broker mode in your application code's call to the MS SDK.</span></span>
2. <span data-ttu-id="29d6c-218">建立新的重新導向 URI，並將其提供給應用程式與應用程式註冊。</span><span class="sxs-lookup"><span data-stu-id="29d6c-218">Establish a new redirect URI and provide that to both the app and your app registration.</span></span>
3. <span data-ttu-id="29d6c-219">註冊 URL 配置。</span><span class="sxs-lookup"><span data-stu-id="29d6c-219">Registering a URL Scheme.</span></span>
4. <span data-ttu-id="29d6c-220">iOS9 支援︰新增權限至 info.plist 檔案。</span><span class="sxs-lookup"><span data-stu-id="29d6c-220">iOS9 Support: Add a permission to your info.plist file.</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="29d6c-221">步驟 1︰在應用程式中啟用訊息代理程式模式</span><span class="sxs-lookup"><span data-stu-id="29d6c-221">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="29d6c-222">當您建立「內容」或驗證物件的初始設定時，已開啟應用程式使用訊息代理程式的功能。</span><span class="sxs-lookup"><span data-stu-id="29d6c-222">The ability for your application to use the broker is turned on when you create the "context" or initial setup of your Authentication object.</span></span> <span data-ttu-id="29d6c-223">您可以設定程式碼中的認證類型就可以辦到︰</span><span class="sxs-lookup"><span data-stu-id="29d6c-223">You do this by setting your credentials type in your code:</span></span>

```
/*! See the ADCredentialsType enumeration definition for details */
@propertyADCredentialsType credentialsType;
```
<span data-ttu-id="29d6c-224">`AD_CREDENTIALS_AUTO` 設定可讓 Microsoft Identity SDK 嘗試呼叫訊息代理程式，`AD_CREDENTIALS_EMBEDDED` 會防止 Microsoft Identity SDK 呼叫訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-224">The `AD_CREDENTIALS_AUTO` setting will allow the Microsoft Identity SDK to try to call out to the broker, `AD_CREDENTIALS_EMBEDDED` will prevent the Microsoft Identity SDK from calling to the broker.</span></span>

#### <a name="step-2-registering-a-url-scheme"></a><span data-ttu-id="29d6c-225">步驟 2︰註冊 URL 配置</span><span class="sxs-lookup"><span data-stu-id="29d6c-225">Step 2: Registering a URL Scheme</span></span>
<span data-ttu-id="29d6c-226">Microsoft 身分識別平台會使用 URL 叫用訊息代理程式，然後將控制項傳回至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-226">The Microsoft Identity platform uses URLs to invoke the broker and then return control back to your application.</span></span> <span data-ttu-id="29d6c-227">若要完成該往返行程，您需要為應用程式註冊的 URL 配置，Microsoft 身分識別平台將會了解該配置。</span><span class="sxs-lookup"><span data-stu-id="29d6c-227">To finish that round trip you need a URL scheme registered for your application that the Microsoft Identity platform will know about.</span></span> <span data-ttu-id="29d6c-228">此配置可以是您先前可能已向應用程式註冊之任何其他應用程式配置以外的配置。</span><span class="sxs-lookup"><span data-stu-id="29d6c-228">This can be in addition to any other app schemes you may have previously registered with your application.</span></span>

> [!WARNING]
> <span data-ttu-id="29d6c-229">建議您讓 URL 配置唯一無二，將其他應用程式使用相同 URL 配置的機會降到最低。</span><span class="sxs-lookup"><span data-stu-id="29d6c-229">We recommend making the URL scheme fairly unique to minimize the chances of another app using the same URL scheme.</span></span> <span data-ttu-id="29d6c-230">Apple 不會強制要求在應用程式存放區中註冊之 URL 配置的獨特性。</span><span class="sxs-lookup"><span data-stu-id="29d6c-230">Apple does not enforce the uniqueness of URL schemes that are registered in the app store.</span></span>
> 
> 

<span data-ttu-id="29d6c-231">以下是這個情形會如何出現在您的專案組態的範例。</span><span class="sxs-lookup"><span data-stu-id="29d6c-231">Below is an example of how this appears in your project configuration.</span></span> <span data-ttu-id="29d6c-232">您可能也會在 XCode 中這樣做︰</span><span class="sxs-lookup"><span data-stu-id="29d6c-232">You may also do this in XCode as well:</span></span>

```
<key>CFBundleURLTypes</key>
<array>
    <dict>
        <key>CFBundleTypeRole</key>
        <string>Editor</string>
        <key>CFBundleURLName</key>
        <string>com.myapp.mytestapp</string>
        <key>CFBundleURLSchemes</key>
        <array>
            <string>x-msauth-mytestiosapp</string>
        </array>
    </dict>
</array>
```

#### <a name="step-3-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="29d6c-233">步驟 3︰利用 URL 配置建立新的重新導向 URI</span><span class="sxs-lookup"><span data-stu-id="29d6c-233">Step 3: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="29d6c-234">為了確保我們永遠傳回認證權杖給正確的應用程式，我們必須確定 iOS 作業系統可以確認我們回呼應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-234">In order to ensure that we always return the credential tokens to the correct application, we need to make sure we call back to your application in a way that the iOS operating system can verify.</span></span> <span data-ttu-id="29d6c-235">iOS 作業系統會向 Microsoft 訊息代理程式應用程式回報呼叫它之應用程式的組合識別碼。</span><span class="sxs-lookup"><span data-stu-id="29d6c-235">The iOS operating system reports to the Microsoft broker applications the Bundle ID of the application calling it.</span></span> <span data-ttu-id="29d6c-236">這樣就不會讓惡意應用程式假冒。</span><span class="sxs-lookup"><span data-stu-id="29d6c-236">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="29d6c-237">因此，我們利用這個方法搭配訊息代理程式應用程式的 URI，以確保將權杖傳回給正確的應用程式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-237">Therefore, we leverage this along with the URI of our broker application to ensure that the tokens are returned to the correct application.</span></span> <span data-ttu-id="29d6c-238">我們需要您在應用程式中建立此唯一重新導向 URI，並在我們的開發人員入口網站中設定為重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="29d6c-238">We require you to establish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="29d6c-239">您的重新導向 URI 必須是適當的格式︰</span><span class="sxs-lookup"><span data-stu-id="29d6c-239">Your redirect URI must be in the proper form of:</span></span>

`<app-scheme>://<your.bundle.id>`

<span data-ttu-id="29d6c-240">例如︰x-msauth-mytestiosapp://com.myapp.mytestapp </span><span class="sxs-lookup"><span data-stu-id="29d6c-240">ex: *x-msauth-mytestiosapp://com.myapp.mytestapp*</span></span>

<span data-ttu-id="29d6c-241">此重新導向 URI 必須使用 [Azure 入口網站](https://portal.azure.com/)在應用程式註冊中指定。</span><span class="sxs-lookup"><span data-stu-id="29d6c-241">This Redirect URI needs to be specified in your app registration using the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="29d6c-242">如需 Azure AD 應用程式註冊的詳細資訊，請參閱 [與 Azure Active Directory 整合](active-directory-how-to-integrate.md)。</span><span class="sxs-lookup"><span data-stu-id="29d6c-242">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

##### <a name="step-3a-add-a-redirect-uri-in-your-app-and-dev-portal-to-support-certificate-based-authentication"></a><span data-ttu-id="29d6c-243">步驟 3a︰在應用程式與開發人員入口網站中新增重新導向 URI 以支援以憑證為基礎的驗證</span><span class="sxs-lookup"><span data-stu-id="29d6c-243">Step 3a: Add a redirect URI in your app and dev portal to support certificate based authentication</span></span>
<span data-ttu-id="29d6c-244">若要支援以憑證為基礎的驗證，必須在您的應用程式與 [Azure 入口網站](https://portal.azure.com/) 中註冊第二個 "msauth"，才能在應用程式中新增該支援。</span><span class="sxs-lookup"><span data-stu-id="29d6c-244">To support cert based authentication a second "msauth"  needs to be registered in your application and the [Azure portal](https://portal.azure.com/) to handle certificate authentication if you wish to add that support in your application.</span></span>

`msauth://code/<broker-redirect-uri-in-url-encoded-form>`

<span data-ttu-id="29d6c-245">例如︰msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp</span><span class="sxs-lookup"><span data-stu-id="29d6c-245">ex: *msauth://code/x-msauth-mytestiosapp%3A%2F%2Fcom.myapp.mytestapp*</span></span>

#### <a name="step-4-ios9-add-a-configuration-parameter-to-your-app"></a><span data-ttu-id="29d6c-246">步驟 4：iOS9︰將組態參數新增至您的應用程式</span><span class="sxs-lookup"><span data-stu-id="29d6c-246">Step 4: iOS9: Add a configuration parameter to your app</span></span>
<span data-ttu-id="29d6c-247">ADAL 會使用 –canOpenURL: 檢查裝置上是否已安裝訊息代理程式。</span><span class="sxs-lookup"><span data-stu-id="29d6c-247">ADAL uses –canOpenURL: to check if the broker is installed on the device.</span></span> <span data-ttu-id="29d6c-248">在 iOS 9 中，Apple 會鎖定應用程式可以查詢的配置。</span><span class="sxs-lookup"><span data-stu-id="29d6c-248">In iOS 9 Apple locked down what schemes an application can query for.</span></span> <span data-ttu-id="29d6c-249">您必須將 “msauth” 新增至 `info.plist file`的 LSApplicationQueriesSchemes 區段。</span><span class="sxs-lookup"><span data-stu-id="29d6c-249">You will need to add “msauth” to the LSApplicationQueriesSchemes section of your `info.plist file`.</span></span>

<span data-ttu-id="29d6c-250"><key>LSApplicationQueriesSchemes</key></span><span class="sxs-lookup"><span data-stu-id="29d6c-250"><key>LSApplicationQueriesSchemes</key></span></span>

<span data-ttu-id="29d6c-251"><array><string>msauth</string>
</array></span><span class="sxs-lookup"><span data-stu-id="29d6c-251"><array> <string>msauth</string>
</array></span></span>

### <a name="youve-configured-sso"></a><span data-ttu-id="29d6c-252">您已設定 SSO！</span><span class="sxs-lookup"><span data-stu-id="29d6c-252">You've configured SSO!</span></span>
<span data-ttu-id="29d6c-253">現在 Microsoft Identity SDK 會自動跨應用程式共用認證，並在訊息代理程式出現在其裝置上時叫用它。</span><span class="sxs-lookup"><span data-stu-id="29d6c-253">Now the Microsoft Identity SDK will automatically both share credentials across your applications and invoke the broker if it's present on their device.</span></span>

