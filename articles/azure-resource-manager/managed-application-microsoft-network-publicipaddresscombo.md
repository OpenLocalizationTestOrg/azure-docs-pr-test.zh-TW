---
title: "aaaAzure 受管理的應用程式 PublicIpAddressCombo UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Network.PublicIpAddressCombo UI 項目"
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
ms.openlocfilehash: 8ba689005c0eccda0a57bf628de4b5197886a950
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="5d185-103">Microsoft.Network.PublicIpAddressCombo UI 元素</span><span class="sxs-lookup"><span data-stu-id="5d185-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="5d185-104">選取新的或現有公用 IP 位址的控制項群組。</span><span class="sxs-lookup"><span data-stu-id="5d185-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="5d185-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="5d185-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="5d185-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="5d185-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="5d185-108">如果 hello 使用者選取 'None' 的公用 IP 位址時，會隱藏 hello 網域名稱標籤 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5d185-108">If hello user selects 'None' for public IP address, hello domain name label text box is hidden.</span></span>
- <span data-ttu-id="5d185-109">如果 hello 使用者選取現有的公用 IP 位址，已停用 hello 網域名稱標籤 文字方塊。</span><span class="sxs-lookup"><span data-stu-id="5d185-109">If hello user selects an existing public IP address, hello domain name label text box is disabled.</span></span> <span data-ttu-id="5d185-110">其值為 hello 選取 IP 位址的 hello 網域名稱標籤。</span><span class="sxs-lookup"><span data-stu-id="5d185-110">Its value is hello domain name label of hello selected IP address.</span></span>
- <span data-ttu-id="5d185-111">自動根據選取的 hello 位置 hello 網域名稱尾碼 (例如，westus.cloudapp.azure.com) 更新。</span><span class="sxs-lookup"><span data-stu-id="5d185-111">hello domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on hello selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="5d185-112">結構描述</span><span class="sxs-lookup"><span data-stu-id="5d185-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.PublicIpAddressCombo",
  "label": {
    "publicIpAddress": "Public IP address",
    "domainNameLabel": "Domain name label"
  },
  "toolTip": {
    "publicIpAddress": "",
    "domainNameLabel": ""
  },
  "defaultValue": {
    "publicIpAddressName": "ip01",
    "domainNameLabel": "foobar"
  },
  "constraints": {
    "required": {
      "domainNameLabel": true
    }
  },
  "options": {
    "hideNone": false,
    "hideDomainNameLabel": false,
    "hideExisting": false
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="5d185-113">備註</span><span class="sxs-lookup"><span data-stu-id="5d185-113">Remarks</span></span>
- <span data-ttu-id="5d185-114">如果`constraints.required.domainNameLabel`設定得**true**，hello 使用者必須提供網域名稱標籤，建立新的公用 IP 位址時。</span><span class="sxs-lookup"><span data-stu-id="5d185-114">If `constraints.required.domainNameLabel` is set too**true**, hello user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="5d185-115">無法選取沒有標籤的現有公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5d185-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="5d185-116">如果`options.hideNone`設定得**true**，然後 hello 選項 tooselect**無**隱藏 hello 公用 ip 位址。</span><span class="sxs-lookup"><span data-stu-id="5d185-116">If `options.hideNone` is set too**true**, then hello option tooselect **None** for hello public IP address is hidden.</span></span> <span data-ttu-id="5d185-117">hello 預設值是**false**。</span><span class="sxs-lookup"><span data-stu-id="5d185-117">hello default value is **false**.</span></span>
- <span data-ttu-id="5d185-118">如果`options.hideDomainNameLabel`設定得**true**，則隱藏 hello 文字方塊的網域名稱標籤。</span><span class="sxs-lookup"><span data-stu-id="5d185-118">If `options.hideDomainNameLabel` is set too**true**, then hello text box for domain name label is hidden.</span></span> <span data-ttu-id="5d185-119">hello 預設值是**false**。</span><span class="sxs-lookup"><span data-stu-id="5d185-119">hello default value is **false**.</span></span>
- <span data-ttu-id="5d185-120">如果`options.hideExisting`為 true，則 hello 使用者不能 toochoose 現有公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="5d185-120">If `options.hideExisting` is true, then hello user is not able toochoose an existing public IP address.</span></span> <span data-ttu-id="5d185-121">hello 預設值是**false**。</span><span class="sxs-lookup"><span data-stu-id="5d185-121">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="5d185-122">範例輸出</span><span class="sxs-lookup"><span data-stu-id="5d185-122">Sample output</span></span>
<span data-ttu-id="5d185-123">如果 hello 使用者選取未公用 IP 位址，hello 是預期產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="5d185-123">If hello user selects no public IP address, hello following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="5d185-124">如果 hello 使用者選取新的或現有的 IP 位址，hello 是預期產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="5d185-124">If hello user selects a new or existing IP address, hello following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="5d185-125">當指定 `options.hideNone` 時，`newOrExistingOrNone` 一律會傳回 [無]。</span><span class="sxs-lookup"><span data-stu-id="5d185-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="5d185-126">當指定 `options.hideDomainNameLabel` 時，`domainNameLabel` 為未宣告。</span><span class="sxs-lookup"><span data-stu-id="5d185-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5d185-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5d185-127">Next steps</span></span>
* <span data-ttu-id="5d185-128">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5d185-128">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="5d185-129">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="5d185-129">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="5d185-130">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="5d185-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
