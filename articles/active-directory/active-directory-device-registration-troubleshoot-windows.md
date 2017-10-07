---
title: "適用於 Windows 10 和 Windows Server 2016 aaaTroubleshooting hello 自動註冊的 Azure AD 網域加入的電腦 |Microsoft 文件"
description: "疑難排解 hello 自動註冊的 Azure AD 網域加入適用於 Windows 10 和 Windows Server 2016 的電腦。"
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
ms.openlocfilehash: 3795323ce9392368b412b3e1208868431e59a74b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshooting-auto-registration-of-domain-joined-computers-tooazure-ad--windows-10-and-windows-server-2016"></a><span data-ttu-id="9df01-103">疑難排解自動登錄的網域加入電腦 tooAzure AD – Windows 10 和 Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="9df01-103">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>

<span data-ttu-id="9df01-104">本主題僅適用於 toohello 下列用戶端：</span><span class="sxs-lookup"><span data-stu-id="9df01-104">This topic is applicable toohello following clients:</span></span>

-   <span data-ttu-id="9df01-105">Windows 10</span><span class="sxs-lookup"><span data-stu-id="9df01-105">Windows 10</span></span>
-   <span data-ttu-id="9df01-106">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="9df01-106">Windows Server 2016</span></span>

<span data-ttu-id="9df01-107">其他 Windows 用戶端，請參閱[疑難排解自動登錄的網域加入 Windows 下層用戶端電腦 tooAzure AD](active-directory-device-registration-troubleshoot-windows-legacy.md)。</span><span class="sxs-lookup"><span data-stu-id="9df01-107">For other Windows clients, see [Troubleshooting auto-registration of domain joined computers tooAzure AD for Windows down-level clients](active-directory-device-registration-troubleshoot-windows-legacy.md).</span></span>

<span data-ttu-id="9df01-108">本主題假設您已設定自動註冊已加入網域的裝置如中所述述[如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory](active-directory-device-registration-get-started.md)下列案例 toosupport hello:</span><span class="sxs-lookup"><span data-stu-id="9df01-108">This topic assumes that you have configured auto-registration of domain-joined devices as outlined in described in [How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory](active-directory-device-registration-get-started.md) toosupport hello following scenarios:</span></span>

- [<span data-ttu-id="9df01-109">裝置型條件式存取</span><span class="sxs-lookup"><span data-stu-id="9df01-109">Device-based conditional access</span></span>](active-directory-conditional-access-automatic-device-registration-setup.md)

- [<span data-ttu-id="9df01-110">設定的企業漫遊</span><span class="sxs-lookup"><span data-stu-id="9df01-110">Enterprise roaming of settings</span></span>](active-directory-windows-enterprise-state-roaming-overview.md)

- [<span data-ttu-id="9df01-111">Windows Hello 企業版</span><span class="sxs-lookup"><span data-stu-id="9df01-111">Windows Hello for Business</span></span>](active-directory-azureadjoin-passport-deployment.md)


<span data-ttu-id="9df01-112">這份文件上如何 tooresolve 可能的問題提供疑難排解指引。</span><span class="sxs-lookup"><span data-stu-id="9df01-112">This document provides troubleshooting guidance on how tooresolve potential issues.</span></span> 

<span data-ttu-id="9df01-113">hello 註冊支援 hello Windows 10 11 月版 2015年更新和更新版本。</span><span class="sxs-lookup"><span data-stu-id="9df01-113">hello registration is supported in hello Windows 10 November 2015 Update and above.</span></span>  
<span data-ttu-id="9df01-114">我們建議使用 hello 週年紀念日更新啟用上述的 hello 案例。</span><span class="sxs-lookup"><span data-stu-id="9df01-114">We recommend using hello Anniversary Update for enabling hello scenarios above.</span></span>

## <a name="step-1-retrieve-hello-registration-status"></a><span data-ttu-id="9df01-115">步驟 1： 擷取 hello 註冊狀態</span><span class="sxs-lookup"><span data-stu-id="9df01-115">Step 1: Retrieve hello registration status</span></span> 

<span data-ttu-id="9df01-116">**tooretrieve hello 註冊狀態：**</span><span class="sxs-lookup"><span data-stu-id="9df01-116">**tooretrieve hello registration status:**</span></span>

