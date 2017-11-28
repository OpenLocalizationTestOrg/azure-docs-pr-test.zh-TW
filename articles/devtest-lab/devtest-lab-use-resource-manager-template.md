---
title: "aaaView 並使用虛擬機器的 Azure Resource Manager 範本 |Microsoft 文件"
description: "了解如何 toouse 會 hello Azure 資源管理員範本，從虛擬機器 toocreate 其他 Vm"
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
ms.openlocfilehash: b79f7eb4171793681a0b654e6e72a83191c76bde
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-a-virtual-machines-azure-resource-manager-template"></a><span data-ttu-id="3ace5-103">使用虛擬機器的 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="3ace5-103">Use a virtual machine's Azure Resource Manager template</span></span>

<span data-ttu-id="3ace5-104">您可以在建立時虛擬機器 (VM) 中的 DevTest Labs 透過 hello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=525040)，儲存 hello VM 之前，您可以檢視 hello Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="3ace5-104">When you are creating a virtual machine (VM) in DevTest Labs through hello [Azure portal](http://go.microsoft.com/fwlink/p/?LinkID=525040), you can view hello Azure Resource Manager template before you save hello VM.</span></span> <span data-ttu-id="3ace5-105">hello 範本然後可用來當作基礎 toocreate 更具有實驗室 Vm hello 相同的設定。</span><span class="sxs-lookup"><span data-stu-id="3ace5-105">hello template can then be used as a basis toocreate more lab VMs with hello same settings.</span></span>

<span data-ttu-id="3ace5-106">本文說明如何 tooview hello Resource Manager 範本建立 VM，以及如何 toodeploy 它的更新版本的 tooautomate 建立 hello 相同的 VM。</span><span class="sxs-lookup"><span data-stu-id="3ace5-106">This article describes how tooview hello Resource Manager template when creating a VM, and how toodeploy it later tooautomate creation of hello same VM.</span></span>

## <a name="multi-vm-vs-single-vm-resource-manager-templates"></a><span data-ttu-id="3ace5-107">多部 VM 與單一 VM Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="3ace5-107">Multi-VM vs. single-VM Resource Manager templates</span></span>
<span data-ttu-id="3ace5-108">有兩種方式 toocreate Vm 中使用資源管理員範本的 DevTest Labs: hello Microsoft.DevTestLab/labs/virtualmachines 資源佈建或佈建 hello Microsoft.Commpute/virtualmachines 資源。</span><span class="sxs-lookup"><span data-stu-id="3ace5-108">There are two ways toocreate VMs in DevTest Labs using a Resource Manager template: provision hello Microsoft.DevTestLab/labs/virtualmachines resource or provision hello Microsoft.Commpute/virtualmachines resource.</span></span> <span data-ttu-id="3ace5-109">每種方式在不同案例中使用，而且需要不同的權限。</span><span class="sxs-lookup"><span data-stu-id="3ace5-109">Each is used in different scenarios and require different permissions.</span></span>

- <span data-ttu-id="3ace5-110">使用 Microsoft.DevTestLab/labs/virtualmachines 資源類型 （如在 hello hello 範本中的 「 資源 」 屬性中宣告） 的資源管理員範本，可以佈建個別實驗室 Vm。</span><span class="sxs-lookup"><span data-stu-id="3ace5-110">Resource Manager templates that use a Microsoft.DevTestLab/labs/virtualmachines resource type (as declared in hello “resource” property in hello template) can provision individual lab VMs.</span></span> <span data-ttu-id="3ace5-111">每個 VM 然後顯示成 hello DevTest Labs 虛擬機器清單中的單一項目：</span><span class="sxs-lookup"><span data-stu-id="3ace5-111">Each VM then shows up as a single item in hello DevTest Labs virtual machines list:</span></span>

   ![Vm 中當做 hello DevTest Labs 虛擬機器清單中的單一項目清單](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-item.png)

   <span data-ttu-id="3ace5-113">這種類型的資源管理員範本，可以透過 hello Azure PowerShell 命令，佈建**新增 AzureRmResourceGroupDeployment**或透過 hello Azure CLI 命令**az 群組部署建立**.</span><span class="sxs-lookup"><span data-stu-id="3ace5-113">This type of Resource Manager template can be provisioned through hello Azure PowerShell command **New-AzureRmResourceGroupDeployment** or through hello Azure CLI command **az group deployment create**.</span></span> <span data-ttu-id="3ace5-114">它需要系統管理員權限，所以與 DevTest 實驗室使用者角色指派的使用者無法執行 hello 部署。</span><span class="sxs-lookup"><span data-stu-id="3ace5-114">It requires administrator permissions, so users who are assigned with a DevTest Labs user role can’t perform hello deployment.</span></span> 

- <span data-ttu-id="3ace5-115">使用 Microsoft.Compute/virtualmachines 資源類型的資源管理員範本可以做為單一環境 hello DevTest Labs 虛擬機器清單中，佈建多個 Vm:</span><span class="sxs-lookup"><span data-stu-id="3ace5-115">Resource Manager templates that use a Microsoft.Compute/virtualmachines resource type can provision multiple VMs as a single environment in hello DevTest Labs virtual machines list:</span></span>

   ![Vm 中當做 hello DevTest Labs 虛擬機器清單中的單一項目清單](./media/devtest-lab-use-arm-template/devtestlab-lab-vm-single-environment.png)

   <span data-ttu-id="3ace5-117">可以同時管理相同的環境的 hello 和共用中的 Vm hello 相同生命週期。</span><span class="sxs-lookup"><span data-stu-id="3ace5-117">VMs in hello same environment can be managed together and share hello same lifecycle.</span></span> <span data-ttu-id="3ace5-118">DevTest 實驗室使用者角色指派的使用者可以建立環境，只要 hello 系統管理員設定 hello 實驗室，這樣一來，使用這些範本。</span><span class="sxs-lookup"><span data-stu-id="3ace5-118">Users who are assigned with a DevTest Labs user role can create environments using those templates as long as hello administrator has configured hello lab that way.</span></span>

<span data-ttu-id="3ace5-119">這篇文章的 hello 其餘部分將討論使用 Mirosoft.DevTestLab/labs/virtualmachines 的資源管理員範本。</span><span class="sxs-lookup"><span data-stu-id="3ace5-119">hello remainder of this article discusses Resource Manager templates that use Mirosoft.DevTestLab/labs/virtualmachines.</span></span> <span data-ttu-id="3ace5-120">會使用這些實驗室系統管理員 」 tooautomate 實驗室建立 VM (例如，claimable Vm) 或標準映像層代 （例如，原廠映像）。</span><span class="sxs-lookup"><span data-stu-id="3ace5-120">These are used by lab admins tooautomate lab VM creation (for example, claimable VMs) or golden image generation (for example, image factory).</span></span>

<span data-ttu-id="3ace5-121">[最佳作法來建立 Azure 資源管理員範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)提供許多的指導方針及建議 toohelp 建立可靠且容易 toouse 的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="3ace5-121">[Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions toohelp you create Azure Resource Manager templates that are reliable and easy toouse.</span></span>

## <a name="view-and-save-a-virtual-machines-resource-manager-template"></a><span data-ttu-id="3ace5-122">檢視及儲存虛擬機器的 Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="3ace5-122">View and save a virtual machine's Resource Manager template</span></span>
1. <span data-ttu-id="3ace5-123">請依照下列步驟 hello[的實驗室中建立您的第一個 VM](devtest-lab-create-first-vm.md) toobegin 建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3ace5-123">Follow hello steps at [Create your first VM in a lab](devtest-lab-create-first-vm.md) toobegin creating a virtual machine.</span></span>
1. <span data-ttu-id="3ace5-124">輸入您的虛擬機器的所需的 hello 資訊並加入您想要用於此 VM 的任何成品。</span><span class="sxs-lookup"><span data-stu-id="3ace5-124">Enter hello required information for your virtual machine and add any artifacts you want for this VM.</span></span>
1. <span data-ttu-id="3ace5-125">在 hello hello 設定 設定 視窗底部，選擇 **檢視 ARM 範本**。</span><span class="sxs-lookup"><span data-stu-id="3ace5-125">At hello bottom of hello Configure settings window, choose **View ARM template**.</span></span>

   ![檢視 ARM 範本按鈕](./media/devtest-lab-use-arm-template/devtestlab-lab-view-rm-template.png)
1. <span data-ttu-id="3ace5-127">複製並儲存 hello 資源管理員範本 toouse 稍後 toocreate 另一個虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3ace5-127">Copy and save hello Resource Manager template toouse later toocreate another virtual machine.</span></span>

   ![資源管理員範本 toosave 供日後使用](./media/devtest-lab-use-arm-template/devtestlab-lab-copy-rm-template.png)

<span data-ttu-id="3ace5-129">儲存 hello Resource Manager 範本之後，您必須先更新 hello 範本 hello 參數 區段，才能使用它。</span><span class="sxs-lookup"><span data-stu-id="3ace5-129">After you have saved hello Resource Manager template, you must update hello parameters section of hello template before you can use it.</span></span> <span data-ttu-id="3ace5-130">您可以建立自訂剛才 hello 參數，外部 hello 實際 Resource Manager 範本 parameter.json。</span><span class="sxs-lookup"><span data-stu-id="3ace5-130">You can create a parameter.json that customizes just hello parameters, outside of hello actual Resource Manager template.</span></span> 

![使用 JSON 檔案自訂參數](./media/devtest-lab-use-arm-template/devtestlab-lab-custom-params.png)

## <a name="deploy-a-resource-manager-template-toocreate-a-vm"></a><span data-ttu-id="3ace5-132">部署資源管理員範本 toocreate VM</span><span class="sxs-lookup"><span data-stu-id="3ace5-132">Deploy a Resource Manager template toocreate a VM</span></span>
<span data-ttu-id="3ace5-133">您已儲存的資源管理員範本，並自訂您的需求之後，您可以使用它建立 tooautomate VM。</span><span class="sxs-lookup"><span data-stu-id="3ace5-133">After you have saved a Resource Manager template and customized it for your needs, you can use it tooautomate VM creation.</span></span> <span data-ttu-id="3ace5-134">[部署資源與資源管理員範本和 Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)描述如何使用資源管理員範本 toodeploy toouse Azure PowerShell 資源 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="3ace5-134">[Deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy) describes how toouse Azure PowerShell with Resource Manager templates toodeploy your resources tooAzure.</span></span> <span data-ttu-id="3ace5-135">[部署資源，資源管理員範本與 Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli)描述如何使用資源管理員範本 toodeploy toouse Azure CLI 資源 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="3ace5-135">[Deploy resources with Resource Manager templates and Azure CLI](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy-cli) describes how toouse Azure CLI with Resource Manager templates toodeploy your resources tooAzure.</span></span>

> [!NOTE]
> <span data-ttu-id="3ace5-136">只有具備實驗室擁有者權限的使用者才可以使用 Azure PowerShell 從 Resource Manager 範本建立 VM。</span><span class="sxs-lookup"><span data-stu-id="3ace5-136">Only a user with lab owner permissions can create VMs from a Resource Manager template by using Azure PowerShell.</span></span> <span data-ttu-id="3ace5-137">如果您想要使用資源管理員範本建立 tooautomate VM，您只需要使用者權限，您可以使用 hello [ **az 實驗室 vm 建立**hello CLI 命令](https://docs.microsoft.com/cli/azure/lab/vm#create)。</span><span class="sxs-lookup"><span data-stu-id="3ace5-137">If you want tooautomate VM creation using a Resource Manager template and you only have user permissions, you can use hello [**az lab vm create** command in hello CLI](https://docs.microsoft.com/cli/azure/lab/vm#create).</span></span>

### <a name="next-steps"></a><span data-ttu-id="3ace5-138">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ace5-138">Next steps</span></span>
* <span data-ttu-id="3ace5-139">了解如何太[建立多部 VM 環境使用資源管理員範本](devtest-lab-create-environment-from-arm.md)。</span><span class="sxs-lookup"><span data-stu-id="3ace5-139">Learn how too[Create multi-VM environments with Resource Manager templates](devtest-lab-create-environment-from-arm.md).</span></span>
* <span data-ttu-id="3ace5-140">瀏覽的 DevTest Labs 自動化更多的快速入門資源管理員範本，從 hello[公用的 DevTest Labs GitHub 儲存機制](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="3ace5-140">Explore more quick-start Resource Manager templates for DevTest Labs automation from hello [public DevTest Labs GitHub repo](https://github.com/Azure/azure-quickstart-templates).</span></span>
