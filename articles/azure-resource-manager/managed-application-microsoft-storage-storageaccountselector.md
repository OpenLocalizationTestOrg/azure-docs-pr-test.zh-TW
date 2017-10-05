---
title: "Azure 受管理的應用程式 StorageAccountSelector UI 元素 | Microsoft Docs"
description: "描述 Azure 受管理應用程式的 Microsoft.Storage.StorageAccountSelector UI 元素"
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
ms.openlocfilehash: 15e69c0deb4bce64b7413b557eb69db5165bde73
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="c0bba-103">Microsoft.Storage.StorageAccountSelector UI 元素</span><span class="sxs-lookup"><span data-stu-id="c0bba-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="c0bba-104">選取新的或現有儲存體帳戶的控制項。</span><span class="sxs-lookup"><span data-stu-id="c0bba-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="c0bba-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="c0bba-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="c0bba-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="c0bba-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="c0bba-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="c0bba-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Storage.StorageAccountSelector",
  "label": "Storage account",
  "toolTip": "",
  "defaultValue": {
    "name": "storageaccount01",
    "type": "Premium_LRS"
  },
  "constraints": {
    "allowedTypes": [],
    "excludedTypes": []
  },
  "options": {
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="c0bba-109">備註</span><span class="sxs-lookup"><span data-stu-id="c0bba-109">Remarks</span></span>
- <span data-ttu-id="c0bba-110">如果指定，就會自動驗證 `defaultValue.name` 的唯一性。</span><span class="sxs-lookup"><span data-stu-id="c0bba-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="c0bba-111">如果儲存體帳戶名稱不是唯一的，使用者就必須指定不同的名稱，或選擇現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c0bba-111">If the storage account name is not unique, the user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="c0bba-112">`defaultValue.type` 的預設值為 **Premium_LRS**。</span><span class="sxs-lookup"><span data-stu-id="c0bba-112">The default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="c0bba-113">`constraints.allowedTypes` 中未指定的任何類型都會加以隱藏，`constraints.excludedTypes` 中未指定的任何類型都會加以顯示。</span><span class="sxs-lookup"><span data-stu-id="c0bba-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="c0bba-114">`constraints.allowedTypes` 和 `constraints.excludedTypes` 都是選擇性的，但不能同時使用。</span><span class="sxs-lookup"><span data-stu-id="c0bba-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="c0bba-115">如果 `options.hideExisting` 為 **true**，使用者就無法選擇現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="c0bba-115">If `options.hideExisting` is **true**, the user can't choose an existing storage account.</span></span> <span data-ttu-id="c0bba-116">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="c0bba-116">The default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="c0bba-117">範例輸出</span><span class="sxs-lookup"><span data-stu-id="c0bba-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="c0bba-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c0bba-118">Next steps</span></span>
* <span data-ttu-id="c0bba-119">如需受管理應用程式的簡介，請參閱 [Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c0bba-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="c0bba-120">如需建立 UI 定義的簡介，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c0bba-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="c0bba-121">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="c0bba-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
