---
title: "aaaHow tooenable 跨應用程式使用 ADAL 的 Android 上的 SSO |Microsoft 文件"
description: "如何 toouse hello 功能 hello 跨應用程式的 ADAL SDK tooenable 單一登入。 "
services: active-directory
documentationcenter: 
author: danieldobalian
manager: mbaldwin
editor: 
ms.assetid: 40710225-05ab-40a3-9aec-8b4e96b6b5e7
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: android
ms.devlang: java
ms.topic: article
ms.date: 04/07/2017
ms.author: dadobali
ms.custom: aaddev
ms.openlocfilehash: 3867e15030e5516464e4dbd92ba35894430daf00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooenable-cross-app-sso-on-android-using-adal"></a><span data-ttu-id="7c5c0-103">如何 tooenable 跨應用程式使用 ADAL 的 Android 上的 SSO</span><span class="sxs-lookup"><span data-stu-id="7c5c0-103">How tooenable cross-app SSO on Android using ADAL</span></span>
<span data-ttu-id="7c5c0-104">現在必須由客戶提供單一登入 (SSO)，讓使用者只需要 tooenter 其認證一次，並跨應用程式具有這些認證會自動運作。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-104">Providing Single Sign-On (SSO) so that users only need tooenter their credentials once and have those credentials automatically work across applications is now expected by customers.</span></span> <span data-ttu-id="7c5c0-105">在小型螢幕上，通常時間結合其他因素 (2FA)，例如通話或簡訊的程式碼中，輸入使用者名稱和密碼的 hello 難度導致快速不滿，如果使用者有 toodo 這一次以上為您的產品。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-105">hello difficulty in entering their username and password on a small screen, often times combined with an additional factor (2FA) like a phone call or a texted code, results in quick dissatisfaction if a user has toodo this more than one time for your product.</span></span>

<span data-ttu-id="7c5c0-106">此外，如果您套用其他應用程式可能會使用如 Microsoft 帳戶或從 Office365 工作帳戶的身分識別平台時，客戶會預期，提供其所有的應用程式 toouse 那些認證 toobe 無論 hello 廠商。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-106">In addition, if you apply an identity platform that other applications may use such as Microsoft Accounts or a work account from Office365, customers expect that those credentials toobe available toouse across all their applications no matter hello vendor.</span></span>

<span data-ttu-id="7c5c0-107">hello Microsoft 識別身分平台，以及我們 Microsoft 身分識別的 Sdk，運作所有此硬碟的您，並可讓客戶可以發生在您自己的 suite 應用程式，或做為 SSO hello 能力 toodelight 與我們的 broker 功能和驗證器跨應用程式，hello 整個裝置。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-107">hello Microsoft Identity platform, along with our Microsoft Identity SDKs, does all this hard work for you and gives you hello ability toodelight your customers with SSO either within your own suite of applications or, as with our broker capability and Authenticator applications, across hello entire device.</span></span>

<span data-ttu-id="7c5c0-108">本逐步解說會告訴您如何 tooconfigure 我們 SDK 內的應用程式 tooprovide 此權益 tooyour 客戶。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-108">This walkthrough will tell you how tooconfigure our SDK within your application tooprovide this benefit tooyour customers.</span></span>

<span data-ttu-id="7c5c0-109">本逐步解說適用於：</span><span class="sxs-lookup"><span data-stu-id="7c5c0-109">This walkthrough applies to:</span></span>

* <span data-ttu-id="7c5c0-110">Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7c5c0-110">Azure Active Directory</span></span>
* <span data-ttu-id="7c5c0-111">Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="7c5c0-111">Azure Active Directory B2C</span></span>
* <span data-ttu-id="7c5c0-112">Azure Active Directory B2B</span><span class="sxs-lookup"><span data-stu-id="7c5c0-112">Azure Active Directory B2B</span></span>
* <span data-ttu-id="7c5c0-113">Azure Active Directory 條件式存取</span><span class="sxs-lookup"><span data-stu-id="7c5c0-113">Azure Active Directory Conditional Access</span></span>

