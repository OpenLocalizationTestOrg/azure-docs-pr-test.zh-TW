---
title: "Azure 受管理的應用程式 UserNameTextBox UI 元素 | Microsoft Docs"
description: "描述 Azure 受管理應用程式的 Microsoft.Compute.UserNameTextBox UI 元素"
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
ms.openlocfilehash: c90be5a0ed3aadda81d7ec9b5388a96472f69af0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="6bd8b-103">Microsoft.Compute.UserNameTextBox UI 元素</span><span class="sxs-lookup"><span data-stu-id="6bd8b-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="6bd8b-104">使用 Windows 和 Linux 使用者名稱內建驗證的文字方塊控制項。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="6bd8b-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="6bd8b-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="6bd8b-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="6bd8b-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="6bd8b-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Compute.UserNameTextBox",
  "label": "User name",
  "defaultValue": "",
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "^[a-z0-9A-Z]{1,30}$",
    "validationMessage": "Only alphanumeric characters are allowed, and the value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="6bd8b-109">備註</span><span class="sxs-lookup"><span data-stu-id="6bd8b-109">Remarks</span></span>
- <span data-ttu-id="6bd8b-110">如果將 `constraints.required` 設為 **true**，文字方塊就必須包含值，才能順利通過驗證。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-110">If `constraints.required` is set to **true**, then the text box must contain a value to validate successfully.</span></span> <span data-ttu-id="6bd8b-111">預設值為 **true**。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-111">The default value is **true**.</span></span>
- <span data-ttu-id="6bd8b-112">必須指定 `osPlatform`，且可以是 **Windows** 或 **Linux**。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="6bd8b-113">`constraints.regex` 是 JavaScript 規則運算式模式。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="6bd8b-114">如果指定，文字方塊的值就必須符合模式，才能順利通過驗證。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-114">If specified, then the text box's value must match the pattern to validate successfully.</span></span> <span data-ttu-id="6bd8b-115">預設值為 **null**。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-115">The default value is **null**.</span></span>
- <span data-ttu-id="6bd8b-116">當文字方塊的值無法通過 `constraints.regex` 驗證時，就會顯示 `constraints.validationMessage` 字串。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-116">`constraints.validationMessage` is a string to display when the text box's value fails the validation specified by `constraints.regex`.</span></span> <span data-ttu-id="6bd8b-117">如果未指定，則會使用文字方塊的內建的驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-117">If not specified, then the text box's built-in validation messages are used.</span></span> <span data-ttu-id="6bd8b-118">預設值為 **null**。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-118">The default value is **null**.</span></span>
- <span data-ttu-id="6bd8b-119">這個元素具有根據 `osPlatform` 指定值的內建驗證。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-119">This element has built-in validation that is based on the value specified for `osPlatform`.</span></span> <span data-ttu-id="6bd8b-120">內建驗證可以與自訂規則運算式搭配使用。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-120">The built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="6bd8b-121">如果指定了 `constraints.regex` 值，就會觸發內建和自訂驗證。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-121">If a value for `constraints.regex` is specified, then both the built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="6bd8b-122">範例輸出</span><span class="sxs-lookup"><span data-stu-id="6bd8b-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="6bd8b-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6bd8b-123">Next steps</span></span>
* <span data-ttu-id="6bd8b-124">如需受管理應用程式的簡介，請參閱 [Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-124">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="6bd8b-125">如需建立 UI 定義的簡介，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-125">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="6bd8b-126">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="6bd8b-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
