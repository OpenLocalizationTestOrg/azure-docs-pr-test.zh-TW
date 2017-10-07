---
title: "aaaPassing 認證使用 DSC tooAzure |Microsoft 文件"
description: "安全地傳遞概觀認證 tooAzure 使用 PowerShell 預期狀態設定的虛擬機器"
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
ms.openlocfilehash: 306ecd3fd481f49a0beca5052fc7531a52999330
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="passing-credentials-toohello-azure-dsc-extension-handler"></a><span data-ttu-id="0bbbc-103">傳遞認證 toohello Azure DSC 延伸模組處理常式</span><span class="sxs-lookup"><span data-stu-id="0bbbc-103">Passing credentials toohello Azure DSC extension handler</span></span>
[!INCLUDE [learn-about-deployment-models](../../../includes/learn-about-deployment-models-both-include.md)]

<span data-ttu-id="0bbbc-104">本文涵蓋 Azure hello Desired State Configuration 延伸模組。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-104">This article covers hello Desired State Configuration extension for Azure.</span></span> <span data-ttu-id="0bbbc-105">Hello DSC 延伸模組處理常式的概觀，請參閱[簡介 toohello Azure Desired State Configuration 延伸模組處理常式](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-105">An overview of hello DSC extension handler can be found at [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

## <a name="passing-in-credentials"></a><span data-ttu-id="0bbbc-106">傳入認證</span><span class="sxs-lookup"><span data-stu-id="0bbbc-106">Passing in credentials</span></span>
<span data-ttu-id="0bbbc-107">Hello 設定程序的一部分，您可能需要 tooset 使用者帳戶、 存取服務，或安裝程式在使用者內容中。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-107">As a part of hello configuration process, you may need tooset up user accounts, access services, or install a program in a user context.</span></span> <span data-ttu-id="0bbbc-108">toodo 情況，您需要 tooprovide 認證。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-108">toodo these things, you need tooprovide credentials.</span></span> 

<span data-ttu-id="0bbbc-109">DSC 可以參數化設定認證會傳遞至 hello 組態和安全地儲存在 MOF 檔案中。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-109">DSC allows for parameterized configurations in which credentials are passed into hello configuration and securely stored in MOF files.</span></span> <span data-ttu-id="0bbbc-110">hello Azure 延伸模組處理常式會提供自動管理的憑證，以簡化認證管理。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-110">hello Azure Extension Handler simplifies credential management by providing automatic management of certificates.</span></span> 

<span data-ttu-id="0bbbc-111">請考慮下列使用 hello 指定的密碼建立本機使用者帳戶的 DSC 設定指令碼的 hello:</span><span class="sxs-lookup"><span data-stu-id="0bbbc-111">Consider hello following DSC configuration script that creates a local user account with hello specified password:</span></span>

<span data-ttu-id="0bbbc-112">*user_configuration.ps1*</span><span class="sxs-lookup"><span data-stu-id="0bbbc-112">*user_configuration.ps1*</span></span>

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

<span data-ttu-id="0bbbc-113">它是重要的 tooinclude*節點 localhost* hello 組態的一部分。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-113">It is important tooinclude *node localhost* as part of hello configuration.</span></span> <span data-ttu-id="0bbbc-114">如果此陳述式遺漏，hello 下列步驟不如 hello 延伸模組處理常式特別會尋找 hello 節點 localhost 陳述式。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-114">If this statement is missing, hello following steps do not work as hello extension handler specifically looks for hello node localhost statement.</span></span> <span data-ttu-id="0bbbc-115">很重要，因為 tooinclude hello 類型轉換*[PsCredential]*，如這個特定類型的觸發程序 hello 延伸 tooencrypt hello 認證。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-115">It is also important tooinclude hello typecast *[PsCredential]*, as this specific type triggers hello extension tooencrypt hello credential.</span></span> 

<span data-ttu-id="0bbbc-116">發行此指令碼 tooblob 存放裝置：</span><span class="sxs-lookup"><span data-stu-id="0bbbc-116">Publish this script tooblob storage:</span></span>

`Publish-AzureVMDscConfiguration -ConfigurationPath .\user_configuration.ps1`

<span data-ttu-id="0bbbc-117">設定 hello Azure DSC 延伸模組，並提供 hello 認證：</span><span class="sxs-lookup"><span data-stu-id="0bbbc-117">Set hello Azure DSC extension and provide hello credential:</span></span>

```
$configurationName = "Main"
$configurationArguments = @{ Credential = Get-Credential }
$configurationArchive = "user_configuration.ps1.zip"
$vm = Get-AzureVM "example-1"

$vm = Set-AzureVMDSCExtension -VM $vm -ConfigurationArchive $configurationArchive 
-ConfigurationName $configurationName -ConfigurationArgument @configurationArguments

$vm | Update-AzureVM
```
## <a name="how-credentials-are-secured"></a><span data-ttu-id="0bbbc-118">保護認證的方式</span><span class="sxs-lookup"><span data-stu-id="0bbbc-118">How credentials are secured</span></span>
<span data-ttu-id="0bbbc-119">執行此程式碼會提示您輸入認證。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-119">Running this code prompts for a credential.</span></span> <span data-ttu-id="0bbbc-120">一旦提供認證之後，就會很快地儲存在記憶體中。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-120">Once it is provided, it is stored in memory briefly.</span></span> <span data-ttu-id="0bbbc-121">當發行與`Set-AzureVmDscExtension`cmdlet，它透過 HTTPS toohello VM 傳輸之後，在 Azure 儲存在磁碟上，使用 hello 本機 VM 憑證加密。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-121">When it is published with `Set-AzureVmDscExtension` cmdlet, it is transmitted over HTTPS toohello VM, where Azure stores it encrypted on disk, using hello local VM certificate.</span></span> <span data-ttu-id="0bbbc-122">簡短解密和重新加密的 toopass 記憶體，則它 tooDSC。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-122">Then it is briefly decrypted in memory and re-encrypted toopass it tooDSC.</span></span>

<span data-ttu-id="0bbbc-123">此行為是不同於[使用安全的設定，而 hello 延伸模組處理常式不](https://msdn.microsoft.com/powershell/dsc/securemof)。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-123">This behavior is different than [using secure configurations without hello extension handler](https://msdn.microsoft.com/powershell/dsc/securemof).</span></span> <span data-ttu-id="0bbbc-124">hello Azure 環境可讓您安全地透過憑證的方式 tootransmit 組態資料。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-124">hello Azure environment gives a way tootransmit configuration data securely via certificates.</span></span> <span data-ttu-id="0bbbc-125">使用 hello DSC 延伸模組處理常式時, 沒有任何需要 tooprovide $CertificatePath 或 $CertificateID / $Thumbprint ConfigurationData 中的項目。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-125">When using hello DSC extension handler, there is no need tooprovide $CertificatePath or a $CertificateID / $Thumbprint entry in ConfigurationData.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0bbbc-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0bbbc-126">Next steps</span></span>
<span data-ttu-id="0bbbc-127">如需有關 hello Azure DSC 延伸模組處理常式的詳細資訊，請參閱[簡介 toohello Azure Desired State Configuration 延伸模組處理常式](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-127">For more information on hello Azure DSC extension handler, see [Introduction toohello Azure Desired State Configuration extension handler](extensions-dsc-overview.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="0bbbc-128">檢查 hello [hello DSC 延伸模組的 Azure Resource Manager 範本](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-128">Examine hello [Azure Resource Manager template for hello DSC extension](extensions-dsc-template.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="0bbbc-129">如需有關 PowerShell DSC[造訪 hello PowerShell 文件中心](https://msdn.microsoft.com/powershell/dsc/overview)。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-129">For more information about PowerShell DSC, [visit hello PowerShell documentation center](https://msdn.microsoft.com/powershell/dsc/overview).</span></span> 

<span data-ttu-id="0bbbc-130">toofind 額外的功能，您可以使用 PowerShell DSC[瀏覽 hello PowerShell 資源庫](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0)的多個 DSC 資源。</span><span class="sxs-lookup"><span data-stu-id="0bbbc-130">toofind additional functionality you can manage with PowerShell DSC, [browse hello PowerShell gallery](https://www.powershellgallery.com/packages?q=DscResource&x=0&y=0) for more DSC resources.</span></span>

