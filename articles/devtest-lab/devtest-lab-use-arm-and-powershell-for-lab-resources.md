---
title: "使用 PowerShell 及 Azure Resource Manager 範本自動建立或修改實驗室 |Microsoft 文件"
description: "了解如何使用 Powershell 及 Azure Resource Manager 範本，在 DevTest 實驗室中自動建立或修改實驗室"
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
ms.openlocfilehash: cea4531175df2cc39790497dc049d27e23ffa0c6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-or-modify-labs-automatically-using-azure-resource-manager-templates-and-powershell"></a><span data-ttu-id="c4a35-103">使用 PowerShell 及 Azure Resource Manager 範本自動建立或修改實驗室</span><span class="sxs-lookup"><span data-stu-id="c4a35-103">Create or modify labs automatically using Azure Resource Manager templates and PowerShell</span></span>

<span data-ttu-id="c4a35-104">DevTest 實驗室提供許多 Azure Resource Manager 範本和 PowerShell 指令碼，可以協助您快速及自動建立新的實驗室，或修改現有的實驗室，並進行資源部署。</span><span class="sxs-lookup"><span data-stu-id="c4a35-104">DevTest Labs provides many Azure Resource Manager templates and PowerShell scripts that can help you quickly and automatically create new labs or modify existing labs and then deploy these resources.</span></span>

<span data-ttu-id="c4a35-105">本文循序指導您使用這些範本及指令碼，來自動化實驗室的建立、修改及部署。</span><span class="sxs-lookup"><span data-stu-id="c4a35-105">This article helps guide you through the process of using these templates and scripts to automate the creation, modification, and deployment of your labs.</span></span> <span data-ttu-id="c4a35-106">本文也將說明，您將可以在哪裡找到如何使用 PowerShell 來執行 DevTest 實驗室中的若干一般工作的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="c4a35-106">This article also shows you where you can find more information about how to use PowerShell to perform some common tasks in DevTest Labs.</span></span>

