---
title: "aaaAzure 受管理的應用程式 VirtualNetworkCombo UI 項目 |Microsoft 文件"
description: "Azure 受管理的應用程式描述 hello Microsoft.Network.VirtualNetworkCombo UI 項目"
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
ms.openlocfilehash: 1b0fa5360d93306f7a814723f77e42540bdaaa9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="microsoftnetworkvirtualnetworkcombo-ui-element"></a><span data-ttu-id="a1750-103">Microsoft.Network.VirtualNetworkCombo UI 元素</span><span class="sxs-lookup"><span data-stu-id="a1750-103">Microsoft.Network.VirtualNetworkCombo UI element</span></span>
<span data-ttu-id="a1750-104">選取新的或現有虛擬網路的控制項群組。</span><span class="sxs-lookup"><span data-stu-id="a1750-104">A group of controls for selecting a new or existing virtual network.</span></span> <span data-ttu-id="a1750-105">您可以在[建立 Azure 受管理應用程式](managed-application-publishing.md)時使用此元素。</span><span class="sxs-lookup"><span data-stu-id="a1750-105">You use this element when [creating an Azure Managed Application](managed-application-publishing.md).</span></span>

## <a name="ui-sample"></a><span data-ttu-id="a1750-106">UI 範例</span><span class="sxs-lookup"><span data-stu-id="a1750-106">UI sample</span></span>
![Microsoft.Network.VirtualNetworkCombo](./media/managed-application-elements/microsoft.network.virtualnetworkcombo.png)

- <span data-ttu-id="a1750-108">在 hello 上框線，hello 使用者已挑選新的虛擬網路，因此 hello 使用者可以自訂每個子網路的名稱和位址前置詞。</span><span class="sxs-lookup"><span data-stu-id="a1750-108">In hello top wireframe, hello user has picked a new virtual network, so hello user can customize each subnet's name and address prefix.</span></span> <span data-ttu-id="a1750-109">在此情況下，設定子網路為選擇性的。</span><span class="sxs-lookup"><span data-stu-id="a1750-109">Configuring subnets in this case is optional.</span></span>
- <span data-ttu-id="a1750-110">在 hello 底部框線，hello 使用者已挑選現有的虛擬網路，因此 hello 使用者必須對應每一個子網路 hello 部署範本需要 tooan 現有的子網路。</span><span class="sxs-lookup"><span data-stu-id="a1750-110">In hello bottom wireframe, hello user has picked an existing virtual network, so hello user must map each subnet hello deployment template requires tooan existing subnet.</span></span> <span data-ttu-id="a1750-111">在此情況下，設定子網路為必要的。</span><span class="sxs-lookup"><span data-stu-id="a1750-111">Configuring subnets in this case is required.</span></span>

## <a name="schema"></a><span data-ttu-id="a1750-112">結構描述</span><span class="sxs-lookup"><span data-stu-id="a1750-112">Schema</span></span>
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

