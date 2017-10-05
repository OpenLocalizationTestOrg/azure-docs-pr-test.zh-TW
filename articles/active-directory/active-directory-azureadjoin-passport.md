---
title: "透過 Windows Hello 企業版和 Azure AD 不需要密碼就能驗證身分識別 | Microsoft Docs"
description: "提供 Windows Hello 企業版概觀以及部署 Windows Hello 企業版的其他資訊。"
services: active-directory
documentationcenter: 
author: femila
manager: femila
editor: 
tags: azure-classic-portal
ms.assetid: f907bb90-8776-46ca-9e12-279949af66ff
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/16/2017
ms.author: markvi
ms.openlocfilehash: 62adf8a9fd4400a056e2c0f59c79431acbad5865
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="authenticating-identities-without-passwords-through-windows-hello-for-business"></a><span data-ttu-id="3f603-103">透過 Windows Hello 企業版不需要密碼就能驗證身分識別</span><span class="sxs-lookup"><span data-stu-id="3f603-103">Authenticating identities without passwords through Windows Hello for Business</span></span>
<span data-ttu-id="3f603-104">目前單獨驗證密碼的方法不足以保障使用者的安全。</span><span class="sxs-lookup"><span data-stu-id="3f603-104">The current methods of authentication with passwords alone are not sufficient to keep users safe.</span></span> <span data-ttu-id="3f603-105">使用者會重複使用和忘記密碼。</span><span class="sxs-lookup"><span data-stu-id="3f603-105">Users reuse and forget passwords.</span></span> <span data-ttu-id="3f603-106">密碼是可破壞、可進行網路釣魚、易於破解且可猜測的。</span><span class="sxs-lookup"><span data-stu-id="3f603-106">Passwords are breachable, phishable, prone to cracks, and guessable.</span></span> <span data-ttu-id="3f603-107">密碼也很難記住，而且易於遭受攻擊，例如「[傳送雜湊](https://technet.microsoft.com/dn785092.aspx)」。</span><span class="sxs-lookup"><span data-stu-id="3f603-107">They also get difficult to remember and prone to attacks like “[pass the hash](https://technet.microsoft.com/dn785092.aspx)”.</span></span>

## <a name="about-windows-hello-for-business"></a><span data-ttu-id="3f603-108">關於 Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="3f603-108">About Windows Hello for Business</span></span>
<span data-ttu-id="3f603-109">對於組織和取用者來說，Windows Hello 企業版是超越密碼的私密金鑰/公開金鑰或憑證式驗證方法。</span><span class="sxs-lookup"><span data-stu-id="3f603-109">Windows Hello for Business is a private/public key or certificate-based authentication approach for organizations and consumers that goes beyond passwords.</span></span> <span data-ttu-id="3f603-110">這種形式的驗證依賴金鑰組認證，其可取代密碼且能抵抗漏洞、竊取及網路釣魚。</span><span class="sxs-lookup"><span data-stu-id="3f603-110">This form of authentication relies on  key pair credentials that can replace passwords and are resistant to breaches, thefts, and phishing.</span></span>

 <span data-ttu-id="3f603-111">Windows Hello 企業版讓使用者能夠向 Microsoft 帳戶、Windows Server Active Directory 帳戶、Microsoft Azure Active Directory (Azure AD) 帳戶或支援 Fast IDentity Online (FIDO) 驗證的非 Microsoft 服務進行驗證。</span><span class="sxs-lookup"><span data-stu-id="3f603-111">Windows Hello for Business lets a user authenticate to a Microsoft account, a Windows Server Active Directory account, a Microsoft Azure Active Directory (Azure AD) account, or a non-Microsoft service that supports Fast IDentity Online (FIDO) authentication.</span></span> <span data-ttu-id="3f603-112">在 Windows Hello 企業版註冊期間進行最初的兩步驟驗證之後，就會在使用者的裝置上設定 Windows Hello 企業版，而該使用者需設定一個手勢，可能是 Windows Hello 或 PIN。</span><span class="sxs-lookup"><span data-stu-id="3f603-112">After an initial two-step verification during Windows Hello for Business enrollment, Windows Hello for Business is set up on the user's device, and the user sets a gesture, which can be Windows Hello or a PIN.</span></span> <span data-ttu-id="3f603-113">使用者會提供該手勢來驗證其身分識別。</span><span class="sxs-lookup"><span data-stu-id="3f603-113">The user provides the gesture to verify their identity.</span></span> <span data-ttu-id="3f603-114">Windows 接著會使用 Windows Hello 企業版來驗證使用者，並協助他們存取受保護的資源和服務。</span><span class="sxs-lookup"><span data-stu-id="3f603-114">Windows then uses Windows Hello for Business to authenticate the user and help them to access protected resources and services.</span></span>

<span data-ttu-id="3f603-115">私密金鑰可以透過「使用者手勢」單獨使用，例如，PIN、生物識別技術、遠端裝置 (像是使用者用來登入裝置的智慧卡)。</span><span class="sxs-lookup"><span data-stu-id="3f603-115">The private key is made available solely through a “user gesture” like a PIN, biometrics, or a remote device like a smart card that the user uses to sign in to the device.</span></span> <span data-ttu-id="3f603-116">此資訊會連結到憑證或非對稱式金鑰組。</span><span class="sxs-lookup"><span data-stu-id="3f603-116">This information is linked to a certificate or an asymmetrical key pair.</span></span> <span data-ttu-id="3f603-117">如果裝置具備信賴平台模組 (TPM) 晶片，此私密金鑰就已通過硬體證明。</span><span class="sxs-lookup"><span data-stu-id="3f603-117">The private key is hardware attested if the device has a Trusted Platform Module (TPM) chip.</span></span> <span data-ttu-id="3f603-118">私密金鑰永遠都不會離開裝置。</span><span class="sxs-lookup"><span data-stu-id="3f603-118">The private key never leaves the device.</span></span>

<span data-ttu-id="3f603-119">公開金鑰是使用 Azure Active Directory 和 Windows Server Active Directory (適用於內部部署) 進行登錄。</span><span class="sxs-lookup"><span data-stu-id="3f603-119">The public key is registered with Azure Active Directory and Windows Server Active Directory (for on-premises).</span></span> <span data-ttu-id="3f603-120">身分識別提供者 (IDP) 會藉由將使用者的公開金鑰對應到私密金鑰來驗證該使用者，並透過單次密碼 (OTP)、PhoneFactor 或不同的通知機制來提供登入資訊。</span><span class="sxs-lookup"><span data-stu-id="3f603-120">Identity Providers (IDPs) validate the user by mapping the public key of the user to the private key, and provide sign-in information through One Time Password (OTP), PhoneFactor, or a different notification mechanism.</span></span>

## <a name="why-enterprises-should-adopt-windows-hello-for-business"></a><span data-ttu-id="3f603-121">為什麼企業應該採用 Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="3f603-121">Why enterprises should adopt Windows Hello for Business</span></span>
<span data-ttu-id="3f603-122">藉由啟用 Windows Hello 企業版，企業可透過下列動作，使其資源更安全：</span><span class="sxs-lookup"><span data-stu-id="3f603-122">By enabling Windows Hello for Business, enterprises can make their resources even more secure by:</span></span>

* <span data-ttu-id="3f603-123">使用硬體慣用選項來設定 Windows Hello 企業版。</span><span class="sxs-lookup"><span data-stu-id="3f603-123">Setting up Windows Hello for Business with a hardware-preferred option.</span></span> <span data-ttu-id="3f603-124">這表示將會在可用時於 TPM 1.2 或 TPM 2.0 上產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="3f603-124">This means that keys will be generated on TPM 1.2 or TPM 2.0 when available.</span></span> <span data-ttu-id="3f603-125">無法使用 TPM 時，軟體將會產生金鑰。</span><span class="sxs-lookup"><span data-stu-id="3f603-125">When TPM is not available, software will generate the key.</span></span>
* <span data-ttu-id="3f603-126">定義 PIN 的複雜度和長度，以及是否要在組織中啟用 Hello 使用方式。</span><span class="sxs-lookup"><span data-stu-id="3f603-126">Defining the complexity and length of the PIN, and whether Hello usage is enabled in your organization.</span></span>
* <span data-ttu-id="3f603-127">設定 Windows Hello 企業版，使用憑證式信任來支援類似智慧卡的案例。</span><span class="sxs-lookup"><span data-stu-id="3f603-127">Configuring Windows Hello for Business to support smart card-like scenarios by using certificate-based trust.</span></span>

## <a name="how-windows-hello-for-business-works"></a><span data-ttu-id="3f603-128">Windows Hello 企業版的運作方式</span><span class="sxs-lookup"><span data-stu-id="3f603-128">How Windows Hello for Business works</span></span>
1. <span data-ttu-id="3f603-129">金鑰是在硬體上由 TPM 或軟體所產生。</span><span class="sxs-lookup"><span data-stu-id="3f603-129">Keys are generated on the hardware by TPM or software.</span></span> <span data-ttu-id="3f603-130">許多裝置都會內建 TPM 晶片，藉由將密碼編譯金鑰整合到裝置來保護硬體。</span><span class="sxs-lookup"><span data-stu-id="3f603-130">Many devices have a built-in TPM chip that secures the hardware by integrating cryptographic keys into devices.</span></span> <span data-ttu-id="3f603-131">TPM 1.2 或 TPM 2.0 會產生金鑰或是從產生的金鑰建立的憑證。</span><span class="sxs-lookup"><span data-stu-id="3f603-131">TPM 1.2 or TPM 2.0 generates keys or certificates that are created from the generated keys.</span></span>
2. <span data-ttu-id="3f603-132">TPM 會證明這些硬體繫結的金鑰。</span><span class="sxs-lookup"><span data-stu-id="3f603-132">The TPM attests these hardware-bound keys.</span></span>
3. <span data-ttu-id="3f603-133">單一解除鎖定手勢會解除鎖定裝置。</span><span class="sxs-lookup"><span data-stu-id="3f603-133">A single unlock gesture unlocks the device.</span></span> <span data-ttu-id="3f603-134">如果裝置已加入網域或已加入 Azure AD，則此手勢能夠存取多個資源。</span><span class="sxs-lookup"><span data-stu-id="3f603-134">This gesture allows access to multiple resources if the device is domain-joined or Azure AD-joined.</span></span>

## <a name="how-the-windows-hello-for-business-lifecycle-works"></a><span data-ttu-id="3f603-135">Windows Hello 企業版生命週期的運作方式</span><span class="sxs-lookup"><span data-stu-id="3f603-135">How the Windows Hello for Business lifecycle works</span></span>
![Windows Hello 企業版生命週期](./media/active-directory-azureadjoin/active-directory-azureadjoin-microsoft-passport.png)

<span data-ttu-id="3f603-137">上圖說明私密/公開金鑰組，以及身分識別提供者所提供的驗證。</span><span class="sxs-lookup"><span data-stu-id="3f603-137">The preceding diagram illustrates the private/public key pair and the validation by the identity provider.</span></span> <span data-ttu-id="3f603-138">以下將詳細說明每個步驟：</span><span class="sxs-lookup"><span data-stu-id="3f603-138">Each of these steps is explained in detail here:</span></span>

1. <span data-ttu-id="3f603-139">使用者透過多個內建校訂方法 (手勢、實體智慧卡、多重要素驗證) 證明其身分識別，並將此資訊傳送到類似 Azure Active Directory 或內部部署 Active Directory 的身分識別提供者 (IDP)。</span><span class="sxs-lookup"><span data-stu-id="3f603-139">The user proves their identity through multiple built-in proofing methods (gestures, physical smart cards, multi-factor authentication) and sends this information to an Identity Provider (IDP) like Azure Active Directory or on-premises Active Directory.</span></span>
2. <span data-ttu-id="3f603-140">裝置接著會建立金鑰、證明金鑰、接受此金鑰的公開部分、為其附加站台聲明、登入並傳送至 IDP 以登錄此金鑰。</span><span class="sxs-lookup"><span data-stu-id="3f603-140">The device then creates the key, attests the key, takes the public portion of this key, attaches it with station statements, signs in, and sends it to the IDP to register the key.</span></span>
3. <span data-ttu-id="3f603-141">一旦 IDP 登錄金鑰的公開部分之後，IDP 就會要求裝置使用金鑰的私密部分進行簽署。</span><span class="sxs-lookup"><span data-stu-id="3f603-141">As soon as the IDP registers the public portion of the key, the IDP challenges the device to sign with the private portion of the key.</span></span>
4. <span data-ttu-id="3f603-142">IDP 接著會驗證並發出驗證權杖，讓使用者和裝置能夠存取受保護的資源。</span><span class="sxs-lookup"><span data-stu-id="3f603-142">The IDP then validates and issues the authentication token that lets the user and the device access the protected resources.</span></span> <span data-ttu-id="3f603-143">IDP 可以撰寫跨平台的應用程式，或者透過 JavaScript/Webcrypto API 使用瀏覽器支援，為其使用者建立和使用 Windows Hello 企業版認證。</span><span class="sxs-lookup"><span data-stu-id="3f603-143">IDPs can write cross-platform apps or use browser support (via JavaScript/Webcrypto APIs) to create and use Windows Hello for Business credentials for their users.</span></span>

## <a name="the-deployment-requirements-for-windows-hello-for-business"></a><span data-ttu-id="3f603-144">Windows Hello 企業版的部署需求</span><span class="sxs-lookup"><span data-stu-id="3f603-144">The deployment requirements for Windows Hello for Business</span></span>
### <a name="at-the-enterprise-level"></a><span data-ttu-id="3f603-145">在企業層級</span><span class="sxs-lookup"><span data-stu-id="3f603-145">At the enterprise level</span></span>
* <span data-ttu-id="3f603-146">企業擁有 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3f603-146">The enterprise has an Azure subscription.</span></span>

### <a name="at-the-user-level"></a><span data-ttu-id="3f603-147">在使用者層級</span><span class="sxs-lookup"><span data-stu-id="3f603-147">At the user level</span></span>
* <span data-ttu-id="3f603-148">使用者的電腦執行 Windows 10 專業版或企業版。</span><span class="sxs-lookup"><span data-stu-id="3f603-148">The user's computer runs Windows 10 Professional or Enterprise.</span></span>

<span data-ttu-id="3f603-149">如需部署指示的詳細資訊，請參閱[在組織中啟用 Windows Hello 企業版](active-directory-azureadjoin-passport-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="3f603-149">For detailed deployment instructions, see [Enable Windows Hello for Business in the organization](active-directory-azureadjoin-passport-deployment.md).</span></span>

## <a name="additional-information"></a><span data-ttu-id="3f603-150">其他資訊</span><span class="sxs-lookup"><span data-stu-id="3f603-150">Additional information</span></span>
* [<span data-ttu-id="3f603-151">適合企業使用的 Windows 10：使用裝置工作的方式</span><span class="sxs-lookup"><span data-stu-id="3f603-151">Windows 10 for the enterprise: Ways to use devices for work</span></span>](active-directory-azureadjoin-windows10-devices-overview.md)
* [<span data-ttu-id="3f603-152">透過 Azure Active Directory Join 擴充 Windows 10 裝置的雲端功能</span><span class="sxs-lookup"><span data-stu-id="3f603-152">Extending cloud capabilities to Windows 10 devices through Azure Active Directory Join</span></span>](active-directory-azureadjoin-user-upgrade.md)
* [<span data-ttu-id="3f603-153">了解適用於 Azure AD Join 的使用案例</span><span class="sxs-lookup"><span data-stu-id="3f603-153">Learn about usage scenarios for Azure AD Join</span></span>](active-directory-azureadjoin-deployment-aadjoindirect.md)
* [<span data-ttu-id="3f603-154">將已加入網域裝置連接到 Azure AD 以體驗 Windows 10</span><span class="sxs-lookup"><span data-stu-id="3f603-154">Connect domain-joined devices to Azure AD for Windows 10 experiences</span></span>](active-directory-azureadjoin-devices-group-policy.md)
* [<span data-ttu-id="3f603-155">設定 Azure AD Join</span><span class="sxs-lookup"><span data-stu-id="3f603-155">Set up Azure AD Join</span></span>](active-directory-azureadjoin-setup.md)

