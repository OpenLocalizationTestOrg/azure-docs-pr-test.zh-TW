---
title: "Visual Studio Azure 資源群組 Visual Studio 專案 | Microsoft Docs"
description: "使用 Visual Studio 建立 Azure 資源群組專案，並將資源部署至 Azure。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 4bd084c8-0842-4a10-8460-080c6a085bec
ms.service: azure-resource-manager
ms.devlang: multiple
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/10/2017
ms.author: tomfitz
ms.openlocfilehash: f82f59f363507b69a729580302c2d11202e93a87
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a><span data-ttu-id="8107b-103">透過 Visual Studio 建立與部署 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="8107b-103">Creating and deploying Azure resource groups through Visual Studio</span></span>
<span data-ttu-id="8107b-104">使用 Visual Studio 和 [Azure SDK](https://azure.microsoft.com/downloads/)，您可以建立專案，將您的基礎結構和程式碼部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="8107b-104">With Visual Studio and the [Azure SDK](https://azure.microsoft.com/downloads/), you can create a project that deploys your infrastructure and code to Azure.</span></span> <span data-ttu-id="8107b-105">例如，您可以為您的應用程式定義 Web 主機、網站和資料庫，並且部署該基礎結構與程式碼。</span><span class="sxs-lookup"><span data-stu-id="8107b-105">For example, you can define the web host, web site, and database for your app, and deploy that infrastructure along with the code.</span></span> <span data-ttu-id="8107b-106">或者，您可以定義虛擬機器、虛擬網路和儲存體帳戶，並且部署該基礎結構以及在虛擬機器上執行的指令碼。</span><span class="sxs-lookup"><span data-stu-id="8107b-106">Or, you can define a Virtual Machine, Virtual Network and Storage Account, and deploy that infrastructure along with a script that is executed on Virtual Machine.</span></span> <span data-ttu-id="8107b-107">**Azure 資源群組** 部署專案可讓您在單一、可重複執行的作業中部署所有所需的資源。</span><span class="sxs-lookup"><span data-stu-id="8107b-107">The **Azure Resource Group** deployment project enables you to deploy all the needed resources in a single, repeatable operation.</span></span> <span data-ttu-id="8107b-108">如需部署與管理資源的詳細資訊，請參閱 [Azure Resource Manager 概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8107b-108">For more information about deploying and managing your resources, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="8107b-109">Azure 資源群組專案包含 Azure Resource Manager JSON 範本，可定義部署到 Azure 的資源。</span><span class="sxs-lookup"><span data-stu-id="8107b-109">Azure Resource Group projects contain Azure Resource Manager JSON templates, which define the resources that you deploy to Azure.</span></span> <span data-ttu-id="8107b-110">若要了解資源管理員範本的元素，請參閱 [撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="8107b-110">To learn about the elements of the Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span> <span data-ttu-id="8107b-111">Visual Studio 可讓您編輯這些範本，並提供工具，可簡化範本的使用。</span><span class="sxs-lookup"><span data-stu-id="8107b-111">Visual Studio enables you to edit these templates, and provides tools that simplify working with templates.</span></span>

<span data-ttu-id="8107b-112">在本文中，您將會部署 Web 應用程式和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="8107b-112">In this article, you deploy a web app and SQL Database.</span></span> <span data-ttu-id="8107b-113">不過對於各種類型的資源來說，其步驟幾乎相同。</span><span class="sxs-lookup"><span data-stu-id="8107b-113">However, the steps are almost the same for any type resource.</span></span> <span data-ttu-id="8107b-114">您可以輕鬆地部署虛擬機器和其相關的資源。</span><span class="sxs-lookup"><span data-stu-id="8107b-114">You can as easily deploy a Virtual Machine and its related resources.</span></span> <span data-ttu-id="8107b-115">Visual Studio 針對部署常見案例提供許多不同的入門範本。</span><span class="sxs-lookup"><span data-stu-id="8107b-115">Visual Studio provides many different starter templates for deploying common scenarios.</span></span>

<span data-ttu-id="8107b-116">本文說明 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="8107b-116">This article shows Visual Studio 2017.</span></span> <span data-ttu-id="8107b-117">如果您使用 Visual Studio 2015 Update 2 和 Microsoft Azure SDK for .NET 2.9，或 Visual Studio 2013 與 Azure SDK 2.9，您的經驗會大致相同。</span><span class="sxs-lookup"><span data-stu-id="8107b-117">If you use Visual Studio 2015 Update 2 and Microsoft Azure SDK for .NET 2.9, or Visual Studio 2013 with Azure SDK 2.9, your experience is largely the same.</span></span> <span data-ttu-id="8107b-118">您可以使用 Azure SDK 2.6 或更新版本，不過您的使用者介面體驗可能會與本文所示的使用者介面不同。</span><span class="sxs-lookup"><span data-stu-id="8107b-118">You can use versions of the Azure SDK from 2.6 or later; however, your experience of the user interface may be different than the user interface shown in this article.</span></span> <span data-ttu-id="8107b-119">開始執行步驟前，我們強烈建議您安裝最新版本的 [Azure SDK](https://azure.microsoft.com/downloads/) 。</span><span class="sxs-lookup"><span data-stu-id="8107b-119">We strongly recommend that you install the latest version of the [Azure SDK](https://azure.microsoft.com/downloads/) before starting the steps.</span></span> 

## <a name="create-azure-resource-group-project"></a><span data-ttu-id="8107b-120">建立 Azure 資源群組專案</span><span class="sxs-lookup"><span data-stu-id="8107b-120">Create Azure Resource Group project</span></span>
<span data-ttu-id="8107b-121">在此程序中，您會利用 **Web 應用程式 + SQL** 範本建立 Azure 資源群組專案。</span><span class="sxs-lookup"><span data-stu-id="8107b-121">In this procedure, you create an Azure Resource Group project with a **Web app + SQL** template.</span></span>

1. <span data-ttu-id="8107b-122">在 Visual Studio 中，選擇 [檔案]、[新增專案]，再選擇 [C#] 或 [Visual Basic]。</span><span class="sxs-lookup"><span data-stu-id="8107b-122">In Visual Studio, choose **File**, **New Project**, choose **C#** or **Visual Basic**.</span></span> <span data-ttu-id="8107b-123">然後選擇 [雲端]，再選擇 [Azure 資源群組] 專案。</span><span class="sxs-lookup"><span data-stu-id="8107b-123">Then choose **Cloud**, and **Azure Resource Group** project.</span></span>
   
    ![雲端部署專案](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. <span data-ttu-id="8107b-125">選擇您想要部署至 Azure 資源管理員的範本。</span><span class="sxs-lookup"><span data-stu-id="8107b-125">Choose the template that you want to deploy to Azure Resource Manager.</span></span> <span data-ttu-id="8107b-126">請注意，根據您想要部署的專案類型，有許多不同的選項。</span><span class="sxs-lookup"><span data-stu-id="8107b-126">Notice there are many different options based on the type of project you wish to deploy.</span></span> <span data-ttu-id="8107b-127">在本文中，我們將選擇 **Web 應用程式 + SQL** 範本。</span><span class="sxs-lookup"><span data-stu-id="8107b-127">For this article, choose the **Web app + SQL** template.</span></span>
   
    ![選擇範本](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    <span data-ttu-id="8107b-129">您選擇的範本只是起點；您可以加入和移除資源，以滿足您的案例。</span><span class="sxs-lookup"><span data-stu-id="8107b-129">The template you pick is just a starting point; you can add and remove resources to fulfill your scenario.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8107b-130">Visual Studio 會在線上擷取一份可用範本清單。</span><span class="sxs-lookup"><span data-stu-id="8107b-130">Visual Studio retrieves a list of available templates online.</span></span> <span data-ttu-id="8107b-131">清單可能會變更。</span><span class="sxs-lookup"><span data-stu-id="8107b-131">The list may change.</span></span>
   > 
   > 
   
    <span data-ttu-id="8107b-132">Visual Studio 會建立 web 應用程式和 SQL Database 的資源群組部署專案。</span><span class="sxs-lookup"><span data-stu-id="8107b-132">Visual Studio creates a resource group deployment project for the web app and SQL database.</span></span>
3. <span data-ttu-id="8107b-133">若要查看建立的內容，請看部署專案中的節點。</span><span class="sxs-lookup"><span data-stu-id="8107b-133">To see what you created, look at the node in the deployment project.</span></span>
   
    ![顯示節點](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    <span data-ttu-id="8107b-135">因為我們針對此範例選擇 Web 應用程式 + SQL 範本，所以您會看到下列檔案：</span><span class="sxs-lookup"><span data-stu-id="8107b-135">Since we chose the Web app + SQL template for this example, you see the following files:</span></span> 
   
   | <span data-ttu-id="8107b-136">檔案名稱</span><span class="sxs-lookup"><span data-stu-id="8107b-136">File name</span></span> | <span data-ttu-id="8107b-137">說明</span><span class="sxs-lookup"><span data-stu-id="8107b-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="8107b-138">Deploy-AzureResourceGroup.ps1</span><span class="sxs-lookup"><span data-stu-id="8107b-138">Deploy-AzureResourceGroup.ps1</span></span> |<span data-ttu-id="8107b-139">叫用 PowerShell 命令部署至 Azure 資源管理員的 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="8107b-139">A PowerShell script that invokes PowerShell commands to deploy to Azure Resource Manager.</span></span><br /><span data-ttu-id="8107b-140">**注意** Visual studio 會使用此 PowerShell 指令碼部署您的範本。</span><span class="sxs-lookup"><span data-stu-id="8107b-140">**Note** Visual Studio uses this PowerShell script to deploy your template.</span></span> <span data-ttu-id="8107b-141">對此指令碼所進行的任何變更也會影響 Visual Studio 中的部署，因此請務必小心。</span><span class="sxs-lookup"><span data-stu-id="8107b-141">Any changes you make to this script affect deployment in Visual Studio, so be careful.</span></span> |
   | <span data-ttu-id="8107b-142">WebSiteSQLDatabase.json</span><span class="sxs-lookup"><span data-stu-id="8107b-142">WebSiteSQLDatabase.json</span></span> |<span data-ttu-id="8107b-143">Resource Manager 範本 (定義您想要部署至 Azure 的基礎結構)，以及在部署期間您可以提供的參數。</span><span class="sxs-lookup"><span data-stu-id="8107b-143">The Resource Manager template that defines the infrastructure you want deploy to Azure, and the parameters you can provide during deployment.</span></span> <span data-ttu-id="8107b-144">同時定義資源之間的相依性，讓 Resource Manager 以正確的順序部署資源。</span><span class="sxs-lookup"><span data-stu-id="8107b-144">It also defines the dependencies between the resources so Resource Manager deploys the resources in the correct order.</span></span> |
   | <span data-ttu-id="8107b-145">WebSiteSQLDatabase.parameters.json</span><span class="sxs-lookup"><span data-stu-id="8107b-145">WebSiteSQLDatabase.parameters.json</span></span> |<span data-ttu-id="8107b-146">參數檔案，包含範本所需的值。</span><span class="sxs-lookup"><span data-stu-id="8107b-146">A parameters file that contains values needed by the template.</span></span> <span data-ttu-id="8107b-147">您可以傳遞參數值以自訂每個部署。</span><span class="sxs-lookup"><span data-stu-id="8107b-147">You pass in parameter values to customize each deployment.</span></span> |
   
    <span data-ttu-id="8107b-148">所有資源群組部署專案都包含這些基本檔案。</span><span class="sxs-lookup"><span data-stu-id="8107b-148">All resource group deployment projects contain these basic files.</span></span> <span data-ttu-id="8107b-149">其他專案可能包含其他檔案以支援其他功能。</span><span class="sxs-lookup"><span data-stu-id="8107b-149">Other projects may contain additional files to support other functionality.</span></span>

## <a name="customize-the-resource-manager-template"></a><span data-ttu-id="8107b-150">自訂資源管理員範本</span><span class="sxs-lookup"><span data-stu-id="8107b-150">Customize the Resource Manager template</span></span>
<span data-ttu-id="8107b-151">您可以藉由修改 JSON 範本 (描述您想要部署的資源) 來自訂部署專案。</span><span class="sxs-lookup"><span data-stu-id="8107b-151">You can customize a deployment project by modifying the JSON templates that describe the resources you want to deploy.</span></span> <span data-ttu-id="8107b-152">JSON 代表 JavaScript 物件標記法，而且是很容易使用的序列化資料格式。</span><span class="sxs-lookup"><span data-stu-id="8107b-152">JSON stands for JavaScript Object Notation, and is a serialized data format that is easy to work with.</span></span> <span data-ttu-id="8107b-153">JSON 檔案使用的結構描述在每個檔案的頂端提供做為參考。</span><span class="sxs-lookup"><span data-stu-id="8107b-153">The JSON files use a schema that you reference at the top of each file.</span></span> <span data-ttu-id="8107b-154">如果您想要更了解這個結構描述，您可以下載並分析它。</span><span class="sxs-lookup"><span data-stu-id="8107b-154">If you want to understand the schema, you can download and analyze it.</span></span> <span data-ttu-id="8107b-155">結構描述會定義哪些是有效項目、欄位的類型和格式、可能的列舉值等等。</span><span class="sxs-lookup"><span data-stu-id="8107b-155">The schema defines what elements are valid, the types and formats of fields, the possible values of enumerated values, and so on.</span></span> <span data-ttu-id="8107b-156">若要了解資源管理員範本的元素，請參閱 [撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="8107b-156">To learn about the elements of the Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="8107b-157">若要使用您的範本，請開啟 **WebSiteSQLDatabase.json**。</span><span class="sxs-lookup"><span data-stu-id="8107b-157">To work on your template, open **WebSiteSQLDatabase.json**.</span></span>

<span data-ttu-id="8107b-158">Visual Studio 編輯器提供工具，協助您編輯 Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="8107b-158">The Visual Studio editor provides tools to assist you with editing the Resource Manager template.</span></span> <span data-ttu-id="8107b-159">[JSON 大綱]  視窗可讓您輕鬆查看在您的範本中定義的元素。</span><span class="sxs-lookup"><span data-stu-id="8107b-159">The **JSON Outline** window makes it easy to see the elements defined in your template.</span></span>

![顯示 JSON 大綱](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

<span data-ttu-id="8107b-161">選取大綱中的任何元素，會帶您前往範本的該部分，並且醒目提示對應的 JSON。</span><span class="sxs-lookup"><span data-stu-id="8107b-161">Selecting any of the elements in the outline takes you to that part of the template and highlights the corresponding JSON.</span></span>

![瀏覽 JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

<span data-ttu-id="8107b-163">您可以選取 [JSON 大綱] 視窗頂端的 [加入資源] 按鈕，或以滑鼠右鍵按一下 [資源]然後選取 [加入新資源]，藉以加入新資源。</span><span class="sxs-lookup"><span data-stu-id="8107b-163">You can add a resource by either selecting the **Add Resource** button at the top of the JSON Outline window, or by right-clicking **resources** and selecting **Add New Resource**.</span></span>

![新增資源](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

<span data-ttu-id="8107b-165">在本教學課程中，選取 [儲存體帳戶]  並提供它的名稱。</span><span class="sxs-lookup"><span data-stu-id="8107b-165">For this tutorial, select **Storage Account** and give it a name.</span></span> <span data-ttu-id="8107b-166">提供的名稱不能超過 11 個字元，而且只包含數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="8107b-166">Provide a name that is no more than 11 characters, and only contains numbers and lower-case letters.</span></span>

![加入儲存體](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

<span data-ttu-id="8107b-168">請注意，不只是加入資源，也會加入儲存體帳戶類型的參數，以及儲存體帳戶名稱的變數。</span><span class="sxs-lookup"><span data-stu-id="8107b-168">Notice that not only was the resource added, but also a parameter for the type storage account, and a variable for the name of the storage account.</span></span>

![顯示大綱](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

<span data-ttu-id="8107b-170">**storageType** 參數是以允許的類型與預設類型預先定義。</span><span class="sxs-lookup"><span data-stu-id="8107b-170">The **storageType** parameter is pre-defined with allowed types and a default type.</span></span> <span data-ttu-id="8107b-171">您可以保留這些值，或針對您的案例進行編輯。</span><span class="sxs-lookup"><span data-stu-id="8107b-171">You can leave these values or edit them for your scenario.</span></span> <span data-ttu-id="8107b-172">如果您不想要讓任何人透過此範本部署 **Premium_LRS** 儲存體帳戶，請將它從允許的類型中移除。</span><span class="sxs-lookup"><span data-stu-id="8107b-172">If you do not want anyone to deploy a **Premium_LRS** storage account through this template, remove it from the allowed types.</span></span> 

```json
"storageType": {
  "type": "string",
  "defaultValue": "Standard_LRS",
  "allowedValues": [
    "Standard_LRS",
    "Standard_ZRS",
    "Standard_GRS",
    "Standard_RAGRS"
  ]
}
```

<span data-ttu-id="8107b-173">Visual Studio 也會提供 Intellisense 以協助您了解編輯範本時可以使用哪些屬性。</span><span class="sxs-lookup"><span data-stu-id="8107b-173">Visual Studio also provides intellisense to help you understand what properties are available when editing the template.</span></span> <span data-ttu-id="8107b-174">例如，若要編輯 App Service 方案的屬性，請瀏覽至 **HostingPlan** 資源，並針對 [屬性] 加入值。</span><span class="sxs-lookup"><span data-stu-id="8107b-174">For example, to edit the properties for your App Service plan, navigate to the **HostingPlan** resource, and add a value for the **properties**.</span></span> <span data-ttu-id="8107b-175">請注意，Intellisense 會顯示可用的值，並提供該值的描述。</span><span class="sxs-lookup"><span data-stu-id="8107b-175">Notice that intellisense shows the available values and provides a description of that value.</span></span>

![顯示 intellisense](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

<span data-ttu-id="8107b-177">您可以將 **numberOfWorkers** 設定為 1。</span><span class="sxs-lookup"><span data-stu-id="8107b-177">You can set **numberOfWorkers** to 1.</span></span>

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-the-resource-group-project-to-azure"></a><span data-ttu-id="8107b-178">將資源群組部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="8107b-178">Deploy the Resource Group project to Azure</span></span>
<span data-ttu-id="8107b-179">您現在已可開始部署您的專案。</span><span class="sxs-lookup"><span data-stu-id="8107b-179">You are now ready to deploy your project.</span></span> <span data-ttu-id="8107b-180">當您部署 Azure 資源群組專案時，您會將它部署至 Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="8107b-180">When you deploy an Azure Resource Group project, you deploy it to an Azure resource group.</span></span> <span data-ttu-id="8107b-181">資源群組是共用共同生命週期的資源邏輯分組。</span><span class="sxs-lookup"><span data-stu-id="8107b-181">The resource group is a logical grouping of resources that share a common lifecycle.</span></span>

1. <span data-ttu-id="8107b-182">在部署專案節點的捷徑功能表上，選擇 [部署] > [新增]。</span><span class="sxs-lookup"><span data-stu-id="8107b-182">On the shortcut menu of the deployment project node, choose **Deploy** > **New**.</span></span>
   
    ![部署，新的部署功能表項目](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    <span data-ttu-id="8107b-184">[部署到資源群組]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="8107b-184">The **Deploy to Resource Group** dialog box appears.</span></span>
   
    ![[部署到資源群組] 對話方塊](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. <span data-ttu-id="8107b-186">在 [資源群組]  下拉式方塊中，選擇現有資源群組或建立新群組。</span><span class="sxs-lookup"><span data-stu-id="8107b-186">In the **Resource group** dropdown box, choose an existing resource group or create a new one.</span></span> <span data-ttu-id="8107b-187">若要建立資源群組，請開啟 [資源群組] 下拉式方塊，然後選擇 [新建]。</span><span class="sxs-lookup"><span data-stu-id="8107b-187">To create a resource group, open the **Resource Group** dropdown box and choose **Create New**.</span></span>
   
    ![[部署到資源群組] 對話方塊](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    <span data-ttu-id="8107b-189">[建立資源群組]  對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="8107b-189">The **Create Resource Group** dialog box appears.</span></span> <span data-ttu-id="8107b-190">給予群組名稱與位置，然後選取 [建立]  按鈕。</span><span class="sxs-lookup"><span data-stu-id="8107b-190">Give your group a name and location, and select the **Create** button.</span></span>
   
    ![[建立資源群組] 對話方塊](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. <span data-ttu-id="8107b-192">選取 [編輯參數]  按鈕，以編輯部署的參數。</span><span class="sxs-lookup"><span data-stu-id="8107b-192">Edit the parameters for the deployment by selecting the **Edit Parameters** button.</span></span>
   
    ![[編輯參數] 按鈕](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. <span data-ttu-id="8107b-194">提供空白參數的值，然後選取 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8107b-194">Provide values for the empty parameters and select the **Save** button.</span></span> <span data-ttu-id="8107b-195">空白參數為 **hostingPlanName**、**administratorLogin**、**administratorLoginPassword** 和 **databaseName**。</span><span class="sxs-lookup"><span data-stu-id="8107b-195">The empty parameters are **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, and **databaseName**.</span></span>
   
    <span data-ttu-id="8107b-196">**hostingPlanName** 指定要建立之 [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) 的名稱。</span><span class="sxs-lookup"><span data-stu-id="8107b-196">**hostingPlanName** specifies a name for the [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) to create.</span></span> 
   
    <span data-ttu-id="8107b-197">**administratorLogin** 指定 SQL Server 系統管理員的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="8107b-197">**administratorLogin** specifies the user name for the SQL Server administrator.</span></span> <span data-ttu-id="8107b-198">請勿使用常見的系統管理員名稱，例如 **sa** 或 **admin**。</span><span class="sxs-lookup"><span data-stu-id="8107b-198">Do not use common admin names like **sa** or **admin**.</span></span> 
   
    <span data-ttu-id="8107b-199">**AdministratorLoginPassword** 指定 SQL Server 系統管理員的密碼。</span><span class="sxs-lookup"><span data-stu-id="8107b-199">The **administratorLoginPassword** specifies a password for SQL Server administrator.</span></span> <span data-ttu-id="8107b-200">[將密碼儲存為參數檔案中的純文字]  選項並不安全；因此，請勿選取此選項。</span><span class="sxs-lookup"><span data-stu-id="8107b-200">The **Save passwords as plain text in the parameters file** option is not secure; therefore, do not select this option.</span></span> <span data-ttu-id="8107b-201">因為不會以純文字方式儲存密碼，所以您必須在部署期間再次提供此密碼。</span><span class="sxs-lookup"><span data-stu-id="8107b-201">Since the password is not saved as plain text, you need to provide this password again during deployment.</span></span> 
   
    <span data-ttu-id="8107b-202">**databaseName** 指定要建立之資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="8107b-202">**databaseName** specifies a name for the database to create.</span></span> 
   
    ![[編輯參數] 對話方塊](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. <span data-ttu-id="8107b-204">選擇 [部署] 按鈕，將專案部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="8107b-204">Choose the **Deploy** button to deploy the project to Azure.</span></span> <span data-ttu-id="8107b-205">PowerShell 主控台會在 Visual Studio 執行個體的外部開啟。</span><span class="sxs-lookup"><span data-stu-id="8107b-205">A PowerShell console opens outside of the Visual Studio instance.</span></span> <span data-ttu-id="8107b-206">出現提示時，請在 PowerShell 主控台中輸入 SQL Server 系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="8107b-206">Enter the SQL Server administrator password in the PowerShell console when prompted.</span></span> <span data-ttu-id="8107b-207">**PowerShell 主控台可能會隱藏在其他項目之後或在工作列中最小化。**</span><span class="sxs-lookup"><span data-stu-id="8107b-207">**Your PowerShell console may be hidden behind other items or minimized in the task bar.**</span></span> <span data-ttu-id="8107b-208">尋找此主控台並加以選取，以便提供密碼。</span><span class="sxs-lookup"><span data-stu-id="8107b-208">Look for this console and select it to provide the password.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="8107b-209">Visual Studio 可能會要求您安裝 Azure PowerShell Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="8107b-209">Visual Studio may ask you to install the Azure PowerShell cmdlets.</span></span> <span data-ttu-id="8107b-210">您需要 Azure PowerShell Cmdlet 才能成功部署資源群組。</span><span class="sxs-lookup"><span data-stu-id="8107b-210">You need the Azure PowerShell cmdlets to successfully deploy resource groups.</span></span> <span data-ttu-id="8107b-211">如果出現提示，請予以安裝。</span><span class="sxs-lookup"><span data-stu-id="8107b-211">If prompted, install them.</span></span>
   > 
   > 
6. <span data-ttu-id="8107b-212">部署可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="8107b-212">The deployment may take a few minutes.</span></span> <span data-ttu-id="8107b-213">您可在 [輸出]  視窗中查看部署的狀態。</span><span class="sxs-lookup"><span data-stu-id="8107b-213">In the **Output** windows, you see the status of the deployment.</span></span> <span data-ttu-id="8107b-214">部署完成時，最後一則訊息會表示成功部署，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="8107b-214">When the deployment has finished, the last message indicates a successful deployment with something similar to:</span></span>
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' to resource group 'DemoSiteGroup'.
7. <span data-ttu-id="8107b-215">在瀏覽器中，開啟 [Azure 入口網站](https://portal.azure.com/) 並登入您的帳戶。</span><span class="sxs-lookup"><span data-stu-id="8107b-215">In a browser, open the [Azure portal](https://portal.azure.com/) and sign in to your account.</span></span> <span data-ttu-id="8107b-216">若要查看資源群組，請選取 [資源群組]  ，然後選取您部署所在的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8107b-216">To see the resource group, select **Resource groups** and the resource group you deployed to.</span></span>
   
    ![選取群組](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. <span data-ttu-id="8107b-218">您會看到所有已部署的資源。</span><span class="sxs-lookup"><span data-stu-id="8107b-218">You see all the deployed resources.</span></span> <span data-ttu-id="8107b-219">請注意，儲存體帳戶的名稱不完全是新增該資源時所指定的名稱。</span><span class="sxs-lookup"><span data-stu-id="8107b-219">Notice that the name of the storage account is not exactly what you specified when adding that resource.</span></span> <span data-ttu-id="8107b-220">儲存體帳戶必須是獨一無二的。</span><span class="sxs-lookup"><span data-stu-id="8107b-220">The storage account must be unique.</span></span> <span data-ttu-id="8107b-221">範本會在您所提供的名稱中自動新增字元字串，以提供唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="8107b-221">The template automatically adds a string of characters to the name you provided to provide a unique name.</span></span> 
   
    ![顯示資源](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. <span data-ttu-id="8107b-223">如果您進行變更並想要重新部署專案，可以從 Azure 資源群組專案的捷徑功能表選擇現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8107b-223">If you make changes and want to redeploy your project, choose the existing resource group from the shortcut menu of Azure resource group project.</span></span> <span data-ttu-id="8107b-224">在捷徑功能表上，選擇 [部署] ，然後選擇您部署的資源群組。</span><span class="sxs-lookup"><span data-stu-id="8107b-224">On the shortcut menu, choose **Deploy**, and then choose the resource group you deployed.</span></span>
   
    ![已部署 Azure 資源群組](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a><span data-ttu-id="8107b-226">以您的基礎結構部署程式碼</span><span class="sxs-lookup"><span data-stu-id="8107b-226">Deploy code with your infrastructure</span></span>
<span data-ttu-id="8107b-227">此時，您已為您的應用程式部署基礎結構，但是專案尚未部署實際程式碼。</span><span class="sxs-lookup"><span data-stu-id="8107b-227">At this point, you have deployed the infrastructure for your app, but there is no actual code deployed with the project.</span></span> <span data-ttu-id="8107b-228">本文說明如何在部署期間部署 Web 應用程式和 SQL Database 資料表。</span><span class="sxs-lookup"><span data-stu-id="8107b-228">This article shows how to deploy a web app and SQL Database tables during deployment.</span></span> <span data-ttu-id="8107b-229">如果您是部署虛擬機器而不是 Web 應用程式，您想要在機器上執行一些程式碼做為部署的一部分。</span><span class="sxs-lookup"><span data-stu-id="8107b-229">If you are deploying a Virtual Machine instead of a web app, you want to run some code on the machine as part of deployment.</span></span> <span data-ttu-id="8107b-230">部署 Web 應用程式的程式碼或設定虛擬機器的程序幾乎完全相同。</span><span class="sxs-lookup"><span data-stu-id="8107b-230">The process for deploying code for a web app or for setting up a Virtual Machine is almost the same.</span></span>

1. <span data-ttu-id="8107b-231">將專案新增至您的 Visual Studio 方案。</span><span class="sxs-lookup"><span data-stu-id="8107b-231">Add a project to your Visual Studio solution.</span></span> <span data-ttu-id="8107b-232">以滑鼠右鍵按一下方案，然後選取 [新增] > [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="8107b-232">Right-click the solution, and select **Add** > **New Project**.</span></span>
   
    ![新增專案](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. <span data-ttu-id="8107b-234">新增 **ASP.NET Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8107b-234">Add an **ASP.NET Web Application**.</span></span> 
   
    ![加入 Web 應用程式](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. <span data-ttu-id="8107b-236">選取 **MVC**。</span><span class="sxs-lookup"><span data-stu-id="8107b-236">Select **MVC**.</span></span>
   
    ![選取 MVC](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. <span data-ttu-id="8107b-238">在 Visual Studio 建立 Web 應用程式之後，您會在方案中看到這兩個專案。</span><span class="sxs-lookup"><span data-stu-id="8107b-238">After Visual Studio creates your web app, you see both projects in the solution.</span></span>
   
    ![顯示專案](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. <span data-ttu-id="8107b-240">現在，您必須確定資源群組專案已察覺新的專案。</span><span class="sxs-lookup"><span data-stu-id="8107b-240">Now, you need to make sure your resource group project is aware of the new project.</span></span> <span data-ttu-id="8107b-241">回到您的資源群組專案 (AzureResourceGroup1)。</span><span class="sxs-lookup"><span data-stu-id="8107b-241">Go back to your resource group project (AzureResourceGroup1).</span></span> <span data-ttu-id="8107b-242">以滑鼠右鍵按一下 [參考]，然後選取 [新增參考]。</span><span class="sxs-lookup"><span data-stu-id="8107b-242">Right-click **References** and select **Add Reference**.</span></span>
   
    ![加入參考](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. <span data-ttu-id="8107b-244">選取您所建立的 Web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="8107b-244">Select the web app project that you created.</span></span>
   
    ![加入參考](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    <span data-ttu-id="8107b-246">加入參考，您可以將 Web 應用程式專案連結至資源群組專案中，並自動設定三個重要屬性。</span><span class="sxs-lookup"><span data-stu-id="8107b-246">By adding a reference, you link the web app project to the resource group project, and automatically set three key properties.</span></span> <span data-ttu-id="8107b-247">您會在參考的 [屬性]  視窗中看到這些屬性。</span><span class="sxs-lookup"><span data-stu-id="8107b-247">You see these properties in the **Properties** window for the reference.</span></span>
   
      ![查看參考](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    <span data-ttu-id="8107b-249">屬性如下︰</span><span class="sxs-lookup"><span data-stu-id="8107b-249">The properties are:</span></span>
   
   * <span data-ttu-id="8107b-250">[其他屬性]  包含會推送至 Azure 儲存體的 Web 部署套件預備位置。</span><span class="sxs-lookup"><span data-stu-id="8107b-250">The **Additional Properties** contains the web deployment package staging location that is pushed to the Azure Storage.</span></span> <span data-ttu-id="8107b-251">請注意資料夾 (ExampleApp) 和檔案 (package.zip)。</span><span class="sxs-lookup"><span data-stu-id="8107b-251">Note the folder (ExampleApp) and file (package.zip).</span></span> <span data-ttu-id="8107b-252">您必須知道這些值，因為您會提供這些值做為部署應用程式時的參數。</span><span class="sxs-lookup"><span data-stu-id="8107b-252">You need to know these values because you provide them as parameters when deploying the app.</span></span> 
   * <span data-ttu-id="8107b-253">[包含檔案路徑]  包含建立套件所在的路徑。</span><span class="sxs-lookup"><span data-stu-id="8107b-253">The **Include File Path** contains the path where the package is created.</span></span> <span data-ttu-id="8107b-254">[包含目標]  包含部署執行的命令。</span><span class="sxs-lookup"><span data-stu-id="8107b-254">The **Include Targets** contains the command that deployment executes.</span></span> 
   * <span data-ttu-id="8107b-255">預設值 [建立封裝]  會讓部署建立 Web 部署封裝 (package.zip)。</span><span class="sxs-lookup"><span data-stu-id="8107b-255">The default value of **Build;Package** enables the deployment to build and create a web deployment package (package.zip).</span></span>  
     
     <span data-ttu-id="8107b-256">您不需要發佈設定檔，因為部署會從屬性取得必要的資訊來建立套件。</span><span class="sxs-lookup"><span data-stu-id="8107b-256">You do not need a publish profile as the deployment gets the necessary information from the properties to create the package.</span></span>
7. <span data-ttu-id="8107b-257">請回到 WebSiteSQLDatabase.json，並將資源新增至範本。</span><span class="sxs-lookup"><span data-stu-id="8107b-257">Go back to WebSiteSQLDatabase.json and add a resource to the template.</span></span>
   
    ![新增資源](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. <span data-ttu-id="8107b-259">這次請選取 [Web Deploy for Web Apps] 。</span><span class="sxs-lookup"><span data-stu-id="8107b-259">This time select **Web Deploy for Web Apps**.</span></span> 
   
    ![加入 Web 部署](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. <span data-ttu-id="8107b-261">將您的資源群組專案重新部署至資源群組。</span><span class="sxs-lookup"><span data-stu-id="8107b-261">Redeploy your resource group project to the resource group.</span></span> <span data-ttu-id="8107b-262">這次還有一些新的參數。</span><span class="sxs-lookup"><span data-stu-id="8107b-262">This time there are some new parameters.</span></span> <span data-ttu-id="8107b-263">您不需要提供 **_artifactsLocation** 或 **_artifactsLocationSasToken** 的值，因為 Visual Studio 會自動產生這些值。</span><span class="sxs-lookup"><span data-stu-id="8107b-263">You do not need to provide values for **_artifactsLocation** or **_artifactsLocationSasToken** because Visual Studio automatically generates those values.</span></span> <span data-ttu-id="8107b-264">不過，您必須將資料夾和檔案名稱設定為包含部署套件的路徑 (如下圖中顯示的 **ExampleAppPackageFolder** 和 **ExampleAppPackageFileName**)。</span><span class="sxs-lookup"><span data-stu-id="8107b-264">However, you have to set the folder and file name to the path that contains the deployment package (shown as **ExampleAppPackageFolder** and **ExampleAppPackageFileName** in the following image).</span></span> <span data-ttu-id="8107b-265">提供您稍早在參考屬性 (**ExampleApp** 和 **package.zip**) 中看到的值。</span><span class="sxs-lookup"><span data-stu-id="8107b-265">Provide the values you saw earlier in the reference properties (**ExampleApp** and **package.zip**).</span></span>
   
    ![加入 Web 部署](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    <span data-ttu-id="8107b-267">對於 [構件儲存體帳戶] ，選取與此資源群組一起部署的帳戶。</span><span class="sxs-lookup"><span data-stu-id="8107b-267">For the **Artifact storage account**, select the one deployed with this resource group.</span></span>
10. <span data-ttu-id="8107b-268">部署完成後，請在入口網站中選取您的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8107b-268">After the deployment has finished, select your web app in the portal.</span></span> <span data-ttu-id="8107b-269">按一下 URL 以瀏覽至此網站。</span><span class="sxs-lookup"><span data-stu-id="8107b-269">Select the URL to browse to the site.</span></span>
    
     ![瀏覽網站](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. <span data-ttu-id="8107b-271">請注意，您已成功部署預設的 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="8107b-271">Notice that you have successfully deployed the default ASP.NET app.</span></span>
    
     ![顯示已部署的應用程式](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a><span data-ttu-id="8107b-273">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8107b-273">Next steps</span></span>
* <span data-ttu-id="8107b-274">若要了解透過入口網站管理資源，請參閱 [使用 Azure 入口網站來管理您的 Azure 資源](resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8107b-274">To learn about managing your resources through the portal, see [Using the Azure portal to manage your Azure resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="8107b-275">若要了解範本，請參閱 [撰寫 Azure Resource Manager 範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="8107b-275">To learn more about templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

