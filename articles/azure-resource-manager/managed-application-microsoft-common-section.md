---
title: "aaaAzure 受管理的應用程式 > 一節 UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Common.Section UI 項目"
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
ms.openlocfilehash: d20b365b12fab66177e1a12db2ebbeefe507212e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonsection-ui-element"></a><span data-ttu-id="848c0-103">Microsoft.Common.Section UI 元素</span><span class="sxs-lookup"><span data-stu-id="848c0-103">Microsoft.Common.Section UI element</span></span>
<span data-ttu-id="848c0-104">將標題下方一個或多個元素進行群組的控制項。</span><span class="sxs-lookup"><span data-stu-id="848c0-104">A control that groups one or more elements under a heading.</span></span> <span data-ttu-id="848c0-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="848c0-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="848c0-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="848c0-106">UI sample</span></span>
![Microsoft.Common.Section](./media/managed-application-elements/microsoft.common.section.png)

## <a name="schema"></a><span data-ttu-id="848c0-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="848c0-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="848c0-109">備註</span><span class="sxs-lookup"><span data-stu-id="848c0-109">Remarks</span></span>
- <span data-ttu-id="848c0-110">`elements` 必須包含至少一個元素，且可以包含 `Microsoft.Common.Section` 以外的所有元素類型。</span><span class="sxs-lookup"><span data-stu-id="848c0-110">`elements` must contain at least one element, and can contain all element types except `Microsoft.Common.Section`.</span></span>
- <span data-ttu-id="848c0-111">這個項目不支援 hello`toolTip`屬性。</span><span class="sxs-lookup"><span data-stu-id="848c0-111">This element doesn't support hello `toolTip` property.</span></span>

## <a name="sample-output"></a><span data-ttu-id="848c0-112">範例輸出</span><span class="sxs-lookup"><span data-stu-id="848c0-112">Sample output</span></span>
<span data-ttu-id="848c0-113">tooaccess hello 輸出中的項目值`elements`，使用 hello [basics()](managed-application-createuidefinition-functions.md#basics)或[steps()](managed-application-createuidefinition-functions.md#steps)函式和點標記法：</span><span class="sxs-lookup"><span data-stu-id="848c0-113">tooaccess hello output values of elements in `elements`, use hello [basics()](managed-application-createuidefinition-functions.md#basics) or [steps()](managed-application-createuidefinition-functions.md#steps) functions and dot notation:</span></span>

```json
basics('section1').element1
```

<span data-ttu-id="848c0-114">`Microsoft.Common.Section` 類型的元素本身沒有任何輸出值。</span><span class="sxs-lookup"><span data-stu-id="848c0-114">Elements of type `Microsoft.Common.Section` have no output values themselves.</span></span>

## <a name="next-steps"></a><span data-ttu-id="848c0-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="848c0-115">Next steps</span></span>
* <span data-ttu-id="848c0-116">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="848c0-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="848c0-117">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="848c0-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="848c0-118">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="848c0-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
