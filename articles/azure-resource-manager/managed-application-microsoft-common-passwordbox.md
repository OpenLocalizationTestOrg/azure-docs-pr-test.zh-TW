---
title: "aaaAzure 受管理的應用程式 PasswordBox UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Common.PasswordBox UI 項目"
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
ms.openlocfilehash: bcb1f54c0bee464075ed732ead9aa3f88697f49e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonpasswordbox-ui-element"></a><span data-ttu-id="e21d4-103">Microsoft.Common.PasswordBox UI 元素</span><span class="sxs-lookup"><span data-stu-id="e21d4-103">Microsoft.Common.PasswordBox UI element</span></span>
<span data-ttu-id="e21d4-104">控制項可使用的 tooprovide 和確認密碼。</span><span class="sxs-lookup"><span data-stu-id="e21d4-104">A control that can be used tooprovide and confirm a password.</span></span> <span data-ttu-id="e21d4-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="e21d4-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="e21d4-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="e21d4-106">UI sample</span></span>
![Microsoft.Common.PasswordBox](./media/managed-application-elements/microsoft.common.passwordbox.png)

## <a name="schema"></a><span data-ttu-id="e21d4-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="e21d4-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="e21d4-109">備註</span><span class="sxs-lookup"><span data-stu-id="e21d4-109">Remarks</span></span>
- <span data-ttu-id="e21d4-110">這個項目不支援 hello`defaultValue`屬性。</span><span class="sxs-lookup"><span data-stu-id="e21d4-110">This element doesn't support hello `defaultValue` property.</span></span>
- <span data-ttu-id="e21d4-111">如需 `constraints` 的實作詳細資料，請參閱 [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md)。</span><span class="sxs-lookup"><span data-stu-id="e21d4-111">For implementation details of `constraints`, see [Microsoft.Common.TextBox](managed-application-microsoft-common-textbox.md).</span></span>
- <span data-ttu-id="e21d4-112">如果`options.hideConfirmation`設定得**true**，隱藏 hello 第二個文字方塊中確認 hello 使用者的密碼。</span><span class="sxs-lookup"><span data-stu-id="e21d4-112">If `options.hideConfirmation` is set too**true**, hello second text box for confirming hello user's password is hidden.</span></span> <span data-ttu-id="e21d4-113">hello 預設值是**false**。</span><span class="sxs-lookup"><span data-stu-id="e21d4-113">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="e21d4-114">範例輸出</span><span class="sxs-lookup"><span data-stu-id="e21d4-114">Sample output</span></span>
```json
"p4ssw0rd"
```

## <a name="next-steps"></a><span data-ttu-id="e21d4-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e21d4-115">Next steps</span></span>
* <span data-ttu-id="e21d4-116">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e21d4-116">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="e21d4-117">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e21d4-117">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="e21d4-118">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="e21d4-118">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
