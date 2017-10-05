---
title: "如何設定讓已加入網域的 Windows 裝置自動向 Azure Active Directory 註冊 | Microsoft Docs"
description: "設定讓已加入網域的 Windows 裝置以自動和無訊息方式向 Azure Active Directory 註冊。"
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
ms.openlocfilehash: dccd7df6a5f85df4179c7ea7cfc476cfb57f48c0
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-configure-automatic-registration-of-windows-domain-joined-devices-with-azure-active-directory"></a><span data-ttu-id="3d2f8-103">如何設定讓已加入網域的 Windows 裝置自動向 Azure Active Directory 註冊</span><span class="sxs-lookup"><span data-stu-id="3d2f8-103">How to configure automatic registration of Windows domain-joined devices with Azure Active Directory</span></span>

<span data-ttu-id="3d2f8-104">若要使用 [Azure Active Directory 裝置型條件式存取](active-directory-conditional-access-azure-portal.md)，電腦必須向 Azure Active Directory (Azure AD) 註冊。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-104">To use [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md), your computers must be registered with Azure Active Directory (Azure AD).</span></span> <span data-ttu-id="3d2f8-105">您可以在 [Azure Active Directory PowerShell 模組](/powershell/azure/install-msonlinev1?view=azureadps-2.0) 中使用 [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) Cmdlet，以取得您組織中已註冊的裝置清單。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-105">You can get a list of registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span> 

<span data-ttu-id="3d2f8-106">本文會提供可供設定讓已加入網域的 Windows 裝置自動向組織中之 Azure AD 註冊的相關步驟。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-106">This article provides you with the steps for configuring the automatic registration of Windows domain-joined devices with Azure AD in your organization.</span></span>


<span data-ttu-id="3d2f8-107">如需下列詳細資訊︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-107">For more information about:</span></span>

