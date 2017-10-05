---
title: "針對已加入 Azure AD 網域之 Windows 10 和 Windows Server 2016 電腦的自動註冊進行疑難排解 | Microsoft Docs"
description: "針對已加入 Azure AD 網域之 Windows 10 和 Windows Server 2016 電腦的自動註冊進行疑難排解。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
ms.assetid: cdc25576-37f2-4afb-a786-f59ba4c284c2
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 5b7f95f302f716d9221b5fae59aa2df5c956a524
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-to-azure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="3330a-103">針對已加入 Azure AD 網域之電腦的自動註冊進行疑難排解 – Windows 10 和 Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3330a-103">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="3330a-104">本主題適用於下列用戶端：</span><span class="sxs-lookup"><span data-stu-id="3330a-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="3330a-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="3330a-105">Windows 10</span></span>
-   <span data-ttu-id="3330a-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3330a-106">Windows Server 2016</span></span>

<span data-ttu-id="3330a-107">針對其他 Windows 用戶端，請參閱[針對已加入 Azure AD 網域之 Windows 下層用戶端電腦的自動註冊進行疑難排解](active-directory-device-registration-troubleshoot-windows-legacy.md)。</span><span class="sxs-lookup"><span data-stu-id="3330a-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers to Azure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="3330a-108">本主題假設您已經依照[如何設定讓已加入網域的 Windows 裝置自動向 Azure Active Directory 註冊](active-directory-device-registration-get-started.md)所述，設定讓已加入網域的裝置自動註冊，以支援下列案例：</span><span class="sxs-lookup"><span data-stu-id="3330a-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How to configure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) to support the following scenarios:</span></span>

