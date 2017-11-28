---
title: "Azure 虛擬機器，從 伺服器總管 aaaAccessing |Microsoft 文件"
description: "取得 tooview 如何建立和管理 Azure 虛擬機器 (Vm) 在 Visual Studio 中的 伺服器總管中的概觀。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: eb3afde6-ba90-4308-9ac1-3cc29da4ede0
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/18/2016
ms.author: kraigb
ms.openlocfilehash: f8326aed105a64ca558f766d712cc68701f82c15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-azure-virtual-machines-from-server-explorer"></a><span data-ttu-id="71a62-103">從伺服器總管存取 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="71a62-103">Accessing Azure Virtual Machines from Server Explorer</span></span>
<span data-ttu-id="71a62-104">藉由使用 Visual Studio 中的 [伺服器總管]，您可以顯示 Azure 主控的虛擬機器相關資訊。</span><span class="sxs-lookup"><span data-stu-id="71a62-104">By using Server Explorer in Visual Studio, you can display information about your virtual machines hosted by Azure.</span></span>

## <a name="accessing-virtual-machines-in-server-explorer"></a><span data-ttu-id="71a62-105">在 [伺服器總管] 中存取 Azure 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="71a62-105">Accessing virtual machines in Server Explorer</span></span>
<span data-ttu-id="71a62-106">如果您有 Azure 主控的虛擬機器，您可以在 [伺服器總管] 中存取它們。</span><span class="sxs-lookup"><span data-stu-id="71a62-106">If you have virtual machines hosted by Azure, you can access them in Server Explorer.</span></span> <span data-ttu-id="71a62-107">您必須先登入 tooyour Azure 訂用帳戶 tooview 您的行動服務。</span><span class="sxs-lookup"><span data-stu-id="71a62-107">You must first sign in tooyour Azure subscription tooview your mobile services.</span></span> <span data-ttu-id="71a62-108">toosign 中，在 伺服器總管中開啟 hello hello Azure 節點的捷徑功能表，然後選擇 **連接 tooMicrosoft Azure**。</span><span class="sxs-lookup"><span data-stu-id="71a62-108">toosign in, open hello shortcut menu for hello Azure node in Server Explorer, and choose **Connect tooMicrosoft Azure**.</span></span>

### <a name="tooget-information-about-your-virtual-machines"></a><span data-ttu-id="71a62-109">您的虛擬機器的 tooget 資訊</span><span class="sxs-lookup"><span data-stu-id="71a62-109">tooget information about your virtual machines</span></span>
1. <span data-ttu-id="71a62-110">在伺服器總管 中，選擇為虛擬機器，，然後選擇 hello F4 鍵 tooshow 其屬性視窗。</span><span class="sxs-lookup"><span data-stu-id="71a62-110">In Server Explorer, choose a virtual machine, and then choose hello F4 key tooshow its properties window.</span></span>
   
    <span data-ttu-id="71a62-111">hello 下表顯示哪些屬性可用，但它們是唯讀。</span><span class="sxs-lookup"><span data-stu-id="71a62-111">hello following table shows what properties are available, but they are all read-only.</span></span> <span data-ttu-id="71a62-112">toochange，使用 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="71a62-112">toochange them, use hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span>
   
   | <span data-ttu-id="71a62-113">屬性</span><span class="sxs-lookup"><span data-stu-id="71a62-113">Property</span></span> | <span data-ttu-id="71a62-114">說明</span><span class="sxs-lookup"><span data-stu-id="71a62-114">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="71a62-115">DNS 名稱</span><span class="sxs-lookup"><span data-stu-id="71a62-115">DNS Name</span></span> |<span data-ttu-id="71a62-116">hello 以 hello hello 虛擬機器網際網路位址的 URL。</span><span class="sxs-lookup"><span data-stu-id="71a62-116">hello URL with hello Internet address of hello virtual machine.</span></span> |
   | <span data-ttu-id="71a62-117">Environment</span><span class="sxs-lookup"><span data-stu-id="71a62-117">Environment</span></span> |<span data-ttu-id="71a62-118">對於虛擬機器，hello 這個屬性的值一律是生產環境。</span><span class="sxs-lookup"><span data-stu-id="71a62-118">For a virtual machine, hello value of this property is always Production.</span></span> |
   | <span data-ttu-id="71a62-119">名稱</span><span class="sxs-lookup"><span data-stu-id="71a62-119">Name</span></span> |<span data-ttu-id="71a62-120">hello hello 虛擬機器名稱。</span><span class="sxs-lookup"><span data-stu-id="71a62-120">hello name of hello virtual machine.</span></span> |
   | <span data-ttu-id="71a62-121">大小</span><span class="sxs-lookup"><span data-stu-id="71a62-121">Size</span></span> |<span data-ttu-id="71a62-122">hello hello 虛擬機器，其會反映 hello 數量的記憶體和磁碟可用空間大小。</span><span class="sxs-lookup"><span data-stu-id="71a62-122">hello size of hello virtual machine, which reflects hello amount of memory and disk space that’s available.</span></span> <span data-ttu-id="71a62-123">如需詳細資訊，請參閱如何：設定虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="71a62-123">For more information, see How To: Configure Virtual Machine Sizes.</span></span> |
   | <span data-ttu-id="71a62-124">狀態</span><span class="sxs-lookup"><span data-stu-id="71a62-124">Status</span></span> |<span data-ttu-id="71a62-125">值包括 [啟動中]、[已啟動]、[停止中]、[已停止] 和 [正在擷取狀態]。</span><span class="sxs-lookup"><span data-stu-id="71a62-125">Values include Starting, Started, Stopping, Stopped, and Retrieving Status.</span></span> <span data-ttu-id="71a62-126">如果出現 正在擷取狀態，hello 目前狀態是未知的。</span><span class="sxs-lookup"><span data-stu-id="71a62-126">If Retrieving Status appears, hello current status is unknown.</span></span> <span data-ttu-id="71a62-127">hello 這個屬性的值不同於用於 hello 的 hello 值[Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="71a62-127">hello values for this property differ from hello values that are used on hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> |
   | <span data-ttu-id="71a62-128">SubscriptionID</span><span class="sxs-lookup"><span data-stu-id="71a62-128">SubscriptionID</span></span> |<span data-ttu-id="71a62-129">hello 您的 Azure 帳戶的訂用帳戶 ID。</span><span class="sxs-lookup"><span data-stu-id="71a62-129">hello subscription ID for your Azure account.</span></span> <span data-ttu-id="71a62-130">您可以將這項資訊顯示在 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)檢視 hello 訂用帳戶的內容。</span><span class="sxs-lookup"><span data-stu-id="71a62-130">You can show this information on hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885) by viewing hello properties for a subscription.</span></span> |
