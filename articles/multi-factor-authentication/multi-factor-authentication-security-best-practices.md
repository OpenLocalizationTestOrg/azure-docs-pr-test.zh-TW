---
title: "MFA 的安全性最佳做法 | Microsoft Docs"
description: "本文件提供搭配 Azure 帳戶使用 Azure MFA 的最佳做法"
services: multi-factor-authentication
documentationcenter: 
author: kgremban
manager: femila
ms.assetid: 3be7d968-96bb-4320-8701-869fd04a2595
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2017
ms.author: kgremban
ms.reviewer: yossib
ms.custom: it-pro
ms.openlocfilehash: f43f6e33976325920da9cf0f6aef6decae5bde26
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="security-best-practices-for-using-azure-multi-factor-authentication-with-azure-ad-accounts"></a><span data-ttu-id="eb22f-103">搭配 Azure AD 帳戶使用 Azure Multi-Factor Authentication 的安全性最佳做法</span><span class="sxs-lookup"><span data-stu-id="eb22f-103">Security Best Practices for using Azure Multi-Factor Authentication with Azure AD accounts</span></span>

<span data-ttu-id="eb22f-104">對於想要加強驗證程序的大多數組織而言，雙步驟驗證是首選。</span><span class="sxs-lookup"><span data-stu-id="eb22f-104">Two-step verification is the preferred choice for most organizations that want to enhance their authentication process.</span></span> <span data-ttu-id="eb22f-105">Azure Multi-Factor Authentication (MFA) 協助公司符合其安全性和合規性需求，同時為使用者提供簡單的登入體驗。</span><span class="sxs-lookup"><span data-stu-id="eb22f-105">Azure Multi-Factor Authentication (MFA) helps companies meet their security and compliance requirements while providing a simple sign-in experience for their users.</span></span> <span data-ttu-id="eb22f-106">本文涵蓋一些您在規劃採用 Azure MFA 時應該考慮的祕訣。</span><span class="sxs-lookup"><span data-stu-id="eb22f-106">This article covers some tips that you should consider when planning for the adoption of Azure MFA.</span></span>

## <a name="deploy-azure-mfa-in-the-cloud"></a><span data-ttu-id="eb22f-107">在雲端部署 Azure MFA</span><span class="sxs-lookup"><span data-stu-id="eb22f-107">Deploy Azure MFA in the cloud</span></span>

<span data-ttu-id="eb22f-108">有兩種方式可以為所有使用者啟用 Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="eb22f-108">There are two ways to enable Azure MFA for all your users.</span></span>

* <span data-ttu-id="eb22f-109">為每個使用者購買授權 (Azure MFA、Azure AD Premium 或 Enterprise Mobility + Security)</span><span class="sxs-lookup"><span data-stu-id="eb22f-109">Buy licenses for each user (Either Azure MFA, Azure AD Premium, or Enterprise Mobility + Security)</span></span>
* <span data-ttu-id="eb22f-110">建立 Multi-Factor Auth Provider，並依每個使用者或每次驗證付費</span><span class="sxs-lookup"><span data-stu-id="eb22f-110">Create a Multi-Factor Auth Provider and pay per-user or per-authentication</span></span>

### <a name="licenses"></a><span data-ttu-id="eb22f-111">授權</span><span class="sxs-lookup"><span data-stu-id="eb22f-111">Licenses</span></span>
![EMS](./media/multi-factor-authentication-security-best-practices/ems.png)

<span data-ttu-id="eb22f-113">如果您有 Azure AD Premium 或 Enterprise Mobility + Security 授權，則您已經有 Azure MFA。</span><span class="sxs-lookup"><span data-stu-id="eb22f-113">If you have Azure AD Premium or Enterprise Mobility + Security licenses, you already have Azure MFA.</span></span> <span data-ttu-id="eb22f-114">您的組織不需要任何其他項目，即可將雙步驟驗證功能延伸到所有使用者。</span><span class="sxs-lookup"><span data-stu-id="eb22f-114">Your organization doesn't need anything additional to extend the two-step verification capability to all users.</span></span> <span data-ttu-id="eb22f-115">您只需要將授權指派給使用者，接著就可以開啟 MFA。</span><span class="sxs-lookup"><span data-stu-id="eb22f-115">You only need to assign a license to a user, and then you can turn on MFA.</span></span>

