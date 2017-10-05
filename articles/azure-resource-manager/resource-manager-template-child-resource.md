---
title: "在 Azure 範本中定義子資源 | Microsoft Docs"
description: "示範如何在 Azure Resource Manager 範本中設定資源類型和子資源名稱"
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: tomfitz
ms.openlocfilehash: 5b6ce5526f354008eb4a697deec737876f22391f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="67f05-103">在 Resource Manager 範本中設定子資源的名稱和類型</span><span class="sxs-lookup"><span data-stu-id="67f05-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="67f05-104">建立範本時，您經常需要包含與父資源相關的子資源。</span><span class="sxs-lookup"><span data-stu-id="67f05-104">When creating a template, you frequently need to include a child resource that is related to a parent resource.</span></span> <span data-ttu-id="67f05-105">例如，您的範本可能包含 SQL Server 和資料庫。</span><span class="sxs-lookup"><span data-stu-id="67f05-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="67f05-106">SQL Server 是父系的資源，而資料庫則為子資源。</span><span class="sxs-lookup"><span data-stu-id="67f05-106">The SQL server is the parent resource, and the database is the child resource.</span></span> 

<span data-ttu-id="67f05-107">子資源類型的格式如下︰`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="67f05-107">The format of the child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="67f05-108">子資源名稱的格式如下︰`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="67f05-108">The format of the child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="67f05-109">不過，根據子資源是以巢狀方式內嵌於父資源中，還是本身位於最上層而定，您在範本中指定類型和名稱的方式會有所不同。</span><span class="sxs-lookup"><span data-stu-id="67f05-109">However, you specify the type and name in a template differently based on whether it is nested within the parent resource, or on its own at the top level.</span></span> <span data-ttu-id="67f05-110">本主題說明如何處理這兩種方式。</span><span class="sxs-lookup"><span data-stu-id="67f05-110">This topic shows how to handle both approaches.</span></span>

<span data-ttu-id="67f05-111">當建構資源的完整參考時，要從類型和名稱合併區段的順序並非只是將兩個串連。</span><span class="sxs-lookup"><span data-stu-id="67f05-111">When constructing a fully qualified reference to a resource, the order to combine segments from the type and name  is not simply a concatenation of the two.</span></span>  <span data-ttu-id="67f05-112">相反地，在命名空間之後，使用從最特定到最不特定的一連串*類型/名稱*組：</span><span class="sxs-lookup"><span data-stu-id="67f05-112">Instead, after the namespace, use a sequence of *type/name* pairs from least specific to most specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="67f05-113">例如：</span><span class="sxs-lookup"><span data-stu-id="67f05-113">For example:</span></span>

<span data-ttu-id="67f05-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` 為正確 `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` 為不正確</span><span class="sxs-lookup"><span data-stu-id="67f05-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="67f05-115">巢狀子資源</span><span class="sxs-lookup"><span data-stu-id="67f05-115">Nested child resource</span></span>
<span data-ttu-id="67f05-116">定義子資源的最簡單方式是將其以巢狀方式內嵌於父資源中。</span><span class="sxs-lookup"><span data-stu-id="67f05-116">The easiest way to define a child resource is to nest it within the parent resource.</span></span> <span data-ttu-id="67f05-117">下列範例顯示以巢狀方式內嵌於 SQL Server 中的 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="67f05-117">The following example shows a SQL database nested within in a SQL Server.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  ...
  "resources": [
    {
      "name": "exampledatabase",
      "type": "databases",
      "apiVersion": "2014-04-01",
      ...
    }
  ]
}
```

<span data-ttu-id="67f05-118">子資源的類型已設為 `databases`，但是其完整資源類型為 `Microsoft.Sql/servers/databases`。</span><span class="sxs-lookup"><span data-stu-id="67f05-118">For the child resource, the type is set to `databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="67f05-119">您未提供 `Microsoft.Sql/servers/`，因為它被認為是來自父資源類型。</span><span class="sxs-lookup"><span data-stu-id="67f05-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from the parent resource type.</span></span> <span data-ttu-id="67f05-120">子資源名稱會設為 `exampledatabase`，但是完整名稱包含父系名稱。</span><span class="sxs-lookup"><span data-stu-id="67f05-120">The child resource name is set to `exampledatabase` but the full name includes the parent name.</span></span> <span data-ttu-id="67f05-121">您未提供 `exampleserver`，因為它被認為是來自父資源。</span><span class="sxs-lookup"><span data-stu-id="67f05-121">You do not provide `exampleserver` because it is assumed from the parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="67f05-122">最上層的子資源</span><span class="sxs-lookup"><span data-stu-id="67f05-122">Top-level child resource</span></span>
<span data-ttu-id="67f05-123">您可以定義最上層的子資源。</span><span class="sxs-lookup"><span data-stu-id="67f05-123">You can define the child resource at the top level.</span></span> <span data-ttu-id="67f05-124">如果父資源並未部署在相同範本中，或者想要使用 `copy` 來建立多個子資源，您可以使用此方法。</span><span class="sxs-lookup"><span data-stu-id="67f05-124">You might use this approach if the parent resource is not deployed in the same template, or if want to use `copy` to create multiple child resources.</span></span> <span data-ttu-id="67f05-125">使用這個方法，您必須提供完整資源類型，並將父資源名稱納入子資源名稱中。</span><span class="sxs-lookup"><span data-stu-id="67f05-125">With this approach, you must provide the full resource type, and include the parent resource name in the child resource name.</span></span>

```json
{
  "name": "exampleserver",
  "type": "Microsoft.Sql/servers",
  "apiVersion": "2014-04-01",
  "resources": [ 
  ],
  ...
},
{
  "name": "exampleserver/exampledatabase",
  "type": "Microsoft.Sql/servers/databases",
  "apiVersion": "2014-04-01",
  ...
}
```

<span data-ttu-id="67f05-126">資料庫是伺服器的子資源，即使兩者都定義於範本中的相同層級上。</span><span class="sxs-lookup"><span data-stu-id="67f05-126">The database is a child resource to the server even though they are defined on the same level in the template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="67f05-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="67f05-127">Next steps</span></span>
* <span data-ttu-id="67f05-128">如需如何建立範本的建議，請參閱 [建立 Azure Resource Manager 範本的最佳做法](resource-manager-template-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="67f05-128">For recommendations about how to create templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="67f05-129">如需建立多個子資源的範例，請參閱[在 Azure Resource Manager 範本中部署資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="67f05-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
