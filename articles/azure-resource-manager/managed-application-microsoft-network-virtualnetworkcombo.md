---
title: "Azure 受管理的應用程式 VirtualNetworkCombo UI 元素 | Microsoft Docs"
description: "描述 Azure 受管理應用程式的 Microsoft.Network.VirtualNetworkCombo UI 元素"
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
ms.openlocfilehash: 8bb255b76ac5c3de570fa569a1cfb3ee953f9687
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="3afd0-103">Microsoft.Network.VirtualNetworkCombo UI 元素</span><span class="sxs-lookup"><span data-stu-id="3afd0-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="3afd0-104">選取新的或現有虛擬網路的控制項群組。</span><span class="sxs-lookup"><span data-stu-id="3afd0-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="3afd0-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="3afd0-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="3afd0-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="3afd0-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="3afd0-108">在最上層的框線中，使用者已選取新的虛擬網路，因此使用者可以自訂每一個子網路的名稱和位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="3afd0-108">In the top wireframe, the user has picked a new virtual network, so the user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="3afd0-109">在此情況下，設定子網路為選擇性的。</span><span class="sxs-lookup"><span data-stu-id="3afd0-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="3afd0-110">在最下層的框線中，使用者已選取現有的虛擬網路，因此使用者必須將部署範本所需的每個子網路對應到現有的子網路。</span><span class="sxs-lookup"><span data-stu-id="3afd0-110">In the bottom wireframe, the user has picked an existing virtual network, so the user must map each subnet the deployment template requires to an existing subnet.</span></span> <span data-ttu-id="3afd0-111">在此情況下，設定子網路為必要的。</span><span class="sxs-lookup"><span data-stu-id="3afd0-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="3afd0-112">結構描述</span><span class="sxs-lookup"><span data-stu-id="3afd0-112">Schema</span></span>
```json
{
  "name": "element1",
  "type": "Microsoft.Network.VirtualNetworkCombo",
  "label": {
    "virtualNetwork": "Virtual network",
    "subnets": "Subnets"
  },
  "toolTip": {
    "virtualNetwork": "",
    "subnets": ""
  },
  "defaultValue": {
    "name": "vnet01",
    "addressPrefixSize": "/16"
  },
  "constraints": {
    "minAddressPrefixSize": "/16"
  },
  "options": {
    "hideExisting": false
  },
  "subnets": {
    "subnet1": {
      "label": "First subnet",
      "defaultValue": {
        "name": "subnet-1",
        "addressPrefixSize": "/24"
      },
      "constraints": {
        "minAddressPrefixSize": "/24",
        "minAddressCount": 12,
        "requireContiguousAddresses": true
      }
    },
    "subnet2": {
      "label": "Second subnet",
      "defaultValue": {
        "name": "subnet-2",
        "addressPrefixSize": "/26"
      },
      "constraints": {
        "minAddressPrefixSize": "/26",
        "minAddressCount": 8,
        "requireContiguousAddresses": true
      }
    }
  },
  "visible": true
}
```

## <a name="remarks"></a><span data-ttu-id="3afd0-113">備註</span><span class="sxs-lookup"><span data-stu-id="3afd0-113">Remarks</span></span>
- <span data-ttu-id="3afd0-114">如果指定，就會根據使用者訂用帳戶中的現有虛擬網路，自動決定 `defaultValue.addressPrefixSize` 大小的第一個非重疊位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="3afd0-114">If specified, the first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in the user's subscription.</span></span>
- <span data-ttu-id="3afd0-115">`defaultValue.name` 和 `defaultValue.addressPrefixSize` 的預設值為 **null**。</span><span class="sxs-lookup"><span data-stu-id="3afd0-115">The default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="3afd0-116">必須指定 `constraints.minAddressPrefixSize`。</span><span class="sxs-lookup"><span data-stu-id="3afd0-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="3afd0-117">任何現有虛擬網路的位址空間若低於指定的值，就無法加以選取。</span><span class="sxs-lookup"><span data-stu-id="3afd0-117">Any existing virtual networks with an address space smaller than the specified value are unavailable for selection.</span></span>
- <span data-ttu-id="3afd0-118">必須指定 `subnets`，且必須指定每個子網路的 `constraints.minAddressPrefixSize`。</span><span class="sxs-lookup"><span data-stu-id="3afd0-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="3afd0-119">在建立新的虛擬網路時，會根據虛擬網路的位址前置詞和個別的 `addressPrefixSize`自動計算每個子網路的位址首碼。</span><span class="sxs-lookup"><span data-stu-id="3afd0-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on the virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="3afd0-120">在使用現有的虛擬網路時，無法選取任何小於個別 `constraints.minAddressPrefixSize` 的子網路。</span><span class="sxs-lookup"><span data-stu-id="3afd0-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="3afd0-121">此外，如果指定，就無法選取未至少包含 `minAddressCount` 的子網路。</span><span class="sxs-lookup"><span data-stu-id="3afd0-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="3afd0-122">預設值為 **0**。</span><span class="sxs-lookup"><span data-stu-id="3afd0-122">The default value is **0**.</span></span> <span data-ttu-id="3afd0-123">若要確保可用位址是連續的，請將 `requireContiguousAddresses` 指定為 **true**。</span><span class="sxs-lookup"><span data-stu-id="3afd0-123">To ensure that the available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="3afd0-124">預設值為 **true**。</span><span class="sxs-lookup"><span data-stu-id="3afd0-124">The default value is **true**.</span></span>
- <span data-ttu-id="3afd0-125">不支援在現有的虛擬網路中建立子網路。</span><span class="sxs-lookup"><span data-stu-id="3afd0-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="3afd0-126">如果 `options.hideExisting` 為 **true**，使用者就無法選擇現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="3afd0-126">If `options.hideExisting` is **true**, the user can't choose an existing virtual network.</span></span> <span data-ttu-id="3afd0-127">預設值為 **false**。</span><span class="sxs-lookup"><span data-stu-id="3afd0-127">The default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="3afd0-128">範例輸出</span><span class="sxs-lookup"><span data-stu-id="3afd0-128">Sample output</span></span>
```json
{
  "name": "vnet01",
  "resourceGroup": "rg01",
  "addressPrefixes": ["10.0.0.0/16"],
  "newOrExisting": "new",
  "subnets": {
    "subnet1": {
      "name": "subnet-1",
      "addressPrefix": "10.0.0.0/24",
      "startAddress": "10.0.0.1"
    },
    "subnet2": {
      "name": "subnet-2",
      "addressPrefix": "10.0.1.0/26",
      "startAddress": "10.0.1.1"
    }
  }
}
```

## <a name="next-steps"></a><span data-ttu-id="3afd0-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3afd0-129">Next steps</span></span>
* <span data-ttu-id="3afd0-130">如需受管理應用程式的簡介，請參閱 [Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3afd0-130">For an introduction to managed applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="3afd0-131">如需建立 UI 定義的簡介，請參閱[開始使用 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3afd0-131">For an introduction to creating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="3afd0-132">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="3afd0-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
