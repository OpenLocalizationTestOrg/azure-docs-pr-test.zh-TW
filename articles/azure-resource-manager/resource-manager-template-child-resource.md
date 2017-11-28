---
title: "在 Azure 範本 aaaDefine 子資源 |Microsoft 文件"
description: "示範如何 tooset hello 資源類型和 Azure 資源管理員範本中的子資源的名稱"
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
ms.openlocfilehash: c502c589100d7ae864d7fb01b5ba10ddfaf92592
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-name-and-type-for-child-resource-in-resource-manager-template"></a><span data-ttu-id="6fa65-103">在 Resource Manager 範本中設定子資源的名稱和類型</span><span class="sxs-lookup"><span data-stu-id="6fa65-103">Set name and type for child resource in Resource Manager template</span></span>
<span data-ttu-id="6fa65-104">建立範本時，您經常需要 tooinclude 相關的 tooa 父資源的子資源。</span><span class="sxs-lookup"><span data-stu-id="6fa65-104">When creating a template, you frequently need tooinclude a child resource that is related tooa parent resource.</span></span> <span data-ttu-id="6fa65-105">例如，您的範本可能包含 SQL Server 和資料庫。</span><span class="sxs-lookup"><span data-stu-id="6fa65-105">For example, your template may include a SQL server and a database.</span></span> <span data-ttu-id="6fa65-106">hello SQL server，就是 「 hello 父資源，而且 hello 資料庫 hello 子資源。</span><span class="sxs-lookup"><span data-stu-id="6fa65-106">hello SQL server is hello parent resource, and hello database is hello child resource.</span></span> 

<span data-ttu-id="6fa65-107">hello hello 子資源類型的格式如下：`{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span><span class="sxs-lookup"><span data-stu-id="6fa65-107">hello format of hello child resource type is: `{resource-provider-namespace}/{parent-resource-type}/{child-resource-type}`</span></span>

<span data-ttu-id="6fa65-108">hello 的 hello 子資源名稱的格式如下：`{parent-resource-name}/{child-resource-name}`</span><span class="sxs-lookup"><span data-stu-id="6fa65-108">hello format of hello child resource name is: `{parent-resource-name}/{child-resource-name}`</span></span>

<span data-ttu-id="6fa65-109">不過，您可以指定 hello 類型和範本中的名稱以不同的方式根據它是否為巢狀方式內 hello 父資源，或它自己在 hello 高層級。</span><span class="sxs-lookup"><span data-stu-id="6fa65-109">However, you specify hello type and name in a template differently based on whether it is nested within hello parent resource, or on its own at hello top level.</span></span> <span data-ttu-id="6fa65-110">本主題說明如何 toohandle 這兩個方法。</span><span class="sxs-lookup"><span data-stu-id="6fa65-110">This topic shows how toohandle both approaches.</span></span>

<span data-ttu-id="6fa65-111">當建構完整的參考 tooa 資源，hello 順序 toocombine 區段從 hello 類型和名稱不是只需串連 hello 兩個。</span><span class="sxs-lookup"><span data-stu-id="6fa65-111">When constructing a fully qualified reference tooa resource, hello order toocombine segments from hello type and name  is not simply a concatenation of hello two.</span></span>  <span data-ttu-id="6fa65-112">相反地，在 hello 命名空間之後, 使用一連串的*類型/名稱*最不特定 toomost 特定配對：</span><span class="sxs-lookup"><span data-stu-id="6fa65-112">Instead, after hello namespace, use a sequence of *type/name* pairs from least specific toomost specific:</span></span>

```json
{resource-provider-namespace}/{parent-resource-type}/{parent-resource-name}[/{child-resource-type}/{child-resource-name}]*
```

<span data-ttu-id="6fa65-113">例如：</span><span class="sxs-lookup"><span data-stu-id="6fa65-113">For example:</span></span>

<span data-ttu-id="6fa65-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` 為正確 `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` 為不正確</span><span class="sxs-lookup"><span data-stu-id="6fa65-114">`Microsoft.Compute/virtualMachines/myVM/extensions/myExt` is correct `Microsoft.Compute/virtualMachines/extensions/myVM/myExt` is not correct</span></span>

