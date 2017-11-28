---
title: "aaaLOB 應用程式測試環境 |Microsoft 文件"
description: "了解如何以 web 為基礎，toocreate 企業營運應用程式中的混合式雲端環境的 IT 專業人員或開發測試。"
services: virtual-machines-windows
documentationcenter: 
author: JoeDavies-MSFT
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 92d2d8ce-60ed-4512-95e5-a7fe3b0ca00b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 09/30/2016
ms.author: josephd
ms.openlocfilehash: e9f825bbb1cbeb841ee3c974ebf6721dc236c311
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="b9913-103">在混合式雲端中設定 Web 型 LOB 應用程式進行測試</span><span class="sxs-lookup"><span data-stu-id="b9913-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="b9913-104">本主題將逐步引導您建立模擬混合式雲端環境測試 Microsoft Azure 代管的 Web 型企業營運 (LOB) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b9913-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="b9913-105">以下是 hello 產生的設定。</span><span class="sxs-lookup"><span data-stu-id="b9913-105">Here is hello resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="b9913-106">此組態包含下列各項：</span><span class="sxs-lookup"><span data-stu-id="b9913-106">This configuration consists of:</span></span>

* <span data-ttu-id="b9913-107">裝載於 Azure (hello 測試實驗室 VNet) 模擬在內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="b9913-107">A simulated on-premises network hosted in Azure (hello TestLab VNet).</span></span>
* <span data-ttu-id="b9913-108">Azure (TestVNET) 代管的跨單位部署虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="b9913-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="b9913-109">VNet 對 VNet VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="b9913-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="b9913-110">網頁型 LOB 伺服器、 SQL server 和 hello TestVNET 虛擬網路中的次要網域控制站。</span><span class="sxs-lookup"><span data-stu-id="b9913-110">A web-based LOB server, SQL server, and secondary domain controller in hello TestVNET virtual network.</span></span>

<span data-ttu-id="b9913-111">這個組態一般可供您開始：</span><span class="sxs-lookup"><span data-stu-id="b9913-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="b9913-112">針對 Azure 中的 SQL Server 2014 資料庫後端開發和測試網際網路資訊服務 (IIS) 代管的 LOB 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b9913-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="b9913-113">執行此模擬混合式雲端型 IT 工作負載的測試。</span><span class="sxs-lookup"><span data-stu-id="b9913-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="b9913-114">有三個主要階段 toosetting 這個混合式雲端測試環境：</span><span class="sxs-lookup"><span data-stu-id="b9913-114">There are three major phases toosetting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="b9913-115">設定 hello 模擬的混合式雲端環境。</span><span class="sxs-lookup"><span data-stu-id="b9913-115">Set up hello simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="b9913-116">設定 hello SQL server 電腦 (SQL1)。</span><span class="sxs-lookup"><span data-stu-id="b9913-116">Configure hello SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="b9913-117">Hello LOB 伺服器 (LOB1) 設定。</span><span class="sxs-lookup"><span data-stu-id="b9913-117">Configure hello LOB server (LOB1).</span></span>