<span data-ttu-id="eb22f-116">設定 Multi-Factor Authentication 時，請考慮下列訣竅：</span><span class="sxs-lookup"><span data-stu-id="eb22f-116">When setting up Multi-Factor Authentication, consider the following tips:</span></span>

* <span data-ttu-id="eb22f-117">不要建立依每次驗證的 Multi-Factor Auth Provider。</span><span class="sxs-lookup"><span data-stu-id="eb22f-117">Do not create a per-authentication Multi-Factor Auth Provider.</span></span> <span data-ttu-id="eb22f-118">如果這麼做，您可能因為已有授權的使用者提出驗證要求而需要付費。</span><span class="sxs-lookup"><span data-stu-id="eb22f-118">If you do, you could end up paying for verification requests from users that already have licenses.</span></span>
* <span data-ttu-id="eb22f-119">如果您沒有足夠的授權給所有使用者，您可以建立依每個使用者的 Multi-Factor Auth Provider，以涵蓋組織的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="eb22f-119">If you don't have enough licenses for all your users, you can create a per-user Multi-Factor Auth Provider to cover the rest of your organization.</span></span> 
* <span data-ttu-id="eb22f-120">唯有當您將內部部署 Active Directory 環境與 Azure AD 目錄同步處理時，才需要 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="eb22f-120">Azure AD Connect is only required if you are synchronizing your on-premises Active Directory environment with an Azure AD directory.</span></span> <span data-ttu-id="eb22f-121">如果您使用不與內部部署 Active Directory 執行個體同步處理的 Azure AD 目錄，就不需要 Azure AD Connect。</span><span class="sxs-lookup"><span data-stu-id="eb22f-121">If you use an Azure AD directory that is not synchronized with an on-premises instance of Active Directory, you do not need Azure AD Connect.</span></span>

### <a name="multi-factor-auth-provider"></a><span data-ttu-id="eb22f-122">Multi-Factor Auth Provider</span><span class="sxs-lookup"><span data-stu-id="eb22f-122">Multi-Factor Auth Provider</span></span>
![Multi-Factor Auth Provider](./media/multi-factor-authentication-security-best-practices/authprovider.png)

<span data-ttu-id="eb22f-124">如果沒有包含 Azure MFA 的授權，您可以建立 MFA 驗證提供者。</span><span class="sxs-lookup"><span data-stu-id="eb22f-124">If you don't have licenses that include Azure MFA, then you can create an MFA Auth Provider.</span></span> 

<span data-ttu-id="eb22f-125">建立 Auth Provider 時，您必須選取目錄並考慮下列詳細資料：</span><span class="sxs-lookup"><span data-stu-id="eb22f-125">When creating the Auth Provider, you need to select a directory and consider the following details:</span></span>

* <span data-ttu-id="eb22f-126">您不需要 Azure AD 目錄即可建立多因素驗證提供者，但如果有則可以獲得更多功能。</span><span class="sxs-lookup"><span data-stu-id="eb22f-126">You do not need an Azure AD directory to create a Multi-Factor Auth Provider, but you get more functionality with one.</span></span> <span data-ttu-id="eb22f-127">將驗證提供者與 Azure AD 目錄相關聯時，將會啟用下列功能︰</span><span class="sxs-lookup"><span data-stu-id="eb22f-127">The following features are enabled when you associate the Auth Provider with an Azure AD directory:</span></span>  
  * <span data-ttu-id="eb22f-128">將雙步驟驗證延伸到所有使用者</span><span class="sxs-lookup"><span data-stu-id="eb22f-128">Extend two-step verification to all your users</span></span>  
  * <span data-ttu-id="eb22f-129">將其他功能提供給全域管理員，例如管理入口網站、自訂問候語和報告。</span><span class="sxs-lookup"><span data-stu-id="eb22f-129">Offer your global administrators additional features, such as the management portal, custom greetings, and reports.</span></span>
