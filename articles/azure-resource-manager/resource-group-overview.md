---
title: "aaaAzure 資源管理員概觀 |Microsoft 文件"
description: "描述如何 toouse Azure 資源管理員部署、 管理和 Azure 上的存取控制的資源。"
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
ms.openlocfilehash: a44fccd96d722c006224145d71cc44292255debf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-overview"></a><span data-ttu-id="90e32-103">Azure Resource Manager 概觀</span><span class="sxs-lookup"><span data-stu-id="90e32-103">Azure Resource Manager overview</span></span>
<span data-ttu-id="90e32-104">許多元件 – 也許虛擬機器、 儲存體帳戶和虛擬網路或 web 應用程式、 資料庫、 資料庫伺服器和第 3 個合作對象服務 hello 基礎結構，您的應用程式通常由所組成。</span><span class="sxs-lookup"><span data-stu-id="90e32-104">hello infrastructure for your application is typically made up of many components – maybe a virtual machine, storage account, and virtual network, or a web app, database, database server, and 3rd party services.</span></span> <span data-ttu-id="90e32-105">您看不到這些元件作為個別的實體，而是看到它們作為單一實體相關且彼此相依的組件。</span><span class="sxs-lookup"><span data-stu-id="90e32-105">You do not see these components as separate entities, instead you see them as related and interdependent parts of a single entity.</span></span> <span data-ttu-id="90e32-106">您想 toodeploy、 管理和監視這些群組。</span><span class="sxs-lookup"><span data-stu-id="90e32-106">You want toodeploy, manage, and monitor them as a group.</span></span> <span data-ttu-id="90e32-107">Azure 資源管理員可讓您與您的方案中的 hello 資源 toowork 為群組。</span><span class="sxs-lookup"><span data-stu-id="90e32-107">Azure Resource Manager enables you toowork with hello resources in your solution as a group.</span></span> <span data-ttu-id="90e32-108">您可以部署、 更新或刪除您的解決方案是單一的協調作業，在 hello 的所有資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-108">You can deploy, update, or delete all hello resources for your solution in a single, coordinated operation.</span></span> <span data-ttu-id="90e32-109">您會使用部署的範本，且該範本可以用於不同的環境，例如測試、預備和生產環境。</span><span class="sxs-lookup"><span data-stu-id="90e32-109">You use a template for deployment and that template can work for different environments such as testing, staging, and production.</span></span> <span data-ttu-id="90e32-110">資源管理員提供安全性、 稽核和標記功能 toohelp 部署後管理您的資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-110">Resource Manager provides security, auditing, and tagging features toohelp you manage your resources after deployment.</span></span> 

## <a name="terminology"></a><span data-ttu-id="90e32-111">術語</span><span class="sxs-lookup"><span data-stu-id="90e32-111">Terminology</span></span>
<span data-ttu-id="90e32-112">如果您是新 tooAzure 資源管理員，有一些您可能不熟悉的一些辭彙。</span><span class="sxs-lookup"><span data-stu-id="90e32-112">If you are new tooAzure Resource Manager, there are some terms you might not be familiar with.</span></span>