<span data-ttu-id="b9913-118">此工作負載需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9913-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="b9913-119">如果您有 MSDN 或 Visual Studio 訂用帳戶，請參閱 [Visual Studio 訂閱者的每月 Azure 點數](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)。</span><span class="sxs-lookup"><span data-stu-id="b9913-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="b9913-120">如需實際執行環境中 Azure 託管的 LOB 應用程式的範例，請參閱 hello**企業營運應用程式**在架構藍圖[Microsoft 軟體架構圖表和藍圖](http://msdn.microsoft.com/dn630664)。</span><span class="sxs-lookup"><span data-stu-id="b9913-120">For an example of a production LOB application hosted in Azure, see hello **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a><span data-ttu-id="b9913-121">階段 1： 設定 hello 模擬的混合式雲端環境</span><span class="sxs-lookup"><span data-stu-id="b9913-121">Phase 1: Set up hello simulated hybrid cloud environment</span></span>
<span data-ttu-id="b9913-122">建立 hello[模擬的混合式雲端測試環境](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b9913-122">Create hello [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="b9913-123">因為這個測試環境不需要 hello hello APP1 伺服器 hello Corpnet 子網路上存在，您可以現在將它關機。</span><span class="sxs-lookup"><span data-stu-id="b9913-123">Because this test environment does not require hello presence of hello APP1 server on hello Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="b9913-124">這是您目前的組態。</span><span class="sxs-lookup"><span data-stu-id="b9913-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a><span data-ttu-id="b9913-125">階段 2： 設定 hello SQL server 電腦 (SQL1)</span><span class="sxs-lookup"><span data-stu-id="b9913-125">Phase 2: Configure hello SQL server computer (SQL1)</span></span>
<span data-ttu-id="b9913-126">如有需要請從 hello Azure 入口網站，開始 hello DC2 電腦。</span><span class="sxs-lookup"><span data-stu-id="b9913-126">From hello Azure portal, start hello DC2 computer if needed.</span></span>

<span data-ttu-id="b9913-127">然後，在本機電腦的 Azure PowerShell 命令提示字元下，使用下列命令建立 SQL1 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b9913-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="b9913-128">先前 toorunning 這些命令中，填入 hello 變數值以及移除 hello < 和 > 字元。</span><span class="sxs-lookup"><span data-stu-id="b9913-128">Prior toorunning these commands, fill in hello variable values and remove hello < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<hello Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for hello SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="b9913-129">使用 hello Azure 入口網站 tooconnect tooSQL1 使用 SQL1 的 hello 本機系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="b9913-129">Use hello Azure portal tooconnect tooSQL1 using hello local administrator account of SQL1.</span></span>

<span data-ttu-id="b9913-130">接著，設定 Windows 防火牆規則 tooallow 基本連線測試和 SQL Server 流量。</span><span class="sxs-lookup"><span data-stu-id="b9913-130">Next, configure Windows Firewall rules tooallow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="b9913-131">從 SQL1 的系統管理員層級 Windows PowerShell 命令提示字元下，執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="b9913-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="b9913-132">四個來自 IP 位址為 192.168.0.4 的成功回覆時產生 hello ping 命令。</span><span class="sxs-lookup"><span data-stu-id="b9913-132">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="b9913-133">接下來，新增 hello 做為新的磁碟區與 hello 磁碟機代號 f： 在 SQL1 上額外的資料磁碟。</span><span class="sxs-lookup"><span data-stu-id="b9913-133">Next, add hello extra data disk on SQL1 as a new volume with hello drive letter F:.</span></span>

1. <span data-ttu-id="b9913-134">在 hello 左窗格的 伺服器管理員中，按一下 **檔案和存放服務**，然後按一下**磁碟**。</span><span class="sxs-lookup"><span data-stu-id="b9913-134">In hello left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="b9913-135">在 hello 內容窗格中 hello**磁碟**群組中，按一下**磁碟 2** (以 hello**磁碟分割**設定得**未知**)。</span><span class="sxs-lookup"><span data-stu-id="b9913-135">In hello contents pane, in hello **Disks** group, click **disk 2** (with hello **Partition** set too**Unknown**).</span></span>
3. <span data-ttu-id="b9913-136">按一下 工作，然後按一下新增磁碟區。</span><span class="sxs-lookup"><span data-stu-id="b9913-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="b9913-137">在 hello 開始 hello 新增磁碟區精靈頁面之前，請按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b9913-137">On hello Before you begin page of hello New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="b9913-138">在 hello 選取 hello 伺服器及磁碟 頁面上，按一下**磁碟 2**，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b9913-138">On hello Select hello server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="b9913-139">出現提示時，按一下 [新增功能] 架構藍圖。</span><span class="sxs-lookup"><span data-stu-id="b9913-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="b9913-140">在 hello 指定 hello 大小的 hello 磁碟區 頁面，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="b9913-140">On hello Specify hello size of hello volume page, click **Next**.</span></span>
7. <span data-ttu-id="b9913-141">在 hello 分派 tooa 磁碟機代號或資料夾 頁面上，按一下 **下一步**。</span><span class="sxs-lookup"><span data-stu-id="b9913-141">On hello Assign tooa drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="b9913-142">Hello 選取檔案系統設定] 頁面上，按一下 [**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b9913-142">On hello Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="b9913-143">在 hello 確認選取項目頁面上，按一下 **建立**。</span><span class="sxs-lookup"><span data-stu-id="b9913-143">On hello Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="b9913-144">完成時，按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="b9913-144">When complete, click **Close**.</span></span>

<span data-ttu-id="b9913-145">在 SQL1 上，在 hello Windows PowerShell 命令提示字元執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="b9913-145">Run these commands at hello Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="b9913-146">接著，將這些命令 hello 在 SQL1 上的 Windows PowerShell 命令提示字元 SQL1 toohello CORP Windows Server Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="b9913-146">Next, join SQL1 toohello CORP Windows Server Active Directory domain with these commands at hello Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="b9913-147">使用 hello CORP\User1 帳戶出現提示時 hello toosupply 網域帳戶認證**Add-computer**命令。</span><span class="sxs-lookup"><span data-stu-id="b9913-147">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="b9913-148">重新啟動之後，使用 hello Azure 入口網站 tooconnect tooSQL1*搭配 SQL1 hello 本機系統管理員帳戶*。</span><span class="sxs-lookup"><span data-stu-id="b9913-148">After restarting, use hello Azure portal tooconnect tooSQL1 *with hello local administrator account of SQL1*.</span></span>

<span data-ttu-id="b9913-149">接著，設定 SQL Server 2014 toouse hello f： 磁碟機與使用者帳戶權限的新資料庫。</span><span class="sxs-lookup"><span data-stu-id="b9913-149">Next, configure SQL Server 2014 toouse hello F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="b9913-150">從 hello [開始] 畫面，輸入**SQL Server Management**，然後按一下 **SQL Server 2014 Management Studio**。</span><span class="sxs-lookup"><span data-stu-id="b9913-150">From hello Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="b9913-151">在**連接 tooServer**，按一下 **連接**。</span><span class="sxs-lookup"><span data-stu-id="b9913-151">In **Connect tooServer**, click **Connect**.</span></span>
3. <span data-ttu-id="b9913-152">在 hello 物件總管 樹狀目錄窗格中，以滑鼠右鍵按一下**SQL1**，然後按一下**屬性**。</span><span class="sxs-lookup"><span data-stu-id="b9913-152">In hello Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="b9913-153">在 hello**伺服器屬性**視窗中，按一下 **資料庫設定**。</span><span class="sxs-lookup"><span data-stu-id="b9913-153">In hello **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="b9913-154">找出 hello**資料庫預設位置**和設定這些值：</span><span class="sxs-lookup"><span data-stu-id="b9913-154">Locate hello **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="b9913-155">如**資料**，型別 hello 路徑**f:\Data**。</span><span class="sxs-lookup"><span data-stu-id="b9913-155">For **Data**, type hello path **f:\Data**.</span></span>
   * <span data-ttu-id="b9913-156">如**記錄**，型別 hello 路徑**f:\Log**。</span><span class="sxs-lookup"><span data-stu-id="b9913-156">For **Log**, type hello path **f:\Log**.</span></span>
   * <span data-ttu-id="b9913-157">如**備份**，型別 hello 路徑**f:\Backup**。</span><span class="sxs-lookup"><span data-stu-id="b9913-157">For **Backup**, type hello path **f:\Backup**.</span></span>
   * <span data-ttu-id="b9913-158">注意：只有新的資料庫才會使用這些位置。</span><span class="sxs-lookup"><span data-stu-id="b9913-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="b9913-159">按一下 hello**確定**tooclose hello 視窗。</span><span class="sxs-lookup"><span data-stu-id="b9913-159">Click hello **OK** tooclose hello window.</span></span>
7. <span data-ttu-id="b9913-160">在 [hello**物件總管] 中**樹狀目錄窗格中，開啟**安全性**。</span><span class="sxs-lookup"><span data-stu-id="b9913-160">In hello **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="b9913-161">以滑鼠右鍵按一下 登入，然後按一下新增登入。</span><span class="sxs-lookup"><span data-stu-id="b9913-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="b9913-162">在 [登入名稱] 中，輸入 **CORP\User1**。</span><span class="sxs-lookup"><span data-stu-id="b9913-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="b9913-163">在 hello**伺服器角色**頁面上，按一下**sysadmin**，然後按一下 **確定**。</span><span class="sxs-lookup"><span data-stu-id="b9913-163">On hello **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="b9913-164">關閉 Microsoft SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="b9913-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="b9913-165">這是您目前的組態。</span><span class="sxs-lookup"><span data-stu-id="b9913-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a><span data-ttu-id="b9913-166">階段 3： 設定 hello LOB 伺服器 (LOB1)</span><span class="sxs-lookup"><span data-stu-id="b9913-166">Phase 3: Configure hello LOB server (LOB1)</span></span>
<span data-ttu-id="b9913-167">使用這些命令在本機電腦上的 hello Azure PowerShell 命令提示字元，如 LOB1 首先，建立虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="b9913-167">First, create a virtual machine for LOB1 with these commands at hello Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="b9913-168">接下來，使用 hello Azure 入口網站 tooconnect tooLOB1 hello LOB1 hello 本機系統管理員帳戶認證。</span><span class="sxs-lookup"><span data-stu-id="b9913-168">Next, use hello Azure portal tooconnect tooLOB1 with hello credentials of hello local administrator account of LOB1.</span></span>

<span data-ttu-id="b9913-169">接著，設定基本連線測試的 Windows 防火牆規則 tooallow 的流量。</span><span class="sxs-lookup"><span data-stu-id="b9913-169">Next, configure a Windows Firewall rule tooallow traffic for basic connectivity testing.</span></span> <span data-ttu-id="b9913-170">從 LOB1 的系統管理員層級 Windows PowerShell 命令提示字元下，執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="b9913-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="b9913-171">四個來自 IP 位址為 192.168.0.4 的成功回覆時產生 hello ping 命令。</span><span class="sxs-lookup"><span data-stu-id="b9913-171">hello ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="b9913-172">接著，將這些命令在 Windows PowerShell 提示字元中 hello LOB1 toohello CORP Active Directory 網域。</span><span class="sxs-lookup"><span data-stu-id="b9913-172">Next, join LOB1 toohello CORP Active Directory domain with these commands at hello Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="b9913-173">使用 hello CORP\User1 帳戶出現提示時 hello toosupply 網域帳戶認證**Add-computer**命令。</span><span class="sxs-lookup"><span data-stu-id="b9913-173">Use hello CORP\User1 account when prompted toosupply domain account credentials for hello **Add-Computer** command.</span></span>

<span data-ttu-id="b9913-174">重新啟動之後，使用 hello Azure 入口網站 tooconnect tooLOB1 hello CORP\User1 帳戶與密碼。</span><span class="sxs-lookup"><span data-stu-id="b9913-174">After restarting, use hello Azure portal tooconnect tooLOB1 with hello CORP\User1 account and password.</span></span>

<span data-ttu-id="b9913-175">接著，為 IIS 設定 LOB1，並且測試從 CLIENT1 進行的存取。</span><span class="sxs-lookup"><span data-stu-id="b9913-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="b9913-176">在 [伺服器管理員] 中，按一下 [新增角色及功能] 。</span><span class="sxs-lookup"><span data-stu-id="b9913-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="b9913-177">在 hello**開始之前**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b9913-177">On hello **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="b9913-178">在 hello**選取安裝類型**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b9913-178">On hello **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="b9913-179">在 hello**選取目的地伺服器**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b9913-179">On hello **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="b9913-180">在 hello**伺服器角色**頁面上，按一下**網頁伺服器 (IIS)** hello 清單中**角色**。</span><span class="sxs-lookup"><span data-stu-id="b9913-180">On hello **Server roles** page, click **Web Server (IIS)** in hello list of **Roles**.</span></span>
6. <span data-ttu-id="b9913-181">出現提示時，按一下 [新增功能]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="b9913-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="b9913-182">在 hello**選取功能**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b9913-182">On hello **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="b9913-183">在 hello**網頁伺服器 (IIS)**頁面上，按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b9913-183">On hello **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="b9913-184">在 hello**選取角色服務**頁面上，選取或清除您測試您的 LOB 應用程式，您需要的 hello 服務的 hello 核取方塊，然後按一下**下一步**。</span><span class="sxs-lookup"><span data-stu-id="b9913-184">On hello **Select role services** page, select or clear hello check boxes for hello services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="b9913-185">在 hello**確認安裝選項**頁面上，按一下**安裝**。</span><span class="sxs-lookup"><span data-stu-id="b9913-185">On hello **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="b9913-186">等候 hello 元件的安裝已完成，然後按一下**關閉**。</span><span class="sxs-lookup"><span data-stu-id="b9913-186">Wait until hello installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="b9913-187">Hello Azure 入口網站，從連接 toohello CLIENT1 電腦 hello CORP\User1 帳戶的認證，然後再啟動 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="b9913-187">From hello Azure portal, connect toohello CLIENT1 computer with hello CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="b9913-188">在 hello 網址列中輸入**http://lob1/**然後按 ENTER 鍵。</span><span class="sxs-lookup"><span data-stu-id="b9913-188">In hello Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="b9913-189">您應該會看到 hello 預設 IIS 8 網頁。</span><span class="sxs-lookup"><span data-stu-id="b9913-189">You should see hello default IIS 8 web page.</span></span>

<span data-ttu-id="b9913-190">這是您目前的組態。</span><span class="sxs-lookup"><span data-stu-id="b9913-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="b9913-191">此環境便已準備好您 toodeploy web 應用程式 LOB1 和測試功能從 CLIENT1 hello Corpnet 子網路上的。</span><span class="sxs-lookup"><span data-stu-id="b9913-191">This environment is now ready for you toodeploy your web-based application on LOB1 and test functionality from CLIENT1 on hello Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="b9913-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b9913-192">Next step</span></span>
* <span data-ttu-id="b9913-193">加入新的虛擬機器使用 hello [Azure 入口網站](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="b9913-193">Add a new virtual machine using hello [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

