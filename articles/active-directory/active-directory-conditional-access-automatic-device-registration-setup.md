---
title: "aaaHow tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory |Microsoft 文件"
description: "設定您已加入網域的 Windows 裝置 tooregister 自動且無訊息地與 Azure Active Directory。"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 54e1b01b-03ee-4c46-bcf0-e01affc0419d
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: markvi
ms.reviewer: jairoc
ms.openlocfilehash: 6a1aab753f5456ed06ba7979ab05f70f29b4ddee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="bdb74-103">如何 tooconfigure 自動註冊的 Windows 網域的裝置與 Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="bdb74-103">How tooconfigure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="bdb74-104">toouse [Azure Active Directory 裝置型條件式存取](active-directory-conditional-access-azure-portal.md)，您的電腦必須向 Azure Active Directory (Azure AD)。</span><span class="sxs-lookup"><span data-stu-id="bdb74-104">toouse [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="bdb74-105">您可以在組織中取得一份已註冊的裝置使用 hello [Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice)指令程式在 hello [Azure Active Directory PowerShell 模組](/powershell/azure/install-msonlinev1?view=azureadps-2.0)。</span><span class="sxs-lookup"><span data-stu-id="bdb74-105">You can get a list of registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="bdb74-106">本文章提供您 hello 步驟來設定與 Azure AD 組織中的 hello 自動註冊的 Windows 網域的裝置。</span><span class="sxs-lookup"><span data-stu-id="bdb74-106">This article provides you with hello steps for configuring hello automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="bdb74-107">如需下列詳細資訊︰</span><span class="sxs-lookup"><span data-stu-id="bdb74-107">For more information about:</span></span>

- <span data-ttu-id="bdb74-108">有關條件式存取，請參閱 [Azure Active Directory 裝置型條件式存取](active-directory-conditional-access-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="bdb74-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="bdb74-109">Windows 10 裝置 hello 工作地點和增強的 hello 體驗時向 Azure AD，請參閱[hello 企業版的 Windows 10： 使用工作用裝置](active-directory-azureadjoin-windows10-devices-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="bdb74-109">Windows 10 devices in hello workplace and hello enhanced experiences when registered with Azure AD, see [Windows 10 for hello enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="bdb74-110">Windows 10 企業版 E3 中的 CSP，請參閱 hello [CSP 概觀中的 Windows 10 企業版 E3](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview)。</span><span class="sxs-lookup"><span data-stu-id="bdb74-110">Windows 10 Enterprise E3 in CSP, see hello [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="bdb74-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="bdb74-111">Before you begin</span></span>

<span data-ttu-id="bdb74-112">開始設定您的環境中的 hello 自動註冊的 Windows 網域的裝置之前，您應該熟悉 hello 支援案例和 hello 條件約束。</span><span class="sxs-lookup"><span data-stu-id="bdb74-112">Before you start configuring hello automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with hello supported scenarios and hello constraints.</span></span>  

<span data-ttu-id="bdb74-113">tooimprove hello 可讀性的 hello 描述，本主題會使用下列詞彙的 hello:</span><span class="sxs-lookup"><span data-stu-id="bdb74-113">tooimprove hello readability of hello descriptions, this topic uses hello following term:</span></span> 

- <span data-ttu-id="bdb74-114">**目前的 Windows 裝置**-此一詞是指 toodomain 聯結的裝置執行 Windows 10 或 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="bdb74-114">**Windows current devices** - This term refers toodomain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="bdb74-115">**舊版的 Windows 裝置**-此一詞是指 tooall**支援**加入網域的 Windows 裝置的非執行 Windows 10 或 Windows Server 2016。</span><span class="sxs-lookup"><span data-stu-id="bdb74-115">**Windows down-level devices** - This term refers tooall **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="bdb74-116">現行 Windows 裝置</span><span class="sxs-lookup"><span data-stu-id="bdb74-116">Windows current devices</span></span>

- <span data-ttu-id="bdb74-117">對於執行 hello Windows 桌面作業系統的裝置，我們建議使用 Windows 10 年度更新 （版本 1607年） 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="bdb74-117">For devices running hello Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="bdb74-118">hello Windows 目前裝置的註冊**是**支援在非同盟的環境，例如密碼雜湊同步處理設定。</span><span class="sxs-lookup"><span data-stu-id="bdb74-118">hello registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="bdb74-119">舊版 Windows 裝置</span><span class="sxs-lookup"><span data-stu-id="bdb74-119">Windows down-level devices</span></span>

- <span data-ttu-id="bdb74-120">支援下列舊版的 Windows 裝置 hello:</span><span class="sxs-lookup"><span data-stu-id="bdb74-120">hello following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="bdb74-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="bdb74-121">Windows 8.1</span></span>
    - <span data-ttu-id="bdb74-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="bdb74-122">Windows 7</span></span>
    - <span data-ttu-id="bdb74-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="bdb74-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="bdb74-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="bdb74-124">Windows Server 2012</span></span>
    - <span data-ttu-id="bdb74-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="bdb74-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="bdb74-126">hello 舊版的 Windows 裝置的註冊**是**透過無接縫單一登入的非同盟環境中支援[Azure Active Directory 無接縫單一登入](https://aka.ms/hybrid/sso)。</span><span class="sxs-lookup"><span data-stu-id="bdb74-126">hello registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="bdb74-127">hello 舊版的 Windows 裝置的註冊**不**支援使用漫遊設定檔的裝置。</span><span class="sxs-lookup"><span data-stu-id="bdb74-127">hello registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="bdb74-128">如果您倚賴設定檔或設定的漫遊，請使用 Windows 10。</span><span class="sxs-lookup"><span data-stu-id="bdb74-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="bdb74-129">必要條件</span><span class="sxs-lookup"><span data-stu-id="bdb74-129">Prerequisites</span></span>

<span data-ttu-id="bdb74-130">開始啟用 hello 自動登錄的組織中已加入網域的裝置之前，您需要確定您正在執行最新版的 Azure AD toomake 連接。</span><span class="sxs-lookup"><span data-stu-id="bdb74-130">Before you start enabling hello auto-registration of domain-joined devices in your organization, you need toomake sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="bdb74-131">Azure AD Connect：</span><span class="sxs-lookup"><span data-stu-id="bdb74-131">Azure AD Connect:</span></span>

- <span data-ttu-id="bdb74-132">會保留在內部部署 Active Directory (AD) 和 Azure AD 中的 hello 裝置物件中的 hello 電腦帳戶的 hello 關聯。</span><span class="sxs-lookup"><span data-stu-id="bdb74-132">Keeps hello association between hello computer account in your on-premises Active Directory (AD) and hello device object in Azure AD.</span></span> 
- <span data-ttu-id="bdb74-133">啟用其他裝置相關功能，例如 Windows Hello 企業版。</span><span class="sxs-lookup"><span data-stu-id="bdb74-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="bdb74-134">組態步驟</span><span class="sxs-lookup"><span data-stu-id="bdb74-134">Configuration steps</span></span>

<span data-ttu-id="bdb74-135">本主題包含所有的一般組態案例的 hello 必要步驟。</span><span class="sxs-lookup"><span data-stu-id="bdb74-135">This topic includes hello required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="bdb74-136">使用下列資料表 tooget 您案例所需的 hello 步驟的概觀的 hello:</span><span class="sxs-lookup"><span data-stu-id="bdb74-136">Use hello following table tooget an overview of hello steps that are required for your scenario:</span></span>  



| <span data-ttu-id="bdb74-137">步驟</span><span class="sxs-lookup"><span data-stu-id="bdb74-137">Steps</span></span>                                      | <span data-ttu-id="bdb74-138">現行 Windows 和密碼雜湊同步處理</span><span class="sxs-lookup"><span data-stu-id="bdb74-138">Windows current and password hash sync</span></span> | <span data-ttu-id="bdb74-139">現行 Windows 和同盟</span><span class="sxs-lookup"><span data-stu-id="bdb74-139">Windows current and federation</span></span> | <span data-ttu-id="bdb74-140">舊版 Windows</span><span class="sxs-lookup"><span data-stu-id="bdb74-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="bdb74-141">步驟 1︰設定服務連接點</span><span class="sxs-lookup"><span data-stu-id="bdb74-141">Step 1: Configure service connection point</span></span> | ![勾選][1]                            | ![勾選][1]                    | ![勾選][1]        |
| <span data-ttu-id="bdb74-145">步驟 2︰設定宣告的發行</span><span class="sxs-lookup"><span data-stu-id="bdb74-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![勾選][1]                    | ![勾選][1]        |
| <span data-ttu-id="bdb74-148">步驟 3︰啟用非 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="bdb74-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![勾選][1]        |
| <span data-ttu-id="bdb74-150">步驟 4︰控制部署與導入</span><span class="sxs-lookup"><span data-stu-id="bdb74-150">Step 4: Control deployment and rollout</span></span>     | ![勾選][1]                            | ![勾選][1]                    | ![勾選][1]        |
| <span data-ttu-id="bdb74-154">步驟 5︰驗證已註冊的裝置</span><span class="sxs-lookup"><span data-stu-id="bdb74-154">Step 5: Verify registered devices</span></span>          | ![勾選][1]                            | ![勾選][1]                    | ![勾選][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="bdb74-158">步驟 1︰設定服務連接點</span><span class="sxs-lookup"><span data-stu-id="bdb74-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="bdb74-159">在 hello 註冊 toodiscover Azure AD 租用戶資訊期間使用您的裝置 hello 服務連線點 (SCP) 物件。</span><span class="sxs-lookup"><span data-stu-id="bdb74-159">hello service connection point (SCP) object is used by your devices during hello registration toodiscover Azure AD tenant information.</span></span> <span data-ttu-id="bdb74-160">在您內部部署 Active Directory (AD)、 hello 自動登錄的裝置已加入網域的 hello SCP 物件必須存在於 hello 設定命名內容分割 hello 電腦樹系。</span><span class="sxs-lookup"><span data-stu-id="bdb74-160">In your on-premises Active Directory (AD), hello SCP object for hello auto-registration of domain-joined devices must exist in hello configuration naming context partition of hello computer's forest.</span></span> <span data-ttu-id="bdb74-161">每個樹系只有一個組態命名內容。</span><span class="sxs-lookup"><span data-stu-id="bdb74-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="bdb74-162">在多樹系 Active Directory 組態中，包含已加入網域的電腦的所有樹系中必須有 hello 服務連接點。</span><span class="sxs-lookup"><span data-stu-id="bdb74-162">In a multi-forest Active Directory configuration, hello service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="bdb74-163">您可以使用 hello [ **Get ADRootDSE** ](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello 設定命名內容的樹系。</span><span class="sxs-lookup"><span data-stu-id="bdb74-163">You can use hello [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet tooretrieve hello configuration naming context of your forest.</span></span>  

<span data-ttu-id="bdb74-164">Hello Active Directory 網域名稱與為樹系*fabrikam.com*，hello 設定命名內容為：</span><span class="sxs-lookup"><span data-stu-id="bdb74-164">For a forest with hello Active Directory domain name *fabrikam.com*, hello configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="bdb74-165">在您的樹系中 hello 自動登錄的裝置已加入網域的 hello SCP 物件位於：</span><span class="sxs-lookup"><span data-stu-id="bdb74-165">In your forest, hello SCP object for hello auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="bdb74-166">根據您如何部署 Azure AD Connect，hello SCP 物件可能已設定。</span><span class="sxs-lookup"><span data-stu-id="bdb74-166">Depending on how you have deployed Azure AD Connect, hello SCP object may have already been configured.</span></span>
<span data-ttu-id="bdb74-167">您可以確認 hello hello 物件存在，以及擷取使用下列 Windows PowerShell 指令碼的 hello hello 探索值：</span><span class="sxs-lookup"><span data-stu-id="bdb74-167">You can verify hello existence of hello object and retrieve hello discovery values using hello following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="bdb74-168">hello **$scp。關鍵字**輸出會顯示 hello Azure AD 租用戶的資訊，例如：</span><span class="sxs-lookup"><span data-stu-id="bdb74-168">hello **$scp.Keywords** output shows hello Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="bdb74-169">如果 hello 服務連接點不存在，可以建立執行 hello`Initialize-ADSyncDomainJoinedComputerSync`您 Azure AD Connect 的伺服器上的 cmdlet。</span><span class="sxs-lookup"><span data-stu-id="bdb74-169">If hello service connection point does not exist, you can create it by running hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="bdb74-170">企業系統管理員認證是必要的 toorun 這個指令程式。</span><span class="sxs-lookup"><span data-stu-id="bdb74-170">Enterprise admin credential is required toorun this cmdlet.</span></span>  
<span data-ttu-id="bdb74-171">hello cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bdb74-171">hello cmdlet:</span></span>

- <span data-ttu-id="bdb74-172">建立 hello 連接到 Azure AD Connect 的 Active Directory 樹系中的 hello 服務連接點。</span><span class="sxs-lookup"><span data-stu-id="bdb74-172">Creates hello service connection point in hello Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="bdb74-173">您需要 toospecify hello`AdConnectorAccount`參數。</span><span class="sxs-lookup"><span data-stu-id="bdb74-173">Requires you toospecify hello `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="bdb74-174">這是設定為 Active Directory 連接器帳戶，在 Azure AD 中的連接的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="bdb74-174">This is hello account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="bdb74-175">hello 下列指令碼範例示範使用 hello cmdlet。</span><span class="sxs-lookup"><span data-stu-id="bdb74-175">hello following script shows an example for using hello cmdlet.</span></span> <span data-ttu-id="bdb74-176">此指令碼，在`$aadAdminCred = Get-Credential`需要您 tootype 使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="bdb74-176">In this script, `$aadAdminCred = Get-Credential` requires you tootype a user name.</span></span> <span data-ttu-id="bdb74-177">您需要在 hello 使用者主要名稱 (UPN) 格式的 tooprovide hello 使用者名稱 (`user@example.com`)。</span><span class="sxs-lookup"><span data-stu-id="bdb74-177">You need tooprovide hello user name in hello user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="bdb74-178">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span><span class="sxs-lookup"><span data-stu-id="bdb74-178">hello `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="bdb74-179">使用 hello Active Directory PowerShell 模組，而這需依賴 Active Directory Web 服務的網域控制站上執行。</span><span class="sxs-lookup"><span data-stu-id="bdb74-179">Uses hello Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="bdb74-180">執行 Windows Server 2008 R2 和更新版本的網域控制站可支援 Active Directory Web 服務。</span><span class="sxs-lookup"><span data-stu-id="bdb74-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="bdb74-181">只支援 hello **MSOnline PowerShell 模組版本 1.1.166.0**。</span><span class="sxs-lookup"><span data-stu-id="bdb74-181">Is only supported by hello **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="bdb74-182">toodownload 這個模組中使用這個[連結](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)。</span><span class="sxs-lookup"><span data-stu-id="bdb74-182">toodownload this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="bdb74-183">執行 Windows Server 2008 或更早版本的網域控制站，使用下列 toocreate hello 服務連接點的 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="bdb74-183">For domain controllers running Windows Server 2008 or earlier versions, use hello script below toocreate hello service connection point.</span></span>

<span data-ttu-id="bdb74-184">在多樹系組態中，您應該使用下列指令碼 toocreate hello 服務連接點電腦所在的每個樹系中的 hello:</span><span class="sxs-lookup"><span data-stu-id="bdb74-184">In a multi-forest configuration, you should use hello following script toocreate hello service connection point in each forest where computers exist:</span></span>
 
    $verifiedDomain = "contoso.com"    # Replace this with any of your verified domain names in Azure AD
    $tenantID = "72f988bf-86f1-41af-91ab-2d7cd011db47"    # Replace this with you tenant ID
    $configNC = "CN=Configuration,DC=corp,DC=contoso,DC=com"    # Replace this with your AD configuration naming context

    $de = New-Object System.DirectoryServices.DirectoryEntry
    $de.Path = "LDAP://CN=Services," + $configNC

    $deDRC = $de.Children.Add("CN=Device Registration Configuration", "container")
    $deDRC.CommitChanges()

    $deSCP = $deDRC.Children.Add("CN=62a0ff2e-97b9-4513-943f-0d221bd30080", "serviceConnectionPoint")
    $deSCP.Properties["keywords"].Add("azureADName:" + $verifiedDomain)
    $deSCP.Properties["keywords"].Add("azureADId:" + $tenantID)

    $deSCP.CommitChanges()


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="bdb74-185">步驟 2︰設定宣告的發行</span><span class="sxs-lookup"><span data-stu-id="bdb74-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="bdb74-186">在同盟的 Azure AD 設定裝置依賴 Active Directory Federation Services (AD FS)，或第 3 個合作對象在內部部署同盟服務 tooauthenticate tooAzure AD。</span><span class="sxs-lookup"><span data-stu-id="bdb74-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service tooauthenticate tooAzure AD.</span></span> <span data-ttu-id="bdb74-187">裝置驗證 tooget 存取語彙基元 tooregister 針對 hello Azure Active Directory 裝置註冊服務 (Azure DRS)。</span><span class="sxs-lookup"><span data-stu-id="bdb74-187">Devices authenticate tooget an access token tooregister against hello Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="bdb74-188">使用整合式 Windows 驗證 tooan active Ws-trust （1.3 或 2005年版） 裝載端點 hello 內部 federation service 進行驗證的目前裝置的 Windows。</span><span class="sxs-lookup"><span data-stu-id="bdb74-188">Windows current devices authenticate using Integrated Windows Authentication tooan active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by hello on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="bdb74-189">使用 AD FS 時，必須啟用 **adfs/services/trust/13/windowstransport** 或 **adfs/services/trust/2005/windowstransport**。</span><span class="sxs-lookup"><span data-stu-id="bdb74-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="bdb74-190">如果您使用 hello Web 驗證 Proxy，也請確定此端點會透過 hello proxy 發佈。</span><span class="sxs-lookup"><span data-stu-id="bdb74-190">If you are using hello Web Authentication Proxy, also ensure that this endpoint is published through hello proxy.</span></span> <span data-ttu-id="bdb74-191">您可以看到哪些端點會透過 hello AD FS 管理主控台的 啟用**服務 > 端點**。</span><span class="sxs-lookup"><span data-stu-id="bdb74-191">You can see what end-points are enabled through hello AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="bdb74-192">如果您沒有為您在內部部署的 federation service AD FS，請依照 您確定它們支援 Ws-trust 1.3 或 2005年端點，這些會發佈到 hello 的檔案中繼資料交換 (MEX) 的廠商 toomake hello 指示進行。</span><span class="sxs-lookup"><span data-stu-id="bdb74-192">If you don’t have AD FS as your on-premises federation service, follow hello instructions of your vendor toomake sure they support WS-Trust 1.3 or 2005 end-points and that these are published through hello Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="bdb74-193">hello 下列宣告必須存在於 Azure DRS 的裝置註冊 toocomplete 收到 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="bdb74-193">hello following claims must exist in hello token received by Azure DRS for device registration toocomplete.</span></span> <span data-ttu-id="bdb74-194">Azure DRS 會在某些這項資訊接著 hello 電腦帳戶在內部部署與 Azure AD Connect tooassociate hello 新建立的裝置物件所使用的 Azure AD 中建立裝置物件。</span><span class="sxs-lookup"><span data-stu-id="bdb74-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect tooassociate hello newly created device object with hello computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="bdb74-195">如果您有多個已驗證的網域名稱，您需要下列宣告電腦的 tooprovide hello:</span><span class="sxs-lookup"><span data-stu-id="bdb74-195">If you have more than one verified domain name, you need tooprovide hello following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="bdb74-196">如果您已發行的 ImmutableID 的宣告 （例如，替代登入識別碼） 會需要 tooprovide 一個對應的宣告的電腦：</span><span class="sxs-lookup"><span data-stu-id="bdb74-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need tooprovide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="bdb74-197">在 hello 下列各節，尋找的相關資訊：</span><span class="sxs-lookup"><span data-stu-id="bdb74-197">In hello following sections, you find information about:</span></span>
 
- <span data-ttu-id="bdb74-198">每個宣告應該有 hello 值</span><span class="sxs-lookup"><span data-stu-id="bdb74-198">hello values each claim should have</span></span>
- <span data-ttu-id="bdb74-199">定義在 AD FS 中看起來如何</span><span class="sxs-lookup"><span data-stu-id="bdb74-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="bdb74-200">hello 定義可協助您 tooverify hello 值是否存在，或如果您需要 toocreate 它們。</span><span class="sxs-lookup"><span data-stu-id="bdb74-200">hello definition helps you tooverify whether hello values are present or if you need toocreate them.</span></span>

> [!NOTE]
> <span data-ttu-id="bdb74-201">如果您不使用 AD FS 進行您在內部部署的同盟伺服器，請遵循廠商的指示 toocreate hello 適當的組態 tooissue 這些宣告。</span><span class="sxs-lookup"><span data-stu-id="bdb74-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions toocreate hello appropriate configuration tooissue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="bdb74-202">發出帳戶類型宣告</span><span class="sxs-lookup"><span data-stu-id="bdb74-202">Issue account type claim</span></span>

<span data-ttu-id="bdb74-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`**-此宣告必須包含值為**DJ**，其可識別 hello 裝置做為已加入網域的電腦。</span><span class="sxs-lookup"><span data-stu-id="bdb74-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies hello device as a domain-joined computer.</span></span> <span data-ttu-id="bdb74-204">在 AD FS 中，您可以新增發行轉換規則，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="bdb74-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );

### <a name="issue-objectguid-of-hello-computer-account-on-premises"></a><span data-ttu-id="bdb74-205">發出 objectGUID hello 電腦帳戶在內部</span><span class="sxs-lookup"><span data-stu-id="bdb74-205">Issue objectGUID of hello computer account on-premises</span></span>

<span data-ttu-id="bdb74-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`**-此宣告必須包含 hello **objectGUID** hello 的值在內部部署電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="bdb74-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain hello **objectGUID** value of hello on-premises computer account.</span></span> <span data-ttu-id="bdb74-207">在 AD FS 中，您可以新增發行轉換規則，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="bdb74-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );
 
### <a name="issue-objectsid-of-hello-computer-account-on-premises"></a><span data-ttu-id="bdb74-208">發出 hello 電腦帳戶在內部的 objectSID</span><span class="sxs-lookup"><span data-stu-id="bdb74-208">Issue objectSID of hello computer account on-premises</span></span>

<span data-ttu-id="bdb74-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`**-此宣告必須包含 hello hello **objectSid** hello 的值在內部部署電腦帳戶。</span><span class="sxs-lookup"><span data-stu-id="bdb74-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain hello hello **objectSid** value of hello on-premises computer account.</span></span> <span data-ttu-id="bdb74-210">在 AD FS 中，您可以新增發行轉換規則，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="bdb74-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

    @RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="bdb74-211">當 Azure AD 中有多個經過驗證的網域名稱時，發出電腦的 issuerID</span><span class="sxs-lookup"><span data-stu-id="bdb74-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="bdb74-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`**-此宣告必須包含的 hello 任何 hello 的統一資源識別元 (URI) 驗證網域名稱與 hello 連接內部部署同盟服務 （AD FS 或第 3 個合作對象） 發行 hello 語彙基元。</span><span class="sxs-lookup"><span data-stu-id="bdb74-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain hello Uniform Resource Identifier (URI) of any of hello verified domain names that connect with hello on-premises federation service (AD FS or 3rd party) issuing hello token.</span></span> <span data-ttu-id="bdb74-213">在 AD FS 中，您可以加入發行轉換規則看起來像是 hello 的下方之後, 的特定順序 hello 的上方。</span><span class="sxs-lookup"><span data-stu-id="bdb74-213">In AD FS, you can add issuance transform rules that look like hello ones below in that specific order after hello ones above.</span></span> <span data-ttu-id="bdb74-214">請使用者為必要，注意，一個 tooexplicitly 問題 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="bdb74-214">Please note that one rule tooexplicitly issue hello rule for users is necessary.</span></span> <span data-ttu-id="bdb74-215">在下列 hello 規則，會加入第一個規則，用來識別使用者與電腦驗證。</span><span class="sxs-lookup"><span data-stu-id="bdb74-215">In hello rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with hello value User when its not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://<verified-domain-name>/adfs/services/trust/"
    );


<span data-ttu-id="bdb74-216">在上述的 hello 宣告</span><span class="sxs-lookup"><span data-stu-id="bdb74-216">In hello claim above,</span></span>

- <span data-ttu-id="bdb74-217">`$<domain>`hello AD FS 服務 url</span><span class="sxs-lookup"><span data-stu-id="bdb74-217">`$<domain>` is hello AD FS service URL</span></span>
- <span data-ttu-id="bdb74-218">`<verified-domain-name>`是您需要使用其中一個已驗證的網域名稱 tooreplace 在 Azure AD 中的預留位置</span><span class="sxs-lookup"><span data-stu-id="bdb74-218">`<verified-domain-name>` is a placeholder you need tooreplace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="bdb74-219">如需有關驗證的網域名稱的詳細資訊，請參閱[新增自訂網域名稱 tooAzure Active Directory](active-directory-add-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="bdb74-219">For more details about verified domain names, see [Add a custom domain name tooAzure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="bdb74-220">tooget 已驗證的公司網域的清單，您可以使用 hello [Get-msoldomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="bdb74-220">tooget a list of your verified company domains, you can use hello [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="bdb74-222">當使用者存在 ImmutableID (例如已設定替代登入識別碼) 時，請發出電腦的 ImmutableID</span><span class="sxs-lookup"><span data-stu-id="bdb74-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="bdb74-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - 此宣告必須包含電腦的有效值。</span><span class="sxs-lookup"><span data-stu-id="bdb74-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="bdb74-224">在 AD FS 中，您可以新增發行轉換規則，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="bdb74-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

    @RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );

### <a name="helper-script-toocreate-hello-ad-fs-issuance-transform-rules"></a><span data-ttu-id="bdb74-225">協助程式指令碼 toocreate hello AD FS 發行轉換規則</span><span class="sxs-lookup"><span data-stu-id="bdb74-225">Helper script toocreate hello AD FS issuance transform rules</span></span>

<span data-ttu-id="bdb74-226">hello 下列指令碼可協助您建立 hello hello 發行轉換規則上面所述。</span><span class="sxs-lookup"><span data-stu-id="bdb74-226">hello following script helps you with hello creation of hello issuance transform rules described above.</span></span>

    $multipleVerifiedDomainNames = $false
    $immutableIDAlreadyIssuedforUsers = $false
    $oneOfVerifiedDomainNames = 'example.com'   # Replace example.com with one of your verified domains
    
    $rule1 = '@RuleName = "Issue account type for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "DJ"
    );'

    $rule2 = '@RuleName = "Issue object GUID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/identity/claims/onpremobjectguid"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'

    $rule3 = '@RuleName = "Issue objectSID for domain-joined computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(claim = c2);'

    $rule4 = ''
    if ($multipleVerifiedDomainNames -eq $true) {
    $rule4 = '@RuleName = "Issue account type with hello value User when it is not a computer"
    NOT EXISTS(
    [
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "DJ"
    ]
    )
    => add(
        Type = "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value = "User"
    );
    
    @RuleName = "Capture UPN when AccountType is User and issue hello IssuerID"
    c1:[
        Type == "http://schemas.xmlsoap.org/claims/UPN"
    ]
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2012/01/accounttype", 
        Value == "User"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = regexreplace(
        c1.Value, 
        ".+@(?<domain>.+)", 
        "http://${domain}/adfs/services/trust/"
        )
    );
    
    @RuleName = "Issue issuerID for domain-joined computers"
    c:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", 
        Value = "http://' + $oneOfVerifiedDomainNames + '/adfs/services/trust/"
    );'
    }

    $rule5 = ''
    if ($immutableIDAlreadyIssuedforUsers -eq $true) {
    $rule5 = '@RuleName = "Issue ImmutableID for computers"
    c1:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/groupsid", 
        Value =~ "-515$", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ] 
    && 
    c2:[
        Type == "http://schemas.microsoft.com/ws/2008/06/identity/claims/windowsaccountname", 
        Issuer =~ "^(AD AUTHORITY|SELF AUTHORITY|LOCAL AUTHORITY)$"
    ]
    => issue(
        store = "Active Directory", 
        types = ("http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID"), 
        query = ";objectguid;{0}", 
        param = c2.Value
    );'
    }

    $existingRules = (Get-ADFSRelyingPartyTrust -Identifier urn:federation:MicrosoftOnline).IssuanceTransformRules 

    $updatedRules = $existingRules + $rule1 + $rule2 + $rule3 + $rule4 + $rule5

    $crSet = New-ADFSClaimRuleSet -ClaimRule $updatedRules 

    Set-AdfsRelyingPartyTrust -TargetIdentifier urn:federation:MicrosoftOnline -IssuanceTransformRules $crSet.ClaimRulesString 

### <a name="remarks"></a><span data-ttu-id="bdb74-227">備註</span><span class="sxs-lookup"><span data-stu-id="bdb74-227">Remarks</span></span> 

- <span data-ttu-id="bdb74-228">此指令碼會附加 hello 規則 toohello 現有規則。</span><span class="sxs-lookup"><span data-stu-id="bdb74-228">This script appends hello rules toohello existing rules.</span></span> <span data-ttu-id="bdb74-229">不會執行 hello 指令碼兩次，因為 hello 設定的規則將會新增兩次。</span><span class="sxs-lookup"><span data-stu-id="bdb74-229">Do not run hello script twice because hello set of rules would be added twice.</span></span> <span data-ttu-id="bdb74-230">請確定沒有對應的規則存在這些宣告 （hello 對應在情況下），才能再次執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="bdb74-230">Make sure that no corresponding rules exist for these claims (under hello corresponding conditions) before running hello script again.</span></span>

- <span data-ttu-id="bdb74-231">如果您有多個已驗證的網域名稱 （如所示 hello Azure AD 入口網站或透過 hello Get MsolDomains cmdlet），來設定 hello 值**$multipleVerifiedDomainNames** hello 中編寫的指令碼太**$true**。</span><span class="sxs-lookup"><span data-stu-id="bdb74-231">If you have multiple verified domain names (as shown in hello Azure AD portal or via hello Get-MsolDomains cmdlet), set hello value of **$multipleVerifiedDomainNames** in hello script too**$true**.</span></span> <span data-ttu-id="bdb74-232">此外，也務必移除經由 Azure AD Connect 或透過其他方式所建立的任何現有 issuerid 宣告。</span><span class="sxs-lookup"><span data-stu-id="bdb74-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="bdb74-233">此規則的範例如下︰</span><span class="sxs-lookup"><span data-stu-id="bdb74-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="bdb74-234">如果您已經發出**ImmutableID**宣告的使用者帳戶，來設定 hello 值**$immutableIDAlreadyIssuedforUsers** hello 中編寫的指令碼太**$true**。</span><span class="sxs-lookup"><span data-stu-id="bdb74-234">If you have already issued an **ImmutableID** claim  for user accounts, set hello value of **$immutableIDAlreadyIssuedforUsers** in hello script too**$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="bdb74-235">步驟 3：啟用舊版 Windows 裝置</span><span class="sxs-lookup"><span data-stu-id="bdb74-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="bdb74-236">如果有些已加入網域的裝置是舊版 Windows 裝置，您需要︰</span><span class="sxs-lookup"><span data-stu-id="bdb74-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="bdb74-237">在 Azure AD tooenable 使用者 tooregister 裝置設定的原則。</span><span class="sxs-lookup"><span data-stu-id="bdb74-237">Set a policy in Azure AD tooenable users tooregister devices.</span></span>
 
- <span data-ttu-id="bdb74-238">設定您在內部部署同盟服務 tooissue 宣告 toosupport**整合式 Windows 驗證 (IWA)**註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="bdb74-238">Configure your on-premises federation service tooissue claims toosupport **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="bdb74-239">新增 hello Azure AD 裝置驗證端點 toohello 本機內部網路區域驗證 hello 裝置時，會提示 tooavoid 憑證。</span><span class="sxs-lookup"><span data-stu-id="bdb74-239">Add hello Azure AD device authentication end-point toohello local Intranet zones tooavoid certificate prompts when authenticating hello device.</span></span>

### <a name="set-policy-in-azure-ad-tooenable-users-tooregister-devices"></a><span data-ttu-id="bdb74-240">在 Azure AD tooenable 中使用者 tooregister 裝置設定原則</span><span class="sxs-lookup"><span data-stu-id="bdb74-240">Set policy in Azure AD tooenable users tooregister devices</span></span>

<span data-ttu-id="bdb74-241">tooregister Windows 下層裝置，您需要確定已設定該設定 tooallow 使用者 tooregister 裝置在 Azure AD 中的 hello toomake。</span><span class="sxs-lookup"><span data-stu-id="bdb74-241">tooregister Windows down-level devices, you need toomake sure that hello setting tooallow users tooregister devices in Azure AD is set.</span></span> <span data-ttu-id="bdb74-242">在 hello Azure 入口網站，您可以找到此設定下：</span><span class="sxs-lookup"><span data-stu-id="bdb74-242">In hello Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="bdb74-243">hello 下列原則必須設定太**所有**:**使用者可以向 Azure AD 註冊其裝置**</span><span class="sxs-lookup"><span data-stu-id="bdb74-243">hello following policy must be set too**All**: **Users may register their devices with Azure AD**</span></span>

![註冊裝置](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="bdb74-245">設定內部部署同盟服務</span><span class="sxs-lookup"><span data-stu-id="bdb74-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="bdb74-246">您在內部部署的同盟服務必須支援發行 hello **authenticationmehod**和**wiaormultiauthn**宣告時收到的驗證要求保留 toohello Azure AD 信賴憑證者合作對象resouce_params 參數編碼值，以顯示下列：</span><span class="sxs-lookup"><span data-stu-id="bdb74-246">Your on-premises federation service must support issuing hello **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request toohello Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="bdb74-247">這類要求時，hello 內部同盟服務必須驗證 hello 使用者使用整合式 Windows 驗證，並成功時，它必須發出下列兩個宣告的 hello:</span><span class="sxs-lookup"><span data-stu-id="bdb74-247">When such a request comes, hello on-premises federation service must authenticate hello user using Integrated Windows Authentication and upon success, it must issue hello following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="bdb74-248">在 AD FS 中，您必須加入該階段透過 hello 驗證方法的發行轉換規則。</span><span class="sxs-lookup"><span data-stu-id="bdb74-248">In AD FS, you must add an issuance transform rule that passes-through hello authentication method.</span></span>  

<span data-ttu-id="bdb74-249">**tooadd 此規則：**</span><span class="sxs-lookup"><span data-stu-id="bdb74-249">**tooadd this rule:**</span></span>

1. <span data-ttu-id="bdb74-250">在 hello AD FS 管理主控台中，移過`AD FS > Trust Relationships > Relying Party Trusts`。</span><span class="sxs-lookup"><span data-stu-id="bdb74-250">In hello AD FS management console, go too`AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="bdb74-251">Hello Microsoft Office 365 識別平台信賴憑證者信任物件，以滑鼠右鍵按一下，然後選取**編輯宣告規則**。</span><span class="sxs-lookup"><span data-stu-id="bdb74-251">Right-click hello Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="bdb74-252">在 hello**發行轉換規則**索引標籤上，選取**加入規則**。</span><span class="sxs-lookup"><span data-stu-id="bdb74-252">On hello **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="bdb74-253">在 hello**宣告規則**範本清單中，選取**使用自訂規則傳送宣告**。</span><span class="sxs-lookup"><span data-stu-id="bdb74-253">In hello **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="bdb74-254">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="bdb74-254">Select **Next**.</span></span>
6. <span data-ttu-id="bdb74-255">在 hello**宣告規則名稱**方塊中，輸入**驗證方法宣告規則**。</span><span class="sxs-lookup"><span data-stu-id="bdb74-255">In hello **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="bdb74-256">在 [hello**宣告規則**] 方塊中，下列規則類型 hello:</span><span class="sxs-lookup"><span data-stu-id="bdb74-256">In hello **Claim rule** box, type hello following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="bdb74-257">在同盟伺服器上，輸入下面的 hello PowerShell 命令來取代之後 **\<RPObjectName\>** 與 hello 信賴憑證者合作對象的物件名稱您 Azure AD 信賴憑證者信任物件。</span><span class="sxs-lookup"><span data-stu-id="bdb74-257">On your federation server, type hello PowerShell command below after replacing **\<RPObjectName\>** with hello relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="bdb74-258">此物件通常名為「Microsoft Office 365 身分識別平台」。</span><span class="sxs-lookup"><span data-stu-id="bdb74-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-hello-azure-ad-device-authentication-end-point-toohello-local-intranet-zones"></a><span data-ttu-id="bdb74-259">新增 hello Azure AD 裝置驗證端點 toohello 近端內部網路區域</span><span class="sxs-lookup"><span data-stu-id="bdb74-259">Add hello Azure AD device authentication end-point toohello Local Intranet zones</span></span>

<span data-ttu-id="bdb74-260">註冊裝置中的使用者驗證 tooAzure 可以是您推送下列 URL toohello 近端內部網路區域，在 Internet Explorer 原則 tooyour 已加入網域裝置 tooadd hello AD 時，會提示 tooavoid 憑證：</span><span class="sxs-lookup"><span data-stu-id="bdb74-260">tooavoid certificate prompts when users in register devices authenticate tooAzure AD you can push a policy tooyour domain-joined devices tooadd hello following URL toohello Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="bdb74-261">步驟 4︰控制部署與導入</span><span class="sxs-lookup"><span data-stu-id="bdb74-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="bdb74-262">當您完成 hello 所需的步驟時，加入網域的裝置會準備 tooautomatically 向 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="bdb74-262">When you have completed hello required steps, domain-joined devices are ready tooautomatically register with Azure AD.</span></span> <span data-ttu-id="bdb74-263">所有已加入網域且執行 Windows 10 年度更新版和 Windows Server 2016 的裝置會在裝置重新啟動或使用者登入時自動向 Azure AD 註冊。</span><span class="sxs-lookup"><span data-stu-id="bdb74-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="bdb74-264">Hello 網域聯結作業執行完成之後 hello 裝置將重新啟動時的 Azure AD 中註冊新裝置。</span><span class="sxs-lookup"><span data-stu-id="bdb74-264">New devices register with Azure AD when hello device restarts after hello domain join operation is completed.</span></span>

<span data-ttu-id="bdb74-265">過了先前的工作地方聯結 tooAzure AD （例如針對 Intune) 轉換的裝置 」*已加入網域，AAD 已登錄*"; 不過花一些時間的這個程序 toocomplete 到期 toohello 標準的所有裝置上網域和使用者活動流程。</span><span class="sxs-lookup"><span data-stu-id="bdb74-265">Devices that were previously workplace-joined tooAzure AD (for example for Intune) transition too“*Domain Joined, AAD Registered*”; however it takes some time for this process toocomplete across all devices due toohello normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="bdb74-266">備註</span><span class="sxs-lookup"><span data-stu-id="bdb74-266">Remarks</span></span>

- <span data-ttu-id="bdb74-267">您可以使用群組原則物件 toocontrol hello 首度發行的 Windows 10 和 Windows Server 2016 網域的電腦自動註冊。</span><span class="sxs-lookup"><span data-stu-id="bdb74-267">You can use a Group Policy object toocontrol hello rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="bdb74-268">Windows 10 11 月版 2015年更新自動暫存器與 Azure AD**只**如果 hello 首度發行的群組原則物件設定。</span><span class="sxs-lookup"><span data-stu-id="bdb74-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if hello rollout Group Policy object is set.</span></span>

- <span data-ttu-id="bdb74-269">您可以部署 toorollout hello 自動註冊的 Windows 下層電腦[Windows Installer 套件](#windows-installer-packages-for-non-windows-10-computers)toocomputers 您選取。</span><span class="sxs-lookup"><span data-stu-id="bdb74-269">toorollout hello automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) toocomputers that you select.</span></span>

- <span data-ttu-id="bdb74-270">如果您推送 hello 群組原則物件 tooWindows 8.1 已加入網域的裝置，就會嘗試註冊;不過最好是您使用 hello [Windows Installer 套件](#windows-installer-packages-for-non-windows-10-computers)tooregister 所有 Windows 下層裝置。</span><span class="sxs-lookup"><span data-stu-id="bdb74-270">If you push hello Group Policy object tooWindows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use hello [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) tooregister all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="bdb74-271">建立群組原則物件</span><span class="sxs-lookup"><span data-stu-id="bdb74-271">Create a Group Policy object</span></span> 

<span data-ttu-id="bdb74-272">toocontrol hello 首度發行目前的 Windows 電腦的自動註冊，您應該部署 hello**做為裝置註冊加入網域的電腦**想 tooregister 的群組原則物件 toohello 裝置。</span><span class="sxs-lookup"><span data-stu-id="bdb74-272">toocontrol hello rollout of automatic registration of Windows current computers, you should deploy hello **Register domain-joined computers as devices** Group Policy object toohello devices you want tooregister.</span></span> <span data-ttu-id="bdb74-273">例如，您可以部署 hello 原則 tooan 組織單位或 tooa 安全性群組。</span><span class="sxs-lookup"><span data-stu-id="bdb74-273">For example, you can deploy hello policy tooan organizational unit or tooa security group.</span></span>

<span data-ttu-id="bdb74-274">**tooset hello 原則：**</span><span class="sxs-lookup"><span data-stu-id="bdb74-274">**tooset hello policy:**</span></span>

1. <span data-ttu-id="bdb74-275">開啟**伺服器管理員**，然後前往太`Tools > Group Policy Management`。</span><span class="sxs-lookup"><span data-stu-id="bdb74-275">Open **Server Manager**, and then go too`Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="bdb74-276">請移至 toohello 網域節點對應 toohello 想 tooactivate 自動登錄，目前的 Windows 電腦的網域。</span><span class="sxs-lookup"><span data-stu-id="bdb74-276">Go toohello domain node that corresponds toohello domain where you want tooactivate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="bdb74-277">在 [群組原則物件] 上按一下滑鼠右鍵，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="bdb74-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="bdb74-278">輸入群組原則物件的名稱。</span><span class="sxs-lookup"><span data-stu-id="bdb74-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="bdb74-279">例如，*自動註冊 tooAzure AD*。</span><span class="sxs-lookup"><span data-stu-id="bdb74-279">For example, *Automatic Registration tooAzure AD*.</span></span> <span data-ttu-id="bdb74-280">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="bdb74-280">Select **OK**.</span></span>
5. <span data-ttu-id="bdb74-281">以滑鼠右鍵按一下新的群組原則物件，然後選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="bdb74-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="bdb74-282">跳過**電腦設定** > **原則** > **系統管理範本** > **Windows元件** > **裝置註冊**。</span><span class="sxs-lookup"><span data-stu-id="bdb74-282">Go too**Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="bdb74-283">以滑鼠右鍵按一下 [將已加入網域的電腦註冊為裝置]，然後選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="bdb74-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="bdb74-284">此群組原則範本已從舊版的 hello 群組原則管理主控台中重新命名。</span><span class="sxs-lookup"><span data-stu-id="bdb74-284">This Group Policy template has been renamed from earlier versions of hello Group Policy Management console.</span></span> <span data-ttu-id="bdb74-285">如果您使用舊版的 hello 主控台，請移至太`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`。</span><span class="sxs-lookup"><span data-stu-id="bdb74-285">If you are using an earlier version of hello console, go too`Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="bdb74-286">選取 [已啟用]，然後選取 [套用]。</span><span class="sxs-lookup"><span data-stu-id="bdb74-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="bdb74-287">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="bdb74-287">Select **OK**.</span></span>
9. <span data-ttu-id="bdb74-288">連結 hello 群組原則物件 tooa 您選擇的位置。</span><span class="sxs-lookup"><span data-stu-id="bdb74-288">Link hello Group Policy object tooa location of your choice.</span></span> <span data-ttu-id="bdb74-289">例如，您可以將它連結 tooa 特定組織單位。</span><span class="sxs-lookup"><span data-stu-id="bdb74-289">For example, you can link it tooa specific organizational unit.</span></span> <span data-ttu-id="bdb74-290">您也可以將它連結 tooa 特定安全性群自動向 Azure AD 的電腦。</span><span class="sxs-lookup"><span data-stu-id="bdb74-290">You also could link it tooa specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="bdb74-291">tooset 此原則中的所有已加入網域的 Windows 10 和 Windows Server 2016 電腦組織連結 hello 群組原則物件 toohello 網域。</span><span class="sxs-lookup"><span data-stu-id="bdb74-291">tooset this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link hello Group Policy object toohello domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="bdb74-292">非 Windows 10 電腦的 Windows Installer 套件</span><span class="sxs-lookup"><span data-stu-id="bdb74-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="bdb74-293">tooregister 加入網域的 Windows 下層電腦在同盟環境中，您可以下載並安裝從下載中心取得這些 Windows Installer 套件 (.msi)，在 hello[非 Windows 10 電腦的Microsoft工作地方聯結](https://www.microsoft.com/en-us/download/details.aspx?id=53554)頁面。</span><span class="sxs-lookup"><span data-stu-id="bdb74-293">tooregister domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at hello [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="bdb74-294">您可以使用軟體分派系統像 System Center Configuration Manager 部署 hello 封裝。</span><span class="sxs-lookup"><span data-stu-id="bdb74-294">You can deploy hello package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="bdb74-295">hello 封裝支援 hello 標準的無訊息安裝選項以 hello*安靜*參數。</span><span class="sxs-lookup"><span data-stu-id="bdb74-295">hello package supports hello standard silent install options with hello *quiet* parameter.</span></span> <span data-ttu-id="bdb74-296">System Center Configuration Manager 最新分支會提供額外的好處，從較早的版本，例如 hello 能力 tootrack 完成註冊。</span><span class="sxs-lookup"><span data-stu-id="bdb74-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like hello ability tootrack completed registrations.</span></span> <span data-ttu-id="bdb74-297">如需詳細資訊，請參閱 [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager)。</span><span class="sxs-lookup"><span data-stu-id="bdb74-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="bdb74-298">hello installer hello hello 使用者內容中執行的系統上建立排定的工作。</span><span class="sxs-lookup"><span data-stu-id="bdb74-298">hello installer creates a scheduled task on hello system that runs in hello user’s context.</span></span> <span data-ttu-id="bdb74-299">hello 使用者登入時 tooWindows 觸發 hello 工作。</span><span class="sxs-lookup"><span data-stu-id="bdb74-299">hello task is triggered when hello user signs in tooWindows.</span></span> <span data-ttu-id="bdb74-300">hello 工作以無訊息方式註冊 hello 裝置與 Azure AD 與 hello 使用者認證驗證使用整合式 Windows 驗證之後。</span><span class="sxs-lookup"><span data-stu-id="bdb74-300">hello task silently registers hello device with Azure AD with hello user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="bdb74-301">toosee hello 排程的工作，請在 hello 裝置跳過**Microsoft** > **工作地點加入**，並前往 toohello 工作排程器程式庫。</span><span class="sxs-lookup"><span data-stu-id="bdb74-301">toosee hello scheduled task, in hello device, go too**Microsoft** > **Workplace Join**, and then go toohello Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="bdb74-302">步驟 5︰驗證已註冊的裝置</span><span class="sxs-lookup"><span data-stu-id="bdb74-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="bdb74-303">您也可以使用 hello 您組織中查看已註冊的裝置成功[Get MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice)指令程式在 hello [Azure Active Directory PowerShell 模組](/powershell/azure/install-msonlinev1?view=azureadps-2.0)。</span><span class="sxs-lookup"><span data-stu-id="bdb74-303">You can check successful registered devices in your organization by using hello [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in hello [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="bdb74-304">此 cmdlet 的 hello 輸出會顯示在 Azure AD 中註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="bdb74-304">hello output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="bdb74-305">tooget 所有裝置，都使用 hello **-所有**參數，然後再篩選它們使用 hello **deviceTrustType**屬性。</span><span class="sxs-lookup"><span data-stu-id="bdb74-305">tooget all devices, use hello **-All** parameter, and then filter them using hello **deviceTrustType** property.</span></span> <span data-ttu-id="bdb74-306">已加入網域的裝置具有**已加入網域**這個值。</span><span class="sxs-lookup"><span data-stu-id="bdb74-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bdb74-307">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bdb74-307">Next steps</span></span>

* [<span data-ttu-id="bdb74-308">自動裝置註冊常見問題集</span><span class="sxs-lookup"><span data-stu-id="bdb74-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="bdb74-309">疑難排解自動登錄的網域加入電腦 tooAzure AD – Windows 10 和 Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="bdb74-309">Troubleshooting auto-registration of domain joined computers tooAzure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="bdb74-310">疑難排解自動登錄的網域加入電腦 tooAzure AD – 非 Windows 10</span><span class="sxs-lookup"><span data-stu-id="bdb74-310">Troubleshooting auto-registration of domain joined computers tooAzure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="bdb74-311">Azure Active Directory 條件式存取</span><span class="sxs-lookup"><span data-stu-id="bdb74-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
