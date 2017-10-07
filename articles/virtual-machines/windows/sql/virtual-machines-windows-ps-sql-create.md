---
title: "在 Azure PowerShell （資源管理員） 中的 SQL Server 虛擬機器 aaaCreate |Microsoft 文件"
description: "提供使用 SQL Server 虛擬機器資源庫映像建立 Azure VM 的步驟和 PowerShell 指令碼。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
editor: 
tags: azure-resource-manager
ms.assetid: 98d50dd8-48ad-444f-9031-5378d8270d7b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/17/2017
ms.author: jroth
ms.openlocfilehash: 2b8cb8f69ff9894a95eab617816a60c8674eeefa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-resource-manager"></a><span data-ttu-id="3ce23-103">使用 Azure PowerShell 佈建 SQL Server 虛擬機器 (Resource Manager)</span><span class="sxs-lookup"><span data-stu-id="3ce23-103">Provision a SQL Server virtual machine using Azure PowerShell (Resource Manager)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="3ce23-104">入口網站</span><span class="sxs-lookup"><span data-stu-id="3ce23-104">Portal</span></span>](virtual-machines-windows-portal-sql-server-provision.md)
> * [<span data-ttu-id="3ce23-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3ce23-105">PowerShell</span></span>](virtual-machines-windows-ps-sql-create.md)
>
>

## <a name="overview"></a><span data-ttu-id="3ce23-106">概觀</span><span class="sxs-lookup"><span data-stu-id="3ce23-106">Overview</span></span>
<span data-ttu-id="3ce23-107">本教學課程告訴您如何 toocreate 單一 Azure 虛擬機器使用 hello **Azure Resource Manager**部署模型，使用 Azure PowerShell cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3ce23-107">This tutorial shows you how toocreate a single Azure virtual machine using hello **Azure Resource Manager** deployment model using Azure PowerShell cmdlets.</span></span> <span data-ttu-id="3ce23-108">在此教學課程中，我們將建立單一的虛擬機器在 hello SQL 組件庫中使用單一磁碟機從映像。</span><span class="sxs-lookup"><span data-stu-id="3ce23-108">In this tutorial, we will create a single virtual machine using a single disk drive from an image in hello SQL Gallery.</span></span> <span data-ttu-id="3ce23-109">我們將建立新的提供者的 hello 儲存體、 網路和 hello 虛擬機器將使用的計算資源。</span><span class="sxs-lookup"><span data-stu-id="3ce23-109">We will create new providers for hello storage, network, and compute resources that will be used by hello virtual machine.</span></span> <span data-ttu-id="3ce23-110">如果上述任何資源有現有的提供者，您可以改用這些提供者。</span><span class="sxs-lookup"><span data-stu-id="3ce23-110">If you have existing providers for any of these resources, you can use those providers instead.</span></span>