## <a name="step-1-gather-your-templates-and-scripts"></a><span data-ttu-id="c4a35-107">步驟 1︰收集您的範本和指令碼</span><span class="sxs-lookup"><span data-stu-id="c4a35-107">Step 1: Gather your templates and scripts</span></span>
<span data-ttu-id="c4a35-108">您可以在我們公用的 [Github 存放庫](https://github.com/Azure/azure-devtestlab)中找到預先製作的 [Azure Resource Manager 範本](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates)和 [PowerShell 指令碼](https://github.com/Azure/azure-devtestlab/tree/master/Scripts)。</span><span class="sxs-lookup"><span data-stu-id="c4a35-108">You can find pre-made [Azure Resource Manager templates](https://github.com/Azure/azure-devtestlab/tree/master/ARMTemplates) and [PowerShell scripts](https://github.com/Azure/azure-devtestlab/tree/master/Scripts) at our public [Github repository](https://github.com/Azure/azure-devtestlab).</span></span> <span data-ttu-id="c4a35-109">直接使用，或針對您的需求進行自訂，並儲存在您自己的[私人 Git 存放庫](devtest-lab-add-artifact-repo.md)。</span><span class="sxs-lookup"><span data-stu-id="c4a35-109">Use them as-is, or customize them for your needs and store them in your own [private Git repo](devtest-lab-add-artifact-repo.md).</span></span> 

## <a name="step-2-modify-your-azure-resource-manager-template"></a><span data-ttu-id="c4a35-110">步驟 2：修改您的 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="c4a35-110">Step 2: Modify your Azure Resource Manager template</span></span>
<span data-ttu-id="c4a35-111">如果您以前從未建立過範本，您可以遵循[建立第一個 Azure Resource Manager 範本](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template)中的步驟。</span><span class="sxs-lookup"><span data-stu-id="c4a35-111">You can follow the steps at [Create your first Azure Resource Manager template](https://docs.microsoft.com/en-us/azure/azure-resource-manager/resource-manager-create-first-template) if you have never created a template before.</span></span>

<span data-ttu-id="c4a35-112">此外，[建立 Azure Resource Manager 範本的最佳做法](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices)提供許多指導方針和建議，可以協助您建立可靠又容易使用的 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="c4a35-112">In addition, [Best practices for creating Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-manager-template-best-practices) offers many guidelines and suggestions to help you create Azure Resource Manager templates that are reliable and easy to use.</span></span> <span data-ttu-id="c4a35-113">一般而言，您會使用所提供的其中一個方法或範例的某種變化，再針對您的需要來修改範本。</span><span class="sxs-lookup"><span data-stu-id="c4a35-113">Typically, you will use a variation of one of the approaches or examples provided and modify your template for your needs.</span></span>

## <a name="step-3-deploy-resources-with-powershell"></a><span data-ttu-id="c4a35-114">步驟 3︰ 使用 PowerShell 部署資源</span><span class="sxs-lookup"><span data-stu-id="c4a35-114">Step 3: Deploy resources with PowerShell</span></span>
<span data-ttu-id="c4a35-115">自訂您的範本和指令碼之後，請依照下列步驟，[使用 Resource Manager 範本和 Azure PowerShell 部署資源](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy)。</span><span class="sxs-lookup"><span data-stu-id="c4a35-115">After you have customized your templates and scripts, follow the steps necessary to [deploy resources with Resource Manager templates and Azure PowerShell](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-template-deploy).</span></span> <span data-ttu-id="c4a35-116">本文提供有關使用 Azure PowerShell 和 Azure Resource Manager 範本，將您的資源部署至 Azure 的一般資訊。</span><span class="sxs-lookup"><span data-stu-id="c4a35-116">The article provides general information about using Azure PowerShell with Azure Resource Manager templates to deploy your resources to Azure.</span></span>


## <a name="common-tasks-you-can-perform-in-devtest-labs-using-powershell"></a><span data-ttu-id="c4a35-117">您可以使用 PowerShell 在 DevTest 實驗室中執行的一般工作</span><span class="sxs-lookup"><span data-stu-id="c4a35-117">Common tasks you can perform in DevTest labs using PowerShell</span></span>
<span data-ttu-id="c4a35-118">有許多其他一般工作，您可以使用 PowerShell 來自動執行。</span><span class="sxs-lookup"><span data-stu-id="c4a35-118">There are many other common tasks that you can automate by using PowerShell.</span></span> <span data-ttu-id="c4a35-119">下列文件各節說明執行這些工作所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="c4a35-119">The following sections of the documentation outline the steps required to perform these tasks.</span></span>

* [<span data-ttu-id="c4a35-120">使用 PowerShell 從 VHD 檔案建立自訂映像</span><span class="sxs-lookup"><span data-stu-id="c4a35-120">Create a custom image from a VHD file using PowerShell</span></span>](devtest-lab-create-custom-image-from-vhd-using-powershell.md)
* [<span data-ttu-id="c4a35-121">使用 PowerShell 將 VHD 檔案上傳到實驗室的儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="c4a35-121">Upload VHD file to lab's storage account using PowerShell</span></span>](devtest-lab-upload-vhd-using-powershell.md)
* [<span data-ttu-id="c4a35-122">使用 PowerShell 將外部使用者新增至實驗室</span><span class="sxs-lookup"><span data-stu-id="c4a35-122">Add an external user to a lab using PowerShell</span></span>](devtest-lab-add-devtest-user.md#add-an-external-user-to-a-lab-using-powershell)
* [<span data-ttu-id="c4a35-123">使用 PowerShell 建立實驗室自訂角色</span><span class="sxs-lookup"><span data-stu-id="c4a35-123">Create a lab custom role using PowerShell</span></span>](devtest-lab-grant-user-permissions-to-specific-lab-policies.md#creating-a-lab-custom-role-using-powershell)

### <a name="next-steps"></a><span data-ttu-id="c4a35-124">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c4a35-124">Next steps</span></span>
* <span data-ttu-id="c4a35-125">了解如何建立您將儲存自訂範本或指令碼的[私人 Git 存放庫](devtest-lab-add-artifact-repo.md)。</span><span class="sxs-lookup"><span data-stu-id="c4a35-125">Learn how to create a [private Git repository](devtest-lab-add-artifact-repo.md) where you will store your customized templates or scripts.</span></span>
* <span data-ttu-id="c4a35-126">[從 Azure 快速入門範本資源庫中探索 Azure Resource Manager 範本](https://github.com/Azure/azure-quickstart-templates)。</span><span class="sxs-lookup"><span data-stu-id="c4a35-126">Explore the [Azure Resource Manager templates from Azure Quickstart template gallery](https://github.com/Azure/azure-quickstart-templates).</span></span>
