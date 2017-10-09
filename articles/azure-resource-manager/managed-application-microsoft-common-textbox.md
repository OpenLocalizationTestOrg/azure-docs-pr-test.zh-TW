---
title: "aaaAzure 受管理應用程式文字方塊中的 UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Common.TextBox UI 項目"
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
ms.openlocfilehash: 11771cd1d689b720384df98b8d1465703068af37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommontextbox-ui-element"></a><span data-ttu-id="51887-103">Microsoft.Common.TextBox UI 元素</span><span class="sxs-lookup"><span data-stu-id="51887-103">Microsoft.Common.TextBox UI element</span></span>
<span data-ttu-id="51887-104">可以是使用的 tooedit 控制項未格式化的文字。</span><span class="sxs-lookup"><span data-stu-id="51887-104">A control that can be used tooedit unformatted text.</span></span> <span data-ttu-id="51887-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="51887-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="51887-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="51887-106">UI sample</span></span>
![Microsoft.Common.TextBox](./media/managed-application-elements/microsoft.common.textbox.png)

## <a name="schema"></a><span data-ttu-id="51887-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="51887-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="51887-109">備註</span><span class="sxs-lookup"><span data-stu-id="51887-109">Remarks</span></span>
- <span data-ttu-id="51887-110">如果`constraints.required`設定得**true**，則 hello 文字方塊必須包含值 toovalidate 成功。</span><span class="sxs-lookup"><span data-stu-id="51887-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="51887-111">hello 預設值是**false**。</span><span class="sxs-lookup"><span data-stu-id="51887-111">hello default value is **false**.</span></span>
- <span data-ttu-id="51887-112">`constraints.regex` 是 JavaScript 規則運算式模式。</span><span class="sxs-lookup"><span data-stu-id="51887-112">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="51887-113">如果指定，然後 hello 文字方塊的值必須符合 hello 模式 toovalidate 成功。</span><span class="sxs-lookup"><span data-stu-id="51887-113">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="51887-114">預設值為 **null**。</span><span class="sxs-lookup"><span data-stu-id="51887-114">The default value is **null**.</span></span>
- <span data-ttu-id="51887-115">`constraints.validationMessage`時，字串 toodisplay hello 文字方塊的值無法通過驗證。</span><span class="sxs-lookup"><span data-stu-id="51887-115">`constraints.validationMessage` is a string toodisplay when hello text box's value fails validation.</span></span> <span data-ttu-id="51887-116">如果未指定，則 hello 訊息在使用文字方塊中內建的驗證。</span><span class="sxs-lookup"><span data-stu-id="51887-116">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="51887-117">hello 預設值是**null**。</span><span class="sxs-lookup"><span data-stu-id="51887-117">hello default value is **null**.</span></span>
- <span data-ttu-id="51887-118">它的可能 toospecify 值`constraints.regex`時`constraints.required`設定得**false**。</span><span class="sxs-lookup"><span data-stu-id="51887-118">It's possible toospecify a value for `constraints.regex` when `constraints.required` is set too**false**.</span></span> <span data-ttu-id="51887-119">在此案例中，不需要值的 hello 文字方塊 toovalidate 成功。</span><span class="sxs-lookup"><span data-stu-id="51887-119">In this scenario, a value is not required for hello text box toovalidate successfully.</span></span> <span data-ttu-id="51887-120">如果有指定，它必須符合 hello 規則運算式模式。</span><span class="sxs-lookup"><span data-stu-id="51887-120">If one is specified, it must match hello regular expression pattern.</span></span>

## <a name="sample-output"></a><span data-ttu-id="51887-121">範例輸出</span><span class="sxs-lookup"><span data-stu-id="51887-121">Sample output</span></span>

```json
"foobar"
```

## <a name="next-steps"></a><span data-ttu-id="51887-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51887-122">Next steps</span></span>
* <span data-ttu-id="51887-123">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="51887-123">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="51887-124">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="51887-124">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="51887-125">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="51887-125">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