## <a name="nested-child-resource"></a><span data-ttu-id="6fa65-115">巢狀子資源</span><span class="sxs-lookup"><span data-stu-id="6fa65-115">Nested child resource</span></span>
<span data-ttu-id="6fa65-116">最簡單方式 toodefine hello 子資源是 toonest 在 hello 父資源。</span><span class="sxs-lookup"><span data-stu-id="6fa65-116">hello easiest way toodefine a child resource is toonest it within hello parent resource.</span></span> <span data-ttu-id="6fa65-117">hello 下列範例顯示巢狀內，SQL Server 中的 SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="6fa65-117">hello following example shows a SQL database nested within in a SQL Server.</span></span>

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

<span data-ttu-id="6fa65-118">Hello 子資源，hello 類型設定太`databases`完整資源類型，而`Microsoft.Sql/servers/databases`。</span><span class="sxs-lookup"><span data-stu-id="6fa65-118">For hello child resource, hello type is set too`databases` but its full resource type is `Microsoft.Sql/servers/databases`.</span></span> <span data-ttu-id="6fa65-119">您未提供`Microsoft.Sql/servers/`因為它會假設來自 hello 父資源類型。</span><span class="sxs-lookup"><span data-stu-id="6fa65-119">You do not provide `Microsoft.Sql/servers/` because it is assumed from hello parent resource type.</span></span> <span data-ttu-id="6fa65-120">hello 子資源名稱設定得`exampledatabase`但 hello 完整名稱包括 hello 父系名稱。</span><span class="sxs-lookup"><span data-stu-id="6fa65-120">hello child resource name is set too`exampledatabase` but hello full name includes hello parent name.</span></span> <span data-ttu-id="6fa65-121">您未提供`exampleserver`因為它會假設從 hello 父資源。</span><span class="sxs-lookup"><span data-stu-id="6fa65-121">You do not provide `exampleserver` because it is assumed from hello parent resource.</span></span>

## <a name="top-level-child-resource"></a><span data-ttu-id="6fa65-122">最上層的子資源</span><span class="sxs-lookup"><span data-stu-id="6fa65-122">Top-level child resource</span></span>
<span data-ttu-id="6fa65-123">您可以定義在 hello 上層 hello 子資源。</span><span class="sxs-lookup"><span data-stu-id="6fa65-123">You can define hello child resource at hello top level.</span></span> <span data-ttu-id="6fa65-124">您可以使用這個方法，如果 hello 父資源未部署在 hello 相同的範本或如果想 toouse `copy` toocreate 子系的多個資源。</span><span class="sxs-lookup"><span data-stu-id="6fa65-124">You might use this approach if hello parent resource is not deployed in hello same template, or if want toouse `copy` toocreate multiple child resources.</span></span> <span data-ttu-id="6fa65-125">使用此方法時，您必須提供 hello 完整資源類型，而且 hello 父資源中包含 hello 子資源名稱。</span><span class="sxs-lookup"><span data-stu-id="6fa65-125">With this approach, you must provide hello full resource type, and include hello parent resource name in hello child resource name.</span></span>

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

<span data-ttu-id="6fa65-126">hello 資料庫是子資源 toohello 伺服器，即使它們在 hello hello 範本中相同層級上定義。</span><span class="sxs-lookup"><span data-stu-id="6fa65-126">hello database is a child resource toohello server even though they are defined on hello same level in hello template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6fa65-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6fa65-127">Next steps</span></span>
* <span data-ttu-id="6fa65-128">如需有關如何建議 toocreate 範本，請參閱[最佳作法來建立 Azure 資源管理員範本](resource-manager-template-best-practices.md)。</span><span class="sxs-lookup"><span data-stu-id="6fa65-128">For recommendations about how toocreate templates, see [Best practices for creating Azure Resource Manager templates](resource-manager-template-best-practices.md).</span></span>
* <span data-ttu-id="6fa65-129">如需建立多個子資源的範例，請參閱[在 Azure Resource Manager 範本中部署資源的多個執行個體](resource-group-create-multiple.md)。</span><span class="sxs-lookup"><span data-stu-id="6fa65-129">For an example of creating multiple child resources, see [Deploy multiple instances of resources in Azure Resource Manager templates](resource-group-create-multiple.md).</span></span>
