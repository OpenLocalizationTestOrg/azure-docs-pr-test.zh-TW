---
title: "Azure 受管理的應用程式 SizeSelector UI 元素 | Microsoft Docs"
description: "描述 Azure 受管理應用程式的 Microsoft.Compute.SizeSelector UI 元素"
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
ms.openlocfilehash: e54962f73028ada258a7faef271d66f0fbcef649
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputesizeselector-ui-element"></a><span data-ttu-id="9e9d2-103">Microsoft.Compute.SizeSelector UI 元素</span><span class="sxs-lookup"><span data-stu-id="9e9d2-103">Microsoft.Compute.SizeSelector UI element</span></span>
<span data-ttu-id="9e9d2-104">選取一個或多個虛擬機器執行個體之大小的控制項。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-104">A control for selecting a size for one or more virtual machine instances.</span></span> <span data-ttu-id="9e9d2-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="9e9d2-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="9e9d2-106">UI sample</span></span>
![Microsoft.Compute.SizeSelector](./media/managed-application-elements/microsoft.compute.sizeselector.png)

## <a name="schema"></a><span data-ttu-id="9e9d2-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="9e9d2-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="9e9d2-109">備註</span><span class="sxs-lookup"><span data-stu-id="9e9d2-109">Remarks</span></span>
- <span data-ttu-id="9e9d2-110">`recommendedSizes` 須包含至少一個大小。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-110">`recommendedSizes` should contain at least one size.</span></span> <span data-ttu-id="9e9d2-111">會使用第一個建議的大小作為預設值。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-111">The first recommended size is used as the default.</span></span>
- <span data-ttu-id="9e9d2-112">如果選取的位置中無法使用建議的大小，就會將大小自動略過。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-112">If a recommended size is not available in the selected location, the size is automatically skipped.</span></span> <span data-ttu-id="9e9d2-113">反之，會使用下一個建議的大小。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-113">Instead, the next recommended size is used.</span></span>
- <span data-ttu-id="9e9d2-114">`constraints.allowedSizes` 中未指定的任何大小都會加以隱藏，`constraints.excludedSizes` 中未指定的任何大小都會加以顯示。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-114">Any size not specified in the `constraints.allowedSizes` is hidden, and any size not specified in `constraints.excludedSizes` is shown.</span></span>
<span data-ttu-id="9e9d2-115">`constraints.allowedSizes` 和 `constraints.excludedSizes` 都是選擇性的，但不能同時使用。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-115">`constraints.allowedSizes` and `constraints.excludedSizes` are both optional, but cannot be used simultaneously.</span></span> <span data-ttu-id="9e9d2-116">可透過呼叫[列出訂用帳戶的可用虛擬機器大小](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region)來決定可用大小的清單。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-116">The list of available sizes can be determined by calling [List available virtual machine sizes for a subscription](/rest/api/compute/virtualmachines/virtualmachines-list-sizes-region).</span></span>
- <span data-ttu-id="9e9d2-117">必須指定 `osPlatform`，且可以是 **Windows** 或 **Linux**。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-117">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span> <span data-ttu-id="9e9d2-118">它可用來判斷虛擬機器的硬體成本。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-118">It's used to determine the hardware costs of the virtual machines.</span></span>
- <span data-ttu-id="9e9d2-119">第一方映像的 `imageReference` 會加以省略，但會提供給第三方映像。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-119">`imageReference` is omitted for first-party images, but provided for third-party images.</span></span> <span data-ttu-id="9e9d2-120">它可用來判斷虛擬機器的軟體成本。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-120">It's used to determine the software costs of the virtual machines.</span></span>
- <span data-ttu-id="9e9d2-121">`count` 可用來設定元素的適當乘數。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-121">`count` is used to set the appropriate multiplier for the element.</span></span> <span data-ttu-id="9e9d2-122">它支援靜態值 (例如 **2**)，或者另一個元素的動態值 (例如 `[steps('step1').vmCount]`)。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-122">It supports a static value, like **2**, or a dynamic value from another element, like `[steps('step1').vmCount]`.</span></span> <span data-ttu-id="9e9d2-123">預設值為 **1**。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-123">The default value is **1**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="9e9d2-124">範例輸出</span><span class="sxs-lookup"><span data-stu-id="9e9d2-124">Sample output</span></span>
```json
"Standard_D1"
```

## <a name="next-steps"></a><span data-ttu-id="9e9d2-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9e9d2-125">Next steps</span></span>
* <span data-ttu-id="9e9d2-126">如需受管理應用程式的簡介，請參閱 [Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-126">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="9e9d2-127">如需建立 UI 定義的簡介，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-127">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="9e9d2-128">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="9e9d2-128">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
