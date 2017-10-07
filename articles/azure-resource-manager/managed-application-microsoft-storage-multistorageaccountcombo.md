---
title: "aaaAzure 受管理的應用程式 MultiStorageAccountCombo UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Storage.MultiStorageAccountCombo UI 項目"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: reference
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/12/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: 765be145b61c3dbf0a035a7a00aa18eee464a3eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragemultistorageaccountcombo-ui-element"></a><span data-ttu-id="5d7e9-103">Microsoft.Storage.MultiStorageAccountCombo UI 元素</span><span class="sxs-lookup"><span data-stu-id="5d7e9-103">Microsoft.Storage.MultiStorageAccountCombo UI element</span></span>
<span data-ttu-id="5d7e9-104">用來建立名稱以通用前置詞作為開頭的多個儲存體帳戶之控制項群組。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-104">A group of controls for creating multiple storage accounts, with names that start with a common prefix.</span></span> <span data-ttu-id="5d7e9-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="5d7e9-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="5d7e9-106">UI sample</span></span>
![Microsoft.Storage.MultiStorageAccountCombo](./media/managed-application-elements/microsoft.storage.multistorageaccountcombo.png)

## <a name="schema"></a><span data-ttu-id="5d7e9-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="5d7e9-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.MultiStorageAccountCombo",
  "label": {
    "prefix": "Storage account prefix",
    "type": "Storage account type"
  },
  "toolTip": {
    "prefix": "",
    "type": ""
  },
  "defaultValue": {
    "prefix": "sa",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="5d7e9-109">備註</span><span class="sxs-lookup"><span data-stu-id="5d7e9-109">Remarks</span></span>
- <span data-ttu-id="5d7e9-110">hello 值`defaultValue.prefix`串連一或多個整數 toogenerate hello 序列的儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-110">hello value for `defaultValue.prefix` is concatenated with one or more integers toogenerate hello sequence of storage account names.</span></span> <span data-ttu-id="5d7e9-111">例如，如果 `defaultValue.prefix` 為 **foobar** 且 `count` 為 **2**，就會產生 **foobar1** 和 **foobar2** 儲存體帳戶名稱。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-111">For example, if `defaultValue.prefix` is **foobar** and `count` is **2**, then storage account names **foobar1** and **foobar2** are generated.</span></span> <span data-ttu-id="5d7e9-112">會自動驗證所產生儲存體帳戶名稱的唯一性。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-112">Generated storage account names are validated for uniqueness automatically.</span></span>
- <span data-ttu-id="5d7e9-113">hello 儲存體帳戶名稱產生辭典編纂順序根據`count`。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-113">hello storage account names are generated lexicographically based on `count`.</span></span> <span data-ttu-id="5d7e9-114">例如，如果`count`為 10、 則 hello 儲存體帳戶名稱的結尾 2 位數的整數 (01、 02、 03 中，等。)。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-114">For example, if `count` is 10, then hello storage account names end with 2-digit integers (01, 02, 03, etc.).</span></span>
- <span data-ttu-id="5d7e9-115">hello 預設值為`defaultValue.prefix`是**null**，以及`defaultValue.type`是**Premium_LRS**。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-115">hello default value for `defaultValue.prefix` is **null**, and for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="5d7e9-116">`constraints.allowedTypes` 中未指定的任何類型都會加以隱藏，`constraints.excludedTypes` 中未指定的任何類型都會加以顯示。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-116">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="5d7e9-117">`constraints.allowedTypes` 和 `constraints.excludedTypes` 都是選擇性的，但不能同時使用。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-117">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="5d7e9-118">在加法 toogenerating 儲存體帳戶名稱，`count`是使用的 tooset hello 項目的適當的乘數。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-118">In addition toogenerating storage account names, `count` is used tooset the appropriate multiplier for hello element.</span></span> <span data-ttu-id="5d7e9-119">它支援靜態值 (例如 **2**)，或者另一個元素的動態值 (例如 `[steps('step1').storageAccountCount]`)。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-119">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').storageAccountCount]`.</span></span> <span data-ttu-id="5d7e9-120">hello 預設值是**1**。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-120">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="5d7e9-121">範例輸出</span><span class="sxs-lookup"><span data-stu-id="5d7e9-121">Sample output</span></span>
```json
{
  "prefix": "sa",
  "count": 2,
  "resourceGroup": "rg01",
  "type": "Premium_LRS"
}
```

## <a name="next-steps"></a><span data-ttu-id="5d7e9-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d7e9-122">Next steps</span></span>
* <span data-ttu-id="5d7e9-123">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5d7e9-124">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="5d7e9-125">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="5d7e9-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