## <a name="remarks"></a><span data-ttu-id="a1750-113">備註</span><span class="sxs-lookup"><span data-stu-id="a1750-113">Remarks</span></span>
- <span data-ttu-id="a1750-114">如果指定，hello 第一個非重疊位址首碼的大小`defaultValue.addressPrefixSize`根據 hello 使用者訂用帳戶中的現有虛擬網路，自動決定。</span><span class="sxs-lookup"><span data-stu-id="a1750-114">If specified, hello first non-overlapping address prefix of size `defaultValue.addressPrefixSize` is determined automatically based on the existing virtual networks in hello user's subscription.</span></span>
- <span data-ttu-id="a1750-115">預設值的 hello`defaultValue.name`和`defaultValue.addressPrefixSize`是**null**。</span><span class="sxs-lookup"><span data-stu-id="a1750-115">hello default value for `defaultValue.name` and `defaultValue.addressPrefixSize` is **null**.</span></span>
- <span data-ttu-id="a1750-116">必須指定 `constraints.minAddressPrefixSize`。</span><span class="sxs-lookup"><span data-stu-id="a1750-116">`constraints.minAddressPrefixSize` must be specified.</span></span> <span data-ttu-id="a1750-117">任何現有的虛擬網路與小於 hello 指定的值都將無法使用選取的位址空間。</span><span class="sxs-lookup"><span data-stu-id="a1750-117">Any existing virtual networks with an address space smaller than hello specified value are unavailable for selection.</span></span>
- <span data-ttu-id="a1750-118">必須指定 `subnets`，且必須指定每個子網路的 `constraints.minAddressPrefixSize`。</span><span class="sxs-lookup"><span data-stu-id="a1750-118">`subnets` must be specified, and `constraints.minAddressPrefixSize` must be specified for each subnet.</span></span>
- <span data-ttu-id="a1750-119">在建立新的虛擬網路時，每個子網路位址首碼會自動根據計算 hello 虛擬網路的位址前置詞和個別`addressPrefixSize`。</span><span class="sxs-lookup"><span data-stu-id="a1750-119">When creating a new virtual network, each subnet's address prefix is calculated automatically based on hello virtual network's address prefix and the respective `addressPrefixSize`.</span></span>
- <span data-ttu-id="a1750-120">在使用現有的虛擬網路時，無法選取任何小於個別 `constraints.minAddressPrefixSize` 的子網路。</span><span class="sxs-lookup"><span data-stu-id="a1750-120">When using an existing virtual network, any subnets smaller than the respective `constraints.minAddressPrefixSize` are unavailable for selection.</span></span> <span data-ttu-id="a1750-121">此外，如果指定，就無法選取未至少包含 `minAddressCount` 的子網路。</span><span class="sxs-lookup"><span data-stu-id="a1750-121">Additionally, if specified, subnets that do not contain at least `minAddressCount` available addresses are unavailable for selection.</span></span>
<span data-ttu-id="a1750-122">hello 預設值是**0**。</span><span class="sxs-lookup"><span data-stu-id="a1750-122">hello default value is **0**.</span></span> <span data-ttu-id="a1750-123">hello 可用位址的 tooensure 是連續的請指定**true**如`requireContiguousAddresses`。</span><span class="sxs-lookup"><span data-stu-id="a1750-123">tooensure that hello available addresses are contiguous, specify **true** for `requireContiguousAddresses`.</span></span> <span data-ttu-id="a1750-124">hello 預設值是**true**。</span><span class="sxs-lookup"><span data-stu-id="a1750-124">hello default value is **true**.</span></span>
- <span data-ttu-id="a1750-125">不支援在現有的虛擬網路中建立子網路。</span><span class="sxs-lookup"><span data-stu-id="a1750-125">Creating subnets in an existing virtual network is not supported.</span></span>
- <span data-ttu-id="a1750-126">如果`options.hideExisting`是**true**，hello 使用者無法選擇現有的虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="a1750-126">If `options.hideExisting` is **true**, hello user can't choose an existing virtual network.</span></span> <span data-ttu-id="a1750-127">hello 預設值是**false**。</span><span class="sxs-lookup"><span data-stu-id="a1750-127">hello default value is **false**.</span></span>

## <a name="sample-output"></a><span data-ttu-id="a1750-128">範例輸出</span><span class="sxs-lookup"><span data-stu-id="a1750-128">Sample output</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="a1750-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a1750-129">Next steps</span></span>
* <span data-ttu-id="a1750-130">對於簡介 toomanaged 應用程式，請參閱[Azure 受管理的應用程式概觀](managed-application-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a1750-130">For an introduction toomanaged applications, see [Azure Managed Application overview](managed-application-overview.md).</span></span>
* <span data-ttu-id="a1750-131">如需簡介 toocreating UI 定義，請參閱[入門 CreateUiDefinition](managed-application-createuidefinition-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a1750-131">For an introduction toocreating UI definitions, see [Getting started with CreateUiDefinition](managed-application-createuidefinition-overview.md).</span></span>
* <span data-ttu-id="a1750-132">如需 UI 元素中通用屬性的說明，請參閱 [CreateUiDefinition 元素](managed-application-createuidefinition-elements.md)。</span><span class="sxs-lookup"><span data-stu-id="a1750-132">For a description of common properties in UI elements, see [CreateUiDefinition elements](managed-application-createuidefinition-elements.md).</span></span>
