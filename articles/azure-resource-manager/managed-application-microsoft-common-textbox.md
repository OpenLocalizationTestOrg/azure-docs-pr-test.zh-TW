---
title: "Azure 受管理的應用程式 TextBox UI 元素 | Microsoft Docs"
description: "描述 Azure 受管理應用程式的 Microsoft.Common.TextBox UI 元素"
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
ms.openlocfilehash: 5a0ac5b811812c8c03f7f63aae12b8699d248ebf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="d748b-103">Microsoft.Common.TextBox UI 元素</span><span class="sxs-lookup"><span data-stu-id="d748b-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="d748b-104">可以用來編輯未格式化文字的控制項。</span><span class="sxs-lookup"><span data-stu-id="d748b-104">A control that can be used to edit unformatted text.</span></span> <span data-ttu-id="d748b-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="d748b-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="d748b-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="d748b-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="d748b-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="d748b-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.TextBox",
  "label": "Some text box",
  "defaultValue": "foobar",
  "toolTip": "Halp!",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="d748b-109">備註</span><span class="sxs-lookup"><span data-stu-id="d748b-109">Remarks</span></span>
- <span data-ttu-id="d748b-110">如果將 `constraints.required` 設為 **true**，文字方塊就必須包含值，才能順利通過驗證。</span><span class="sxs-lookup"><span data-stu-id="d748b-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="d748b-111">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="d748b-111">The default value is **false**.</span></span>
- <span data-ttu-id="d748b-112">`constraints.regex` 是 JavaScript 規則運算式模式。</span><span class="sxs-lookup"><span data-stu-id="d748b-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="d748b-113">如果指定，文字方塊的值就必須符合模式，才能順利通過驗證。</span><span class="sxs-lookup"><span data-stu-id="d748b-113">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="d748b-114">預設值為 **null**。</span><span class="sxs-lookup"><span data-stu-id="d748b-114">The default value is **null**.</span></span>
- <span data-ttu-id="d748b-115">當文字方塊的值無法通過驗證時，就會顯示 `constraints.validationMessage` 字串。</span><span class="sxs-lookup"><span data-stu-id="d748b-115">`constraints.validationMessage` is a string to display when the text box's value fails validation.</span></span> <span data-ttu-id="d748b-116">如果未指定，則會使用文字方塊的內建的驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="d748b-116">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="d748b-117">預設值為 **null**。</span><span class="sxs-lookup"><span data-stu-id="d748b-117">The default value is **null**.</span></span>
- <span data-ttu-id="d748b-118">當 `constraints.required` 設為 **false** 時，您可指定 `constraints.regex` 的值。</span><span class="sxs-lookup"><span data-stu-id="d748b-118">It's possible to specify a value for `constraints.regex` when `constraints.required` is set to **false**.</span></span> <span data-ttu-id="d748b-119">在此案例中，文字方塊不需要值即可順利通過驗證。</span><span class="sxs-lookup"><span data-stu-id="d748b-119">In this scenario, a value is not required for the text box to validate successfully.</span></span> <span data-ttu-id="d748b-120">如果指定的話，它必須符合規則運算式模式。</span><span class="sxs-lookup"><span data-stu-id="d748b-120">If one is specified, it must match the regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="d748b-121">範例輸出</span><span class="sxs-lookup"><span data-stu-id="d748b-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="d748b-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d748b-122">Next steps</span></span>
* <span data-ttu-id="d748b-123">如需受管理應用程式的簡介，請參閱 [Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d748b-123">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="d748b-124">如需建立 UI 定義的簡介，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d748b-124">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="d748b-125">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="d748b-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
