---
title: "aaaManage Azure 端點的存取控制清單 |PowerShell |傳統 |Microsoft 文件"
description: "深入了解如何使用 PowerShell 的 Acl toomanage"
services: virtual-network
documentationcenter: na
author: jimdial
manager: carmonm
editor: tysonn
ms.assetid: c84e40af-f351-4572-b3f0-d572d46bafe7
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 03/15/2016
ms.author: jdial
ms.openlocfilehash: a7ca241ea108a266085bfb689b742d781e58da1c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-endpoint-access-control-lists-using-powershell-in-hello-classic-deployment-model"></a><span data-ttu-id="772b7-103">管理端點的存取控制清單在 hello 傳統部署模型中使用 PowerShell</span><span class="sxs-lookup"><span data-stu-id="772b7-103">Manage endpoint access control lists using PowerShell in hello classic deployment model</span></span>
<span data-ttu-id="772b7-104">您可以建立和管理網路存取控制清單 (Acl) 端點使用 Azure PowerShell 或 hello 管理入口網站中。</span><span class="sxs-lookup"><span data-stu-id="772b7-104">You can create and manage Network Access Control Lists (ACLs) for endpoints by using Azure PowerShell or in hello Management Portal.</span></span> <span data-ttu-id="772b7-105">在本主題中，您會了解一些可使用 PowerShell 完成 ACL 一般工作的程序。</span><span class="sxs-lookup"><span data-stu-id="772b7-105">In this topic, you'll find procedures for ACL common tasks that you can complete using PowerShell.</span></span> <span data-ttu-id="772b7-106">Hello 清單的 Azure PowerShell cmdlet，請參閱[Azure 管理 Cmdlet](http://go.microsoft.com/fwlink/?LinkId=317721)。</span><span class="sxs-lookup"><span data-stu-id="772b7-106">For hello list of Azure PowerShell cmdlets see [Azure Management Cmdlets](http://go.microsoft.com/fwlink/?LinkId=317721).</span></span> <span data-ttu-id="772b7-107">如需有關 ACL 的詳細資訊，請參閱＜ [什麼是網路存取控制清單 (ACL)？](virtual-networks-acl.md)＞。</span><span class="sxs-lookup"><span data-stu-id="772b7-107">For more information about ACLs, see [What is a Network Access Control List (ACL)?](virtual-networks-acl.md).</span></span> <span data-ttu-id="772b7-108">如果您想要 toomanage Acl hello 管理入口網站，請參閱[如何 tooSet 端點 tooa 虛擬機器](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="772b7-108">If you want toomanage your ACLs by using hello Management Portal, see [How tooSet Up Endpoints tooa Virtual Machine](../virtual-machines/windows/classic/setup-endpoints.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json).</span></span>

## <a name="manage-network-acls-by-using-azure-powershell"></a><span data-ttu-id="772b7-109">使用 Azure PowerShell 來管理網路 ACL</span><span class="sxs-lookup"><span data-stu-id="772b7-109">Manage Network ACLs by using Azure PowerShell</span></span>
<span data-ttu-id="772b7-110">您可以使用 Azure PowerShell cmdlet toocreate、 移除和設定 (set) 網路存取控制清單 (Acl)。</span><span class="sxs-lookup"><span data-stu-id="772b7-110">You can use Azure PowerShell cmdlets toocreate, remove, and configure (set) Network Access Control Lists (ACLs).</span></span> <span data-ttu-id="772b7-111">我們包含了一些您可以設定使用 PowerShell 的 ACL 的 hello 方法的一些範例。</span><span class="sxs-lookup"><span data-stu-id="772b7-111">We've included a few examples of some of hello ways you can configure an ACL using PowerShell.</span></span>

<span data-ttu-id="772b7-112">tooretrieve hello ACL PowerShell 指令程式的完整清單，您可以使用 hello 下列其中一項：</span><span class="sxs-lookup"><span data-stu-id="772b7-112">tooretrieve a complete list of hello ACL PowerShell cmdlets, you can use either of hello following:</span></span>

    Get-Help *AzureACL*
    Get-Command -Noun AzureACLConfig