* <span data-ttu-id="90e32-113">**資源** - 透過 Azure 提供的可管理項目。</span><span class="sxs-lookup"><span data-stu-id="90e32-113">**resource** - A manageable item that is available through Azure.</span></span> <span data-ttu-id="90e32-114">部分常見資源有虛擬機器、儲存體帳戶、Web 應用程式、資料庫和虛擬網路，但這只是其中一小部分。</span><span class="sxs-lookup"><span data-stu-id="90e32-114">Some common resources are a virtual machine, storage account, web app, database, and virtual network, but there are many more.</span></span>
* <span data-ttu-id="90e32-115">**資源群組** - 保留 Azure 方案相關資源的容器。</span><span class="sxs-lookup"><span data-stu-id="90e32-115">**resource group** - A container that holds related resources for an Azure solution.</span></span> <span data-ttu-id="90e32-116">hello 資源群組可包含 hello 方案的所有 hello 資源或您想 toomanage 為群組的資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-116">hello resource group can include all hello resources for hello solution, or only those resources that you want toomanage as a group.</span></span> <span data-ttu-id="90e32-117">您決定要如何 tooallocate 資源 tooresource 根據錯誤群組構成 hello 最適合您的組織。</span><span class="sxs-lookup"><span data-stu-id="90e32-117">You decide how you want tooallocate resources tooresource groups based on what makes hello most sense for your organization.</span></span> <span data-ttu-id="90e32-118">請參閱 [資源群組](#resource-groups)。</span><span class="sxs-lookup"><span data-stu-id="90e32-118">See [Resource groups](#resource-groups).</span></span>
* <span data-ttu-id="90e32-119">**資源提供者**-提供 hello 資源的服務您可以部署及管理透過資源管理員。</span><span class="sxs-lookup"><span data-stu-id="90e32-119">**resource provider** - A service that supplies hello resources you can deploy and manage through Resource Manager.</span></span> <span data-ttu-id="90e32-120">每個資源提供者會提供以使用已部署的 hello 資源的作業。</span><span class="sxs-lookup"><span data-stu-id="90e32-120">Each resource provider offers operations for working with hello resources that are deployed.</span></span> <span data-ttu-id="90e32-121">某些共用的資源提供者是 Microsoft.Compute，提供 hello 虛擬機器資源、 Microsoft.Storage，提供 hello 儲存體帳戶資源，以及 Microsoft.Web，提供資源相關的 tooweb 應用程式。</span><span class="sxs-lookup"><span data-stu-id="90e32-121">Some common resource providers are Microsoft.Compute, which supplies hello virtual machine resource, Microsoft.Storage, which supplies hello storage account resource, and Microsoft.Web, which supplies resources related tooweb apps.</span></span> <span data-ttu-id="90e32-122">請參閱 [資源提供者](#resource-providers)。</span><span class="sxs-lookup"><span data-stu-id="90e32-122">See [Resource providers](#resource-providers).</span></span>
* <span data-ttu-id="90e32-123">**資源管理員範本**-A JavaScript Object Notation (JSON) 檔案，定義一個或多個資源 toodeploy tooa 資源群組。</span><span class="sxs-lookup"><span data-stu-id="90e32-123">**Resource Manager template** - A JavaScript Object Notation (JSON) file that defines one or more resources toodeploy tooa resource group.</span></span> <span data-ttu-id="90e32-124">它也會定義 hello hello 部署資源之間的相依性。</span><span class="sxs-lookup"><span data-stu-id="90e32-124">It also defines hello dependencies between hello deployed resources.</span></span> <span data-ttu-id="90e32-125">一致的方式和重複 hello 範本可以使用的 toodeploy hello 資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-125">hello template can be used toodeploy hello resources consistently and repeatedly.</span></span> <span data-ttu-id="90e32-126">請參閱 [範本部署](#template-deployment)。</span><span class="sxs-lookup"><span data-stu-id="90e32-126">See [Template deployment](#template-deployment).</span></span>
* <span data-ttu-id="90e32-127">**宣告式語法**-可讓您的語法狀態 」 以下是 我想要 toocreate"而不需要的程式設計命令 toocreate toowrite hello 順序它。</span><span class="sxs-lookup"><span data-stu-id="90e32-127">**declarative syntax** - Syntax that lets you state "Here is what I intend toocreate" without having toowrite hello sequence of programming commands toocreate it.</span></span> <span data-ttu-id="90e32-128">hello Resource Manager 範本是宣告式語法的範例。</span><span class="sxs-lookup"><span data-stu-id="90e32-128">hello Resource Manager template is an example of declarative syntax.</span></span> <span data-ttu-id="90e32-129">在 hello 檔案中，您可以定義 hello 基礎結構 toodeploy tooAzure hello 屬性。</span><span class="sxs-lookup"><span data-stu-id="90e32-129">In hello file, you define hello properties for hello infrastructure toodeploy tooAzure.</span></span> 

## <a name="hello-benefits-of-using-resource-manager"></a><span data-ttu-id="90e32-130">使用資源管理員的 hello 優點</span><span class="sxs-lookup"><span data-stu-id="90e32-130">hello benefits of using Resource Manager</span></span>
<span data-ttu-id="90e32-131">Resource Manager 會提供數個優點：</span><span class="sxs-lookup"><span data-stu-id="90e32-131">Resource Manager provides several benefits:</span></span>

* <span data-ttu-id="90e32-132">您可以部署、 管理及監視您的方案 hello 的所有資源群組，而非個別處理這些資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-132">You can deploy, manage, and monitor all hello resources for your solution as a group, rather than handling these resources individually.</span></span>
* <span data-ttu-id="90e32-133">重複，您可以部署整個 hello 開發生命週期方案，並確保一致的狀態以部署您的資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-133">You can repeatedly deploy your solution throughout hello development lifecycle and have confidence your resources are deployed in a consistent state.</span></span>
* <span data-ttu-id="90e32-134">您可以透過宣告式範本而非指令碼來管理基礎結構。</span><span class="sxs-lookup"><span data-stu-id="90e32-134">You can manage your infrastructure through declarative templates rather than scripts.</span></span>
* <span data-ttu-id="90e32-135">您可以定義 hello 資源，所以它們部署在 hello 正確的順序之間的相依性。</span><span class="sxs-lookup"><span data-stu-id="90e32-135">You can define hello dependencies between resources so they are deployed in hello correct order.</span></span>
* <span data-ttu-id="90e32-136">因為角色型存取控制 (RBAC) 原生整合至 hello 管理平台，您可以套用存取控制 tooall 服務資源群組中。</span><span class="sxs-lookup"><span data-stu-id="90e32-136">You can apply access control tooall services in your resource group because Role-Based Access Control (RBAC) is natively integrated into hello management platform.</span></span>
* <span data-ttu-id="90e32-137">您可以將標籤套用 tooresources toologically 組織您的訂用帳戶中的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-137">You can apply tags tooresources toologically organize all hello resources in your subscription.</span></span>
* <span data-ttu-id="90e32-138">您可以藉由檢視群組的資源成本釐清您組織的計費共用 hello 相同的標記。</span><span class="sxs-lookup"><span data-stu-id="90e32-138">You can clarify your organization's billing by viewing costs for a group of resources sharing hello same tag.</span></span>  

<span data-ttu-id="90e32-139">資源管理員提供新的方式 toodeploy 和管理您的方案。</span><span class="sxs-lookup"><span data-stu-id="90e32-139">Resource Manager provides a new way toodeploy and manage your solutions.</span></span> <span data-ttu-id="90e32-140">如果您使用 hello 舊版部署模型而且想 toolearn 有關 hello 變更，請參閱[了解資源管理員部署和傳統部署](resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-140">If you used hello earlier deployment model and want toolearn about hello changes, see [Understanding Resource Manager deployment and classic deployment](resource-manager-deployment-model.md).</span></span>

## <a name="consistent-management-layer"></a><span data-ttu-id="90e32-141">一致的管理層</span><span class="sxs-lookup"><span data-stu-id="90e32-141">Consistent management layer</span></span>
<span data-ttu-id="90e32-142">資源管理員的 hello 執行的工作，透過 Azure PowerShell、 Azure CLI、 Azure 入口網站、 REST API 和開發工具提供一致的管理層。</span><span class="sxs-lookup"><span data-stu-id="90e32-142">Resource Manager provides a consistent management layer for hello tasks you perform through Azure PowerShell, Azure CLI, Azure portal, REST API, and development tools.</span></span> <span data-ttu-id="90e32-143">所有的 hello 工具會使用一組常見的作業。</span><span class="sxs-lookup"><span data-stu-id="90e32-143">All hello tools use a common set of operations.</span></span> <span data-ttu-id="90e32-144">您使用最適合您，且可以交換使用而不會混淆的 hello 工具。</span><span class="sxs-lookup"><span data-stu-id="90e32-144">You use hello tools that work best for you, and can use them interchangeably without confusion.</span></span> 

<span data-ttu-id="90e32-145">hello 下列影像顯示如何與互動的所有 hello 工具 hello 相同的 Azure 資源管理員 API。</span><span class="sxs-lookup"><span data-stu-id="90e32-145">hello following image shows how all hello tools interact with hello same Azure Resource Manager API.</span></span> <span data-ttu-id="90e32-146">hello API 將要求傳遞 toohello 資源管理員服務，以便驗證與授權 hello 要求。</span><span class="sxs-lookup"><span data-stu-id="90e32-146">hello API passes requests toohello Resource Manager service, which authenticates and authorizes hello requests.</span></span> <span data-ttu-id="90e32-147">資源管理員然後路由傳送嗨要求 toohello 適當的資源提供者。</span><span class="sxs-lookup"><span data-stu-id="90e32-147">Resource Manager then routes hello requests toohello appropriate resource providers.</span></span>

![Resource Manager 要求模型](./media/resource-group-overview/consistent-management-layer.png)

## <a name="guidance"></a><span data-ttu-id="90e32-149">指引</span><span class="sxs-lookup"><span data-stu-id="90e32-149">Guidance</span></span>
<span data-ttu-id="90e32-150">hello 下列建議可協助您使用您的方案時，要充分利用的資源管理員。</span><span class="sxs-lookup"><span data-stu-id="90e32-150">hello following suggestions help you take full advantage of Resource Manager when working with your solutions.</span></span>

1. <span data-ttu-id="90e32-151">定義和部署基礎結構透過 hello 資源管理員範本中的宣告式語法，而非透過命令式命令。</span><span class="sxs-lookup"><span data-stu-id="90e32-151">Define and deploy your infrastructure through hello declarative syntax in Resource Manager templates, rather than through imperative commands.</span></span>
2. <span data-ttu-id="90e32-152">Hello 範本中定義所有的部署和設定步驟。</span><span class="sxs-lookup"><span data-stu-id="90e32-152">Define all deployment and configuration steps in hello template.</span></span> <span data-ttu-id="90e32-153">您在設定方案時應該沒有手動步驟。</span><span class="sxs-lookup"><span data-stu-id="90e32-153">You should have no manual steps for setting up your solution.</span></span>
3. <span data-ttu-id="90e32-154">執行您的資源，例如 toostart 命令式命令 toomanage 或停止的應用程式或電腦。</span><span class="sxs-lookup"><span data-stu-id="90e32-154">Run imperative commands toomanage your resources, such as toostart or stop an app or machine.</span></span>
4. <span data-ttu-id="90e32-155">以 hello 排列資源的資源群組中的相同生命週期。</span><span class="sxs-lookup"><span data-stu-id="90e32-155">Arrange resources with hello same lifecycle in a resource group.</span></span> <span data-ttu-id="90e32-156">將標記用於資源的所有其他組織方式。</span><span class="sxs-lookup"><span data-stu-id="90e32-156">Use tags for all other organizing of resources.</span></span>

<span data-ttu-id="90e32-157">如需範本的建議，請參閱[建立 Azure Resource Manager 範本的最佳做法](resource-manager-template-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-157">For recommendations about templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>

<span data-ttu-id="90e32-158">如需指引企業可以如何使用資源管理員 tooeffectively 管理訂用帳戶，請參閱[Azure 企業版 scaffold-精準的訂閱控管](resource-manager-subscription-governance.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-158">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

## <a name="resource-groups"></a><span data-ttu-id="90e32-159">資源群組</span><span class="sxs-lookup"><span data-stu-id="90e32-159">Resource groups</span></span>
<span data-ttu-id="90e32-160">定義您的資源群組時，有一些重要因素 tooconsider:</span><span class="sxs-lookup"><span data-stu-id="90e32-160">There are some important factors tooconsider when defining your resource group:</span></span>

1. <span data-ttu-id="90e32-161">群組中的所有 hello 資源都應該都共用相同的生命週期的 hello。</span><span class="sxs-lookup"><span data-stu-id="90e32-161">All hello resources in your group should share hello same lifecycle.</span></span> <span data-ttu-id="90e32-162">您可一起部署、更新和刪除它們。</span><span class="sxs-lookup"><span data-stu-id="90e32-162">You deploy, update, and delete them together.</span></span> <span data-ttu-id="90e32-163">如果一個資源，例如資料庫伺服器，需要在不同的部署週期 tooexist 應該可以在另一個資源群組中。</span><span class="sxs-lookup"><span data-stu-id="90e32-163">If one resource, such as a database server, needs tooexist on a different deployment cycle it should be in another resource group.</span></span>
2. <span data-ttu-id="90e32-164">每個資源只能存在於一個資源群組中。</span><span class="sxs-lookup"><span data-stu-id="90e32-164">Each resource can only exist in one resource group.</span></span>
3. <span data-ttu-id="90e32-165">您可以新增或移除資源 tooa 資源群組在任何時間。</span><span class="sxs-lookup"><span data-stu-id="90e32-165">You can add or remove a resource tooa resource group at any time.</span></span>
4. <span data-ttu-id="90e32-166">您可以將資源從一個資源群組 tooanother 群組。</span><span class="sxs-lookup"><span data-stu-id="90e32-166">You can move a resource from one resource group tooanother group.</span></span> <span data-ttu-id="90e32-167">如需詳細資訊，請參閱[移動資源 toonew 資源群組或訂用帳戶](resource-group-move-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-167">For more information, see [Move resources toonew resource group or subscription](resource-group-move-resources.md).</span></span>
5. <span data-ttu-id="90e32-168">資源群組可以包含位於不同區域中的資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-168">A resource group can contain resources that reside in different regions.</span></span>
6. <span data-ttu-id="90e32-169">資源群組可以是用於系統管理動作 tooscope 存取控制。</span><span class="sxs-lookup"><span data-stu-id="90e32-169">A resource group can be used tooscope access control for administrative actions.</span></span>
7. <span data-ttu-id="90e32-170">資源可與其他資源群組中的資源互動。</span><span class="sxs-lookup"><span data-stu-id="90e32-170">A resource can interact with resources in other resource groups.</span></span> <span data-ttu-id="90e32-171">Hello 兩個資源相關，但不是會共用時，這個互動是很常見 hello 相同生命週期 （例如，web 應用程式連接 tooa 資料庫）。</span><span class="sxs-lookup"><span data-stu-id="90e32-171">This interaction is common when hello two resources are related but do not share hello same lifecycle (for example, web apps connecting tooa database).</span></span>

<span data-ttu-id="90e32-172">建立資源群組時，您會需要 tooprovide 位置，該資源群組。</span><span class="sxs-lookup"><span data-stu-id="90e32-172">When creating a resource group, you need tooprovide a location for that resource group.</span></span> <span data-ttu-id="90e32-173">您可能會想：「為什麼資源群組需要位置？</span><span class="sxs-lookup"><span data-stu-id="90e32-173">You may be wondering, "Why does a resource group need a location?</span></span> <span data-ttu-id="90e32-174">如果 hello 資源可以有不同的位置比 hello 資源群組，為什麼沒有 hello 資源群組位置重要完全？ 」</span><span class="sxs-lookup"><span data-stu-id="90e32-174">And, if hello resources can have different locations than hello resource group, why does hello resource group location matter at all?"</span></span> <span data-ttu-id="90e32-175">hello 資源群組，儲存 hello 資源的相關中繼資料。</span><span class="sxs-lookup"><span data-stu-id="90e32-175">hello resource group stores metadata about hello resources.</span></span> <span data-ttu-id="90e32-176">因此，當您指定 hello 資源群組的位置，就指定儲存的中繼資料。</span><span class="sxs-lookup"><span data-stu-id="90e32-176">Therefore, when you specify a location for hello resource group, you are specifying where that metadata is stored.</span></span> <span data-ttu-id="90e32-177">基於相容性因素，您可能需要 tooensure 資料儲存在特定區域中。</span><span class="sxs-lookup"><span data-stu-id="90e32-177">For compliance reasons, you may need tooensure that your data is stored in a particular region.</span></span>

## <a name="resource-providers"></a><span data-ttu-id="90e32-178">資源提供者</span><span class="sxs-lookup"><span data-stu-id="90e32-178">Resource providers</span></span>
<span data-ttu-id="90e32-179">每個資源提供者都會提供一組資源和作業，以便能運用 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="90e32-179">Each resource provider offers a set of resources and operations for working with an Azure service.</span></span> <span data-ttu-id="90e32-180">例如，如果您想 toostore 金鑰和密碼，則處理 hello **Microsoft.KeyVault**資源提供者。</span><span class="sxs-lookup"><span data-stu-id="90e32-180">For example, if you want toostore keys and secrets, you work with hello **Microsoft.KeyVault** resource provider.</span></span> <span data-ttu-id="90e32-181">這個資源提供者提供的資源類型，稱為**保存庫**建立 hello 金鑰保存庫。</span><span class="sxs-lookup"><span data-stu-id="90e32-181">This resource provider offers a resource type called **vaults** for creating hello key vault.</span></span> 

<span data-ttu-id="90e32-182">hello 資源類型名稱的格式 hello: **{資源提供者} / {資源類型}**。</span><span class="sxs-lookup"><span data-stu-id="90e32-182">hello name of a resource type is in hello format: **{resource-provider}/{resource-type}**.</span></span> <span data-ttu-id="90e32-183">例如，hello 金鑰保存庫類型是**Microsoft.KeyVault/vaults**。</span><span class="sxs-lookup"><span data-stu-id="90e32-183">For example, hello key vault type is **Microsoft.KeyVault/vaults**.</span></span>

<span data-ttu-id="90e32-184">開始與部署您的資源，使用之前，您應該了解 hello 可用資源提供者。</span><span class="sxs-lookup"><span data-stu-id="90e32-184">Before getting started with deploying your resources, you should gain an understanding of hello available resource providers.</span></span> <span data-ttu-id="90e32-185">您想 toodeploy tooAzure 知道 hello 名稱的資源提供者和資源可協助您定義的資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-185">Knowing hello names of resource providers and resources helps you define resources you want toodeploy tooAzure.</span></span> <span data-ttu-id="90e32-186">此外，您可以針對每個資源類型需要 tooknow hello 有效的位置和 API 版本。</span><span class="sxs-lookup"><span data-stu-id="90e32-186">Also, you need tooknow hello valid locations and API versions for each resource type.</span></span> <span data-ttu-id="90e32-187">如需詳細資訊，請參閱[資源提供者和類型](resource-manager-supported-services.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-187">For more information, see [Resource providers and types](resource-manager-supported-services.md).</span></span>

## <a name="template-deployment"></a><span data-ttu-id="90e32-188">範本部署</span><span class="sxs-lookup"><span data-stu-id="90e32-188">Template deployment</span></span>
<span data-ttu-id="90e32-189">使用資源管理員中，您可以建立定義 hello 基礎結構和 Azure 方案的組態 （以 JSON 格式） 的範本。</span><span class="sxs-lookup"><span data-stu-id="90e32-189">With Resource Manager, you can create a template (in JSON format) that defines hello infrastructure and configuration of your Azure solution.</span></span> <span data-ttu-id="90e32-190">透過範本，您可以在整個生命週期中重複部署方案，並確信您的資源會以一致的狀態部署。</span><span class="sxs-lookup"><span data-stu-id="90e32-190">By using a template, you can repeatedly deploy your solution throughout its lifecycle and have confidence your resources are deployed in a consistent state.</span></span> <span data-ttu-id="90e32-191">當您從 hello 入口網站建立一個方案時，hello 方案會自動包含部署範本。</span><span class="sxs-lookup"><span data-stu-id="90e32-191">When you create a solution from hello portal, hello solution automatically includes a deployment template.</span></span> <span data-ttu-id="90e32-192">您不需要 toocreate 從頭範本因為您可以從您的方案的開始 hello 範本並進行自訂 toomeet 您的特定需求。</span><span class="sxs-lookup"><span data-stu-id="90e32-192">You do not have toocreate your template from scratch because you can start with hello template for your solution and customize it toomeet your specific needs.</span></span> <span data-ttu-id="90e32-193">您可以匯出 hello hello 資源群組，目前的狀態或是檢視用於特定部署的 hello 範本來擷取現有的資源群組的範本。</span><span class="sxs-lookup"><span data-stu-id="90e32-193">You can retrieve a template for an existing resource group by either exporting hello current state of hello resource group, or viewing hello template used for a particular deployment.</span></span> <span data-ttu-id="90e32-194">檢視 hello[匯出範本](resource-manager-export-template.md)是很有幫助方式 toolearn hello 範本語法的相關。</span><span class="sxs-lookup"><span data-stu-id="90e32-194">Viewing hello [exported template](resource-manager-export-template.md) is a helpful way toolearn about hello template syntax.</span></span>

<span data-ttu-id="90e32-195">toolearn hello 格式的 hello 範本和建構它，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-195">toolearn about hello format of hello template and how you construct it, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span> <span data-ttu-id="90e32-196">tooview hello JSON 語法資源類型，請參閱[Azure Resource Manager 範本中定義的資源](/azure/templates/)。</span><span class="sxs-lookup"><span data-stu-id="90e32-196">tooview hello JSON syntax for resources types, see [Define resources in Azure Resource Manager templates](/azure/templates/).</span></span>

<span data-ttu-id="90e32-197">資源管理員處理 hello 像任何其他要求的範本 (請參閱 hello 影像[一致的管理層](#consistent-management-layer))。</span><span class="sxs-lookup"><span data-stu-id="90e32-197">Resource Manager processes hello template like any other request (see hello image for [Consistent management layer](#consistent-management-layer)).</span></span> <span data-ttu-id="90e32-198">它會剖析 hello 範本，並將其語法轉換成的 hello 適當的資源提供者 REST API 作業。</span><span class="sxs-lookup"><span data-stu-id="90e32-198">It parses hello template and converts its syntax into REST API operations for hello appropriate resource providers.</span></span> <span data-ttu-id="90e32-199">例如，當資源管理員收到範本具有下列資源定義的 hello:</span><span class="sxs-lookup"><span data-stu-id="90e32-199">For example, when Resource Manager receives a template with hello following resource definition:</span></span>

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

<span data-ttu-id="90e32-200">它會將轉換 hello 定義 toohello 下列 REST API 作業，因為它會傳送 toohello Microsoft.Storage 資源提供者：</span><span class="sxs-lookup"><span data-stu-id="90e32-200">It converts hello definition toohello following REST API operation, which is sent toohello Microsoft.Storage resource provider:</span></span>

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

<span data-ttu-id="90e32-201">您定義的範本和資源群組已完全啟動 tooyou 和您要如何 toomanage 您的方案。</span><span class="sxs-lookup"><span data-stu-id="90e32-201">How you define templates and resource groups is entirely up tooyou and how you want toomanage your solution.</span></span> <span data-ttu-id="90e32-202">例如，您可以部署三層應用程式透過單一範本 tooa 單一資源群組。</span><span class="sxs-lookup"><span data-stu-id="90e32-202">For example, you can deploy your three tier application through a single template tooa single resource group.</span></span>

![三層式範本](./media/resource-group-overview/3-tier-template.png)

<span data-ttu-id="90e32-204">但是，如果您沒有 toodefine 整個基礎結構在單一範本。</span><span class="sxs-lookup"><span data-stu-id="90e32-204">But, you do not have toodefine your entire infrastructure in a single template.</span></span> <span data-ttu-id="90e32-205">通常，它可讓意義 toodivide 成一組目標、 目的特定範本部署需求。</span><span class="sxs-lookup"><span data-stu-id="90e32-205">Often, it makes sense toodivide your deployment requirements into a set of targeted, purpose-specific templates.</span></span> <span data-ttu-id="90e32-206">您可以輕鬆地將這些份本重複使用於不同的方案。</span><span class="sxs-lookup"><span data-stu-id="90e32-206">You can easily reuse these templates for different solutions.</span></span> <span data-ttu-id="90e32-207">toodeploy 特定的方案，您會建立主要的範本，用來連結所有必要的 hello 範本。</span><span class="sxs-lookup"><span data-stu-id="90e32-207">toodeploy a particular solution, you create a master template that links all hello required templates.</span></span> <span data-ttu-id="90e32-208">hello 如下圖所示 toodeploy 三層解決方案透過父範本包含三個巢狀方式範本。</span><span class="sxs-lookup"><span data-stu-id="90e32-208">hello following image shows how toodeploy a three tier solution through a parent template that includes three nested templates.</span></span>

![巢狀階層範本](./media/resource-group-overview/nested-tiers-template.png)

<span data-ttu-id="90e32-210">如果您想像您具有獨立的生命週期的層，您可以部署三個層級 tooseparate 資源群組。</span><span class="sxs-lookup"><span data-stu-id="90e32-210">If you envision your tiers having separate lifecycles, you can deploy your three tiers tooseparate resource groups.</span></span> <span data-ttu-id="90e32-211">請注意 hello 資源仍然可以在其他資源群組中的連結的 tooresources。</span><span class="sxs-lookup"><span data-stu-id="90e32-211">Notice hello resources can still be linked tooresources in other resource groups.</span></span>

![階層範本](./media/resource-group-overview/tier-templates.png)

<span data-ttu-id="90e32-213">如需更多有關設計範本的建議，請參閱[設計 Azure Resource Manager 範本的模式](best-practices-resource-manager-design-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-213">For more suggestions about designing your templates, see [Patterns for designing Azure Resource Manager templates](best-practices-resource-manager-design-templates.md).</span></span> <span data-ttu-id="90e32-214">如需巢狀範本的相關資訊，請參閱[透過 Azure Resource Manager 使用連結的範本](resource-group-linked-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-214">For information about nested templates, see [Using linked templates with Azure Resource Manager](resource-group-linked-templates.md).</span></span>

<span data-ttu-id="90e32-215">Azure 資源管理員會分析 hello 正確的順序會建立 tooensure 資源的相依性。</span><span class="sxs-lookup"><span data-stu-id="90e32-215">Azure Resource Manager analyzes dependencies tooensure resources are created in hello correct order.</span></span> <span data-ttu-id="90e32-216">如果某個資源依賴另一個資源的值 (例如需要儲存體帳戶以供磁碟使用的虛擬機器)，您必須設定相依性。</span><span class="sxs-lookup"><span data-stu-id="90e32-216">If one resource relies on a value from another resource (such as a virtual machine needing a storage account for disks), you set a dependency.</span></span> <span data-ttu-id="90e32-217">如需詳細資訊，請參閱 [定義 Azure Resource Manager 範本中的相依性](resource-group-define-dependencies.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-217">For more information, see [Defining dependencies in Azure Resource Manager templates](resource-group-define-dependencies.md).</span></span>

<span data-ttu-id="90e32-218">您也可以使用 hello 範本更新 toohello 基礎結構。</span><span class="sxs-lookup"><span data-stu-id="90e32-218">You can also use hello template for updates toohello infrastructure.</span></span> <span data-ttu-id="90e32-219">例如，您可以將資源 tooyour 方案，並將已部署的 hello 資源設定規則。</span><span class="sxs-lookup"><span data-stu-id="90e32-219">For example, you can add a resource tooyour solution and add configuration rules for hello resources that are already deployed.</span></span> <span data-ttu-id="90e32-220">如果 hello 範本會指定建立資源，但該資源已存在，Azure 資源管理員會執行更新，而不是建立新的資產。</span><span class="sxs-lookup"><span data-stu-id="90e32-220">If hello template specifies creating a resource but that resource already exists, Azure Resource Manager performs an update instead of creating a new asset.</span></span> <span data-ttu-id="90e32-221">Azure 資源管理員更新 hello 現有資產 toohello 相同狀態做為它就是當新的。</span><span class="sxs-lookup"><span data-stu-id="90e32-221">Azure Resource Manager updates hello existing asset toohello same state as it would be as new.</span></span>  

<span data-ttu-id="90e32-222">當您需要其他的作業，例如安裝不包含在 hello 安裝程式的特定軟體時，資源管理員會提供擴充功能案例。</span><span class="sxs-lookup"><span data-stu-id="90e32-222">Resource Manager provides extensions for scenarios when you need additional operations such as installing particular software that is not included in hello setup.</span></span> <span data-ttu-id="90e32-223">如果您已經使用組態管理服務，例如 DSC、Chef 或 Puppet，您可以透過使用擴充功能繼續使用該服務。</span><span class="sxs-lookup"><span data-stu-id="90e32-223">If you are already using a configuration management service, like DSC, Chef or Puppet, you can continue working with that service by using extensions.</span></span> <span data-ttu-id="90e32-224">如需虛擬機器擴充功能的相關資訊，請參閱[有關虛擬機器擴充功能和功能](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="90e32-224">For information about virtual machine extensions, see [About virtual machine extensions and features](../virtual-machines/windows/extensions-features.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> 

<span data-ttu-id="90e32-225">最後，hello 範本會變成 hello 原始碼應用程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="90e32-225">Finally, hello template becomes part of hello source code for your app.</span></span> <span data-ttu-id="90e32-226">您可以將它簽入 tooyour 原始程式碼儲存機制，並隨著您的應用程式發展更新。</span><span class="sxs-lookup"><span data-stu-id="90e32-226">You can check it in tooyour source code repository and update it as your app evolves.</span></span> <span data-ttu-id="90e32-227">您可以編輯 hello 範本，透過 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="90e32-227">You can edit hello template through Visual Studio.</span></span>

<span data-ttu-id="90e32-228">定義您的範本之後, 您就準備好 toodeploy hello 資源 tooAzure。</span><span class="sxs-lookup"><span data-stu-id="90e32-228">After defining your template, you are ready toodeploy hello resources tooAzure.</span></span> <span data-ttu-id="90e32-229">如需 hello 命令 toodeploy hello 資源，請參閱：</span><span class="sxs-lookup"><span data-stu-id="90e32-229">For hello commands toodeploy hello resources, see:</span></span>

* [<span data-ttu-id="90e32-230">使用 Resource Manager 範本與 Azure PowerShell 來部署資源</span><span class="sxs-lookup"><span data-stu-id="90e32-230">Deploy resources with Resource Manager templates and Azure PowerShell</span></span>](resource-group-template-deploy.md)
* [<span data-ttu-id="90e32-231">使用 Resource Manager 範本與 Azure CLI 部署資源</span><span class="sxs-lookup"><span data-stu-id="90e32-231">Deploy resources with Resource Manager templates and Azure CLI</span></span>](resource-group-template-deploy-cli.md)
* [<span data-ttu-id="90e32-232">使用 Resource Manager 範本與 Azure 入口網站來部署資源</span><span class="sxs-lookup"><span data-stu-id="90e32-232">Deploy resources with Resource Manager templates and Azure portal</span></span>](resource-group-template-deploy-portal.md)
* [<span data-ttu-id="90e32-233">使用 Resource Manager 範本和 Resource Manager REST API 部署資源</span><span class="sxs-lookup"><span data-stu-id="90e32-233">Deploy resources with Resource Manager templates and Resource Manager REST API</span></span>](resource-group-template-deploy-rest.md)

## <a name="tags"></a><span data-ttu-id="90e32-234">標記</span><span class="sxs-lookup"><span data-stu-id="90e32-234">Tags</span></span>
<span data-ttu-id="90e32-235">資源管理員提供標記的功能可讓您根據管理或帳單的 tooyour 需求 toocategorize 資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-235">Resource Manager provides a tagging feature that enables you toocategorize resources according tooyour requirements for managing or billing.</span></span> <span data-ttu-id="90e32-236">當您有複雜的資源群組和資源，而且需要 toovisualize 這些資產，可透過 hello 大部分意義 tooyou hello 方式，請使用標記。</span><span class="sxs-lookup"><span data-stu-id="90e32-236">Use tags when you have a complex collection of resource groups and resources, and need toovisualize those assets in hello way that makes hello most sense tooyou.</span></span> <span data-ttu-id="90e32-237">例如，您可以標記您的組織中具有類似的角色，或屬於 toohello 資源相同的部門。</span><span class="sxs-lookup"><span data-stu-id="90e32-237">For example, you could tag resources that serve a similar role in your organization or belong toohello same department.</span></span> <span data-ttu-id="90e32-238">沒有標記，您的組織中的使用者可以建立多個資源，可能會難以 toolater 識別及管理。</span><span class="sxs-lookup"><span data-stu-id="90e32-238">Without tags, users in your organization can create multiple resources that may be difficult toolater identify and manage.</span></span> <span data-ttu-id="90e32-239">比方說，您可能需要 toodelete 特定專案的所有 hello 資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-239">For example, you may wish toodelete all hello resources for a particular project.</span></span> <span data-ttu-id="90e32-240">如果這些資源不會標記為 hello 專案，您必須 toomanually 找到它們。</span><span class="sxs-lookup"><span data-stu-id="90e32-240">If those resources are not tagged for hello project, you have toomanually find them.</span></span> <span data-ttu-id="90e32-241">標記可以是重要的方式，讓您 tooreduce 不必要的成本，您的訂用帳戶中。</span><span class="sxs-lookup"><span data-stu-id="90e32-241">Tagging can be an important way for you tooreduce unnecessary costs in your subscription.</span></span> 

<span data-ttu-id="90e32-242">資源不需要在 hello tooreside 相同資源群組 tooshare 標記。</span><span class="sxs-lookup"><span data-stu-id="90e32-242">Resources do not need tooreside in hello same resource group tooshare a tag.</span></span> <span data-ttu-id="90e32-243">您可以建立您自己標記分類 tooensure 您組織中的所有使用者都使用通用標記，而不是使用者不小心套用稍微不同的標籤 （例如 「 部門 」 而不是 「 部門 」）。</span><span class="sxs-lookup"><span data-stu-id="90e32-243">You can create your own tag taxonomy tooensure that all users in your organization use common tags rather than users inadvertently applying slightly different tags (such as "dept" instead of "department").</span></span>

<span data-ttu-id="90e32-244">hello 下列範例會顯示套用標籤 tooa 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="90e32-244">hello following example shows a tag applied tooa virtual machine.</span></span>

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

<span data-ttu-id="90e32-245">tooretrieve 所有 hello 資源標記值，都使用下列 PowerShell cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="90e32-245">tooretrieve all hello resources with a tag value, use hello following PowerShell cmdlet:</span></span>

```powershell
Find-AzureRmResource -TagName costCenter -TagValue Finance
```

<span data-ttu-id="90e32-246">或者，hello 下列 Azure CLI 2.0 命令：</span><span class="sxs-lookup"><span data-stu-id="90e32-246">Or, hello following Azure CLI 2.0 command:</span></span>

```azurecli
az resource list --tag costCenter=Finance
```

<span data-ttu-id="90e32-247">您也可以檢視透過 hello Azure 入口網站已加上標籤的資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-247">You can also view tagged resources through hello Azure portal.</span></span>

<span data-ttu-id="90e32-248">hello[使用量報告](../billing/billing-understand-your-bill.md)針對您的訂閱包含標記的名稱和值，這可讓您依標記的 toobreak 出成本。</span><span class="sxs-lookup"><span data-stu-id="90e32-248">hello [usage report](../billing/billing-understand-your-bill.md) for your subscription includes tag names and values, which enables you toobreak out costs by tags.</span></span> <span data-ttu-id="90e32-249">如需標記的詳細資訊，請參閱[使用標記 tooorganize 您的 Azure 資源](resource-group-using-tags.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-249">For more information about tags, see [Using tags tooorganize your Azure resources](resource-group-using-tags.md).</span></span>

## <a name="access-control"></a><span data-ttu-id="90e32-250">存取控制</span><span class="sxs-lookup"><span data-stu-id="90e32-250">Access control</span></span>
<span data-ttu-id="90e32-251">資源管理員可讓您能夠存取您組織的 toospecific 動作 toocontrol。</span><span class="sxs-lookup"><span data-stu-id="90e32-251">Resource Manager enables you toocontrol who has access toospecific actions for your organization.</span></span> <span data-ttu-id="90e32-252">原生至 hello 管理平台整合以角色為基礎的存取控制 (RBAC)，以及適用於資源群組中的存取控制 tooall 服務。</span><span class="sxs-lookup"><span data-stu-id="90e32-252">It natively integrates role-based access control (RBAC) into hello management platform and applies that access control tooall services in your resource group.</span></span> 

<span data-ttu-id="90e32-253">使用角色型存取控制時，有兩個主要概念 toounderstand:</span><span class="sxs-lookup"><span data-stu-id="90e32-253">There are two main concepts toounderstand when working with role-based access control:</span></span>

* <span data-ttu-id="90e32-254">角色定義 - 描述一組權限，並可用於許多指派。</span><span class="sxs-lookup"><span data-stu-id="90e32-254">Role definitions - describe a set of permissions and can be used in many assignments.</span></span>
* <span data-ttu-id="90e32-255">角色指派 - 為定義與特定範圍 (訂用帳戶、資源群組或資源) 的身分識別 (使用者或群組) 建立關聯。</span><span class="sxs-lookup"><span data-stu-id="90e32-255">Role assignments - associate a definition with an identity (user or group) for a particular scope (subscription, resource group, or resource).</span></span> <span data-ttu-id="90e32-256">hello 分派繼承較低範圍。</span><span class="sxs-lookup"><span data-stu-id="90e32-256">hello assignment is inherited by lower scopes.</span></span>

<span data-ttu-id="90e32-257">您可以加入使用者 toopre 定義的平台和資源特定角色。</span><span class="sxs-lookup"><span data-stu-id="90e32-257">You can add users toopre-defined platform and resource-specific roles.</span></span> <span data-ttu-id="90e32-258">例如，您可以利用 hello 稱為允許使用者 tooview 資源的讀取器的預先定義角色，但無法變更它們。</span><span class="sxs-lookup"><span data-stu-id="90e32-258">For example, you can take advantage of hello pre-defined role called Reader that permits users tooview resources but not change them.</span></span> <span data-ttu-id="90e32-259">您將使用者加入您的組織需要這種類型的存取 toohello 讀取者角色中，並套用 hello 角色 toohello 訂用帳戶、 資源群組或資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-259">You add users in your organization that need this type of access toohello Reader role and apply hello role toohello subscription, resource group, or resource.</span></span>

<span data-ttu-id="90e32-260">Azure 提供下列四個平台角色的 hello:</span><span class="sxs-lookup"><span data-stu-id="90e32-260">Azure provides hello following four platform roles:</span></span>

1. <span data-ttu-id="90e32-261">擁有者 - 可以管理所有項目，包括存取</span><span class="sxs-lookup"><span data-stu-id="90e32-261">Owner - can manage everything, including access</span></span>
2. <span data-ttu-id="90e32-262">參與者 - 可以管理存取以外的所有內容</span><span class="sxs-lookup"><span data-stu-id="90e32-262">Contributor - can manage everything except access</span></span>
3. <span data-ttu-id="90e32-263">讀取者 - 可以檢視所有項目，但是無法進行變更</span><span class="sxs-lookup"><span data-stu-id="90e32-263">Reader - can view everything, but can't make changes</span></span>
4. <span data-ttu-id="90e32-264">使用者存取管理員可以管理使用者存取 tooAzure 資源</span><span class="sxs-lookup"><span data-stu-id="90e32-264">User Access Administrator - can manage user access tooAzure resources</span></span>

<span data-ttu-id="90e32-265">Azure 也提供數個資源特有的角色。</span><span class="sxs-lookup"><span data-stu-id="90e32-265">Azure also provides several resource-specific roles.</span></span> <span data-ttu-id="90e32-266">一些常見的角色有︰</span><span class="sxs-lookup"><span data-stu-id="90e32-266">Some common ones are:</span></span>

1. <span data-ttu-id="90e32-267">虛擬機器參與者-可以管理虛擬機器，但不是授與存取 toothem，而且不能管理 hello 虛擬網路或存放裝置帳戶 toowhich 連線</span><span class="sxs-lookup"><span data-stu-id="90e32-267">Virtual Machine Contributor - can manage virtual machines but not grant access toothem, and cannot manage hello virtual network or storage account toowhich they are connected</span></span>
2. <span data-ttu-id="90e32-268">網路參與者-可以管理所有的網路資源，但不是授與存取 toothem</span><span class="sxs-lookup"><span data-stu-id="90e32-268">Network Contributor - can manage all network resources, but not grant access toothem</span></span>
3. <span data-ttu-id="90e32-269">儲存體帳戶參與者-可以管理儲存體帳戶，但不是授與存取 toothem</span><span class="sxs-lookup"><span data-stu-id="90e32-269">Storage Account Contributor - Can manage storage accounts, but not grant access toothem</span></span>
4. <span data-ttu-id="90e32-270">SQL Server 參與者 - 可以管理 SQL Server 和資料庫，但是無法管理它們的安全性相關原則</span><span class="sxs-lookup"><span data-stu-id="90e32-270">SQL Server Contributor - Can manage SQL servers and databases, but not their security-related policies</span></span>
5. <span data-ttu-id="90e32-271">網站參與者-可以管理網站，但不是 hello web 計劃 toowhich 連線</span><span class="sxs-lookup"><span data-stu-id="90e32-271">Website Contributor - Can manage websites, but not hello web plans toowhich they are connected</span></span>

<span data-ttu-id="90e32-272">Hello 的角色和允許的動作的完整清單，請參閱[RBAC： 內建的角色](../active-directory/role-based-access-built-in-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-272">For hello full list of roles and permitted actions, see [RBAC: Built in Roles](../active-directory/role-based-access-built-in-roles.md).</span></span> <span data-ttu-id="90e32-273">如需角色型存取控制的詳細資訊，請參閱 [Azure 角色型存取控制](../active-directory/role-based-access-control-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-273">For more information about role-based access control, see [Azure Role-based Access Control](../active-directory/role-based-access-control-configure.md).</span></span> 

<span data-ttu-id="90e32-274">在某些情況下，您想 toorun 程式碼或指令碼，存取資源，但是不想讓 toorun 在使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="90e32-274">In some cases, you want toorun code or script that accesses resources, but you do not want toorun it under a user’s credentials.</span></span> <span data-ttu-id="90e32-275">相反地，您會想 toocreate hello 應用程式，稱為 「 服務主體的身分識別，以及指派 hello 服務主體的 hello 適當角色。</span><span class="sxs-lookup"><span data-stu-id="90e32-275">Instead, you want toocreate an identity called a service principal for hello application and assign hello appropriate role for hello service principal.</span></span> <span data-ttu-id="90e32-276">資源管理員可讓您 toocreate hello 應用程式認證，並且以程式設計方式驗證 hello 應用程式。</span><span class="sxs-lookup"><span data-stu-id="90e32-276">Resource Manager enables you toocreate credentials for hello application and programmatically authenticate hello application.</span></span> <span data-ttu-id="90e32-277">toolearn 有關建立服務主體，請參閱下列主題之一：</span><span class="sxs-lookup"><span data-stu-id="90e32-277">toolearn about creating service principals, see one of following topics:</span></span>

* [<span data-ttu-id="90e32-278">使用 Azure PowerShell toocreate 服務主體 tooaccess 資源</span><span class="sxs-lookup"><span data-stu-id="90e32-278">Use Azure PowerShell toocreate a service principal tooaccess resources</span></span>](resource-group-authenticate-service-principal.md)
* [<span data-ttu-id="90e32-279">使用 Azure CLI toocreate 服務主體 tooaccess 資源</span><span class="sxs-lookup"><span data-stu-id="90e32-279">Use Azure CLI toocreate a service principal tooaccess resources</span></span>](resource-group-authenticate-service-principal-cli.md)
* [<span data-ttu-id="90e32-280">使用入口網站 toocreate Azure Active Directory 應用程式和服務主體可存取資源</span><span class="sxs-lookup"><span data-stu-id="90e32-280">Use portal toocreate Azure Active Directory application and service principal that can access resources</span></span>](resource-group-create-service-principal-portal.md)

<span data-ttu-id="90e32-281">您可以同時也可以明確鎖定重要的資源 tooprevent 使用者刪除或修改它們。</span><span class="sxs-lookup"><span data-stu-id="90e32-281">You can also explicitly lock critical resources tooprevent users from deleting or modifying them.</span></span> <span data-ttu-id="90e32-282">如需詳細資訊，請參閱[使用 Azure Resource Manager 來鎖定資源](resource-group-lock-resources.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-282">For more information, see [Lock resources with Azure Resource Manager](resource-group-lock-resources.md).</span></span>

## <a name="activity-logs"></a><span data-ttu-id="90e32-283">活動記錄</span><span class="sxs-lookup"><span data-stu-id="90e32-283">Activity logs</span></span>
<span data-ttu-id="90e32-284">Resource Manager 會記錄所有建立、修改或刪除資源的作業。</span><span class="sxs-lookup"><span data-stu-id="90e32-284">Resource Manager logs all operations that create, modify, or delete a resource.</span></span> <span data-ttu-id="90e32-285">您可以使用 hello 活動記錄檔 toofind 錯誤進行疑難排解時或 toomonitor 您組織中的使用者如何修改資源。</span><span class="sxs-lookup"><span data-stu-id="90e32-285">You can use hello activity logs toofind an error when troubleshooting or toomonitor how a user in your organization modified a resource.</span></span> <span data-ttu-id="90e32-286">toosee hello 記錄檔中，選取**活動記錄**在 hello**設定**刀鋒視窗中的資源群組。</span><span class="sxs-lookup"><span data-stu-id="90e32-286">toosee hello logs, select **Activity logs** in hello **Settings** blade for a resource group.</span></span> <span data-ttu-id="90e32-287">您可以由許多不同的值包括哪些使用者起始 hello 作業篩選 hello 記錄檔。</span><span class="sxs-lookup"><span data-stu-id="90e32-287">You can filter hello logs by many different values including which user initiated hello operation.</span></span> <span data-ttu-id="90e32-288">如需有關使用 hello 活動記錄檔資訊，請參閱[檢視活動記錄 toomanage Azure 資源](resource-group-audit.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-288">For information about working with hello activity logs, see [View activity logs toomanage Azure resources](resource-group-audit.md).</span></span>

## <a name="customized-policies"></a><span data-ttu-id="90e32-289">自訂的原則</span><span class="sxs-lookup"><span data-stu-id="90e32-289">Customized policies</span></span>
<span data-ttu-id="90e32-290">資源管理員可讓您管理您的資源 toocreate 自訂原則。</span><span class="sxs-lookup"><span data-stu-id="90e32-290">Resource Manager enables you toocreate customized policies for managing your resources.</span></span> <span data-ttu-id="90e32-291">hello 您所建立的原則類型可以包含各種不同的案例。</span><span class="sxs-lookup"><span data-stu-id="90e32-291">hello types of policies you create can include diverse scenarios.</span></span> <span data-ttu-id="90e32-292">您可以強制執行資源的的命名慣例、限制可以部署的資源類型和執行個體，或限制可以裝載某個資源類型的區域。</span><span class="sxs-lookup"><span data-stu-id="90e32-292">You can enforce a naming convention on resources, limit which types and instances of resources can be deployed, or limit which regions can host a type of resource.</span></span> <span data-ttu-id="90e32-293">您可以依部門要求資源 tooorganize 帳單上的標記值。</span><span class="sxs-lookup"><span data-stu-id="90e32-293">You can require a tag value on resources tooorganize billing by departments.</span></span> <span data-ttu-id="90e32-294">您可以建立原則 toohelp 降低成本和維護您的訂用帳戶中的一致性。</span><span class="sxs-lookup"><span data-stu-id="90e32-294">You create policies toohelp reduce costs and maintain consistency in your subscription.</span></span> 

<span data-ttu-id="90e32-295">您需要使用 JSON 來定義原則，然後將這些原則套用到您的訂用帳戶或資源群組內。</span><span class="sxs-lookup"><span data-stu-id="90e32-295">You define policies with JSON and then apply those policies either across your subscription or within a resource group.</span></span> <span data-ttu-id="90e32-296">原則是不同角色型存取控制，因為它們是套用的 tooresource 類型。</span><span class="sxs-lookup"><span data-stu-id="90e32-296">Policies are different than role-based access control because they are applied tooresource types.</span></span>

<span data-ttu-id="90e32-297">下列範例中的 hello 顯示原則，以確保指定的所有資源都包括 costCenter 標記的標記一致性。</span><span class="sxs-lookup"><span data-stu-id="90e32-297">hello following example shows a policy that ensures tag consistency by specifying that all resources include a costCenter tag.</span></span>

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

<span data-ttu-id="90e32-298">您還可以建立其他類型的原則。</span><span class="sxs-lookup"><span data-stu-id="90e32-298">There are many more types of policies you can create.</span></span> <span data-ttu-id="90e32-299">如需詳細資訊，請參閱[使用原則 toomanage 資源和控制存取](resource-manager-policy.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-299">For more information, see [Use Policy toomanage resources and control access](resource-manager-policy.md).</span></span>

## <a name="sdks"></a><span data-ttu-id="90e32-300">SDK</span><span class="sxs-lookup"><span data-stu-id="90e32-300">SDKs</span></span>
<span data-ttu-id="90e32-301">Azure SDK 可供多個語言和平台使用。</span><span class="sxs-lookup"><span data-stu-id="90e32-301">Azure SDKs are available for multiple languages and platforms.</span></span> <span data-ttu-id="90e32-302">這些語言實作都是透過其生態系統的套件管理員和 GitHub 提供。</span><span class="sxs-lookup"><span data-stu-id="90e32-302">Each of these language implementations is available through its ecosystem package manager and GitHub.</span></span>

<span data-ttu-id="90e32-303">以下是我們的開放原始碼 SDK 存放庫。</span><span class="sxs-lookup"><span data-stu-id="90e32-303">Here are our Open Source SDK repositories.</span></span> <span data-ttu-id="90e32-304">歡迎提供意見反應、問題並提取要求。</span><span class="sxs-lookup"><span data-stu-id="90e32-304">We welcome feedback, issues, and pull requests.</span></span>

* [<span data-ttu-id="90e32-305">Azure SDK for .NET</span><span class="sxs-lookup"><span data-stu-id="90e32-305">Azure SDK for .NET</span></span>](https://github.com/Azure/azure-sdk-for-net)
* [<span data-ttu-id="90e32-306">適用於 Java 的 Azure 管理程式庫</span><span class="sxs-lookup"><span data-stu-id="90e32-306">Azure Management Libraries for Java</span></span>](https://github.com/Azure/azure-sdk-for-java)
* [<span data-ttu-id="90e32-307">Azure SDK for Node.js</span><span class="sxs-lookup"><span data-stu-id="90e32-307">Azure SDK for Node.js</span></span>](https://github.com/Azure/azure-sdk-for-node)
* [<span data-ttu-id="90e32-308">Azure SDK for PHP</span><span class="sxs-lookup"><span data-stu-id="90e32-308">Azure SDK for PHP</span></span>](https://github.com/Azure/azure-sdk-for-php)
* [<span data-ttu-id="90e32-309">Azure SDK for Python</span><span class="sxs-lookup"><span data-stu-id="90e32-309">Azure SDK for Python</span></span>](https://github.com/Azure/azure-sdk-for-python)
* [<span data-ttu-id="90e32-310">Azure SDK for Ruby</span><span class="sxs-lookup"><span data-stu-id="90e32-310">Azure SDK for Ruby</span></span>](https://github.com/Azure/azure-sdk-for-ruby)

<span data-ttu-id="90e32-311">如需使用這些語言搭配您的資源的相關資訊，請參閱：</span><span class="sxs-lookup"><span data-stu-id="90e32-311">For information about using these languages with your resources, see:</span></span>

* [<span data-ttu-id="90e32-312">適用於 .NET 開發人員的 Azure</span><span class="sxs-lookup"><span data-stu-id="90e32-312">Azure for .NET developers</span></span>](/dotnet/azure/?view=azure-dotnet)
* [<span data-ttu-id="90e32-313">適用於 Java 開發人員的 Azure</span><span class="sxs-lookup"><span data-stu-id="90e32-313">Azure for Java developers</span></span>](/java/azure/)
* [<span data-ttu-id="90e32-314">適用於 Node.js 開發人員的 Azure</span><span class="sxs-lookup"><span data-stu-id="90e32-314">Azure for Node.js developers</span></span>](/nodejs/azure/)
* [<span data-ttu-id="90e32-315">適用於 Python 開發人員的 Azure</span><span class="sxs-lookup"><span data-stu-id="90e32-315">Azure for Python developers</span></span>](/python/azure/)

> [!NOTE]
> <span data-ttu-id="90e32-316">如果 hello SDK 並不提供所需的 hello 功能，您也可以呼叫 toohello [Azure REST API](https://docs.microsoft.com/rest/api/resources/)直接。</span><span class="sxs-lookup"><span data-stu-id="90e32-316">If hello SDK doesn't provide hello required functionality, you can also call toohello [Azure REST API](https://docs.microsoft.com/rest/api/resources/) directly.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="90e32-317">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90e32-317">Next steps</span></span>
* <span data-ttu-id="90e32-318">簡單介紹 tooworking 範本，請參閱[匯出 Azure Resource Manager 範本，從現有的資源](resource-manager-export-template.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-318">For a simple introduction tooworking with templates, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="90e32-319">如需更詳細的建立範本逐步解說，請參閱[建立第一個 Azure Resource Manager 範本](resource-manager-create-first-template.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-319">For a more thorough walkthrough of creating a template, see [Create your first Azure Resource Manager template](resource-manager-create-first-template.md).</span></span>
* <span data-ttu-id="90e32-320">toounderstand hello 函式，您可以使用在範本中，請參閱[樣板函式](resource-group-template-functions.md)</span><span class="sxs-lookup"><span data-stu-id="90e32-320">toounderstand hello functions you can use in a template, see [Template functions](resource-group-template-functions.md)</span></span>
* <span data-ttu-id="90e32-321">如需有關如何搭配使用 Visual Studio 與 Resource Manager 的相關資訊，請參閱 [透過 Visual Studio 建立和部署 Azure 資源群組](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md)。</span><span class="sxs-lookup"><span data-stu-id="90e32-321">For information about using Visual Studio with Resource Manager, see [Creating and deploying Azure resource groups through Visual Studio](vs-azure-tools-resource-groups-deployment-projects-create-deploy.md).</span></span>

<span data-ttu-id="90e32-322">以下是此概觀的示範影片。</span><span class="sxs-lookup"><span data-stu-id="90e32-322">Here's a video demonstration of this overview:</span></span>

>[!VIDEO https://channel9.msdn.com/Blogs/Azure-Documentation-Shorts/Azure-Resource-Manager-Overview/player]


[powershellref]: https://docs.microsoft.com/powershell/resourcemanager/azurerm.resources/v3.2.0/azurerm.resources
