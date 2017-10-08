---
title: "aaaTroubleshooting 混合 Azure Active Directory 已加入 Windows 10 和 Windows Server 2016 的裝置 |Microsoft 文件"
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
ms.openlocfilehash: cc252d1d0684d6632694afc8a367327794228c19
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-hybrid-azure-active-directory-joined-windows-10-and-windows-server-2016-devices"></a><span data-ttu-id="cf2ec-103">針對已加入混合式 Azure Active Directory 的 Windows 10 和 Windows Server 2016 裝置進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="cf2ec-103">Troubleshooting hybrid Azure Active Directory joined Windows 10 and Windows Server 2016 devices</span></span> 

<span data-ttu-id="cf2ec-104">本主題僅適用於 toohello 下列用戶端：</span><span class="sxs-lookup"><span data-stu-id="cf2ec-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="cf2ec-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="cf2ec-105">Windows 10</span></span>
-   <span data-ttu-id="cf2ec-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="cf2ec-106">Windows Server 2016</span></span>

<span data-ttu-id="cf2ec-107">至於其他 Windows 用戶端，請參閱[針對已加入混合式 Azure Active Directory 的下層裝置進行疑難排解](device-management-troubleshoot-hybrid-join-windows-legacy.md)。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-107">For other Windows clients, see [Troubleshooting hybrid Azure Active Directory joined down-level devices](device-management-troubleshoot-hybrid-join-windows-legacy.md).</span></span>

<span data-ttu-id="cf2ec-108">本主題假設您有[設定混合式 Azure Active Directory 加入裝置](device-management-hybrid-azuread-joined-devices-setup.md)toosupport hello 下列案例：</span><span class="sxs-lookup"><span data-stu-id="cf2ec-108">This topic assumes that you have [configured hybrid Azure Active Directory joined devices](device-management-hybrid-azuread-joined-devices-setup.md) toosupport hello following scenarios:</span></span>

- <span data-ttu-id="cf2ec-109">裝置型條件式存取</span><span class="sxs-lookup"><span data-stu-id="cf2ec-109">Device-based conditional access</span></span>

