---
title: "aaaVisual Studio Azure 資源群組專案 |Microsoft 文件"
description: "使用 Visual Studio toocreate Azure 資源群組專案並將部署 hello 資源 tooAzure。"
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
ms.openlocfilehash: 672c1e71fb809b3b547f0fad30240d45de1ba923
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="creating-and-deploying-azure-resource-groups-through-visual-studio"></a><span data-ttu-id="51b71-103">透過 Visual Studio 建立與部署 Azure 資源群組</span><span class="sxs-lookup"><span data-stu-id="51b71-103">Creating and deploying Azure resource groups through Visual Studio</span></span>
<span data-ttu-id="51b71-104">與 Visual Studio 和 hello [Azure SDK](https://azure.microsoft.com/downloads/)，您可以建立您的基礎結構和程式碼 tooAzure 會將部署的專案。</span><span class="sxs-lookup"><span data-stu-id="51b71-104">With Visual Studio and hello [Azure SDK](https://azure.microsoft.com/downloads/), you can create a project that deploys your infrastructure and code tooAzure.</span></span> <span data-ttu-id="51b71-105">例如，您可以定義 hello web 主機、 網站和資料庫應用程式和部署該基礎結構，以及 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="51b71-105">For example, you can define hello web host, web site, and database for your app, and deploy that infrastructure along with hello code.</span></span> <span data-ttu-id="51b71-106">或者，您可以定義虛擬機器、虛擬網路和儲存體帳戶，並且部署該基礎結構以及在虛擬機器上執行的指令碼。</span><span class="sxs-lookup"><span data-stu-id="51b71-106">Or, you can define a Virtual Machine, Virtual Network and Storage Account, and deploy that infrastructure along with a script that is executed on Virtual Machine.</span></span> <span data-ttu-id="51b71-107">hello **Azure 資源群組**部署專案可讓您 toodeploy 單一、 可重複執行作業中的所有所需的 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="51b71-107">hello **Azure Resource Group** deployment project enables you toodeploy all hello needed resources in a single, repeatable operation.</span></span> <span data-ttu-id="51b71-108">如需部署與管理資源的詳細資訊，請參閱 [Azure Resource Manager 概觀](resource-group-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="51b71-108">For more information about deploying and managing your resources, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

<span data-ttu-id="51b71-109">Azure 資源群組專案包含 Azure 資源管理員 JSON 範本，其中定義部署 tooAzure hello 資源。</span><span class="sxs-lookup"><span data-stu-id="51b71-109">Azure Resource Group projects contain Azure Resource Manager JSON templates, which define hello resources that you deploy tooAzure.</span></span> <span data-ttu-id="51b71-110">toolearn 有關 hello 元素 hello 資源管理員範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="51b71-110">toolearn about hello elements of hello Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span> <span data-ttu-id="51b71-111">Visual Studio 可讓您 tooedit 這些範本，並提供工具，可簡化範本使用。</span><span class="sxs-lookup"><span data-stu-id="51b71-111">Visual Studio enables you tooedit these templates, and provides tools that simplify working with templates.</span></span>

<span data-ttu-id="51b71-112">在本文中，您將會部署 Web 應用程式和 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="51b71-112">In this article, you deploy a web app and SQL Database.</span></span> <span data-ttu-id="51b71-113">不過，hello 步驟 hello 是幾乎相同的任何類型的資源。</span><span class="sxs-lookup"><span data-stu-id="51b71-113">However, hello steps are almost hello same for any type resource.</span></span> <span data-ttu-id="51b71-114">您可以輕鬆地部署虛擬機器和其相關的資源。</span><span class="sxs-lookup"><span data-stu-id="51b71-114">You can as easily deploy a Virtual Machine and its related resources.</span></span> <span data-ttu-id="51b71-115">Visual Studio 針對部署常見案例提供許多不同的入門範本。</span><span class="sxs-lookup"><span data-stu-id="51b71-115">Visual Studio provides many different starter templates for deploying common scenarios.</span></span>

<span data-ttu-id="51b71-116">本文說明 Visual Studio 2017。</span><span class="sxs-lookup"><span data-stu-id="51b71-116">This article shows Visual Studio 2017.</span></span> <span data-ttu-id="51b71-117">如果您使用 Visual Studio 2015 Update 2 和 Microsoft Azure SDK for.NET 2.9 或 Visual Studio 2013 與 Azure SDK 2.9 中，您的體驗主要是 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="51b71-117">If you use Visual Studio 2015 Update 2 and Microsoft Azure SDK for .NET 2.9, or Visual Studio 2013 with Azure SDK 2.9, your experience is largely hello same.</span></span> <span data-ttu-id="51b71-118">您可以使用 hello Azure SDK 2.6 或更新版本的版本不過，您的經驗 hello 使用者介面的可能不同於本文中所顯示的 hello 使用者介面。</span><span class="sxs-lookup"><span data-stu-id="51b71-118">You can use versions of hello Azure SDK from 2.6 or later; however, your experience of hello user interface may be different than hello user interface shown in this article.</span></span> <span data-ttu-id="51b71-119">我們強烈建議您安裝新版 hello hello [Azure SDK](https://azure.microsoft.com/downloads/)啟動 hello 步驟之前。</span><span class="sxs-lookup"><span data-stu-id="51b71-119">We strongly recommend that you install hello latest version of hello [Azure SDK](https://azure.microsoft.com/downloads/) before starting hello steps.</span></span> 

## <a name="create-azure-resource-group-project"></a><span data-ttu-id="51b71-120">建立 Azure 資源群組專案</span><span class="sxs-lookup"><span data-stu-id="51b71-120">Create Azure Resource Group project</span></span>
<span data-ttu-id="51b71-121">在此程序中，您會利用 **Web 應用程式 + SQL** 範本建立 Azure 資源群組專案。</span><span class="sxs-lookup"><span data-stu-id="51b71-121">In this procedure, you create an Azure Resource Group project with a **Web app + SQL** template.</span></span>

1. <span data-ttu-id="51b71-122">在 Visual Studio 中，選擇 [檔案]、[新增專案]，再選擇 [C#] 或 [Visual Basic]。</span><span class="sxs-lookup"><span data-stu-id="51b71-122">In Visual Studio, choose **File**, **New Project**, choose **C#** or **Visual Basic**.</span></span> <span data-ttu-id="51b71-123">然後選擇 [雲端]，再選擇 [Azure 資源群組] 專案。</span><span class="sxs-lookup"><span data-stu-id="51b71-123">Then choose **Cloud**, and **Azure Resource Group** project.</span></span>
   
    ![雲端部署專案](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-project.png)
2. <span data-ttu-id="51b71-125">選擇 hello 範本的 toodeploy tooAzure 資源管理員。</span><span class="sxs-lookup"><span data-stu-id="51b71-125">Choose hello template that you want toodeploy tooAzure Resource Manager.</span></span> <span data-ttu-id="51b71-126">請注意，有許多不同的選項根據 hello 輸入專案的您希望 toodeploy。</span><span class="sxs-lookup"><span data-stu-id="51b71-126">Notice there are many different options based on hello type of project you wish toodeploy.</span></span> <span data-ttu-id="51b71-127">本文中，選擇 hello **Web 應用程式 + SQL**範本。</span><span class="sxs-lookup"><span data-stu-id="51b71-127">For this article, choose hello **Web app + SQL** template.</span></span>
   
    ![選擇範本](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-project.png)
   
    <span data-ttu-id="51b71-129">您挑選的 hello 範本，只要開始;您可以加入和移除資源 toofulfill 您的案例。</span><span class="sxs-lookup"><span data-stu-id="51b71-129">hello template you pick is just a starting point; you can add and remove resources toofulfill your scenario.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="51b71-130">Visual Studio 會在線上擷取一份可用範本清單。</span><span class="sxs-lookup"><span data-stu-id="51b71-130">Visual Studio retrieves a list of available templates online.</span></span> <span data-ttu-id="51b71-131">hello 清單可能會變更。</span><span class="sxs-lookup"><span data-stu-id="51b71-131">hello list may change.</span></span>
   > 
   > 
   
    <span data-ttu-id="51b71-132">Visual Studio 建立 hello web 應用程式和 SQL database 的資源群組部署專案。</span><span class="sxs-lookup"><span data-stu-id="51b71-132">Visual Studio creates a resource group deployment project for hello web app and SQL database.</span></span>
3. <span data-ttu-id="51b71-133">toosee 您建立的內容，查看在 hello hello 部署專案中的節點。</span><span class="sxs-lookup"><span data-stu-id="51b71-133">toosee what you created, look at hello node in hello deployment project.</span></span>
   
    ![顯示節點](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-items.png)
   
    <span data-ttu-id="51b71-135">因為我們選擇 hello Web 應用程式 + SQL 範本，此範例中，您會看見 hello 下列檔案：</span><span class="sxs-lookup"><span data-stu-id="51b71-135">Since we chose hello Web app + SQL template for this example, you see hello following files:</span></span> 
   
   | <span data-ttu-id="51b71-136">檔案名稱</span><span class="sxs-lookup"><span data-stu-id="51b71-136">File name</span></span> | <span data-ttu-id="51b71-137">說明</span><span class="sxs-lookup"><span data-stu-id="51b71-137">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="51b71-138">Deploy-AzureResourceGroup.ps1</span><span class="sxs-lookup"><span data-stu-id="51b71-138">Deploy-AzureResourceGroup.ps1</span></span> |<span data-ttu-id="51b71-139">PowerShell 命令 toodeploy tooAzure 資源管理員會叫用 PowerShell 指令碼。</span><span class="sxs-lookup"><span data-stu-id="51b71-139">A PowerShell script that invokes PowerShell commands toodeploy tooAzure Resource Manager.</span></span><br /><span data-ttu-id="51b71-140">**請注意**Visual Studio 會使用此 PowerShell 指令碼 toodeploy 您的範本。</span><span class="sxs-lookup"><span data-stu-id="51b71-140">**Note** Visual Studio uses this PowerShell script toodeploy your template.</span></span> <span data-ttu-id="51b71-141">任何您所做變更影響在 Visual Studio 中的部署，因此請謹慎的 toothis 指令碼。</span><span class="sxs-lookup"><span data-stu-id="51b71-141">Any changes you make toothis script affect deployment in Visual Studio, so be careful.</span></span> |
   | <span data-ttu-id="51b71-142">WebSiteSQLDatabase.json</span><span class="sxs-lookup"><span data-stu-id="51b71-142">WebSiteSQLDatabase.json</span></span> |<span data-ttu-id="51b71-143">定義您要部署 tooAzure，hello 基礎結構和 hello 參數，您可以在部署期間提供的 hello Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="51b71-143">hello Resource Manager template that defines hello infrastructure you want deploy tooAzure, and hello parameters you can provide during deployment.</span></span> <span data-ttu-id="51b71-144">它也會定義 hello hello 資源，因此資源管理員部署的 hello 正確的順序中的 hello 資源之間的相依性。</span><span class="sxs-lookup"><span data-stu-id="51b71-144">It also defines hello dependencies between hello resources so Resource Manager deploys hello resources in hello correct order.</span></span> |
   | <span data-ttu-id="51b71-145">WebSiteSQLDatabase.parameters.json</span><span class="sxs-lookup"><span data-stu-id="51b71-145">WebSiteSQLDatabase.parameters.json</span></span> |<span data-ttu-id="51b71-146">包含 hello 範本所需值的參數檔案。</span><span class="sxs-lookup"><span data-stu-id="51b71-146">A parameters file that contains values needed by hello template.</span></span> <span data-ttu-id="51b71-147">您要傳入參數值 toocustomize 每個部署。</span><span class="sxs-lookup"><span data-stu-id="51b71-147">You pass in parameter values toocustomize each deployment.</span></span> |
   
    <span data-ttu-id="51b71-148">所有資源群組部署專案都包含這些基本檔案。</span><span class="sxs-lookup"><span data-stu-id="51b71-148">All resource group deployment projects contain these basic files.</span></span> <span data-ttu-id="51b71-149">其他專案可能包含其他檔案 toosupport 其他功能。</span><span class="sxs-lookup"><span data-stu-id="51b71-149">Other projects may contain additional files toosupport other functionality.</span></span>

## <a name="customize-hello-resource-manager-template"></a><span data-ttu-id="51b71-150">自訂 hello Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="51b71-150">Customize hello Resource Manager template</span></span>
<span data-ttu-id="51b71-151">您可以修改描述您想要 toodeploy hello 資源的 hello JSON 範本，以自訂部署專案。</span><span class="sxs-lookup"><span data-stu-id="51b71-151">You can customize a deployment project by modifying hello JSON templates that describe hello resources you want toodeploy.</span></span> <span data-ttu-id="51b71-152">JSON 代表 JavaScript 物件標記法，而且會與簡單 toowork 的序列化的資料格式。</span><span class="sxs-lookup"><span data-stu-id="51b71-152">JSON stands for JavaScript Object Notation, and is a serialized data format that is easy toowork with.</span></span> <span data-ttu-id="51b71-153">hello JSON 檔案會使用您在每個檔案的 hello 頂端所參考的結構描述。</span><span class="sxs-lookup"><span data-stu-id="51b71-153">hello JSON files use a schema that you reference at hello top of each file.</span></span> <span data-ttu-id="51b71-154">如果您想 toounderstand hello 結構描述，您可以下載並進行分析。</span><span class="sxs-lookup"><span data-stu-id="51b71-154">If you want toounderstand hello schema, you can download and analyze it.</span></span> <span data-ttu-id="51b71-155">hello 結構描述會定義哪些項目都有效，hello 類型及格式的欄位，hello 可能值的列舉值，依此類推。</span><span class="sxs-lookup"><span data-stu-id="51b71-155">hello schema defines what elements are valid, hello types and formats of fields, hello possible values of enumerated values, and so on.</span></span> <span data-ttu-id="51b71-156">toolearn 有關 hello 元素 hello 資源管理員範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="51b71-156">toolearn about hello elements of hello Resource Manager template, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="51b71-157">toowork 您在範本上，開啟**WebSiteSQLDatabase.json**。</span><span class="sxs-lookup"><span data-stu-id="51b71-157">toowork on your template, open **WebSiteSQLDatabase.json**.</span></span>

<span data-ttu-id="51b71-158">hello Visual Studio 編輯器提供工具 tooassist 您編輯 hello Resource Manager 範本。</span><span class="sxs-lookup"><span data-stu-id="51b71-158">hello Visual Studio editor provides tools tooassist you with editing hello Resource Manager template.</span></span> <span data-ttu-id="51b71-159">hello **JSON 大綱**視窗可讓您的範本中定義的簡單 toosee hello 項目。</span><span class="sxs-lookup"><span data-stu-id="51b71-159">hello **JSON Outline** window makes it easy toosee hello elements defined in your template.</span></span>

![顯示 JSON 大綱](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-json-outline.png)

<span data-ttu-id="51b71-161">Hello 大綱 中選取任一 hello 項目會將您帶 toothat hello 範本的一部分，並反白顯示對應 JSON 的 hello。</span><span class="sxs-lookup"><span data-stu-id="51b71-161">Selecting any of hello elements in hello outline takes you toothat part of hello template and highlights hello corresponding JSON.</span></span>

![瀏覽 JSON](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/navigate-json.png)

<span data-ttu-id="51b71-163">您可以將資源加入其中一個選取的 hello**加入資源**hello 頂端的 hello [JSON 大綱] 視窗，或以滑鼠右鍵按一下按鈕，在**資源**，然後選取**加入新資源**.</span><span class="sxs-lookup"><span data-stu-id="51b71-163">You can add a resource by either selecting hello **Add Resource** button at hello top of hello JSON Outline window, or by right-clicking **resources** and selecting **Add New Resource**.</span></span>

![新增資源](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource.png)

<span data-ttu-id="51b71-165">在本教學課程中，選取 [儲存體帳戶]  並提供它的名稱。</span><span class="sxs-lookup"><span data-stu-id="51b71-165">For this tutorial, select **Storage Account** and give it a name.</span></span> <span data-ttu-id="51b71-166">提供的名稱不能超過 11 個字元，而且只包含數字和小寫字母。</span><span class="sxs-lookup"><span data-stu-id="51b71-166">Provide a name that is no more than 11 characters, and only contains numbers and lower-case letters.</span></span>

![加入儲存體](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-storage.png)

<span data-ttu-id="51b71-168">請注意，不只加入 hello 資源，但也 hello 的參數輸入儲存體帳戶和 hello hello 儲存體帳戶名稱的變數。</span><span class="sxs-lookup"><span data-stu-id="51b71-168">Notice that not only was hello resource added, but also a parameter for hello type storage account, and a variable for hello name of hello storage account.</span></span>

![顯示大綱](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-new-items.png)

<span data-ttu-id="51b71-170">hello **storageType**參數是預先定義允許的類型和預設類型。</span><span class="sxs-lookup"><span data-stu-id="51b71-170">hello **storageType** parameter is pre-defined with allowed types and a default type.</span></span> <span data-ttu-id="51b71-171">您可以保留這些值，或針對您的案例進行編輯。</span><span class="sxs-lookup"><span data-stu-id="51b71-171">You can leave these values or edit them for your scenario.</span></span> <span data-ttu-id="51b71-172">如果您不要的任何人 toodeploy **Premium_LRS**儲存體帳戶，透過這個範本中，會將它移除 hello 允許的類型。</span><span class="sxs-lookup"><span data-stu-id="51b71-172">If you do not want anyone toodeploy a **Premium_LRS** storage account through this template, remove it from hello allowed types.</span></span> 

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

<span data-ttu-id="51b71-173">Visual Studio 也提供編輯 hello 範本時，就可以使用 intellisense toohelp 您了解哪些屬性。</span><span class="sxs-lookup"><span data-stu-id="51b71-173">Visual Studio also provides intellisense toohelp you understand what properties are available when editing hello template.</span></span> <span data-ttu-id="51b71-174">例如，您的應用程式服務方案的 tooedit hello 屬性瀏覽 toohello **HostingPlan**資源，並新增值 hello**屬性**。</span><span class="sxs-lookup"><span data-stu-id="51b71-174">For example, tooedit hello properties for your App Service plan, navigate toohello **HostingPlan** resource, and add a value for hello **properties**.</span></span> <span data-ttu-id="51b71-175">請注意該 intellisense 會顯示 hello 可用的值，並提供該值的描述。</span><span class="sxs-lookup"><span data-stu-id="51b71-175">Notice that intellisense shows hello available values and provides a description of that value.</span></span>

![顯示 intellisense](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-intellisense.png)

<span data-ttu-id="51b71-177">您可以設定**numberOfWorkers** too1。</span><span class="sxs-lookup"><span data-stu-id="51b71-177">You can set **numberOfWorkers** too1.</span></span>

```json
"properties": {
  "name": "[parameters('hostingPlanName')]",
  "numberOfWorkers": 1
}
```

## <a name="deploy-hello-resource-group-project-tooazure"></a><span data-ttu-id="51b71-178">部署 hello 資源群組專案 tooAzure</span><span class="sxs-lookup"><span data-stu-id="51b71-178">Deploy hello Resource Group project tooAzure</span></span>
<span data-ttu-id="51b71-179">您會 toodeploy 現在準備好您的專案。</span><span class="sxs-lookup"><span data-stu-id="51b71-179">You are now ready toodeploy your project.</span></span> <span data-ttu-id="51b71-180">當您部署 Azure 資源群組專案時，您將它部署 tooan Azure 資源群組。</span><span class="sxs-lookup"><span data-stu-id="51b71-180">When you deploy an Azure Resource Group project, you deploy it tooan Azure resource group.</span></span> <span data-ttu-id="51b71-181">hello 資源群組是共用常見的生命週期資源的邏輯群組。</span><span class="sxs-lookup"><span data-stu-id="51b71-181">hello resource group is a logical grouping of resources that share a common lifecycle.</span></span>

1. <span data-ttu-id="51b71-182">Hello hello 部署專案節點的捷徑功能表，選擇 **部署** > **新增**。</span><span class="sxs-lookup"><span data-stu-id="51b71-182">On hello shortcut menu of hello deployment project node, choose **Deploy** > **New**.</span></span>
   
    ![部署，新的部署功能表項目](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/deploy.png)
   
    <span data-ttu-id="51b71-184">hello**部署 tooResource 群組** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="51b71-184">hello **Deploy tooResource Group** dialog box appears.</span></span>
   
    ![部署 tooResource 群組對話方塊](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployment.png)
2. <span data-ttu-id="51b71-186">在 hello**資源群組**下拉式方塊中，選擇現有的資源群組，或另外新建一個。</span><span class="sxs-lookup"><span data-stu-id="51b71-186">In hello **Resource group** dropdown box, choose an existing resource group or create a new one.</span></span> <span data-ttu-id="51b71-187">toocreate 資源群組中，開啟 hello**資源群組**下拉式清單方塊，然後選擇**新建**。</span><span class="sxs-lookup"><span data-stu-id="51b71-187">toocreate a resource group, open hello **Resource Group** dropdown box and choose **Create New**.</span></span>
   
    ![部署 tooResource 群組對話方塊](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-new-group.png)
   
    <span data-ttu-id="51b71-189">hello**建立資源群組** 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="51b71-189">hello **Create Resource Group** dialog box appears.</span></span> <span data-ttu-id="51b71-190">為您的群組的名稱和位置，然後選取 hello**建立** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51b71-190">Give your group a name and location, and select hello **Create** button.</span></span>
   
    ![[建立資源群組] 對話方塊](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/create-resource-group.png)
3. <span data-ttu-id="51b71-192">編輯 hello 部署的 hello 參數選取 hello**編輯參數** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51b71-192">Edit hello parameters for hello deployment by selecting hello **Edit Parameters** button.</span></span>
   
    ![[編輯參數] 按鈕](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/edit-parameters.png)
4. <span data-ttu-id="51b71-194">提供 hello 空參數的值，然後選取 hello**儲存** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51b71-194">Provide values for hello empty parameters and select hello **Save** button.</span></span> <span data-ttu-id="51b71-195">hello 空參數**hostingPlanName**， **administratorLogin**， **administratorLoginPassword**，和**databaseName**。</span><span class="sxs-lookup"><span data-stu-id="51b71-195">hello empty parameters are **hostingPlanName**, **administratorLogin**, **administratorLoginPassword**, and **databaseName**.</span></span>
   
    <span data-ttu-id="51b71-196">**hostingPlanName**指定名稱，以 hello [App Service 方案](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md)toocreate。</span><span class="sxs-lookup"><span data-stu-id="51b71-196">**hostingPlanName** specifies a name for hello [App Service plan](../app-service/azure-web-sites-web-hosting-plans-in-depth-overview.md) toocreate.</span></span> 
   
    <span data-ttu-id="51b71-197">**administratorLogin**指定 hello hello SQL Server 系統管理員的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="51b71-197">**administratorLogin** specifies hello user name for hello SQL Server administrator.</span></span> <span data-ttu-id="51b71-198">請勿使用常見的系統管理員名稱，例如 **sa** 或 **admin**。</span><span class="sxs-lookup"><span data-stu-id="51b71-198">Do not use common admin names like **sa** or **admin**.</span></span> 
   
    <span data-ttu-id="51b71-199">hello **administratorLoginPassword**指定 SQL Server 系統管理員的密碼。</span><span class="sxs-lookup"><span data-stu-id="51b71-199">hello **administratorLoginPassword** specifies a password for SQL Server administrator.</span></span> <span data-ttu-id="51b71-200">hello**以 hello 參數檔案中的純文字儲存密碼**選項不安全; 因此，請勿選取此選項。</span><span class="sxs-lookup"><span data-stu-id="51b71-200">hello **Save passwords as plain text in hello parameters file** option is not secure; therefore, do not select this option.</span></span> <span data-ttu-id="51b71-201">由於 hello 密碼不會儲存為純文字，您必須 tooprovide 這個密碼一次在部署期間。</span><span class="sxs-lookup"><span data-stu-id="51b71-201">Since hello password is not saved as plain text, you need tooprovide this password again during deployment.</span></span> 
   
    <span data-ttu-id="51b71-202">**databaseName**指定 hello 資料庫 toocreate 的名稱。</span><span class="sxs-lookup"><span data-stu-id="51b71-202">**databaseName** specifies a name for hello database toocreate.</span></span> 
   
    ![[編輯參數] 對話方塊](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/provide-parameters.png)
5. <span data-ttu-id="51b71-204">選擇 hello**部署**按鈕 toodeploy hello 專案 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="51b71-204">Choose hello **Deploy** button toodeploy hello project tooAzure.</span></span> <span data-ttu-id="51b71-205">PowerShell 主控台開啟 hello Visual Studio 執行個體的外部。</span><span class="sxs-lookup"><span data-stu-id="51b71-205">A PowerShell console opens outside of hello Visual Studio instance.</span></span> <span data-ttu-id="51b71-206">在 hello PowerShell 主控台中出現提示時輸入 hello SQL Server 系統管理員密碼。</span><span class="sxs-lookup"><span data-stu-id="51b71-206">Enter hello SQL Server administrator password in hello PowerShell console when prompted.</span></span> <span data-ttu-id="51b71-207">**PowerShell 主控台可能會隱藏在其他項目後面或 hello 工作列中的最小化。**</span><span class="sxs-lookup"><span data-stu-id="51b71-207">**Your PowerShell console may be hidden behind other items or minimized in hello task bar.**</span></span> <span data-ttu-id="51b71-208">尋找此主控台，並選取該 tooprovide hello 密碼。</span><span class="sxs-lookup"><span data-stu-id="51b71-208">Look for this console and select it tooprovide hello password.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="51b71-209">Visual Studio 可能會要求您 tooinstall hello Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="51b71-209">Visual Studio may ask you tooinstall hello Azure PowerShell cmdlets.</span></span> <span data-ttu-id="51b71-210">您需要 hello Azure PowerShell cmdlet toosuccessfully 部署資源群組。</span><span class="sxs-lookup"><span data-stu-id="51b71-210">You need hello Azure PowerShell cmdlets toosuccessfully deploy resource groups.</span></span> <span data-ttu-id="51b71-211">如果出現提示，請予以安裝。</span><span class="sxs-lookup"><span data-stu-id="51b71-211">If prompted, install them.</span></span>
   > 
   > 
6. <span data-ttu-id="51b71-212">hello 部署可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="51b71-212">hello deployment may take a few minutes.</span></span> <span data-ttu-id="51b71-213">在 hello**輸出**windows 中，您看到 hello 部署的 hello 狀態。</span><span class="sxs-lookup"><span data-stu-id="51b71-213">In hello **Output** windows, you see hello status of hello deployment.</span></span> <span data-ttu-id="51b71-214">Hello 部署完成時，hello 最後一則訊息表示成功的部署與類似的項目：</span><span class="sxs-lookup"><span data-stu-id="51b71-214">When hello deployment has finished, hello last message indicates a successful deployment with something similar to:</span></span>
   
        ... 
        18:00:58 - Successfully deployed template 'websitesqldatabase.json' tooresource group 'DemoSiteGroup'.
7. <span data-ttu-id="51b71-215">在瀏覽器中，開啟 hello [Azure 入口網站](https://portal.azure.com/)並登入 tooyour 帳戶。</span><span class="sxs-lookup"><span data-stu-id="51b71-215">In a browser, open hello [Azure portal](https://portal.azure.com/) and sign in tooyour account.</span></span> <span data-ttu-id="51b71-216">toosee hello 資源群組中，選取**資源群組**與您部署的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="51b71-216">toosee hello resource group, select **Resource groups** and hello resource group you deployed to.</span></span>
   
    ![選取群組](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-group.png)
8. <span data-ttu-id="51b71-218">您會看到部署的 hello 的所有資源。</span><span class="sxs-lookup"><span data-stu-id="51b71-218">You see all hello deployed resources.</span></span> <span data-ttu-id="51b71-219">請注意 hello 儲存體帳戶不是完全加入該資源時，指定您的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="51b71-219">Notice that hello name of hello storage account is not exactly what you specified when adding that resource.</span></span> <span data-ttu-id="51b71-220">hello 儲存體帳戶必須是唯一的。</span><span class="sxs-lookup"><span data-stu-id="51b71-220">hello storage account must be unique.</span></span> <span data-ttu-id="51b71-221">hello 範本會自動加入字串的字元 toohello 名稱提供 tooprovide 唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="51b71-221">hello template automatically adds a string of characters toohello name you provided tooprovide a unique name.</span></span> 
   
    ![顯示資源](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-resources.png)
9. <span data-ttu-id="51b71-223">如果您進行變更，而且想 tooredeploy 您的專案，請從 hello 的 Azure 資源群組專案的捷徑功能表選擇 hello 現有的資源群組。</span><span class="sxs-lookup"><span data-stu-id="51b71-223">If you make changes and want tooredeploy your project, choose hello existing resource group from hello shortcut menu of Azure resource group project.</span></span> <span data-ttu-id="51b71-224">Hello 快顯功能表上，選擇**部署**，然後選擇您所部署的 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="51b71-224">On hello shortcut menu, choose **Deploy**, and then choose hello resource group you deployed.</span></span>
   
    ![已部署 Azure 資源群組](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/redeploy.png)

## <a name="deploy-code-with-your-infrastructure"></a><span data-ttu-id="51b71-226">以您的基礎結構部署程式碼</span><span class="sxs-lookup"><span data-stu-id="51b71-226">Deploy code with your infrastructure</span></span>
<span data-ttu-id="51b71-227">此時，您應用程式部署 hello 基礎結構，但沒有實際程式碼與 hello 專案部署。</span><span class="sxs-lookup"><span data-stu-id="51b71-227">At this point, you have deployed hello infrastructure for your app, but there is no actual code deployed with hello project.</span></span> <span data-ttu-id="51b71-228">本文將說明如何 toodeploy web 應用程式和 SQL Database 資料表在部署期間。</span><span class="sxs-lookup"><span data-stu-id="51b71-228">This article shows how toodeploy a web app and SQL Database tables during deployment.</span></span> <span data-ttu-id="51b71-229">如果您要部署虛擬機器，而不是 web 應用程式，您要 toorun hello 做為部署的一部分的電腦上的某些程式碼。</span><span class="sxs-lookup"><span data-stu-id="51b71-229">If you are deploying a Virtual Machine instead of a web app, you want toorun some code on hello machine as part of deployment.</span></span> <span data-ttu-id="51b71-230">hello 程序部署 web 應用程式的程式碼，或將虛擬機器設定為幾乎 hello 相同。</span><span class="sxs-lookup"><span data-stu-id="51b71-230">hello process for deploying code for a web app or for setting up a Virtual Machine is almost hello same.</span></span>

1. <span data-ttu-id="51b71-231">加入專案 tooyour Visual Studio 方案。</span><span class="sxs-lookup"><span data-stu-id="51b71-231">Add a project tooyour Visual Studio solution.</span></span> <span data-ttu-id="51b71-232">Hello 方案上按一下滑鼠右鍵，然後選取**新增** > **新專案**。</span><span class="sxs-lookup"><span data-stu-id="51b71-232">Right-click hello solution, and select **Add** > **New Project**.</span></span>
   
    ![新增專案](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-project.png)
2. <span data-ttu-id="51b71-234">新增 **ASP.NET Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="51b71-234">Add an **ASP.NET Web Application**.</span></span> 
   
    ![加入 Web 應用程式](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-app.png)
3. <span data-ttu-id="51b71-236">選取 **MVC**。</span><span class="sxs-lookup"><span data-stu-id="51b71-236">Select **MVC**.</span></span>
   
    ![選取 MVC](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/select-mvc.png)
4. <span data-ttu-id="51b71-238">Visual Studio 會建立您的 web 應用程式之後，您會看到 hello 方案中的這兩個專案。</span><span class="sxs-lookup"><span data-stu-id="51b71-238">After Visual Studio creates your web app, you see both projects in hello solution.</span></span>
   
    ![顯示專案](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-projects.png)
5. <span data-ttu-id="51b71-240">現在，您必須確定您的資源群組專案可感知 hello 新專案的 toomake。</span><span class="sxs-lookup"><span data-stu-id="51b71-240">Now, you need toomake sure your resource group project is aware of hello new project.</span></span> <span data-ttu-id="51b71-241">返回 tooyour 資源群組專案 (AzureResourceGroup1)。</span><span class="sxs-lookup"><span data-stu-id="51b71-241">Go back tooyour resource group project (AzureResourceGroup1).</span></span> <span data-ttu-id="51b71-242">以滑鼠右鍵按一下 [參考]，然後選取 [新增參考]。</span><span class="sxs-lookup"><span data-stu-id="51b71-242">Right-click **References** and select **Add Reference**.</span></span>
   
    ![加入參考](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-new-reference.png)
6. <span data-ttu-id="51b71-244">選取您建立的 hello web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="51b71-244">Select hello web app project that you created.</span></span>
   
    ![加入參考](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-reference.png)
   
    <span data-ttu-id="51b71-246">藉由加入參考，將會連結 hello web 應用程式專案 toohello 資源群組專案，並自動設定三個索引鍵屬性。</span><span class="sxs-lookup"><span data-stu-id="51b71-246">By adding a reference, you link hello web app project toohello resource group project, and automatically set three key properties.</span></span> <span data-ttu-id="51b71-247">您會看到這些屬性在 hello**屬性**hello 參考的視窗。</span><span class="sxs-lookup"><span data-stu-id="51b71-247">You see these properties in hello **Properties** window for hello reference.</span></span>
   
      ![查看參考](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/see-reference.png)
   
    <span data-ttu-id="51b71-249">hello 屬性如下：</span><span class="sxs-lookup"><span data-stu-id="51b71-249">hello properties are:</span></span>
   
   * <span data-ttu-id="51b71-250">hello**其他屬性**包含預備位置，而被排除 toohello Azure 儲存體 hello web 部署套件。</span><span class="sxs-lookup"><span data-stu-id="51b71-250">hello **Additional Properties** contains hello web deployment package staging location that is pushed toohello Azure Storage.</span></span> <span data-ttu-id="51b71-251">請注意 hello 資料夾 (ExampleApp) 和檔案 (package.zip)。</span><span class="sxs-lookup"><span data-stu-id="51b71-251">Note hello folder (ExampleApp) and file (package.zip).</span></span> <span data-ttu-id="51b71-252">您需要 tooknow 這些值因為您提供為參數來部署 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51b71-252">You need tooknow these values because you provide them as parameters when deploying hello app.</span></span> 
   * <span data-ttu-id="51b71-253">hello**包含檔案路徑**包含 hello 路徑建立 hello 封裝的位置。</span><span class="sxs-lookup"><span data-stu-id="51b71-253">hello **Include File Path** contains hello path where hello package is created.</span></span> <span data-ttu-id="51b71-254">hello**包含目標**包含執行部署的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="51b71-254">hello **Include Targets** contains hello command that deployment executes.</span></span> 
   * <span data-ttu-id="51b71-255">hello 預設值是**建置。封裝**可讓 hello 部署 toobuild，並建立 web 部署套件 (package.zip)。</span><span class="sxs-lookup"><span data-stu-id="51b71-255">hello default value of **Build;Package** enables hello deployment toobuild and create a web deployment package (package.zip).</span></span>  
     
     <span data-ttu-id="51b71-256">您不需要的發行設定檔為 hello 部署從 hello 屬性 toocreate hello 封裝取得 hello 所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="51b71-256">You do not need a publish profile as hello deployment gets hello necessary information from hello properties toocreate hello package.</span></span>
7. <span data-ttu-id="51b71-257">返回 tooWebSiteSQLDatabase.json，並加入資源 toohello 範本。</span><span class="sxs-lookup"><span data-stu-id="51b71-257">Go back tooWebSiteSQLDatabase.json and add a resource toohello template.</span></span>
   
    ![新增資源](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-resource-2.png)
8. <span data-ttu-id="51b71-259">這次請選取 [Web Deploy for Web Apps] 。</span><span class="sxs-lookup"><span data-stu-id="51b71-259">This time select **Web Deploy for Web Apps**.</span></span> 
   
    ![加入 Web 部署](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/add-web-deploy.png)
9. <span data-ttu-id="51b71-261">重新部署您的資源群組專案 toohello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="51b71-261">Redeploy your resource group project toohello resource group.</span></span> <span data-ttu-id="51b71-262">這次還有一些新的參數。</span><span class="sxs-lookup"><span data-stu-id="51b71-262">This time there are some new parameters.</span></span> <span data-ttu-id="51b71-263">您不需要 tooprovide 值**_artifactsLocation**或**_artifactsLocationSasToken**因為 Visual Studio 會自動產生這些值。</span><span class="sxs-lookup"><span data-stu-id="51b71-263">You do not need tooprovide values for **_artifactsLocation** or **_artifactsLocationSasToken** because Visual Studio automatically generates those values.</span></span> <span data-ttu-id="51b71-264">不過，您必須 tooset hello 資料夾和檔案名稱 toohello 路徑包含 hello 部署封裝 (顯示為**ExampleAppPackageFolder**和**ExampleAppPackageFileName** hello 下列映像中).</span><span class="sxs-lookup"><span data-stu-id="51b71-264">However, you have tooset hello folder and file name toohello path that contains hello deployment package (shown as **ExampleAppPackageFolder** and **ExampleAppPackageFileName** in hello following image).</span></span> <span data-ttu-id="51b71-265">提供您已看到，稍早在 hello 值 hello 參考屬性 (**ExampleApp**和**package.zip**)。</span><span class="sxs-lookup"><span data-stu-id="51b71-265">Provide hello values you saw earlier in hello reference properties (**ExampleApp** and **package.zip**).</span></span>
   
    ![加入 Web 部署](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/set-new-parameters.png)
   
    <span data-ttu-id="51b71-267">Hello**成品儲存體帳戶**，選取 hello 與此資源群組部署的其中一個。</span><span class="sxs-lookup"><span data-stu-id="51b71-267">For hello **Artifact storage account**, select hello one deployed with this resource group.</span></span>
10. <span data-ttu-id="51b71-268">Hello 部署完成之後，請在 hello 入口網站中選取您 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51b71-268">After hello deployment has finished, select your web app in hello portal.</span></span> <span data-ttu-id="51b71-269">選取 hello URL toobrowse toohello 站台。</span><span class="sxs-lookup"><span data-stu-id="51b71-269">Select hello URL toobrowse toohello site.</span></span>
    
     ![瀏覽網站](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/browse-site.png)
11. <span data-ttu-id="51b71-271">請注意您已成功部署 hello 預設 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="51b71-271">Notice that you have successfully deployed hello default ASP.NET app.</span></span>
    
     ![顯示已部署的應用程式](./media/vs-azure-tools-resource-groups-deployment-projects-create-deploy/show-deployed-app.png)

## <a name="next-steps"></a><span data-ttu-id="51b71-273">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51b71-273">Next steps</span></span>
* <span data-ttu-id="51b71-274">toolearn 關於管理您的資源，透過 hello 入口網站，請參閱[使用 hello Azure 入口網站 toomanage 您的 Azure 資源](resource-group-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="51b71-274">toolearn about managing your resources through hello portal, see [Using hello Azure portal toomanage your Azure resources](resource-group-portal.md).</span></span>
* <span data-ttu-id="51b71-275">toolearn 進一步了解範本，請參閱[撰寫 Azure 資源管理員範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="51b71-275">toolearn more about templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

