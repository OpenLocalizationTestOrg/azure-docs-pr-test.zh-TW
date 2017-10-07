---
title: "設定 Azure 堆疊中可用的 aaaMake 虛擬機器規模"
description: "了解雲端系統管理員可以將虛擬機器規模 toohello Marketplace</堆疊"
services: azure-stack
author: anjayajodha
ms.service: azure-stack
ms.topic: article
ms.date: 8/4/2017
ms.author: anajod
keywords: 
ms.openlocfilehash: 14365d62ac2f2bc453c25ce4769464eb30180ea8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machine-scale-sets-available-in-azure-stack"></a><span data-ttu-id="79574-103">在 Azure Stack 中提供虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="79574-103">Make virtual machine scale sets available in Azure Stack</span></span>
<span data-ttu-id="79574-104">虛擬機器擴展集是 Azure Stack 計算資源。</span><span class="sxs-lookup"><span data-stu-id="79574-104">Virtual machine scale sets are an Azure Stack compute resource.</span></span> <span data-ttu-id="79574-105">您可以使用這些 toodeploy 和管理一組相同的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="79574-105">You can use them toodeploy and manage a set of identical virtual machines.</span></span> <span data-ttu-id="79574-106">設定的所有虛擬機器與 hello 相同，規模集不需要預先佈建虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="79574-106">With all virtual machines configured hello same, scale sets don’t require pre-provisioning of virtual machines.</span></span> <span data-ttu-id="79574-107">很容易 toobuild 中大規模服務 big compute、 大型資料，以及進行容器化工作負載為目標。</span><span class="sxs-lookup"><span data-stu-id="79574-107">It's easier toobuild large-scale services that target big compute, big data, and containerized workloads.</span></span>

<span data-ttu-id="79574-108">本主題會引導您完成 hello 程序 toomake 規模集 hello Marketplace</堆疊中提供。</span><span class="sxs-lookup"><span data-stu-id="79574-108">This topic guides you through hello process toomake scale sets available in hello Azure Stack Marketplace.</span></span> <span data-ttu-id="79574-109">完成此程序之後，使用者可以將虛擬機器規模設定 tootheir 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="79574-109">After you complete this procedure, your users can add virtual machine scale sets tootheir subscriptions.</span></span>