<span data-ttu-id="7c5c0-114">上述的 hello 文件假設您知道如何太[佈建 Azure Active Directory 的 hello 舊版入口網站中的應用程式](active-directory-how-to-integrate.md)hello 與整合您的應用程式和[Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span><span class="sxs-lookup"><span data-stu-id="7c5c0-114">hello document preceding assumes you know how too[provision applications in hello legacy portal for Azure Active Directory](active-directory-how-to-integrate.md) and integrated your application with hello [Microsoft Identity Android SDK](https://github.com/AzureAD/azure-activedirectory-library-for-android).</span></span>

## <a name="sso-concepts-in-hello-microsoft-identity-platform"></a><span data-ttu-id="7c5c0-115">在 hello Microsoft 識別身分平台中的 SSO 概念</span><span class="sxs-lookup"><span data-stu-id="7c5c0-115">SSO Concepts in hello Microsoft Identity Platform</span></span>
### <a name="microsoft-identity-brokers"></a><span data-ttu-id="7c5c0-116">Microsoft 身分識別代理人</span><span class="sxs-lookup"><span data-stu-id="7c5c0-116">Microsoft Identity Brokers</span></span>
<span data-ttu-id="7c5c0-117">Microsoft 提供應用程式的每個行動平台，允許不同廠商的應用程式間 hello 橋接的認證，並允許特殊的增強功能需要單一的安全位置，從哪裡 toovalidate 認證。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-117">Microsoft provides applications for every mobile platform that allow for hello bridging of credentials across applications from different vendors and allows for special enhanced features that require a single secure place from where toovalidate credentials.</span></span> <span data-ttu-id="7c5c0-118">我們稱它們為 **訊息代理程式**。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-118">We call these **brokers**.</span></span> <span data-ttu-id="7c5c0-119">IOS 和 Android 上提供這些項目透過可下載的應用程式的客戶獨立安裝或由負責管理其員工的部分或全部 hello 裝置的公司可以推送 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-119">On iOS and Android these are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages some or all of hello device for their employee.</span></span> <span data-ttu-id="7c5c0-120">這些代理程式只用於某些應用程式或根據 IT 系統管理員想要的 hello 整個裝置支援管理安全性。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-120">These brokers support managing security just for some applications or hello entire device based on what IT Administrators desire.</span></span> <span data-ttu-id="7c5c0-121">在 Windows 中，這項功能是由 toohello 作業系統，技術上來說稱為 hello Web 驗證代理人內建帳戶選擇器提供的。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-121">In Windows, this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>

<span data-ttu-id="7c5c0-122">如需詳細資訊，我們使用這些仲介和如何您的客戶可能會看到它們在其登入資料流程中為 hello Microsoft 身分識別平台上讀取。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-122">For more information on how we use these brokers and how your customers might see them in their login flow for hello Microsoft Identity platform read on.</span></span>

### <a name="patterns-for-logging-in-on-mobile-devices"></a><span data-ttu-id="7c5c0-123">在行動裝置上登入的模式</span><span class="sxs-lookup"><span data-stu-id="7c5c0-123">Patterns for logging in on mobile devices</span></span>
<span data-ttu-id="7c5c0-124">在裝置上的存取 toocredentials 遵循 hello Microsoft 識別身分平台中的兩個基本模式：</span><span class="sxs-lookup"><span data-stu-id="7c5c0-124">Access toocredentials on devices follow two basic patterns for hello Microsoft Identity platform:</span></span>

* <span data-ttu-id="7c5c0-125">非訊息代理程式協助登入</span><span class="sxs-lookup"><span data-stu-id="7c5c0-125">Non-broker assisted logins</span></span>
* <span data-ttu-id="7c5c0-126">訊息代理程式協助登入</span><span class="sxs-lookup"><span data-stu-id="7c5c0-126">Broker assisted logins</span></span>

#### <a name="non-broker-assisted-logins"></a><span data-ttu-id="7c5c0-127">非訊息代理程式協助登入</span><span class="sxs-lookup"><span data-stu-id="7c5c0-127">Non-broker assisted logins</span></span>
<span data-ttu-id="7c5c0-128">非 broker 協助登入是內嵌於 hello 應用程式，就可能發生，在該應用程式的 hello 裝置上使用本機儲存體 hello 登入體驗。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-128">Non-broker assisted logins are login experiences that happen inline with hello application and use hello local storage on hello device for that application.</span></span> <span data-ttu-id="7c5c0-129">這個儲存體可能會跨應用程式共用但 hello 認證緊密繫結的 toohello 應用程式或套件的應用程式使用該認證。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-129">This storage may be shared across applications but hello credentials are tightly bound toohello app or suite of apps using that credential.</span></span> <span data-ttu-id="7c5c0-130">最有可能遭遇這許多行動應用程式中輸入使用者名稱和密碼 hello 應用程式本身內時。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-130">You've most likely experienced this in many mobile applications when you enter a username and password within hello application itself.</span></span>

<span data-ttu-id="7c5c0-131">這些登入具有下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="7c5c0-131">These logins have hello following benefits:</span></span>

* <span data-ttu-id="7c5c0-132">使用者經驗完全內含 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-132">User experience exists entirely within hello application.</span></span>
* <span data-ttu-id="7c5c0-133">認證可 hello 所簽署的應用程式之間共用相同的憑證，提供單一登入體驗 tooyour 套應用程式。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-133">Credentials can be shared across applications that are signed by hello same certificate, providing a single sign-on experience tooyour suite of applications.</span></span>
* <span data-ttu-id="7c5c0-134">控制項周圍的登入的 hello 經驗提供 toohello 應用程式之前和之後登入。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-134">Control around hello experience of logging in is provided toohello application before and after sign-in.</span></span>

<span data-ttu-id="7c5c0-135">這些登入有下列缺點 hello:</span><span class="sxs-lookup"><span data-stu-id="7c5c0-135">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="7c5c0-136">使用者無法跨所有使用 Microsoft 身分識別的應用程式體驗單一登入，只會跨應用程式已設定的那些 Microsoft 身分識別。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-136">User cannot experience single-sign on across all apps that use a Microsoft Identity, only across those Microsoft Identities that your application has configured.</span></span>
* <span data-ttu-id="7c5c0-137">您的應用程式不能與更進階的商業功能，例如條件式存取或使用 hello InTune 套件的產品。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-137">Your application cannot be used with more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="7c5c0-138">您的應用程式無法針對商務使用者支援以憑證為基礎的驗證。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-138">Your application can't support certificate-based authentication for business users.</span></span>

<span data-ttu-id="7c5c0-139">以下是與您的應用程式 tooenable SSO 的 hello 共用存放裝置 hello Microsoft 識別 Sdk 的運作方式的表示法：</span><span class="sxs-lookup"><span data-stu-id="7c5c0-139">Here is a representation of how hello Microsoft Identity SDKs work with hello shared storage of your applications tooenable SSO:</span></span>

```
+------------+ +------------+  +-------------+
|            | |            |  |             |
|   App 1    | |   App 2    |  |   App 3     |
|            | |            |  |             |
|            | |            |  |             |
+------------+ +------------+  +-------------+
| Azure SDK  | | Azure SDK  |  | Azure SDK   |
+------------+-+------------+--+-------------+
|                                            |
|            App Shared Storage              |
+--------------------------------------------+
```

#### <a name="broker-assisted-logins"></a><span data-ttu-id="7c5c0-140">訊息代理程式協助登入</span><span class="sxs-lookup"><span data-stu-id="7c5c0-140">Broker assisted logins</span></span>
<span data-ttu-id="7c5c0-141">Broker 輔助登入係指 hello broker 應用程式內發生，並且套用 hello Microsoft 識別身分平台中 hello 裝置上所有應用程式使用 hello 儲存和安全性的 hello broker tooshare 認證登入體驗。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-141">Broker-assisted logins are login experiences that occur within hello broker application and use hello storage and security of hello broker tooshare credentials across all applications on hello device that apply hello Microsoft Identity platform.</span></span> <span data-ttu-id="7c5c0-142">這表示您的應用程式依賴中的 hello broker toosign 使用者。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-142">This means that your applications rely on hello broker toosign users in.</span></span> <span data-ttu-id="7c5c0-143">IOS 和 Android 上是在透過可下載的應用程式提供這些 broker 客戶獨立安裝或由負責管理其使用者的 hello 裝置的公司可以推送 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-143">On iOS and Android these brokers are provided through downloadable applications that customers either install independently or can be pushed toohello device by a company who manages hello device for their user.</span></span> <span data-ttu-id="7c5c0-144">這種類型的應用程式的範例是在 iOS 上的 hello Microsoft 驗證器應用程式。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-144">An example of this type of application is hello Microsoft Authenticator application on iOS.</span></span> <span data-ttu-id="7c5c0-145">在 Windows 中 toohello 作業系統，技術上來說稱為 hello Web 驗證代理人內建帳戶選擇器會提供此功能。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-145">In Windows this functionality is provided by an account chooser built in toohello operating system, known technically as hello Web Authentication Broker.</span></span>
<span data-ttu-id="7c5c0-146">hello 體驗會依平台而有所不同，有時可能干擾 toousers 如果未正確管理。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-146">hello experience varies by platform and can sometimes be disruptive toousers if not managed correctly.</span></span> <span data-ttu-id="7c5c0-147">如果您已安裝的 hello Facebook 應用程式，並從另一個應用程式中使用 Facebook Connect，您已使用此模式可能是最熟悉。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-147">You're probably most familiar with this pattern if you have hello Facebook application installed and use Facebook Connect from another application.</span></span> <span data-ttu-id="7c5c0-148">hello Microsoft 身分識別平台使用 hello 相同的模式。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-148">hello Microsoft Identity platform uses hello same pattern.</span></span>

<span data-ttu-id="7c5c0-149">適用於 iOS 這會導致 tooa 「 過渡 」 動畫的應用程式傳送 toohello 背景 hello Microsoft 驗證器應用程式時出現的 hello 使用者 tooselect toohello 前景他們想 toosign 中使用哪一個帳戶。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-149">For iOS this leads tooa "transition" animation where your application is sent toohello background while hello Microsoft Authenticator applications comes toohello foreground for hello user tooselect which account they would like toosign in with.</span></span>  

<span data-ttu-id="7c5c0-150">Android 和 Windows hello 帳戶選擇器會顯示在您的應用程式也就是比較不會干擾 toohello 使用者之上。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-150">For Android and Windows hello account chooser is displayed on top of your application which is less disruptive toohello user.</span></span>

#### <a name="how-hello-broker-gets-invoked"></a><span data-ttu-id="7c5c0-151">Hello broker 取得叫用的方式</span><span class="sxs-lookup"><span data-stu-id="7c5c0-151">How hello broker gets invoked</span></span>
<span data-ttu-id="7c5c0-152">如果在 hello 裝置，例如 hello Microsoft 驗證器應用程式，hello Microsoft 識別 Sdk 會自動安裝相容的 broker hello 當使用者表示他們想在使用中的任何帳戶 toolog 叫用 hello broker，為您的工作hello Microsoft 身分識別平台。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-152">If a compatible broker is installed on hello device, like hello Microsoft Authenticator application, hello Microsoft Identity SDKs will automatically do hello work of invoking hello broker for you when a user indicates they wish toolog in using any account from hello Microsoft Identity platform.</span></span> <span data-ttu-id="7c5c0-153">這個帳戶可以是個人的 Microsoft 帳戶、工作或學校帳戶，或您提供的帳戶，以及在 Azure 中使用 B2C 和 B2B 產品的主機。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-153">This account could be a personal Microsoft Account, a work or school account, or an account that you provide and host in Azure using our B2C and B2B products.</span></span> 
 
 #### <a name="how-we-ensure-hello-application-is-valid"></a><span data-ttu-id="7c5c0-154">我們如何確保 hello 應用程式無效</span><span class="sxs-lookup"><span data-stu-id="7c5c0-154">How we ensure hello application is valid</span></span>
 
 <span data-ttu-id="7c5c0-155">我們提供協助的 broker 登入中的重要 toohello 安全性 hello 需要 tooensure hello 識別的應用程式呼叫 hello 代理人。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-155">hello need tooensure hello identity of an application call hello broker is crucial toohello security we provide in broker assisted logins.</span></span> <span data-ttu-id="7c5c0-156">IOS 和 Android 都不會強制執行唯一的識別項僅適用於特定應用程式，讓惡意應用程式可能會 「 詐騙 」 合法應用程式的識別項和接收 hello 語彙基元適用於 hello 合法的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-156">Neither iOS nor Android enforces unique identifiers that are valid only for a given application, so malicious applications may "spoof" a legitimate application's identifier and receive hello tokens meant for hello legitimate application.</span></span> <span data-ttu-id="7c5c0-157">tooensure 我們一律會與 hello 右應用程式在執行階段通訊，我們會要求 hello 開發人員 tooprovide 自訂 redirectURI 向 Microsoft 註冊他們的應用程式時。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-157">tooensure we are always communicating with hello right application at runtime, we ask hello developer tooprovide a custom redirectURI when registering their application with Microsoft.</span></span> <span data-ttu-id="7c5c0-158">**以下將詳細討論開發人員應該如何製作此重新導向 URI。**</span><span class="sxs-lookup"><span data-stu-id="7c5c0-158">**How developers should craft this redirect URI is discussed in detail below.**</span></span> <span data-ttu-id="7c5c0-159">這個自訂的 redirectURI 包含 hello hello 應用程式的憑證指紋，並確保 toobe 唯一 toohello 應用程式的 hello Google Play 商店。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-159">This custom redirectURI contains hello certificate thumbprint of hello application and is ensured toobe unique toohello application by hello Google Play Store.</span></span> <span data-ttu-id="7c5c0-160">當應用程式呼叫 hello broker hello broker 詢問 hello Android 作業系統 tooprovide hello 與憑證指紋該呼叫的 hello broker。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-160">When an application calls hello broker, hello broker asks hello Android operating system tooprovide it with hello certificate thumbprint that called hello broker.</span></span> <span data-ttu-id="7c5c0-161">hello broker 提供此憑證指紋 tooMicrosoft hello 呼叫 tooour 身分識別系統中。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-161">hello broker provides this certificate thumbprint tooMicrosoft in hello call tooour identity system.</span></span> <span data-ttu-id="7c5c0-162">如果在註冊期間，hello hello 應用程式的憑證指紋不符合 hello 憑證指紋的憑證提供 toous hello 開發人員，我們將會拒絕存取 toohello 語彙基元的 hello 資源 hello 應用程式要求。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-162">If hello certificate thumbprint of hello application does not match hello certificate thumbprint provided toous by hello developer during registration, we will deny access toohello tokens for hello resource hello application is requesting.</span></span> <span data-ttu-id="7c5c0-163">此檢查可確保只有 hello 開發人員所註冊的 hello 應用程式接收權杖。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-163">This check ensures that only hello application registered by hello developer receives tokens.</span></span>

<span data-ttu-id="7c5c0-164">**hello 開發人員有 hello 選擇的如果呼叫 hello broker hello Microsoft Identity SDK，或使用 hello 非 broker 協助的流程。**</span><span class="sxs-lookup"><span data-stu-id="7c5c0-164">**hello developer has hello choice of if hello Microsoft Identity SDK calls hello broker or uses hello non-broker assisted flow.**</span></span> <span data-ttu-id="7c5c0-165">不過 hello 開發人員所選擇不 toouse hello broker 輔助流程失去使用 SSO 認證的 hello 優點 hello 使用者可能已經加入 hello 裝置上，並防止他們從 Microsoft 的商務功能搭配使用的應用程式提供例如條件式存取、 Intune 管理功能，以及使用憑證式驗證其客戶。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-165">However if hello developer chooses not toouse hello broker-assisted flow they lose hello benefit of using SSO credentials that hello user may have already added on hello device and prevents their application from being used with business features Microsoft provides its customers such as Conditional Access, Intune Management capabilities, and certificate-based authentication.</span></span>

<span data-ttu-id="7c5c0-166">這些登入具有下列優點 hello:</span><span class="sxs-lookup"><span data-stu-id="7c5c0-166">These logins have hello following benefits:</span></span>

* <span data-ttu-id="7c5c0-167">使用者體驗 SSO hello 廠商無論其所有應用程式。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-167">User experiences SSO across all their applications no matter hello vendor.</span></span>
* <span data-ttu-id="7c5c0-168">您的應用程式可以使用更進階的商業功能，例如條件式存取，或使用 hello InTune 套件的產品。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-168">Your application can use more advanced business features such as Conditional Access or use hello InTune suite of products.</span></span>
* <span data-ttu-id="7c5c0-169">您的應用程式可針對商務使用者支援以憑證為基礎的驗證。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-169">Your application can support certificate-based authentication for business users.</span></span>
* <span data-ttu-id="7c5c0-170">更安全登入體驗 hello 的 hello 應用程式和 hello 使用者的身分識別會驗證 hello broker 的應用程式與其他安全性演算法和加密。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-170">Much more secure sign-in experience as hello identity of hello application and hello user are verified by hello broker application with additional security algorithms and encryption.</span></span>

<span data-ttu-id="7c5c0-171">這些登入有下列缺點 hello:</span><span class="sxs-lookup"><span data-stu-id="7c5c0-171">These logins have hello following drawbacks:</span></span>

* <span data-ttu-id="7c5c0-172">在 iOS 中已超出您的應用程式體驗轉換 hello 使用者時選擇的認證。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-172">In iOS hello user is transitioned out of your application's experience while credentials are chosen.</span></span>
* <span data-ttu-id="7c5c0-173">遺失 hello 能力 toomanage hello 登入，為您應用程式中的客戶體驗。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-173">Loss of hello ability toomanage hello login experience for your customers within your application.</span></span>

<span data-ttu-id="7c5c0-174">以下是如何 hello hello Microsoft 識別 Sdk 使用 broker 應用程式 tooenable SSO 的表示法：</span><span class="sxs-lookup"><span data-stu-id="7c5c0-174">Here is a representation of how hello Microsoft Identity SDKs work with hello broker applications tooenable SSO:</span></span>

```
+------------+ +------------+   +-------------+
|            | |            |   |             |
|   App 1    | |   App 2    |   |   Someone   |
|            | |            |   |    Else's   |
|            | |            |   |     App     |
+------------+ +------------+   +-------------+
|  ADAL SDK  | |  ADAL SDK  |   |  ADAL SDK   |
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

<span data-ttu-id="7c5c0-175">此背景資訊為利器您應該要能夠 toobetter 了解和使用 hello Microsoft 識別身分平台和 Sdk 的應用程式中實作 SSO。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-175">Armed with this background information you should be able toobetter understand and implement SSO within your application using hello Microsoft Identity platform and SDKs.</span></span>

## <a name="enabling-cross-app-sso-using-adal"></a><span data-ttu-id="7c5c0-176">使用 ADAL 啟用跨應用程式的 SSO</span><span class="sxs-lookup"><span data-stu-id="7c5c0-176">Enabling cross-app SSO using ADAL</span></span>
<span data-ttu-id="7c5c0-177">我們在此使用 ADAL 的 Android SDK hello 至：</span><span class="sxs-lookup"><span data-stu-id="7c5c0-177">Here we use hello ADAL Android SDK to:</span></span>

* <span data-ttu-id="7c5c0-178">開啟應用程式套件的非訊息代理程式協助 SSO</span><span class="sxs-lookup"><span data-stu-id="7c5c0-178">Turn on non-broker assisted SSO for your suite of apps</span></span>
* <span data-ttu-id="7c5c0-179">開啟訊息代理程式協助 SSO 的支援</span><span class="sxs-lookup"><span data-stu-id="7c5c0-179">Turn on support for broker-assisted SSO</span></span>

### <a name="turning-on-sso-for-non-broker-assisted-sso"></a><span data-ttu-id="7c5c0-180">開啟非訊息代理程式協助 SSO 的 SSO</span><span class="sxs-lookup"><span data-stu-id="7c5c0-180">Turning on SSO for non-broker assisted SSO</span></span>
<span data-ttu-id="7c5c0-181">非 broker 跨應用程式的協助 sso hello Microsoft 識別 Sdk 許多 SSO hello 複雜度為您管理。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-181">For non-broker assisted SSO across applications hello Microsoft Identity SDKs manage much of hello complexity of SSO for you.</span></span> <span data-ttu-id="7c5c0-182">這包括尋找 hello 快取中的 hello 正確的使用者和維護您 tooquery 已登入的使用者清單。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-182">This includes finding hello right user in hello cache and maintaining a list of logged in users for you tooquery.</span></span>

<span data-ttu-id="7c5c0-183">跨應用程式，您擁有需要遵循 toodo hello tooenable SSO:</span><span class="sxs-lookup"><span data-stu-id="7c5c0-183">tooenable SSO across applications you own you need toodo hello following:</span></span>

1. <span data-ttu-id="7c5c0-184">請確定所有您的應用程式使用者 hello 相同的用戶端 ID 或應用程式 id。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-184">Ensure all your applications user hello same Client ID or Application ID.</span></span>
2. <span data-ttu-id="7c5c0-185">請確定您的應用程式有相同 SharedUserID 設定的 hello。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-185">Ensure all your applications have hello same SharedUserID set.</span></span>
3. <span data-ttu-id="7c5c0-186">確保所有相同的簽章憑證，從 Google Play hello 儲存，以便您可以使用共用儲存體您的應用程式共用 hello。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-186">Ensure that all of your applications share hello same signing certificate from hello Google Play store so that you can share storage.</span></span>

#### <a name="step-1-using-hello-same-client-id--application-id-for-all-hello-applications-in-your-suite-of-apps"></a><span data-ttu-id="7c5c0-187">步驟 1： 使用 hello 相同的用戶端識別碼 / 應用程式 ID 的所有 hello 您的應用程式套件中的應用程式</span><span class="sxs-lookup"><span data-stu-id="7c5c0-187">Step 1: Using hello same Client ID / Application ID for all hello applications in your suite of apps</span></span>
<span data-ttu-id="7c5c0-188">為了讓 hello Microsoft 身分識別平台 tooknow 跨應用程式允許 tooshare 語彙基元，每個應用程式需要 tooshare hello 相同的用戶端 ID 或應用程式 id。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-188">In order for hello Microsoft Identity platform tooknow that it's allowed tooshare tokens across your applications, each of your applications will need tooshare hello same Client ID or Application ID.</span></span> <span data-ttu-id="7c5c0-189">這是 hello tooyou hello 入口網站中註冊您的第一個應用程式時提供的唯一識別碼。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-189">This is hello unique identifier that was provided tooyou when you registered your first application in hello portal.</span></span>

<span data-ttu-id="7c5c0-190">您可能想知道識別不同的應用程式的方式 toohello Microsoft 的身分識別服務，如果它使用 hello 相同應用程式識別碼。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-190">You may be wondering how you will identify different apps toohello Microsoft Identity service if it uses hello same Application ID.</span></span> <span data-ttu-id="7c5c0-191">hello 回應是以 hello**重新導向 Uri**。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-191">hello answer is with hello **Redirect URIs**.</span></span> <span data-ttu-id="7c5c0-192">每個應用程式可以有多個重新導向 Uri hello 登入入口網站中註冊。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-192">Each application can have multiple Redirect URIs registered in hello onboarding portal.</span></span> <span data-ttu-id="7c5c0-193">組件中的每個應用程式將會有不同的重新導向 URI。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-193">Each app in your suite will have a different redirect URI.</span></span> <span data-ttu-id="7c5c0-194">其外觀的範例如下：</span><span class="sxs-lookup"><span data-stu-id="7c5c0-194">An example of how this looks is below:</span></span>

<span data-ttu-id="7c5c0-195">App1 重新導向 URI： `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span><span class="sxs-lookup"><span data-stu-id="7c5c0-195">App1 Redirect URI: `msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D`</span></span>

<span data-ttu-id="7c5c0-196">App2 重新導向 URI： `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span><span class="sxs-lookup"><span data-stu-id="7c5c0-196">App2 Redirect URI: `msauth://com.example.userapp1/KmB7PxIytyLkbGHuI%2UitkW%2Fejk%4E`</span></span>

<span data-ttu-id="7c5c0-197">App3 重新導向 URI： `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span><span class="sxs-lookup"><span data-stu-id="7c5c0-197">App3 Redirect URI: `msauth://com.example.userapp2/Pt85PxIyvbLkbKUtBI%2SitkW%2Fejk%9F`</span></span>

<span data-ttu-id="7c5c0-198">....</span><span class="sxs-lookup"><span data-stu-id="7c5c0-198">....</span></span>

<span data-ttu-id="7c5c0-199">這些之下巢狀 hello 相同的用戶端識別碼 / 應用程式識別碼和查閱根據的 hello 重新導向的 URI 傳回 toous SDK 組態中。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-199">These are nested under hello same client ID / application ID and looked up based on hello redirect URI you return toous in your SDK configuration.</span></span>

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


<span data-ttu-id="7c5c0-200">*請注意，hello 這些重新導向 Uri 的格式說明如下。除非您希望 toosupport hello broker，您便可以使用任何重新導向 URI，在此情況下它們必須看起來像上述 hello*</span><span class="sxs-lookup"><span data-stu-id="7c5c0-200">*Note that hello format of these Redirect URIs are explained below. You may use any Redirect URI unless you wish toosupport hello broker, in which case they must look something like hello above*</span></span>

#### <a name="step-2-configuring-shared-storage-in-android"></a><span data-ttu-id="7c5c0-201">步驟 2︰在 Android 中設定共用儲存體</span><span class="sxs-lookup"><span data-stu-id="7c5c0-201">Step 2: Configuring shared storage in Android</span></span>
<span data-ttu-id="7c5c0-202">設定 hello`SharedUserID`已超出本文件 hello 範圍，但是可以透過讀取 hello hello Google Android 文件取得[資訊清單](http://developer.android.com/guide/topics/manifest/manifest-element.html)。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-202">Setting hello `SharedUserID` is beyond hello scope of this document but can be learned by reading hello Google Android documentation on hello [Manifest](http://developer.android.com/guide/topics/manifest/manifest-element.html).</span></span> <span data-ttu-id="7c5c0-203">您必須決定 sharedUserID 的名稱，並且跨所有的應用程式使用該名稱。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-203">What is important is that you decide what you want your sharedUserID will be called and use that across all your applications.</span></span>

<span data-ttu-id="7c5c0-204">一旦您擁有 hello`SharedUserID`在所有的應用程式中，您是準備 toouse SSO。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-204">Once you have hello `SharedUserID` in all your applications you are ready toouse SSO.</span></span>

> [!WARNING]
> <span data-ttu-id="7c5c0-205">當您跨應用程式共用儲存體的任何應用程式可以刪除使用者或更糟的是整個應用程式中刪除所有 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-205">When you share storage across your applications any application can delete users, or worse delete all hello tokens across your application.</span></span> <span data-ttu-id="7c5c0-206">這是特別而言，如果您擁有 hello 語彙基元 toodo 背景工作所依賴的應用程式。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-206">This is particularly disastrous if you have applications that rely on hello tokens toodo background work.</span></span> <span data-ttu-id="7c5c0-207">共用儲存體表示，您必須非常小心移除所有作業，透過 hello Microsoft 識別 Sdk 中。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-207">Sharing storage means that you must be very careful in any and all remove operations through hello Microsoft Identity SDKs.</span></span>
> 
> 

<span data-ttu-id="7c5c0-208">就這麼簡單！</span><span class="sxs-lookup"><span data-stu-id="7c5c0-208">That's it!</span></span> <span data-ttu-id="7c5c0-209">hello Microsoft Identity SDK 現在會跨所有應用程式共用認證。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-209">hello Microsoft Identity SDK will now share credentials across all your applications.</span></span> <span data-ttu-id="7c5c0-210">hello 使用者清單也會在應用程式執行個體之間共用。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-210">hello user list will also be shared across application instances.</span></span>

### <a name="turning-on-sso-for-broker-assisted-sso"></a><span data-ttu-id="7c5c0-211">開啟訊息代理程式協助 SSO 的 SSO</span><span class="sxs-lookup"><span data-stu-id="7c5c0-211">Turning on SSO for broker assisted SSO</span></span>
<span data-ttu-id="7c5c0-212">hello hello 裝置上安裝任何 broker 應用程式 toouse 能力**預設關閉**。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-212">hello ability for an application toouse any broker that is installed on hello device is **turned off by default**.</span></span> <span data-ttu-id="7c5c0-213">若要 toouse 您的應用程式使用 hello broker，您必須執行一些額外的設定並新增一些程式碼 tooyour 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-213">In order toouse your application with hello broker you must do some additional configuration and add some code tooyour application.</span></span>

<span data-ttu-id="7c5c0-214">hello 步驟 toofollow 如下：</span><span class="sxs-lookup"><span data-stu-id="7c5c0-214">hello steps toofollow are:</span></span>

1. <span data-ttu-id="7c5c0-215">啟用您的應用程式程式碼呼叫 toohello MS SDK 中的 broker 模式</span><span class="sxs-lookup"><span data-stu-id="7c5c0-215">Enable broker mode in your application code's call toohello MS SDK</span></span>
2. <span data-ttu-id="7c5c0-216">建立新的重新導向 URI，並提供該 tooboth hello 應用程式和應用程式註冊</span><span class="sxs-lookup"><span data-stu-id="7c5c0-216">Establish a new redirect URI and provide that tooboth hello app and your app registration</span></span>
3. <span data-ttu-id="7c5c0-217">設定 hello hello Android 資訊清單中的正確權限</span><span class="sxs-lookup"><span data-stu-id="7c5c0-217">Setting up hello correct permissions in hello Android manifest</span></span>

#### <a name="step-1-enable-broker-mode-in-your-application"></a><span data-ttu-id="7c5c0-218">步驟 1︰在應用程式中啟用訊息代理程式模式</span><span class="sxs-lookup"><span data-stu-id="7c5c0-218">Step 1: Enable broker mode in your application</span></span>
<span data-ttu-id="7c5c0-219">您的應用程式 toouse hello broker hello 能力時，會開啟您建立 hello 「 設定 」 或驗證執行個體的初始設定。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-219">hello ability for your application toouse hello broker is turned on when you create hello "settings" or initial setup of your Authentication instance.</span></span> <span data-ttu-id="7c5c0-220">您可以設定程式碼中的 ApplicationSettings 類型就可以辦到︰</span><span class="sxs-lookup"><span data-stu-id="7c5c0-220">You do this by setting your ApplicationSettings type in your code:</span></span>

```
AuthenticationSettings.Instance.setUseBroker(true);
```


#### <a name="step-2-establish-a-new-redirect-uri-with-your-url-scheme"></a><span data-ttu-id="7c5c0-221">步驟 2︰利用 URL 配置建立新的重新導向 URI</span><span class="sxs-lookup"><span data-stu-id="7c5c0-221">Step 2: Establish a new redirect URI with your URL Scheme</span></span>
<span data-ttu-id="7c5c0-222">中，我們一律會傳回 hello 認證權杖 toohello 正確的應用程式的順序 tooensure，我們需要確定我們回撥 tooyour hello Android 作業系統的方式的應用程式可以驗證 toomake。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-222">In order tooensure that we always return hello credential tokens toohello correct application, we need toomake sure we call back tooyour application in a way that hello Android operating system can verify.</span></span> <span data-ttu-id="7c5c0-223">Android 作業系統 hello 使用 hello Google Play 商店中的 hello hello 憑證雜湊。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-223">hello Android operating system uses hello hash of hello certificate in hello Google Play store.</span></span> <span data-ttu-id="7c5c0-224">這樣就不會讓惡意應用程式假冒。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-224">This cannot be spoofed by a rogue application.</span></span> <span data-ttu-id="7c5c0-225">因此，我們會利用這以及 hello 我們 broker 應用程式 tooensure hello 權杖會傳回 toohello 正確的應用程式的 URI。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-225">Therefore, we leverage this along with hello URI of our broker application tooensure that hello tokens are returned toohello correct application.</span></span> <span data-ttu-id="7c5c0-226">我們需要您 tooestablish 此唯一的重新導向 URI，在您的應用程式和設定為重新導向 URI 的我們的開發人員入口網站。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-226">We require you tooestablish this unique redirect URI both in your application and set as a Redirect URI in our developer portal.</span></span>

<span data-ttu-id="7c5c0-227">Hello 的適當的格式必須為您重新導向 URI:</span><span class="sxs-lookup"><span data-stu-id="7c5c0-227">Your redirect URI must be in hello proper form of:</span></span>

`msauth://packagename/Base64UrlencodedSignature`

<span data-ttu-id="7c5c0-228">例如：msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D</span><span class="sxs-lookup"><span data-stu-id="7c5c0-228">ex: *msauth://com.example.userapp/IcB5PxIyvbLkbFVtBI%2FitkW%2Fejk%3D*</span></span>

<span data-ttu-id="7c5c0-229">此重新導向 URI 必須指定在您的應用程式註冊使用 hello toobe [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-229">This Redirect URI needs toobe specified in your app registration using hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="7c5c0-230">如需 Azure AD 應用程式註冊的詳細資訊，請參閱 [與 Azure Active Directory 整合](active-directory-how-to-integrate.md)。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-230">For more information on Azure AD app registration, see [Integrating with Azure Active Directory](active-directory-how-to-integrate.md).</span></span>

#### <a name="step-3-set-up-hello-correct-permissions-in-your-application"></a><span data-ttu-id="7c5c0-231">步驟 3： 設定您的應用程式中的 hello 正確權限</span><span class="sxs-lookup"><span data-stu-id="7c5c0-231">Step 3: Set up hello correct permissions in your application</span></span>
<span data-ttu-id="7c5c0-232">我們 broker 的應用程式在 Android 中跨應用程式使用 hello 的 hello Android OS toomanage 認證的帳戶管理員功能。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-232">Our broker application in Android uses hello Accounts Manager feature of hello Android OS toomanage credentials across applications.</span></span> <span data-ttu-id="7c5c0-233">在 Android 中的順序 toouse hello broker 您應用程式資訊清單必須有權限 toouse AccountManager 帳戶。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-233">In order toouse hello broker in Android your app manifest must have permissions toouse AccountManager accounts.</span></span> <span data-ttu-id="7c5c0-234">這在 hello 中詳細討論[Google 文件的帳戶管理員](http://developer.android.com/reference/android/accounts/AccountManager.html)</span><span class="sxs-lookup"><span data-stu-id="7c5c0-234">This is discussed in detail in hello [Google documentation for Account Manager here](http://developer.android.com/reference/android/accounts/AccountManager.html)</span></span>

<span data-ttu-id="7c5c0-235">特別是以下這些權限︰</span><span class="sxs-lookup"><span data-stu-id="7c5c0-235">In particular, these permissions are:</span></span>

```
GET_ACCOUNTS
USE_CREDENTIALS
MANAGE_ACCOUNTS
```

### <a name="youve-configured-sso"></a><span data-ttu-id="7c5c0-236">您已設定 SSO！</span><span class="sxs-lookup"><span data-stu-id="7c5c0-236">You've configured SSO!</span></span>
<span data-ttu-id="7c5c0-237">現在 hello Microsoft Identity SDK 會自動同時在您的應用程式之間共用的認證並叫用 hello broker 是否出現在其裝置上。</span><span class="sxs-lookup"><span data-stu-id="7c5c0-237">Now hello Microsoft Identity SDK will automatically both share credentials across your applications and invoke hello broker if it's present on their device.</span></span>

