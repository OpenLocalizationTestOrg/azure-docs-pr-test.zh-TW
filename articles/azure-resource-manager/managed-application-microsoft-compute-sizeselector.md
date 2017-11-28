---
title: "aaaAzure 受管理的應用程式 SizeSelector UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Compute.SizeSelector UI 項目"
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
ms.openlocfilehash: d93306135d9c6f9a83692766ce1ca7ea2b688086
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="9ab8f-103">Microsoft.Compute.SizeSelector UI 元素</span><span class="sxs-lookup"><span data-stu-id="9ab8f-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="9ab8f-104">選取一個或多個虛擬機器執行個體之大小的控制項。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="9ab8f-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="9ab8f-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="9ab8f-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="9ab8f-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="9ab8f-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.SizeSelector",
  "label": "Size",
  "toolTip": "",
  "recommendedSizes": [
    "Standard_D1",
    "Standard_D2",
    "Standard_D3"
  ],
  "constraints": {
    "allowedSizes": [],
    "excludedSizes": []
  },
  "osPlatform": "Windows",
  "imageReference": {
    "publisher": "MicrosoftWindowsServer",
    "offer": "WindowsServer",
    "sku": "2012-R2-Datacenter"
  },
  "count": 2,
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="9ab8f-109">備註</span><span class="sxs-lookup"><span data-stu-id="9ab8f-109">Remarks</span></span>
- <span data-ttu-id="9ab8f-110">`recommendedSizes` 須包含至少一個大小。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="9ab8f-111">hello 先建議 hello 預設會使用大小。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-111">hello first recommended size is used as hello default.</span></span>
- <span data-ttu-id="9ab8f-112">如果在選取的 hello 位置無法使用建議的大小，會自動略過 hello 大小。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-112">If a recommended size is not available in hello selected location, hello size is automatically skipped.</span></span> <span data-ttu-id="9ab8f-113">相反地，hello 下一步建議使用大小。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-113">Instead, hello next recommended size is used.</span></span>
- <span data-ttu-id="9ab8f-114">Hello 中未指定任何大小`constraints.allowedSizes`隱藏的並在未指定任何大小`constraints.excludedSizes`顯示。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-114">Any size not specified in hello `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="9ab8f-115">`constraints.allowedSizes` 和 `constraints.excludedSizes` 都是選擇性的，但不能同時使用。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="9ab8f-116">hello 清單中的可用大小由呼叫[清單的訂用帳戶可用的虛擬機器大小](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-116">hello list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="9ab8f-117">必須指定 `osPlatform`，且可以是 **Windows** 或 **Linux**。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="9ab8f-118">它已用 toodetermine hello 硬體成本的 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-118">It's used toodetermine hello hardware costs of hello virtual machines.</span></span>
- <span data-ttu-id="9ab8f-119">第一方映像的 `imageReference` 會加以省略，但會提供給第三方映像。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="9ab8f-120">它已用 hello 虛擬機器的 toodetermine hello 軟體成本。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-120">It's used toodetermine hello software costs of hello virtual machines.</span></span>
- <span data-ttu-id="9ab8f-121">`count`是使用的 tooset hello 適當的乘數 hello 項目。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-121">`count` is used tooset hello appropriate multiplier for hello element.</span></span> <span data-ttu-id="9ab8f-122">它支援靜態值 (例如 **2**)，或者另一個元素的動態值 (例如 `[steps('step1').vmCount]`)。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="9ab8f-123">hello 預設值是**1**。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-123">hello default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="9ab8f-124">範例輸出</span><span class="sxs-lookup"><span data-stu-id="9ab8f-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="9ab8f-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9ab8f-125">Next steps</span></span>
* <span data-ttu-id="9ab8f-126">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-126">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="9ab8f-127">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-127">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="9ab8f-128">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="9ab8f-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
