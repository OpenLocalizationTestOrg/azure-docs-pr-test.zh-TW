---
title: "使用 PowerShell 的 Windows VM aaaCreate |Microsoft 文件"
description: "建立 Windows 虛擬機器使用 Azure PowerShell 及 hello 傳統部署模型。"
services: virtual-machines-windows
documentationcenter: 
author: cynthn
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 42c0d4be-573c-45d1-b9b0-9327537702f7
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 05/30/2017
ms.author: cynthn
ms.openlocfilehash: 5339f458c1f08f6e1752a53191f19402fab8ea25
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a><span data-ttu-id="177cf-103">使用 PowerShell 和 hello 傳統部署模型中建立 Windows 虛擬機器</span><span class="sxs-lookup"><span data-stu-id="177cf-103">Create a Windows virtual machine with PowerShell and hello classic deployment model</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="177cf-104">Azure 入口網站 - Windows</span><span class="sxs-lookup"><span data-stu-id="177cf-104">Azure portal - Windows</span></span>](tutorial.md)
> * [<span data-ttu-id="177cf-105">PowerShell - Windows</span><span class="sxs-lookup"><span data-stu-id="177cf-105">PowerShell - Windows</span></span>](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> <span data-ttu-id="177cf-106">Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。</span><span class="sxs-lookup"><span data-stu-id="177cf-106">Azure has two different deployment models for creating and working with resources: [Resource Manager and Classic](../../../resource-manager-deployment-model.md).</span></span> <span data-ttu-id="177cf-107">本文件涵蓋使用 hello 傳統部署模型。</span><span class="sxs-lookup"><span data-stu-id="177cf-107">This article covers using hello Classic deployment model.</span></span> <span data-ttu-id="177cf-108">Microsoft 建議最新的部署使用 hello 資源管理員的模型。</span><span class="sxs-lookup"><span data-stu-id="177cf-108">Microsoft recommends that most new deployments use hello Resource Manager model.</span></span> <span data-ttu-id="177cf-109">了解如何太[使用 hello 資源管理員的模型執行這些步驟](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="177cf-109">Learn how too[perform these steps using hello Resource Manager model](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="177cf-110">這些步驟顯示如何 toocustomize 一組的 Azure PowerShell 命令，建立並預先設定 windows Azure 虛擬機器使用的建置組塊方法。</span><span class="sxs-lookup"><span data-stu-id="177cf-110">These steps show you how toocustomize a set of Azure PowerShell commands that create and preconfigure a Windows-based Azure virtual machine by using a building block approach.</span></span> <span data-ttu-id="177cf-111">您可以使用此程序 tooquickly 建立新的 windows 虛擬機器的一組命令，並擴充現有的部署一或多個命令會將設定的快速 toocreate 建置自訂的開發/測試或 IT 專業人員的環境。</span><span class="sxs-lookup"><span data-stu-id="177cf-111">You can use this process tooquickly create a command set for a new Windows-based virtual machine and expand an existing deployment or toocreate multiple command sets that quickly build out a custom dev/test or IT pro environment.</span></span>

<span data-ttu-id="177cf-112">這些步驟遵循建立 Azure PowerShell 命令集合的填空方法。</span><span class="sxs-lookup"><span data-stu-id="177cf-112">These steps follow a fill-in-the-blanks approach for creating Azure PowerShell command sets.</span></span> <span data-ttu-id="177cf-113">如果您是新 tooPowerShell 或只是想 tooknow 哪些值 toospecify 成功的組態，這種方法十分有用。</span><span class="sxs-lookup"><span data-stu-id="177cf-113">This approach can be useful if you are new tooPowerShell or you just want tooknow what values toospecify for successful configuration.</span></span> <span data-ttu-id="177cf-114">進階的 PowerShell 使用者可以採取 hello 命令，並以取代其值為 hello 變數 （hello 行開頭為"$"）。</span><span class="sxs-lookup"><span data-stu-id="177cf-114">Advanced PowerShell users can take hello commands and substitute their own values for hello variables (hello lines beginning with "$").</span></span>

<span data-ttu-id="177cf-115">如果還沒有這麼做，使用中的 hello 指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell，在本機電腦上的。</span><span class="sxs-lookup"><span data-stu-id="177cf-115">If you haven't done so already, use hello instructions in [How tooinstall and configure Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell on your local computer.</span></span> <span data-ttu-id="177cf-116">然後，開啟 Windows PowerShell 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="177cf-116">Then, open a Windows PowerShell command prompt.</span></span>

## <a name="step-1-add-your-account"></a><span data-ttu-id="177cf-117">步驟 1︰加入您的帳戶</span><span class="sxs-lookup"><span data-stu-id="177cf-117">Step 1: Add your account</span></span>
1. <span data-ttu-id="177cf-118">在 hello PowerShell 提示字元中輸入**Add-azureaccount**按一下**Enter**。</span><span class="sxs-lookup"><span data-stu-id="177cf-118">At hello PowerShell prompt, type **Add-AzureAccount** and click **Enter**.</span></span> 
2. <span data-ttu-id="177cf-119">輸入您 Azure 訂用帳戶相關聯的 hello 電子郵件地址，然後按一下**繼續**。</span><span class="sxs-lookup"><span data-stu-id="177cf-119">Type in hello email address associated with your Azure subscription and click **Continue**.</span></span> 
3. <span data-ttu-id="177cf-120">輸入 hello 您帳戶的密碼。</span><span class="sxs-lookup"><span data-stu-id="177cf-120">Type in hello password for your account.</span></span> 
4. <span data-ttu-id="177cf-121">按一下 [ **登入**]。</span><span class="sxs-lookup"><span data-stu-id="177cf-121">Click **Sign in**.</span></span>

## <a name="step-2-set-your-subscription-and-storage-account"></a><span data-ttu-id="177cf-122">步驟 2：設定您的訂用帳戶和儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="177cf-122">Step 2: Set your subscription and storage account</span></span>
<span data-ttu-id="177cf-123">Hello Windows PowerShell 命令提示字元中執行這些命令來設定您的 Azure 訂用帳戶和儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="177cf-123">Set your Azure subscription and storage account by running these commands at hello Windows PowerShell command prompt.</span></span> <span data-ttu-id="177cf-124">Hello 括在引號，包括 hello < 和 > 字元內的所有項目取代 hello 正確名稱。</span><span class="sxs-lookup"><span data-stu-id="177cf-124">Replace everything within hello quotes, including hello < and > characters, with hello correct names.</span></span>

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

<span data-ttu-id="177cf-125">您可以從 hello 的 hello hello 輸出的訂用帳戶名稱屬性來取得 hello 正確的訂用帳戶名稱**Get-azuresubscription**命令。</span><span class="sxs-lookup"><span data-stu-id="177cf-125">You can get hello correct subscription name from hello SubscriptionName property of hello output of hello **Get-AzureSubscription** command.</span></span> <span data-ttu-id="177cf-126">您可以從 hello Label 屬性的 hello hello 輸出取得 hello 正確的儲存體帳戶名稱**Get AzureStorageAccount**命令之後執行 hello **Select-azuresubscription**命令。</span><span class="sxs-lookup"><span data-stu-id="177cf-126">You can get hello correct storage account name from hello Label property of hello output of hello **Get-AzureStorageAccount** command after you run hello **Select-AzureSubscription** command.</span></span>

## <a name="step-3-determine-hello-imagefamily"></a><span data-ttu-id="177cf-127">步驟 3： 決定 hello ImageFamily</span><span class="sxs-lookup"><span data-stu-id="177cf-127">Step 3: Determine hello ImageFamily</span></span>
<span data-ttu-id="177cf-128">接下來，您需要 toodetermine hello ImageFamily 或標籤值 hello 特定映像對應 toohello 想 toocreate 的 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="177cf-128">Next, you need toodetermine hello ImageFamily or Label value for hello specific image corresponding toohello Azure virtual machine you want toocreate.</span></span> <span data-ttu-id="177cf-129">您可以取得 hello 可用 ImageFamily 值，這個命令的清單。</span><span class="sxs-lookup"><span data-stu-id="177cf-129">You can get hello list of available ImageFamily values with this command.</span></span>

    Get-AzureVMImage | select ImageFamily -Unique

<span data-ttu-id="177cf-130">以下是以 Windows 為基礎的電腦本身 ImageFamily 值的一些範例：</span><span class="sxs-lookup"><span data-stu-id="177cf-130">Here are some examples of ImageFamily values for Windows-based computers:</span></span>

* <span data-ttu-id="177cf-131">Windows Server 2012 R2 Datacenter</span><span class="sxs-lookup"><span data-stu-id="177cf-131">Windows Server 2012 R2 Datacenter</span></span>
* <span data-ttu-id="177cf-132">Windows Server 2008 R2 SP1</span><span class="sxs-lookup"><span data-stu-id="177cf-132">Windows Server 2008 R2 SP1</span></span>
* <span data-ttu-id="177cf-133">Windows Server 2016 Technical Preview 4</span><span class="sxs-lookup"><span data-stu-id="177cf-133">Windows Server 2016 Technical Preview 4</span></span>
* <span data-ttu-id="177cf-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="177cf-134">SQL Server 2012 SP1 Enterprise on Windows Server 2012</span></span>

<span data-ttu-id="177cf-135">如果您發現您所需的 hello 映像，請開啟 選擇或 hello PowerShell 整合式指令碼環境 (ISE) 的 hello 文字編輯器的新執行個體。</span><span class="sxs-lookup"><span data-stu-id="177cf-135">If you find hello image you are looking for, open a fresh instance of hello text editor of your choice or hello PowerShell Integrated Scripting Environment (ISE).</span></span> <span data-ttu-id="177cf-136">將下列 hello 複製到新文字檔 hello 或 hello PowerShell ISE 中，以取代 hello ImageFamily 值。</span><span class="sxs-lookup"><span data-stu-id="177cf-136">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello ImageFamily value.</span></span>

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

<span data-ttu-id="177cf-137">在某些情況下，hello 映像名稱已在 hello Label 屬性，而不是 hello ImageFamily 值。</span><span class="sxs-lookup"><span data-stu-id="177cf-137">In some cases, hello image name is in hello Label property instead of hello ImageFamily value.</span></span> <span data-ttu-id="177cf-138">如果找不到想要使用 hello ImageFamily 屬性的 hello 映像，會依其 Label 屬性，此命令列出 hello 映像。</span><span class="sxs-lookup"><span data-stu-id="177cf-138">If you didn't find hello image that you are looking for using hello ImageFamily property, list hello images by their Label property with this command.</span></span>

    Get-AzureVMImage | select Label -Unique

<span data-ttu-id="177cf-139">如果您發現 hello 這個命令的正確映像，請開啟 hello 文字編輯器選項或 hello PowerShell ISE 的新執行的個體。</span><span class="sxs-lookup"><span data-stu-id="177cf-139">If you find hello right image with this command, open a fresh instance of hello text editor of your choice or hello PowerShell ISE.</span></span> <span data-ttu-id="177cf-140">將下列 hello 複製到新文字檔 hello 或 hello PowerShell ISE 中，以取代 hello 標籤值。</span><span class="sxs-lookup"><span data-stu-id="177cf-140">Copy hello following into hello new text file or hello PowerShell ISE, substituting hello Label value.</span></span>

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a><span data-ttu-id="177cf-141">步驟 4：建置命令集</span><span class="sxs-lookup"><span data-stu-id="177cf-141">Step 4: Build your command set</span></span>
<span data-ttu-id="177cf-142">建置 hello 其餘部分將 hello 適當的一組區塊下方複製到您新的文字檔或 hello ISE 然後填入 hello 變數值並移除 hello < 和 > 字元來設定您的命令。</span><span class="sxs-lookup"><span data-stu-id="177cf-142">Build hello rest of your command set by copying hello appropriate set of blocks below into your new text file or hello ISE and then filling in hello variable values and removing hello < and > characters.</span></span> <span data-ttu-id="177cf-143">請參閱 hello 兩[範例](#examples)hello 以了解 hello 最終結果的這篇文章結尾處。</span><span class="sxs-lookup"><span data-stu-id="177cf-143">See hello two [examples](#examples) at hello end of this article for an idea of hello final result.</span></span>

<span data-ttu-id="177cf-144">選擇兩個命令區塊的其中一個，啟動命令集 (必要)。</span><span class="sxs-lookup"><span data-stu-id="177cf-144">Start your command set by choosing one of these two command blocks (required).</span></span>

<span data-ttu-id="177cf-145">選項 1：指定虛擬機器名稱和大小。</span><span class="sxs-lookup"><span data-stu-id="177cf-145">Option 1: Specify a virtual machine name and a size.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

<span data-ttu-id="177cf-146">選項 2：指定名稱、大小和可用性設定組名稱。</span><span class="sxs-lookup"><span data-stu-id="177cf-146">Option 2: Specify a name, size, and availability set name.</span></span>

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

<span data-ttu-id="177cf-147">D、 DS 或 G 系列虛擬機器的 hello InstanceSize 值，請參閱[虛擬機器和 Azure 的雲端服務大小](https://msdn.microsoft.com/library/azure/dn197896.aspx)。</span><span class="sxs-lookup"><span data-stu-id="177cf-147">For hello InstanceSize values for D-, DS-, or G-series virtual machines, see [Virtual Machine and Cloud Service Sizes for Azure](https://msdn.microsoft.com/library/azure/dn197896.aspx).</span></span>

> [!NOTE]
> <span data-ttu-id="177cf-148">如果您有 Enterprise 合約附有軟體保證，而想 tootake 利用 Windows Server hello[混合使用權益](https://azure.microsoft.com/pricing/hybrid-use-benefit/)，新增**-LicenseType**參數 toohello **New-azurevmconfig** cmdlet，將傳遞 hello 值**Windows_Server** hello 一般使用案例。</span><span class="sxs-lookup"><span data-stu-id="177cf-148">If you have an Enterprise Agreement with Software Assurance, and intend tootake advantage of hello Windows Server [Hybrid Use Benefit](https://azure.microsoft.com/pricing/hybrid-use-benefit/), add the **-LicenseType** parameter toohello **New-AzureVMConfig** cmdlet, passing hello value **Windows_Server** for hello typical use case.</span></span>  <span data-ttu-id="177cf-149">請務必使用您已上傳; 映像您無法使用從 hello 組件庫的標準映像以 hello 混合使用好處。</span><span class="sxs-lookup"><span data-stu-id="177cf-149">Be sure you are using an image you have uploaded; you cannot use a standard image from hello Gallery with hello Hybrid Use Benefit.</span></span>
> 
> 

<span data-ttu-id="177cf-150">（選擇性） 針對獨立 Windows 電腦，指定 hello 本機系統管理員帳戶和密碼。</span><span class="sxs-lookup"><span data-stu-id="177cf-150">Optionally, for a standalone Windows computer, specify hello local administrator account and password.</span></span>

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

<span data-ttu-id="177cf-151">選擇強式密碼。</span><span class="sxs-lookup"><span data-stu-id="177cf-151">Choose a strong password.</span></span> <span data-ttu-id="177cf-152">toocheck 其強度，請參閱[密碼檢查程式： 使用強式密碼](https://www.microsoft.com/security/pc-security/password-checker.aspx)。</span><span class="sxs-lookup"><span data-stu-id="177cf-152">toocheck its strength, see [Password Checker: Using Strong Passwords](https://www.microsoft.com/security/pc-security/password-checker.aspx).</span></span>

<span data-ttu-id="177cf-153">（選擇性） tooadd hello Windows 電腦 tooan 現有 Active Directory 網域，指定 hello 本機系統管理員帳戶和密碼、 hello 網域以及 hello 名稱和密碼的網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="177cf-153">Optionally, tooadd hello Windows computer tooan existing Active Directory domain, specify hello local administrator account and password, hello domain, and hello name and password of a domain account.</span></span>

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

<span data-ttu-id="177cf-154">Windows 型虛擬機器的其他預先設定選項，請參閱 hello hello 語法**Windows**和**WindowsDomain**參數會設定[新增 AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig)。</span><span class="sxs-lookup"><span data-stu-id="177cf-154">For additional pre-configuration options for Windows-based virtual machines, see hello syntax for hello **Windows** and **WindowsDomain** parameter sets in [Add-AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig).</span></span>

<span data-ttu-id="177cf-155">選擇性地指派特定的 IP 位址，稱為靜態 DIP hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="177cf-155">Optionally, assign hello virtual machine a specific IP address, known as a static DIP.</span></span>

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

<span data-ttu-id="177cf-156">您可以確認特定 IP 位址可用於：</span><span class="sxs-lookup"><span data-stu-id="177cf-156">You can verify that a specific IP address is available with:</span></span>

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

<span data-ttu-id="177cf-157">選擇性地指派 hello 虛擬機器 tooa 特定子網路中的 Azure 虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="177cf-157">Optionally, assign hello virtual machine tooa specific subnet in an Azure virtual network.</span></span>

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

<span data-ttu-id="177cf-158">（選擇性） 加入單一資料磁碟 toohello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="177cf-158">Optionally, add a single data disk toohello virtual machine.</span></span>

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

<span data-ttu-id="177cf-159">Active Directory 網域控制站設定 $hcaching 太"None"。</span><span class="sxs-lookup"><span data-stu-id="177cf-159">For an Active Directory domain controller, set $hcaching too"None".</span></span>

<span data-ttu-id="177cf-160">（選擇性） 加入 hello 虛擬機器 tooan 現有負載平衡集外部流量。</span><span class="sxs-lookup"><span data-stu-id="177cf-160">Optionally, add hello virtual machine tooan existing load-balanced set for external traffic.</span></span>

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

<span data-ttu-id="177cf-161">最後，選擇其中一個這些必要的命令區塊，如建立 hello 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="177cf-161">Finally, choose one of these required command blocks for creating hello virtual machine.</span></span>

<span data-ttu-id="177cf-162">選項 1： 建立現有的雲端服務中的 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="177cf-162">Option 1: Create hello virtual machine in an existing cloud service.</span></span>

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

<span data-ttu-id="177cf-163">hello hello 雲端服務的簡短名稱是出現在 hello 清單的雲端服務或資源群組的 hello Azure 入口網站中的 hello 清單 hello Azure 入口網站中的 hello 名稱。</span><span class="sxs-lookup"><span data-stu-id="177cf-163">hello short name of hello cloud service is hello name that appears in hello list of Cloud Services in hello Azure portal or in hello list of Resource Groups in hello Azure portal.</span></span>

<span data-ttu-id="177cf-164">選項 2： 建立在現有的雲端服務和虛擬網路中的 hello 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="177cf-164">Option 2: Create hello virtual machine in an existing cloud service and virtual network.</span></span>

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a><span data-ttu-id="177cf-165">步驟 5：執行命令集</span><span class="sxs-lookup"><span data-stu-id="177cf-165">Step 5: Run your command set</span></span>
<span data-ttu-id="177cf-166">檢閱您在文字編輯器中建立 hello Azure PowerShell 命令集，或 hello 步驟 4 中的命令的多個區塊所組成的 PowerShell ISE。</span><span class="sxs-lookup"><span data-stu-id="177cf-166">Review hello Azure PowerShell command set you built in your text editor or hello PowerShell ISE consisting of multiple blocks of commands from step 4.</span></span> <span data-ttu-id="177cf-167">請確定您已指定所有必要的 hello 變數，而且它們有 hello 正確的值。</span><span class="sxs-lookup"><span data-stu-id="177cf-167">Ensure that you have specified all hello needed variables and that they have hello correct values.</span></span> <span data-ttu-id="177cf-168">也請確定您已移除所有 hello < 和 > 字元。</span><span class="sxs-lookup"><span data-stu-id="177cf-168">Also make sure that you have removed all hello < and > characters.</span></span>

<span data-ttu-id="177cf-169">如果您使用文字編輯器，複製 hello 命令設定 toohello 剪貼簿，然後以滑鼠右鍵按一下 開啟 Windows PowerShell 命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="177cf-169">If you are using a text editor, copy hello command set toohello clipboard and then right-click your open Windows PowerShell command prompt.</span></span> <span data-ttu-id="177cf-170">這會為一系列的 PowerShell 命令發出 hello 命令集，並建立 Azure 虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="177cf-170">This will issue hello command set as a series of PowerShell commands and create your Azure virtual machine.</span></span> <span data-ttu-id="177cf-171">或者，執行設定 hello PowerShell ISE 中的 hello 命令。</span><span class="sxs-lookup"><span data-stu-id="177cf-171">Alternately, run hello command set in hello PowerShell ISE.</span></span>

<span data-ttu-id="177cf-172">如果您將再次建立這個虛擬機器或類似的虛擬機器，您可以：</span><span class="sxs-lookup"><span data-stu-id="177cf-172">If you will be creating this virtual machine again or a similar one, you can:</span></span>

* <span data-ttu-id="177cf-173">將此命令集儲存為 PowerShell 指令碼檔案 (*.ps1)。</span><span class="sxs-lookup"><span data-stu-id="177cf-173">Save this command set as a PowerShell script file (*.ps1).</span></span>
* <span data-ttu-id="177cf-174">儲存此設定為在 hello Azure 自動化 runbook 的命令**自動化帳戶**hello Azure 入口網站的區段。</span><span class="sxs-lookup"><span data-stu-id="177cf-174">Save this command set as an Azure Automation runbook in hello **Automation Accounts** section of hello Azure portal.</span></span>

## <span data-ttu-id="177cf-175"><a id="examples"></a>範例</span><span class="sxs-lookup"><span data-stu-id="177cf-175"><a id="examples"></a>Examples</span></span>
<span data-ttu-id="177cf-176">以下是兩個範例使用 hello 上方建立 windows Azure 虛擬機器的 toobuild Azure PowerShell 命令集的步驟。</span><span class="sxs-lookup"><span data-stu-id="177cf-176">Here are two examples of using hello steps above toobuild Azure PowerShell command sets that create Windows-based Azure virtual machines.</span></span>

### <a name="example-1"></a><span data-ttu-id="177cf-177">範例 1</span><span class="sxs-lookup"><span data-stu-id="177cf-177">Example 1</span></span>
<span data-ttu-id="177cf-178">我需要 PowerShell 命令集 toocreate hello 初始虛擬機器的 Active Directory 網域控制站：</span><span class="sxs-lookup"><span data-stu-id="177cf-178">I need a PowerShell command set toocreate hello initial virtual machine for an Active Directory domain controller that:</span></span>

* <span data-ttu-id="177cf-179">使用 hello Windows Server 2012 R2 Datacenter 映像。</span><span class="sxs-lookup"><span data-stu-id="177cf-179">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="177cf-180">具有 hello AZDC1 的名稱。</span><span class="sxs-lookup"><span data-stu-id="177cf-180">Has hello name AZDC1.</span></span>
* <span data-ttu-id="177cf-181">屬於獨立電腦。</span><span class="sxs-lookup"><span data-stu-id="177cf-181">Is a standalone computer.</span></span>
* <span data-ttu-id="177cf-182">有 20 GB 的額外資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="177cf-182">Has an additional data disk of 20 GB.</span></span>
* <span data-ttu-id="177cf-183">具有靜態 IP 位址 hello 192.168.244.4。</span><span class="sxs-lookup"><span data-stu-id="177cf-183">Has hello static IP address 192.168.244.4.</span></span>
* <span data-ttu-id="177cf-184">Hello 後端 hello AZDatacenter 虛擬網路子網路內。</span><span class="sxs-lookup"><span data-stu-id="177cf-184">Is in hello BackEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="177cf-185">Hello Azure TailspinToys 雲端服務內。</span><span class="sxs-lookup"><span data-stu-id="177cf-185">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="177cf-186">以下是 hello 對應 Azure PowerShell 命令集 toocreate 之間可讀性的每個區塊的空白行與此虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="177cf-186">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine, with blank lines between each block for readability.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="AZDC1"
    $vmsize="Medium"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

    $vm1 | Set-AzureSubnet -SubnetNames "BackEnd"

    $vm1 | Set-AzureStaticVNetIP -IPAddress 192.168.244.4

    $disksize=20
    $disklabel="DCData"
    $lun=0
    $hcaching="None"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

### <a name="example-2"></a><span data-ttu-id="177cf-187">範例 2</span><span class="sxs-lookup"><span data-stu-id="177cf-187">Example 2</span></span>
<span data-ttu-id="177cf-188">我需要 PowerShell 命令設定 toocreate 業務的伺服器虛擬機器的：</span><span class="sxs-lookup"><span data-stu-id="177cf-188">I need a PowerShell command set toocreate a virtual machine for a line-of-business server that:</span></span>

* <span data-ttu-id="177cf-189">使用 hello Windows Server 2012 R2 Datacenter 映像。</span><span class="sxs-lookup"><span data-stu-id="177cf-189">Uses hello Windows Server 2012 R2 Datacenter image.</span></span>
* <span data-ttu-id="177cf-190">具有 hello LOB1 的名稱。</span><span class="sxs-lookup"><span data-stu-id="177cf-190">Has hello name LOB1.</span></span>
* <span data-ttu-id="177cf-191">是 hello corp.contoso.com 網域的成員。</span><span class="sxs-lookup"><span data-stu-id="177cf-191">Is a member of hello corp.contoso.com domain.</span></span>
* <span data-ttu-id="177cf-192">具有 200 GB 的額外資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="177cf-192">Has an additional data disk of 200 GB.</span></span>
* <span data-ttu-id="177cf-193">Hello AZDatacenter 虛擬網路的 hello FrontEnd 子網路內。</span><span class="sxs-lookup"><span data-stu-id="177cf-193">Is in hello FrontEnd subnet of hello AZDatacenter virtual network.</span></span>
* <span data-ttu-id="177cf-194">Hello Azure TailspinToys 雲端服務內。</span><span class="sxs-lookup"><span data-stu-id="177cf-194">Is in hello Azure-TailspinToys cloud service.</span></span>

<span data-ttu-id="177cf-195">以下是 hello 對應 Azure PowerShell 命令集 toocreate 此虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="177cf-195">Here is hello corresponding Azure PowerShell command set toocreate this virtual machine.</span></span>

    $family="Windows Server 2012 R2 Datacenter"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1
    $vmname="LOB1"
    $vmsize="Large"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="corp.contoso.com"
    $domacctdomain="CORP"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

    $vm1 | Set-AzureSubnet -SubnetNames "FrontEnd"

    $disksize=200
    $disklabel="LOBData"
    $lun=0
    $hcaching="ReadWrite"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

    $svcname="Azure-TailspinToys"
    $vnetname="AZDatacenter"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname


## <a name="next-steps"></a><span data-ttu-id="177cf-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="177cf-196">Next steps</span></span>
<span data-ttu-id="177cf-197">如果您需要大於 127 GB 的作業系統磁碟，您可以[展開 hello 作業系統磁碟機](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="177cf-197">If you need an OS disk that is larger than 127 GB, you can [expand hello OS drive](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

