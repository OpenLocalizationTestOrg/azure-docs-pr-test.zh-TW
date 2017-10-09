---
title: "aaaAzure 受管理應用程式下拉式清單中的 UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Common.DropDown UI 項目"
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
ms.openlocfilehash: 1c07a48ad66b8e8b7fd8f59561776ecb1fc6224f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftcommondropdown-ui-element"></a><span data-ttu-id="a8d03-103">Microsoft.Common.DropDown UI 元素</span><span class="sxs-lookup"><span data-stu-id="a8d03-103">Microsoft.Common.DropDown UI element</span></span>
<span data-ttu-id="a8d03-104">下拉式清單中的選取控制項。</span><span class="sxs-lookup"><span data-stu-id="a8d03-104">A selection control with a dropdown list.</span></span> <span data-ttu-id="a8d03-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="a8d03-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="a8d03-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="a8d03-106">UI sample</span></span>
![Microsoft.Common.DropDown](./media/managed-application-elements/microsoft.common.dropdown.png)

## <a name="schema"></a><span data-ttu-id="a8d03-108">結構描述</span><span class="sxs-lookup"><span data-stu-id="a8d03-108">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="a8d03-109">備註</span><span class="sxs-lookup"><span data-stu-id="a8d03-109">Remarks</span></span>
- <span data-ttu-id="a8d03-110">hello 標籤`constraints.allowedValues`hello 顯示文字項目，且其值為 hello hello 項目時選取的輸出值。</span><span class="sxs-lookup"><span data-stu-id="a8d03-110">hello label for `constraints.allowedValues` is hello display text for an item, and its value is hello output value of hello element when selected.</span></span>
- <span data-ttu-id="a8d03-111">如果指定，hello 預設值必須是存在於標籤`constraints.allowedValues`。</span><span class="sxs-lookup"><span data-stu-id="a8d03-111">If specified, hello default value must be a label present in `constraints.allowedValues`.</span></span> <span data-ttu-id="a8d03-112">如果未指定，hello 中的第一個項目`constraints.allowedValues`已選取。</span><span class="sxs-lookup"><span data-stu-id="a8d03-112">If not specified, hello first item in `constraints.allowedValues` is selected.</span></span> <span data-ttu-id="a8d03-113">hello 預設值是**null**。</span><span class="sxs-lookup"><span data-stu-id="a8d03-113">hello default value is **null**.</span></span>
- <span data-ttu-id="a8d03-114">`constraints.allowedValues` 必須包含至少一個項目。</span><span class="sxs-lookup"><span data-stu-id="a8d03-114">`constraints.allowedValues` must contain at least one item.</span></span>
- <span data-ttu-id="a8d03-115">這個項目不支援 hello`constraints.required`屬性。</span><span class="sxs-lookup"><span data-stu-id="a8d03-115">This element doesn't support hello `constraints.required` property.</span></span> <span data-ttu-id="a8d03-116">tooemulate 這種行為，將標籤和值的項目`""`（空字串） 太`constraints.allowedValues`。</span><span class="sxs-lookup"><span data-stu-id="a8d03-116">tooemulate this behavior, add an item with a label and value of `""` (empty string) too`constraints.allowedValues`.</span></span>

## <a name="sample-output"></a><span data-ttu-id="a8d03-117">範例輸出</span><span class="sxs-lookup"><span data-stu-id="a8d03-117">Sample output</span></span>
```json
"Bar"
```

## <a name="next-steps"></a><span data-ttu-id="a8d03-118">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a8d03-118">Next steps</span></span>
* <span data-ttu-id="a8d03-119">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a8d03-119">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="a8d03-120">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a8d03-120">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="a8d03-121">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="a8d03-121">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
