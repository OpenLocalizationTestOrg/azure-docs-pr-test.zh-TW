---
title: "aaaEnable Azure 堆疊中的多租用戶 |Microsoft 文件"
description: "深入了解如何 toosupport Azure 堆疊中的多個 Azure Active Directory 目錄"
services: azure-stack
documentationcenter: 
author: HeathL17
manager: byronr
editor: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/26/2017
ms.author: helaw
ms.openlocfilehash: d7e404894a65f6786c42c5c27f76d46f353cb8c1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-multi-tenancy-in-azure-stack"></a><span data-ttu-id="61d6b-103">在 Azure Stack 中啟用多重租用</span><span class="sxs-lookup"><span data-stu-id="61d6b-103">Enable multi-tenancy in Azure Stack</span></span>

<span data-ttu-id="61d6b-104">您可以設定多個 Azure Active Directory (Azure AD) 租用戶 toouse 服務從 Azure 堆疊 toosupport 使用者 Azure 堆疊中。</span><span class="sxs-lookup"><span data-stu-id="61d6b-104">You can configure Azure Stack toosupport users from multiple Azure Active Directory (Azure AD) tenants toouse services in Azure Stack.</span></span> <span data-ttu-id="61d6b-105">例如，請考慮下列案例中的 hello:</span><span class="sxs-lookup"><span data-stu-id="61d6b-105">As an example, consider hello following scenario:</span></span>

 - <span data-ttu-id="61d6b-106">您已安裝 Azure 堆疊 hello contoso.onmicrosoft.com，服務系統管理員。</span><span class="sxs-lookup"><span data-stu-id="61d6b-106">You are hello Service Administrator of contoso.onmicrosoft.com, where Azure Stack is installed.</span></span>
 - <span data-ttu-id="61d6b-107">Mary 是 hello fabrikam.onmicrosoft.com，目錄管理員 guest 使用者的所在位置。</span><span class="sxs-lookup"><span data-stu-id="61d6b-107">Mary is hello Directory Administrator of fabrikam.onmicrosoft.com, where guest users are located.</span></span> 
 - <span data-ttu-id="61d6b-108">Mary 的公司會從您的公司接收 IaaS 和 paas 整合服務和必須在 hello 客體目錄 (fabrikam.onmicrosoft.com) toosign tooallow 使用者和 contoso.onmicrosoft.com 中使用 Azure 堆疊資源。</span><span class="sxs-lookup"><span data-stu-id="61d6b-108">Mary's company receives IaaS and PaaS services from your company, and needs tooallow users from hello guest directory (fabrikam.onmicrosoft.com) toosign in and use Azure Stack resources in contoso.onmicrosoft.com.</span></span>

<span data-ttu-id="61d6b-109">本指南提供 hello 需要執行步驟，在此案例中，hello 內容中 tooconfigure Azure 堆疊中的多租用戶。</span><span class="sxs-lookup"><span data-stu-id="61d6b-109">This guide provides hello steps required, in hello context of this scenario, tooconfigure multi-tenancy in Azure Stack.</span></span>  <span data-ttu-id="61d6b-110">在此案例中，您和 Mary 必須完成步驟 tooenable 使用者從 Fabrikam toosign 中，並從 hello Azure 堆疊在 Contoso 中的部署使用服務。</span><span class="sxs-lookup"><span data-stu-id="61d6b-110">In this scenario, you and Mary must complete steps tooenable users from Fabrikam toosign in and consume services from hello Azure Stack deployment in Contoso.</span></span>  

