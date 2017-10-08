---
title: "aaaAzure 受管理的應用程式 StorageAccountSelector UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Storage.StorageAccountSelector UI 項目"
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
ms.openlocfilehash: a2c9545feed4c4afb3c64b30b42c94d5382a108d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftstoragestorageaccountselector-ui-element"></a><span data-ttu-id="981c5-103">Microsoft.Storage.StorageAccountSelector UI 元素</span><span class="sxs-lookup"><span data-stu-id="981c5-103">Microsoft.Storage.StorageAccountSelector UI element</span></span>
<span data-ttu-id="981c5-104">選取新的或現有儲存體帳戶的控制項。</span><span class="sxs-lookup"><span data-stu-id="981c5-104">A control for selecting a new or existing storage account.</span></span> <span data-ttu-id="981c5-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="981c5-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="981c5-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="981c5-106">UI sample</span></span>
![Microsoft.Storage.StorageAccountSelector](./media/managed-application-elements/microsoft.storage.storageaccountselector.png)

## <a name="schema"></a><span data-ttu-id="981c5-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="981c5-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="981c5-109">備註</span><span class="sxs-lookup"><span data-stu-id="981c5-109">Remarks</span></span>
- <span data-ttu-id="981c5-110">如果指定，就會自動驗證 `defaultValue.name` 的唯一性。</span><span class="sxs-lookup"><span data-stu-id="981c5-110">If specified, `defaultValue.name` is automatically validated for uniqueness.</span></span> <span data-ttu-id="981c5-111">如果 hello 儲存體帳戶名稱不是唯一的 hello 使用者必須指定不同的名稱，或選擇現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="981c5-111">If hello storage account name is not unique, hello user must specify a different name or choose an existing storage account.</span></span>
- <span data-ttu-id="981c5-112">預設值的 hello`defaultValue.type`是**Premium_LRS**。</span><span class="sxs-lookup"><span data-stu-id="981c5-112">hello default value for `defaultValue.type` is **Premium_LRS**.</span></span>
- <span data-ttu-id="981c5-113">`constraints.allowedTypes` 中未指定的任何類型都會加以隱藏，`constraints.excludedTypes` 中未指定的任何類型都會加以顯示。</span><span class="sxs-lookup"><span data-stu-id="981c5-113">Any type not specified in `constraints.allowedTypes` is hidden, and any type not specified in `constraints.excludedTypes` is shown.</span></span>
<span data-ttu-id="981c5-114">`constraints.allowedTypes` 和 `constraints.excludedTypes` 都是選擇性的，但不能同時使用。</span><span class="sxs-lookup"><span data-stu-id="981c5-114">`constraints.allowedTypes` and `constraints.excludedTypes` are both optional, but cannot be used simultaneously.</span></span>
- <span data-ttu-id="981c5-115">如果`options.hideExisting`是**true**，hello 使用者無法選擇現有的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="981c5-115">If `options.hideExisting` is **true**, hello user can't choose an existing storage account.</span></span> <span data-ttu-id="981c5-116">hello 預設值是**false**。</span><span class="sxs-lookup"><span data-stu-id="981c5-116">hello default value is **false**.</span></span>


## <a name="sample-output"></a><span data-ttu-id="981c5-117">範例輸出</span><span class="sxs-lookup"><span data-stu-id="981c5-117">Sample output</span></span>
```json
{
  "name": "storageaccount01",
  "resourceGroup": "rg01",
  "type": "Premium_LRS",
  "newOrExisting": "new"
}
```

## <a name="next-steps"></a><span data-ttu-id="981c5-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="981c5-118">Next steps</span></span>
* <span data-ttu-id="981c5-119">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="981c5-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="981c5-120">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="981c5-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="981c5-121">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="981c5-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
