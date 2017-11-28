---
title: "aaaAzure 受管理的應用程式 OptionsGroup UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Common.OptionsGroup UI 項目"
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
ms.openlocfilehash: e222468009c8db567bdde9f42836a48fb791da00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommonoptionsgroup-ui-element"></a><span data-ttu-id="1752f-103">Microsoft.Common.OptionsGroup UI 元素</span><span class="sxs-lookup"><span data-stu-id="1752f-103">Microsoft.Common.OptionsGroup UI element</span></span>
<span data-ttu-id="1752f-104">包含可用選項資料列的選取控制項。</span><span class="sxs-lookup"><span data-stu-id="1752f-104">A selection control with a row of available options.</span></span> <span data-ttu-id="1752f-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="1752f-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="1752f-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="1752f-106">UI sample</span></span>
![Microsoft.Common.OptionsGroup](./media/managed-application-elements/microsoft.common.optionsgroup.png)

## <a name="schema"></a><span data-ttu-id="1752f-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="1752f-108">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Common.OptionsGroup",
  "label": "Some options group",
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

## <a name="remarks"></a><span data-ttu-id="1752f-109">備註</span><span class="sxs-lookup"><span data-stu-id="1752f-109">Remarks</span></span>
- <span data-ttu-id="1752f-110">hello 標籤`constraints.allowedValues`hello 顯示文字項目，且其值為 hello hello 項目時選取的輸出值。</span><span class="sxs-lookup"><span data-stu-id="1752f-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="1752f-111">如果指定，hello 預設值必須是存在於標籤`constraints.allowedValues`。</span><span class="sxs-lookup"><span data-stu-id="1752f-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="1752f-112">如果未指定，hello 中的第一個項目`constraints.allowedValues`預設會選取。</span><span class="sxs-lookup"><span data-stu-id="1752f-112">If not specified, hello first item in `constraints.allowedValues` is selected by default.</span></span> <span data-ttu-id="1752f-113">hello 預設值是**null**。</span><span class="sxs-lookup"><span data-stu-id="1752f-113">hello default value is **null**.</span></span>
- <span data-ttu-id="1752f-114">`constraints.allowedValues` 必須包含至少一個項目。</span><span class="sxs-lookup"><span data-stu-id="1752f-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="1752f-115">這個項目不支援 hello`constraints.required`屬性; 項目必須選取的 toovalidate 成功。</span><span class="sxs-lookup"><span data-stu-id="1752f-115">This element doesn't support hello `constraints.required` property; an item must be selected toovalidate successfully.</span></span>

## <a name="sample-output"></a><span data-ttu-id="1752f-116">範例輸出</span><span class="sxs-lookup"><span data-stu-id="1752f-116">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="1752f-117">後續步驟</span><span class="sxs-lookup"><span data-stu-id="1752f-117">Next steps</span></span>
* <span data-ttu-id="1752f-118">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1752f-118">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="1752f-119">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="1752f-119">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="1752f-120">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="1752f-120">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