## <a name="before-you-begin"></a><span data-ttu-id="61d6b-111">開始之前</span><span class="sxs-lookup"><span data-stu-id="61d6b-111">Before you begin</span></span>
<span data-ttu-id="61d6b-112">Azure 堆疊中設定多租用戶之前，有幾個必要條件 tooaccount 為：</span><span class="sxs-lookup"><span data-stu-id="61d6b-112">There are a few pre-requisites tooaccount for before you configure multi-tenancy in Azure Stack:</span></span>
  
 - <span data-ttu-id="61d6b-113">您和 Mary 必須管理步驟跨 Azure 堆疊會安裝在 (Contoso)，這兩個 hello 目錄和座標 hello 客體目錄 (Fabrikam)。</span><span class="sxs-lookup"><span data-stu-id="61d6b-113">You and Mary must coordinate administrative steps across both hello directory Azure Stack is installed in (Contoso), and hello guest directory (Fabrikam).</span></span>  
 - <span data-ttu-id="61d6b-114">請確定您已經[安裝](azure-stack-powershell-install.md)和[設定](azure-stack-powershell-configure-admin.md)好適用於 Azure Stack 的 PowerShell。</span><span class="sxs-lookup"><span data-stu-id="61d6b-114">Make sure you've [installed](azure-stack-powershell-install.md) and [configured](azure-stack-powershell-configure-admin.md) PowerShell for Azure Stack.</span></span>
 - <span data-ttu-id="61d6b-115">[下載 hello Azure 堆疊 Tools](azure-stack-powershell-download.md)，並且 hello 連接和身分識別模組匯入：</span><span class="sxs-lookup"><span data-stu-id="61d6b-115">[Download hello Azure Stack Tools](azure-stack-powershell-download.md), and import hello Connect and Identity modules:</span></span>

    ````PowerShell
        Import-Module .\Connect\AzureStack.Connect.psm1
        Import-Module .\Identity\AzureStack.Identity.psm1
    ```` 
 - <span data-ttu-id="61d6b-116">Mary 將需要[VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn)存取 tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="61d6b-116">Mary will require [VPN](azure-stack-connect-azure-stack.md#connect-to-azure-stack-with-vpn) access tooAzure Stack.</span></span> 

## <a name="configure-azure-stack-directory"></a><span data-ttu-id="61d6b-117">設定 Azure Stack 目錄</span><span class="sxs-lookup"><span data-stu-id="61d6b-117">Configure Azure Stack directory</span></span>
<span data-ttu-id="61d6b-118">在本節中，您可以設定 Azure 堆疊 tooallow 登入來自 Fabrikam 的 Azure AD 目錄租用戶。</span><span class="sxs-lookup"><span data-stu-id="61d6b-118">In this section, you configure Azure Stack tooallow sign-ins from Fabrikam Azure AD directory tenants.</span></span>

### <a name="onboard-guest-directory-tenant"></a><span data-ttu-id="61d6b-119">加入來賓目錄租用戶</span><span class="sxs-lookup"><span data-stu-id="61d6b-119">Onboard guest directory tenant</span></span>
<span data-ttu-id="61d6b-120">接下來，內建 hello 客體目錄租用戶 (Fabrikam) tooAzure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="61d6b-120">Next, onboard hello Guest Directory Tenant (Fabrikam) tooAzure Stack.</span></span>  <span data-ttu-id="61d6b-121">此步驟會設定 Azure 資源管理員 tooaccept 使用者和服務主體與 hello 客體目錄租用戶。</span><span class="sxs-lookup"><span data-stu-id="61d6b-121">This step configures Azure Resource Manager tooaccept users and service principals from hello guest directory tenant.</span></span>

````PowerShell
$adminARMEndpoint = "https://adminmanagement.local.azurestack.external"

## Replace hello value below with hello Azure Stack directory
$azureStackDirectoryTenant = "contoso.onmicrosoft.com"

## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantToBeOnboarded = "fabrikam.onmicrosoft.com"

Register-AzSGuestDirectoryTenant -AdminResourceManagerEndpoint $adminARMEndpoint `
 -DirectoryTenantName $azureStackDirectoryTenant `
 -GuestDirectoryTenantName $guestDirectoryTenantToBeOnboarded `
 -Location "local"
````



## <a name="configure-guest-directory"></a><span data-ttu-id="61d6b-122">設定來賓目錄</span><span class="sxs-lookup"><span data-stu-id="61d6b-122">Configure guest directory</span></span>
<span data-ttu-id="61d6b-123">完成 hello Azure 堆疊目錄中的步驟之後，必須提供同意 tooAzure 堆疊存取 hello 客體目錄和 hello 客體 directory 中註冊 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="61d6b-123">After you complete steps in hello Azure Stack directory, Mary must provide consent tooAzure Stack accessing hello guest directory and register Azure Stack with hello guest directory.</span></span> 

### <a name="registering-azure-stack-with-hello-guest-directory"></a><span data-ttu-id="61d6b-124">註冊 Azure 堆疊與 hello 客體目錄</span><span class="sxs-lookup"><span data-stu-id="61d6b-124">Registering Azure Stack with hello guest directory</span></span>
<span data-ttu-id="61d6b-125">一旦 hello 客體目錄系統管理員已經提供同意，Azure 堆疊 tooaccess Fabrikam 的目錄，它們必須與 Fabrikam 的目錄租用戶註冊 Azure 堆疊。</span><span class="sxs-lookup"><span data-stu-id="61d6b-125">Once hello guest directory administrator has provided consent for Azure Stack tooaccess Fabrikam's directory, they must register Azure Stack with Fabrikam's directory tenant.</span></span>

````PowerShell
$tenantARMEndpoint = "https://management.local.azurestack.external"
    
## Replace hello value below with hello guest tenant directory. 
$guestDirectoryTenantName = "fabrikam.onmicrosoft.com"

Register-AzSWithMyDirectoryTenant `
 -TenantResourceManagerEndpoint $tenantARMEndpoint `
 -DirectoryTenantName $guestDirectoryTenantName ` 
 -Verbose 
````
## <a name="direct-users-toosign-in"></a><span data-ttu-id="61d6b-126">將使用者導向 toosign 中</span><span class="sxs-lookup"><span data-stu-id="61d6b-126">Direct users toosign in</span></span>
<span data-ttu-id="61d6b-127">現在，您和 Mary 已完成 hello 步驟 tooonboard Mary 的目錄，可以將 Fabrikam 中的使用者 toosign 導向 Mary。</span><span class="sxs-lookup"><span data-stu-id="61d6b-127">Now that you and Mary have completed hello steps tooonboard Mary's directory, Mary can direct Fabrikam users toosign in.</span></span>  <span data-ttu-id="61d6b-128">瀏覽 https://portal.local.azurestack.external，Fabrikam 使用者 （亦即，具有 hello fabrikam.onmicrosoft.com 尾碼） 登入。</span><span class="sxs-lookup"><span data-stu-id="61d6b-128">Fabrikam users (that is, users with hello fabrikam.onmicrosoft.com suffix) sign in by visiting https://portal.local.azurestack.external.</span></span>  

<span data-ttu-id="61d6b-129">Mary 引導任何[外部主體](../active-directory/active-directory-understanding-resource-access.md)hello Fabrikam 目錄 （也就是沒有 fabrikam.onmicrosoft.com hello 尾碼 hello Fabrikam 目錄中的使用者） toosign 中使用 https://portal.local.azurestack.external/fabrikam.onmicrosoft.com 中。如果它們不會使用此 URL，它們可以 tootheir 預設目錄 (Fabrikam) 傳送和接收錯誤，指出系統管理員不同意。</span><span class="sxs-lookup"><span data-stu-id="61d6b-129">Mary will direct any [foreign principals](../active-directory/active-directory-understanding-resource-access.md) in hello Fabrikam directory (that is, users in hello Fabrikam directory without hello suffix of fabrikam.onmicrosoft.com) toosign in using https://portal.local.azurestack.external/fabrikam.onmicrosoft.com.  If they do not use this URL, they are sent tootheir default directory (Fabrikam) and receive an error that says their admin has not consented.</span></span>

## <a name="next-steps"></a><span data-ttu-id="61d6b-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="61d6b-130">Next Steps</span></span>

- [<span data-ttu-id="61d6b-131">管理委派提供者</span><span class="sxs-lookup"><span data-stu-id="61d6b-131">Manage delegated providers</span></span>](azure-stack-delegated-provider.md)
- [<span data-ttu-id="61d6b-132">Azure Stack 重要概念</span><span class="sxs-lookup"><span data-stu-id="61d6b-132">Azure Stack key concepts</span></span>](azure-stack-key-features.md)