### <a name="create-a-network-acl-with-rules-that-permit-access-from-a-remote-subnet"></a><span data-ttu-id="772b7-113">建立網路 ACL 搭配規則以允許從遠端子網路進行存取</span><span class="sxs-lookup"><span data-stu-id="772b7-113">Create a Network ACL with rules that permit access from a remote subnet</span></span>
<span data-ttu-id="772b7-114">hello 下列範例所示方式 toocreate 包含規則的新 ACL。</span><span class="sxs-lookup"><span data-stu-id="772b7-114">hello example below illustrates a way toocreate a new ACL that contains rules.</span></span> <span data-ttu-id="772b7-115">此 ACL 隨後將套用 tooa 虛擬機器端點。</span><span class="sxs-lookup"><span data-stu-id="772b7-115">This ACL is then applied tooa virtual machine endpoint.</span></span> <span data-ttu-id="772b7-116">在 hello 面範例中的 hello ACL 規則將允許從遠端子網路的存取。</span><span class="sxs-lookup"><span data-stu-id="772b7-116">hello ACL rules in hello example below will allow access from a remote subnet.</span></span> <span data-ttu-id="772b7-117">新的網路 ACL 對遠端子網路，允許規則與 toocreate 開啟 Azure PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="772b7-117">toocreate a new Network ACL with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="772b7-118">複製和貼上 hello 下方，使用您自己的值，設定 hello 指令碼的指令碼，然後執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="772b7-118">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="772b7-119">建立 hello 新的網路 ACL 物件。</span><span class="sxs-lookup"><span data-stu-id="772b7-119">Create hello new network ACL object.</span></span>
   
        $acl1 = New-AzureAclConfig
2. <span data-ttu-id="772b7-120">設定規則以允許從遠端子網路進行存取。</span><span class="sxs-lookup"><span data-stu-id="772b7-120">Set a rule that permits access from a remote subnet.</span></span> <span data-ttu-id="772b7-121">在 hello 下列範例中，您可以設定規則*100* （優先順序高於 200 及以上） tooallow hello 遠端子網路*10.0.0.0/8*存取 toohello 虛擬機器端點。</span><span class="sxs-lookup"><span data-stu-id="772b7-121">In hello example below, you set rule *100* (which has priority over rule 200 and higher) tooallow hello remote subnet *10.0.0.0/8* access toohello virtual machine endpoint.</span></span> <span data-ttu-id="772b7-122">Hello 值取代為您自己的組態需求。</span><span class="sxs-lookup"><span data-stu-id="772b7-122">Replace hello values with your own configuration requirements.</span></span> <span data-ttu-id="772b7-123">hello 名稱"SharePoint ACL config"應該取代 hello 您要 toocall 此規則的好記名稱。</span><span class="sxs-lookup"><span data-stu-id="772b7-123">hello name "SharePoint ACL config" should be replaced with hello friendly name that you want toocall this rule.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "SharePoint ACL config"
3. <span data-ttu-id="772b7-124">針對其他規則，請重複 hello cmdlet，hello 值取代為您自己的組態需求。</span><span class="sxs-lookup"><span data-stu-id="772b7-124">For additional rules, repeat hello cmdlet, replacing hello values with your own configuration requirements.</span></span> <span data-ttu-id="772b7-125">為確定 toochange hello 規則順序 tooreflect hello 依照您想要套用的 hello 規則 toobe。</span><span class="sxs-lookup"><span data-stu-id="772b7-125">Be sure toochange hello rule number Order tooreflect hello order in which you want hello rules toobe applied.</span></span> <span data-ttu-id="772b7-126">hello 低的規則數會優先於 hello 高的數字。</span><span class="sxs-lookup"><span data-stu-id="772b7-126">hello lower rule number takes precedence over hello higher number.</span></span>
   
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
4. <span data-ttu-id="772b7-127">接下來，您可以建立新的端點 (Add)，或設定現有端點 (Set) 的 hello ACL。</span><span class="sxs-lookup"><span data-stu-id="772b7-127">Next, you can either create a new endpoint (Add) or set hello ACL for an existing endpoint (Set).</span></span> <span data-ttu-id="772b7-128">在此範例中，我們將加入新的虛擬機器端點呼叫 hello 與"web"並更新 hello 虛擬機器端點 ACL 設定。</span><span class="sxs-lookup"><span data-stu-id="772b7-128">In this example, we will add a new virtual machine endpoint called "web" and update hello virtual machine endpoint with hello ACL settings.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        | Update-AzureVM
5. <span data-ttu-id="772b7-129">接著，結合 hello cmdlet，並執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="772b7-129">Next, combine hello cmdlets and run hello script.</span></span> <span data-ttu-id="772b7-130">例如，hello 結合各指令程式會看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="772b7-130">For this example, hello combined cmdlets would look like this:</span></span>
   
        $acl1 = New-AzureAclConfig
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 100 `
            –Action permit –RemoteSubnet "10.0.0.0/8" `
            –Description "Sharepoint ACL config"
        Set-AzureAclConfig –AddRule –ACL $acl1 –Order 200 `
            –Action permit –RemoteSubnet "157.0.0.0/8" `
            –Description "web frontend ACL config"
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        |Add-AzureEndpoint –Name "web" –Protocol tcp –Localport 80 - PublicPort 80 –ACL $acl1 `
        |Update-AzureVM

### <a name="remove-a-network-acl-rule-that-permits-access-from-a-remote-subnet"></a><span data-ttu-id="772b7-131">設定網路 ACL 規則以允許從遠端子網路進行存取</span><span class="sxs-lookup"><span data-stu-id="772b7-131">Remove a Network ACL rule that permits access from a remote subnet</span></span>
<span data-ttu-id="772b7-132">hello 下列範例所示方式 tooremove 網路 ACL 規則。</span><span class="sxs-lookup"><span data-stu-id="772b7-132">hello example below illustrates a way tooremove a network ACL rule.</span></span>  <span data-ttu-id="772b7-133">tooremove 的網路 ACL 規則，以允許規則對遠端子網路中，開啟 Azure PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="772b7-133">tooremove a Network ACL rule with permit rules for a remote subnet, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="772b7-134">複製和貼上 hello 下方，使用您自己的值，設定 hello 指令碼的指令碼，然後執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="772b7-134">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

1. <span data-ttu-id="772b7-135">第一個步驟是針對 hello 虛擬機器端點 tooget hello 網路 ACL 物件。</span><span class="sxs-lookup"><span data-stu-id="772b7-135">First step is tooget hello Network ACL object for hello virtual machine endpoint.</span></span> <span data-ttu-id="772b7-136">然後，您要移除 hello ACL 規則。</span><span class="sxs-lookup"><span data-stu-id="772b7-136">You'll then remove hello ACL rule.</span></span> <span data-ttu-id="772b7-137">在此案例中，我們依據規則 ID 進行移除。</span><span class="sxs-lookup"><span data-stu-id="772b7-137">In this case, we are removing it by rule ID.</span></span> <span data-ttu-id="772b7-138">這只會移除 hello 規則 ID 0 從 hello ACL。</span><span class="sxs-lookup"><span data-stu-id="772b7-138">This will only remove hello rule ID 0 from hello ACL.</span></span> <span data-ttu-id="772b7-139">它不會移除 hello ACL 物件 hello 虛擬機器端點。</span><span class="sxs-lookup"><span data-stu-id="772b7-139">It does not remove hello ACL object from hello virtual machine endpoint.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Get-AzureAclConfig –EndpointName "web" `
        | Set-AzureAclConfig –RemoveRule –ID 0 –ACL $acl1