1. <span data-ttu-id="9df01-117">系統管理員身分開啟命令提示字元中 hello。</span><span class="sxs-lookup"><span data-stu-id="9df01-117">Open hello command prompt as an administrator.</span></span>

2. <span data-ttu-id="9df01-118">輸入 **dsregcmd /status**</span><span class="sxs-lookup"><span data-stu-id="9df01-118">Type **dsregcmd /status**</span></span>



    <span data-ttu-id="9df01-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="9df01-119">+----------------------------------------------------------------------+
    | Device State                                                         |  +----------------------------------------------------------------------+</span></span>
    
        AzureAdJoined : YES
     <span data-ttu-id="9df01-120">EnterpriseJoined: 沒有 DeviceId: 5820fbe9-60c8-43b0-bb11-44aee233e4e7 指紋： B753A6679CE720451921302CA873794D94C6204A KeyContainerId: bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider: Microsoft 平台密碼編譯提供者 TpmProtected： 是KeySignTest:: 必須執行更高的 tootest。</span><span class="sxs-lookup"><span data-stu-id="9df01-120">EnterpriseJoined : NO DeviceId : 5820fbe9-60c8-43b0-bb11-44aee233e4e7 Thumbprint : B753A6679CE720451921302CA873794D94C6204A KeyContainerId : bae6a60b-1d2f-4d2a-a298-33385f6d05e9 KeyProvider : Microsoft Platform Crypto Provider TpmProtected : YES KeySignTest: : MUST Run elevated tootest.</span></span>
                  <span data-ttu-id="9df01-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span><span class="sxs-lookup"><span data-stu-id="9df01-121">Idp : login.windows.net TenantId : 72b988bf-86f1-41af-91ab-2d7cd011db47 TenantName : Contoso AuthCodeUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/authorize AccessTokenUrl : https://login.microsoftonline.com/msitsupp.microsoft.com/oauth2/token MdmUrl : https://enrollment.manage-beta.microsoft.com/EnrollmentServer/Discovery.svc MdmTouUrl : https://portal.manage-beta.microsoft.com/TermsOfUse.aspx dmComplianceUrl : https://portal.manage-beta.microsoft.com/?portalAction=Compliance SettingsUrl : eyJVcmlzIjpbImh0dHBzOi8va2FpbGFuaS5vbmUubWljcm9zb2Z0LmNvbS8iLCJodHRwczovL2thaWxhbmkxLm9uZS5taWNyb3NvZnQuY29tLyJdfQ== JoinSrvVersion : 1.0 JoinSrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/device/ JoinSrvId : urn:ms-drs:enterpriseregistration.windows.net KeySrvVersion : 1.0 KeySrvUrl : https://enterpriseregistration.windows.net/EnrollmentServer/key/ KeySrvId : urn:ms-drs:enterpriseregistration.windows.net DomainJoined : YES DomainName : CONTOSO</span></span>
    
    <span data-ttu-id="9df01-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span><span class="sxs-lookup"><span data-stu-id="9df01-122">+----------------------------------------------------------------------+
    | User State                                                           |  +----------------------------------------------------------------------+</span></span>
    
                 NgcSet : YES
               NgcKeyId : {C7A9AEDC-780E-4FDA-B200-1AE15561A46B}
        WorkplaceJoined : NO
          WamDefaultSet : YES
    <span data-ttu-id="9df01-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span><span class="sxs-lookup"><span data-stu-id="9df01-123">WamDefaultAuthority : organizations         WamDefaultId : https://login.microsoft.com       WamDefaultGUID : {B16898C6-A148-4967-9171-64D755DA8520} (AzureAd)           AzureAdPrt : YES</span></span>



## <a name="step-2-evaluate-hello-registration-status"></a><span data-ttu-id="9df01-124">步驟 2： 評估 hello 登錄狀態</span><span class="sxs-lookup"><span data-stu-id="9df01-124">Step 2: Evaluate hello registration status</span></span> 

<span data-ttu-id="9df01-125">檢閱 hello 下列欄位，並確定它們有 hello 預期值：</span><span class="sxs-lookup"><span data-stu-id="9df01-125">Review hello following fields and make sure that they have hello expected values:</span></span>

