---
title: "Azure 資源的 aaaSet 部署順序 |Microsoft 文件"
description: "描述如何將 tooset 一個資源依存於另一個資源期間部署 tooensure 資源部署 hello 正確的順序。"
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.assetid: 34ebaf1e-480c-4b4d-9bf6-251bd3f8f2cf
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/03/2017
ms.author: tomfitz
ms.openlocfilehash: 2f658f4c85236966c46b34a65aafb8426c92806c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="define-hello-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="e715c-103">定義 hello 順序來部署 Azure 資源管理員範本中的資源</span><span class="sxs-lookup"><span data-stu-id="e715c-103">Define hello order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="e715c-104">指定的資源，可以有其他資源，必須先建立 hello 資源部署。</span><span class="sxs-lookup"><span data-stu-id="e715c-104">For a given resource, there can be other resources that must exist before hello resource is deployed.</span></span> <span data-ttu-id="e715c-105">比方說，SQL server 必須存在，然後再嘗試 toodeploy SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="e715c-105">For example, a SQL server must exist before attempting toodeploy a SQL database.</span></span> <span data-ttu-id="e715c-106">您定義此關聯性標示一個資源依存於 hello 與其他資源。</span><span class="sxs-lookup"><span data-stu-id="e715c-106">You define this relationship by marking one resource as dependent on hello other resource.</span></span> <span data-ttu-id="e715c-107">您定義的相依性以 hello **dependsOn**項目，或使用 hello**參考**函式。</span><span class="sxs-lookup"><span data-stu-id="e715c-107">You define a dependency with hello **dependsOn** element, or by using hello **reference** function.</span></span> 

<span data-ttu-id="e715c-108">資源管理員會評估 hello 資源之間的相依性，並將它們部署在其相依順序。</span><span class="sxs-lookup"><span data-stu-id="e715c-108">Resource Manager evaluates hello dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="e715c-109">資源若不互相依賴，資源管理員就會平行部署資源。</span><span class="sxs-lookup"><span data-stu-id="e715c-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="e715c-110">您只需要 toodefine 相依性的 hello 以部署的資源相同的範本。</span><span class="sxs-lookup"><span data-stu-id="e715c-110">You only need toodefine dependencies for resources that are deployed in hello same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="e715c-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="e715c-111">dependsOn</span></span>
<span data-ttu-id="e715c-112">在您的範本，hello dependsOn 元素可讓您 toodefine 一個資源當做一個或多個資源相依性。</span><span class="sxs-lookup"><span data-stu-id="e715c-112">Within your template, hello dependsOn element enables you toodefine one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="e715c-113">其值可以是以逗號分隔的資源名稱清單。</span><span class="sxs-lookup"><span data-stu-id="e715c-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="e715c-114">hello 下列範例顯示取決於負載平衡器、 虛擬網路和一個迴圈，建立多個儲存體帳戶的虛擬機器規模集。</span><span class="sxs-lookup"><span data-stu-id="e715c-114">hello following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="e715c-115">這些其他的資源不會顯示 hello 遵循範例中，但它們需要 tooexist hello 範本中的其他位置。</span><span class="sxs-lookup"><span data-stu-id="e715c-115">These other resources are not shown in hello following example, but they would need tooexist elsewhere in hello template.</span></span>

```json
{
  "type": "Microsoft.Compute/virtualMachineScaleSets",
  "name": "[variables('namingInfix')]",
  "location": "[variables('location')]",
  "apiVersion": "2016-03-30",
  "tags": {
    "displayName": "VMScaleSet"
  },
  "dependsOn": [
    "[variables('loadBalancerName')]",
    "[variables('virtualNetworkName')]",
    "storageLoop",
  ],
  ...
}
```