2. <span data-ttu-id="772b7-140">接下來，您必須套用 hello 網路 ACL 物件 toohello 虛擬機器端點，並且更新 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="772b7-140">Next, you must apply hello Network ACL object toohello virtual machine endpoint and update hello virtual machine.</span></span>
   
        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Set-AzureEndpoint –ACL $acl1 –Name "web" `
        | Update-AzureVM

### <a name="remove-a-network-acl-from-a-virtual-machine-endpoint"></a><span data-ttu-id="772b7-141">從虛擬機器端點移除網路 ACL</span><span class="sxs-lookup"><span data-stu-id="772b7-141">Remove a Network ACL from a virtual machine endpoint</span></span>
<span data-ttu-id="772b7-142">在某些情況下，您可能想 tooremove 從虛擬機器端點的網路 ACL 物件。</span><span class="sxs-lookup"><span data-stu-id="772b7-142">In certain scenarios, you might want tooremove a Network ACL object from a virtual machine endpoint.</span></span> <span data-ttu-id="772b7-143">toodo，開啟 Azure PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="772b7-143">toodo that, open an Azure PowerShell ISE.</span></span> <span data-ttu-id="772b7-144">複製和貼上 hello 下方，使用您自己的值，設定 hello 指令碼的指令碼，然後執行 hello 指令碼。</span><span class="sxs-lookup"><span data-stu-id="772b7-144">Copy and paste hello script below, configuring hello script with your own values, and then run hello script.</span></span>

        Get-AzureVM –ServiceName $serviceName –Name $vmName `
        | Remove-AzureAclConfig –EndpointName "web" `
        | Update-AzureVM

## <a name="next-steps"></a><span data-ttu-id="772b7-145">後續步驟</span><span class="sxs-lookup"><span data-stu-id="772b7-145">Next steps</span></span>
[<span data-ttu-id="772b7-146">什麼是網路存取控制清單 (ACL)？</span><span class="sxs-lookup"><span data-stu-id="772b7-146">What is a Network Access Control List (ACL)?</span></span>](virtual-networks-acl.md)