### <a name="azureadjoined--yes"></a><span data-ttu-id="9df01-126">AzureAdJoined : YES</span><span class="sxs-lookup"><span data-stu-id="9df01-126">AzureAdJoined : YES</span></span>  

<span data-ttu-id="9df01-127">此欄位會顯示 hello 裝置是否已向 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="9df01-127">This field shows whether hello device is registered with Azure AD.</span></span> <span data-ttu-id="9df01-128">如果 hello 值顯示為 [否]，註冊尚未完成。</span><span class="sxs-lookup"><span data-stu-id="9df01-128">If hello value shows as ‘NO’, registration has not completed.</span></span> 

<span data-ttu-id="9df01-129">**可能的原因：**</span><span class="sxs-lookup"><span data-stu-id="9df01-129">**Possible causes:**</span></span>

- <span data-ttu-id="9df01-130">註冊的 hello 電腦驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="9df01-130">Authentication of hello computer for registration failed.</span></span>

- <span data-ttu-id="9df01-131">無法探索 hello 電腦的 hello 組織中沒有 HTTP proxy</span><span class="sxs-lookup"><span data-stu-id="9df01-131">There is an HTTP proxy in hello organization that cannot be discovered by hello computer</span></span>

- <span data-ttu-id="9df01-132">hello 電腦無法連線到 Azure AD 進行驗證或註冊的 Azure DRS</span><span class="sxs-lookup"><span data-stu-id="9df01-132">hello computer cannot reach Azure AD for authentication or Azure DRS for registration</span></span>

- <span data-ttu-id="9df01-133">hello 電腦可能不是 VPN 或 hello 組織內部網路上的直接視線 tooan 在內部部署 AD 網域控制站。</span><span class="sxs-lookup"><span data-stu-id="9df01-133">hello computer may not be on hello organization’s internal network or on VPN with direct line of sight tooan on-premises AD domain controller.</span></span>

- <span data-ttu-id="9df01-134">如果 hello 電腦有 TPM，它可能處於不正常的狀態。</span><span class="sxs-lookup"><span data-stu-id="9df01-134">If hello computer has a TPM, it may be in a bad state.</span></span>

- <span data-ttu-id="9df01-135">可能會在 服務設定不正確前文所述 hello 文件中，您需要 tooverify 一次。</span><span class="sxs-lookup"><span data-stu-id="9df01-135">There may be a misconfiguration in services noted in hello document earlier that you will need tooverify again.</span></span> <span data-ttu-id="9df01-136">常見範例包括：</span><span class="sxs-lookup"><span data-stu-id="9df01-136">Common examples are:</span></span>

    - <span data-ttu-id="9df01-137">您的同盟伺服器未啟用 WS-Trust 端點</span><span class="sxs-lookup"><span data-stu-id="9df01-137">Your federation server does not have WS-Trust endpoints enabled</span></span>

    - <span data-ttu-id="9df01-138">您的同盟伺服器可能不允許來自您網路中使用「整合式 Windows 驗證」之電腦的輸入驗證。</span><span class="sxs-lookup"><span data-stu-id="9df01-138">Your federation server may not allow inbound authentication from computers in your network using Integrated Windows Authentication.</span></span>

    - <span data-ttu-id="9df01-139">在 Azure AD 中點 tooyour 驗證的網域名稱，其中 hello 電腦屬於 hello AD 樹系中沒有服務連接點物件</span><span class="sxs-lookup"><span data-stu-id="9df01-139">There is no Service Connection Point object that points tooyour verified domain name in Azure AD in hello AD forest where hello computer belongs to</span></span>

---

### <a name="domainjoined--yes"></a><span data-ttu-id="9df01-140">DomainJoined : YES</span><span class="sxs-lookup"><span data-stu-id="9df01-140">DomainJoined : YES</span></span>  

