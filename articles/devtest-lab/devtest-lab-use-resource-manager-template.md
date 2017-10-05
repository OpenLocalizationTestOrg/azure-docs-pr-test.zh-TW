---
title: "檢視及使用虛擬機器的 Azure Resource Manager 範本 | Microsoft Docs"
description: "了解如何從虛擬機器使用 Azure Resource Manager 範本來建立其他 VM"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: a759d9ce-655c-4ac6-8834-cb29dd7d30dd
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/05/2017
ms.author: tarcher
ms.openlocfilehash: 12cdb61667f77215c894800d5c439235e767a26b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a><span data-ttu-id="6ccfb-103">使用虛擬機器的 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="6ccfb-103">Use a virtual machine's Azure Resource Manager template</span></span>

<span data-ttu-id="6ccfb-104">透過 [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)在 DevTest Labs 中建立虛擬機器 (VM) 時，您可以在儲存 VM 之前檢視 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-104">When you are creating a virtual machine (VM) in DevTest Labs through the [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), you can view the Azure Resource Manager template before you save the VM.</span></span> <span data-ttu-id="6ccfb-105">然後可以使用範本作為基礎來建立具有相同設定的多個實驗室 VM。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-105">The template can then be used as a basis to create more lab VMs with the same settings.</span></span>

<span data-ttu-id="6ccfb-106">本文說明如何在建立 VM 時檢視 Resource Manager 範本，以及稍後如何部署它以自動化建立相同 VM。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-106">This article describes how to view the Resource Manager template when creating a VM, and how to deploy it later to automate creation of the same VM.</span></span>

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a><span data-ttu-id="6ccfb-107">多部 VM 與單一 VM Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="6ccfb-107">Multi-VM vs. single-VM Resource Manager templates</span></span>
<span data-ttu-id="6ccfb-108">有兩種方式可以在使用Resource Manager 範本，在 DevTest Labs 中建立 VM：佈建 Microsoft.DevTestLab/labs/virtualmachines 資源或佈建 Microsoft.Commpute/virtualmachines 資源。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-108">There are two ways to create VMs in DevTest Labs using a Resource Manager template: provision the Microsoft.DevTestLab/labs/virtualmachines resource or provision the Microsoft.Commpute/virtualmachines resource.</span></span> <span data-ttu-id="6ccfb-109">每種方式在不同案例中使用，而且需要不同的權限。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-109">Each is used in different scenarios and require different permissions.</span></span>

