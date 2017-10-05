---
title: "設定 Azure 資源的部署順序 | Microsoft Docs"
description: "說明如何在部署期間，將某個資源設定為相依於另一個資源，確保以正確的順序部署資源。"
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
ms.openlocfilehash: 3d6a46116ae9d7d940bc10dfa832540f42c0af7e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="define-the-order-for-deploying-resources-in-azure-resource-manager-templates"></a><span data-ttu-id="13e94-103">定義 Azure Resource Manager 範本中部署資源的順序</span><span class="sxs-lookup"><span data-stu-id="13e94-103">Define the order for deploying resources in Azure Resource Manager templates</span></span>
<span data-ttu-id="13e94-104">針對指定的資源，可能會有部署資源之前必須存在的其他資源。</span><span class="sxs-lookup"><span data-stu-id="13e94-104">For a given resource, there can be other resources that must exist before the resource is deployed.</span></span> <span data-ttu-id="13e94-105">例如，SQL Server 必須存在，才能嘗試部署 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="13e94-105">For example, a SQL server must exist before attempting to deploy a SQL database.</span></span> <span data-ttu-id="13e94-106">您可以將一個資源標示為相依於其他資源，來定義此關聯性。</span><span class="sxs-lookup"><span data-stu-id="13e94-106">You define this relationship by marking one resource as dependent on the other resource.</span></span> <span data-ttu-id="13e94-107">您可以使用 **dependsOn** 元素或使用 **reference** 函式定義相依性。</span><span class="sxs-lookup"><span data-stu-id="13e94-107">You define a dependency with the **dependsOn** element, or by using the **reference** function.</span></span> 

<span data-ttu-id="13e94-108">資源管理員會評估資源之間的相依性，並依其相依順序進行部署。</span><span class="sxs-lookup"><span data-stu-id="13e94-108">Resource Manager evaluates the dependencies between resources, and deploys them in their dependent order.</span></span> <span data-ttu-id="13e94-109">資源若不互相依賴，資源管理員就會平行部署資源。</span><span class="sxs-lookup"><span data-stu-id="13e94-109">When resources are not dependent on each other, Resource Manager deploys them in parallel.</span></span> <span data-ttu-id="13e94-110">您只需要針對部署在相同範本中的資源定義相依性。</span><span class="sxs-lookup"><span data-stu-id="13e94-110">You only need to define dependencies for resources that are deployed in the same template.</span></span> 

## <a name="dependson"></a><span data-ttu-id="13e94-111">dependsOn</span><span class="sxs-lookup"><span data-stu-id="13e94-111">dependsOn</span></span>
<span data-ttu-id="13e94-112">在您的範本內，dependsOn 元素可讓您定義一個資源作為一或多個資源的相依項目。</span><span class="sxs-lookup"><span data-stu-id="13e94-112">Within your template, the dependsOn element enables you to define one resource as a dependent on one or more resources.</span></span> <span data-ttu-id="13e94-113">其值可以是以逗號分隔的資源名稱清單。</span><span class="sxs-lookup"><span data-stu-id="13e94-113">Its value can be a comma-separated list of resource names.</span></span> 

<span data-ttu-id="13e94-114">下列範例示範一個虛擬機器擴展集，此擴展集依存於負載平衡器、虛擬網路，以及會建立多個儲存體帳戶的迴圈。</span><span class="sxs-lookup"><span data-stu-id="13e94-114">The following example shows a virtual machine scale set that depends on a load balancer, virtual network, and a loop that creates multiple storage accounts.</span></span> <span data-ttu-id="13e94-115">這些其他資源不會顯示在下列範例中，但是必須存在於範本中其他的位置。</span><span class="sxs-lookup"><span data-stu-id="13e94-115">These other resources are not shown in the following example, but they would need to exist elsewhere in the template.</span></span>

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

