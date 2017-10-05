---
title: "Azure 受管理的應用程式 PublicIpAddressCombo UI 元素 | Microsoft Docs"
description: "描述 Azure 受管理應用程式的 Microsoft.Network.PublicIpAddressCombo UI 元素"
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
ms.openlocfilehash: 2eb773f5f0cf389fc39bc3a0f5fbf9ac726d1949
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkpublicipaddresscombo-ui-element"></a><span data-ttu-id="62e86-103">Microsoft.Network.PublicIpAddressCombo UI 元素</span><span class="sxs-lookup"><span data-stu-id="62e86-103">Microsoft.Network.PublicIpAddressCombo UI element</span></span>
<span data-ttu-id="62e86-104">選取新的或現有公用 IP 位址的控制項群組。</span><span class="sxs-lookup"><span data-stu-id="62e86-104">A group of controls for selecting a new or existing public IP address.</span></span> <span data-ttu-id="62e86-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="62e86-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="62e86-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="62e86-106">UI sample</span></span>
![Microsoft.Network.PublicIpAddressCombo](./media/managed-application-elements/microsoft.network.publicipaddresscombo.png)

- <span data-ttu-id="62e86-108">如果使用者的公用 IP 位址選擇 [無]，網域名稱標籤文字方塊就會加以隱藏。</span><span class="sxs-lookup"><span data-stu-id="62e86-108">If the user selects 'None' for public IP address, the domain name label text box is hidden.</span></span>
- <span data-ttu-id="62e86-109">如果使用者選擇現有的公用 IP 位址，網域名稱標籤文字方塊就會加以停用。</span><span class="sxs-lookup"><span data-stu-id="62e86-109">If the user selects an existing public IP address, the domain name label text box is disabled.</span></span> <span data-ttu-id="62e86-110">其值為所選取 IP 位址的網域名稱標籤。</span><span class="sxs-lookup"><span data-stu-id="62e86-110">Its value is the domain name label of the selected IP address.</span></span>
- <span data-ttu-id="62e86-111">網域名稱尾碼 (例如，westus.cloudapp.azure.com) 會根據選取的位置自動更新。</span><span class="sxs-lookup"><span data-stu-id="62e86-111">The domain name suffix (for example, westus.cloudapp.azure.com) updates automatically based on the selected location.</span></span>

## <a name="schema"></a><span data-ttu-id="62e86-112">結構描述</span><span class="sxs-lookup"><span data-stu-id="62e86-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="62e86-113">備註</span><span class="sxs-lookup"><span data-stu-id="62e86-113">Remarks</span></span>
- <span data-ttu-id="62e86-114">如果將 `constraints.required.domainNameLabel` 設為 **true**，使用者在建立新的公用 IP 位址時，就必須提供網域名稱標籤。</span><span class="sxs-lookup"><span data-stu-id="62e86-114">If `constraints.required.domainNameLabel` is set to **true**, the user must provide a domain name label when creating a new public IP address.</span></span> <span data-ttu-id="62e86-115">無法選取沒有標籤的現有公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="62e86-115">Existing public IP addresses without a label are not available for selection.</span></span>
- <span data-ttu-id="62e86-116">如果將 `options.hideNone` 設為 **true**，公用 IP 位址的 [無] 選項就會加以隱藏。</span><span class="sxs-lookup"><span data-stu-id="62e86-116">If `options.hideNone` is set to **true**, then the option to select **None** for the public IP address is hidden.</span></span> <span data-ttu-id="62e86-117">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="62e86-117">The default value is **false**.</span></span>
- <span data-ttu-id="62e86-118">如果將 `options.hideDomainNameLabel` 設為 **true**，網域名稱標籤的文字方塊就會加以隱藏。</span><span class="sxs-lookup"><span data-stu-id="62e86-118">If `options.hideDomainNameLabel` is set to **true**, then the text box for domain name label is hidden.</span></span> <span data-ttu-id="62e86-119">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="62e86-119">The default value is **false**.</span></span>
- <span data-ttu-id="62e86-120">如果 `options.hideExisting` 為 true，使用者就無法選擇現有的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="62e86-120">If `options.hideExisting` is true, then the user is not able to choose an existing public IP address.</span></span> <span data-ttu-id="62e86-121">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="62e86-121">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="62e86-122">範例輸出</span><span class="sxs-lookup"><span data-stu-id="62e86-122">Sample output</span></span>
<span data-ttu-id="62e86-123">如果使用者未選取公用 IP 位址，則預期會產生下列輸出︰</span><span class="sxs-lookup"><span data-stu-id="62e86-123">If the user selects no public IP address, the following output is expected:</span></span>
```json
{
  "newOrExistingOrNone": "none"
}
```

<span data-ttu-id="62e86-124">如果使用者選取新的或現有 IP 位址，則預期會產生下列輸出︰</span><span class="sxs-lookup"><span data-stu-id="62e86-124">If the user selects a new or existing IP address, the following output is expected:</span></span>
```json
{
  "name": "ip01",
  "resourceGroup": "rg01",
  "domainNameLabel": "foobar",
  "newOrExistingOrNone": "new"
}
```
- <span data-ttu-id="62e86-125">當指定 `options.hideNone` 時，`newOrExistingOrNone` 一律會傳回 [無]。</span><span class="sxs-lookup"><span data-stu-id="62e86-125">When `options.hideNone` is specified, `newOrExistingOrNone` always returns **none**.</span></span>
- <span data-ttu-id="62e86-126">當指定 `options.hideDomainNameLabel` 時，`domainNameLabel` 為未宣告。</span><span class="sxs-lookup"><span data-stu-id="62e86-126">When `options.hideDomainNameLabel` is specified, `domainNameLabel` is undeclared.</span></span>

## <a name="next-steps"></a><span data-ttu-id="62e86-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="62e86-127">Next steps</span></span>
* <span data-ttu-id="62e86-128">如需受管理應用程式的簡介，請參閱 [Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="62e86-128">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="62e86-129">如需建立 UI 定義的簡介，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="62e86-129">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="62e86-130">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="62e86-130">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