- <span data-ttu-id="3d2f8-108">有關條件式存取，請參閱 [Azure Active Directory 裝置型條件式存取](active-directory-conditional-access-azure-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-108">Conditional access, see [Azure Active Directory device-based conditional access](active-directory-conditional-access-azure-portal.md).</span></span> 
- <span data-ttu-id="3d2f8-109">有關工作場所中的 Windows 10 裝置以及向 Azure AD 註冊後的進階體驗，請參閱[適合企業使用的 Windows 10：使用裝置處理工作](active-directory-azureadjoin-windows10-devices-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-109">Windows 10 devices in the workplace and the enhanced experiences when registered with Azure AD, see [Windows 10 for the enterprise: Use devices for work](active-directory-azureadjoin-windows10-devices-overview.md).</span></span>
- <span data-ttu-id="3d2f8-110">CSP 中的 Windows 10 企業版 E3，請參閱 [CSP 中的 Windows 10 企業版 E3 概觀](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview)。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-110">Windows 10 Enterprise E3 in CSP, see the [Windows 10 Enterprise E3 in CSP Overview](https://docs.microsoft.com/en-us/windows/deployment/windows-10-enterprise-e3-overview).</span></span>


## <a name="before-you-begin"></a><span data-ttu-id="3d2f8-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="3d2f8-111">Before you begin</span></span>

<span data-ttu-id="3d2f8-112">開始在您的環境中設定自動註冊已加入網域的 Windows 裝置之前，您應該先熟悉支援的案例和條件約束。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-112">Before you start configuring the automatic registration of Windows domain-joined devices in your environment, you should familiarize yourself with the supported scenarios and the constraints.</span></span>  

<span data-ttu-id="3d2f8-113">為了改善說明的可讀性，本主題使用下列詞彙︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-113">To improve the readability of the descriptions, this topic uses the following term:</span></span> 

- <span data-ttu-id="3d2f8-114">**現行 Windows 裝置** - 這個詞彙是指執行 Windows 10 或 Windows Server 2016 之已加入網域的裝置。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-114">**Windows current devices** - This term refers to domain-joined devices running Windows 10 or Windows Server 2016.</span></span>
- <span data-ttu-id="3d2f8-115">**舊版 Windows 裝置** - 這個詞彙是指並非執行 Windows 10 或 Windows Server 2016 之所有**支援的**已加入網域 Windows 裝置。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-115">**Windows down-level devices** - This term refers to all **supported** domain-joined Windows devices that are neither running Windows 10 nor Windows Server 2016.</span></span>  


### <a name="windows-current-devices"></a><span data-ttu-id="3d2f8-116">現行 Windows 裝置</span><span class="sxs-lookup"><span data-stu-id="3d2f8-116">Windows current devices</span></span>

- <span data-ttu-id="3d2f8-117">對於執行 Windows 桌面作業系統的裝置，我們建議使用 Windows 10 年度更新版 (版本 1607) 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-117">For devices running the Windows desktop operating system, we recommend using Windows 10 Anniversary Update (version 1607) or later.</span></span> 
- <span data-ttu-id="3d2f8-118">非同盟的環境**支援**現行 Windows 裝置註冊，例如密碼雜湊同步處理組態。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-118">The registration of Windows current devices **is** supported in non-federated environments such as password hash sync configurations.</span></span>  


### <a name="windows-down-level-devices"></a><span data-ttu-id="3d2f8-119">舊版 Windows 裝置</span><span class="sxs-lookup"><span data-stu-id="3d2f8-119">Windows down-level devices</span></span>

- <span data-ttu-id="3d2f8-120">以下是支援的舊版 Windows Server 裝置：</span><span class="sxs-lookup"><span data-stu-id="3d2f8-120">The following Windows down-level devices are supported:</span></span>
    - <span data-ttu-id="3d2f8-121">Windows 8.1</span><span class="sxs-lookup"><span data-stu-id="3d2f8-121">Windows 8.1</span></span>
    - <span data-ttu-id="3d2f8-122">Windows 7</span><span class="sxs-lookup"><span data-stu-id="3d2f8-122">Windows 7</span></span>
    - <span data-ttu-id="3d2f8-123">Windows Server 2012 R2</span><span class="sxs-lookup"><span data-stu-id="3d2f8-123">Windows Server 2012 R2</span></span>
    - <span data-ttu-id="3d2f8-124">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="3d2f8-124">Windows Server 2012</span></span>
    - <span data-ttu-id="3d2f8-125">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="3d2f8-125">Windows Server 2008 R2</span></span>
- <span data-ttu-id="3d2f8-126">在非同盟環境中，**支援**透過無縫單一登入 [Azure Active Directory 無縫單一登入](https://aka.ms/hybrid/sso)來註冊舊版 Windows 裝置。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-126">The registration of Windows down-level devices **is** supported in non-federated environments through Seamless Single Sign On [Azure Active Directory Seamless Single Sign-On](https://aka.ms/hybrid/sso).</span></span>
- <span data-ttu-id="3d2f8-127">對於使用漫遊設定檔的裝置，**不支援**註冊舊版 Windows 裝置。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-127">The registration of Windows down-level devices **is not** supported for devices using roaming profiles.</span></span> <span data-ttu-id="3d2f8-128">如果您倚賴設定檔或設定的漫遊，請使用 Windows 10。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-128">If you are relying on roaming of profiles or settings, use Windows 10.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="3d2f8-129">必要條件</span><span class="sxs-lookup"><span data-stu-id="3d2f8-129">Prerequisites</span></span>

<span data-ttu-id="3d2f8-130">開始啟用自動註冊組織中已加入網域的裝置之前，您必須先確定執行最新版的 Azure AD connect。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-130">Before you start enabling the auto-registration of domain-joined devices in your organization, you need to make sure that you are running an up-to-date version of Azure AD connect.</span></span>

<span data-ttu-id="3d2f8-131">Azure AD Connect：</span><span class="sxs-lookup"><span data-stu-id="3d2f8-131">Azure AD Connect:</span></span>

- <span data-ttu-id="3d2f8-132">保持內部部署 Active Directory (AD) 中的電腦帳戶和 Azure AD 中的裝置物件之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-132">Keeps the association between the computer account in your on-premises Active Directory (AD) and the device object in Azure AD.</span></span> 
- <span data-ttu-id="3d2f8-133">啟用其他裝置相關功能，例如 Windows Hello 企業版。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-133">Enables other device related features like Windows Hello for Business.</span></span>



## <a name="configuration-steps"></a><span data-ttu-id="3d2f8-134">組態步驟</span><span class="sxs-lookup"><span data-stu-id="3d2f8-134">Configuration steps</span></span>

<span data-ttu-id="3d2f8-135">本主題包含所有一般組態案例所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-135">This topic includes the required steps for all typical configuration scenarios.</span></span>  
<span data-ttu-id="3d2f8-136">使用下表來取得您的案例所需步驟的概觀︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-136">Use the following table to get an overview of the steps that are required for your scenario:</span></span>  



| <span data-ttu-id="3d2f8-137">步驟</span><span class="sxs-lookup"><span data-stu-id="3d2f8-137">Steps</span></span>                                      | <span data-ttu-id="3d2f8-138">現行 Windows 和密碼雜湊同步處理</span><span class="sxs-lookup"><span data-stu-id="3d2f8-138">Windows current and password hash sync</span></span> | <span data-ttu-id="3d2f8-139">現行 Windows 和同盟</span><span class="sxs-lookup"><span data-stu-id="3d2f8-139">Windows current and federation</span></span> | <span data-ttu-id="3d2f8-140">舊版 Windows</span><span class="sxs-lookup"><span data-stu-id="3d2f8-140">Windows down-level</span></span> |
| :--                                        | :-:                                    | :-:                            | :-:                |
| <span data-ttu-id="3d2f8-141">步驟 1︰設定服務連接點</span><span class="sxs-lookup"><span data-stu-id="3d2f8-141">Step 1: Configure service connection point</span></span> | ![勾選][1]                            | ![勾選][1]                    | ![勾選][1]        |
| <span data-ttu-id="3d2f8-145">步驟 2︰設定宣告的發行</span><span class="sxs-lookup"><span data-stu-id="3d2f8-145">Step 2: Setup issuance of claims</span></span>           |                                        | ![勾選][1]                    | ![勾選][1]        |
| <span data-ttu-id="3d2f8-148">步驟 3︰啟用非 Windows 10 裝置</span><span class="sxs-lookup"><span data-stu-id="3d2f8-148">Step 3: Enable non-Windows 10 devices</span></span>      |                                        |                                | ![勾選][1]        |
| <span data-ttu-id="3d2f8-150">步驟 4︰控制部署與導入</span><span class="sxs-lookup"><span data-stu-id="3d2f8-150">Step 4: Control deployment and rollout</span></span>     | ![勾選][1]                            | ![勾選][1]                    | ![勾選][1]        |
| <span data-ttu-id="3d2f8-154">步驟 5︰驗證已註冊的裝置</span><span class="sxs-lookup"><span data-stu-id="3d2f8-154">Step 5: Verify registered devices</span></span>          | ![勾選][1]                            | ![勾選][1]                    | ![勾選][1]        |



## <a name="step-1-configure-service-connection-point"></a><span data-ttu-id="3d2f8-158">步驟 1︰設定服務連接點</span><span class="sxs-lookup"><span data-stu-id="3d2f8-158">Step 1: Configure service connection point</span></span>

<span data-ttu-id="3d2f8-159">您的裝置會在註冊期間使用服務連接點 (SCP) 物件來探索 Azure AD 租用戶資訊。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-159">The service connection point (SCP) object is used by your devices during the registration to discover Azure AD tenant information.</span></span> <span data-ttu-id="3d2f8-160">在內部部署 Active Directory (AD) 中，用於自動註冊已加入網域裝置的 SCP 物件必須存在於電腦樹系的組態命名內容資料分割中。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-160">In your on-premises Active Directory (AD), the SCP object for the auto-registration of domain-joined devices must exist in the configuration naming context partition of the computer's forest.</span></span> <span data-ttu-id="3d2f8-161">每個樹系只有一個組態命名內容。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-161">There is only one configuration naming context per forest.</span></span> <span data-ttu-id="3d2f8-162">在多樹系 Active Directory 組態中，服務連接點必須存在於包含已加入網域電腦的所有樹系中。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-162">In a multi-forest Active Directory configuration, the service connection point must exist in all forests containing domain-joined computers.</span></span>

<span data-ttu-id="3d2f8-163">您可以使用 [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) Cmdlet 來擷取樹系的組態命名內容。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-163">You can use the [**Get-ADRootDSE**](https://technet.microsoft.com/library/ee617246.aspx) cmdlet to retrieve the configuration naming context of your forest.</span></span>  

<span data-ttu-id="3d2f8-164">如果樹系的 Active Directory 網域名稱為 fabrikam.com，則組態命名內容為：</span><span class="sxs-lookup"><span data-stu-id="3d2f8-164">For a forest with the Active Directory domain name *fabrikam.com*, the configuration naming context is:</span></span>

`CN=Configuration,DC=fabrikam,DC=com`

<span data-ttu-id="3d2f8-165">在您的樹系中，用於自動註冊已加入網域裝置的 SCP 物件位於︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-165">In your forest, the SCP object for the auto-registration of domain-joined devices is located at:</span></span>  

`CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,[Your Configuration Naming Context]`

<span data-ttu-id="3d2f8-166">視您部署 Azure AD Connect 的方式而定，可能已經設定 SCP 物件。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-166">Depending on how you have deployed Azure AD Connect, the SCP object may have already been configured.</span></span>
<span data-ttu-id="3d2f8-167">您可以使用下列 Windows PowerShell 指令碼，確認物件是否存在並擷取探索值︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-167">You can verify the existence of the object and retrieve the discovery values using the following Windows PowerShell script:</span></span> 

    $scp = New-Object System.DirectoryServices.DirectoryEntry;

    $scp.Path = "LDAP://CN=62a0ff2e-97b9-4513-943f-0d221bd30080,CN=Device Registration Configuration,CN=Services,CN=Configuration,DC=fabrikam,DC=com";

    $scp.Keywords;

<span data-ttu-id="3d2f8-168">**$scp.Keywords** 的輸出會顯示 Azure AD 租用戶資訊，例如：</span><span class="sxs-lookup"><span data-stu-id="3d2f8-168">The **$scp.Keywords** output shows the Azure AD tenant information, for example:</span></span>

    azureADName:microsoft.com
    azureADId:72f988bf-86f1-41af-91ab-2d7cd011db47

<span data-ttu-id="3d2f8-169">如果服務連接點不存在，請在 Azure AD Connect 伺服器上執行 `Initialize-ADSyncDomainJoinedComputerSync` Cmdlet 加以建立。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-169">If the service connection point does not exist, you can create it by running the `Initialize-ADSyncDomainJoinedComputerSync` cmdlet on your Azure AD Connect server.</span></span> <span data-ttu-id="3d2f8-170">需要企業系統管理員認證才能執行此 Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-170">Enterprise admin credential is required to run this cmdlet.</span></span>  
<span data-ttu-id="3d2f8-171">此 Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="3d2f8-171">The cmdlet:</span></span>

- <span data-ttu-id="3d2f8-172">在 Azure AD Connect 連線到的 Active Directory 樹系中建立服務連接點。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-172">Creates the service connection point in the Active Directory forest Azure AD Connect is connected to.</span></span> 
- <span data-ttu-id="3d2f8-173">要求您指定 `AdConnectorAccount` 參數。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-173">Requires you to specify the `AdConnectorAccount` parameter.</span></span> <span data-ttu-id="3d2f8-174">這是在 Azure AD Connect 中設定為 Active Directory 連接器帳戶的帳戶。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-174">This is the account that is configured as Active Directory connector account in Azure AD connect.</span></span> 


<span data-ttu-id="3d2f8-175">以下指令碼顯示使用此 Cmdlet 的範例。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-175">The following script shows an example for using the cmdlet.</span></span> <span data-ttu-id="3d2f8-176">在此指令碼中，`$aadAdminCred = Get-Credential` 會要求您輸入使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-176">In this script, `$aadAdminCred = Get-Credential` requires you to type a user name.</span></span> <span data-ttu-id="3d2f8-177">您必須提供使用者主體名稱 (UPN) 格式 (`user@example.com`) 的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-177">You need to provide the user name in the user principal name (UPN) format (`user@example.com`).</span></span> 


    Import-Module -Name "C:\Program Files\Microsoft Azure Active Directory Connect\AdPrep\AdSyncPrep.psm1";

    $aadAdminCred = Get-Credential;

    Initialize-ADSyncDomainJoinedComputerSync –AdConnectorAccount [connector account name] -AzureADCredentials $aadAdminCred;

<span data-ttu-id="3d2f8-178">`Initialize-ADSyncDomainJoinedComputerSync` Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="3d2f8-178">The `Initialize-ADSyncDomainJoinedComputerSync` cmdlet:</span></span>

- <span data-ttu-id="3d2f8-179">使用 Active Directory PowerShell 模組，此模組依賴網域控制站上執行的 Active Directory Web 服務。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-179">Uses the Active Directory PowerShell module, which relies on Active Directory Web Services running on a domain controller.</span></span> <span data-ttu-id="3d2f8-180">執行 Windows Server 2008 R2 和更新版本的網域控制站可支援 Active Directory Web 服務。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-180">Active Directory Web Services is supported on domain controllers running Windows Server 2008 R2 and later.</span></span>
- <span data-ttu-id="3d2f8-181">只有 **MSOnline PowerShell 模組 1.1.166.0 版**才支援。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-181">Is only supported by the **MSOnline PowerShell module version 1.1.166.0**.</span></span> <span data-ttu-id="3d2f8-182">若要下載此模組，請使用這個[連結](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185)。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-182">To download this module, use this [link](http://connect.microsoft.com/site1164/Downloads/DownloadDetails.aspx?DownloadID=59185).</span></span>   

<span data-ttu-id="3d2f8-183">對於執行 Windows Server 2008 或更早版本的網域控制站，請使用下列指令碼來建立服務連接點。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-183">For domain controllers running Windows Server 2008 or earlier versions, use the script below to create the service connection point.</span></span>

<span data-ttu-id="3d2f8-184">在多樹系組態中，您應該使用下列指令碼在電腦所在的樹系中建立服務連接點︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-184">In a multi-forest configuration, you should use the following script to create the service connection point in each forest where computers exist:</span></span>
 
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


## <a name="step-2-setup-issuance-of-claims"></a><span data-ttu-id="3d2f8-185">步驟 2︰設定宣告的發行</span><span class="sxs-lookup"><span data-stu-id="3d2f8-185">Step 2: Setup issuance of claims</span></span>

<span data-ttu-id="3d2f8-186">在同盟 Azure AD 組態中，裝置倚賴 Active Directory Federation Services (AD FS) 或協力廠商內部部署同盟伺服器向 Azure AD 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-186">In a federated Azure AD configuration, devices rely on Active Directory Federation Services (AD FS) or a 3rd party on-premises federation service to authenticate to Azure AD.</span></span> <span data-ttu-id="3d2f8-187">裝置會進行驗證以取得向 Azure Active Directory 裝置註冊服務 (Azure ADS) 註冊的存取權杖。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-187">Devices authenticate to get an access token to register against the Azure Active Directory Device Registration Service (Azure DRS).</span></span>

<span data-ttu-id="3d2f8-188">現行 Windows 裝置會使用整合式 Windows 驗證向內部部署同盟服務所裝載的作用中 WS-Trust 端點 (1.3 或 2005 版) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-188">Windows current devices authenticate using Integrated Windows Authentication to an active WS-Trust endpoint (either 1.3 or 2005 versions) hosted by the on-premises federation service.</span></span>

> [!NOTE]
> <span data-ttu-id="3d2f8-189">使用 AD FS 時，必須啟用 **adfs/services/trust/13/windowstransport** 或 **adfs/services/trust/2005/windowstransport**。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-189">When using AD FS, either **adfs/services/trust/13/windowstransport** or **adfs/services/trust/2005/windowstransport** must be enabled.</span></span> <span data-ttu-id="3d2f8-190">如果您使用 Web 驗證 Proxy，也需確定已透過 Proxy 發佈此端點。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-190">If you are using the Web Authentication Proxy, also ensure that this endpoint is published through the proxy.</span></span> <span data-ttu-id="3d2f8-191">您可以在 AD FS 管理主控台的 [服務] > [端點] 底下看到已啟用的端點。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-191">You can see what end-points are enabled through the AD FS management console under **Service > Endpoints**.</span></span>
>
><span data-ttu-id="3d2f8-192">如果您沒有以 AD FS 做為您的內部部署同盟伺服器，請依照廠商的指示來確定支援 WS-Trust 1.3 或 2005 端點，而這些端點是透過中繼資料交換檔 (MEX) 發佈。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-192">If you don’t have AD FS as your on-premises federation service, follow the instructions of your vendor to make sure they support WS-Trust 1.3 or 2005 end-points and that these are published through the Metadata Exchange file (MEX).</span></span>

<span data-ttu-id="3d2f8-193">下列宣告必須存在於 Azure DRS 所收到的權杖中，才能完成裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-193">The following claims must exist in the token received by Azure DRS for device registration to complete.</span></span> <span data-ttu-id="3d2f8-194">Azure DRS 會使用其中一些資訊在 Azure AD 中建立裝置物件，而 Azure AD Connect 接著會使用此資訊將新建立的裝置物件與內部部署電腦帳戶建立關聯。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-194">Azure DRS will create a device object in Azure AD with some of this information which is then used by Azure AD Connect to associate the newly created device object with the computer account on-premises.</span></span>

* `http://schemas.microsoft.com/ws/2012/01/accounttype`
* `http://schemas.microsoft.com/identity/claims/onpremobjectguid`
* `http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`

<span data-ttu-id="3d2f8-195">如果您有多個經過驗證的網域名稱，您必須為電腦提供下列宣告︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-195">If you have more than one verified domain name, you need to provide the following claim for computers:</span></span>

* `http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`

<span data-ttu-id="3d2f8-196">如果您已發出 ImmutableID 宣告 (例如，替代登入 ID)，您必須為電腦提供一個對應宣告：</span><span class="sxs-lookup"><span data-stu-id="3d2f8-196">If you are already issuing an ImmutableID claim (e.g., alternate login ID) you need to provide one corresponding claim for computers:</span></span>

* `http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`

<span data-ttu-id="3d2f8-197">在下列各節中，您可找到下列相關資訊：</span><span class="sxs-lookup"><span data-stu-id="3d2f8-197">In the following sections, you find information about:</span></span>
 
- <span data-ttu-id="3d2f8-198">每個宣告應該具有的值</span><span class="sxs-lookup"><span data-stu-id="3d2f8-198">The values each claim should have</span></span>
- <span data-ttu-id="3d2f8-199">定義在 AD FS 中看起來如何</span><span class="sxs-lookup"><span data-stu-id="3d2f8-199">How a definition would look like in AD FS</span></span>

<span data-ttu-id="3d2f8-200">此定義可協助您確認值是否存在，或者您是否需要加以建立。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-200">The definition helps you to verify whether the values are present or if you need to create them.</span></span>

> [!NOTE]
> <span data-ttu-id="3d2f8-201">如果您未將 AD FS 用於您的內部部署同盟伺服器，請依照廠商的指示來建立適當組態以發出這些宣告。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-201">If you don’t use AD FS for your on-premises federation server, follow your vendor's instructions to create the appropriate configuration to issue these claims.</span></span>

### <a name="issue-account-type-claim"></a><span data-ttu-id="3d2f8-202">發出帳戶類型宣告</span><span class="sxs-lookup"><span data-stu-id="3d2f8-202">Issue account type claim</span></span>

<span data-ttu-id="3d2f8-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - 此宣告必須包含 **DJ** 這個值，此值可將裝置識別為已加入網域的電腦。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-203">**`http://schemas.microsoft.com/ws/2012/01/accounttype`** - This claim must contain a value of **DJ**, which identifies the device as a domain-joined computer.</span></span> <span data-ttu-id="3d2f8-204">在 AD FS 中，您可以新增發行轉換規則，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-204">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-objectguid-of-the-computer-account-on-premises"></a><span data-ttu-id="3d2f8-205">發出內部部署電腦帳戶的 objectGUID</span><span class="sxs-lookup"><span data-stu-id="3d2f8-205">Issue objectGUID of the computer account on-premises</span></span>

<span data-ttu-id="3d2f8-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - 此宣告必須包含內部電腦帳戶的 **objectGUID** 值。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-206">**`http://schemas.microsoft.com/identity/claims/onpremobjectguid`** - This claim must contain the **objectGUID** value of the on-premises computer account.</span></span> <span data-ttu-id="3d2f8-207">在 AD FS 中，您可以新增發行轉換規則，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-207">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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
 
### <a name="issue-objectsid-of-the-computer-account-on-premises"></a><span data-ttu-id="3d2f8-208">發出內部部署電腦帳戶的 objectSID</span><span class="sxs-lookup"><span data-stu-id="3d2f8-208">Issue objectSID of the computer account on-premises</span></span>

<span data-ttu-id="3d2f8-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - 此宣告必須包含內部電腦帳戶的 **objectSid** 值。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-209">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/primarysid`** - This claim must contain the the **objectSid** value of the on-premises computer account.</span></span> <span data-ttu-id="3d2f8-210">在 AD FS 中，您可以新增發行轉換規則，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-210">In AD FS, you can add an issuance transform rule that looks like this:</span></span>

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

### <a name="issue-issuerid-for-computer-when-multiple-verified-domain-names-in-azure-ad"></a><span data-ttu-id="3d2f8-211">當 Azure AD 中有多個經過驗證的網域名稱時，發出電腦的 issuerID</span><span class="sxs-lookup"><span data-stu-id="3d2f8-211">Issue issuerID for computer when multiple verified domain names in Azure AD</span></span>

<span data-ttu-id="3d2f8-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - 此宣告必須包含與發行權杖的內部部署同盟服務 (AD FS 或協力廠商) 連線之任何已驗證網域名稱的統一資源識別項 (URI)。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-212">**`http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid`** - This claim must contain the Uniform Resource Identifier (URI) of any of the verified domain names that connect with the on-premises federation service (AD FS or 3rd party) issuing the token.</span></span> <span data-ttu-id="3d2f8-213">在 AD FS 中，您可以在上述內容之後，以該特定順序新增如下所示的發行轉換規則。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-213">In AD FS, you can add issuance transform rules that look like the ones below in that specific order after the ones above.</span></span> <span data-ttu-id="3d2f8-214">請注意，需要有一個規則可為使用者明確發出此規則。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-214">Please note that one rule to explicitly issue the rule for users is necessary.</span></span> <span data-ttu-id="3d2f8-215">下列規則中會新增用來識別使用者與電腦驗證的優先規則。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-215">In the rules below, a first rule identifying user vs. computer authentication is added.</span></span>

    @RuleName = "Issue account type with the value User when its not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
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


<span data-ttu-id="3d2f8-216">在上述宣告中，</span><span class="sxs-lookup"><span data-stu-id="3d2f8-216">In the claim above,</span></span>

- <span data-ttu-id="3d2f8-217">`$<domain>` 是 AD FS 服務 URL</span><span class="sxs-lookup"><span data-stu-id="3d2f8-217">`$<domain>` is the AD FS service URL</span></span>
- <span data-ttu-id="3d2f8-218">`<verified-domain-name>` 是您要使用您在 Azure AD 中的其中一個已驗證網域名稱來取代的預留位置</span><span class="sxs-lookup"><span data-stu-id="3d2f8-218">`<verified-domain-name>` is a placeholder you need to replace with one of your verified domain names in Azure AD</span></span>



<span data-ttu-id="3d2f8-219">如需已驗證之網域名稱的詳細資料，請參閱[將自訂網域名稱新增至 Azure Active Directory](active-directory-add-domain.md)。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-219">For more details about verified domain names, see [Add a custom domain name to Azure Active Directory](active-directory-add-domain.md).</span></span>  
<span data-ttu-id="3d2f8-220">若要取得已驗證之公司網域的清單，您可以使用 [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-220">To get a list of your verified company domains, you can use the [Get-MsolDomain](/powershell/module/msonline/get-msoldomain?view=azureadps-1.0) cmdlet.</span></span> 

![Get-MsolDomain](./media/active-directory-conditional-access-automatic-device-registration-setup/01.png)

### <a name="issue-immutableid-for-computer-when-one-for-users-exist-eg-alternate-login-id-is-set"></a><span data-ttu-id="3d2f8-222">當使用者存在 ImmutableID (例如已設定替代登入識別碼) 時，請發出電腦的 ImmutableID</span><span class="sxs-lookup"><span data-stu-id="3d2f8-222">Issue ImmutableID for computer when one for users exist (e.g. alternate login ID is set)</span></span>

<span data-ttu-id="3d2f8-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - 此宣告必須包含電腦的有效值。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-223">**`http://schemas.microsoft.com/LiveID/Federation/2008/05/ImmutableID`** - This claim must contain a valid value for computers.</span></span> <span data-ttu-id="3d2f8-224">在 AD FS 中，您可以新增發行轉換規則，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-224">In AD FS, you can create an issuance transform rule as follows:</span></span>

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

### <a name="helper-script-to-create-the-ad-fs-issuance-transform-rules"></a><span data-ttu-id="3d2f8-225">建立 AD FS 發行轉換規則的協助程式指令碼</span><span class="sxs-lookup"><span data-stu-id="3d2f8-225">Helper script to create the AD FS issuance transform rules</span></span>

<span data-ttu-id="3d2f8-226">下列指令碼可協助您建立上面所述的發行轉換規則。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-226">The following script helps you with the creation of the issuance transform rules described above.</span></span>

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
    $rule4 = '@RuleName = "Issue account type with the value User when it is not a computer"
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
    
    @RuleName = "Capture UPN when AccountType is User and issue the IssuerID"
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

### <a name="remarks"></a><span data-ttu-id="3d2f8-227">備註</span><span class="sxs-lookup"><span data-stu-id="3d2f8-227">Remarks</span></span> 

- <span data-ttu-id="3d2f8-228">此指令碼會將規則附加至現有的規則。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-228">This script appends the rules to the existing rules.</span></span> <span data-ttu-id="3d2f8-229">請勿執行此指令碼兩次，因為會新增這組規則兩次。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-229">Do not run the script twice because the set of rules would be added twice.</span></span> <span data-ttu-id="3d2f8-230">先確定這些宣告沒有對應的規則存在 (在對應的條件下)，才能再次執行指令碼。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-230">Make sure that no corresponding rules exist for these claims (under the corresponding conditions) before running the script again.</span></span>

- <span data-ttu-id="3d2f8-231">如果您有多個經過驗證的網域名稱 (如 Azure AD 入口網站中所示，或透過 Get-MsolDomains cmdlet)，將指令碼中 **$multipleVerifiedDomainNames** 的值設定為 **$true**。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-231">If you have multiple verified domain names (as shown in the Azure AD portal or via the Get-MsolDomains cmdlet), set the value of **$multipleVerifiedDomainNames** in the script to **$true**.</span></span> <span data-ttu-id="3d2f8-232">此外，也務必移除經由 Azure AD Connect 或透過其他方式所建立的任何現有 issuerid 宣告。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-232">Also make sure that you remove any existing issuerid claim that might have been created by Azure AD Connect or via other means.</span></span> <span data-ttu-id="3d2f8-233">此規則的範例如下︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-233">Here is an example for this rule:</span></span>


        c:[Type == "http://schemas.xmlsoap.org/claims/UPN"]
        => issue(Type = "http://schemas.microsoft.com/ws/2008/06/identity/claims/issuerid", Value = regexreplace(c.Value, ".+@(?<domain>.+)",  "http://${domain}/adfs/services/trust/")); 

- <span data-ttu-id="3d2f8-234">如果您已對使用者帳戶發出 **ImmutableID** 宣告，請將指令碼中 **$immutableIDAlreadyIssuedforUsers** 的值設定為 **$true**。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-234">If you have already issued an **ImmutableID** claim  for user accounts, set the value of **$immutableIDAlreadyIssuedforUsers** in the script to **$true**.</span></span>

## <a name="step-3-enable-windows-down-level-devices"></a><span data-ttu-id="3d2f8-235">步驟 3：啟用舊版 Windows 裝置</span><span class="sxs-lookup"><span data-stu-id="3d2f8-235">Step 3: Enable Windows down-level devices</span></span>

<span data-ttu-id="3d2f8-236">如果有些已加入網域的裝置是舊版 Windows 裝置，您需要︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-236">If some of your domain-joined devices Windows down-level devices, you need to:</span></span>

- <span data-ttu-id="3d2f8-237">在 Azure AD 中設定原則，讓使用者可以註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-237">Set a policy in Azure AD to enable users to register devices.</span></span>
 
- <span data-ttu-id="3d2f8-238">設定內部部署同盟服務來發出宣告，以支援**整合式 Windows 驗證 (IWA)** 來進行裝置註冊。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-238">Configure your on-premises federation service to issue claims to support **Integrated Windows Authentication (IWA)** for device registration.</span></span>
 
- <span data-ttu-id="3d2f8-239">將 Azure AD 裝置驗證端點新增至近端內部網路區域，以避免在驗證裝置時出現憑證提示。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-239">Add the Azure AD device authentication end-point to the local Intranet zones to avoid certificate prompts when authenticating the device.</span></span>

### <a name="set-policy-in-azure-ad-to-enable-users-to-register-devices"></a><span data-ttu-id="3d2f8-240">在 Azure AD 中設定原則，讓使用者可以註冊裝置</span><span class="sxs-lookup"><span data-stu-id="3d2f8-240">Set policy in Azure AD to enable users to register devices</span></span>

<span data-ttu-id="3d2f8-241">若要註冊舊版 Windows 裝置，您需要確定已設定可允許使用者在 Azure AD 中註冊裝置的設定。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-241">To register Windows down-level devices, you need to make sure that the setting to allow users to register devices in Azure AD is set.</span></span> <span data-ttu-id="3d2f8-242">在 Azure 入口網站中，您可以在底下找到此設定：</span><span class="sxs-lookup"><span data-stu-id="3d2f8-242">In the Azure portal, you can find this setting under:</span></span>

`Azure Active Directory > Users and groups > Device settings`
    
<span data-ttu-id="3d2f8-243">下列原則必須設定為 [全部]：**使用者可以向 Azure AD 註冊其裝置**</span><span class="sxs-lookup"><span data-stu-id="3d2f8-243">The following policy must be set to **All**: **Users may register their devices with Azure AD**</span></span>

![註冊裝置](./media/active-directory-conditional-access-automatic-device-registration-setup/23.png)


### <a name="configure-on-premises-federation-service"></a><span data-ttu-id="3d2f8-245">設定內部部署同盟服務</span><span class="sxs-lookup"><span data-stu-id="3d2f8-245">Configure on-premises federation service</span></span> 

<span data-ttu-id="3d2f8-246">內部部署同盟服務必須支援在收到對 Azure AD 信賴憑證者 (持有 resouce_params 參數且編碼值如下所示) 的驗證要求時發出 **authenticationmehod** 和 **wiaormultiauthn** 宣告︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-246">Your on-premises federation service must support issuing the **authenticationmehod** and **wiaormultiauthn** claims when receiving an authentication request to the Azure AD relying party holding a resouce_params parameter with an encoded value as shown below:</span></span>

    eyJQcm9wZXJ0aWVzIjpbeyJLZXkiOiJhY3IiLCJWYWx1ZSI6IndpYW9ybXVsdGlhdXRobiJ9XX0

    which decoded is {"Properties":[{"Key":"acr","Value":"wiaormultiauthn"}]}

<span data-ttu-id="3d2f8-247">收到這類要求時，內部部署同盟服務必須先使用整合式 Windows 驗證來驗證使用者，並且在成功時發出下列兩個宣告︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-247">When such a request comes, the on-premises federation service must authenticate the user using Integrated Windows Authentication and upon success, it must issue the following two claims:</span></span>

    http://schemas.microsoft.com/ws/2008/06/identity/authenticationmethod/windows
    http://schemas.microsoft.com/claims/wiaormultiauthn

<span data-ttu-id="3d2f8-248">在 AD FS 中，您必須新增可傳遞驗證方法的發行轉換規則。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-248">In AD FS, you must add an issuance transform rule that passes-through the authentication method.</span></span>  

<span data-ttu-id="3d2f8-249">**若要新增此規則︰**</span><span class="sxs-lookup"><span data-stu-id="3d2f8-249">**To add this rule:**</span></span>

1. <span data-ttu-id="3d2f8-250">在 AD FS 管理主控台中，移至 `AD FS > Trust Relationships > Relying Party Trusts`。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-250">In the AD FS management console, go to `AD FS > Trust Relationships > Relying Party Trusts`.</span></span>
2. <span data-ttu-id="3d2f8-251">在 [Microsoft Office 365 身分識別平台] 信賴憑證者信任物件上按一下滑鼠右鍵，然後選取 [編輯宣告規則]。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-251">Right-click the Microsoft Office 365 Identity Platform relying party trust object, and then select **Edit Claim Rules**.</span></span>
3. <span data-ttu-id="3d2f8-252">在 [發佈轉換規則] 索引標籤上，選取 [新增規則]。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-252">On the **Issuance Transform Rules** tab, select **Add Rule**.</span></span>
4. <span data-ttu-id="3d2f8-253">在 [宣告規則] 範本清單中，選取 [使用自訂規則傳送宣告]。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-253">In the **Claim rule** template list, select **Send Claims Using a Custom Rule**.</span></span>
5. <span data-ttu-id="3d2f8-254">選取 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-254">Select **Next**.</span></span>
6. <span data-ttu-id="3d2f8-255">在 [宣告規則名稱] 方塊中，輸入**驗證方法宣告規則**。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-255">In the **Claim rule name** box, type **Auth Method Claim Rule**.</span></span>
7. <span data-ttu-id="3d2f8-256">在 [宣告規則] 方塊中，輸入下列規則︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-256">In the **Claim rule** box, type the following rule:</span></span>

    `c:[Type == "http://schemas.microsoft.com/claims/authnmethodsreferences"] => issue(claim = c);`

8. <span data-ttu-id="3d2f8-257">在同盟伺服器上，以 Azure AD 信賴憑證者信任物件的信賴憑證者物件名稱取代 **\<RPObjectName\>** 之後，輸入下列 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-257">On your federation server, type the PowerShell command below after replacing **\<RPObjectName\>** with the relying party object name for your Azure AD relying party trust object.</span></span> <span data-ttu-id="3d2f8-258">此物件通常名為「Microsoft Office 365 身分識別平台」。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-258">This object usually is named **Microsoft Office 365 Identity Platform**.</span></span>
   
    `Set-AdfsRelyingPartyTrust -TargetName <RPObjectName> -AllowedAuthenticationClassReferences wiaormultiauthn`

### <a name="add-the-azure-ad-device-authentication-end-point-to-the-local-intranet-zones"></a><span data-ttu-id="3d2f8-259">將 Azure AD 裝置驗證端點新增至近端內部網路區域</span><span class="sxs-lookup"><span data-stu-id="3d2f8-259">Add the Azure AD device authentication end-point to the Local Intranet zones</span></span>

<span data-ttu-id="3d2f8-260">若要避免在註冊裝置中的使用者向 Azure AD 進行驗證時出現憑證提示時，您可以將原則推送到已加入網域的裝置，進而將下列 URL 新增至 Internet Explorer 的近端內部網路區域︰</span><span class="sxs-lookup"><span data-stu-id="3d2f8-260">To avoid certificate prompts when users in register devices authenticate to Azure AD you can push a policy to your domain-joined devices to add the following URL to the Local Intranet zone in Internet Explorer:</span></span>

`https://device.login.microsoftonline.com`

## <a name="step-4-control-deployment-and-rollout"></a><span data-ttu-id="3d2f8-261">步驟 4︰控制部署與導入</span><span class="sxs-lookup"><span data-stu-id="3d2f8-261">Step 4: Control deployment and rollout</span></span>

<span data-ttu-id="3d2f8-262">當您完成所需的步驟時，已加入網域的裝置即可自動向 Azure AD 註冊。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-262">When you have completed the required steps, domain-joined devices are ready to automatically register with Azure AD.</span></span> <span data-ttu-id="3d2f8-263">所有已加入網域且執行 Windows 10 年度更新版和 Windows Server 2016 的裝置會在裝置重新啟動或使用者登入時自動向 Azure AD 註冊。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-263">All domain-joined devices running Windows 10 Anniversary Update and Windows Server 2016 automatically register with Azure AD at device restart or user sign-in.</span></span> <span data-ttu-id="3d2f8-264">在完成加入網域作業之後，新裝置會在重新啟動時向 Azure AD 註冊。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-264">New devices register with Azure AD when the device restarts after the domain join operation is completed.</span></span>

<span data-ttu-id="3d2f8-265">先前由工作場所加入 Azure AD 的裝置 (例如 Intune) 會轉換成「已加入網域，AAD 已登錄」。不過，由於網域和使用者活動的一般流程，在所有裝置上完成此程序需要一些時間。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-265">Devices that were previously workplace-joined to Azure AD (for example for Intune) transition to “*Domain Joined, AAD Registered*”; however it takes some time for this process to complete across all devices due to the normal flow of domain and user activity.</span></span>

### <a name="remarks"></a><span data-ttu-id="3d2f8-266">備註</span><span class="sxs-lookup"><span data-stu-id="3d2f8-266">Remarks</span></span>

- <span data-ttu-id="3d2f8-267">您可以使用「群組原則」物件來控制已加入網域之 Windows 10 和 Windows Server 2016 電腦的自動註冊導入。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-267">You can use a Group Policy object to control the rollout of automatic registration of Windows 10 and Windows Server 2016 domain-joined computers.</span></span>

- <span data-ttu-id="3d2f8-268">**只有**已設定導入群組原則物件的情況下，Windows 10 2015 年 11 月更新才會自動向 Azure AD 註冊。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-268">Windows 10 November 2015 Update automatically registers with Azure AD **only** if the rollout Group Policy object is set.</span></span>

- <span data-ttu-id="3d2f8-269">若要導入舊版 Windows 電腦的自動註冊，您可以將 [Windows Installer 套件](#windows-installer-packages-for-non-windows-10-computers)部署到您所選的電腦。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-269">To rollout the automatic registration of Windows down-level computers, you can deploy a [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to computers that you select.</span></span>

- <span data-ttu-id="3d2f8-270">如果您將群組原則物件推送到已加入網域的 Windows 8.1 裝置，將會嘗試註冊。不過，建議您使用 [Windows Installer 套件](#windows-installer-packages-for-non-windows-10-computers)來註冊所有的舊版 Windows 裝置。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-270">If you push the Group Policy object to Windows 8.1 domain-joined devices, registration will be attempted; however it is recommended that you use the [Windows Installer package](#windows-installer-packages-for-non-windows-10-computers) to register all your Windows down-level devices.</span></span> 

### <a name="create-a-group-policy-object"></a><span data-ttu-id="3d2f8-271">建立群組原則物件</span><span class="sxs-lookup"><span data-stu-id="3d2f8-271">Create a Group Policy object</span></span> 

<span data-ttu-id="3d2f8-272">若要控制現行 Windows 電腦的自動註冊導入，您應將 [將已加入網域的電腦註冊為裝置] 群組原則物件部署到您要註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-272">To control the rollout of automatic registration of Windows current computers, you should deploy the **Register domain-joined computers as devices** Group Policy object to the devices you want to register.</span></span> <span data-ttu-id="3d2f8-273">例如，您可以將此原則部署到組織單位或安全性群組。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-273">For example, you can deploy the policy to an organizational unit or to a security group.</span></span>

<span data-ttu-id="3d2f8-274">**若要設定原則︰**</span><span class="sxs-lookup"><span data-stu-id="3d2f8-274">**To set the policy:**</span></span>

1. <span data-ttu-id="3d2f8-275">開啟 [伺服器管理員]，然後移至 `Tools > Group Policy Management`。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-275">Open **Server Manager**, and then go to `Tools > Group Policy Management`.</span></span>
2. <span data-ttu-id="3d2f8-276">移至您要啟用自動註冊現行 Windows 電腦的網域所對應的網域節點。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-276">Go to the domain node that corresponds to the domain where you want to activate auto-registration of Windows current computers.</span></span>
3. <span data-ttu-id="3d2f8-277">在 [群組原則物件] 上按一下滑鼠右鍵，然後選取 [新增]。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-277">Right-click **Group Policy Objects**, and then select **New**.</span></span>
4. <span data-ttu-id="3d2f8-278">輸入群組原則物件的名稱。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-278">Type a name for your Group Policy object.</span></span> <span data-ttu-id="3d2f8-279">例如，「自動向 Azure AD 註冊」。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-279">For example, *Automatic Registration to Azure AD*.</span></span> <span data-ttu-id="3d2f8-280">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-280">Select **OK**.</span></span>
5. <span data-ttu-id="3d2f8-281">以滑鼠右鍵按一下新的群組原則物件，然後選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-281">Right-click your new Group Policy object, and then select **Edit**.</span></span>
6. <span data-ttu-id="3d2f8-282">移至 [電腦設定]  >  [原則]  >  [系統管理範本]  >  [Windows 元件]  >  [裝置註冊]。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-282">Go to **Computer Configuration** > **Policies** > **Administrative Templates** > **Windows Components** > **Device Registration**.</span></span> <span data-ttu-id="3d2f8-283">以滑鼠右鍵按一下 [將已加入網域的電腦註冊為裝置]，然後選取 [編輯]。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-283">Right-click **Register domain-joined computers as devices**, and then select **Edit**.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="3d2f8-284">此「群組原則」範本已從舊版 [群組原則管理] 主控台重新命名。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-284">This Group Policy template has been renamed from earlier versions of the Group Policy Management console.</span></span> <span data-ttu-id="3d2f8-285">如果您使用舊版的主控台，請移至 `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-285">If you are using an earlier version of the console, go to `Computer Configuration > Policies > Administrative Templates > Windows Components > Workplace Join > Automatically workplace join client computers`.</span></span> 

7. <span data-ttu-id="3d2f8-286">選取 [已啟用]，然後選取 [套用]。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-286">Select **Enabled**, and then select **Apply**.</span></span>
8. <span data-ttu-id="3d2f8-287">選取 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-287">Select **OK**.</span></span>
9. <span data-ttu-id="3d2f8-288">將群組原則物件連結到您選擇的位置。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-288">Link the Group Policy object to a location of your choice.</span></span> <span data-ttu-id="3d2f8-289">例如，您可以將它連結到特定組織單位。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-289">For example, you can link it to a specific organizational unit.</span></span> <span data-ttu-id="3d2f8-290">也可以將它連結到會向 Azure AD 自動註冊的特定電腦安全性群組。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-290">You also could link it to a specific security group of computers that automatically register with Azure AD.</span></span> <span data-ttu-id="3d2f8-291">若要為貴組織中所有已加入網域的 Windows 10 和 Windows Server 2016 電腦設定此原則，請將「群組原則」物件連結至網域。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-291">To set this policy for all domain-joined Windows 10 and Windows Server 2016 computers in your organization, link the Group Policy object to the domain.</span></span>

### <a name="windows-installer-packages-for-non-windows-10-computers"></a><span data-ttu-id="3d2f8-292">非 Windows 10 電腦的 Windows Installer 套件</span><span class="sxs-lookup"><span data-stu-id="3d2f8-292">Windows Installer packages for non-Windows 10 computers</span></span>

<span data-ttu-id="3d2f8-293">若要在同盟環境中註冊已加入網域的舊版 Windows 電腦，您可以從下載中心的 [適用於非 Windows 10 電腦的 Microsoft Workplace Join](https://www.microsoft.com/en-us/download/details.aspx?id=53554) 頁面下載並安裝下列 Windows Installer 套件 (.msi)。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-293">To register domain-joined Windows down-level computers in a federated environment, you can download and install these Windows Installer package (.msi) from Download Center at the [Microsoft Workplace Join for non-Windows 10 computers](https://www.microsoft.com/en-us/download/details.aspx?id=53554) page.</span></span>

<span data-ttu-id="3d2f8-294">您可以使用軟體發佈系統 (例如 System Center Configuration Manager) 來部署此套件。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-294">You can deploy the package by using a software distribution system like System Center Configuration Manager.</span></span> <span data-ttu-id="3d2f8-295">此套件使用 quiet 參數來支援標準的無訊息安裝選項。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-295">The package supports the standard silent install options with the *quiet* parameter.</span></span> <span data-ttu-id="3d2f8-296">System Center Configuration Manager Current Branch 提供額外的舊版好處，例如能夠追蹤已完成的註冊。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-296">System Center Configuration Manager Current Branch offers additional benefits from earlier versions, like the ability to track completed registrations.</span></span> <span data-ttu-id="3d2f8-297">如需詳細資訊，請參閱 [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager)。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-297">For more information, see [System Center Configuration Manager](https://www.microsoft.com/cloud-platform/system-center-configuration-manager).</span></span>

<span data-ttu-id="3d2f8-298">安裝程式會在系統上建立排定的工作，此工作是在使用者的內容中執行。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-298">The installer creates a scheduled task on the system that runs in the user’s context.</span></span> <span data-ttu-id="3d2f8-299">此工作會在使用者登入 Windows 時觸發。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-299">The task is triggered when the user signs in to Windows.</span></span> <span data-ttu-id="3d2f8-300">此工作會在使用整合式 Windows 驗證進行驗證之後，使用使用者認證以無訊息方式向 Azure AD 註冊裝置。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-300">The task silently registers the device with Azure AD with the user credentials after authenticating using Integrated Windows Authentication.</span></span> <span data-ttu-id="3d2f8-301">若要查看裝置中排定的工作，請移至 [Microsoft] > [Workplace Join]，然後移至工作排程器程式庫。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-301">To see the scheduled task, in the device, go to **Microsoft** > **Workplace Join**, and then go to the Task Scheduler library.</span></span>

## <a name="step-5-verify-registered-devices"></a><span data-ttu-id="3d2f8-302">步驟 5︰驗證已註冊的裝置</span><span class="sxs-lookup"><span data-stu-id="3d2f8-302">Step 5: Verify registered devices</span></span>

<span data-ttu-id="3d2f8-303">您可以在 [Azure Active Directory PowerShell 模組](/powershell/azure/install-msonlinev1?view=azureadps-2.0) 中使用 [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) Cmdlet，以查看您組織中已註冊成功的裝置。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-303">You can check successful registered devices in your organization by using the [Get-MsolDevice](https://docs.microsoft.com/powershell/msonline/v1/get-msoldevice) cmdlet in the [Azure Active Directory PowerShell module](/powershell/azure/install-msonlinev1?view=azureadps-2.0).</span></span>

<span data-ttu-id="3d2f8-304">此 Cmdlet 的輸出會顯示 Azure AD 中已註冊的裝置。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-304">The output of this cmdlet shows devices registered in Azure AD.</span></span> <span data-ttu-id="3d2f8-305">若要取得所有裝置，請使用 **-All** 參數，然後使用 **deviceTrustType** 屬性進行篩選。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-305">To get all devices, use the **-All** parameter, and then filter them using the **deviceTrustType** property.</span></span> <span data-ttu-id="3d2f8-306">已加入網域的裝置具有**已加入網域**這個值。</span><span class="sxs-lookup"><span data-stu-id="3d2f8-306">Domain joined devices have a value of **Domain Joined**.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3d2f8-307">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3d2f8-307">Next steps</span></span>

* [<span data-ttu-id="3d2f8-308">自動裝置註冊常見問題集</span><span class="sxs-lookup"><span data-stu-id="3d2f8-308">Automatic device registration FAQ</span></span>](active-directory-device-registration-faq.md)
* [<span data-ttu-id="3d2f8-309">針對已加入 Azure AD 網域之電腦的自動註冊進行疑難排解 – Windows 10 和 Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="3d2f8-309">Troubleshooting auto-registration of domain joined computers to Azure AD – Windows 10 and Windows Server 2016</span></span>](active-directory-device-registration-troubleshoot-windows.md)
* [<span data-ttu-id="3d2f8-310">針對向 Azure AD 自動註冊已加入網域的電腦進行疑難排解 - 非 Windows 10</span><span class="sxs-lookup"><span data-stu-id="3d2f8-310">Troubleshooting auto-registration of domain joined computers to Azure AD – non-Windows 10</span></span>](active-directory-device-registration-troubleshoot-windows-legacy.md)
* [<span data-ttu-id="3d2f8-311">Azure Active Directory 條件式存取</span><span class="sxs-lookup"><span data-stu-id="3d2f8-311">Azure Active Directory conditional access</span></span>](active-directory-conditional-access-azure-portal.md)



<!--Image references-->
[1]: ./media/active-directory-conditional-access-automatic-device-registration-setup/12.png