- [<span data-ttu-id="cf2ec-110">設定的企業漫遊</span><span class="sxs-lookup"><span data-stu-id="cf2ec-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="cf2ec-111">Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="cf2ec-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="cf2ec-112">這份文件上如何 tooresolve 可能的問題提供疑難排解指引。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 


<span data-ttu-id="cf2ec-113">適用於 Windows 10 和 Windows Server 2016，混合 Azure Active Directory 聯結支援 hello Windows 10 11 月更新 2015年和更新版本。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-113">For Windows 10 and Windows Server 2016, hybrid Azure Active Directory join supports hello Windows 10 November 2015 Update and above.</span></span> <span data-ttu-id="cf2ec-114">我們建議使用 hello 週年日更新。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-114">We recommend using hello Anniversary update.</span></span>

## <a name="step-1-retrieve-hello-join-status"></a><span data-ttu-id="cf2ec-115">步驟 1： 擷取 hello 聯結狀態</span><span class="sxs-lookup"><span data-stu-id="cf2ec-115">Step 1: Retrieve hello join status</span></span> 

<span data-ttu-id="cf2ec-116">**tooretrieve hello 聯結狀態：**</span><span class="sxs-lookup"><span data-stu-id="cf2ec-116">**tooretrieve hello join status:**</span></span>

1. <span data-ttu-id="cf2ec-117">以系統管理員身分開啟 hello 命令提示字元</span><span class="sxs-lookup"><span data-stu-id="cf2ec-117">Open hello command prompt as an administrator</span></span>

2. <span data-ttu-id="cf2ec-118">輸入 **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="cf2ec-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="cf2ec-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="cf2ec-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined: YES
     <span data-ttu-id="cf2ec-120">EnterpriseJoined: 沒有 DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 指紋： B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft 平台密碼編譯提供者 TpmProtected： 是KeySignTest:: 必須執行更高的 tootest。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-120">EnterpriseJoined: NO DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint: B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft Platform Crypto Provider TpmProtected: YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="cf2ec-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span><span class="sxs-lookup"><span data-stu-id="cf2ec-121">Idp: login.windows.net TenantId: 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName: Contoso AuthCodeUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl: https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl: https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl: https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl: https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl: eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion: 1.0 JoinSrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId: urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion: 1.0 KeySrvUrl: https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId: urn:ms-drs:enterpriseregistration.windows.net DomainJoined: YES DomainName: CONTOSO</span></span>
    
    <span data-ttu-id="cf2ec-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="cf2ec-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet: YES
               NgcKeyId: {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined: NO
          WamDefaultSet: YES
    <span data-ttu-id="cf2ec-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span><span class="sxs-lookup"><span data-stu-id="cf2ec-123">WamDefaultAuthority: organizations         WamDefaultId: https://login.microsoft.com       WamDefaultGUID: {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt: YES</span></span>



## <a name="step-2-evaluate-hello-join-status"></a><span data-ttu-id="cf2ec-124">步驟 2： 評估 hello 聯結狀態</span><span class="sxs-lookup"><span data-stu-id="cf2ec-124">Step 2: Evaluate hello join status</span></span> 

<span data-ttu-id="cf2ec-125">檢閱 hello 下列欄位，並確定它們有 hello 預期值：</span><span class="sxs-lookup"><span data-stu-id="cf2ec-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="cf2ec-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="cf2ec-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="cf2ec-127">此欄位會指出是否要將 hello 裝置加入 Azure ad。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-127">This field indicates whether hello device is joined with Azure AD.</span></span> <span data-ttu-id="cf2ec-128">如果 hello 值**否**，hello 聯結 tooAzure AD 尚未完成。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-128">If hello value is **NO**, hello join tooAzure AD has not completed yet.</span></span> 

<span data-ttu-id="cf2ec-129">**可能的原因：**</span><span class="sxs-lookup"><span data-stu-id="cf2ec-129">**Possible causes:**</span></span>

- <span data-ttu-id="cf2ec-130">聯結的 hello 電腦驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-130">Authentication of hello computer for a join failed.</span></span>

- <span data-ttu-id="cf2ec-131">無法探索 hello 電腦的 hello 組織中沒有 HTTP proxy</span><span class="sxs-lookup"><span data-stu-id="cf2ec-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="cf2ec-132">hello 電腦無法連線到 Azure AD tooauthenticate 或 Azure DRS 的註冊</span><span class="sxs-lookup"><span data-stu-id="cf2ec-132">hello computer cannot reach Azure AD tooauthenticate or Azure DRS for registration</span></span>

- <span data-ttu-id="cf2ec-133">hello 電腦可能不是 VPN 或 hello 組織內部網路上的直接視線 tooan 在內部部署 AD 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="cf2ec-134">如果 hello 電腦有 TPM，它可以處於不正常的狀態。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-134">If hello computer has a TPM, it can be in a bad state.</span></span>

- <span data-ttu-id="cf2ec-135">可能有在 hello 服務設定不正確前文所述 hello 文件中，您需要 tooverify 一次。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-135">There might be a misconfiguration in hello services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="cf2ec-136">常見範例包括：</span><span class="sxs-lookup"><span data-stu-id="cf2ec-136">Common examples are:</span></span>

    - <span data-ttu-id="cf2ec-137">您的同盟伺服器未啟用 WS-Trust 端點</span><span class="sxs-lookup"><span data-stu-id="cf2ec-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="cf2ec-138">您的同盟伺服器不允許來自您網路中使用「整合式 Windows 驗證」之電腦的輸入驗證。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-138">Your federation server does not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="cf2ec-139">在 Azure AD 中點 tooyour 驗證的網域名稱，其中 hello 電腦屬於 hello AD 樹系中沒有服務連接點物件</span><span class="sxs-lookup"><span data-stu-id="cf2ec-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="cf2ec-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="cf2ec-140">DomainJoined : YES</span></span>  

<span data-ttu-id="cf2ec-141">此欄位會指出是否已加入 hello 裝置 tooan 內部部署 Active Directory 或不。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-141">This field indicates whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="cf2ec-142">如果 hello 值**否**，hello 裝置無法執行 Azure AD 混合式連接。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-142">If hello value is **NO**, hello device cannot perform a hybrid Azure AD join.</span></span>  

---

### <a name="workplacejoined--no"></a><span data-ttu-id="cf2ec-143">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="cf2ec-143">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="cf2ec-144">此欄位會指出是否註冊為個人裝置的 Azure AD 裝置 hello (標示為*工作地方聯結*)。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-144">This field indicates whether hello device is registered with Azure AD as a personal device (marked as *Workplace Joined*).</span></span> <span data-ttu-id="cf2ec-145">如果已加入網域的電腦同時加入混合式 Azure AD，此值應為 **NO**。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-145">This value should be **NO** for a domain-joined computer that is also hybrid Azure AD joined.</span></span> <span data-ttu-id="cf2ec-146">如果 hello 值**是**、 工作或學校帳戶加入先前 toohello 完成的 hello Azure AD 混合式連接。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-146">If hello value is **YES**, a work or school account was added prior toohello completion of hello hybrid Azure AD join.</span></span> <span data-ttu-id="cf2ec-147">在此情況下，使用 hello 年度更新版的 Windows 10 (1607) 時，會忽略 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-147">In this case, hello account is ignored when using hello Anniversary Update version of Windows 10 (1607).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="cf2ec-148">WamDefaultSet : YES 和 AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="cf2ec-148">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="cf2ec-149">這些欄位會指出 hello 使用者是否已成功驗證 tooAzure AD toohello 裝置在登入時。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-149">These fields indicate whether hello user has successfully authenticated tooAzure AD when signing in toohello device.</span></span> <span data-ttu-id="cf2ec-150">如果 hello 值**否**，可能是因為：</span><span class="sxs-lookup"><span data-stu-id="cf2ec-150">If hello values are **NO**, it could be due:</span></span>

- <span data-ttu-id="cf2ec-151">不正確的儲存體金鑰 (STK) 與 hello 裝置時註冊 (核取 hello KeySignTest 執行提高權限) 相關聯的 TPM。</span><span class="sxs-lookup"><span data-stu-id="cf2ec-151">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="cf2ec-152">替代登入識別碼</span><span class="sxs-lookup"><span data-stu-id="cf2ec-152">Alternate Login ID</span></span>

- <span data-ttu-id="cf2ec-153">找不到 HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="cf2ec-153">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="cf2ec-154">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cf2ec-154">Next steps</span></span>

<span data-ttu-id="cf2ec-155">如有問題，請參閱 hello[裝置管理常見問題集](device-management-faq.md)</span><span class="sxs-lookup"><span data-stu-id="cf2ec-155">For questions, see hello [device management FAQ](device-management-faq.md)</span></span> 
