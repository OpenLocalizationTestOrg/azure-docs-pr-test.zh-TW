---
title: "Azure 受管理的應用程式 DropDown UI 元素 | Microsoft Docs"
description: "描述 Azure 受管理應用程式的 Microsoft.Common.DropDown UI 元素"
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
ms.openlocfilehash: a769e14efbae928b811fa1f1b1c2d4fba3c7692b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="41d20-103">Microsoft.Common.DropDown UI 元素</span><span class="sxs-lookup"><span data-stu-id="41d20-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="41d20-104">下拉式清單中的選取控制項。</span><span class="sxs-lookup"><span data-stu-id="41d20-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="41d20-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="41d20-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="41d20-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="41d20-106">UI sample</span></span>
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="41d20-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="41d20-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.DropDown",
  "label": "Some drop down",
  "defaultValue": "Foo",
  "toolTip": "",
  "constraints": {
    "allowedValues": [
      {
        "label": "Foo",
        "value": "Bar"
      },
      {
        "label": "Baz",
        "value": "Qux"
      }
    ]
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="41d20-109">備註</span><span class="sxs-lookup"><span data-stu-id="41d20-109">Remarks</span></span>
- <span data-ttu-id="41d20-110">`constraints.allowedValues` 的標籤是項目的顯示文字，其值為選取時的元素輸出值。</span><span class="sxs-lookup"><span data-stu-id="41d20-110">The label for `constraints.allowedValues` is the display text for an item, and its value is the output value of the element when selected.</span></span>
- <span data-ttu-id="41d20-111">如果指定，預設值必須是 `constraints.allowedValues` 中存在的標籤。</span><span class="sxs-lookup"><span data-stu-id="41d20-111">If specified, the default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="41d20-112">如果未指定，則會選取 `constraints.allowedValues` 中的第一個項目。</span><span class="sxs-lookup"><span data-stu-id="41d20-112">If not specified, the first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="41d20-113">預設值為 **null**。</span><span class="sxs-lookup"><span data-stu-id="41d20-113">The default value is **null**.</span></span>
- <span data-ttu-id="41d20-114">`constraints.allowedValues` 必須包含至少一個項目。</span><span class="sxs-lookup"><span data-stu-id="41d20-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="41d20-115">此元素不支援 `constraints.required` 屬性。</span><span class="sxs-lookup"><span data-stu-id="41d20-115">This element doesn't support the `constraints.required` property.</span></span> <span data-ttu-id="41d20-116">若要模擬此行為，將包含標籤和 `""` (空字串) 值的項目新增至 `constraints.allowedValues`。</span><span class="sxs-lookup"><span data-stu-id="41d20-116">To emulate this behavior, add an item with a label and value of `""` (empty string) to `constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="41d20-117">範例輸出</span><span class="sxs-lookup"><span data-stu-id="41d20-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="41d20-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="41d20-118">Next steps</span></span>
* <span data-ttu-id="41d20-119">如需受管理應用程式的簡介，請參閱 [Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="41d20-119">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="41d20-120">如需建立 UI 定義的簡介，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="41d20-120">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="41d20-121">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="41d20-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