* <span data-ttu-id="eb22f-130">如果您將內部部署 Active Directory 環境與 Azure AD 目錄同步處理，則需要 DirSync 或 AAD Sync。</span><span class="sxs-lookup"><span data-stu-id="eb22f-130">If you synchronize your on-premises Active Directory environment with an Azure AD directory, you need DirSync or AAD Sync.</span></span> <span data-ttu-id="eb22f-131">如果您使用不與內部部署 Active Directory 執行個體同步處理的 Azure AD 目錄，就不需要 DirSync 或 AAD Sync。</span><span class="sxs-lookup"><span data-stu-id="eb22f-131">If you use an Azure AD directory that is not synchronized with an on-premises instance of Active Directory, you do not need DirSync or AAD Sync.</span></span>
* <span data-ttu-id="eb22f-132">選擇最適合您企業的使用情況模型。</span><span class="sxs-lookup"><span data-stu-id="eb22f-132">Choose the consumption model that best suits your business.</span></span> <span data-ttu-id="eb22f-133">使用量模型在選取之後，就無法再進行變更。</span><span class="sxs-lookup"><span data-stu-id="eb22f-133">Once you select the usage model, you can’t change it.</span></span> <span data-ttu-id="eb22f-134">兩個模型如下︰</span><span class="sxs-lookup"><span data-stu-id="eb22f-134">The two models are:</span></span>
  * <span data-ttu-id="eb22f-135">每次驗證︰向您收取每次驗證的費用。</span><span class="sxs-lookup"><span data-stu-id="eb22f-135">Per authentication: charges you for each verification.</span></span> <span data-ttu-id="eb22f-136">如果您想要所有存取特定應用程式的人員都使用雙步驟驗證，請使用這個模型。</span><span class="sxs-lookup"><span data-stu-id="eb22f-136">Use this model if you want two-step verification for anyone that accesses a certain app, not for specific users.</span></span>
  * <span data-ttu-id="eb22f-137">每個啟用的使用者︰會針對啟用 Azure MFA 的每個使用者向您數費。</span><span class="sxs-lookup"><span data-stu-id="eb22f-137">Per enabled user: charges you for each user that you enable for Azure MFA.</span></span> <span data-ttu-id="eb22f-138">如果您有某些使用者具有 Azure AD Premium 或 Enterprise Mobility Suite 授權，有些則沒有，請使用此模型。</span><span class="sxs-lookup"><span data-stu-id="eb22f-138">Use this model if you have some users with Azure AD Premium or Enterprise Mobility Suite licenses, and some without.</span></span>

### <a name="supportability"></a><span data-ttu-id="eb22f-139">支援能力</span><span class="sxs-lookup"><span data-stu-id="eb22f-139">Supportability</span></span>
<span data-ttu-id="eb22f-140">因為大多數使用者已經習慣僅使用密碼來驗證，所以公司務必讓所有使用者了解此程序。</span><span class="sxs-lookup"><span data-stu-id="eb22f-140">Since most users are accustomed to using only passwords to authenticate, it is important that your company brings awareness to all users regarding this process.</span></span> <span data-ttu-id="eb22f-141">這番了解可以避免使用者因為 MFA 的小問題就連絡技術人員。</span><span class="sxs-lookup"><span data-stu-id="eb22f-141">This awareness can reduce the likelihood that users call your help desk for minor issues related to MFA.</span></span> <span data-ttu-id="eb22f-142">不過，有一些案例是需要暫時停用 MFA。</span><span class="sxs-lookup"><span data-stu-id="eb22f-142">However, there are some scenarios where temporarily disabling MFA is necessary.</span></span> <span data-ttu-id="eb22f-143">使用下列指導方針了解如何處理這些案例：</span><span class="sxs-lookup"><span data-stu-id="eb22f-143">Use the following guidelines to understand how to handle those scenarios:</span></span>

