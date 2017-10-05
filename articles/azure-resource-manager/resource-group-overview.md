---
title: "Azure Resource Manager 概觀 | Microsoft Docs"
description: "描述如何使用 Azure Resource Manager 在 Azure 上進行資源的部署、管理及存取控制。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 76df7de1-1d3b-436e-9b44-e1b3766b3961
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/19/2017
ms.author: tomfitz
ms.openlocfilehash: f539931e0704f904f4b942f185f086a790caf4da
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="azure-resource-manager-overview"></a><span data-ttu-id="3ea13-103">Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="3ea13-103">Azure Resource Manager overview</span></span>
<span data-ttu-id="3ea13-104">應用程式的基礎結構通常由許多元件所組成 – 或許是虛擬機器、儲存體帳戶和虛擬網路，或者 web 應用程式、資料庫、資料庫伺服器和第三方服務。</span><span class="sxs-lookup"><span data-stu-id="3ea13-104">The infrastructure for your application is typically made up of many components – maybe a virtual machine, storage account, and virtual network, or a web app, database, database server, and 3rd party services.</span></span> <span data-ttu-id="3ea13-105">您看不到這些元件作為個別的實體，而是看到它們作為單一實體相關且彼此相依的組件。</span><span class="sxs-lookup"><span data-stu-id="3ea13-105">You do not see these components as separate entities, instead you see them as related and interdependent parts of a single entity.</span></span> <span data-ttu-id="3ea13-106">您會想要將其當成群組來部署、管理和監視。</span><span class="sxs-lookup"><span data-stu-id="3ea13-106">You want to deploy, manage, and monitor them as a group.</span></span> <span data-ttu-id="3ea13-107">Azure Resource Manager 可讓您將方案中的資源作為群組使用。</span><span class="sxs-lookup"><span data-stu-id="3ea13-107">Azure Resource Manager enables you to work with the resources in your solution as a group.</span></span> <span data-ttu-id="3ea13-108">您可以透過單一、協調的作業來部署、更新或刪除方案的所有資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-108">You can deploy, update, or delete all the resources for your solution in a single, coordinated operation.</span></span> <span data-ttu-id="3ea13-109">您會使用部署的範本，且該範本可以用於不同的環境，例如測試、預備和生產環境。</span><span class="sxs-lookup"><span data-stu-id="3ea13-109">You use a template for deployment and that template can work for different environments such as testing, staging, and production.</span></span> <span data-ttu-id="3ea13-110">Resource Manager 會提供安全性、稽核和標記功能，以協助您在部署後管理您的資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-110">Resource Manager provides security, auditing, and tagging features to help you manage your resources after deployment.</span></span> 

## <a name="terminology"></a><span data-ttu-id="3ea13-111">術語</span><span class="sxs-lookup"><span data-stu-id="3ea13-111">Terminology</span></span>
<span data-ttu-id="3ea13-112">如果您不熟悉 Azure Resource Manager，則您可能不熟悉一些詞彙。</span><span class="sxs-lookup"><span data-stu-id="3ea13-112">If you are new to Azure Resource Manager, there are some terms you might not be familiar with.</span></span>

