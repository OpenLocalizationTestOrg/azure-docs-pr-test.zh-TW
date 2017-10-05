---
title: "Azure 受管理的應用程式 PasswordBox UI 元素 | Microsoft Docs"
description: "描述 Azure 受管理應用程式的 Microsoft.Common.PasswordBox UI 元素"
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
ms.openlocfilehash: 196a4b8f77145f83e46b4b23e148bb3a9dffc1b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="8be15-103">Microsoft.Common.PasswordBox UI 元素</span><span class="sxs-lookup"><span data-stu-id="8be15-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="8be15-104">可使用控制項來提供及確認密碼。</span><span class="sxs-lookup"><span data-stu-id="8be15-104">A control that can be used to provide and confirm a password.</span></span> <span data-ttu-id="8be15-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="8be15-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="8be15-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="8be15-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="8be15-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="8be15-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.PasswordBox",
  "label": {
    "password": "Password",
    "confirmPassword": "Confirm password"
  },
  "toolTip": "",
  "constraints": {
    "required": true,
    "regex": "",
    "validationMessage": ""
  },
  "options": {
    "hideConfirmation": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="8be15-109">備註</span><span class="sxs-lookup"><span data-stu-id="8be15-109">Remarks</span></span>
- <span data-ttu-id="8be15-110">此元素不支援 `defaultValue` 屬性。</span><span class="sxs-lookup"><span data-stu-id="8be15-110">This element doesn't support the `defaultValue` property.</span></span>
- <span data-ttu-id="8be15-111">如需 `constraints` 的實作詳細資料，請參閱 [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)。</span><span class="sxs-lookup"><span data-stu-id="8be15-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="8be15-112">如果將 `options.hideConfirmation` 設為 **true**，就會將確認使用者密碼的第二個文字方塊加以隱藏。</span><span class="sxs-lookup"><span data-stu-id="8be15-112">If `options.hideConfirmation` is set to **true**, the second text box for confirming the user's password is hidden.</span></span> <span data-ttu-id="8be15-113">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="8be15-113">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="8be15-114">範例輸出</span><span class="sxs-lookup"><span data-stu-id="8be15-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="8be15-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="8be15-115">Next steps</span></span>
* <span data-ttu-id="8be15-116">如需受管理應用程式的簡介，請參閱 [Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8be15-116">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="8be15-117">如需建立 UI 定義的簡介，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="8be15-117">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="8be15-118">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="8be15-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
