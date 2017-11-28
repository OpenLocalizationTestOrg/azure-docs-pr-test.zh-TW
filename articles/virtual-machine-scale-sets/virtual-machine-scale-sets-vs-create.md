---
title: "使用 Visual Studio 部署虛擬機器擴展集 | Microsoft Docs"
description: "使用 Visual Studio 和 Resource Manager 範本部署虛擬機器調整集"
services: virtual-machine-scale-sets
documentationcenter: 
author: gbowerman
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: ed0786b8-34b2-49a8-85b5-2a628128ead6
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/13/2017
ms.author: guybo
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 78a4b0c8d305f57f495402cecb92d18425ff6bff
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="how-to-create-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="97a43-103">如何使用 Visual Studio 建立虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="97a43-103">How to create a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="97a43-104">本文說明如何使用 Visual Studio 資源群組部署，部署 Azure 虛擬機器調整集。</span><span class="sxs-lookup"><span data-stu-id="97a43-104">This article shows you how to deploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="97a43-105">[Azure 虛擬機器擴展集 (英文)](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) 是一個 Azure 計算資源，可使用自動調整規模和負載平衡來部署和管理類似虛擬機器的集合。</span><span class="sxs-lookup"><span data-stu-id="97a43-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource to deploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="97a43-106">您可以使用 [Azure Resource Manager 範本 (英文)](https://github.com/Azure/azure-quickstart-templates) 來佈建和部署虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="97a43-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="97a43-107">您可以使用 Azure CLI、PowerShell、REST 部署 Azure Resource Manager 範本，也可以直接從 Visual Studio 部署。</span><span class="sxs-lookup"><span data-stu-id="97a43-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="97a43-108">Visual Studio 會提供一組範例範本，這些範本可部署為 Azure 資源群組部署專案的一部分。</span><span class="sxs-lookup"><span data-stu-id="97a43-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="97a43-109">Azure 資源群組部署是一種方式，可在單一部署作業中將一組相關的 Azure 資源群組在一起並加以發佈。</span><span class="sxs-lookup"><span data-stu-id="97a43-109">Azure Resource Group deployments are a way to group and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="97a43-110">您可以在以下位置深入了解： [透過 Visual Studio 建立與部署 Azure 資源群組](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="97a43-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="97a43-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="97a43-111">Pre-requisites</span></span>
<span data-ttu-id="97a43-112">若要開始在 Visual Studio 中部署虛擬機器擴展集，您需要下列項目：</span><span class="sxs-lookup"><span data-stu-id="97a43-112">To get started deploying Virtual Machine Scale Sets in Visual Studio, you need the following:</span></span>

* <span data-ttu-id="97a43-113">Visual Studio 2013 或更新版本</span><span class="sxs-lookup"><span data-stu-id="97a43-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="97a43-114">Azure SDK 2.7、2.8 或 2.9</span><span class="sxs-lookup"><span data-stu-id="97a43-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="97a43-115">這些指示假設您使用 Visual Studio 搭配 [Azure SDK 2.8 (英文)](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)。</span><span class="sxs-lookup"><span data-stu-id="97a43-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="97a43-116">建立專案</span><span class="sxs-lookup"><span data-stu-id="97a43-116">Creating a Project</span></span>
1. <span data-ttu-id="97a43-117">選擇 [檔案 | 新增 | 專案]，在 Visual Studio 中建立新專案。</span><span class="sxs-lookup"><span data-stu-id="97a43-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![新增檔案][file_new]

2. <span data-ttu-id="97a43-119">在 [Visual C# | 雲端] 底下，選擇 [Azure Resource Manager] 來建立專案，以部署 Azure Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="97a43-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** to create a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![建立專案][create_project]

3. <span data-ttu-id="97a43-121">從範本清單中，選取 Linux 或 Windows 虛擬機器調整集範本。</span><span class="sxs-lookup"><span data-stu-id="97a43-121">From the list of Templates, select either the Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![選取範本][select_Template]

4. <span data-ttu-id="97a43-123">建立專案之後，您會看到 PowerShell 部署指令碼、Azure Resource Manager 範本，以及虛擬機器擴展集的參數檔。</span><span class="sxs-lookup"><span data-stu-id="97a43-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for the Virtual Machine Scale Set.</span></span>
   
    ![Solution Explorer][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="97a43-125">自訂您的專案</span><span class="sxs-lookup"><span data-stu-id="97a43-125">Customize your project</span></span>
<span data-ttu-id="97a43-126">現在您可以編輯範本，以針對您的應用程式需求自訂，例如新增 VM 延伸模組屬性或編輯負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="97a43-126">Now you can edit the Template to customize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="97a43-127">預設會設定虛擬機器擴展集範本來部署 AzureDiagnostics 延伸模組，以便更容易新增自動調整規模規則。</span><span class="sxs-lookup"><span data-stu-id="97a43-127">By default the Virtual Machine Scale Set Templates are configured to deploy the AzureDiagnostics extension, which makes it easy to add autoscale rules.</span></span> <span data-ttu-id="97a43-128">它也會部署具有公用 IP 位址的負載平衡器 (使用輸入 NAT 規則所設定)。</span><span class="sxs-lookup"><span data-stu-id="97a43-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="97a43-129">負載平衡器可讓您透過 SSH (Linux) 或 RDP (Windows) 連接到 VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="97a43-129">The load balancer lets you connect to the VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="97a43-130">前端連接埠範圍是從 50000 開始。</span><span class="sxs-lookup"><span data-stu-id="97a43-130">The front-end port range starts at 50000.</span></span> <span data-ttu-id="97a43-131">針對 Linux，這表示如果您透過 SSH 連接到通訊埠 50000，系統就會將您路由傳送到擴展集中第一個 VM 的連接埠 22。</span><span class="sxs-lookup"><span data-stu-id="97a43-131">For linux this means that if you SSH to port 50000, you are routed to port 22 of the first VM in the Scale Set.</span></span> <span data-ttu-id="97a43-132">連接到連接埠 50001，將路由傳送到第二個 VM 的連接埠 22，依此類推。</span><span class="sxs-lookup"><span data-stu-id="97a43-132">Connecting to port 50001 is routed to port 22 of the second VM and so on.</span></span>

 <span data-ttu-id="97a43-133">使用 Visual Studio 編輯範本的好方法是使用 JSON 大綱來組織參數、變數和資源。</span><span class="sxs-lookup"><span data-stu-id="97a43-133">A good way to edit your Templates with Visual Studio is to use the JSON Outline to organize the parameters, variables, and resources.</span></span> <span data-ttu-id="97a43-134">了解結構描述 Visual Studio 可以在部署範本之前在其中指出錯誤。</span><span class="sxs-lookup"><span data-stu-id="97a43-134">With an understanding of the schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![JSON 總管][json_explorer]

## <a name="deploy-the-project"></a><span data-ttu-id="97a43-136">部署專案</span><span class="sxs-lookup"><span data-stu-id="97a43-136">Deploy the project</span></span>
1. <span data-ttu-id="97a43-137">部署 Azure Resource Manager 範本來建立虛擬機器擴展集資源。</span><span class="sxs-lookup"><span data-stu-id="97a43-137">Deploy the Azure Resource Manager Template to create the Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="97a43-138">以滑鼠右鍵按一下專案節點，然後選擇 [部署 | 新增部署]。</span><span class="sxs-lookup"><span data-stu-id="97a43-138">Right-click on the project node and choose **Deploy | New Deployment**.</span></span>
   
    ![部署範本][5deploy_Template]
    
2. <span data-ttu-id="97a43-140">在 [部署到資源群組] 對話方塊中選取您的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="97a43-140">Select your subscription in the “Deploy to Resource Group” dialog.</span></span>
   
    ![部署範本][6deploy_Template]

3. <span data-ttu-id="97a43-142">您可以從這裡建立新的 Azure 資源群組，以將範本部署到其中。</span><span class="sxs-lookup"><span data-stu-id="97a43-142">From here, you can create an Azure Resource Group to deploy your Template to.</span></span>
   
    ![新增資源群組][new_resource]

4. <span data-ttu-id="97a43-144">接著，按一下 [編輯參數] 以輸入要傳遞到範本的參數。</span><span class="sxs-lookup"><span data-stu-id="97a43-144">Next, click **Edit Parameters** to enter parameters that are passed to your Template.</span></span> <span data-ttu-id="97a43-145">提供建立部署所需的 OS 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="97a43-145">Provide the username and password for the OS, which is required to create the deployment.</span></span> <span data-ttu-id="97a43-146">如果尚未安裝 PowerShell Tools for Visual Studio，建議核取 [儲存密碼] 以避免隱藏的 PowerShell 命令列提示字元，或使用[金鑰保存庫支援 (英文)](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/)。</span><span class="sxs-lookup"><span data-stu-id="97a43-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended to check **Save passwords** to avoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![編輯參數][edit_parameters]

5. <span data-ttu-id="97a43-148">現在，按一下 [部署]。</span><span class="sxs-lookup"><span data-stu-id="97a43-148">Now click **Deploy**.</span></span> <span data-ttu-id="97a43-149">[輸出] 視窗會顯示部署進度。</span><span class="sxs-lookup"><span data-stu-id="97a43-149">The **Output** window shows the deployment progress.</span></span> <span data-ttu-id="97a43-150">請注意，動作正在執行 **Deploy-AzureResourceGroup.ps1** 指令碼。</span><span class="sxs-lookup"><span data-stu-id="97a43-150">Note that the action is executing the **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![輸出視窗][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="97a43-152">探索您的虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="97a43-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="97a43-153">部署完成之後，您可以在 Visual Studio 的 [Cloud Explorer] 中檢視新的虛擬機器擴展集 (重新整理清單)。</span><span class="sxs-lookup"><span data-stu-id="97a43-153">Once the deployment completes, you can view the new Virtual Machine Scale Set in the Visual Studio **Cloud Explorer** (refresh the list).</span></span> <span data-ttu-id="97a43-154">雲端總管可讓您在開發應用程式的同時，於 Visual Studio 中管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="97a43-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="97a43-155">您也可以在 [Azure 入口網站](https://portal.azure.com)和 [Azure 資源總管 (英文)](https://resources.azure.com/) 中檢視虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="97a43-155">You can also view your Virtual Machine Scale Set in the [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![雲端總管][cloud_explorer]

 <span data-ttu-id="97a43-157">入口網站提供使用網頁瀏覽器以視覺化方式管理 Azure 基礎結構的最佳方式，而 Azure 資源總管則提供一個簡單的方式來探索 Azure 資源及進行偵錯，其中提供視窗來深入「執行個體檢視」，同時也顯示您要尋找之資源的 PowerShell 命令。</span><span class="sxs-lookup"><span data-stu-id="97a43-157">The portal provides the best way to visually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way to explore and debug Azure resources, giving a window into the "instance view" and also showing PowerShell commands for the resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="97a43-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="97a43-158">Next steps</span></span>
<span data-ttu-id="97a43-159">一旦透過 Visual Studio 成功部署虛擬機器擴展集之後，就可進一步自訂專案以符合應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="97a43-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project to suit your application requirements.</span></span> <span data-ttu-id="97a43-160">例如，設定自動調整規模，方法是新增 **Insights** 資源、將基礎結構新增至範本 (例如獨立 VM)，或是使用自訂指令碼延伸模組部署應用程式。</span><span class="sxs-lookup"><span data-stu-id="97a43-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure to your Template (like standalone VMs), or deploying applications using the custom script extension.</span></span> <span data-ttu-id="97a43-161">您可以在 [Azure 快速入門範本 (英文)](https://github.com/Azure/azure-quickstart-templates) GitHub 儲存機制中找到良好的範例範本 (搜尋 "vmss")。</span><span class="sxs-lookup"><span data-stu-id="97a43-161">Good example templates can be found in the [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

[file_new]: ./media/virtual-machine-scale-sets-vs-create/1-FileNew.png
[create_project]: ./media/virtual-machine-scale-sets-vs-create/2-CreateProject.png
[select_Template]: ./media/virtual-machine-scale-sets-vs-create/3b-SelectTemplateLin.png
[solution_explorer]: ./media/virtual-machine-scale-sets-vs-create/4-SolutionExplorer.png
[json_explorer]: ./media/virtual-machine-scale-sets-vs-create/10-JsonExplorer.png
[5deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/5-DeployTemplate.png
[6deploy_Template]: ./media/virtual-machine-scale-sets-vs-create/6-DeployTemplate.png
[new_resource]: ./media/virtual-machine-scale-sets-vs-create/7-NewResourceGroup.png
[edit_parameters]: ./media/virtual-machine-scale-sets-vs-create/8-EditParameter.png
[output_window]: ./media/virtual-machine-scale-sets-vs-create/9-Output.png
[cloud_explorer]: ./media/virtual-machine-scale-sets-vs-create/12-CloudExplorer.png