<span data-ttu-id="e715c-116">建立名為複製迴圈的 hello 資源相依性都會包含在上述範例中的 hello， **storageLoop**。</span><span class="sxs-lookup"><span data-stu-id="e715c-116">In hello preceding example, a dependency is included on hello resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="e715c-117">例如，請參閱 [在 Azure 資源管理員中建立多個資源的執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="e715c-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="e715c-118">當定義相依性，您可以加入 hello 資源提供者命名空間和資源類型 tooavoid 模稜兩可。</span><span class="sxs-lookup"><span data-stu-id="e715c-118">When defining dependencies, you can include hello resource provider namespace and resource type tooavoid ambiguity.</span></span> <span data-ttu-id="e715c-119">例如，tooclarify 負載平衡器和虛擬網路，可能會有相同名稱與其他資源，使用下列的 hello hello 格式：</span><span class="sxs-lookup"><span data-stu-id="e715c-119">For example, tooclarify a load balancer and virtual network that may have hello same names as other resources, use hello following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="e715c-120">雖然您的資源之間可以想的 toouse dependsOn toomap 關聯性，是為什麼您所做的重要 toounderstand。</span><span class="sxs-lookup"><span data-stu-id="e715c-120">While you may be inclined toouse dependsOn toomap relationships between your resources, it's important toounderstand why you're doing it.</span></span> <span data-ttu-id="e715c-121">Toodocument 資源互連的方式，例如 dependsOn 不 hello 正確的方法。</span><span class="sxs-lookup"><span data-stu-id="e715c-121">For example, toodocument how resources are interconnected, dependsOn is not hello right approach.</span></span> <span data-ttu-id="e715c-122">您無法查詢哪些資源 hello dependsOn 元素中定義部署後。</span><span class="sxs-lookup"><span data-stu-id="e715c-122">You cannot query which resources were defined in hello dependsOn element after deployment.</span></span> <span data-ttu-id="e715c-123">使用 dependsOn 可能會影響部署時間，因為 Resource Manager 不會平行部署具有相依性的兩個資源。</span><span class="sxs-lookup"><span data-stu-id="e715c-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="e715c-124">toodocument 資源之間的關聯性改用[連結資源](/rest/api/resources/resourcelinks)。</span><span class="sxs-lookup"><span data-stu-id="e715c-124">toodocument relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="e715c-125">子資源</span><span class="sxs-lookup"><span data-stu-id="e715c-125">Child resources</span></span>
<span data-ttu-id="e715c-126">hello 資源屬性可讓您正在定義的相關的 toohello 資源的 toospecify 子資源。</span><span class="sxs-lookup"><span data-stu-id="e715c-126">hello resources property allows you toospecify child resources that are related toohello resource being defined.</span></span> <span data-ttu-id="e715c-127">定義子資源時，深度只能有 5 層。</span><span class="sxs-lookup"><span data-stu-id="e715c-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="e715c-128">請務必子資源與 hello 父資源之間建立 toonote 不是隱含的相依性。</span><span class="sxs-lookup"><span data-stu-id="e715c-128">It is important toonote that an implicit dependency is not created between a child resource and hello parent resource.</span></span> <span data-ttu-id="e715c-129">如果您需要 hello 子資源 toobe 部署 hello 父資源之後，您必須明確 hello dependsOn 屬性與該相依性。</span><span class="sxs-lookup"><span data-stu-id="e715c-129">If you need hello child resource toobe deployed after hello parent resource, you must explicitly state that dependency with hello dependsOn property.</span></span> 

<span data-ttu-id="e715c-130">每個父資源只接受特定的資源類型做為子資源。</span><span class="sxs-lookup"><span data-stu-id="e715c-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="e715c-131">hello 接受 hello 中指定的資源類型[範本結構描述](https://github.com/Azure/azure-resource-manager-schemas)的 hello 父資源。</span><span class="sxs-lookup"><span data-stu-id="e715c-131">hello accepted resource types are specified in hello [template schema](https://github.com/Azure/azure-resource-manager-schemas) of hello parent resource.</span></span> <span data-ttu-id="e715c-132">hello 子資源類型名稱包含 hello 型別的名稱 hello 父資源，例如**Microsoft.Web/sites/config**和**Microsoft.Web/sites/extensions**這兩個的子資源 hello **Microsoft.Web/sites**。</span><span class="sxs-lookup"><span data-stu-id="e715c-132">hello name of child resource type includes hello name of hello parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of hello **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="e715c-133">hello 下列範例會顯示 SQL server 和 SQL database。</span><span class="sxs-lookup"><span data-stu-id="e715c-133">hello following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="e715c-134">即使 hello 資料庫 hello 伺服器的子系，請注意 hello SQL database 與 SQL server 之間的已定義明確的相依性。</span><span class="sxs-lookup"><span data-stu-id="e715c-134">Notice that an explicit dependency is defined between hello SQL database and SQL server, even though hello database is a child of hello server.</span></span>

```json
"resources": [
  {
    "name": "[variables('sqlserverName')]",
    "type": "Microsoft.Sql/servers",
    "location": "[resourceGroup().location]",
    "tags": {
      "displayName": "SqlServer"
    },
    "apiVersion": "2014-04-01-preview",
    "properties": {
      "administratorLogin": "[parameters('administratorLogin')]",
      "administratorLoginPassword": "[parameters('administratorLoginPassword')]"
    },
    "resources": [
      {
        "name": "[parameters('databaseName')]",
        "type": "databases",
        "location": "[resourceGroup().location]",
        "tags": {
          "displayName": "Database"
        },
        "apiVersion": "2014-04-01-preview",
        "dependsOn": [
          "[variables('sqlserverName')]"
        ],
        "properties": {
          "edition": "[parameters('edition')]",
          "collation": "[parameters('collation')]",
          "maxSizeBytes": "[parameters('maxSizeBytes')]",
          "requestedServiceObjectiveName": "[parameters('requestedServiceObjectiveName')]"
        }
      }
    ]
  }
]
```

## <a name="reference-function"></a><span data-ttu-id="e715c-135">reference 函式</span><span class="sxs-lookup"><span data-stu-id="e715c-135">reference function</span></span>
<span data-ttu-id="e715c-136">hello[參考函式](resource-group-template-functions-resource.md#reference)可讓運算式 tooderive 它從其他的 JSON 名稱 / 值組或執行階段資源的值。</span><span class="sxs-lookup"><span data-stu-id="e715c-136">hello [reference function](resource-group-template-functions-resource.md#reference) enables an expression tooderive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="e715c-137">reference 運算式會隱含地宣告某個資源相依於另一個資源。</span><span class="sxs-lookup"><span data-stu-id="e715c-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="e715c-138">hello 一般格式為：</span><span class="sxs-lookup"><span data-stu-id="e715c-138">hello general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="e715c-139">在下列範例的 hello，CDN 端點明確相依於 hello 的 CDN 設定檔，並以隱含方式取決於 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e715c-139">In hello following example, a CDN endpoint explicitly depends on hello CDN profile, and implicitly depends on a web app.</span></span>

```json
{
    "name": "[variables('endpointName')]",
    "type": "endpoints",
    "location": "[resourceGroup().location]",
    "apiVersion": "2016-04-02",
    "dependsOn": [
            "[variables('profileName')]"
    ],
    "properties": {
        "originHostHeader": "[reference(variables('webAppName')).hostNames[0]]",
        ...
    }
```

<span data-ttu-id="e715c-140">您可以使用這個項目 」 或 「 hello dependsOn 元素 toospecify 相依性，但是您不需要這兩個 toouse hello 相同的相依資源。</span><span class="sxs-lookup"><span data-stu-id="e715c-140">You can use either this element or hello dependsOn element toospecify dependencies, but you do not need toouse both for hello same dependent resource.</span></span> <span data-ttu-id="e715c-141">可能的話，請使用 加入不必要的相依性的隱含參考 tooavoid。</span><span class="sxs-lookup"><span data-stu-id="e715c-141">Whenever possible, use an implicit reference tooavoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="e715c-142">詳細資訊，請參閱 toolearn[參考函式](resource-group-template-functions-resource.md#reference)。</span><span class="sxs-lookup"><span data-stu-id="e715c-142">toolearn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="e715c-143">設定相依性的建議</span><span class="sxs-lookup"><span data-stu-id="e715c-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="e715c-144">在決定哪些相依性 tooset 時，使用下列指導方針的 hello:</span><span class="sxs-lookup"><span data-stu-id="e715c-144">When deciding what dependencies tooset, use hello following guidelines:</span></span>

* <span data-ttu-id="e715c-145">設定越少相依性越好。</span><span class="sxs-lookup"><span data-stu-id="e715c-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="e715c-146">設定子資源為相依於其父資源。</span><span class="sxs-lookup"><span data-stu-id="e715c-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="e715c-147">使用 hello**參考**函式之間需要 tooshare 屬性資源 tooset 隱含的相依性。</span><span class="sxs-lookup"><span data-stu-id="e715c-147">Use hello **reference** function tooset implicit dependencies between resources that need tooshare a property.</span></span> <span data-ttu-id="e715c-148">當您已經定義隱含的相依性時，不要新增明確的相依性 (**dependsOn**)。</span><span class="sxs-lookup"><span data-stu-id="e715c-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="e715c-149">這種方法可減少 hello 風險不必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="e715c-149">This approach reduces hello risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="e715c-150">當資源必須有另一個資源的功能才能**建立**時，請設定相依性。</span><span class="sxs-lookup"><span data-stu-id="e715c-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="e715c-151">如果在部署之後只能互動 hello 資源未設定相依性。</span><span class="sxs-lookup"><span data-stu-id="e715c-151">Do not set a dependency if hello resources only interact after deployment.</span></span>
* <span data-ttu-id="e715c-152">讓相依性重疊顯示，而不需要明確設定它們。</span><span class="sxs-lookup"><span data-stu-id="e715c-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="e715c-153">例如，在虛擬網路介面，取決於您的虛擬機器和 hello 虛擬網路介面取決於虛擬網路與公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="e715c-153">For example, your virtual machine depends on a virtual network interface, and hello virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="e715c-154">因此，hello 虛擬機器是部署在所有三個資源，但未明確設定 hello 虛擬機器做為相依於所有的三個資源。</span><span class="sxs-lookup"><span data-stu-id="e715c-154">Therefore, hello virtual machine is deployed after all three resources, but do not explicitly set hello virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="e715c-155">此方法將釐清 hello 相依性順序並讓它更容易 toochange hello 範本稍後。</span><span class="sxs-lookup"><span data-stu-id="e715c-155">This approach clarifies hello dependency order and makes it easier toochange hello template later.</span></span>
* <span data-ttu-id="e715c-156">如果值無法決定部署之前，請嘗試部署 hello 資源，而不相依。</span><span class="sxs-lookup"><span data-stu-id="e715c-156">If a value can be determined before deployment, try deploying hello resource without a dependency.</span></span> <span data-ttu-id="e715c-157">例如，如果設定值需要 hello 名稱的另一個資源，您可能不需要相依性。</span><span class="sxs-lookup"><span data-stu-id="e715c-157">For example, if a configuration value needs hello name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="e715c-158">本指南不會永遠運作，因為某些資源確認 hello hello 存在其他資源。</span><span class="sxs-lookup"><span data-stu-id="e715c-158">This guidance does not always work because some resources verify hello existence of hello other resource.</span></span> <span data-ttu-id="e715c-159">如果您收到錯誤，請加入相依性。</span><span class="sxs-lookup"><span data-stu-id="e715c-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="e715c-160">Resource Manager 範本會在驗證期間識別循環相依性。</span><span class="sxs-lookup"><span data-stu-id="e715c-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="e715c-161">如果您收到錯誤訊息指出循環相依性存在時，評估範本 toosee，如果不需要任何相依性，而且可以移除。</span><span class="sxs-lookup"><span data-stu-id="e715c-161">If you receive an error stating that a circular dependency exists, evaluate your template toosee if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="e715c-162">如果移除相依性無法運作，您可以避免循環相依性，將某些部署作業移到部署後 hello 循環相依性的 「 hello 」 資源的子資源。</span><span class="sxs-lookup"><span data-stu-id="e715c-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after hello resources that have hello circular dependency.</span></span> <span data-ttu-id="e715c-163">例如，假設您要部署兩部虛擬機器，但您必須設定，請參閱 toohello 其他每一個屬性。</span><span class="sxs-lookup"><span data-stu-id="e715c-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer toohello other.</span></span> <span data-ttu-id="e715c-164">您可以將它們部署在 hello 順序：</span><span class="sxs-lookup"><span data-stu-id="e715c-164">You can deploy them in hello following order:</span></span>

1. <span data-ttu-id="e715c-165">vm1</span><span class="sxs-lookup"><span data-stu-id="e715c-165">vm1</span></span>
2. <span data-ttu-id="e715c-166">vm2</span><span class="sxs-lookup"><span data-stu-id="e715c-166">vm2</span></span>
3. <span data-ttu-id="e715c-167">vm1 的擴充相依於 vm1 和 vm2。</span><span class="sxs-lookup"><span data-stu-id="e715c-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="e715c-168">hello 延伸模組設定 vm1 它 vm2 從取得的值。</span><span class="sxs-lookup"><span data-stu-id="e715c-168">hello extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="e715c-169">vm2 的擴充相依於 vm1 和 vm2。</span><span class="sxs-lookup"><span data-stu-id="e715c-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="e715c-170">hello 延伸模組設定 vm2 它 vm1 從取得的值。</span><span class="sxs-lookup"><span data-stu-id="e715c-170">hello extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="e715c-171">評估 hello 部署順序及解決相依性錯誤的相關資訊，請參閱[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="e715c-171">For information about assessing hello deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="e715c-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e715c-172">Next steps</span></span>
* <span data-ttu-id="e715c-173">toolearn 有關疑難排解的相依性，在部署期間，請參閱[疑難排解常見的 Azure 部署錯誤與 Azure 資源管理員](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="e715c-173">toolearn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="e715c-174">toolearn 有關建立 Azure 資源管理員範本，請參閱[撰寫樣板](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="e715c-174">toolearn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="e715c-175">如需在範本中的 hello 可用函數的清單，請參閱[樣板函式](resource-group-template-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="e715c-175">For a list of hello available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