- [<span data-ttu-id="3330a-109">裝置型條件式存取</span><span class="sxs-lookup"><span data-stu-id="3330a-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="3330a-110">設定的企業漫遊</span><span class="sxs-lookup"><span data-stu-id="3330a-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="3330a-111">Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="3330a-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="3330a-112">本文件提供有關如何解決潛在問題的疑難排解指引。</span><span class="sxs-lookup"><span data-stu-id="3330a-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 

<span data-ttu-id="3330a-113">Windows 10 的 2015 年 11 月更新和更新版本皆支援註冊。</span><span class="sxs-lookup"><span data-stu-id="3330a-113">The registration is supported in the Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="3330a-114">建議使用「年度更新」來啟用上述案例。</span><span class="sxs-lookup"><span data-stu-id="3330a-114">We recommend using the Anniversary Update for enabling the scenarios above.</span></span>

## <a name="step-1-retrieve-the-registration-status"></a><span data-ttu-id="3330a-115">步驟 1：擷取註冊狀態</span><span class="sxs-lookup"><span data-stu-id="3330a-115">Step 1: Retrieve the registration status</span></span> 

<span data-ttu-id="3330a-116">**擷取註冊狀態：**</span><span class="sxs-lookup"><span data-stu-id="3330a-116">**To retrieve the registration status:**</span></span>

1. <span data-ttu-id="3330a-117">以系統管理員身分開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="3330a-117">Open the command prompt as an administrator.</span></span>

2. <span data-ttu-id="3330a-118">輸入 **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="3330a-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="3330a-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="3330a-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="3330a-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span><span class="sxs-lookup"><span data-stu-id="3330a-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="3330a-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="3330a-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="3330a-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="3330a-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="3330a-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="3330a-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-the-registration-status"></a><span data-ttu-id="3330a-124">步驟 2：評估註冊狀態</span><span class="sxs-lookup"><span data-stu-id="3330a-124">Step 2: Evaluate the registration status</span></span> 

<span data-ttu-id="3330a-125">請檢閱下列欄位，並確定它們具有預期的值：</span><span class="sxs-lookup"><span data-stu-id="3330a-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="3330a-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="3330a-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="3330a-127">此欄位顯示裝置是否已向 Azure AD 註冊。</span><span class="sxs-lookup"><span data-stu-id="3330a-127">This field shows whether the device is registered with Azure AD.</span></span> <span data-ttu-id="3330a-128">如果值顯示為 ‘NO’，即表示尚未完成註冊。</span><span class="sxs-lookup"><span data-stu-id="3330a-128">If the value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="3330a-129">**可能的原因：**</span><span class="sxs-lookup"><span data-stu-id="3330a-129">**Possible causes:**</span></span>

- <span data-ttu-id="3330a-130">驗證要註冊的電腦失敗。</span><span class="sxs-lookup"><span data-stu-id="3330a-130">Authentication of the computer for registration failed.</span></span>

- <span data-ttu-id="3330a-131">組織中有電腦探索不到的 HTTP Proxy。</span><span class="sxs-lookup"><span data-stu-id="3330a-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="3330a-132">電腦無法連線到 Azure AD 來進行驗證，或無法連線到 Azure DRS 來進行註冊</span><span class="sxs-lookup"><span data-stu-id="3330a-132">The computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="3330a-133">電腦可能不在組織的內部網路上，或不在可直接看到內部部署 AD 網域控制站的 VPN 上。</span><span class="sxs-lookup"><span data-stu-id="3330a-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="3330a-134">如果電腦有 TPM，它可能是處於不正常狀態。</span><span class="sxs-lookup"><span data-stu-id="3330a-134">If the computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="3330a-135">在本文件稍早提到的服務中可能有設定錯誤的情況，您將必須重新確認。</span><span class="sxs-lookup"><span data-stu-id="3330a-135">There may be a misconfiguration in services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="3330a-136">常見範例包括：</span><span class="sxs-lookup"><span data-stu-id="3330a-136">Common examples are:</span></span>

    - <span data-ttu-id="3330a-137">您的同盟伺服器未啟用 WS-Trust 端點</span><span class="sxs-lookup"><span data-stu-id="3330a-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="3330a-138">您的同盟伺服器可能不允許來自您網路中使用「整合式 Windows 驗證」之電腦的輸入驗證。</span><span class="sxs-lookup"><span data-stu-id="3330a-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="3330a-139">沒有「服務連接點」物件指向電腦所屬 AD 樹系之 Azure AD 中已驗證的網域名稱</span><span class="sxs-lookup"><span data-stu-id="3330a-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="3330a-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="3330a-140">DomainJoined : YES</span></span>  

<span data-ttu-id="3330a-141">此欄位顯示裝置是否已加入內部部署 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="3330a-141">This field shows whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="3330a-142">如果值顯示為 **NO**，即表示裝置無法自動向 Azure AD 註冊。</span><span class="sxs-lookup"><span data-stu-id="3330a-142">If the value shows as **NO**, the device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="3330a-143">請先確認將裝置加入內部部署 Active Directory，如此它才能向 Azure AD 註冊。</span><span class="sxs-lookup"><span data-stu-id="3330a-143">Check first that the device joins to the on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="3330a-144">如果您想要將電腦直接加入 Azure AD，請了解 Azure Active Directory Join 的功能。</span><span class="sxs-lookup"><span data-stu-id="3330a-144">If you are looking for joining the computer to Azure AD directly, please go to Learn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="3330a-145">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="3330a-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="3330a-146">此欄位顯示裝置是否已向 Azure AD 註冊，但是是以個人裝置的形式註冊 (標示為 [已加入工作場所])。</span><span class="sxs-lookup"><span data-stu-id="3330a-146">This field shows whether the device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="3330a-147">如果針對已向 Azure AD 註冊的已加入網域電腦，這個值應該顯示為 ‘NO’，但卻顯示為 YES，即表示在電腦完成註冊之前已新增工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="3330a-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior to the computer completing registration.</span></span> <span data-ttu-id="3330a-148">在此情況下，如果使用的是 Windows 10「年度更新」版 (在 [執行] 視窗或命令提示字元視窗中執行 WinVer 命令時會顯示 1607)，將會忽略該帳戶。</span><span class="sxs-lookup"><span data-stu-id="3330a-148">In this case the account will be ignored if using the Anniversary Update version of Windows 10 (1607 when running the WinVer command in the ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="3330a-149">WamDefaultSet : YES 和 AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="3330a-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="3330a-150">這些欄位顯示使用者在登入裝置時，已順利向 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="3330a-150">These fields show that the user has successfully authenticated to Azure AD upon signing in to the device.</span></span> <span data-ttu-id="3330a-151">如果顯示為 ‘NO’，則可能的原因如下：</span><span class="sxs-lookup"><span data-stu-id="3330a-151">If they show ‘NO’ the following are possible causes:</span></span>

- <span data-ttu-id="3330a-152">註冊時，與裝置關聯之 TPM 中的儲存體金鑰 (STK) 無效 (請在提高權限執行的情況下，檢查 KeySignTest)。</span><span class="sxs-lookup"><span data-stu-id="3330a-152">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="3330a-153">替代登入識別碼</span><span class="sxs-lookup"><span data-stu-id="3330a-153">Alternate Login ID</span></span>

- <span data-ttu-id="3330a-154">找不到 HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="3330a-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="3330a-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3330a-155">Next steps</span></span>

<span data-ttu-id="3330a-156">如需詳細資訊，請參閱[自動裝置註冊常見問題集](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="3330a-156">For more information, see the [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 