<span data-ttu-id="13e94-116">在上述範例中，相依性是包含在透過名為 **storageLoop**複製迴圈所建立的資源上。</span><span class="sxs-lookup"><span data-stu-id="13e94-116">In the preceding example, a dependency is included on the resources that are created through a copy loop named **storageLoop**.</span></span> <span data-ttu-id="13e94-117">例如，請參閱 [在 Azure 資源管理員中建立多個資源的執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="13e94-117">For an example, see [Create multiple instances of resources in Azure Resource Manager](resource-group-create-multiple.md).</span></span>

<span data-ttu-id="13e94-118">當定義相依性時，您可以包含資源提供者命名空間和資源類型，以避免模稜兩可。</span><span class="sxs-lookup"><span data-stu-id="13e94-118">When defining dependencies, you can include the resource provider namespace and resource type to avoid ambiguity.</span></span> <span data-ttu-id="13e94-119">比方說，若要釐清可能有和其他資源名稱相同的負載平衡器和虛擬網路，請使用下列格式：</span><span class="sxs-lookup"><span data-stu-id="13e94-119">For example, to clarify a load balancer and virtual network that may have the same names as other resources, use the following format:</span></span>

```json
"dependsOn": [
  "[concat('Microsoft.Network/loadBalancers/', variables('loadBalancerName'))]",
  "[concat('Microsoft.Network/virtualNetworks/', variables('virtualNetworkName'))]"
]
``` 

<span data-ttu-id="13e94-120">雖然您可能比較傾向於使用 dependsOn 來對應資源之間的關聯性，但是請務必了解為什麼您要這麼做。</span><span class="sxs-lookup"><span data-stu-id="13e94-120">While you may be inclined to use dependsOn to map relationships between your resources, it's important to understand why you're doing it.</span></span> <span data-ttu-id="13e94-121">例如，若是要記載資源互連的方式，dependsOn 並不是適當的方法。</span><span class="sxs-lookup"><span data-stu-id="13e94-121">For example, to document how resources are interconnected, dependsOn is not the right approach.</span></span> <span data-ttu-id="13e94-122">在部署之後，您便無法查詢 dependsOn 元素中定義了哪些資源。</span><span class="sxs-lookup"><span data-stu-id="13e94-122">You cannot query which resources were defined in the dependsOn element after deployment.</span></span> <span data-ttu-id="13e94-123">使用 dependsOn 可能會影響部署時間，因為 Resource Manager 不會平行部署具有相依性的兩個資源。</span><span class="sxs-lookup"><span data-stu-id="13e94-123">By using dependsOn, you potentially impact deployment time because Resource Manager does not deploy in parallel two resources that have a dependency.</span></span> <span data-ttu-id="13e94-124">若要記載資源之間的關聯性，請改用 [資源連結](/rest/api/resources/resourcelinks)。</span><span class="sxs-lookup"><span data-stu-id="13e94-124">To document relationships between resources, instead use [resource linking](/rest/api/resources/resourcelinks).</span></span>

## <a name="child-resources"></a><span data-ttu-id="13e94-125">子資源</span><span class="sxs-lookup"><span data-stu-id="13e94-125">Child resources</span></span>
<span data-ttu-id="13e94-126">resources 屬性可讓您指定與所定義的資源相關的子資源。</span><span class="sxs-lookup"><span data-stu-id="13e94-126">The resources property allows you to specify child resources that are related to the resource being defined.</span></span> <span data-ttu-id="13e94-127">定義子資源時，深度只能有 5 層。</span><span class="sxs-lookup"><span data-stu-id="13e94-127">Child resources can only be defined five levels deep.</span></span> <span data-ttu-id="13e94-128">請務必注意，在子資源與父資源之間並不會建立隱含的相依性。</span><span class="sxs-lookup"><span data-stu-id="13e94-128">It is important to note that an implicit dependency is not created between a child resource and the parent resource.</span></span> <span data-ttu-id="13e94-129">如果您需要在父資源之後部署子資源，您必須使用 dependsOn 屬性明確地敘述該相依性。</span><span class="sxs-lookup"><span data-stu-id="13e94-129">If you need the child resource to be deployed after the parent resource, you must explicitly state that dependency with the dependsOn property.</span></span> 

<span data-ttu-id="13e94-130">每個父資源只接受特定的資源類型做為子資源。</span><span class="sxs-lookup"><span data-stu-id="13e94-130">Each parent resource accepts only certain resource types as child resources.</span></span> <span data-ttu-id="13e94-131">可接受的資源類型是在父資源的 [範本結構描述](https://github.com/Azure/azure-resource-manager-schemas) 中指定。</span><span class="sxs-lookup"><span data-stu-id="13e94-131">The accepted resource types are specified in the [template schema](https://github.com/Azure/azure-resource-manager-schemas) of the parent resource.</span></span> <span data-ttu-id="13e94-132">子資源類型的名稱包含父資源類型的名稱，例如 **Microsoft.Web/sites/config** 和 **Microsoft.Web/sites/extensions** 兩者皆為 **Microsoft.Web/sites** 的子資源。</span><span class="sxs-lookup"><span data-stu-id="13e94-132">The name of child resource type includes the name of the parent resource type, such as **Microsoft.Web/sites/config** and **Microsoft.Web/sites/extensions** are both child resources of the **Microsoft.Web/sites**.</span></span>

<span data-ttu-id="13e94-133">下列範例示範 SQL 伺服器和 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="13e94-133">The following example shows a SQL server and SQL database.</span></span> <span data-ttu-id="13e94-134">請注意，SQL 資料庫與 SQL 伺服器之間定義明確相依性，即使資料庫是伺服器的子系也是一樣。</span><span class="sxs-lookup"><span data-stu-id="13e94-134">Notice that an explicit dependency is defined between the SQL database and SQL server, even though the database is a child of the server.</span></span>

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

## <a name="reference-function"></a><span data-ttu-id="13e94-135">reference 函式</span><span class="sxs-lookup"><span data-stu-id="13e94-135">reference function</span></span>
<span data-ttu-id="13e94-136">[reference 函式](resource-group-template-functions-resource.md#reference) 可讓運算式從其他 JSON 名稱和值組或執行階段資源衍生其值。</span><span class="sxs-lookup"><span data-stu-id="13e94-136">The [reference function](resource-group-template-functions-resource.md#reference) enables an expression to derive its value from other JSON name and value pairs or runtime resources.</span></span> <span data-ttu-id="13e94-137">reference 運算式會隱含地宣告某個資源相依於另一個資源。</span><span class="sxs-lookup"><span data-stu-id="13e94-137">Reference expressions implicitly declare that one resource depends on another.</span></span> <span data-ttu-id="13e94-138">一般的格式如下︰</span><span class="sxs-lookup"><span data-stu-id="13e94-138">The general format is:</span></span>

```json
reference('resourceName').propertyPath
```

<span data-ttu-id="13e94-139">在下列範例中，CDN 端點明確相依於 CDN 設定檔，並隱含相依於 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="13e94-139">In the following example, a CDN endpoint explicitly depends on the CDN profile, and implicitly depends on a web app.</span></span>

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

<span data-ttu-id="13e94-140">您可以使用此元素或 dependsOn 元素指定相依性，但是您不需要針對相同的相依資源使用兩者。</span><span class="sxs-lookup"><span data-stu-id="13e94-140">You can use either this element or the dependsOn element to specify dependencies, but you do not need to use both for the same dependent resource.</span></span> <span data-ttu-id="13e94-141">請盡可能使用隱含的參考，以避免新增不必要的相依性。</span><span class="sxs-lookup"><span data-stu-id="13e94-141">Whenever possible, use an implicit reference to avoid adding an unnecessary dependency.</span></span>

<span data-ttu-id="13e94-142">若要深入了解，請參閱 [reference 函數](resource-group-template-functions-resource.md#reference)。</span><span class="sxs-lookup"><span data-stu-id="13e94-142">To learn more, see [reference function](resource-group-template-functions-resource.md#reference).</span></span>

## <a name="recommendations-for-setting-dependencies"></a><span data-ttu-id="13e94-143">設定相依性的建議</span><span class="sxs-lookup"><span data-stu-id="13e94-143">Recommendations for setting dependencies</span></span>

<span data-ttu-id="13e94-144">決定設定哪種相依性時，請使用下列指導方針︰</span><span class="sxs-lookup"><span data-stu-id="13e94-144">When deciding what dependencies to set, use the following guidelines:</span></span>

* <span data-ttu-id="13e94-145">設定越少相依性越好。</span><span class="sxs-lookup"><span data-stu-id="13e94-145">Set as few dependencies as possible.</span></span>
* <span data-ttu-id="13e94-146">設定子資源為相依於其父資源。</span><span class="sxs-lookup"><span data-stu-id="13e94-146">Set a child resource as dependent on its parent resource.</span></span>
* <span data-ttu-id="13e94-147">使用 **reference** 函式以設定必須共用屬性的資源之間的隱含相依性。</span><span class="sxs-lookup"><span data-stu-id="13e94-147">Use the **reference** function to set implicit dependencies between resources that need to share a property.</span></span> <span data-ttu-id="13e94-148">當您已經定義隱含的相依性時，不要新增明確的相依性 (**dependsOn**)。</span><span class="sxs-lookup"><span data-stu-id="13e94-148">Do not add an explicit dependency (**dependsOn**) when you have already defined an implicit dependency.</span></span> <span data-ttu-id="13e94-149">這種方法可減少產生不必要相依性的風險。</span><span class="sxs-lookup"><span data-stu-id="13e94-149">This approach reduces the risk of having unnecessary dependencies.</span></span> 
* <span data-ttu-id="13e94-150">當資源必須有另一個資源的功能才能**建立**時，請設定相依性。</span><span class="sxs-lookup"><span data-stu-id="13e94-150">Set a dependency when a resource cannot be **created** without functionality from another resource.</span></span> <span data-ttu-id="13e94-151">如果資源只在部署之後互動，請勿設定相依性。</span><span class="sxs-lookup"><span data-stu-id="13e94-151">Do not set a dependency if the resources only interact after deployment.</span></span>
* <span data-ttu-id="13e94-152">讓相依性重疊顯示，而不需要明確設定它們。</span><span class="sxs-lookup"><span data-stu-id="13e94-152">Let dependencies cascade without setting them explicitly.</span></span> <span data-ttu-id="13e94-153">例如，您的虛擬機器相依於虛擬網路介面，而虛擬網路介面相依於虛擬網路和公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="13e94-153">For example, your virtual machine depends on a virtual network interface, and the virtual network interface depends on a virtual network and public IP addresses.</span></span> <span data-ttu-id="13e94-154">因此，會在所有三個資源之後部署虛擬機器，但沒有明確設定虛擬機器為相依於所有三個資源。</span><span class="sxs-lookup"><span data-stu-id="13e94-154">Therefore, the virtual machine is deployed after all three resources, but do not explicitly set the virtual machine as dependent on all three resources.</span></span> <span data-ttu-id="13e94-155">這種方法可釐清相依性順序，而且稍後可以比較容易變更範本。</span><span class="sxs-lookup"><span data-stu-id="13e94-155">This approach clarifies the dependency order and makes it easier to change the template later.</span></span>
* <span data-ttu-id="13e94-156">如果部署之前可以決定值，請嘗試部署沒有相依性的資源。</span><span class="sxs-lookup"><span data-stu-id="13e94-156">If a value can be determined before deployment, try deploying the resource without a dependency.</span></span> <span data-ttu-id="13e94-157">例如，如果設定值需要另一個資源的名稱，您可能就不需要相依性。</span><span class="sxs-lookup"><span data-stu-id="13e94-157">For example, if a configuration value needs the name of another resource, you might not need a dependency.</span></span> <span data-ttu-id="13e94-158">本指引不會永遠有效，因為某些資源會確認其他資源是否存在。</span><span class="sxs-lookup"><span data-stu-id="13e94-158">This guidance does not always work because some resources verify the existence of the other resource.</span></span> <span data-ttu-id="13e94-159">如果您收到錯誤，請加入相依性。</span><span class="sxs-lookup"><span data-stu-id="13e94-159">If you receive an error, add a dependency.</span></span> 

<span data-ttu-id="13e94-160">Resource Manager 範本會在驗證期間識別循環相依性。</span><span class="sxs-lookup"><span data-stu-id="13e94-160">Resource Manager identifies circular dependencies during template validation.</span></span> <span data-ttu-id="13e94-161">如果您收到錯誤表示循環相依性存在時，請評估您的範本以查看是否有任何不需要的相依性可以移除。</span><span class="sxs-lookup"><span data-stu-id="13e94-161">If you receive an error stating that a circular dependency exists, evaluate your template to see if any dependencies are not needed and can be removed.</span></span> <span data-ttu-id="13e94-162">如果移除相依性沒有用，可以將某些部署作業移到在有循環相依性的資源之後部署的子資源中，以避免循環相依性。</span><span class="sxs-lookup"><span data-stu-id="13e94-162">If removing dependencies does not work, you can avoid circular dependencies by moving some deployment operations into child resources that are deployed after the resources that have the circular dependency.</span></span> <span data-ttu-id="13e94-163">例如，假設您要部署兩部虛擬機器，但是您必須分別在上面設定互相參考的屬性。</span><span class="sxs-lookup"><span data-stu-id="13e94-163">For example, suppose you are deploying two virtual machines but you must set properties on each one that refer to the other.</span></span> <span data-ttu-id="13e94-164">您可以採取下列順序部署︰</span><span class="sxs-lookup"><span data-stu-id="13e94-164">You can deploy them in the following order:</span></span>

1. <span data-ttu-id="13e94-165">vm1</span><span class="sxs-lookup"><span data-stu-id="13e94-165">vm1</span></span>
2. <span data-ttu-id="13e94-166">vm2</span><span class="sxs-lookup"><span data-stu-id="13e94-166">vm2</span></span>
3. <span data-ttu-id="13e94-167">vm1 的擴充相依於 vm1 和 vm2。</span><span class="sxs-lookup"><span data-stu-id="13e94-167">Extension on vm1 depends on vm1 and vm2.</span></span> <span data-ttu-id="13e94-168">擴充在 vm1 上設定從 vm2 取得的值。</span><span class="sxs-lookup"><span data-stu-id="13e94-168">The extension sets values on vm1 that it gets from vm2.</span></span>
4. <span data-ttu-id="13e94-169">vm2 的擴充相依於 vm1 和 vm2。</span><span class="sxs-lookup"><span data-stu-id="13e94-169">Extension on vm2 depends on vm1 and vm2.</span></span> <span data-ttu-id="13e94-170">擴充在 vm2 上設定從 vm1 取得的值。</span><span class="sxs-lookup"><span data-stu-id="13e94-170">The extension sets values on vm2 that it gets from vm1.</span></span>

<span data-ttu-id="13e94-171">如需評估部署順序及解決相依性錯誤的相關資訊，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="13e94-171">For information about assessing the deployment order and resolving dependency errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="13e94-172">後續步驟</span><span class="sxs-lookup"><span data-stu-id="13e94-172">Next steps</span></span>
* <span data-ttu-id="13e94-173">若要了解在部署期間如何對相依性進行疑難排解，請參閱[使用 Azure Resource Manager 針對常見的 Azure 部署錯誤進行疑難排解](resource-manager-common-deployment-errors.md)。</span><span class="sxs-lookup"><span data-stu-id="13e94-173">To learn about troubleshooting dependencies during deployment, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="13e94-174">若要了解如何建立 Azure 資源管理員範本，請參閱 [撰寫範本](resource-group-authoring-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="13e94-174">To learn about creating Azure Resource Manager templates, see [Authoring templates](resource-group-authoring-templates.md).</span></span> 
* <span data-ttu-id="13e94-175">如需在範本中可用函式的清單，請參閱 [範本函式](resource-group-template-functions.md)。</span><span class="sxs-lookup"><span data-stu-id="13e94-175">For a list of the available functions in a template, see [Template functions](resource-group-template-functions.md).</span></span>

