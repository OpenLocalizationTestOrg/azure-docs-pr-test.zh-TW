---
title: "針對已加入混合式 Azure Active Directory 的 Windows 10 和 Windows Server 2016 裝置進行疑難排解 | Microsoft Docs"
description: "針對已加入混合式 Azure Active Directory 的 Windows 10 和 Windows Server 2016 裝置進行疑難排解。"
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
ms.date: 08/17/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 51962c14a3c32bbfa9a613fa203cc48cfea50c0b
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="d023a-103">針對已加入混合式 Azure Active Directory 的 Windows 10 和 Windows Server 2016 裝置進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="d023a-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="d023a-104">本主題適用於下列用戶端：</span><span class="sxs-lookup"><span data-stu-id="d023a-104">This topic is applicable to the following clients:</span></span>

-   <span data-ttu-id="d023a-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="d023a-105">Windows 10</span></span>
-   <span data-ttu-id="d023a-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="d023a-106">Windows Server 2016</span></span>

<span data-ttu-id="d023a-107">至於其他 Windows 用戶端，請參閱[針對已加入混合式 Azure Active Directory 的下層裝置進行疑難排解](device-management-troubleshoot-hybrid-join-windows-legacy.md)。</span><span class="sxs-lookup"><span data-stu-id="d023a-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="d023a-108">本主題假設您[設定已加入混合式 Azure Active Directory 的裝置](device-management-hybrid-azuread-joined-devices-setup.md)來支援下列案例：</span><span class="sxs-lookup"><span data-stu-id="d023a-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) to support the following scenarios:</span></span>

- <span data-ttu-id="d023a-109">裝置型條件式存取</span><span class="sxs-lookup"><span data-stu-id="d023a-109">Device-based conditional access</span></span>

