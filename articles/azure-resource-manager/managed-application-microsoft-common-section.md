---
title: "Azure 受管理的應用程式 Section UI 元素 | Microsoft Docs"
description: "描述 Azure 受管理應用程式的 Microsoft.Common.Section UI 元素"
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
ms.openlocfilehash: 34c0f2f88e6af5a0f822ec116e7e2334e4e29e8d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="0ff3f-103">Microsoft.Common.Section UI 元素</span><span class="sxs-lookup"><span data-stu-id="0ff3f-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="0ff3f-104">將標題下方一個或多個元素進行群組的控制項。</span><span class="sxs-lookup"><span data-stu-id="0ff3f-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="0ff3f-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="0ff3f-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="0ff3f-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="0ff3f-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="0ff3f-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="0ff3f-108">Schema</span></span>
```json
{
  "name": "section1",
  "type": "Microsoft.Common.Section",
  "label": "Some section",
  "elements": [
    {
      "name": "element1",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 1"
    },
    {
      "name": "element2",
      "type": "Microsoft.Common.TextBox",
      "label": "Some text box 2"
    }
  ],
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="0ff3f-109">備註</span><span class="sxs-lookup"><span data-stu-id="0ff3f-109">Remarks</span></span>
- <span data-ttu-id="0ff3f-110">`elements` 必須包含至少一個元素，且可以包含 `Microsoft.Common.Section` 以外的所有元素類型。</span><span class="sxs-lookup"><span data-stu-id="0ff3f-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="0ff3f-111">此元素不支援 `toolTip` 屬性。</span><span class="sxs-lookup"><span data-stu-id="0ff3f-111">This element doesn't support the `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="0ff3f-112">範例輸出</span><span class="sxs-lookup"><span data-stu-id="0ff3f-112">Sample output</span></span>
<span data-ttu-id="0ff3f-113">若要存取 `elements` 中的元素輸出值，可使用 [basics()](managed-application-createuidefinition-functions.md#basics) 或 [steps()](managed-application-createuidefinition-functions.md#steps) 函式和點標記法︰</span><span class="sxs-lookup"><span data-stu-id="0ff3f-113">To access the output values of elements in `elements`, use the [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="0ff3f-114">`Microsoft.Common.Section` 類型的元素本身沒有任何輸出值。</span><span class="sxs-lookup"><span data-stu-id="0ff3f-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0ff3f-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0ff3f-115">Next steps</span></span>
* <span data-ttu-id="0ff3f-116">如需受管理應用程式的簡介，請參閱 [Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0ff3f-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="0ff3f-117">如需建立 UI 定義的簡介，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="0ff3f-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="0ff3f-118">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="0ff3f-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
