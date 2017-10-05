---
title: "使用 DSC 將認證傳遞至 Azure | Microsoft Docs"
description: "使用 PowerShell 期望的狀態組態將認證安全地傳遞到 Azure 虛擬機器的概觀"
services: virtual-machines-windows
documentationcenter: 
author: zjalexander
manager: timlt
editor: 
tags: azure-service-management,azure-resource-manager
keywords: 
ms.assetid: ea76b7e8-b576-445a-8107-88ea2f3876b9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: na
ms.date: 09/15/2016
ms.author: zachal
ms.openlocfilehash: acd768c0219ec23c0453a65c575faf5213d9c616
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="passing-credentials-to-the-azure-dsc-extension-handler"></a><span data-ttu-id="f7de1-103">將認證傳遞至 Azure DSC 延伸模組處理常式</span><span class="sxs-lookup"><span data-stu-id="f7de1-103">Passing credentials to the Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="f7de1-104">本文涵蓋適用於 Azure 的期望的狀態組態延伸模組。</span><span class="sxs-lookup"><span data-stu-id="f7de1-104">This article covers the Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="f7de1-105">如需 DSC 延伸模組處理常式的概觀，請參閱 [Azure 期望的狀態組態延伸模組處理常式簡介](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f7de1-105">An overview of the DSC extension handler can be found at [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="f7de1-106">傳入認證</span><span class="sxs-lookup"><span data-stu-id="f7de1-106">Passing in credentials</span></span>
<span data-ttu-id="f7de1-107">設定過程中，您可能需要在使用者內容中設定使用者帳戶、存取服務，或安裝程式。</span><span class="sxs-lookup"><span data-stu-id="f7de1-107">As a part of the configuration process, you may need to set up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="f7de1-108">若要執行這些動作，您需要提供認證。</span><span class="sxs-lookup"><span data-stu-id="f7de1-108">To do these things, you need to provide credentials.</span></span> 

<span data-ttu-id="f7de1-109">DSC 允許使用參數化的組態，其中會將認證傳入組態並安全地儲存在 MOF 檔案中。</span><span class="sxs-lookup"><span data-stu-id="f7de1-109">DSC allows for parameterized configurations in which credentials are passed into the configuration and securely stored in MOF files.</span></span> <span data-ttu-id="f7de1-110">Azure 延伸模組處理常式會提供憑證的自動管理功能，藉以簡化認證的管理。</span><span class="sxs-lookup"><span data-stu-id="f7de1-110">The Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="f7de1-111">請考慮使用下列 DSC 組態指令碼，此指令碼會建立包含指定的密碼的本機使用者帳戶︰</span><span class="sxs-lookup"><span data-stu-id="f7de1-111">Consider the following DSC configuration script that creates a local user account with the specified password:</span></span>

<span data-ttu-id="f7de1-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="f7de1-112">*user_configuration.ps1*</span></span>

```
configuration Main
{
    param(
        [Parameter(Mandatory=$true)]
        [ValidateNotNullorEmpty()]
        [PSCredential]
        $Credential
    )    
    Node localhost {       
        User LocalUserAccount
        {
            Username = $Credential.UserName
            Password = $Credential
            Disabled = $false
            Ensure = "Present"
            FullName = "Local User Account"
            Description = "Local User Account"
            PasswordNeverExpires = $true
        } 
    }  
} 
```

<span data-ttu-id="f7de1-113">請務必將 *node localhost* 納入為組態的一部分。</span><span class="sxs-lookup"><span data-stu-id="f7de1-113">It is important to include *node localhost* as part of the configuration.</span></span> <span data-ttu-id="f7de1-114">如果遺漏此陳述式，接下來的步驟將無法運作，因為延伸模組處理常式會特別尋找節點 localhost 陳述式。</span><span class="sxs-lookup"><span data-stu-id="f7de1-114">If this statement is missing, the following steps do not work as the extension handler specifically looks for the node localhost statement.</span></span> <span data-ttu-id="f7de1-115">也請務必納入 typecast *[PsCredential]*，因為這個特定的類型會觸發擴充功能將認證加密。</span><span class="sxs-lookup"><span data-stu-id="f7de1-115">It is also important to include the typecast *[PsCredential]*, as this specific type triggers the extension to encrypt the credential.</span></span> 

<span data-ttu-id="f7de1-116">將此指令碼發佈至 Blob 儲存體︰</span><span class="sxs-lookup"><span data-stu-id="f7de1-116">Publish this script to blob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="f7de1-117">設定 Azure DSC 延伸模組，並提供認證︰</span><span class="sxs-lookup"><span data-stu-id="f7de1-117">Set the Azure DSC extension and provide the credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="f7de1-118">保護認證的方式</span><span class="sxs-lookup"><span data-stu-id="f7de1-118">How credentials are secured</span></span>
<span data-ttu-id="f7de1-119">執行此程式碼會提示您輸入認證。</span><span class="sxs-lookup"><span data-stu-id="f7de1-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="f7de1-120">一旦提供認證之後，就會很快地儲存在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="f7de1-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="f7de1-121">使用 `Set-AzureVmDscExtension` Cmdlet 發佈認證時，會透過 HTTPS 傳輸到 VM，Azure 就會使用本機 VM 憑證，以加密的形式將該認證儲存在 VM 的磁碟上。</span><span class="sxs-lookup"><span data-stu-id="f7de1-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS to the VM, where Azure stores it encrypted on disk, using the local VM certificate.</span></span> <span data-ttu-id="f7de1-122">接著，它會在記憶體中短暫地解密後再重新加密，以便傳遞給 DSC。</span><span class="sxs-lookup"><span data-stu-id="f7de1-122">Then it is briefly decrypted in memory and re-encrypted to pass it to DSC.</span></span>

<span data-ttu-id="f7de1-123">此行為與 [使用不含擴充功能處理常式的安全組態](https://msdn.microsoft.com/powershell/dsc/securemof)不同。</span><span class="sxs-lookup"><span data-stu-id="f7de1-123">This behavior is different than [using secure configurations without the extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="f7de1-124">Azure 環境提供一個透過憑證來安全地傳輸組態資料的方式。</span><span class="sxs-lookup"><span data-stu-id="f7de1-124">The Azure environment gives a way to transmit configuration data securely via certificates.</span></span> <span data-ttu-id="f7de1-125">使用 DSC 擴充功能處理常式時，不需要在 ConfigurationData 中提供 $CertificatePath 或 $CertificateID / $Thumbprint 項目。</span><span class="sxs-lookup"><span data-stu-id="f7de1-125">When using the DSC extension handler, there is no need to provide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f7de1-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="f7de1-126">Next steps</span></span>
<span data-ttu-id="f7de1-127">如需有關 Azure DSC 擴充功能處理常式的詳細資訊，請參閱 [Azure 期望狀態組態擴充功能處理常式簡介](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f7de1-127">For more information on the Azure DSC extension handler, see [Introduction to the Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="f7de1-128">查看 [適用於 DSC 擴充功能的 Azure Resource Manager 範本](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="f7de1-128">Examine the [Azure Resource Manager template for the DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="f7de1-129">如需有關 PowerShell DSC 的詳細資訊，請 [瀏覽 PowerShell 文件中心](https://msdn.microsoft.com/powershell/dsc/overview)。</span><span class="sxs-lookup"><span data-stu-id="f7de1-129">For more information about PowerShell DSC, [visit the PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="f7de1-130">若要尋找您可以使用 PowerShell DSC 來管理的其他功能，請 [瀏覽 PowerShell 資源庫](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) 以取得更多 DSC 資源。</span><span class="sxs-lookup"><span data-stu-id="f7de1-130">To find additional functionality you can manage with PowerShell DSC, [browse the PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

