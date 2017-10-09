---
title: "使用 Visual Studio 虛擬機器擴展集 aaaDeploy |Microsoft 文件"
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
ms.openlocfilehash: c89a9f2478ccc3d22989aea604a4273bcc46df82
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toocreate-a-virtual-machine-scale-set-with-visual-studio"></a><span data-ttu-id="bc8dd-103">如何 toocreate 虛擬機器規模集與 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="bc8dd-103">How toocreate a Virtual Machine Scale Set with Visual Studio</span></span>
<span data-ttu-id="bc8dd-104">本文章將示範如何 toodeploy Azure 虛擬機器規模集使用 Visual Studio 資源群組部署。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-104">This article shows you how toodeploy an Azure Virtual Machine Scale Set using a Visual Studio Resource Group Deployment.</span></span>

<span data-ttu-id="bc8dd-105">[Azure 虛擬機器擴展集](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/)是 Azure 計算資源 toodeploy 和管理類似的虛擬機器的自動調整大小的集合，以及負載平衡。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-105">[Azure Virtual Machine Scale Sets](https://azure.microsoft.com/blog/azure-vm-scale-sets-public-preview/) is an Azure Compute resource toodeploy and manage a collection of similar virtual machines with auto-scale and load balancing.</span></span> <span data-ttu-id="bc8dd-106">您可以使用 [Azure Resource Manager 範本 (英文)](https://github.com/Azure/azure-quickstart-templates) 來佈建和部署虛擬機器擴展集。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-106">You can provision and deploy Virtual Machine Scale Sets using [Azure Resource Manager Templates](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="bc8dd-107">您可以使用 Azure CLI、PowerShell、REST 部署 Azure Resource Manager 範本，也可以直接從 Visual Studio 部署。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-107">Azure Resource Manager Templates can be deployed using Azure CLI, PowerShell, REST and also directly from Visual Studio.</span></span> <span data-ttu-id="bc8dd-108">Visual Studio 會提供一組範例範本，這些範本可部署為 Azure 資源群組部署專案的一部分。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-108">Visual Studio provides a set of example templates, which can be deployed as part of an Azure Resource Group Deployment project.</span></span>

<span data-ttu-id="bc8dd-109">Azure 資源群組部署方式 toogroup 也發行在單一部署作業中的一組相關的 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-109">Azure Resource Group deployments are a way toogroup and publish a set of related Azure resources in a single deployment operation.</span></span> <span data-ttu-id="bc8dd-110">您可以在以下位置深入了解： [透過 Visual Studio 建立與部署 Azure 資源群組](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-110">You can learn more about them here: [Creating and deploying Azure resource groups through Visual Studio](../vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

## <a name="pre-requisites"></a><span data-ttu-id="bc8dd-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="bc8dd-111">Pre-requisites</span></span>
<span data-ttu-id="bc8dd-112">tooget 啟動部署 Visual Studio 中的虛擬機器擴展集，您需要下列 hello:</span><span class="sxs-lookup"><span data-stu-id="bc8dd-112">tooget started deploying Virtual Machine Scale Sets in Visual Studio, you need hello following:</span></span>

* <span data-ttu-id="bc8dd-113">Visual Studio 2013 或更新版本</span><span class="sxs-lookup"><span data-stu-id="bc8dd-113">Visual Studio 2013 or later</span></span>
* <span data-ttu-id="bc8dd-114">Azure SDK 2.7、2.8 或 2.9</span><span class="sxs-lookup"><span data-stu-id="bc8dd-114">Azure SDK 2.7, 2.8 or 2.9</span></span>

>[!NOTE]
><span data-ttu-id="bc8dd-115">這些指示假設您使用 Visual Studio 搭配 [Azure SDK 2.8 (英文)](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/)。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-115">These instructions assume you are using Visual Studio with [Azure SDK 2.8](https://azure.microsoft.com/blog/announcing-the-azure-sdk-2-8-for-net/).</span></span>

## <a name="creating-a-project"></a><span data-ttu-id="bc8dd-116">建立專案</span><span class="sxs-lookup"><span data-stu-id="bc8dd-116">Creating a Project</span></span>
1. <span data-ttu-id="bc8dd-117">選擇 [檔案 | 新增 | 專案]，在 Visual Studio 中建立新專案。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-117">Create a new project in Visual Studio by choosing **File | New | Project**.</span></span>
   
    ![新增檔案][file_new]

2. <span data-ttu-id="bc8dd-119">在下**Visual C# |雲端**，選擇**Azure Resource Manager** toocreate 部署 Azure Resource Manager 範本的專案。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-119">Under **Visual C# | Cloud**, choose **Azure Resource Manager** toocreate a project for deploying an Azure Resource Manager Template.</span></span>
   
    ![建立專案][create_project]

3. <span data-ttu-id="bc8dd-121">從範本 hello 清單，選取 hello Linux 或 Windows 虛擬機器規模設定的範本。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-121">From hello list of Templates, select either hello Linux or Windows Virtual Machine Scale Set Template.</span></span>
   
   ![選取範本][select_Template]

4. <span data-ttu-id="bc8dd-123">一旦您的專案建立您可以看到 PowerShell 部署指令碼、 Azure 資源管理員範本和虛擬機器擴展集 hello 參數檔案。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-123">Once your project is created you see PowerShell deployment scripts, an Azure Resource Manager Template, and a parameter file for hello Virtual Machine Scale Set.</span></span>
   
    ![Solution Explorer][solution_explorer]

## <a name="customize-your-project"></a><span data-ttu-id="bc8dd-125">自訂您的專案</span><span class="sxs-lookup"><span data-stu-id="bc8dd-125">Customize your project</span></span>
<span data-ttu-id="bc8dd-126">現在您可以編輯 hello 範本 toocustomize 會針對您的應用程式需求，例如加入 VM 擴充功能屬性，或編輯負載平衡規則。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-126">Now you can edit hello Template toocustomize it for your application's needs, such as adding VM extension properties or editing load balancing rules.</span></span> <span data-ttu-id="bc8dd-127">根據預設 hello 虛擬機器規模集範本會設定的 toodeploy hello AzureDiagnostics 延伸，可讓您輕鬆 tooadd 自動調整規模規則。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-127">By default hello Virtual Machine Scale Set Templates are configured toodeploy hello AzureDiagnostics extension, which makes it easy tooadd autoscale rules.</span></span> <span data-ttu-id="bc8dd-128">它也會部署具有公用 IP 位址的負載平衡器 (使用輸入 NAT 規則所設定)。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-128">It also deploys a load balancer with a public IP address, configured with inbound NAT rules.</span></span> 

<span data-ttu-id="bc8dd-129">hello 負載平衡器可讓您使用 SSH (Linux) 或 RDP (Windows) 連線 toohello VM 執行個體。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-129">hello load balancer lets you connect toohello VM instances with SSH (Linux) or RDP (Windows).</span></span> <span data-ttu-id="bc8dd-130">hello 前端連接埠範圍會從 50000 開始。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-130">hello front-end port range starts at 50000.</span></span> <span data-ttu-id="bc8dd-131">適用於 linux，這表示，如果您 SSH tooport 50000，您會路由的 tooport 22 的 hello hello 規模調整集合中的第一個 VM。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-131">For linux this means that if you SSH tooport 50000, you are routed tooport 22 of hello first VM in hello Scale Set.</span></span> <span data-ttu-id="bc8dd-132">連接 tooport 50001 是路由的 tooport 22 hello 的第二個 VM，依此類推。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-132">Connecting tooport 50001 is routed tooport 22 of hello second VM and so on.</span></span>

 <span data-ttu-id="bc8dd-133">好的方式 tooedit toouse hello JSON 大綱 tooorganize hello 參數、 變數和資源，是您使用 Visual Studio 的範本。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-133">A good way tooedit your Templates with Visual Studio is toouse hello JSON Outline tooorganize hello parameters, variables, and resources.</span></span> <span data-ttu-id="bc8dd-134">了解 hello 的結構描述 Visual Studio 可以指向出您的範本中的錯誤，再部署。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-134">With an understanding of hello schema Visual Studio can point out errors in your Template before you deploy it.</span></span>

![JSON 總管][json_explorer]

## <a name="deploy-hello-project"></a><span data-ttu-id="bc8dd-136">部署 hello 專案</span><span class="sxs-lookup"><span data-stu-id="bc8dd-136">Deploy hello project</span></span>
1. <span data-ttu-id="bc8dd-137">部署 hello Azure Resource Manager 範本 toocreate hello 虛擬機器擴展集的資源。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-137">Deploy hello Azure Resource Manager Template toocreate hello Virtual Machine Scale Set resource.</span></span> <span data-ttu-id="bc8dd-138">Hello 專案節點上按一下滑鼠右鍵，然後選擇 **部署 |新的部署**。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-138">Right-click on hello project node and choose **Deploy | New Deployment**.</span></span>
   
    ![部署範本][5deploy_Template]
    
2. <span data-ttu-id="bc8dd-140">Hello 」 部署 tooResource 群組 」 對話方塊中，選取您的訂閱。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-140">Select your subscription in hello “Deploy tooResource Group” dialog.</span></span>
   
    ![部署範本][6deploy_Template]

3. <span data-ttu-id="bc8dd-142">從這裡，您可以建立 Azure 資源群組 toodeploy 您的範本。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-142">From here, you can create an Azure Resource Group toodeploy your Template to.</span></span>
   
    ![新增資源群組][new_resource]

4. <span data-ttu-id="bc8dd-144">接下來，按一下**編輯參數**tooenter 傳遞 tooyour 範本的參數。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-144">Next, click **Edit Parameters** tooenter parameters that are passed tooyour Template.</span></span> <span data-ttu-id="bc8dd-145">提供 hello OS，這是必要的 toocreate hello 部署的 hello 使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-145">Provide hello username and password for hello OS, which is required toocreate hello deployment.</span></span> <span data-ttu-id="bc8dd-146">如果您還沒有 PowerShell Tools for Visual Studio 安裝，則建議 toocheck**儲存密碼**tooavoid 隱藏 PowerShell 命令列提示字元中，或使用[keyvault 支援](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/)。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-146">If you don't have PowerShell Tools for Visual Studio installed, it is recommended toocheck **Save passwords** tooavoid a hidden PowerShell command-line prompt, or use [keyvault support](https://azure.microsoft.com/blog/keyvault-support-for-arm-templates/).</span></span>
   
    ![編輯參數][edit_parameters]

5. <span data-ttu-id="bc8dd-148">現在，按一下 [部署]。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-148">Now click **Deploy**.</span></span> <span data-ttu-id="bc8dd-149">hello**輸出** 視窗會顯示 hello 部署進度。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-149">hello **Output** window shows hello deployment progress.</span></span> <span data-ttu-id="bc8dd-150">請注意 hello 動作執行 hello **Deploy-azureresourcegroup.ps1**指令碼。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-150">Note that hello action is executing hello **Deploy-AzureResourceGroup.ps1** script.</span></span>
   
   ![輸出視窗][output_window]

## <a name="exploring-your-virtual-machine-scale-set"></a><span data-ttu-id="bc8dd-152">探索您的虛擬機器擴展集</span><span class="sxs-lookup"><span data-stu-id="bc8dd-152">Exploring your Virtual Machine Scale Set</span></span>
<span data-ttu-id="bc8dd-153">Hello 部署完成之後，您可以檢視新虛擬機器擴展集 hello Visual Studio 中的 hello **Cloud Explorer** （重新整理 hello 清單）。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-153">Once hello deployment completes, you can view hello new Virtual Machine Scale Set in hello Visual Studio **Cloud Explorer** (refresh hello list).</span></span> <span data-ttu-id="bc8dd-154">雲端總管可讓您在開發應用程式的同時，於 Visual Studio 中管理 Azure 資源。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-154">Cloud Explorer lets you manage Azure resources in Visual Studio while developing applications.</span></span> <span data-ttu-id="bc8dd-155">您也可以檢視您虛擬機器擴展集在 hello [Azure 入口網站](https://portal.azure.com)和[Azure 資源總管](https://resources.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-155">You can also view your Virtual Machine Scale Set in hello [Azure portal](https://portal.azure.com) and [Azure Resource Explorer](https://resources.azure.com/).</span></span>

![雲端總管][cloud_explorer]

 <span data-ttu-id="bc8dd-157">hello 入口網站提供 hello toovisually 管理的網頁瀏覽器中，Azure 基礎結構，而 Azure 資源總管提供簡單的方式 tooexplore 的最佳方式和偵錯 Azure 資源，讓視窗成 hello 「 執行個體檢視 」 及也顯示 PowerShell您正在查看的 hello 資源的命令。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-157">hello portal provides hello best way toovisually manage your Azure infrastructure with a web browser, while Azure Resource Explorer provides an easy way tooexplore and debug Azure resources, giving a window into hello "instance view" and also showing PowerShell commands for hello resources you are looking at.</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc8dd-158">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bc8dd-158">Next steps</span></span>
<span data-ttu-id="bc8dd-159">一旦您已成功部署虛擬機器擴展集，透過 Visual Studio，您可以進一步自訂您的專案 toosuit 應用程式的需求。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-159">Once you’ve successfully deployed Virtual Machine Scale Sets through Visual Studio, you can further customize your project toosuit your application requirements.</span></span> <span data-ttu-id="bc8dd-160">例如，藉由新增設定自動調整規模**Insights**資源，新增基礎結構 tooyour 範本 （例如獨立 Vm），或部署應用程式使用 hello 自訂指令碼延伸。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-160">For example, configure auto-scale by adding an **Insights** resource, adding infrastructure tooyour Template (like standalone VMs), or deploying applications using hello custom script extension.</span></span> <span data-ttu-id="bc8dd-161">良好的範例範本可以在 hello [Azure 快速入門範本](https://github.com/Azure/azure-quickstart-templates)GitHub 儲存機制 （搜尋"vmss"）。</span><span class="sxs-lookup"><span data-stu-id="bc8dd-161">Good example templates can be found in hello [Azure Quickstart Templates](https://github.com/Azure/azure-quickstart-templates) GitHub repository (search for "vmss").</span></span>

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