<span data-ttu-id="3ce23-111">如果您需要 hello 傳統本主題的版本，請參閱[佈建 SQL Server 虛擬機器使用 Azure PowerShell 傳統](../classic/ps-sql-create.md)。</span><span class="sxs-lookup"><span data-stu-id="3ce23-111">If you need hello classic version of this topic, see [Provision a SQL Server virtual machine using Azure PowerShell Classic](../classic/ps-sql-create.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3ce23-112">必要條件</span><span class="sxs-lookup"><span data-stu-id="3ce23-112">Prerequisites</span></span>
<span data-ttu-id="3ce23-113">本教學課程中，您將需要：</span><span class="sxs-lookup"><span data-stu-id="3ce23-113">For this tutorial you'll need:</span></span>

* <span data-ttu-id="3ce23-114">在開始之前，您需要有 Azure 帳戶和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ce23-114">An Azure account and subscription before you start.</span></span> <span data-ttu-id="3ce23-115">如果您沒有帳戶，請註冊 [免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="3ce23-115">If you don't have one, sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="3ce23-116">[Azure PowerShell)](/powershell/azure/overview)，最低版本 1.4.0 或更新版本 (本教學課程是以 1.5.0 版撰寫)。</span><span class="sxs-lookup"><span data-stu-id="3ce23-116">[Azure PowerShell)](/powershell/azure/overview), minimum version of 1.4.0 or later (this tutorial written using version 1.5.0).</span></span>
  * <span data-ttu-id="3ce23-117">tooretrieve 程式版本中，輸入**Azure Get-module-ListAvailable**。</span><span class="sxs-lookup"><span data-stu-id="3ce23-117">tooretrieve your version, type **Get-Module Azure -ListAvailable**.</span></span>

## <a name="configure-your-subscription"></a><span data-ttu-id="3ce23-118">設定您的訂用帳戶</span><span class="sxs-lookup"><span data-stu-id="3ce23-118">Configure your subscription</span></span>
<span data-ttu-id="3ce23-119">開啟 Windows PowerShell 並執行下列 cmdlet 的 hello 建立存取 tooyour Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ce23-119">Open Windows PowerShell and establish access tooyour Azure account by running hello following cmdlet.</span></span> <span data-ttu-id="3ce23-120">您會有登入畫面 tooenter 您的認證。</span><span class="sxs-lookup"><span data-stu-id="3ce23-120">You will be presented with a sign in screen tooenter your credentials.</span></span> <span data-ttu-id="3ce23-121">使用 hello 相同電子郵件和密碼，您會使用 toosign toohello Azure 入口網站中。</span><span class="sxs-lookup"><span data-stu-id="3ce23-121">Use hello same email and password that you use toosign in toohello Azure portal.</span></span>

    Add-AzureRmAccount

<span data-ttu-id="3ce23-122">已成功登入之後您會看到一些資訊，其中包含您登入的 hello SubscriptionId 螢幕上。</span><span class="sxs-lookup"><span data-stu-id="3ce23-122">After successfully signing in you will see some information on screen that includes hello SubscriptionId with which you signed in.</span></span> <span data-ttu-id="3ce23-123">這是 hello 訂用帳戶中的 hello 本教學課程會建立資源除非您變更 tooa 不同訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ce23-123">This is hello subscription in which hello resources for this tutorial will be created unless you change tooa different subscription.</span></span> <span data-ttu-id="3ce23-124">如果您有多個訂用帳戶，執行下列 cmdlet tooreturn hello 所有您訂用帳戶的清單：</span><span class="sxs-lookup"><span data-stu-id="3ce23-124">If you have multiple SubscriptionIds, run hello following cmdlet tooreturn a list of all of your SubscriptionIds:</span></span>

    Get-AzureRmSubscription

<span data-ttu-id="3ce23-125">執行下列 cmdlet 與您想要的訂用帳戶 Id 的 hello toochange tooanother SubscriptionID、。</span><span class="sxs-lookup"><span data-stu-id="3ce23-125">toochange tooanother SubscriptionID, run hello following cmdlet with your desired SubscriptionId.</span></span>

    Select-AzureRmSubscription -SubscriptionId xxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx

## <a name="define-image-variables"></a><span data-ttu-id="3ce23-126">定義映像變數</span><span class="sxs-lookup"><span data-stu-id="3ce23-126">Define image variables</span></span>
<span data-ttu-id="3ce23-127">toosimplify 可用性與了解從本教學課程中的 hello 完成指令碼，我們一開始會定義變數的數目。</span><span class="sxs-lookup"><span data-stu-id="3ce23-127">toosimplify usability and understanding of hello completed script from this tutorial, we will start by defining a number of variables.</span></span> <span data-ttu-id="3ce23-128">當您，但修改提供的 hello 值時，請注意命名的限制相關的 tooname 長度和特殊字元，請變更 hello 參數值。</span><span class="sxs-lookup"><span data-stu-id="3ce23-128">Change hello parameter values as you see fit, but beware of naming restrictions related tooname lengths and special characters when modifying hello values provided.</span></span>

### <a name="location-and-resource-group"></a><span data-ttu-id="3ce23-129">位置和資源群組</span><span class="sxs-lookup"><span data-stu-id="3ce23-129">Location and Resource Group</span></span>
<span data-ttu-id="3ce23-130">使用兩個變數 toodefine hello 資料區域和 hello 資源群組到其中您將建立 hello hello 虛擬機器的其他資源。</span><span class="sxs-lookup"><span data-stu-id="3ce23-130">Use two variables toodefine hello data region and hello resource group into which you will create hello other resources for hello virtual machine.</span></span>

<span data-ttu-id="3ce23-131">請視需要修改，然後執行下列 cmdlet tooinitialize hello 這些變數。</span><span class="sxs-lookup"><span data-stu-id="3ce23-131">Modify as desired and then execute hello following cmdlets tooinitialize these variables.</span></span>

    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"

### <a name="storage-properties"></a><span data-ttu-id="3ce23-132">儲存體屬性</span><span class="sxs-lookup"><span data-stu-id="3ce23-132">Storage properties</span></span>
<span data-ttu-id="3ce23-133">使用下列變數 toodefine hello 儲存體帳戶和 hello 型別 hello 虛擬機器所使用的儲存體 toobe hello。</span><span class="sxs-lookup"><span data-stu-id="3ce23-133">Use hello following variables toodefine hello storage account and hello type of storage toobe used by hello virtual machine.</span></span>

<span data-ttu-id="3ce23-134">請視需要修改，然後執行下列 cmdlet tooinitialize hello 這些變數。</span><span class="sxs-lookup"><span data-stu-id="3ce23-134">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span> <span data-ttu-id="3ce23-135">請注意，在此範例中，我們使用 [進階儲存體](../../../storage/common/storage-premium-storage.md)，這是針對生產環境工作負載建議使用的儲存體。</span><span class="sxs-lookup"><span data-stu-id="3ce23-135">Note that in this example, we are using [Premium Storage](../../../storage/common/storage-premium-storage.md), which is recommended for production workloads.</span></span> <span data-ttu-id="3ce23-136">如需有關本指南及其他建議的詳細資料，請參閱 [Azure 虛擬機器中的 SQL Server 效能最佳做法](virtual-machines-windows-sql-performance.md)。</span><span class="sxs-lookup"><span data-stu-id="3ce23-136">For details on this guidance and other recommendations, see [Performance best practices for SQL Server in Azure Virtual Machines](virtual-machines-windows-sql-performance.md).</span></span>

    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

### <a name="network-properties"></a><span data-ttu-id="3ce23-137">網路屬性</span><span class="sxs-lookup"><span data-stu-id="3ce23-137">Network properties</span></span>
<span data-ttu-id="3ce23-138">使用下列變數 toodefine hello 網路介面、 hello TCP/IP 配置方法，hello 虛擬網路名稱、 hello 虛擬子網路名稱、 hello 虛擬網路的 hello 範圍的 IP 位址、 hello 的 IP 位址範圍的 hello 子網路和 hello hello公用網域名稱標籤 toobe hello 虛擬機器中的 hello 網路所使用。</span><span class="sxs-lookup"><span data-stu-id="3ce23-138">Use hello following variables toodefine hello network interface, hello TCP/IP allocation method, hello virtual network name, hello virtual subnet name, hello range of IP addresses for hello virtual network, hello range of IP addresses for hello subnet, and hello public domain name label toobe used by hello network in hello virtual machine.</span></span>

<span data-ttu-id="3ce23-139">請視需要修改，然後執行下列 cmdlet tooinitialize hello 這些變數。</span><span class="sxs-lookup"><span data-stu-id="3ce23-139">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $TCPIPAllocationMethod = "Dynamic"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $DomainName = "sqlvm1"

### <a name="virtual-machine-properties"></a><span data-ttu-id="3ce23-140">虛擬機器屬性</span><span class="sxs-lookup"><span data-stu-id="3ce23-140">Virtual machine properties</span></span>
<span data-ttu-id="3ce23-141">使用下列變數 toodefine hello 虛擬機器名稱、 hello 電腦名稱、 hello 虛擬機器大小和 hello hello 虛擬機器的作業系統磁碟名稱的 hello。</span><span class="sxs-lookup"><span data-stu-id="3ce23-141">Use hello following variables toodefine hello virtual machine name, hello computer name, hello virtual machine size, and hello operating system disk name for hello virtual machine.</span></span>

<span data-ttu-id="3ce23-142">請視需要修改，然後執行下列 cmdlet tooinitialize hello 這些變數。</span><span class="sxs-lookup"><span data-stu-id="3ce23-142">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

### <a name="image-properties"></a><span data-ttu-id="3ce23-143">映像屬性</span><span class="sxs-lookup"><span data-stu-id="3ce23-143">Image properties</span></span>
<span data-ttu-id="3ce23-144">使用下列變數 toodefine hello hello 虛擬機器的映像 toouse hello。</span><span class="sxs-lookup"><span data-stu-id="3ce23-144">Use hello following variables toodefine hello image toouse for hello virtual machine.</span></span> <span data-ttu-id="3ce23-145">在此範例中，會使用 hello SQL Server 2016 Enterprise 映像。</span><span class="sxs-lookup"><span data-stu-id="3ce23-145">In this example, hello SQL Server 2016 Enterprise image is used.</span></span>

<span data-ttu-id="3ce23-146">請視需要修改，然後執行下列 cmdlet tooinitialize hello 這些變數。</span><span class="sxs-lookup"><span data-stu-id="3ce23-146">Modify as desired and then execute hello following cmdlet tooinitialize these variables.</span></span>

    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

<span data-ttu-id="3ce23-147">請注意，您可以取得 SQL Server 映像供應項目與 hello Get AzureRmVMImageOffer 命令的完整清單：</span><span class="sxs-lookup"><span data-stu-id="3ce23-147">Note that you can get a full list of SQL Server image offerings with hello Get-AzureRmVMImageOffer command:</span></span>

    Get-AzureRmVMImageOffer -Location 'East US' -Publisher 'MicrosoftSQLServer'

<span data-ttu-id="3ce23-148">而且您可以看見 hello Sku 供 hello Get AzureRmVMImageSku 命令的供應項目。</span><span class="sxs-lookup"><span data-stu-id="3ce23-148">And you can see hello Skus available for an offering with hello Get-AzureRmVMImageSku command.</span></span> <span data-ttu-id="3ce23-149">hello 下列命令會顯示所有 Sku 供 hello **SQL2014SP1 WS2012R2**提供。</span><span class="sxs-lookup"><span data-stu-id="3ce23-149">hello following command shows all Skus available for hello **SQL2014SP1-WS2012R2** offer.</span></span>

    Get-AzureRmVMImageSku -Location 'East US' -Publisher 'MicrosoftSQLServer' -Offer 'SQL2014SP1-WS2012R2' | Select Skus

## <a name="create-a-resource-group"></a><span data-ttu-id="3ce23-150">建立資源群組</span><span class="sxs-lookup"><span data-stu-id="3ce23-150">Create a resource group</span></span>
<span data-ttu-id="3ce23-151">Hello Resource Manager 部署模型，與 hello 您所建立的第一個物件是 hello 資源群組。</span><span class="sxs-lookup"><span data-stu-id="3ce23-151">With hello Resource Manager deployment model, hello first object that you create is hello resource group.</span></span> <span data-ttu-id="3ce23-152">我們將使用 hello[新增 AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate Azure 資源群組和其資源與 hello 資源群組名稱與先前初始化的 hello 變數所定義的位置。</span><span class="sxs-lookup"><span data-stu-id="3ce23-152">We will use hello [New-AzureRmResourceGroup](/powershell/module/azurerm.resources/new-azurermresourcegroup) cmdlet toocreate an Azure resource group and its resources with hello resource group name and location defined by hello variables that you previously initialized.</span></span>

<span data-ttu-id="3ce23-153">執行下列 cmdlet toocreate hello 您新資源群組。</span><span class="sxs-lookup"><span data-stu-id="3ce23-153">Execute hello following cmdlet toocreate your new resource group.</span></span>

    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

## <a name="create-a-storage-account"></a><span data-ttu-id="3ce23-154">建立儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="3ce23-154">Create a storage account</span></span>
<span data-ttu-id="3ce23-155">hello 虛擬機器需要存放裝置資源 hello 作業系統磁碟和 hello SQL Server 資料和記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3ce23-155">hello virtual machine requires storage resources for hello operating system disk and for hello SQL Server data and log files.</span></span> <span data-ttu-id="3ce23-156">為了簡單起見，我們將針對兩者建立單一磁碟。</span><span class="sxs-lookup"><span data-stu-id="3ce23-156">For simplicity, we will create a single disk for both.</span></span> <span data-ttu-id="3ce23-157">您可以附加額外的磁碟，稍後再使用 hello[新增 Azure 磁碟](/powershell/module/azure/add-azuredisk)中的 cmdlet 順序 tooplace SQL Server 資料和專用磁碟上記錄檔。</span><span class="sxs-lookup"><span data-stu-id="3ce23-157">You can attach additional disks later using hello [Add-Azure Disk](/powershell/module/azure/add-azuredisk) cmdlet in order tooplace your SQL Server data and log files on dedicated disks.</span></span> <span data-ttu-id="3ce23-158">我們將使用 hello[新增 AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate 標準儲存體帳戶中新的資源群組和 hello 儲存體帳戶名稱、 儲存體 Sku 名稱，與使用 hello 變數定義的位置，您先前初始化。</span><span class="sxs-lookup"><span data-stu-id="3ce23-158">We will use hello [New-AzureRmStorageAccount](/powershell/module/azurerm.storage/new-azurermstorageaccount) cmdlet toocreate a standard storage account in your new resource group and with hello storage account name, storage Sku name, and location defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="3ce23-159">執行下列 cmdlet toocreate hello 新的儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ce23-159">Execute hello following cmdlet toocreate your new storage account.</span></span>

    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

## <a name="create-network-resources"></a><span data-ttu-id="3ce23-160">建立網路資源</span><span class="sxs-lookup"><span data-stu-id="3ce23-160">Create network resources</span></span>
<span data-ttu-id="3ce23-161">hello 虛擬機器需要的網路連線的網路資源數目。</span><span class="sxs-lookup"><span data-stu-id="3ce23-161">hello virtual machine requires a number of network resources for network connectivity.</span></span>

* <span data-ttu-id="3ce23-162">每部虛擬機器都需要虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="3ce23-162">Each virtual machine requires a virtual network.</span></span>
* <span data-ttu-id="3ce23-163">虛擬網路必須定義至少一個子網路。</span><span class="sxs-lookup"><span data-stu-id="3ce23-163">A virtual network must have at least one subnet defined.</span></span>
* <span data-ttu-id="3ce23-164">網路介面必須以公用或私人 IP 位址定義。</span><span class="sxs-lookup"><span data-stu-id="3ce23-164">A network interface must be defined with either a public or a private IP address.</span></span>

### <a name="create-a-virtual-network-subnet-configuration"></a><span data-ttu-id="3ce23-165">建立虛擬網路子網路組態</span><span class="sxs-lookup"><span data-stu-id="3ce23-165">Create a virtual network subnet configuration</span></span>
<span data-ttu-id="3ce23-166">我們首先會建立虛擬網路的子網路組態。</span><span class="sxs-lookup"><span data-stu-id="3ce23-166">We will start by creating a subnet configuration for our virtual network.</span></span> <span data-ttu-id="3ce23-167">教學課程中，我們將建立預設子網路使用 hello[新增 AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3ce23-167">For our tutorial, we will create a default subnet using hello [New-AzureRmVirtualNetworkSubnetConfig](/powershell/module/azurerm.network/new-azurermvirtualnetworksubnetconfig) cmdlet.</span></span> <span data-ttu-id="3ce23-168">我們將建立虛擬網路子網路組態設定與 hello 子網路名稱和位址定義的前置詞使用您先前初始化的 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="3ce23-168">We will create our virtual network subnet configuration with hello subnet name and address prefix defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="3ce23-169">您可以定義使用這個指令程式，hello 虛擬網路子網路組態的其他屬性，但這超出本教學課程的 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="3ce23-169">You can define additional properties of hello virtual network subnet configuration using this cmdlet, but that is beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="3ce23-170">執行下列 cmdlet toocreate hello 虛擬子網路組態。</span><span class="sxs-lookup"><span data-stu-id="3ce23-170">Execute hello following cmdlet toocreate your virtual subnet configuration.</span></span>

    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix

### <a name="create-a-virtual-network"></a><span data-ttu-id="3ce23-171">建立虛擬網路</span><span class="sxs-lookup"><span data-stu-id="3ce23-171">Create a virtual network</span></span>
<span data-ttu-id="3ce23-172">接下來，我們將建立虛擬網路使用 hello[新增 AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3ce23-172">Next, we will create our virtual network using hello [New-AzureRmVirtualNetwork](/powershell/module/azurerm.network/new-azurermvirtualnetwork) cmdlet.</span></span> <span data-ttu-id="3ce23-173">新資源群組，以 hello 名稱、 位置和位址定義的前置詞使用 hello 先前初始化的變數，以及使用 hello 在 hello 上一個步驟中所定義的子網路組態中，我們將建立虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="3ce23-173">We will create our virtual network in your new resource group, with hello name, location, and address prefix defined using hello variables that you previously initialized, and using hello subnet configuration that you defined in hello previous step.</span></span>

<span data-ttu-id="3ce23-174">執行下列 cmdlet toocreate hello 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="3ce23-174">Execute hello following cmdlet toocreate your virtual network.</span></span>

    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig

### <a name="create-hello-public-ip-address"></a><span data-ttu-id="3ce23-175">建立 hello 公用 IP 位址</span><span class="sxs-lookup"><span data-stu-id="3ce23-175">Create hello public IP address</span></span>
<span data-ttu-id="3ce23-176">現在我們有虛擬網路定義，我們需要 tooconfigure IP 位址連線 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3ce23-176">Now that we have our virtual network defined, we need tooconfigure an IP address for connectivity toohello virtual machine.</span></span> <span data-ttu-id="3ce23-177">此教學課程中，我們將建立使用動態 IP 位址 toosupport 網際網路連線的公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3ce23-177">For this tutorial, we will create a public IP address using dynamic IP addressing toosupport Internet connectivity.</span></span> <span data-ttu-id="3ce23-178">我們將使用 hello[新增 AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello 公用 IP 位址以 hello 資源群組建立先前和 hello 名稱、 位置、 配置方法，以及使用 hello 定義 DNS 網域名稱標籤您先前初始化的變數。</span><span class="sxs-lookup"><span data-stu-id="3ce23-178">We will use hello [New-AzureRmPublicIpAddress](/powershell/module/azurerm.network/new-azurermpublicipaddress) cmdlet toocreate hello public IP address in hello resource group created prevously and with hello name, location, allocation method, and DNS domain name label defined using hello variables that you previously initialized.</span></span>

> [!NOTE]
> <span data-ttu-id="3ce23-179">您可以定義 hello 使用這個指令程式，公用 IP 位址的其他屬性，但這超出本教學課程中初始 hello 範圍。</span><span class="sxs-lookup"><span data-stu-id="3ce23-179">You can define additional properties of hello public IP address using this cmdlet, but that is beyond hello scope of this initial tutorial.</span></span> <span data-ttu-id="3ce23-180">您也可以建立私用位址，且具有靜態位址，但其同時也是本教學課程的 hello 範圍之外。</span><span class="sxs-lookup"><span data-stu-id="3ce23-180">You could also create a private address or an address with a static address, but that is also beyond hello scope of this tutorial.</span></span>
>
>

<span data-ttu-id="3ce23-181">執行下列 cmdlet toocreate hello 公用 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="3ce23-181">Execute hello following cmdlet toocreate your public IP address.</span></span>

    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName

### <a name="create-hello-network-interface"></a><span data-ttu-id="3ce23-182">建立 hello 網路介面</span><span class="sxs-lookup"><span data-stu-id="3ce23-182">Create hello network interface</span></span>
<span data-ttu-id="3ce23-183">我們現在是我們的虛擬機器將使用的準備 toocreate hello 網路介面。</span><span class="sxs-lookup"><span data-stu-id="3ce23-183">We are now ready toocreate hello network interface that our virtual machine will use.</span></span> <span data-ttu-id="3ce23-184">我們將使用 hello[新增 AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate 先前定義我們稍早建立的 hello 資源群組，並使用 hello 名稱、 位置、 子網路和公用 IP 位址的網路介面。</span><span class="sxs-lookup"><span data-stu-id="3ce23-184">We will use hello [New-AzureRmNetworkInterface](/powershell/module/azurerm.network/new-azurermnetworkinterface) cmdlet toocreate our network interface in hello resource group created earlier and with hello name, location, subnet and public IP address previously defined.</span></span>

<span data-ttu-id="3ce23-185">執行下列 cmdlet toocreate hello 您的網路介面。</span><span class="sxs-lookup"><span data-stu-id="3ce23-185">Execute hello following cmdlet toocreate your network interface.</span></span>

    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

## <a name="configure-a-vm-object"></a><span data-ttu-id="3ce23-186">設定 VM 物件</span><span class="sxs-lookup"><span data-stu-id="3ce23-186">Configure a VM object</span></span>
<span data-ttu-id="3ce23-187">現在，我們已經定義的儲存體和網路資源，我們會準備 toodefine hello 虛擬機器計算資源。</span><span class="sxs-lookup"><span data-stu-id="3ce23-187">Now that we have storage and network resources defined, we are ready toodefine compute resources for hello virtual machine.</span></span> <span data-ttu-id="3ce23-188">教學課程中，我們會指定 hello 虛擬機器大小和各種作業系統屬性指定 hello 先前建立的網路介面，定義 blob 儲存體，，然後指定 hello 作業系統磁碟。</span><span class="sxs-lookup"><span data-stu-id="3ce23-188">For our tutorial, we will specify hello virtual machine size and various operating system properties, specify hello network interface that we previously created, define blob storage, and then specify hello operating system disk.</span></span>

### <a name="create-hello-vm-object"></a><span data-ttu-id="3ce23-189">建立 hello VM 物件</span><span class="sxs-lookup"><span data-stu-id="3ce23-189">Create hello VM object</span></span>
<span data-ttu-id="3ce23-190">我們一開始會指定 hello 虛擬機器大小。</span><span class="sxs-lookup"><span data-stu-id="3ce23-190">We will start by specifying hello virtual machine size.</span></span> <span data-ttu-id="3ce23-191">在本教學課程諸ㄥ，我們會指定 DS13。</span><span class="sxs-lookup"><span data-stu-id="3ce23-191">For this tutorial, we are specifying a DS13.</span></span> <span data-ttu-id="3ce23-192">我們將使用 hello[新增 AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate hello 名稱與使用您先前初始化的 hello 變數定義的大小可設定的虛擬機器物件。</span><span class="sxs-lookup"><span data-stu-id="3ce23-192">We will use hello [New-AzureRmVMConfig](/powershell/module/azurerm.compute/new-azurermvmconfig) cmdlet toocreate a configurable virtual machine object with hello name and size defined using hello variables that you previously initialized.</span></span>

<span data-ttu-id="3ce23-193">執行下列 cmdlet toocreate hello 虛擬機器物件的 hello。</span><span class="sxs-lookup"><span data-stu-id="3ce23-193">Execute hello following cmdlet toocreate hello virtual machine object.</span></span>

    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize

### <a name="create-a-credential-object-toohold-hello-name-and-password-for-hello-local-administrator-credentials"></a><span data-ttu-id="3ce23-194">建立認證物件 toohold hello 名稱與 hello 本機系統管理員認證的密碼</span><span class="sxs-lookup"><span data-stu-id="3ce23-194">Create a credential object toohold hello name and password for hello local administrator credentials</span></span>
<span data-ttu-id="3ce23-195">我們可以設定 hello hello 虛擬機器的作業系統內容之前，我們需要 toosupply hello 認證 hello 本機系統管理員帳戶為安全字串。</span><span class="sxs-lookup"><span data-stu-id="3ce23-195">Before we can set hello operating system properties for hello virtual machine, we need toosupply hello credentials for hello local administrator account as a secure string.</span></span> <span data-ttu-id="3ce23-196">tooaccomplish，我們將使用 hello [Get-credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet。</span><span class="sxs-lookup"><span data-stu-id="3ce23-196">tooaccomplish this, we will use hello [Get-Credential](https://technet.microsoft.com/library/hh849815.aspx) cmdlet.</span></span>

<span data-ttu-id="3ce23-197">執行下列 cmdlet 的 hello 和 hello Windows PowerShell 認證要求在視窗中，輸入 hello hello hello Windows 虛擬機器中的本機系統管理員帳戶的名稱和密碼 toouse。</span><span class="sxs-lookup"><span data-stu-id="3ce23-197">Execute hello following cmdlet and, in hello Windows PowerShell credential request window, type hello name and password toouse for hello local administrator account in hello Windows virtual machine.</span></span>

    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."

### <a name="set-hello-operating-system-properties-for-hello-virtual-machine"></a><span data-ttu-id="3ce23-198">設定 hello hello 虛擬機器的作業系統屬性</span><span class="sxs-lookup"><span data-stu-id="3ce23-198">Set hello operating system properties for hello virtual machine</span></span>
<span data-ttu-id="3ce23-199">現在我們已經準備好 tooset hello 虛擬機器的作業系統內容。</span><span class="sxs-lookup"><span data-stu-id="3ce23-199">Now we are ready tooset hello virtual machine's operating system properties.</span></span> <span data-ttu-id="3ce23-200">我們將使用 hello[組 AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem)作業系統為 Windows，cmdlet tooset hello 類型需要 hello[虛擬機器代理程式](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)toobe 安裝，可讓您指定 hello 指令程式可讓自動更新並設定 hello 虛擬機器名稱、 hello 電腦名稱及使用您先前初始化的 hello 變數 hello 認證。</span><span class="sxs-lookup"><span data-stu-id="3ce23-200">We will use hello [Set-AzureRmVMOperatingSystem](/powershell/module/azurerm.compute/set-azurermvmoperatingsystem) cmdlet tooset hello type of operating system as Windows, require hello [virtual machine agent](../classic/agents-and-extensions.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json) toobe installed, specify that hello cmdlet enables auto update and set hello virtual machine name, hello computer name, and hello credential using hello variables that you previously initialized.</span></span>

<span data-ttu-id="3ce23-201">執行下列 cmdlet tooset hello 作業系統屬性為您的虛擬機器的 hello。</span><span class="sxs-lookup"><span data-stu-id="3ce23-201">Execute hello following cmdlet tooset hello operating system properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate

### <a name="add-hello-network-interface-toohello-virtual-machine"></a><span data-ttu-id="3ce23-202">新增 hello 網路介面 toohello 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="3ce23-202">Add hello network interface toohello virtual machine</span></span>
<span data-ttu-id="3ce23-203">接下來，我們將加入 hello 我們先前建立 toohello 虛擬機器的網路介面。</span><span class="sxs-lookup"><span data-stu-id="3ce23-203">Next, we will add hello network interface that we created previously toohello virtual machine.</span></span> <span data-ttu-id="3ce23-204">我們將使用 hello[新增 AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd hello 網路介面使用您先前定義的 hello 網路介面變數。</span><span class="sxs-lookup"><span data-stu-id="3ce23-204">We will use hello [Add-AzureRmVMNetworkInterface](/powershell/module/azurerm.compute/add-azurermvmnetworkinterface) cmdlet tooadd hello network interface using hello network interface variable that you defined earlier.</span></span>

<span data-ttu-id="3ce23-205">執行下列 cmdlet tooset hello 之虛擬機器的網路介面的 hello。</span><span class="sxs-lookup"><span data-stu-id="3ce23-205">Execute hello following cmdlet tooset hello network interface for your virtual machine.</span></span>

    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id

### <a name="set-hello-blob-storage-location-for-hello-disk-toobe-used-by-hello-virtual-machine"></a><span data-ttu-id="3ce23-206">設定 hello hello 磁碟 toobe hello 虛擬機器所使用的 blob 儲存體位置</span><span class="sxs-lookup"><span data-stu-id="3ce23-206">Set hello blob storage location for hello disk toobe used by hello virtual machine</span></span>
<span data-ttu-id="3ce23-207">接下來，我們會設定為使用您先前定義的 hello 變數 hello 虛擬機器所使用的 hello 磁碟 toobe hello blob 儲存體位置。</span><span class="sxs-lookup"><span data-stu-id="3ce23-207">Next, we will set hello blob storage location for hello disk toobe used by hello virtual machine using hello variables that you defined earlier.</span></span>

<span data-ttu-id="3ce23-208">執行下列 cmdlet tooset hello blob 儲存體位置的 hello。</span><span class="sxs-lookup"><span data-stu-id="3ce23-208">Execute hello following cmdlet tooset hello blob storage location.</span></span>

    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"

### <a name="set-hello-operating-system-disk-properties-for-hello-virtual-machine"></a><span data-ttu-id="3ce23-209">設定 hello 作業系統 hello 虛擬機器的磁碟內容</span><span class="sxs-lookup"><span data-stu-id="3ce23-209">Set hello operating system disk properties for hello virtual machine</span></span>
<span data-ttu-id="3ce23-210">接下來，我們會設定 hello 作業系統磁碟屬性 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3ce23-210">Next, we will set hello operating system disk properties for hello virtual machine.</span></span> <span data-ttu-id="3ce23-211">我們將使用 hello[組 AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify hello hello 虛擬機器的作業系統，將來自映像時，快取只 tooread tooset (因為 hello 上安裝 SQL Server 相同的磁碟)，並定義hello 虛擬機器名稱和 hello 作業系統磁碟使用 hello 我們先前定義的變數定義。</span><span class="sxs-lookup"><span data-stu-id="3ce23-211">We will use hello [Set-AzureRmVMOSDisk](/powershell/module/azurerm.compute/set-azurermvmosdisk) cmdlet toospecify that hello operating system for hello virtual machine will come from an image, tooset caching tooread only (because SQL Server is being installed on hello same disk) and define hello virtual machine name and hello operating system disk defined using hello variables that we defined earlier.</span></span>

<span data-ttu-id="3ce23-212">執行下列 cmdlet tooset hello 作業系統磁碟屬性為您的虛擬機器的 hello。</span><span class="sxs-lookup"><span data-stu-id="3ce23-212">Execute hello following cmdlet tooset hello operating system disk properties for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

### <a name="specify-hello-platform-image-for-hello-virtual-machine"></a><span data-ttu-id="3ce23-213">指定 hello hello 虛擬機器的平台映像</span><span class="sxs-lookup"><span data-stu-id="3ce23-213">Specify hello platform image for hello virtual machine</span></span>
<span data-ttu-id="3ce23-214">我們最後的組態步驟是我們的虛擬機器的 toospecify hello 平台映像。</span><span class="sxs-lookup"><span data-stu-id="3ce23-214">Our last configuration step is toospecify hello platform image for our virtual machine.</span></span> <span data-ttu-id="3ce23-215">教學課程中，我們使用 hello 最新的 SQL Server 2016 CTP 映像。</span><span class="sxs-lookup"><span data-stu-id="3ce23-215">For our tutorial, we are using hello latest SQL Server 2016 CTP image.</span></span> <span data-ttu-id="3ce23-216">我們將使用 hello[組 AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse 先前定義的 hello 變數所定義，此映像。</span><span class="sxs-lookup"><span data-stu-id="3ce23-216">We will use hello [Set-AzureRmVMSourceImage](/powershell/module/azurerm.compute/set-azurermvmsourceimage) cmdlet toouse this image as defined by hello variables that you defined earlier.</span></span>

<span data-ttu-id="3ce23-217">執行下列 cmdlet toospecify hello 平台映像的虛擬機器的 hello。</span><span class="sxs-lookup"><span data-stu-id="3ce23-217">Execute hello following cmdlet toospecify hello platform image for your virtual machine.</span></span>

    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

## <a name="create-hello-sql-vm"></a><span data-ttu-id="3ce23-218">建立 hello SQL VM</span><span class="sxs-lookup"><span data-stu-id="3ce23-218">Create hello SQL VM</span></span>
<span data-ttu-id="3ce23-219">現在完成 hello 組態步驟後，您就準備好 toocreate hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3ce23-219">Now that you have finished hello configuration steps, you are ready toocreate hello virtual machine.</span></span> <span data-ttu-id="3ce23-220">我們將使用 hello[新增 AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello 虛擬機器使用，我們已定義的 hello 變數。</span><span class="sxs-lookup"><span data-stu-id="3ce23-220">We will use hello [New-AzureRmVM](/powershell/module/azurerm.compute/new-azurermvm) cmdlet toocreate hello virtual machine using hello variables that we have defined.</span></span>

<span data-ttu-id="3ce23-221">執行下列 cmdlet toocreate hello 您的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3ce23-221">Execute hello following cmdlet toocreate your virtual machine.</span></span>

    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

<span data-ttu-id="3ce23-222">建立 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="3ce23-222">hello virtual machine is created.</span></span> <span data-ttu-id="3ce23-223">請注意，標準儲存體帳戶已建立的開機診斷，因為 hello 指定 hello 虛擬機器的磁碟儲存體帳戶是進階儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="3ce23-223">Notice that a standard storage account is created for boot diagnostics because hello specified storage account for hello virtual machine's disk is a premium storage account.</span></span>

<span data-ttu-id="3ce23-224">您現在可以檢視此機器在 hello Azure 入口網站 toosee[公用 IP 位址和其完整的網域名稱](virtual-machines-windows-portal-sql-server-provision.md)。</span><span class="sxs-lookup"><span data-stu-id="3ce23-224">You can now view this machine in hello Azure Portal toosee [its public IP address and its fully qualified domain name](virtual-machines-windows-portal-sql-server-provision.md).</span></span>

## <a name="example-script"></a><span data-ttu-id="3ce23-225">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="3ce23-225">Example script</span></span>
<span data-ttu-id="3ce23-226">hello 下列指令碼包含 hello 完整的 PowerShell 指令碼在此教學課程。</span><span class="sxs-lookup"><span data-stu-id="3ce23-226">hello following script contains hello complete PowerShell script for this tutorial.</span></span> <span data-ttu-id="3ce23-227">它會假設您已經安裝 hello Azure 訂用帳戶 toouse 以 hello**新增 AzureRmAccount**和**選取 AzureRmSubscription**命令。</span><span class="sxs-lookup"><span data-stu-id="3ce23-227">It assumes that you have already setup hello Azure subscription toouse with hello **Add-AzureRmAccount** and **Select-AzureRmSubscription** commands.</span></span>

    # Variables
    ## Global
    $Location = "SouthCentralUS"
    $ResourceGroupName = "sqlvm1"
    ## Storage
    $StorageName = $ResourceGroupName + "storage"
    $StorageSku = "Premium_LRS"

    ## Network
    $InterfaceName = $ResourceGroupName + "ServerInterface"
    $VNetName = $ResourceGroupName + "VNet"
    $SubnetName = "Default"
    $VNetAddressPrefix = "10.0.0.0/16"
    $VNetSubnetAddressPrefix = "10.0.0.0/24"
    $TCPIPAllocationMethod = "Dynamic"
    $DomainName = "sqlvm1"

    ##Compute
    $VMName = $ResourceGroupName + "VM"
    $ComputerName = $ResourceGroupName + "Server"
    $VMSize = "Standard_DS13"
    $OSDiskName = $VMName + "OSDisk"

    ##Image
    $PublisherName = "MicrosoftSQLServer"
    $OfferName = "SQL2016-WS2016"
    $Sku = "Enterprise"
    $Version = "latest"

    # Resource Group
    New-AzureRmResourceGroup -Name $ResourceGroupName -Location $Location

    # Storage
    $StorageAccount = New-AzureRmStorageAccount -ResourceGroupName $ResourceGroupName -Name $StorageName -SkuName $StorageSku -Kind "Storage" -Location $Location

    # Network
    $SubnetConfig = New-AzureRmVirtualNetworkSubnetConfig -Name $SubnetName -AddressPrefix $VNetSubnetAddressPrefix
    $VNet = New-AzureRmVirtualNetwork -Name $VNetName -ResourceGroupName $ResourceGroupName -Location $Location -AddressPrefix $VNetAddressPrefix -Subnet $SubnetConfig
    $PublicIp = New-AzureRmPublicIpAddress -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -AllocationMethod $TCPIPAllocationMethod -DomainNameLabel $DomainName
    $Interface = New-AzureRmNetworkInterface -Name $InterfaceName -ResourceGroupName $ResourceGroupName -Location $Location -SubnetId $VNet.Subnets[0].Id -PublicIpAddressId $PublicIp.Id

    # Compute
    $VirtualMachine = New-AzureRmVMConfig -VMName $VMName -VMSize $VMSize
    $Credential = Get-Credential -Message "Type hello name and password of hello local administrator account."
    $VirtualMachine = Set-AzureRmVMOperatingSystem -VM $VirtualMachine -Windows -ComputerName $ComputerName -Credential $Credential -ProvisionVMAgent -EnableAutoUpdate #-TimeZone = $TimeZone
    $VirtualMachine = Add-AzureRmVMNetworkInterface -VM $VirtualMachine -Id $Interface.Id
    $OSDiskUri = $StorageAccount.PrimaryEndpoints.Blob.ToString() + "vhds/" + $OSDiskName + ".vhd"
    $VirtualMachine = Set-AzureRmVMOSDisk -VM $VirtualMachine -Name $OSDiskName -VhdUri $OSDiskUri -Caching ReadOnly -CreateOption FromImage

    # Image
    $VirtualMachine = Set-AzureRmVMSourceImage -VM $VirtualMachine -PublisherName $PublisherName -Offer $OfferName -Skus $Sku -Version $Version

    ## Create hello VM in Azure
    New-AzureRmVM -ResourceGroupName $ResourceGroupName -Location $Location -VM $VirtualMachine

## <a name="next-steps"></a><span data-ttu-id="3ce23-228">後續步驟</span><span class="sxs-lookup"><span data-stu-id="3ce23-228">Next steps</span></span>
<span data-ttu-id="3ce23-229">建立 hello 虛擬機器之後，您就準備好 tooconnect toohello 虛擬機器使用 RDP 和安裝程式的連線能力。</span><span class="sxs-lookup"><span data-stu-id="3ce23-229">After hello virtual machine is created, you are ready tooconnect toohello virtual machine using RDP and setup connectivity.</span></span> <span data-ttu-id="3ce23-230">如需詳細資訊，請參閱[連接 tooa Azure （資源管理員） 上的 SQL Server 虛擬機器](virtual-machines-windows-sql-connect.md)。</span><span class="sxs-lookup"><span data-stu-id="3ce23-230">For more information, see [Connect tooa SQL Server Virtual Machine on Azure (Resource Manager)](virtual-machines-windows-sql-connect.md).</span></span>