2. <span data-ttu-id="71a62-131">選擇 endpoint 節點，然後檢視 hello**屬性**視窗。</span><span class="sxs-lookup"><span data-stu-id="71a62-131">Choose an endpoint node, and then view hello **Properties** window.</span></span>
3. <span data-ttu-id="71a62-132">hello 下表描述 hello 可用屬性的端點，但它們是唯讀狀態。</span><span class="sxs-lookup"><span data-stu-id="71a62-132">hello following table describes hello available properties of endpoints, but they are read-only.</span></span> <span data-ttu-id="71a62-133">虛擬機器，tooadd 或編輯的 hello 端點使用 hello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkID=213885)。</span><span class="sxs-lookup"><span data-stu-id="71a62-133">tooadd or edit hello endpoints for a virtual machine, use hello [Azure classic portal](http://go.microsoft.com/fwlink/?LinkID=213885).</span></span> 
   
   | <span data-ttu-id="71a62-134">屬性</span><span class="sxs-lookup"><span data-stu-id="71a62-134">Property</span></span> | <span data-ttu-id="71a62-135">說明</span><span class="sxs-lookup"><span data-stu-id="71a62-135">Description</span></span> |
   | --- | --- |
   | <span data-ttu-id="71a62-136">名稱</span><span class="sxs-lookup"><span data-stu-id="71a62-136">Name</span></span> |<span data-ttu-id="71a62-137">Hello 端點識別碼。</span><span class="sxs-lookup"><span data-stu-id="71a62-137">An identifier for hello endpoint.</span></span> |
   | <span data-ttu-id="71a62-138">私人連接埠</span><span class="sxs-lookup"><span data-stu-id="71a62-138">Private Port</span></span> |<span data-ttu-id="71a62-139">網路存取內部 tooyour 應用程式的 hello 連接埠。</span><span class="sxs-lookup"><span data-stu-id="71a62-139">hello port for network access internal tooyour application.</span></span> |
   | <span data-ttu-id="71a62-140">通訊協定</span><span class="sxs-lookup"><span data-stu-id="71a62-140">Protocol</span></span> |<span data-ttu-id="71a62-141">使用 hello 這個端點的傳輸層的 hello 通訊協定，TCP 或 UDP。</span><span class="sxs-lookup"><span data-stu-id="71a62-141">hello protocol that hello transport layer for this endpoint uses, either TCP or UDP.</span></span> |
   | <span data-ttu-id="71a62-142">公用連接埠</span><span class="sxs-lookup"><span data-stu-id="71a62-142">Public Port</span></span> |<span data-ttu-id="71a62-143">hello 用於公用存取 tooyour 應用程式的連接埠。</span><span class="sxs-lookup"><span data-stu-id="71a62-143">hello port that’s used for public access tooyour application.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="71a62-144">後續步驟</span><span class="sxs-lookup"><span data-stu-id="71a62-144">Next steps</span></span>
<span data-ttu-id="71a62-145">進一步了解在 Visual Studio 中，使用 Azure 角色 toolearn 看到[透過 Azure 角色使用遠端桌面](vs-azure-tools-remote-desktop-roles.md)。</span><span class="sxs-lookup"><span data-stu-id="71a62-145">toolearn more about using Azure roles in Visual Studio, see [Using Remote Desktop with Azure Roles](vs-azure-tools-remote-desktop-roles.md).</span></span>