* <span data-ttu-id="3ea13-113">**資源** - 透過 Azure 提供的可管理項目。</span><span class="sxs-lookup"><span data-stu-id="3ea13-113">**resource** - A manageable item that is available through Azure.</span></span> <span data-ttu-id="3ea13-114">部分常見資源有虛擬機器、儲存體帳戶、Web 應用程式、資料庫和虛擬網路，但這只是其中一小部分。</span><span class="sxs-lookup"><span data-stu-id="3ea13-114">Some common resources are a virtual machine, storage account, web app, database, and virtual network, but there are many more.</span></span>
* <span data-ttu-id="3ea13-115">**資源群組** - 保留 Azure 方案相關資源的容器。</span><span class="sxs-lookup"><span data-stu-id="3ea13-115">**resource group** - A container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="3ea13-116">資源群組可以包含方案的所有資源，或只包含您要以群組方式管理的資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-116">The resource group can include all the resources for the solution, or only those resources that you want to manage as a group.</span></span> <span data-ttu-id="3ea13-117">您可決定如何根據對組織最有利的方式，將資源配置到資源群組。</span><span class="sxs-lookup"><span data-stu-id="3ea13-117">You decide how you want to allocate resources to resource groups based on what makes the most sense for your organization.</span></span> <span data-ttu-id="3ea13-118">請參閱 [資源群組](#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-118">See [Resource groups](#resource-groups).</span></span>
* <span data-ttu-id="3ea13-119">**資源提供者** - 提供可透過 Resource Manager 部署及管理之資源的一項服務。</span><span class="sxs-lookup"><span data-stu-id="3ea13-119">**resource provider** - A service that supplies the resources you can deploy and manage through Resource Manager.</span></span> <span data-ttu-id="3ea13-120">每個資源提供者都會提供作業，以便能運用所部署的資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-120">Each resource provider offers operations for working with the resources that are deployed.</span></span> <span data-ttu-id="3ea13-121">部分常見資源提供者有 Microsoft.Compute (提供虛擬機器資源)、Microsoft.Storage (提供儲存體帳戶資源) 和 Microsoft.Web (提供與 Web 應用程式相關的資源)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-121">Some common resource providers are Microsoft.Compute, which supplies the virtual machine resource, Microsoft.Storage, which supplies the storage account resource, and Microsoft.Web, which supplies resources related to web apps.</span></span> <span data-ttu-id="3ea13-122">請參閱 [資源提供者](#resource-providers)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-122">See [Resource providers](#resource-providers).</span></span>
* <span data-ttu-id="3ea13-123">**Resource Manager 範本** - 定義一或多個要部署至資源群組之資源的 JavaScript 物件標記法 (JSON) 檔案。</span><span class="sxs-lookup"><span data-stu-id="3ea13-123">**Resource Manager template** - A JavaScript Object Notation (JSON) file that defines one or more resources to deploy to a resource group.</span></span> <span data-ttu-id="3ea13-124">它也會定義所部署資源之間的相依性。</span><span class="sxs-lookup"><span data-stu-id="3ea13-124">It also defines the dependencies between the deployed resources.</span></span> <span data-ttu-id="3ea13-125">範本可用來以一致性方式重複部署資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-125">The template can be used to deploy the resources consistently and repeatedly.</span></span> <span data-ttu-id="3ea13-126">請參閱 [範本部署](#template-deployment)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-126">See [Template deployment](#template-deployment).</span></span>
* <span data-ttu-id="3ea13-127">**宣告式語法** - 可讓您陳述「以下是我想要建立的項目」而不需要撰寫一連串程式設計命令來加以建立的語法。</span><span class="sxs-lookup"><span data-stu-id="3ea13-127">**declarative syntax** - Syntax that lets you state "Here is what I intend to create" without having to write the sequence of programming commands to create it.</span></span> <span data-ttu-id="3ea13-128">Resource Manager 範本便是宣告式語法的其中一個範例。</span><span class="sxs-lookup"><span data-stu-id="3ea13-128">The Resource Manager template is an example of declarative syntax.</span></span> <span data-ttu-id="3ea13-129">在該檔案中，您可以定義要部署至 Azure 之基礎結構的屬性。</span><span class="sxs-lookup"><span data-stu-id="3ea13-129">In the file, you define the properties for the infrastructure to deploy to Azure.</span></span> 

## <a name="the-benefits-of-using-resource-manager"></a><span data-ttu-id="3ea13-130">使用 Resource Manager 的優點</span><span class="sxs-lookup"><span data-stu-id="3ea13-130">The benefits of using Resource Manager</span></span>
<span data-ttu-id="3ea13-131">Resource Manager 會提供數個優點：</span><span class="sxs-lookup"><span data-stu-id="3ea13-131">Resource Manager provides several benefits:</span></span>

* <span data-ttu-id="3ea13-132">您可以以群組形式部署、管理及監視方案的所有資源，而不是個別處理這些資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-132">You can deploy, manage, and monitor all the resources for your solution as a group, rather than handling these resources individually.</span></span>
* <span data-ttu-id="3ea13-133">您可以在整個方案週期重複部署方案，並確信您的資源會部署在一致的狀態中。</span><span class="sxs-lookup"><span data-stu-id="3ea13-133">You can repeatedly deploy your solution throughout the development lifecycle and have confidence your resources are deployed in a consistent state.</span></span>
* <span data-ttu-id="3ea13-134">您可以透過宣告式範本而非指令碼來管理基礎結構。</span><span class="sxs-lookup"><span data-stu-id="3ea13-134">You can manage your infrastructure through declarative templates rather than scripts.</span></span>
* <span data-ttu-id="3ea13-135">您可以定義之間的相依性，使得以正確的順序部署資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-135">You can define the dependencies between resources so they are deployed in the correct order.</span></span>
* <span data-ttu-id="3ea13-136">因為角色型存取控制 (RBAC) 會原生整合至管理平台，您可以將存取控制套用至資源群組中的所有服務。</span><span class="sxs-lookup"><span data-stu-id="3ea13-136">You can apply access control to all services in your resource group because Role-Based Access Control (RBAC) is natively integrated into the management platform.</span></span>
* <span data-ttu-id="3ea13-137">您可以將標籤套用至資源，以便以邏輯方式組織訂用帳戶中的所有資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-137">You can apply tags to resources to logically organize all the resources in your subscription.</span></span>
* <span data-ttu-id="3ea13-138">您可以檢視共用相同標籤之資源群組的成本，以釐清您的組織的計費方式。</span><span class="sxs-lookup"><span data-stu-id="3ea13-138">You can clarify your organization's billing by viewing costs for a group of resources sharing the same tag.</span></span>  

<span data-ttu-id="3ea13-139">Resource Manager 提供一個部署和管理方案的新方式。</span><span class="sxs-lookup"><span data-stu-id="3ea13-139">Resource Manager provides a new way to deploy and manage your solutions.</span></span> <span data-ttu-id="3ea13-140">如果您使用較舊的部署模型並想要了解這些變更，請參閱[瞭解Resource Manager 部署和傳統部署](resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-140">If you used the earlier deployment model and want to learn about the changes, see [Understanding Resource Manager deployment and classic deployment](resource-manager-deployment-model.md).</span></span>

## <a name="consistent-management-layer"></a><span data-ttu-id="3ea13-141">一致的管理層</span><span class="sxs-lookup"><span data-stu-id="3ea13-141">Consistent management layer</span></span>
<span data-ttu-id="3ea13-142">Resource Manager 會針對您透過 Azure PowerShell、Azure CLI、Azure 入口網站、REST API 和開發工具所執行的工作提供一致的管理層。</span><span class="sxs-lookup"><span data-stu-id="3ea13-142">Resource Manager provides a consistent management layer for the tasks you perform through Azure PowerShell, Azure CLI, Azure portal, REST API, and development tools.</span></span> <span data-ttu-id="3ea13-143">所有工具使用一組共同的作業。</span><span class="sxs-lookup"><span data-stu-id="3ea13-143">All the tools use a common set of operations.</span></span> <span data-ttu-id="3ea13-144">您所使用的是最適合您的工具，而且您可以交互使用這些工具而不會發生混淆。</span><span class="sxs-lookup"><span data-stu-id="3ea13-144">You use the tools that work best for you, and can use them interchangeably without confusion.</span></span> 

<span data-ttu-id="3ea13-145">下圖顯示這些工具如何與相同的 Azure Resource Manager API 互動。</span><span class="sxs-lookup"><span data-stu-id="3ea13-145">The following image shows how all the tools interact with the same Azure Resource Manager API.</span></span> <span data-ttu-id="3ea13-146">API 將要求傳遞給 Resource Manager 服務，由其驗證和授權要求。</span><span class="sxs-lookup"><span data-stu-id="3ea13-146">The API passes requests to the Resource Manager service, which authenticates and authorizes the requests.</span></span> <span data-ttu-id="3ea13-147">然後，Resource Manager 將要求路由傳送到適當的資源提供者。</span><span class="sxs-lookup"><span data-stu-id="3ea13-147">Resource Manager then routes the requests to the appropriate resource providers.</span></span>

![Resource Manager 要求模型](./media/resource-group-overview/consistent-management-layer.png)

## <a name="guidance"></a><span data-ttu-id="3ea13-149">指引</span><span class="sxs-lookup"><span data-stu-id="3ea13-149">Guidance</span></span>
<span data-ttu-id="3ea13-150">下列建議可協助您在使用您的方案時充分利用 Resource Manager。</span><span class="sxs-lookup"><span data-stu-id="3ea13-150">The following suggestions help you take full advantage of Resource Manager when working with your solutions.</span></span>

1. <span data-ttu-id="3ea13-151">透過 Resource Manager 範本中的宣告式語法定義和部署基礎結構，而非透過命令式指令。</span><span class="sxs-lookup"><span data-stu-id="3ea13-151">Define and deploy your infrastructure through the declarative syntax in Resource Manager templates, rather than through imperative commands.</span></span>
2. <span data-ttu-id="3ea13-152">在範本中定義所有的部署和設定步驟。</span><span class="sxs-lookup"><span data-stu-id="3ea13-152">Define all deployment and configuration steps in the template.</span></span> <span data-ttu-id="3ea13-153">您在設定方案時應該沒有手動步驟。</span><span class="sxs-lookup"><span data-stu-id="3ea13-153">You should have no manual steps for setting up your solution.</span></span>
3. <span data-ttu-id="3ea13-154">執行命令式指令來管理您的資源，例如啟動或停止應用程式或機器。</span><span class="sxs-lookup"><span data-stu-id="3ea13-154">Run imperative commands to manage your resources, such as to start or stop an app or machine.</span></span>
4. <span data-ttu-id="3ea13-155">利用與資源群組中相同的生命週期排列資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-155">Arrange resources with the same lifecycle in a resource group.</span></span> <span data-ttu-id="3ea13-156">將標記用於資源的所有其他組織方式。</span><span class="sxs-lookup"><span data-stu-id="3ea13-156">Use tags for all other organizing of resources.</span></span>

<span data-ttu-id="3ea13-157">如需範本的建議，請參閱[建立 Azure Resource Manager 範本的最佳做法](resource-manager-template-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-157">For recommendations about templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

<span data-ttu-id="3ea13-158">如需關於企業如何使用 Resource Manager 有效地管理訂用帳戶的指引，請參閱 [Azure 企業 Scaffold - 規定的訂用帳戶治理](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-158">For guidance on how enterprises can use Resource Manager to effectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

## <a name="resource-groups"></a><span data-ttu-id="3ea13-159">資源群組</span><span class="sxs-lookup"><span data-stu-id="3ea13-159">Resource groups</span></span>
<span data-ttu-id="3ea13-160">定義資源群組時，必須考慮一些重要因素：</span><span class="sxs-lookup"><span data-stu-id="3ea13-160">There are some important factors to consider when defining your resource group:</span></span>

1. <span data-ttu-id="3ea13-161">群組中的所有資源應該共用相同的生命週期。</span><span class="sxs-lookup"><span data-stu-id="3ea13-161">All the resources in your group should share the same lifecycle.</span></span> <span data-ttu-id="3ea13-162">您可一起部署、更新和刪除它們。</span><span class="sxs-lookup"><span data-stu-id="3ea13-162">You deploy, update, and delete them together.</span></span> <span data-ttu-id="3ea13-163">如果類似資料庫伺服器這樣的資源必須存在於不同的部署週期，它應該位於另一個資源群組中。</span><span class="sxs-lookup"><span data-stu-id="3ea13-163">If one resource, such as a database server, needs to exist on a different deployment cycle it should be in another resource group.</span></span>
2. <span data-ttu-id="3ea13-164">每個資源只能存在於一個資源群組中。</span><span class="sxs-lookup"><span data-stu-id="3ea13-164">Each resource can only exist in one resource group.</span></span>
3. <span data-ttu-id="3ea13-165">您可以隨時在資源群組中新增或移除資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-165">You can add or remove a resource to a resource group at any time.</span></span>
4. <span data-ttu-id="3ea13-166">您可以將資源從一個資源群組移動到另一個群組。</span><span class="sxs-lookup"><span data-stu-id="3ea13-166">You can move a resource from one resource group to another group.</span></span> <span data-ttu-id="3ea13-167">如需詳細資訊，請參閱 [將資源移動到新的資源群組或訂用帳戶](resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-167">For more information, see [Move resources to new resource group or subscription](resource-group-move-resources.md).</span></span>
5. <span data-ttu-id="3ea13-168">資源群組可以包含位於不同區域中的資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-168">A resource group can contain resources that reside in different regions.</span></span>
6. <span data-ttu-id="3ea13-169">資源群組可以用來設定系統管理動作的存取控制範圍。</span><span class="sxs-lookup"><span data-stu-id="3ea13-169">A resource group can be used to scope access control for administrative actions.</span></span>
7. <span data-ttu-id="3ea13-170">資源可與其他資源群組中的資源互動。</span><span class="sxs-lookup"><span data-stu-id="3ea13-170">A resource can interact with resources in other resource groups.</span></span> <span data-ttu-id="3ea13-171">此互動常見於兩個資源彼此連結，但未共用相同的生命週期 (例如，連接至某個資料庫的 Web 應用程式) 時。</span><span class="sxs-lookup"><span data-stu-id="3ea13-171">This interaction is common when the two resources are related but do not share the same lifecycle (for example, web apps connecting to a database).</span></span>

<span data-ttu-id="3ea13-172">建立資源群組時，您需要提供該資源群組的位置。</span><span class="sxs-lookup"><span data-stu-id="3ea13-172">When creating a resource group, you need to provide a location for that resource group.</span></span> <span data-ttu-id="3ea13-173">您可能會想：「為什麼資源群組需要位置？</span><span class="sxs-lookup"><span data-stu-id="3ea13-173">You may be wondering, "Why does a resource group need a location?</span></span> <span data-ttu-id="3ea13-174">而且，如果資源可以有不同於資源群組的位置，為什麼資源群組位置這麼重要？」</span><span class="sxs-lookup"><span data-stu-id="3ea13-174">And, if the resources can have different locations than the resource group, why does the resource group location matter at all?"</span></span> <span data-ttu-id="3ea13-175">資源群組會儲存資源相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="3ea13-175">The resource group stores metadata about the resources.</span></span> <span data-ttu-id="3ea13-176">因此，當您指定資源群組的位置時，您便是指定中繼資料的儲存位置。</span><span class="sxs-lookup"><span data-stu-id="3ea13-176">Therefore, when you specify a location for the resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="3ea13-177">基於相容性理由，您可能需要確保您的資料存放在特定區域中。</span><span class="sxs-lookup"><span data-stu-id="3ea13-177">For compliance reasons, you may need to ensure that your data is stored in a particular region.</span></span>

## <a name="resource-providers"></a><span data-ttu-id="3ea13-178">資源提供者</span><span class="sxs-lookup"><span data-stu-id="3ea13-178">Resource providers</span></span>
<span data-ttu-id="3ea13-179">每個資源提供者都會提供一組資源和作業，以便能運用 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="3ea13-179">Each resource provider offers a set of resources and operations for working with an Azure service.</span></span> <span data-ttu-id="3ea13-180">例如，如果想要儲存金鑰和密碼，您會使用 **Microsoft.KeyVault** 資源提供者。</span><span class="sxs-lookup"><span data-stu-id="3ea13-180">For example, if you want to store keys and secrets, you work with the **Microsoft.KeyVault** resource provider.</span></span> <span data-ttu-id="3ea13-181">此資源提供者會提供稱為**保存庫**的資源類型來建立金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="3ea13-181">This resource provider offers a resource type called **vaults** for creating the key vault.</span></span> 

<span data-ttu-id="3ea13-182">資源類型名稱的格式：**{resource-provider}/{resource-type}**。</span><span class="sxs-lookup"><span data-stu-id="3ea13-182">The name of a resource type is in the format: **{resource-provider}/{resource-type}**.</span></span> <span data-ttu-id="3ea13-183">例如，金鑰保存庫類型是 **Microsoft.KeyVault/vaults**。</span><span class="sxs-lookup"><span data-stu-id="3ea13-183">For example, the key vault type is **Microsoft.KeyVault/vaults**.</span></span>

<span data-ttu-id="3ea13-184">在開始部署資源之前，您應該先了解可用的資源提供者。</span><span class="sxs-lookup"><span data-stu-id="3ea13-184">Before getting started with deploying your resources, you should gain an understanding of the available resource providers.</span></span> <span data-ttu-id="3ea13-185">了解資源提供者和資源的名稱可協助您定義想要部署至 Azure 的資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-185">Knowing the names of resource providers and resources helps you define resources you want to deploy to Azure.</span></span> <span data-ttu-id="3ea13-186">此外，您需要知道有效的位置，以及每個資源類型的 API 版本。</span><span class="sxs-lookup"><span data-stu-id="3ea13-186">Also, you need to know the valid locations and API versions for each resource type.</span></span> <span data-ttu-id="3ea13-187">如需詳細資訊，請參閱[資源提供者和類型](resource-manager-supported-services.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-187">For more information, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="template-deployment"></a><span data-ttu-id="3ea13-188">範本部署</span><span class="sxs-lookup"><span data-stu-id="3ea13-188">Template deployment</span></span>
<span data-ttu-id="3ea13-189">利用 Resource Manager，您可以建立可定義 Azure 方案之基礎結構和組態的範本 (以 JSON 格式)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-189">With Resource Manager, you can create a template (in JSON format) that defines the infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="3ea13-190">透過範本，您可以在整個生命週期中重複部署方案，並確信您的資源會以一致的狀態部署。</span><span class="sxs-lookup"><span data-stu-id="3ea13-190">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="3ea13-191">當您從入口網站建立方案，方案會自動包含部署範本。</span><span class="sxs-lookup"><span data-stu-id="3ea13-191">When you create a solution from the portal, the solution automatically includes a deployment template.</span></span> <span data-ttu-id="3ea13-192">您不必從頭建立您的範本，因為您可以從方案的範本開始，並自訂範本以符合您的特定需求。</span><span class="sxs-lookup"><span data-stu-id="3ea13-192">You do not have to create your template from scratch because you can start with the template for your solution and customize it to meet your specific needs.</span></span> <span data-ttu-id="3ea13-193">匯出資源群組的目前狀態，或檢視特定部署所用的範本，即可擷取現有資源群組的範本。</span><span class="sxs-lookup"><span data-stu-id="3ea13-193">You can retrieve a template for an existing resource group by either exporting the current state of the resource group, or viewing the template used for a particular deployment.</span></span> <span data-ttu-id="3ea13-194">檢視[匯出的範本](resource-manager-export-template.md)有助於了解範本語法。</span><span class="sxs-lookup"><span data-stu-id="3ea13-194">Viewing the [exported template](resource-manager-export-template.md) is a helpful way to learn about the template syntax.</span></span>

<span data-ttu-id="3ea13-195">若要了解範本格式和其建構方式，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-195">To learn about the format of the template and how you construct it, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span> <span data-ttu-id="3ea13-196">若要檢視資源類型的 JSON 語法，請參閱[在 Azure Resource Manager 範本中定義資源](/azure/templates/)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-196">To view the JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>

<span data-ttu-id="3ea13-197">Resource Manager 處理範本的方式會和處理其他任何要求一樣 (請參閱[一致的管理層](#consistent-management-layer)影像)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-197">Resource Manager processes the template like any other request (see the image for [Consistent management layer](#consistent-management-layer)).</span></span> <span data-ttu-id="3ea13-198">它會剖析範本，並將其語法轉換成適當的資源提供者所需的 REST API 作業。</span><span class="sxs-lookup"><span data-stu-id="3ea13-198">It parses the template and converts its syntax into REST API operations for the appropriate resource providers.</span></span> <span data-ttu-id="3ea13-199">例如，當 Resource Manager 收到具有下列資源定義的範本︰</span><span class="sxs-lookup"><span data-stu-id="3ea13-199">For example, when Resource Manager receives a template with the following resource definition:</span></span>

```json
"resources": [
  {
    "apiVersion": "2016-01-01",
    "type": "Microsoft.Storage/storageAccounts",
    "name": "mystorageaccount",
    "location": "westus",
    "sku": {
      "name": "Standard_LRS"
    },
    "kind": "Storage",
    "properties": {
    }
  }
]
```

<span data-ttu-id="3ea13-200">它會將定義轉換成下列 REST API 作業，該作業會再傳送給 Microsoft.Storage 資源提供者︰</span><span class="sxs-lookup"><span data-stu-id="3ea13-200">It converts the definition to the following REST API operation, which is sent to the Microsoft.Storage resource provider:</span></span>

```HTTP
PUT
https://management.azure.com/subscriptions/{subscriptionId}/resourceGroups/{resourceGroupName}/providers/Microsoft.Storage/storageAccounts/mystorageaccount?api-version=2016-01-01
REQUEST BODY
{
  "location": "westus",
  "properties": {
  }
  "sku": {
    "name": "Standard_LRS"
  },   
  "kind": "Storage"
}
```

<span data-ttu-id="3ea13-201">範本和資源群組的定義方式全由您決定，方案的管理方式也是如此。</span><span class="sxs-lookup"><span data-stu-id="3ea13-201">How you define templates and resource groups is entirely up to you and how you want to manage your solution.</span></span> <span data-ttu-id="3ea13-202">比方說，您可以透過單一範本在單一資源群組中部署三層式應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ea13-202">For example, you can deploy your three tier application through a single template to a single resource group.</span></span>

![三層式範本](./media/resource-group-overview/3-tier-template.png)

<span data-ttu-id="3ea13-204">但您不需要在單一的範本中定義整個基礎結構。</span><span class="sxs-lookup"><span data-stu-id="3ea13-204">But, you do not have to define your entire infrastructure in a single template.</span></span> <span data-ttu-id="3ea13-205">通常的合理作法是將您的部署需求分成一組有目標及特定目的的範本。</span><span class="sxs-lookup"><span data-stu-id="3ea13-205">Often, it makes sense to divide your deployment requirements into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="3ea13-206">您可以輕鬆地將這些份本重複使用於不同的方案。</span><span class="sxs-lookup"><span data-stu-id="3ea13-206">You can easily reuse these templates for different solutions.</span></span> <span data-ttu-id="3ea13-207">若要部署特定的方案，您會建立連結所有必要範本的主版範本。</span><span class="sxs-lookup"><span data-stu-id="3ea13-207">To deploy a particular solution, you create a master template that links all the required templates.</span></span> <span data-ttu-id="3ea13-208">下圖顯示如何透過包含三個巢狀範本的父範本部署三層式方案。</span><span class="sxs-lookup"><span data-stu-id="3ea13-208">The following image shows how to deploy a three tier solution through a parent template that includes three nested templates.</span></span>

![巢狀階層範本](./media/resource-group-overview/nested-tiers-template.png)

<span data-ttu-id="3ea13-210">如果您想像的階層有不同的生命週期，您可以將這三個階層部署到不同的資源群組。</span><span class="sxs-lookup"><span data-stu-id="3ea13-210">If you envision your tiers having separate lifecycles, you can deploy your three tiers to separate resource groups.</span></span> <span data-ttu-id="3ea13-211">請注意，資源仍可連結至其他資源群組中的資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-211">Notice the resources can still be linked to resources in other resource groups.</span></span>

![階層範本](./media/resource-group-overview/tier-templates.png)

<span data-ttu-id="3ea13-213">如需更多有關設計範本的建議，請參閱[設計 Azure Resource Manager 範本的模式](best-practices-resource-manager-design-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-213">For more suggestions about designing your templates, see [Patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="3ea13-214">如需巢狀範本的相關資訊，請參閱[透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-214">For information about nested templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

<span data-ttu-id="3ea13-215">Azure Resource Manager 會分析相依性，確保以正確的順序建立資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-215">Azure Resource Manager analyzes dependencies to ensure resources are created in the correct order.</span></span> <span data-ttu-id="3ea13-216">如果某個資源依賴另一個資源的值 (例如需要儲存體帳戶以供磁碟使用的虛擬機器)，您必須設定相依性。</span><span class="sxs-lookup"><span data-stu-id="3ea13-216">If one resource relies on a value from another resource (such as a virtual machine needing a storage account for disks), you set a dependency.</span></span> <span data-ttu-id="3ea13-217">如需詳細資訊，請參閱 [定義 Azure Resource Manager 範本中的相依性](resource-group-define-dependencies.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-217">For more information, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span>

<span data-ttu-id="3ea13-218">您也可以使用範本進行基礎結構的更新。</span><span class="sxs-lookup"><span data-stu-id="3ea13-218">You can also use the template for updates to the infrastructure.</span></span> <span data-ttu-id="3ea13-219">例如，您可以將資源新增至您的方案，並將組態規則新增至已部署的資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-219">For example, you can add a resource to your solution and add configuration rules for the resources that are already deployed.</span></span> <span data-ttu-id="3ea13-220">如果此範本指定建立資源，但該資源已經存在，Azure Resource Manager 會執行更新，而不必建立新資產。</span><span class="sxs-lookup"><span data-stu-id="3ea13-220">If the template specifies creating a resource but that resource already exists, Azure Resource Manager performs an update instead of creating a new asset.</span></span> <span data-ttu-id="3ea13-221">Azure Resource Manager 會將現有資產更新為和新資產相同的狀態。</span><span class="sxs-lookup"><span data-stu-id="3ea13-221">Azure Resource Manager updates the existing asset to the same state as it would be as new.</span></span>  

<span data-ttu-id="3ea13-222">當您需要其他作業 (例如安裝不包含在安裝程式的特定軟體) 時，Resource Manager 會提供案例的延伸模組。</span><span class="sxs-lookup"><span data-stu-id="3ea13-222">Resource Manager provides extensions for scenarios when you need additional operations such as installing particular software that is not included in the setup.</span></span> <span data-ttu-id="3ea13-223">如果您已經使用組態管理服務，例如 DSC、Chef 或 Puppet，您可以透過使用擴充功能繼續使用該服務。</span><span class="sxs-lookup"><span data-stu-id="3ea13-223">If you are already using a configuration management service, like DSC, Chef or Puppet, you can continue working with that service by using extensions.</span></span> <span data-ttu-id="3ea13-224">如需虛擬機器擴充功能的相關資訊，請參閱[有關虛擬機器擴充功能和功能](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-224">For information about virtual machine extensions, see [About virtual machine extensions and features](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="3ea13-225">最後，範本會成為應用程式原始碼的一部分。</span><span class="sxs-lookup"><span data-stu-id="3ea13-225">Finally, the template becomes part of the source code for your app.</span></span> <span data-ttu-id="3ea13-226">您可以檢查您的原始程式碼存放庫，並隨著您的應用程式發展加以更新。</span><span class="sxs-lookup"><span data-stu-id="3ea13-226">You can check it in to your source code repository and update it as your app evolves.</span></span> <span data-ttu-id="3ea13-227">您可以透過 Visual Studio 編輯範本。</span><span class="sxs-lookup"><span data-stu-id="3ea13-227">You can edit the template through Visual Studio.</span></span>

<span data-ttu-id="3ea13-228">在定義範本之後，您就可以開始將資源部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="3ea13-228">After defining your template, you are ready to deploy the resources to Azure.</span></span> <span data-ttu-id="3ea13-229">如需用來部署資源的命令，請參閱︰</span><span class="sxs-lookup"><span data-stu-id="3ea13-229">For the commands to deploy the resources, see:</span></span>

* [<span data-ttu-id="3ea13-230">使用 Resource Manager 範本與 Azure PowerShell 來部署資源</span><span class="sxs-lookup"><span data-stu-id="3ea13-230">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>](resource-group-template-deploy.md)
* [<span data-ttu-id="3ea13-231">使用 Resource Manager 範本與 Azure CLI 部署資源</span><span class="sxs-lookup"><span data-stu-id="3ea13-231">Deploy resources with Resource Manager templates and Azure CLI</span></span>](resource-group-template-deploy-cli.md)
* [<span data-ttu-id="3ea13-232">使用 Resource Manager 範本與 Azure 入口網站來部署資源</span><span class="sxs-lookup"><span data-stu-id="3ea13-232">Deploy resources with Resource Manager templates and Azure portal</span></span>](resource-group-template-deploy-portal.md)
* [<span data-ttu-id="3ea13-233">使用 Resource Manager 範本和 Resource Manager REST API 部署資源</span><span class="sxs-lookup"><span data-stu-id="3ea13-233">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>](resource-group-template-deploy-rest.md)

## <a name="tags"></a><span data-ttu-id="3ea13-234">標記</span><span class="sxs-lookup"><span data-stu-id="3ea13-234">Tags</span></span>
<span data-ttu-id="3ea13-235">Resource Manager 提供標記的功能，可讓您根據管理或計費需求將資源分類。</span><span class="sxs-lookup"><span data-stu-id="3ea13-235">Resource Manager provides a tagging feature that enables you to categorize resources according to your requirements for managing or billing.</span></span> <span data-ttu-id="3ea13-236">當您有複雜的資源群組和資源集合，而且必須以對您最有意義的方式視覺化資產時，請使用標籤。</span><span class="sxs-lookup"><span data-stu-id="3ea13-236">Use tags when you have a complex collection of resource groups and resources, and need to visualize those assets in the way that makes the most sense to you.</span></span> <span data-ttu-id="3ea13-237">例如，您可以標記在組織中具有類似角色，或屬於相同部門的資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-237">For example, you could tag resources that serve a similar role in your organization or belong to the same department.</span></span> <span data-ttu-id="3ea13-238">如果不使用標籤，貴組織中的使用者可建立多個資源，如此對於日後的身分識別及管理來說可能很困難。</span><span class="sxs-lookup"><span data-stu-id="3ea13-238">Without tags, users in your organization can create multiple resources that may be difficult to later identify and manage.</span></span> <span data-ttu-id="3ea13-239">例如，您可能想要刪除特定專案的所有資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-239">For example, you may wish to delete all the resources for a particular project.</span></span> <span data-ttu-id="3ea13-240">如果未對此專案標記這些資源，您必須手動尋找它們。</span><span class="sxs-lookup"><span data-stu-id="3ea13-240">If those resources are not tagged for the project, you have to manually find them.</span></span> <span data-ttu-id="3ea13-241">標記是降低訂用帳戶不必要成本的重要方法。</span><span class="sxs-lookup"><span data-stu-id="3ea13-241">Tagging can be an important way for you to reduce unnecessary costs in your subscription.</span></span> 

<span data-ttu-id="3ea13-242">資源不需要位於相同的資源群組即可共用標記。</span><span class="sxs-lookup"><span data-stu-id="3ea13-242">Resources do not need to reside in the same resource group to share a tag.</span></span> <span data-ttu-id="3ea13-243">您可以建立自己的標記分類，以確保組織中的所有使用者都使用常見的標記，而不是使用者意外套用稍有不同的標記 (例如 "dept" 而不是 "department")。</span><span class="sxs-lookup"><span data-stu-id="3ea13-243">You can create your own tag taxonomy to ensure that all users in your organization use common tags rather than users inadvertently applying slightly different tags (such as "dept" instead of "department").</span></span>

<span data-ttu-id="3ea13-244">下列範例顯示套用到虛擬機器的標籤。</span><span class="sxs-lookup"><span data-stu-id="3ea13-244">The following example shows a tag applied to a virtual machine.</span></span>

```json
"resources": [    
  {
    "type": "Microsoft.Compute/virtualMachines",
    "apiVersion": "2015-06-15",
    "name": "SimpleWindowsVM",
    "location": "[resourceGroup().location]",
    "tags": {
        "costCenter": "Finance"
    },
    ...
  }
]
```

<span data-ttu-id="3ea13-245">若要擷取所有具有標籤值的資源，請使用下列 PowerShell Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="3ea13-245">To retrieve all the resources with a tag value, use the following PowerShell cmdlet:</span></span>

```powershell
Find-AzureRmResource -TagName costCenter -TagValue Finance
```

<span data-ttu-id="3ea13-246">或是下列 Azure CLI 2.0 命令：</span><span class="sxs-lookup"><span data-stu-id="3ea13-246">Or, the following Azure CLI 2.0 command:</span></span>

```azurecli
az resource list --tag costCenter=Finance
```

<span data-ttu-id="3ea13-247">您也可以透過 Azure 入口網站檢視已加上標籤的資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-247">You can also view tagged resources through the Azure portal.</span></span>

<span data-ttu-id="3ea13-248">訂用帳戶的[使用報告](../billing/billing-understand-your-bill.md)包含標籤名稱和值，可讓您依標籤細分成本。</span><span class="sxs-lookup"><span data-stu-id="3ea13-248">The [usage report](../billing/billing-understand-your-bill.md) for your subscription includes tag names and values, which enables you to break out costs by tags.</span></span> <span data-ttu-id="3ea13-249">如需標記的詳細資訊，請參閱 [使用標記來組織您的 Azure 資源](resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-249">For more information about tags, see [Using tags to organize your Azure resources](resource-group-using-tags.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="3ea13-250">存取控制</span><span class="sxs-lookup"><span data-stu-id="3ea13-250">Access control</span></span>
<span data-ttu-id="3ea13-251">Resource Manager 可讓您控制哪些人能存取組織的特定動作。</span><span class="sxs-lookup"><span data-stu-id="3ea13-251">Resource Manager enables you to control who has access to specific actions for your organization.</span></span> <span data-ttu-id="3ea13-252">以原生方式將角色型存取控制 (RBAC) 整合至管理平台，並將存取控制套用至資源群組中的所有服務。</span><span class="sxs-lookup"><span data-stu-id="3ea13-252">It natively integrates role-based access control (RBAC) into the management platform and applies that access control to all services in your resource group.</span></span> 

<span data-ttu-id="3ea13-253">在使用角色型存取控制時，請了解兩個主要概念︰</span><span class="sxs-lookup"><span data-stu-id="3ea13-253">There are two main concepts to understand when working with role-based access control:</span></span>

* <span data-ttu-id="3ea13-254">角色定義 - 描述一組權限，並可用於許多指派。</span><span class="sxs-lookup"><span data-stu-id="3ea13-254">Role definitions - describe a set of permissions and can be used in many assignments.</span></span>
* <span data-ttu-id="3ea13-255">角色指派 - 為定義與特定範圍 (訂用帳戶、資源群組或資源) 的身分識別 (使用者或群組) 建立關聯。</span><span class="sxs-lookup"><span data-stu-id="3ea13-255">Role assignments - associate a definition with an identity (user or group) for a particular scope (subscription, resource group, or resource).</span></span> <span data-ttu-id="3ea13-256">較低的範圍會繼承指派。</span><span class="sxs-lookup"><span data-stu-id="3ea13-256">The assignment is inherited by lower scopes.</span></span>

<span data-ttu-id="3ea13-257">您可以將使用者新增到預先定義的平台和資源專用的角色。</span><span class="sxs-lookup"><span data-stu-id="3ea13-257">You can add users to pre-defined platform and resource-specific roles.</span></span> <span data-ttu-id="3ea13-258">例如，您可以利用名為「讀取者」的預先定義角色，以允許使用者檢視資源，但不能加以變更。</span><span class="sxs-lookup"><span data-stu-id="3ea13-258">For example, you can take advantage of the pre-defined role called Reader that permits users to view resources but not change them.</span></span> <span data-ttu-id="3ea13-259">您在組織中新增的使用者需要「讀取者」角色的這類存取，並將該角色套用至訂用帳戶、資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-259">You add users in your organization that need this type of access to the Reader role and apply the role to the subscription, resource group, or resource.</span></span>

<span data-ttu-id="3ea13-260">Azure 提供下列四個平台角色︰</span><span class="sxs-lookup"><span data-stu-id="3ea13-260">Azure provides the following four platform roles:</span></span>

1. <span data-ttu-id="3ea13-261">擁有者 - 可以管理所有項目，包括存取</span><span class="sxs-lookup"><span data-stu-id="3ea13-261">Owner - can manage everything, including access</span></span>
2. <span data-ttu-id="3ea13-262">參與者 - 可以管理存取以外的所有內容</span><span class="sxs-lookup"><span data-stu-id="3ea13-262">Contributor - can manage everything except access</span></span>
3. <span data-ttu-id="3ea13-263">讀取者 - 可以檢視所有項目，但是無法進行變更</span><span class="sxs-lookup"><span data-stu-id="3ea13-263">Reader - can view everything, but can't make changes</span></span>
4. <span data-ttu-id="3ea13-264">使用者存取管理員 - 可管理使用者對 Azure 資源的存取權</span><span class="sxs-lookup"><span data-stu-id="3ea13-264">User Access Administrator - can manage user access to Azure resources</span></span>

<span data-ttu-id="3ea13-265">Azure 也提供數個資源特有的角色。</span><span class="sxs-lookup"><span data-stu-id="3ea13-265">Azure also provides several resource-specific roles.</span></span> <span data-ttu-id="3ea13-266">一些常見的角色有︰</span><span class="sxs-lookup"><span data-stu-id="3ea13-266">Some common ones are:</span></span>

1. <span data-ttu-id="3ea13-267">虛擬機器參與者 - 可以管理虛擬機器，但不能授與對它們的存取權，而且無法管理它們所連接的虛擬網路或儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3ea13-267">Virtual Machine Contributor - can manage virtual machines but not grant access to them, and cannot manage the virtual network or storage account to which they are connected</span></span>
2. <span data-ttu-id="3ea13-268">網路參與者 - 可以管理所有網路資源，但不能授與對它們的存取權</span><span class="sxs-lookup"><span data-stu-id="3ea13-268">Network Contributor - can manage all network resources, but not grant access to them</span></span>
3. <span data-ttu-id="3ea13-269">儲存體帳戶參與者 - 可以管理儲存體帳戶，但不能授與對它們的存取權</span><span class="sxs-lookup"><span data-stu-id="3ea13-269">Storage Account Contributor - Can manage storage accounts, but not grant access to them</span></span>
4. <span data-ttu-id="3ea13-270">SQL Server 參與者 - 可以管理 SQL Server 和資料庫，但是無法管理它們的安全性相關原則</span><span class="sxs-lookup"><span data-stu-id="3ea13-270">SQL Server Contributor - Can manage SQL servers and databases, but not their security-related policies</span></span>
5. <span data-ttu-id="3ea13-271">網站參與者 - 可以管理網站，但是不能管理它們連接的 Web 方案</span><span class="sxs-lookup"><span data-stu-id="3ea13-271">Website Contributor - Can manage websites, but not the web plans to which they are connected</span></span>

<span data-ttu-id="3ea13-272">如需角色和允許動作的完整清單，請參閱 [RBAC：內建角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-272">For the full list of roles and permitted actions, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="3ea13-273">如需角色型存取控制的詳細資訊，請參閱 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-273">For more information about role-based access control, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> 

<span data-ttu-id="3ea13-274">在某些情況下，您會想要執行程式碼或指令碼來存取資源，但不想透過使用者的認證來執行。</span><span class="sxs-lookup"><span data-stu-id="3ea13-274">In some cases, you want to run code or script that accesses resources, but you do not want to run it under a user’s credentials.</span></span> <span data-ttu-id="3ea13-275">相反地，您會想要建立稱為應用程式服務主體的身分識別，並為服務主體指派適當的角色。</span><span class="sxs-lookup"><span data-stu-id="3ea13-275">Instead, you want to create an identity called a service principal for the application and assign the appropriate role for the service principal.</span></span> <span data-ttu-id="3ea13-276">Resource Manager 可讓您建立應用程式認證，並以程式設計方式驗證應用程式。</span><span class="sxs-lookup"><span data-stu-id="3ea13-276">Resource Manager enables you to create credentials for the application and programmatically authenticate the application.</span></span> <span data-ttu-id="3ea13-277">若要了解如何建立服務主體，請參閱下列其中一個主題︰</span><span class="sxs-lookup"><span data-stu-id="3ea13-277">To learn about creating service principals, see one of following topics:</span></span>

* [<span data-ttu-id="3ea13-278">使用 Azure PowerShell 建立用來存取資源的服務主體</span><span class="sxs-lookup"><span data-stu-id="3ea13-278">Use Azure PowerShell to create a service principal to access resources</span></span>](resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="3ea13-279">使用 Azure CLI 建立用來存取資源的服務主體</span><span class="sxs-lookup"><span data-stu-id="3ea13-279">Use Azure CLI to create a service principal to access resources</span></span>](resource-group-authenticate-service-principal-cli.md)
* [<span data-ttu-id="3ea13-280">使用入口網站來建立可存取資源的 Azure Active Directory 應用程式和服務主體</span><span class="sxs-lookup"><span data-stu-id="3ea13-280">Use portal to create Azure Active Directory application and service principal that can access resources</span></span>](resource-group-create-service-principal-portal.md)

<span data-ttu-id="3ea13-281">您也可以明確地鎖定重要的資源，以防止使用者刪除或修改它們。</span><span class="sxs-lookup"><span data-stu-id="3ea13-281">You can also explicitly lock critical resources to prevent users from deleting or modifying them.</span></span> <span data-ttu-id="3ea13-282">如需詳細資訊，請參閱[使用 Azure Resource Manager 來鎖定資源](resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-282">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="activity-logs"></a><span data-ttu-id="3ea13-283">活動記錄</span><span class="sxs-lookup"><span data-stu-id="3ea13-283">Activity logs</span></span>
<span data-ttu-id="3ea13-284">Resource Manager 會記錄所有建立、修改或刪除資源的作業。</span><span class="sxs-lookup"><span data-stu-id="3ea13-284">Resource Manager logs all operations that create, modify, or delete a resource.</span></span> <span data-ttu-id="3ea13-285">您可以使用活動記錄在進行疑難排解時發現錯誤，或是監視貴組織使用者修改資源的方式。</span><span class="sxs-lookup"><span data-stu-id="3ea13-285">You can use the activity logs to find an error when troubleshooting or to monitor how a user in your organization modified a resource.</span></span> <span data-ttu-id="3ea13-286">若要查看記錄，請在資源群組的 [設定] 刀鋒視窗中選取 [活動記錄]。</span><span class="sxs-lookup"><span data-stu-id="3ea13-286">To see the logs, select **Activity logs** in the **Settings** blade for a resource group.</span></span> <span data-ttu-id="3ea13-287">您可以透過許多不同的值篩選記錄，包括哪位使用者起始了作業。</span><span class="sxs-lookup"><span data-stu-id="3ea13-287">You can filter the logs by many different values including which user initiated the operation.</span></span> <span data-ttu-id="3ea13-288">如需使用活動記錄的相關資訊，請參閱[檢視活動記錄以管理 Azure 資源](resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-288">For information about working with the activity logs, see [View activity logs to manage Azure resources](resource-group-audit.md).</span></span>

## <a name="customized-policies"></a><span data-ttu-id="3ea13-289">自訂的原則</span><span class="sxs-lookup"><span data-stu-id="3ea13-289">Customized policies</span></span>
<span data-ttu-id="3ea13-290">Resource Manager 可讓您建立自訂的原則，以便管理您的資源。</span><span class="sxs-lookup"><span data-stu-id="3ea13-290">Resource Manager enables you to create customized policies for managing your resources.</span></span> <span data-ttu-id="3ea13-291">您所建立的原則類型可以包含各種案例。</span><span class="sxs-lookup"><span data-stu-id="3ea13-291">The types of policies you create can include diverse scenarios.</span></span> <span data-ttu-id="3ea13-292">您可以強制執行資源的的命名慣例、限制可以部署的資源類型和執行個體，或限制可以裝載某個資源類型的區域。</span><span class="sxs-lookup"><span data-stu-id="3ea13-292">You can enforce a naming convention on resources, limit which types and instances of resources can be deployed, or limit which regions can host a type of resource.</span></span> <span data-ttu-id="3ea13-293">您可以要求資源的標籤值，以便依照部門組織計費方式。</span><span class="sxs-lookup"><span data-stu-id="3ea13-293">You can require a tag value on resources to organize billing by departments.</span></span> <span data-ttu-id="3ea13-294">您可建立原則來協助降低成本，並維護訂用帳戶中的一致性。</span><span class="sxs-lookup"><span data-stu-id="3ea13-294">You create policies to help reduce costs and maintain consistency in your subscription.</span></span> 

<span data-ttu-id="3ea13-295">您需要使用 JSON 來定義原則，然後將這些原則套用到您的訂用帳戶或資源群組內。</span><span class="sxs-lookup"><span data-stu-id="3ea13-295">You define policies with JSON and then apply those policies either across your subscription or within a resource group.</span></span> <span data-ttu-id="3ea13-296">原則會套用到資源類型，因此不同於角色型存取控制。</span><span class="sxs-lookup"><span data-stu-id="3ea13-296">Policies are different than role-based access control because they are applied to resource types.</span></span>

<span data-ttu-id="3ea13-297">下列範例顯示了某個原則，其藉由指定所有資源都包含 costCenter 標籤，來確保標籤的一致性。</span><span class="sxs-lookup"><span data-stu-id="3ea13-297">The following example shows a policy that ensures tag consistency by specifying that all resources include a costCenter tag.</span></span>

```json
{
  "if": {
    "not" : {
      "field" : "tags",
      "containsKey" : "costCenter"
    }
  },
  "then" : {
    "effect" : "deny"
  }
}
```

<span data-ttu-id="3ea13-298">您還可以建立其他類型的原則。</span><span class="sxs-lookup"><span data-stu-id="3ea13-298">There are many more types of policies you can create.</span></span> <span data-ttu-id="3ea13-299">如需詳細資訊，請參閱 [使用原則來管理資源和控制存取](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-299">For more information, see [Use Policy to manage resources and control access](resource-manager-policy.md).</span></span>

## <a name="sdks"></a><span data-ttu-id="3ea13-300">SDK</span><span class="sxs-lookup"><span data-stu-id="3ea13-300">SDKs</span></span>
<span data-ttu-id="3ea13-301">Azure SDK 可供多個語言和平台使用。</span><span class="sxs-lookup"><span data-stu-id="3ea13-301">Azure SDKs are available for multiple languages and platforms.</span></span> <span data-ttu-id="3ea13-302">這些語言實作都是透過其生態系統的套件管理員和 GitHub 提供。</span><span class="sxs-lookup"><span data-stu-id="3ea13-302">Each of these language implementations is available through its ecosystem package manager and GitHub.</span></span>

<span data-ttu-id="3ea13-303">以下是我們的開放原始碼 SDK 存放庫。</span><span class="sxs-lookup"><span data-stu-id="3ea13-303">Here are our Open Source SDK repositories.</span></span> <span data-ttu-id="3ea13-304">歡迎提供意見反應、問題並提取要求。</span><span class="sxs-lookup"><span data-stu-id="3ea13-304">We welcome feedback, issues, and pull requests.</span></span>

* [<span data-ttu-id="3ea13-305">Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="3ea13-305">Azure SDK for .NET</span></span>](https://github.com/Azure/azure-sdk-for-net)
* [<span data-ttu-id="3ea13-306">適用於 Java 的 Azure 管理程式庫</span><span class="sxs-lookup"><span data-stu-id="3ea13-306">Azure Management Libraries for Java</span></span>](https://github.com/Azure/azure-sdk-for-java)
* [<span data-ttu-id="3ea13-307">Azure SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="3ea13-307">Azure SDK for Node.js</span></span>](https://github.com/Azure/azure-sdk-for-node)
* [<span data-ttu-id="3ea13-308">Azure SDK for PHP</span><span class="sxs-lookup"><span data-stu-id="3ea13-308">Azure SDK for PHP</span></span>](https://github.com/Azure/azure-sdk-for-php)
* [<span data-ttu-id="3ea13-309">Azure SDK for Python</span><span class="sxs-lookup"><span data-stu-id="3ea13-309">Azure SDK for Python</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="3ea13-310">Azure SDK for Ruby</span><span class="sxs-lookup"><span data-stu-id="3ea13-310">Azure SDK for Ruby</span></span>](https://github.com/Azure/azure-sdk-for-ruby)

<span data-ttu-id="3ea13-311">如需使用這些語言搭配您的資源的相關資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="3ea13-311">For information about using these languages with your resources, see:</span></span>

* [<span data-ttu-id="3ea13-312">適用於 .NET 開發人員的 Azure</span><span class="sxs-lookup"><span data-stu-id="3ea13-312">Azure for .NET developers</span></span>](/dotnet/azure/?view=azure-dotnet)
* [<span data-ttu-id="3ea13-313">適用於 Java 開發人員的 Azure</span><span class="sxs-lookup"><span data-stu-id="3ea13-313">Azure for Java developers</span></span>](/java/azure/)
* [<span data-ttu-id="3ea13-314">適用於 Node.js 開發人員的 Azure</span><span class="sxs-lookup"><span data-stu-id="3ea13-314">Azure for Node.js developers</span></span>](/nodejs/azure/)
* [<span data-ttu-id="3ea13-315">適用於 Python 開發人員的 Azure</span><span class="sxs-lookup"><span data-stu-id="3ea13-315">Azure for Python developers</span></span>](/python/azure/)

> [!NOTE]
> <span data-ttu-id="3ea13-316">如果 SDK 未提供必要的功能，您也可以直接呼叫 [Azure REST API](https://docs.microsoft.com/rest/api/resources/) 。</span><span class="sxs-lookup"><span data-stu-id="3ea13-316">If the SDK doesn't provide the required functionality, you can also call to the [Azure REST API](https://docs.microsoft.com/rest/api/resources/) directly.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="3ea13-317">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ea13-317">Next steps</span></span>
* <span data-ttu-id="3ea13-318">若要深入了解如何使用匯出的範本， [從現有資源匯出 Azure Resource Manager 範本](resource-manager-export-template.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-318">For a simple introduction to working with templates, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="3ea13-319">如需更詳細的建立範本逐步解說，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-319">For a more thorough walkthrough of creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
* <span data-ttu-id="3ea13-320">若要了解您可以在範本中使用的函式，請參閱 [範本函式](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="3ea13-320">To understand the functions you can use in a template, see [Template functions](resource-group-template-functions.md)</span></span>
* <span data-ttu-id="3ea13-321">如需有關如何搭配使用 Visual Studio 與 Resource Manager 的相關資訊，請參閱 [透過 Visual Studio 建立和部署 Azure 資源群組](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea13-321">For information about using Visual Studio with Resource Manager, see [Creating and deploying Azure resource groups through Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

<span data-ttu-id="3ea13-322">以下是此概觀的示範影片。</span><span class="sxs-lookup"><span data-stu-id="3ea13-322">Here's a video demonstration of this overview:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure-Documentation-Shorts/Azure-Resource-Manager-Overview/player]


[powershellref]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/azurerm.resources