- [<span data-ttu-id="d023a-110">設定的企業漫遊</span><span class="sxs-lookup"><span data-stu-id="d023a-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="d023a-111">Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="d023a-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="d023a-112">本文件提供有關如何解決潛在問題的疑難排解指引。</span><span class="sxs-lookup"><span data-stu-id="d023a-112">This document provides troubleshooting guidance on how to resolve potential issues.</span></span> 


<span data-ttu-id="d023a-113">對於 Windows 10 和 Windows Server 2016，混合式 Azure Active Directory 會加入對 Windows 10 2015 年 11 月更新 (含) 以上版本的支援。</span><span class="sxs-lookup"><span data-stu-id="d023a-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports the Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="d023a-114">建議使用年度更新版。</span><span class="sxs-lookup"><span data-stu-id="d023a-114">We recommend using the Anniversary update.</span></span>

## <a name="step-1-retrieve-the-join-status"></a><span data-ttu-id="d023a-115">步驟 1：擷取加入狀態</span><span class="sxs-lookup"><span data-stu-id="d023a-115">Step 1: Retrieve the join status</span></span> 

<span data-ttu-id="d023a-116">**若要擷取加入狀態：**</span><span class="sxs-lookup"><span data-stu-id="d023a-116">**To retrieve the join status:**</span></span>

1. <span data-ttu-id="d023a-117">以系統管理員身分開啟命令提示字元</span><span class="sxs-lookup"><span data-stu-id="d023a-117">Open the command prompt as an administrator</span></span>

2. <span data-ttu-id="d023a-118">輸入 **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="d023a-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="d023a-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="d023a-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="d023a-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated to test.</span><span class="sxs-lookup"><span data-stu-id="d023a-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated to test.</span></span>
                  <span data-ttu-id="d023a-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="d023a-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="d023a-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="d023a-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="d023a-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span><span class="sxs-lookup"><span data-stu-id="d023a-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-the-join-status"></a><span data-ttu-id="d023a-124">步驟 2：評估加入狀態</span><span class="sxs-lookup"><span data-stu-id="d023a-124">Step 2: Evaluate the join status</span></span> 

<span data-ttu-id="d023a-125">請檢閱下列欄位，並確定它們具有預期的值：</span><span class="sxs-lookup"><span data-stu-id="d023a-125">Review the following fields and make sure that they have the expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="d023a-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="d023a-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="d023a-127">此欄位指出裝置是否已加入 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="d023a-127">This field indicates whether the device is joined with Azure AD.</span></span> <span data-ttu-id="d023a-128">如果值為 **NO**，則尚未完成加入 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="d023a-128">If the value is **NO**, the join to Azure AD has not completed yet.</span></span> 

<span data-ttu-id="d023a-129">**可能的原因：**</span><span class="sxs-lookup"><span data-stu-id="d023a-129">**Possible causes:**</span></span>

- <span data-ttu-id="d023a-130">驗證要加入的電腦失敗。</span><span class="sxs-lookup"><span data-stu-id="d023a-130">Authentication of the computer for a join failed.</span></span>

- <span data-ttu-id="d023a-131">組織中有電腦探索不到的 HTTP Proxy。</span><span class="sxs-lookup"><span data-stu-id="d023a-131">There is an HTTP proxy in the organization that cannot be discovered by the computer</span></span>

- <span data-ttu-id="d023a-132">電腦無法連線到 Azure AD 來進行驗證，或無法連線到 Azure DRS 來進行註冊</span><span class="sxs-lookup"><span data-stu-id="d023a-132">The computer cannot reach Azure AD to authenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="d023a-133">電腦可能不在組織的內部網路上，或不在可直接看到內部部署 AD 網域控制站的 VPN 上。</span><span class="sxs-lookup"><span data-stu-id="d023a-133">The computer may not be on the organization’s internal network or on VPN with direct line of sight to an on-premises AD domain controller.</span></span>

- <span data-ttu-id="d023a-134">如果電腦有 TPM，它可能是處於不正常狀態。</span><span class="sxs-lookup"><span data-stu-id="d023a-134">If the computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="d023a-135">在本文件稍早提到的服務中可能有設定錯誤的情況，您將必須重新確認。</span><span class="sxs-lookup"><span data-stu-id="d023a-135">There might be a misconfiguration in the services noted in the document earlier that you will need to verify again.</span></span> <span data-ttu-id="d023a-136">常見範例包括：</span><span class="sxs-lookup"><span data-stu-id="d023a-136">Common examples are:</span></span>

    - <span data-ttu-id="d023a-137">您的同盟伺服器未啟用 WS-Trust 端點</span><span class="sxs-lookup"><span data-stu-id="d023a-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="d023a-138">您的同盟伺服器不允許來自您網路中使用「整合式 Windows 驗證」之電腦的輸入驗證。</span><span class="sxs-lookup"><span data-stu-id="d023a-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="d023a-139">沒有「服務連接點」物件指向電腦所屬 AD 樹系之 Azure AD 中已驗證的網域名稱</span><span class="sxs-lookup"><span data-stu-id="d023a-139">There is no Service Connection Point object that points to your verified domain name in Azure AD in the AD forest where the computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="d023a-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="d023a-140">DomainJoined : YES</span></span>  

<span data-ttu-id="d023a-141">此欄位指出裝置是否已加入內部部署 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="d023a-141">This field indicates whether the device is joined to an on-premises Active Directory or not.</span></span> <span data-ttu-id="d023a-142">如果值為 **NO**，則裝置無法執行混合式 Azure AD 加入。</span><span class="sxs-lookup"><span data-stu-id="d023a-142">If the value is **NO**, the device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="d023a-143">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="d023a-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="d023a-144">此欄位指出裝置是否已向 Azure AD 註冊為個人裝置 (標示為「已加入工作場所」)。</span><span class="sxs-lookup"><span data-stu-id="d023a-144">This field indicates whether the device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="d023a-145">如果已加入網域的電腦同時加入混合式 Azure AD，此值應為 **NO**。</span><span class="sxs-lookup"><span data-stu-id="d023a-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="d023a-146">如果值為 **YES**，則在完成混合式 Azure AD 加入之前已新增工作或學校帳戶。</span><span class="sxs-lookup"><span data-stu-id="d023a-146">If the value is **YES**, a work or school account was added prior to the completion of the hybrid Azure AD join.</span></span> <span data-ttu-id="d023a-147">在此情況下，使用年度更新版的 Windows 10 (1607) 時會忽略該帳戶。</span><span class="sxs-lookup"><span data-stu-id="d023a-147">In this case, the account is ignored when using the Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="d023a-148">WamDefaultSet : YES 和 AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="d023a-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="d023a-149">這些欄位指出使用者在登入裝置時，是否已順利向 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="d023a-149">These fields indicate whether the user has successfully authenticated to Azure AD when signing in to the device.</span></span> <span data-ttu-id="d023a-150">如果值為 **NO**，可能是因為：</span><span class="sxs-lookup"><span data-stu-id="d023a-150">If the values are **NO**, it could be due:</span></span>

- <span data-ttu-id="d023a-151">註冊時，與裝置關聯之 TPM 中的儲存體金鑰 (STK) 無效 (請在提高權限執行的情況下，檢查 KeySignTest)。</span><span class="sxs-lookup"><span data-stu-id="d023a-151">Bad storage key (STK) in TPM associated with the device upon registration (check the KeySignTest while running elevated).</span></span>

- <span data-ttu-id="d023a-152">替代登入識別碼</span><span class="sxs-lookup"><span data-stu-id="d023a-152">Alternate Login ID</span></span>

- <span data-ttu-id="d023a-153">找不到 HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="d023a-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="d023a-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d023a-154">Next steps</span></span>

<span data-ttu-id="d023a-155">如有問題，請參閱[裝置管理常見問題集](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="d023a-155">For questions, see the [device management FAQ](device-management-faq.md)</span></span> 