* <span data-ttu-id="eb22f-144">如果使用者因為行動裝置應用程式未收到通知或電話來電而無法登入，請訓練您的技術支援工作人員處理這種情況。</span><span class="sxs-lookup"><span data-stu-id="eb22f-144">Train your technical support staff to handle scenarios where the user can't sign in because the mobile app or phone is not receiving a notification or phone call.</span></span> <span data-ttu-id="eb22f-145">技術支援人員可以[啟用單次許可](multi-factor-authentication-whats-next.md#one-time-bypass)，讓使用者「略過」雙步驟驗證而只需要驗證一次。</span><span class="sxs-lookup"><span data-stu-id="eb22f-145">Technical support can [enable a one-time bypass](multi-factor-authentication-whats-next.md#one-time-bypass) to allow a user to authenticate a single time by "bypassing" two-step verification.</span></span> <span data-ttu-id="eb22f-146">許可只是暫時性，經過指定的秒數之後就會到期。</span><span class="sxs-lookup"><span data-stu-id="eb22f-146">The bypass is temporary and expires after a specified number of seconds.</span></span>
* <span data-ttu-id="eb22f-147">請考慮使用 Azure MFA 中的[信任的 IP 功能](multi-factor-authentication-whats-next.md#trusted-ips)，以盡量避免雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="eb22f-147">Consider the [Trusted IPs capability](multi-factor-authentication-whats-next.md#trusted-ips) in Azure MFA as a way to minimize two-step verification.</span></span> <span data-ttu-id="eb22f-148">受管理或同盟租用戶的管理員可以利用此功能，讓從公司近端內部網路登入的使用者略過雙步驟驗證。</span><span class="sxs-lookup"><span data-stu-id="eb22f-148">With this feature, administrators of a managed or federated tenant can bypass two-step verification for users that are signing in from the company’s local intranet.</span></span> <span data-ttu-id="eb22f-149">這些功能適用於擁有 Azure AD Premium、Enterprise Mobility Suite 或 Azure Multi-Factor Authentication 授權的 Azure AD 租用戶。</span><span class="sxs-lookup"><span data-stu-id="eb22f-149">The features are available for Azure AD tenants that have Azure AD Premium, Enterprise Mobility Suite, or Azure Multi-Factor Authentication licenses.</span></span>

## <a name="best-practices-for-an-on-premises-deployment"></a><span data-ttu-id="eb22f-150">內部部署的最佳作法</span><span class="sxs-lookup"><span data-stu-id="eb22f-150">Best Practices for an on-premises deployment</span></span>
<span data-ttu-id="eb22f-151">如果您的公司決定採用自己的基礎結構來啟用 MFA，則您需要在內部部署 Azure Multi-Factor Authentication Server。</span><span class="sxs-lookup"><span data-stu-id="eb22f-151">If your company decided to leverage its own infrastructure to enable MFA, then you need to deploy an Azure Multi-Factor Authentication Server on-premises.</span></span> <span data-ttu-id="eb22f-152">下圖顯示 MFA Server 元件：</span><span class="sxs-lookup"><span data-stu-id="eb22f-152">The MFA Server components are shown in the following diagram:</span></span>

<span data-ttu-id="eb22f-153">![MFA Server 預設元件︰主控台、同步處理引擎、管理入口網站、雲端服務](./media/multi-factor-authentication-security-best-practices/server.png) \*依預設未安裝\**已安裝，但依預設未啟用</span><span class="sxs-lookup"><span data-stu-id="eb22f-153">![Default MFA Server components: console, sync engine, management portal, cloud service](./media/multi-factor-authentication-security-best-practices/server.png) \*Not installed by default \**Installed but not enabled by default</span></span>

<span data-ttu-id="eb22f-154">Azure Multi-Factor Authentication Server 可以使用同盟來保護雲端資源和內部部署資源的安全。</span><span class="sxs-lookup"><span data-stu-id="eb22f-154">Azure Multi-Factor Authentication Server can secure cloud resources and on-premises resources by using federation.</span></span> <span data-ttu-id="eb22f-155">您必須擁有 AD FS 並讓它與您的 Azure AD 租用戶同盟。</span><span class="sxs-lookup"><span data-stu-id="eb22f-155">You must have AD FS and have it federated with your Azure AD tenant.</span></span>
<span data-ttu-id="eb22f-156">設定 Multi-Factor Authentication Server 時，請考慮下列詳細資料：</span><span class="sxs-lookup"><span data-stu-id="eb22f-156">When setting up Multi-Factor Authentication Server, consider the following details:</span></span>

* <span data-ttu-id="eb22f-157">如果您使用 Active Directory Federation Services (AD FS) 保護 Azure AD 資源，則第一個驗證步驟是使用 AD FS 在內部部署執行。</span><span class="sxs-lookup"><span data-stu-id="eb22f-157">If you are securing Azure AD resources using Active Directory Federation Services (AD FS), then the first verification step is performed on-premises using AD FS.</span></span> <span data-ttu-id="eb22f-158">第二個步驟是使用宣告以在內部部署執行。</span><span class="sxs-lookup"><span data-stu-id="eb22f-158">The second step is performed on-premises by honoring the claim.</span></span>
* <span data-ttu-id="eb22f-159">您不需要在 AD FS 同盟伺服器上安裝 Azure Multi-Factor Authentication Server。</span><span class="sxs-lookup"><span data-stu-id="eb22f-159">You don't have to install the Azure Multi-Factor Authentication Server your AD FS federation server.</span></span> <span data-ttu-id="eb22f-160">不過，必須在執行 AD FS 的 Windows Server 2012 R2 上安裝適用於 AD FS 的 Multi-Factor Authentication 配接器。</span><span class="sxs-lookup"><span data-stu-id="eb22f-160">However, the Multi-Factor Authentication Adapter for AD FS must be installed on a Windows Server 2012 R2 running AD FS.</span></span> <span data-ttu-id="eb22f-161">您可以在不同的電腦上安裝伺服器 (只要是支援的版本即可) 以及在 AD FS 同盟伺服器上個別安裝 AD FS 配接器。</span><span class="sxs-lookup"><span data-stu-id="eb22f-161">You can install the server on a different computer, as long as it is a supported version, and install the AD FS adapter separately on your AD FS federation server.</span></span> 
* <span data-ttu-id="eb22f-162">Multi-Factor Authentication AD FS 配接器安裝精靈會在 Active Directory 中建立名為 PhoneFactor Admins 的安全性群組，然後將 AD FS 服務帳戶新增至這個群組。</span><span class="sxs-lookup"><span data-stu-id="eb22f-162">The Multi-Factor Authentication AD FS Adapter installation wizard creates a security group called PhoneFactor Admins in your Active Directory, and then adds your AD FS service account to this group.</span></span> <span data-ttu-id="eb22f-163">確認確實已在網域控制站上建立 PhoneFactor Admins 群組，而且 AD FS 服務帳戶是此群組的成員。</span><span class="sxs-lookup"><span data-stu-id="eb22f-163">Verify that the PhoneFactor Admins group was created on your domain controller, and that the AD FS service account is a member of this group.</span></span> <span data-ttu-id="eb22f-164">如有必要，請以手動方式將 AD FS 服務帳戶加入至網域控制站上的 PhoneFactor Admins 群組。</span><span class="sxs-lookup"><span data-stu-id="eb22f-164">If necessary, add the AD FS service account to the PhoneFactor Admins group on your domain controller manually.</span></span>

### <a name="user-portal"></a><span data-ttu-id="eb22f-165">使用者入口網站</span><span class="sxs-lookup"><span data-stu-id="eb22f-165">User Portal</span></span>
<span data-ttu-id="eb22f-166">使用者入口網站允許自助功能，且提供一組完整的使用者管理功能。</span><span class="sxs-lookup"><span data-stu-id="eb22f-166">The user portal allows self-service capabilities and provides a full set of user administration capabilities.</span></span> <span data-ttu-id="eb22f-167">它在 Internet Information Server (IIS) 網站中執行。</span><span class="sxs-lookup"><span data-stu-id="eb22f-167">It runs in an Internet Information Server (IIS) web site.</span></span> <span data-ttu-id="eb22f-168">遵循下列指導方針以設定此元件：</span><span class="sxs-lookup"><span data-stu-id="eb22f-168">Use the following guidelines to configure this component:</span></span>

* <span data-ttu-id="eb22f-169">使用 IIS 6 或更新版本</span><span class="sxs-lookup"><span data-stu-id="eb22f-169">Use IIS 6 or greater</span></span>
* <span data-ttu-id="eb22f-170">安裝和註冊 ASP.NET v2.0.507207</span><span class="sxs-lookup"><span data-stu-id="eb22f-170">Install and register ASP.NET v2.0.507207</span></span>
* <span data-ttu-id="eb22f-171">請確定此伺服器可以部署在周邊網路中</span><span class="sxs-lookup"><span data-stu-id="eb22f-171">Ensure that this server can be deployed in a perimeter network</span></span>

### <a name="app-passwords"></a><span data-ttu-id="eb22f-172">應用程式密碼</span><span class="sxs-lookup"><span data-stu-id="eb22f-172">App Passwords</span></span>
<span data-ttu-id="eb22f-173">如果您的組織使用 SSO 與 Azure AD 同盟，而且您想要使用 Azure MFA 時，請注意下列細節：</span><span class="sxs-lookup"><span data-stu-id="eb22f-173">If your organization is federated for SSO with Azure AD and you are going to be using Azure MFA, then be aware of the following details:</span></span>

* <span data-ttu-id="eb22f-174">應用程式密碼由 Azure AD 驗證，因此會略過同盟。</span><span class="sxs-lookup"><span data-stu-id="eb22f-174">The app password is verified by Azure AD and therefore bypasses federation.</span></span> <span data-ttu-id="eb22f-175">唯有在設定應用程式密碼時才會使用同盟。</span><span class="sxs-lookup"><span data-stu-id="eb22f-175">Federation is only used when setting up app passwords.</span></span>
* <span data-ttu-id="eb22f-176">對於同盟 (SSO) 使用者，密碼會儲存在組織識別碼中。</span><span class="sxs-lookup"><span data-stu-id="eb22f-176">For federated (SSO) users, passwords are stored in the organizational id.</span></span> <span data-ttu-id="eb22f-177">如果使用者離開公司，這些資訊必須使用 DirSync 流向組織識別碼。</span><span class="sxs-lookup"><span data-stu-id="eb22f-177">If the user leaves the company, that info has to flow to organizational id using DirSync.</span></span> <span data-ttu-id="eb22f-178">停用/刪除帳戶可能需要長達三個小時才能完成同步處理，導致 Azure AD 中停用/刪除應用程式密碼時延遲。</span><span class="sxs-lookup"><span data-stu-id="eb22f-178">Account disable/deletion may take up to three hours to sync, which delays disable/deletion of app passwords in Azure AD.</span></span>
* <span data-ttu-id="eb22f-179">應用程式密碼不會遵守內部部署用戶端存取控制設定。</span><span class="sxs-lookup"><span data-stu-id="eb22f-179">On-premises Client Access Control settings are not honored by App Password.</span></span>
* <span data-ttu-id="eb22f-180">應用程式密碼不適用內部部署驗證記錄/稽核功能。</span><span class="sxs-lookup"><span data-stu-id="eb22f-180">No on-premises authentication logging/auditing capability is available for app passwords.</span></span>
* <span data-ttu-id="eb22f-181">某些進階架構設計在使用雙步驟驗證時，可能需要搭配使用組織使用者名稱和密碼及應用程式密碼，需視驗證的位置而定。</span><span class="sxs-lookup"><span data-stu-id="eb22f-181">Certain advanced architectural designs may require using a combination of organizational username and passwords and app passwords when using two-step verification with clients, depending on where they authenticate.</span></span> <span data-ttu-id="eb22f-182">對於根據內部部署基礎結構進行驗證的用戶端，您可以使用組織使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="eb22f-182">For clients that authenticate against an on-premises infrastructure, you would use an organizational username and password.</span></span> <span data-ttu-id="eb22f-183">對於根據 Azure AD 進行驗證的用戶端，您需要使用應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="eb22f-183">For clients that authenticate against Azure AD, you would use the app password.</span></span>
* <span data-ttu-id="eb22f-184">根據預設，使用者無法建立應用程式密碼。</span><span class="sxs-lookup"><span data-stu-id="eb22f-184">By default, users cannot create app passwords.</span></span> <span data-ttu-id="eb22f-185">如果您需要允許使用者建立應用程式密碼，請選取 [允許使用者建立應用程式密碼以登入非瀏覽器應用程式] 選項。</span><span class="sxs-lookup"><span data-stu-id="eb22f-185">If you need to allow users to create app passwords, select the **Allow users to create app passwords to sign into non-browser applications** option.</span></span>

## <a name="additional-considerations"></a><span data-ttu-id="eb22f-186">其他考量</span><span class="sxs-lookup"><span data-stu-id="eb22f-186">Additional Considerations</span></span>
<span data-ttu-id="eb22f-187">針對部署在內部部署的每個元件，請使用此清單以了解其他考量和最佳做法：</span><span class="sxs-lookup"><span data-stu-id="eb22f-187">Use this list for additional considerations and guidance for each component that is deployed on-premises:</span></span>

- <span data-ttu-id="eb22f-188">搭配 [Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md) 來設定 Multi-Factor Authentication。</span><span class="sxs-lookup"><span data-stu-id="eb22f-188">Set up Azure Multi-Factor Authentication with [Active Directory Federation Service](multi-factor-authentication-get-started-adfs.md).</span></span>
- <span data-ttu-id="eb22f-189">搭配 [RADIUS 驗證](multi-factor-authentication-get-started-server-radius.md)來安裝和設定 Azure MFA Server。</span><span class="sxs-lookup"><span data-stu-id="eb22f-189">Set up and configure the Azure MFA Server with [RADIUS Authentication](multi-factor-authentication-get-started-server-radius.md).</span></span>
- <span data-ttu-id="eb22f-190">搭配 [IIS 驗證](multi-factor-authentication-get-started-server-iis.md)來安裝和設定 Azure MFA Server。</span><span class="sxs-lookup"><span data-stu-id="eb22f-190">Set up and configure the Azure MFA Server with [IIS Authentication](multi-factor-authentication-get-started-server-iis.md).</span></span>
- <span data-ttu-id="eb22f-191">搭配 [Windows 驗證](multi-factor-authentication-get-started-server-windows.md)來安裝和設定 Azure MFA Server。</span><span class="sxs-lookup"><span data-stu-id="eb22f-191">Set up and configure the Azure MFA Server with [Windows Authentication](multi-factor-authentication-get-started-server-windows.md).</span></span>
- <span data-ttu-id="eb22f-192">搭配 [LDAP 驗證](multi-factor-authentication-get-started-server-ldap.md)來安裝和設定 Azure MFA Server。</span><span class="sxs-lookup"><span data-stu-id="eb22f-192">Set up and configure the Azure MFA Server with [LDAP Authentication](multi-factor-authentication-get-started-server-ldap.md).</span></span>
- <span data-ttu-id="eb22f-193">搭配[使用 RADIUS 的遠端桌面閘道和 Azure Multi-Factor Authentication Server](multi-factor-authentication-get-started-server-rdg.md)，以安裝和設定 Azure MFA Server。</span><span class="sxs-lookup"><span data-stu-id="eb22f-193">Set up and configure the Azure MFA Server with [Remote Desktop Gateway and Azure Multi-Factor Authentication Server using RADIUS](multi-factor-authentication-get-started-server-rdg.md).</span></span>
- <span data-ttu-id="eb22f-194">安裝和設定 Azure MFA Server 和 [ndows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md)之間的同步處理。</span><span class="sxs-lookup"><span data-stu-id="eb22f-194">Set up and configure synchronization between the Azure MFA Server and [Windows Server Active Directory](multi-factor-authentication-get-started-server-dirint.md).</span></span>
- <span data-ttu-id="eb22f-195">[部署 Azure Multi-Factor Authentication Server 行動裝置應用程式 Web 服務](multi-factor-authentication-get-started-server-webservice.md)。</span><span class="sxs-lookup"><span data-stu-id="eb22f-195">[Deploy the Azure Multi-Factor Authentication Server Mobile App Web Service](multi-factor-authentication-get-started-server-webservice.md).</span></span>
- <span data-ttu-id="eb22f-196">[採用 Azure Multi-Factor Authentication 的進階 VPN 設定](multi-factor-authentication-advanced-vpn-configurations.md)，適用於使用 LDAP 或 RADIUS 的 Cisco ASA、Citrix Netscaler 和 Juniper/Pulse 安全 VPN 應用裝置。</span><span class="sxs-lookup"><span data-stu-id="eb22f-196">[Advanced VPN Configuration with Azure Multi-Factor Authentication](multi-factor-authentication-advanced-vpn-configurations.md) for Cisco ASA, Citrix Netscaler, and Juniper/Pulse Secure VPN appliances using LDAP or RADIUS.</span></span>

## <a name="next-steps"></a><span data-ttu-id="eb22f-197">後續步驟</span><span class="sxs-lookup"><span data-stu-id="eb22f-197">Next steps</span></span>
<span data-ttu-id="eb22f-198">雖然這篇文章強調 Azure MFA 的一些最佳做法，還有其他資源您也可以在規劃 MFA 部署時使用。</span><span class="sxs-lookup"><span data-stu-id="eb22f-198">While this article highlights some best practices for Azure MFA, there are other resources that you can also use while planning your MFA deployment.</span></span> <span data-ttu-id="eb22f-199">以下清單有可以在此程序期間協助您的一些關鍵文章：</span><span class="sxs-lookup"><span data-stu-id="eb22f-199">The list below has some key articles that can assist you during this process:</span></span>

* [<span data-ttu-id="eb22f-200">Azure Multi-Factor Authentication 中的報告</span><span class="sxs-lookup"><span data-stu-id="eb22f-200">Reports in Azure Multi-Factor Authentication</span></span>](multi-factor-authentication-manage-reports.md)
* [<span data-ttu-id="eb22f-201">雙步驟驗證註冊體驗</span><span class="sxs-lookup"><span data-stu-id="eb22f-201">The two-step verification registration experience</span></span>](multi-factor-authentication-end-user-first-time.md)
* [<span data-ttu-id="eb22f-202">Azure Multi-Factor Authentication 常見問題集</span><span class="sxs-lookup"><span data-stu-id="eb22f-202">Azure Multi-Factor Authentication FAQ</span></span>](multi-factor-authentication-faq.md)
