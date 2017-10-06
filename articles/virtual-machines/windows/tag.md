---
title: "aaaHow tootag 在 Azure 中的 Windows VM 資源 |Microsoft 文件"
description: "深入了解標記使用 hello Resource Manager 部署模型在 Azure 中建立 Windows 虛擬機器"
services: virtual-machines-windows
documentationcenter: 
author: mmccrory
manager: timlt
editor: tysonn
tags: azure-resource-manager
ms.assetid: 56d17f45-e4a7-4d84-8022-b40334ae49d2
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 07/05/2016
ms.author: memccror
ms.openlocfilehash: 160416ddc35998b3c98c6e579668a6a5eb6de6e4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-tootag-a-windows-virtual-machine-in-azure"></a><span data-ttu-id="43dd5-103">如何 tootag Azure 中的 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="43dd5-103">How tootag a Windows virtual machine in Azure</span></span>
<span data-ttu-id="43dd5-104">本文說明不同的方式 tootag Windows 虛擬機器在 Azure 中透過 hello Resource Manager 部署模型。</span><span class="sxs-lookup"><span data-stu-id="43dd5-104">This article describes different ways tootag a Windows virtual machine in Azure through hello Resource Manager deployment model.</span></span> <span data-ttu-id="43dd5-105">標記是使用者定義的成對「索引鍵/值」，可直接置於資源或資源群組。</span><span class="sxs-lookup"><span data-stu-id="43dd5-105">Tags are user-defined key/value pairs which can be placed directly on a resource or a resource group.</span></span> <span data-ttu-id="43dd5-106">Azure 目前支援向上 too15 標記每個資源與資源群組。</span><span class="sxs-lookup"><span data-stu-id="43dd5-106">Azure currently supports up too15 tags per resource and resource group.</span></span> <span data-ttu-id="43dd5-107">標籤可能會放在資源上建立 hello 時，或加入 tooan 現有的資源。</span><span class="sxs-lookup"><span data-stu-id="43dd5-107">Tags may be placed on a resource at hello time of creation or added tooan existing resource.</span></span> <span data-ttu-id="43dd5-108">請注意標記支援的 hello Resource Manager 部署模型只能透過建立的資源。</span><span class="sxs-lookup"><span data-stu-id="43dd5-108">Please note that tags are supported for resources created via hello Resource Manager deployment model only.</span></span> <span data-ttu-id="43dd5-109">如果您想 tootag Linux 虛擬機器，請參閱[如何在 Azure 中 Linux 虛擬機器 tootag](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="43dd5-109">If you want tootag a Linux virtual machine, see [How tootag a Linux virtual machine in Azure](../linux/tag.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

[!INCLUDE [virtual-machines-common-tag](../../../includes/virtual-machines-common-tag.md)]

## <a name="tagging-with-powershell"></a><span data-ttu-id="43dd5-110">使用 PowerShell 來標記</span><span class="sxs-lookup"><span data-stu-id="43dd5-110">Tagging with PowerShell</span></span>
<span data-ttu-id="43dd5-111">toocreate，新增和刪除透過 PowerShell 的標記，則需要 tooset 向上您[PowerShell 環境與 Azure 資源管理員][PowerShell environment with Azure Resource Manager]。</span><span class="sxs-lookup"><span data-stu-id="43dd5-111">toocreate, add, and delete tags through PowerShell, you first need tooset up your [PowerShell environment with Azure Resource Manager][PowerShell environment with Azure Resource Manager].</span></span> <span data-ttu-id="43dd5-112">完成 hello 安裝程式之後，您可以將標籤置於運算、 網路和儲存體資源，在建立或透過 PowerShell 建立 hello 資源之後。</span><span class="sxs-lookup"><span data-stu-id="43dd5-112">Once you have completed hello setup, you can place tags on Compute, Network, and Storage resources at creation or after hello resource is created via PowerShell.</span></span> <span data-ttu-id="43dd5-113">本文將專注於檢視/編輯置於虛擬機器上的標記。</span><span class="sxs-lookup"><span data-stu-id="43dd5-113">This article will concentrate on viewing/editing tags placed on Virtual Machines.</span></span>

<span data-ttu-id="43dd5-114">首先，瀏覽 tooa 虛擬機器透過 hello `Get-AzureRmVM` cmdlet。</span><span class="sxs-lookup"><span data-stu-id="43dd5-114">First, navigate tooa Virtual Machine through hello `Get-AzureRmVM` cmdlet.</span></span>

        PS C:\> Get-AzureRmVM -ResourceGroupName "MyResourceGroup" -Name "MyTestVM"

<span data-ttu-id="43dd5-115">如果您的虛擬機器已經包含標記，您接著會看到您在資源上所有的 hello 標記：</span><span class="sxs-lookup"><span data-stu-id="43dd5-115">If your Virtual Machine already contains tags, you will then see all hello tags on your resource:</span></span>

        Tags : {
                "Application": "MyApp1",
                "Created By": "MyName",
                "Department": "MyDepartment",
                "Environment": "Production"
               }

<span data-ttu-id="43dd5-116">如果您想要透過 PowerShell tooadd 標記，您可以使用 hello`Set-AzureRmResource`命令。</span><span class="sxs-lookup"><span data-stu-id="43dd5-116">If you would like tooadd tags through PowerShell, you can use hello `Set-AzureRmResource` command.</span></span> <span data-ttu-id="43dd5-117">請注意，透過 PowerShell 標記更新時，標記會整體進行更新。</span><span class="sxs-lookup"><span data-stu-id="43dd5-117">Note when updating tags through PowerShell, tags are updated as a whole.</span></span> <span data-ttu-id="43dd5-118">因此，如果您要新增一個標記 tooa 資源已有標籤，您必須 tooinclude 想 toobe 放在 hello 資源上的所有 hello 標記。</span><span class="sxs-lookup"><span data-stu-id="43dd5-118">So if you are adding one tag tooa resource that already has tags, you will need tooinclude all hello tags that you want toobe placed on hello resource.</span></span> <span data-ttu-id="43dd5-119">以下是如何 tooadd 其他標記 tooa 資源，透過 PowerShell Cmdlet 的範例。</span><span class="sxs-lookup"><span data-stu-id="43dd5-119">Below is an example of how tooadd additional tags tooa resource through PowerShell Cmdlets.</span></span>

<span data-ttu-id="43dd5-120">此第一個指令程式會設定所有 hello 標記置於*MyTestVM* toohello *$tags*使用 hello 變數`Get-AzureRmResource`和`Tags`屬性。</span><span class="sxs-lookup"><span data-stu-id="43dd5-120">This first cmdlet sets all of hello tags placed on *MyTestVM* toohello *$tags* variable, using hello `Get-AzureRmResource` and `Tags` property.</span></span>

        PS C:\> $tags = (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

<span data-ttu-id="43dd5-121">hello 第二個命令會顯示 hello 指定變數的 hello 標記。</span><span class="sxs-lookup"><span data-stu-id="43dd5-121">hello second command displays hello tags for hello given variable.</span></span>

        PS C:\> $tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment

<span data-ttu-id="43dd5-122">hello 第三個命令會加入其他標記 toohello *$tags*變數。</span><span class="sxs-lookup"><span data-stu-id="43dd5-122">hello third command adds an additional tag toohello *$tags* variable.</span></span> <span data-ttu-id="43dd5-123">請記下的 hello hello 使用 **+=**  tooappend hello 新的索引鍵/值組 toohello *$tags*清單。</span><span class="sxs-lookup"><span data-stu-id="43dd5-123">Note hello use of hello **+=** tooappend hello new key/value pair toohello *$tags* list.</span></span>

        PS C:\> $tags += @{Name="Location";Value="MyLocation"}

<span data-ttu-id="43dd5-124">hello 第四個命令會將所有定義 hello hello 標記*$tags*變數 toohello 指定資源。</span><span class="sxs-lookup"><span data-stu-id="43dd5-124">hello fourth command sets all of hello tags defined in hello *$tags* variable toohello given resource.</span></span> <span data-ttu-id="43dd5-125">本例中是 MyTestVM。</span><span class="sxs-lookup"><span data-stu-id="43dd5-125">In this case, it is MyTestVM.</span></span>

        PS C:\> Set-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM -ResourceType "Microsoft.Compute/VirtualMachines" -Tag $tags

<span data-ttu-id="43dd5-126">hello 第五個命令會顯示所有 hello 標記 hello 資源上。</span><span class="sxs-lookup"><span data-stu-id="43dd5-126">hello fifth command displays all of hello tags on hello resource.</span></span> <span data-ttu-id="43dd5-127">如您所見，*位置*現在已定義為具有標記*MyLocation* hello 值。</span><span class="sxs-lookup"><span data-stu-id="43dd5-127">As you can see, *Location* is now defined as a tag with *MyLocation* as hello value.</span></span>

        PS C:\> (Get-AzureRmResource -ResourceGroupName MyResourceGroup -Name MyTestVM).Tags

        Name        Value
        ----                           -----
        Value        MyDepartment
        Name        Department
        Value        MyApp1
        Name        Application
        Value        MyName
        Name        Created By
        Value        Production
        Name        Environment
        Value        MyLocation
        Name        Location

<span data-ttu-id="43dd5-128">深入了解 toolearn 標記透過 PowerShell，請參閱 hello [Azure 資源 Cmdlet][Azure Resource Cmdlets]。</span><span class="sxs-lookup"><span data-stu-id="43dd5-128">toolearn more about tagging through PowerShell, check out hello [Azure Resource Cmdlets][Azure Resource Cmdlets].</span></span>

[!INCLUDE [virtual-machines-common-tag-usage](../../../includes/virtual-machines-common-tag-usage.md)]

## <a name="next-steps"></a><span data-ttu-id="43dd5-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="43dd5-129">Next steps</span></span>
* <span data-ttu-id="43dd5-130">toolearn 深入了解標記您的 Azure 資源，請參閱[Azure 資源管理員概觀][ Azure Resource Manager Overview]和[使用標記 tooorganize Azure 資源][ Using Tags tooorganize your Azure Resources].</span><span class="sxs-lookup"><span data-stu-id="43dd5-130">toolearn more about tagging your Azure resources, see [Azure Resource Manager Overview][Azure Resource Manager Overview] and [Using Tags tooorganize your Azure Resources][Using Tags tooorganize your Azure Resources].</span></span>
* <span data-ttu-id="43dd5-131">toosee 如何標記可以協助您管理您使用的 Azure 資源，請參閱[了解您的 Azure 帳單][ Understanding your Azure Bill]和[深入了解您的 Microsoft Azure 資源耗用量][Gain insights into your Microsoft Azure resource consumption].</span><span class="sxs-lookup"><span data-stu-id="43dd5-131">toosee how tags can help you manage your use of Azure resources, see [Understanding your Azure Bill][Understanding your Azure Bill] and [Gain insights into your Microsoft Azure resource consumption][Gain insights into your Microsoft Azure resource consumption].</span></span>

[PowerShell environment with Azure Resource Manager]: ../../azure-resource-manager/powershell-azure-resource-manager.md
[Azure Resource Cmdlets]: https://msdn.microsoft.com/library/azure/dn757692.aspx
[Azure Resource Manager Overview]: ../../azure-resource-manager/resource-group-overview.md
[Using Tags tooorganize your Azure Resources]: ../../azure-resource-manager/resource-group-using-tags.md
[Understanding your Azure Bill]: ../../billing/billing-understand-your-bill.md
[Gain insights into your Microsoft Azure resource consumption]: ../../billing/billing-usage-rate-card-overview.md