- <span data-ttu-id="6ccfb-110">使用 Microsoft.DevTestLab/labs/virtualmachines 資源類型 (在範本的 “resource” 屬性中宣告) 的 Resource Manager 範本可以佈建個別實驗室 VM。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-110">Resource Manager templates that use a Microsoft.DevTestLab/labs/virtualmachines resource type (as declared in the “resource” property in the template) can provision individual lab VMs.</span></span> <span data-ttu-id="6ccfb-111">然後每個 VM 會顯示為 DevTest Labs 虛擬機器清單中的單一項目：</span><span class="sxs-lookup"><span data-stu-id="6ccfb-111">Each VM then shows up as a single item in the DevTest Labs virtual machines list:</span></span>

   ![DevTest Labs 虛擬機器清單中單一項目之 VM 的清單](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   <span data-ttu-id="6ccfb-113">這個類型的 Resource Manager 範本可以透過 Azure PowerShell 命令 **New-AzureRmResourceGroupDeployment**，或透過 Azure CLI 命令 **az group deployment create** 進行佈建。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-113">This type of Resource Manager template can be provisioned through the Azure PowerShell command **New-AzureRmResourceGroupDeployment** or through the Azure CLI command **az group deployment create**.</span></span> <span data-ttu-id="6ccfb-114">它需要系統管理員權限，所以獲得 DevTest Labs 使用者角色指派的使用者無法執行部署。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-114">It requires administrator permissions, so users who are assigned with a DevTest Labs user role can’t perform the deployment.</span></span> 

- <span data-ttu-id="6ccfb-115">使用 Microsoft.Compute/virtualmachines 資源類型的 Resource Manager 範本可以將多個 VM 佈建為 DevTest Labs 虛擬機器清單中的單一環境：</span><span class="sxs-lookup"><span data-stu-id="6ccfb-115">Resource Manager templates that use a Microsoft.Compute/virtualmachines resource type can provision multiple VMs as a single environment in the DevTest Labs virtual machines list:</span></span>

   ![DevTest Labs 虛擬機器清單中單一項目之 VM 的清單](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   <span data-ttu-id="6ccfb-117">在相同環境中的 VM 可以一起管理，並且共用相同生命週期。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-117">VMs in the same environment can be managed together and share the same lifecycle.</span></span> <span data-ttu-id="6ccfb-118">只要系統管理員已對實驗室進行相關設定，獲得 DevTest Labs 使用者角色指派的使用者就可以使用這些範本來建立環境。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-118">Users who are assigned with a DevTest Labs user role can create environments using those templates as long as the administrator has configured the lab that way.</span></span>

<span data-ttu-id="6ccfb-119">本文的其餘部分討論使用 Mirosoft.DevTestLab/labs/virtualmachines 的 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-119">The remainder of this article discusses Resource Manager templates that use Mirosoft.DevTestLab/labs/virtualmachines.</span></span> <span data-ttu-id="6ccfb-120">這些範本是由實驗室管理員用來自動化實驗室 VM 建立 (例如，可宣告 VM) 或黃金映像產生 (例如，映像工廠)。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-120">These are used by lab admins to automate lab VM creation (for example, claimable VMs) or golden image generation (for example, image factory).</span></span>

<span data-ttu-id="6ccfb-121">[建立 Azure Resource Manager 範本的最佳做法](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)提供許多指導方針和建議，可以協助您建立可靠又容易使用的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-121">[Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions to help you create Azure Resource Manager templates that are reliable and easy to use.</span></span>

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a><span data-ttu-id="6ccfb-122">檢視及儲存虛擬機器的 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="6ccfb-122">View and save a virtual machine's Resource Manager template</span></span>
1. <span data-ttu-id="6ccfb-123">請依照[在實驗室中建立您的第一個 VM](devtest-lab-create-first-vm.md) 中的步驟，開始建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-123">Follow the steps at [Create your first VM in a lab](devtest-lab-create-first-vm.md) to begin creating a virtual machine.</span></span>
1. <span data-ttu-id="6ccfb-124">輸入虛擬機器的必要資訊，並且新增您想要用於此 VM 的任何成品。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-124">Enter the required information for your virtual machine and add any artifacts you want for this VM.</span></span>
1. <span data-ttu-id="6ccfb-125">在 [設定] 設定視窗底部，選擇 [檢視 ARM 範本]。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-125">At the bottom of the Configure settings window, choose **View ARM template**.</span></span>

   ![檢視 ARM 範本按鈕](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. <span data-ttu-id="6ccfb-127">複製及儲存 Resource Manager 範本，以便稍後用來建立另一個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-127">Copy and save the Resource Manager template to use later to create another virtual machine.</span></span>

   ![儲存以供稍後使用的 Resource Manager 範本](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

<span data-ttu-id="6ccfb-129">儲存 Resource Manager 範本之後，您必須更新範本的參數區段，才能使用它。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-129">After you have saved the Resource Manager template, you must update the parameters section of the template before you can use it.</span></span> <span data-ttu-id="6ccfb-130">您可以建立 parameter.json，它只會自訂實際 Resource Manager 範本外部的參數。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-130">You can create a parameter.json that customizes just the parameters, outside of the actual Resource Manager template.</span></span> 

![使用 JSON 檔案自訂參數](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-to-create-a-vm"></a><span data-ttu-id="6ccfb-132">部署 Resource Manager 範本以建立 VM</span><span class="sxs-lookup"><span data-stu-id="6ccfb-132">Deploy a Resource Manager template to create a VM</span></span>
<span data-ttu-id="6ccfb-133">儲存 Resource Manager 範本並且針對需求自訂之後，您可以使用它來自動化 VM 建立。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-133">After you have saved a Resource Manager template and customized it for your needs, you can use it to automate VM creation.</span></span> <span data-ttu-id="6ccfb-134">[使用 Resource Manager 範本與 Azure PowerShell 來部署資源](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)說明如何使用 Azure PowerShell 與 Resource Manager 範本以將資源部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-134">[Deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) describes how to use Azure PowerShell with Resource Manager templates to deploy your resources to Azure.</span></span> <span data-ttu-id="6ccfb-135">[使用 Resource Manager 範本與 Azure CLI 來部署資源](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli)說明如何使用 Azure CLI 與 Resource Manager 範本以將資源部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-135">[Deploy resources with Resource Manager templates and Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) describes how to use Azure CLI with Resource Manager templates to deploy your resources to Azure.</span></span>

> [!NOTE]
> <span data-ttu-id="6ccfb-136">只有具備實驗室擁有者權限的使用者才可以使用 Azure PowerShell 從 Resource Manager 範本建立 VM。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-136">Only a user with lab owner permissions can create VMs from a Resource Manager template by using Azure PowerShell.</span></span> <span data-ttu-id="6ccfb-137">如果您想要使用 Resource Manager 範本自動化 VM 建立，而且您只有使用者權限，您可以使用 [CLI 中的 **az lab vm create** 命令](https://docs.microsoft.com/cli/azure/lab/vm#create)。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-137">If you want to automate VM creation using a Resource Manager template and you only have user permissions, you can use the [**az lab vm create** command in the CLI](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>

### <a name="next-steps"></a><span data-ttu-id="6ccfb-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6ccfb-138">Next steps</span></span>
* <span data-ttu-id="6ccfb-139">了解如何[使用 Resource Manager 範本建立多個 VM 環境](devtest-lab-create-environment-from-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-139">Learn how to [Create multi-VM environments with Resource Manager templates](devtest-lab-create-environment-from-arm.md).</span></span>
* <span data-ttu-id="6ccfb-140">從[公用 DevTest Labs GitHub 存放庫](https://github.com/Azure/azure-quickstart-templates)探索 DevTest Labs 的快速入門 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="6ccfb-140">Explore more quick-start Resource Manager templates for DevTest Labs automation from the [public DevTest Labs GitHub repo](https://github.com/Azure/azure-quickstart-templates).</span></span>
