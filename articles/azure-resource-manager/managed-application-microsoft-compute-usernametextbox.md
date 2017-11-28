---
title: "aaaAzure 受管理的應用程式 UserNameTextBox UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Compute.UserNameTextBox UI 項目"
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
ms.openlocfilehash: 33092014e804c4aabd56ba49144d9cd4d6a5fd1e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcomputeusernametextbox-ui-element"></a><span data-ttu-id="5846e-103">Microsoft.Compute.UserNameTextBox UI 元素</span><span class="sxs-lookup"><span data-stu-id="5846e-103">Microsoft.Compute.UserNameTextBox UI element</span></span>
<span data-ttu-id="5846e-104">使用 Windows 和 Linux 使用者名稱內建驗證的文字方塊控制項。</span><span class="sxs-lookup"><span data-stu-id="5846e-104">A text box control with built-in validation for Windows and Linux user names.</span></span> <span data-ttu-id="5846e-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="5846e-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="5846e-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="5846e-106">UI sample</span></span>
![Microsoft.Compute.UserNameTextBox](./media/managed-application-elements/microsoft.compute.usernametextbox.png)

## <a name="schema"></a><span data-ttu-id="5846e-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="5846e-108">Schema</span></span>
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
    "validationMessage": "Only alphanumeric characters are allowed, and hello value must be 1-30 characters long."
  },
  "osPlatform": "Windows",
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="5846e-109">備註</span><span class="sxs-lookup"><span data-stu-id="5846e-109">Remarks</span></span>
- <span data-ttu-id="5846e-110">如果`constraints.required`設定得**true**，則 hello 文字方塊必須包含值 toovalidate 成功。</span><span class="sxs-lookup"><span data-stu-id="5846e-110">If `constraints.required` is set too**true**, then hello text box must contain a value toovalidate successfully.</span></span> <span data-ttu-id="5846e-111">hello 預設值是**true**。</span><span class="sxs-lookup"><span data-stu-id="5846e-111">hello default value is **true**.</span></span>
- <span data-ttu-id="5846e-112">必須指定 `osPlatform`，且可以是 **Windows** 或 **Linux**。</span><span class="sxs-lookup"><span data-stu-id="5846e-112">`osPlatform` must be specified, and can be either **Windows** or **Linux**.</span></span>
- <span data-ttu-id="5846e-113">`constraints.regex` 是 JavaScript 規則運算式模式。</span><span class="sxs-lookup"><span data-stu-id="5846e-113">`constraints.regex` is a JavaScript regular expression pattern.</span></span> <span data-ttu-id="5846e-114">如果指定，然後 hello 文字方塊的值必須符合 hello 模式 toovalidate 成功。</span><span class="sxs-lookup"><span data-stu-id="5846e-114">If specified, then hello text box's value must match hello pattern toovalidate successfully.</span></span> <span data-ttu-id="5846e-115">預設值為 **null**。</span><span class="sxs-lookup"><span data-stu-id="5846e-115">The default value is **null**.</span></span>
- <span data-ttu-id="5846e-116">`constraints.validationMessage`hello 文字方塊的值所指定的 hello 驗證失敗時，是字串 toodisplay `constraints.regex`。</span><span class="sxs-lookup"><span data-stu-id="5846e-116">`constraints.validationMessage` is a string toodisplay when hello text box's value fails hello validation specified by `constraints.regex`.</span></span> <span data-ttu-id="5846e-117">如果未指定，則 hello 訊息在使用文字方塊中內建的驗證。</span><span class="sxs-lookup"><span data-stu-id="5846e-117">If not specified, then hello text box's built-in validation messages are used.</span></span> <span data-ttu-id="5846e-118">hello 預設值是**null**。</span><span class="sxs-lookup"><span data-stu-id="5846e-118">hello default value is **null**.</span></span>
- <span data-ttu-id="5846e-119">這個項目具有內建 hello 值指定為基礎的驗證`osPlatform`。</span><span class="sxs-lookup"><span data-stu-id="5846e-119">This element has built-in validation that is based on hello value specified for `osPlatform`.</span></span> <span data-ttu-id="5846e-120">hello 內建的驗證可以搭配自訂的規則運算式。</span><span class="sxs-lookup"><span data-stu-id="5846e-120">hello built-in validation can be used along with a custom regular expression.</span></span>
<span data-ttu-id="5846e-121">值如果`constraints.regex`指定，則兩者 hello 內建和自訂驗證所觸發。</span><span class="sxs-lookup"><span data-stu-id="5846e-121">If a value for `constraints.regex` is specified, then both hello built-in and custom validations are triggered.</span></span>

## <a name="sample-output"></a><span data-ttu-id="5846e-122">範例輸出</span><span class="sxs-lookup"><span data-stu-id="5846e-122">Sample output</span></span>
```json
"tabrezm"
```

## <a name="next-steps"></a><span data-ttu-id="5846e-123">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5846e-123">Next steps</span></span>
* <span data-ttu-id="5846e-124">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5846e-124">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5846e-125">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5846e-125">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="5846e-126">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="5846e-126">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
