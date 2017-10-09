---
title: "aaaHow tootag Azure Linux 虛擬機器 |Microsoft 文件"
description: "深入了解標記使用 hello Resource Manager 部署模型在 Azure 中建立的 Azure Linux 虛擬機器。"
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
ms.openlocfilehash: 0e99ea66a87b7e00eb21a2f72dd2bce8673778dd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-linux-virtual-machine-in-azure"></a><span data-ttu-id="368e7-103">如何在 Azure 中 Linux 虛擬機器 tootag</span><span class="sxs-lookup"><span data-stu-id="368e7-103">How tootag a Linux virtual machine in Azure</span></span>
<span data-ttu-id="368e7-104">本文說明不同的方式 tootag Azure 中 Linux 虛擬機器，透過 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="368e7-104">This article describes different ways tootag a Linux virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="368e7-105">標記是使用者定義的成對「索引鍵/值」，可直接置於資源或資源群組。</span><span class="sxs-lookup"><span data-stu-id="368e7-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="368e7-106">Azure 目前支援向上 too15 標記每個資源與資源群組。</span><span class="sxs-lookup"><span data-stu-id="368e7-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="368e7-107">標籤可能會放在資源上建立 hello 時，或加入 tooan 現有的資源。</span><span class="sxs-lookup"><span data-stu-id="368e7-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="368e7-108">請注意，支援透過 hello Resource Manager 部署模型只能建立資源標記。</span><span class="sxs-lookup"><span data-stu-id="368e7-108">Please note, tags are supported for resources created via hello Resource Manager deployment model only.</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-azure-cli"></a><span data-ttu-id="368e7-109">透過 Azure CLI 進行標記</span><span class="sxs-lookup"><span data-stu-id="368e7-109">Tagging with Azure CLI</span></span>
<span data-ttu-id="368e7-110">toobegin，[安裝及設定 hello Azure CLI](../../xplat-cli-azure-resource-manager.md) ，並確定您是在 Resource Manager 模式 (`azure config mode arm`)。</span><span class="sxs-lookup"><span data-stu-id="368e7-110">toobegin, [install and configure hello Azure CLI](../../xplat-cli-azure-resource-manager.md) and make sure you are in Resource Manager mode (`azure config mode arm`).</span></span>

<span data-ttu-id="368e7-111">您可以檢視所有屬性指定的虛擬機器，包括 hello 標記，請使用此命令：</span><span class="sxs-lookup"><span data-stu-id="368e7-111">You can view all properties for a given Virtual Machine, including hello tags, using this command:</span></span>

        azure vm show -g MyResourceGroup -n MyTestVM

<span data-ttu-id="368e7-112">tooadd hello Azure CLI 透過新的 VM 標記，您可以使用 hello`azure vm set`命令以及 hello 標記參數**-t**:</span><span class="sxs-lookup"><span data-stu-id="368e7-112">tooadd a new VM tag through hello Azure CLI, you can use hello `azure vm set` command along with hello tag parameter **-t**:</span></span>

        azure vm set -g MyResourceGroup -n MyTestVM –t myNewTagName1=myNewTagValue1;myNewTagName2=myNewTagValue2

<span data-ttu-id="368e7-113">tooremove 所有標記，您可以使用 hello **– T**中 hello 參數`azure vm set`命令。</span><span class="sxs-lookup"><span data-stu-id="368e7-113">tooremove all tags, you can use hello **–T** parameter in hello `azure vm set` command.</span></span>

        azure vm set – g MyResourceGroup –n MyTestVM -T


<span data-ttu-id="368e7-114">現在，我們已套用標籤 tooour 資源 Azure CLI，並 hello 入口網站，讓我們看看 hello 使用量詳細資料 toosee hello 標記 hello 計費入口網站中。</span><span class="sxs-lookup"><span data-stu-id="368e7-114">Now that we have applied tags tooour resources Azure CLI and hello Portal, let’s take a look at hello usage details toosee hello tags in hello billing portal.</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="368e7-115">後續步驟</span><span class="sxs-lookup"><span data-stu-id="368e7-115">Next steps</span></span>
* <span data-ttu-id="368e7-116">toolearn 深入了解標記您的 Azure 資源，請參閱[Azure 資源管理員概觀][ Azure Resource Manager Overview]和[使用標記 tooorganize Azure 資源][ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="368e7-116">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="368e7-117">toosee 如何標記可以協助您管理您使用的 Azure 資源，請參閱[了解您的 Azure 帳單][ Understanding your Azure Bill]和[深入了解您的 Microsoft Azure 資源耗用量][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="368e7-117">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[Azure CLI environment]: ../../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
