---
title: "aaaCreate 或修改實驗室自動使用 PowerShell 建立 Azure 資源管理員範本 |Microsoft 文件"
description: "深入了解如何使用 PowerShell toocreate toouse Azure Resource Manager 範本或修改自動 DevTest 實驗室的實驗室"
services: devtest-lab,virtual-machines,visual-studio-online
documentationcenter: na
author: tomarcher
manager: douge
editor: 
ms.assetid: dad9944c-0b20-48be-ba80-8f4aa0950903
ms.service: devtest-lab
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/21/2017
ms.author: tarcher
ms.openlocfilehash: 29c8bc67caaec17b1f8926dde4e5d9d314b06600
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a><span data-ttu-id="7efdd-103">使用 PowerShell 及 Azure Resource Manager 範本自動建立或修改實驗室</span><span class="sxs-lookup"><span data-stu-id="7efdd-103">Create or modify labs automatically using Azure Resource Manager templates and PowerShell</span></span>

<span data-ttu-id="7efdd-104">DevTest 實驗室提供許多 Azure Resource Manager 範本和 PowerShell 指令碼，可以協助您快速及自動建立新的實驗室，或修改現有的實驗室，並進行資源部署。</span><span class="sxs-lookup"><span data-stu-id="7efdd-104">DevTest Labs provides many Azure Resource Manager templates and PowerShell scripts that can help you quickly and automatically create new labs or modify existing labs and then deploy these resources.</span></span>

<span data-ttu-id="7efdd-105">這篇文章可協助引導您完成使用這些範本與指令碼 tooautomate hello 建立、 修改和部署您的實驗室 hello 程序。</span><span class="sxs-lookup"><span data-stu-id="7efdd-105">This article helps guide you through hello process of using these templates and scripts tooautomate hello creation, modification, and deployment of your labs.</span></span> <span data-ttu-id="7efdd-106">本文也會顯示您可以在其中找到影響 toouse PowerShell tooperform 一些常見工作的 DevTest Labs 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="7efdd-106">This article also shows you where you can find more information about how toouse PowerShell tooperform some common tasks in DevTest Labs.</span></span>

## <a name="step-1-gather-your-templates-and-scripts"></a><span data-ttu-id="7efdd-107">步驟 1︰收集您的範本和指令碼</span><span class="sxs-lookup"><span data-stu-id="7efdd-107">Step 1: Gather your templates and scripts</span></span>
<span data-ttu-id="7efdd-108">您可以在我們公用的 [Github 存放庫](https://github.com/Azure/azure-devtestlab)中找到預先製作的 [Azure Resource Manager 範本](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)和 [PowerShell 指令碼](https://github.com/Azure/azure-devtestlab/tree/master/Scripts)。</span><span class="sxs-lookup"><span data-stu-id="7efdd-108">You can find pre-made [Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) and [PowerShell scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) at our public [Github repository](https://github.com/Azure/azure-devtestlab).</span></span> <span data-ttu-id="7efdd-109">直接使用，或針對您的需求進行自訂，並儲存在您自己的[私人 Git 存放庫](devtest-lab-add-artifact-repo.md)。</span><span class="sxs-lookup"><span data-stu-id="7efdd-109">Use them as-is, or customize them for your needs and store them in your own [private Git repo](devtest-lab-add-artifact-repo.md).</span></span> 

## <a name="step-2-modify-your-azure-resource-manager-template"></a><span data-ttu-id="7efdd-110">步驟 2：修改您的 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="7efdd-110">Step 2: Modify your Azure Resource Manager template</span></span>
<span data-ttu-id="7efdd-111">您可以依照 hello 步驟[建立第一個 Azure Resource Manager 範本](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template)如果永遠不會建立範本之前。</span><span class="sxs-lookup"><span data-stu-id="7efdd-111">You can follow hello steps at [Create your first Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) if you have never created a template before.</span></span>

<span data-ttu-id="7efdd-112">此外，[最佳作法來建立 Azure 資源管理員範本](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)提供許多的指導方針及建議 toohelp 建立可靠且容易 toouse 的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="7efdd-112">In addition, [Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions toohelp you create Azure Resource Manager templates that are reliable and easy toouse.</span></span> <span data-ttu-id="7efdd-113">通常，您將使用的其中一種 hello 方法變化或範例，修改您的範本，針對您的需求。</span><span class="sxs-lookup"><span data-stu-id="7efdd-113">Typically, you will use a variation of one of hello approaches or examples provided and modify your template for your needs.</span></span>

## <a name="step-3-deploy-resources-with-powershell"></a><span data-ttu-id="7efdd-114">步驟 3︰ 使用 PowerShell 部署資源</span><span class="sxs-lookup"><span data-stu-id="7efdd-114">Step 3: Deploy resources with PowerShell</span></span>
<span data-ttu-id="7efdd-115">您已自訂您的範本和指令碼之後，請依照所需的 hello 步驟太[部署資源與資源管理員範本和 Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)。</span><span class="sxs-lookup"><span data-stu-id="7efdd-115">After you have customized your templates and scripts, follow hello steps necessary too[deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span> <span data-ttu-id="7efdd-116">hello 文章提供資源 tooAzure 的 Azure Resource Manager 範本 toodeploy 搭配使用 Azure PowerShell 的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="7efdd-116">hello article provides general information about using Azure PowerShell with Azure Resource Manager templates toodeploy your resources tooAzure.</span></span>


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a><span data-ttu-id="7efdd-117">您可以使用 PowerShell 在 DevTest 實驗室中執行的一般工作</span><span class="sxs-lookup"><span data-stu-id="7efdd-117">Common tasks you can perform in DevTest labs using PowerShell</span></span>
<span data-ttu-id="7efdd-118">有許多其他一般工作，您可以使用 PowerShell 來自動執行。</span><span class="sxs-lookup"><span data-stu-id="7efdd-118">There are many other common tasks that you can automate by using PowerShell.</span></span> <span data-ttu-id="7efdd-119">hello hello 文件的下列各節簡述 hello 步驟需要的 tooperform 這些工作。</span><span class="sxs-lookup"><span data-stu-id="7efdd-119">hello following sections of hello documentation outline hello steps required tooperform these tasks.</span></span>

* [<span data-ttu-id="7efdd-120">使用 PowerShell 從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="7efdd-120">Create a custom image from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [<span data-ttu-id="7efdd-121">上傳 VHD 檔案 toolab 的儲存體帳戶使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="7efdd-121">Upload VHD file toolab's storage account using PowerShell</span></span>](devtest-lab-upload-vhd-using-powershell.md)
* [<span data-ttu-id="7efdd-122">新增外部使用者 tooa 實驗室使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="7efdd-122">Add an external user tooa lab using PowerShell</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [<span data-ttu-id="7efdd-123">使用 PowerShell 建立實驗室自訂角色</span><span class="sxs-lookup"><span data-stu-id="7efdd-123">Create a lab custom role using PowerShell</span></span>](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a><span data-ttu-id="7efdd-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7efdd-124">Next steps</span></span>
* <span data-ttu-id="7efdd-125">深入了解如何 toocreate[私人 Git 儲存機制](devtest-lab-add-artifact-repo.md)您將在其中儲存您的自訂的範本或指令碼。</span><span class="sxs-lookup"><span data-stu-id="7efdd-125">Learn how toocreate a [private Git repository](devtest-lab-add-artifact-repo.md) where you will store your customized templates or scripts.</span></span>
* <span data-ttu-id="7efdd-126">瀏覽 hello [Azure 資源管理員範本，從 Azure 快速入門範本庫](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="7efdd-126">Explore hello [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates).</span></span>