<span data-ttu-id="9df01-141">此欄位會顯示 hello 裝置是否已加入的 tooan 內部部署 Active Directory。</span><span class="sxs-lookup"><span data-stu-id="9df01-141">This field shows whether hello device is joined tooan on-premises Active Directory or not.</span></span> <span data-ttu-id="9df01-142">如果 hello 值顯示為**否**，hello 裝置無法自動註冊使用 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="9df01-142">If hello value shows as **NO**, hello device cannot auto-register with Azure AD.</span></span> <span data-ttu-id="9df01-143">請先檢查該 hello 裝置聯結 toohello 內部部署 Active Directory 之前可以向 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="9df01-143">Check first that hello device joins toohello on-premises Active Directory before it can register with Azure AD.</span></span> <span data-ttu-id="9df01-144">如果您要加入 hello 電腦 tooAzure AD 直接尋找，請移 tooLearn 有關功能的 Azure Active Directory Join。</span><span class="sxs-lookup"><span data-stu-id="9df01-144">If you are looking for joining hello computer tooAzure AD directly, please go tooLearn about capabilities of Azure Active Directory Join.</span></span>

---

### <a name="workplacejoined--no"></a><span data-ttu-id="9df01-145">WorkplaceJoined : NO</span><span class="sxs-lookup"><span data-stu-id="9df01-145">WorkplaceJoined : NO</span></span>  

<span data-ttu-id="9df01-146">此欄位會顯示 hello 裝置註冊的 Azure AD 但為個人裝置 （標示為 ' 加入工作場所 '）。</span><span class="sxs-lookup"><span data-stu-id="9df01-146">This field shows whether hello device is registered with Azure AD but as a personal device (marked as ‘Workplace Joined’).</span></span> <span data-ttu-id="9df01-147">如果向 Azure AD 註冊已加入網域電腦，這個值應顯示為 [否]，但是它會顯示為 [是]，其表示，如果工作或學校帳戶就是加入先前 toohello 電腦完成登錄。</span><span class="sxs-lookup"><span data-stu-id="9df01-147">If this value should show as ‘NO’ for a domain joined computer registered with Azure AD, however if it shows as YES it means that a work or school account was added prior toohello computer completing registration.</span></span> <span data-ttu-id="9df01-148">在此情況下若使用 hello 年度更新版的 Windows 10 (1607 當執行的 hello WinVer 命令 hello 'Run' 視窗或命令提示字元視窗)，將會忽略 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="9df01-148">In this case hello account will be ignored if using hello Anniversary Update version of Windows 10 (1607 when running hello WinVer command in hello ‘Run’ window or a command prompt window).</span></span>

---

### <a name="wamdefaultset--yes-and-azureadprt--yes"></a><span data-ttu-id="9df01-149">WamDefaultSet : YES 和 AzureADPrt : YES</span><span class="sxs-lookup"><span data-stu-id="9df01-149">WamDefaultSet : YES and AzureADPrt : YES</span></span>
  
<span data-ttu-id="9df01-150">這些欄位會顯示該 hello 使用者已成功驗證 tooAzure AD 時登入 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="9df01-150">These fields show that hello user has successfully authenticated tooAzure AD upon signing in toohello device.</span></span> <span data-ttu-id="9df01-151">如果它們顯示 'NO' hello 以下是可能的原因：</span><span class="sxs-lookup"><span data-stu-id="9df01-151">If they show ‘NO’ hello following are possible causes:</span></span>

- <span data-ttu-id="9df01-152">不正確的儲存體金鑰 (STK) 與 hello 裝置時註冊 (核取 hello KeySignTest 執行提高權限) 相關聯的 TPM。</span><span class="sxs-lookup"><span data-stu-id="9df01-152">Bad storage key (STK) in TPM associated with hello device upon registration (check hello KeySignTest while running elevated).</span></span>

- <span data-ttu-id="9df01-153">替代登入識別碼</span><span class="sxs-lookup"><span data-stu-id="9df01-153">Alternate Login ID</span></span>

- <span data-ttu-id="9df01-154">找不到 HTTP Proxy</span><span class="sxs-lookup"><span data-stu-id="9df01-154">HTTP Proxy not found</span></span>

## <a name="next-steps"></a><span data-ttu-id="9df01-155">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9df01-155">Next steps</span></span>

<span data-ttu-id="9df01-156">如需詳細資訊，請參閱 hello[自動裝置註冊常見問題集](active-directory-device-registration-faq.md)</span><span class="sxs-lookup"><span data-stu-id="9df01-156">For more information, see hello [Automatic device registration FAQ](active-directory-device-registration-faq.md)</span></span> 
