---
title: "如何標記 Azure Linux 虛擬機器 | Microsoft Docs"
description: "了解如何標記在 Azure 中以 Resource Manager 部署模型建立的 Azure Linux 虛擬機器。"
services: virtual-machines-linux
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: ca0e17e5-d78e-42e6-9dad-c1e8f1c58027
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 02/28/2017
ms.author: memccror
ms.openlocfilehash: f643001c85e127ae39e9869ffdc689bcac232ccb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-to-tag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="22496-103">如何在 Azure 中標記 Linux 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="22496-103">How to tag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="22496-104">本文說明在 Azure 中透過 Resource Manager 部署模型標記 Linux 虛擬機器的各種不同方式。</span><span class="sxs-lookup"><span data-stu-id="22496-104">This article describes different ways to tag a Linux virtual machine in Azure through the Resource Manager deployment model.</span></span> <span data-ttu-id="22496-105">標記是使用者定義的成對「索引鍵/值」，可直接置於資源或資源群組。</span><span class="sxs-lookup"><span data-stu-id="22496-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="22496-106">Azure 目前對每一個資源和資源群組最多支援 15 個標記。</span><span class="sxs-lookup"><span data-stu-id="22496-106">Azure currently supports up to 15 tags per resource and resource group.</span></span> <span data-ttu-id="22496-107">標記可在建立或加入至現有資源時置於資源上。</span><span class="sxs-lookup"><span data-stu-id="22496-107">Tags may be placed on a resource at the time of creation or added to an existing resource.</span></span> <span data-ttu-id="22496-108">請注意，標記只支援透過 Resource Manager 部署模型建立的資源。</span><span class="sxs-lookup"><span data-stu-id="22496-108">Please note, tags are supported for resources created via the Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="22496-109">透過 Azure CLI 進行標記</span><span class="sxs-lookup"><span data-stu-id="22496-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="22496-110">若要開始，請[安裝和設定 Azure CLI](../../xplat-cli-azure-resource-manager.md)，並確定您處於 Resource Manager 模式 (`azure config mode arm`)。</span><span class="sxs-lookup"><span data-stu-id="22496-110">To begin, [install and configure the Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="22496-111">您可以使用這個命令來檢視指定之虛擬機器的所有屬性，包括標記：</span><span class="sxs-lookup"><span data-stu-id="22496-111">You can view all properties for a given Virtual Machine, including the tags, using this command:</span></span>

        azure vm show -g MyResourceGroup -n MyTestVM

<span data-ttu-id="22496-112">若要透過 Azure CLI 新增 VM 標記，您可以搭配使用 `azure vm set` 命令搭配標記參數 **-t**：</span><span class="sxs-lookup"><span data-stu-id="22496-112">To add a new VM tag through the Azure CLI, you can use the `azure vm set` command along with the tag parameter **-t**:</span></span>

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

<span data-ttu-id="22496-113">若要移除所有標記，您可以在 `azure vm set` 命令中使用 **–T** 參數。</span><span class="sxs-lookup"><span data-stu-id="22496-113">To remove all tags, you can use the **–T** parameter in the `azure vm set` command.</span></span>

        azure vm set – g MyResourceGroup –n MyTestVM -T


<span data-ttu-id="22496-114">既然我們已將標記套用至我們的資源 Azure CLI 和入口網站，就讓我們來看一下使用量詳細資料，以在計費入口網站中查看標記。</span><span class="sxs-lookup"><span data-stu-id="22496-114">Now that we have applied tags to our resources Azure CLI and the Portal, let’s take a look at the usage details to see the tags in the billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="22496-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="22496-115">Next steps</span></span>
* <span data-ttu-id="22496-116">如需深入了解如何標記您的 Azure 資源，請參閱 [Azure Resource Manager 概觀][Azure Resource Manager Overview]與[使用標記來組織您的 Azure 資源][Using Tags to organize your Azure Resources]。</span><span class="sxs-lookup"><span data-stu-id="22496-116">To learn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags to organize your Azure Resources][Using Tags to organize your Azure Resources].</span></span>
* <span data-ttu-id="22496-117">如需查看標記如何協助您管理使用 Azure 資源，請參閱[了解 Azure 帳單][Understanding your Azure Bill]與[深入了解 Microsoft Azure 資源耗用量][Gain insights into your Microsoft Azure resource consumption]。</span><span class="sxs-lookup"><span data-stu-id="22496-117">To see how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags to organize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