<span data-ttu-id="79574-110">Azure Stack 上的虛擬機器擴展集就像是 Azure 上的虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="79574-110">Virtual machine scale sets on Azure Stack are like virtual machine scale sets on Azure.</span></span> <span data-ttu-id="79574-111">如需詳細資訊，請參閱下列影片 hello:</span><span class="sxs-lookup"><span data-stu-id="79574-111">For more information, see hello following videos:</span></span>
* [<span data-ttu-id="79574-112">Mark Russinovich 講述 Azure 擴展集</span><span class="sxs-lookup"><span data-stu-id="79574-112">Mark Russinovich talks Azure scale sets</span></span>](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)
* [<span data-ttu-id="79574-113">Guy Bowerman 與虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="79574-113">Virtual Machine Scale Sets with Guy Bowerman</span></span>](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

<span data-ttu-id="79574-114">在 Azure Stack 上，虛擬機器擴展集不支援自動擴展。</span><span class="sxs-lookup"><span data-stu-id="79574-114">On Azure Stack, Virtual Machine Scale Sets do not support auto-scale.</span></span> <span data-ttu-id="79574-115">您可以新增使用 hello Azure 堆疊入口網站、 資源管理員範本或 PowerShell 設定多個執行個體 tooa 標尺。</span><span class="sxs-lookup"><span data-stu-id="79574-115">You can add more instances tooa scale set using hello Azure Stack portal, Resource Manager templates, or PowerShell.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79574-116">必要條件</span><span class="sxs-lookup"><span data-stu-id="79574-116">Prerequisites</span></span>
* <span data-ttu-id="79574-117">**Powershell 和工具**</span><span class="sxs-lookup"><span data-stu-id="79574-117">**Powershell and tools**</span></span>

   <span data-ttu-id="79574-118">安裝和設定的 PowerShell for Azure 堆疊和 hello Azure 堆疊工具。</span><span class="sxs-lookup"><span data-stu-id="79574-118">Install and configured PowerShell for Azure Stack and hello Azure Stack tools.</span></span> <span data-ttu-id="79574-119">請參閱[在 Azure Stack 使用 PowerShell 啟動和執行](azure-stack-powershell-configure-quickstart.md)。</span><span class="sxs-lookup"><span data-stu-id="79574-119">See [Get up and running with PowerShell in Azure Stack](azure-stack-powershell-configure-quickstart.md).</span></span>

   <span data-ttu-id="79574-120">您安裝 hello Azure 堆疊工具之後，請確定您匯入下列 PowerShell 模組的 hello (路徑相對 toohello。 \ComputeAdmin 資料夾中的 hello AzureStack 工具主資料夾):</span><span class="sxs-lookup"><span data-stu-id="79574-120">After you install hello Azure Stack tools, make sure you import hello following PowerShell module (path relative toohello .\ComputeAdmin folder in hello AzureStack-Tools-master folder):</span></span>

        Import-Module .\AzureStack.ComputeAdmin.psm1

* <span data-ttu-id="79574-121">**作業系統映像**</span><span class="sxs-lookup"><span data-stu-id="79574-121">**Operating system image**</span></span>

   <span data-ttu-id="79574-122">如果您沒有加入作業系統映像 tooyour Marketplace</堆疊，請參閱[新增 hello Windows Server 2016 VM 映像 toohello Azure 堆疊 marketplace](azure-stack-add-default-image.md)。</span><span class="sxs-lookup"><span data-stu-id="79574-122">If you haven’t added an operating system image tooyour Azure Stack Marketplace, see [Add hello Windows Server 2016 VM image toohello Azure Stack marketplace](azure-stack-add-default-image.md).</span></span>

   <span data-ttu-id="79574-123">如需 Linux 支援，下載 Ubuntu Server 16.04，並將它使用```Add-AzsVMImage```以 hello 下列參數： ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```。</span><span class="sxs-lookup"><span data-stu-id="79574-123">For Linux support, download Ubuntu Server 16.04 and add it using ```Add-AzsVMImage``` with hello following parameters: ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```.</span></span>

## <a name="add-hello-virtual-machine-scale-set"></a><span data-ttu-id="79574-124">新增 hello 虛擬機器規模集</span><span class="sxs-lookup"><span data-stu-id="79574-124">Add hello virtual machine scale set</span></span>

<span data-ttu-id="79574-125">編輯下列 PowerShell 指令碼環境，然後加以執行虛擬機器規模集 tooyour Marketplace</堆疊 tooadd hello。</span><span class="sxs-lookup"><span data-stu-id="79574-125">Edit hello following PowerShell script for your environment and then run it tooadd a virtual machine scale set tooyour Azure Stack Marketplace.</span></span> 

<span data-ttu-id="79574-126">``$User``這是您使用 tooconnect hello 管理員入口網站的 hello 帳戶。</span><span class="sxs-lookup"><span data-stu-id="79574-126">``$User`` is hello account you use tooconnect hello administrator portal.</span></span> <span data-ttu-id="79574-127">例如： serviceadmin@contoso.onmicrosoft.com。</span><span class="sxs-lookup"><span data-stu-id="79574-127">For example, serviceadmin@contoso.onmicrosoft.com.</span></span>

```
$Arm = "https://adminmanagement.local.azurestack.external"
$Location = "local"

Add-AzureRMEnvironment -Name AzureStackAdmin -ArmEndpoint $Arm

$Password = ConvertTo-SecureString -AsPlainText -Force "<your Azure Stack administrator password>"

$User = "<your Azure Stack service administrator user name>"

$Creds =  New-Object System.Management.Automation.PSCredential $User, $Password

$AzsEnv = Get-AzureRmEnvironment AzureStackAdmin
$AzsEnvContext = Add-AzureRmAccount -Environment $AzsEnv -Credential $Creds
Select-AzureRmProfile -Profile $AzsEnvContext

Select-AzureRmSubscription -SubscriptionName "Default Provider Subscription"

Add-AzsVMSSGalleryItem -Location $Location
```

## <a name="remove-a-virtual-machine-scale-set"></a><span data-ttu-id="79574-128">移除虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="79574-128">Remove a virtual machine scale set</span></span>

<span data-ttu-id="79574-129">tooremove 的虛擬機器擴展集主機庫項目，執行下列 PowerShell 命令的 hello:</span><span class="sxs-lookup"><span data-stu-id="79574-129">tooremove a virtual machine scale set gallery item, run hello following PowerShell command:</span></span>

    Remove-AzsVMSSGalleryItem

> [!NOTE]
> <span data-ttu-id="79574-130">hello 主機庫項目可能不會立即移除。</span><span class="sxs-lookup"><span data-stu-id="79574-130">hello gallery item may not be removed immediately.</span></span> <span data-ttu-id="79574-131">移除從 hello Marketplace 之前您可能需要指定 toorefresh hello 入口網站數次。</span><span class="sxs-lookup"><span data-stu-id="79574-131">You may need toorefresh hello portal several times before it is removed from hello Marketplace.</span></span>


## <a name="next-steps"></a><span data-ttu-id="79574-132">後續步驟</span><span class="sxs-lookup"><span data-stu-id="79574-132">Next steps</span></span>
[<span data-ttu-id="79574-133">Azure Stack 的常見問題集</span><span class="sxs-lookup"><span data-stu-id="79574-133">Frequently asked questions for Azure Stack</span></span>](azure-stack-faq.md)

