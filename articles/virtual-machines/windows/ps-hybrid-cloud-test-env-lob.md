---
title: "LOB 應用程式測試環境 | Microsoft Docs"
description: "了解如何在混合式雲端環境中建立 IT 專業或開發測試的 Web 型企業營運應用程式。"
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
ms.openlocfilehash: 8e9a380458bfede80ed0fc1ee7e62b0caec09501
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a><span data-ttu-id="a7bfa-103">在混合式雲端中設定 Web 型 LOB 應用程式進行測試</span><span class="sxs-lookup"><span data-stu-id="a7bfa-103">Set up a web-based LOB application in a hybrid cloud for testing</span></span>
<span data-ttu-id="a7bfa-104">本主題將逐步引導您建立模擬混合式雲端環境測試 Microsoft Azure 代管的 Web 型企業營運 (LOB) 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-104">This topic steps you through creating a simulated hybrid cloud environment for testing a web-based line of business (LOB) application hosted in Microsoft Azure.</span></span> <span data-ttu-id="a7bfa-105">以下是產生的組態。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-105">Here is the resulting configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="a7bfa-106">此組態包含下列各項：</span><span class="sxs-lookup"><span data-stu-id="a7bfa-106">This configuration consists of:</span></span>

* <span data-ttu-id="a7bfa-107">Azure (TestLab VNet) 代管的模擬內部部署網路。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-107">A simulated on-premises network hosted in Azure (the TestLab VNet).</span></span>
* <span data-ttu-id="a7bfa-108">Azure (TestVNET) 代管的跨單位部署虛擬網路。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-108">A cross-premises virtual network hosted in Azure (TestVNET).</span></span>
* <span data-ttu-id="a7bfa-109">VNet 對 VNet VPN 連線。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-109">A VNet-to-VNet VPN connection.</span></span>
* <span data-ttu-id="a7bfa-110">Web 型 LOB 伺服器、SQL 伺服器，以及 TestVNET 虛擬網路中的第二個網域控制站。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-110">A web-based LOB server, SQL server, and secondary domain controller in the TestVNET virtual network.</span></span>

<span data-ttu-id="a7bfa-111">這個組態一般可供您開始：</span><span class="sxs-lookup"><span data-stu-id="a7bfa-111">This configuration provides a basis and common starting point from which you can:</span></span>

* <span data-ttu-id="a7bfa-112">針對 Azure 中的 SQL Server 2014 資料庫後端開發和測試網際網路資訊服務 (IIS) 代管的 LOB 應用程式。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-112">Develop and test LOB applications hosted on Internet Information Services (IIS) with a SQL Server 2014 database backend in Azure.</span></span>
* <span data-ttu-id="a7bfa-113">執行此模擬混合式雲端型 IT 工作負載的測試。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-113">Perform testing of this simulated hybrid cloud-based IT workload.</span></span>

<span data-ttu-id="a7bfa-114">設定此混合式雲端測試環境分為三個主要階段：</span><span class="sxs-lookup"><span data-stu-id="a7bfa-114">There are three major phases to setting up this hybrid cloud test environment:</span></span>

1. <span data-ttu-id="a7bfa-115">設定模擬混合式雲端環境。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-115">Set up the simulated hybrid cloud environment.</span></span>
2. <span data-ttu-id="a7bfa-116">設定 SQL 伺服器電腦 (SQL1)。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-116">Configure the SQL server computer (SQL1).</span></span>
3. <span data-ttu-id="a7bfa-117">設定 LOB 伺服器 (LOB1)。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-117">Configure the LOB server (LOB1).</span></span>

<span data-ttu-id="a7bfa-118">此工作負載需要 Azure 訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-118">This workload requires an Azure subscription.</span></span> <span data-ttu-id="a7bfa-119">如果您有 MSDN 或 Visual Studio 訂用帳戶，請參閱 [Visual Studio 訂閱者的每月 Azure 點數](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-119">If you have an MSDN or Visual Studio subscription, see [Monthly Azure credit for Visual Studio subscribers](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/).</span></span>

<span data-ttu-id="a7bfa-120">如需 Azure 代管生產 LOB 應用程式的範例，請參閱 **Microsoft 軟體架構圖表和藍圖** 的 [企業營運應用程式](http://msdn.microsoft.com/dn630664)架構藍圖。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-120">For an example of a production LOB application hosted in Azure, see the **Line of business applications** architecture blueprint at [Microsoft Software Architecture Diagrams and Blueprints](http://msdn.microsoft.com/dn630664).</span></span>

## <a name="phase-1-set-up-the-simulated-hybrid-cloud-environment"></a><span data-ttu-id="a7bfa-121">步驟 1：設定模擬混合式雲端環境</span><span class="sxs-lookup"><span data-stu-id="a7bfa-121">Phase 1: Set up the simulated hybrid cloud environment</span></span>
<span data-ttu-id="a7bfa-122">建立 [模擬混合式雲端測試環境](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-122">Create the [simulated hybrid cloud test environment](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span> <span data-ttu-id="a7bfa-123">由於這個測試環境不需要公司網路子網路上的 APP1 伺服器，您可以暫時將它關閉。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-123">Because this test environment does not require the presence of the APP1 server on the Corpnet subnet, you can shut it down for now.</span></span>

<span data-ttu-id="a7bfa-124">這是您目前的組態。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-124">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-the-sql-server-computer-sql1"></a><span data-ttu-id="a7bfa-125">第 2 階段：設定 SQL 伺服器電腦 (SQL1)</span><span class="sxs-lookup"><span data-stu-id="a7bfa-125">Phase 2: Configure the SQL server computer (SQL1)</span></span>
<span data-ttu-id="a7bfa-126">從 Azure 入口網站，視需要啟動 DC2 電腦。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-126">From the Azure portal, start the DC2 computer if needed.</span></span>

<span data-ttu-id="a7bfa-127">然後，在本機電腦的 Azure PowerShell 命令提示字元下，使用下列命令建立 SQL1 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-127">Next, create a virtual machine for SQL1 with these commands at an Azure PowerShell command prompt on your local computer.</span></span> <span data-ttu-id="a7bfa-128">執行這些命令之前，請先填入變數值並移除 < 和 > 字元。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-128">Prior to running these commands, fill in the variable values and remove the < and > characters.</span></span>

    $rgName="<your resource group name>"
    $locName="<the Azure location of your resource group>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name SQL1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName SQL1 -VMSize Standard_A4
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $vhdURI=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-SQLDataDisk.vhd"
    Add-AzureRMVMDataDisk -VM $vm -Name "Data" -DiskSizeInGB 100 -VhdUri $vhdURI  -CreateOption empty

    $cred=Get-Credential -Message "Type the name and password of the local administrator account for the SQL Server computer." 
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName SQL1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftSQLServer -Offer SQL2014-WS2012R2 -Skus Standard -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/SQL1-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name "OSDisk" -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="a7bfa-129">使用 Azure 入口網站，利用 SQL1 的本機系統管理員帳戶連線到 SQL1。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-129">Use the Azure portal to connect to SQL1 using the local administrator account of SQL1.</span></span>

<span data-ttu-id="a7bfa-130">接著，設定 Windows 防火牆規則，允許基本連線測試和 SQL Server 流量。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-130">Next, configure Windows Firewall rules to allow basic connectivity testing and SQL Server traffic.</span></span> <span data-ttu-id="a7bfa-131">從 SQL1 的系統管理員層級 Windows PowerShell 命令提示字元下，執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-131">From an administrator-level Windows PowerShell command prompt on SQL1, run these commands.</span></span>

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="a7bfa-132">Ping 命令應該會收到來自 IP 位址 192.168.0.4 的四次成功回覆。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-132">The ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="a7bfa-133">接著，將 SQL1 上額外的資料磁碟新增為磁碟機代號 F: 的新磁碟區。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-133">Next, add the extra data disk on SQL1 as a new volume with the drive letter F:.</span></span>

1. <span data-ttu-id="a7bfa-134">在 [伺服器管理員] 的左窗格中，按一下 [檔案和存放服務]，然後按一下 [磁碟]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-134">In the left pane of Server Manager, click **File and Storage Services**, and then click **Disks**.</span></span>
2. <span data-ttu-id="a7bfa-135">在 [內容] 窗格的 [磁碟] 群組中，按一下 [磁碟 2] \([磁碟分割] 設為 [不明])。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-135">In the contents pane, in the **Disks** group, click **disk 2** (with the **Partition** set to **Unknown**).</span></span>
3. <span data-ttu-id="a7bfa-136">按一下 [工作]，然後按一下 [新增磁碟區]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-136">Click **Tasks**, and then click **New Volume**.</span></span>
4. <span data-ttu-id="a7bfa-137">在 [新增磁碟區精靈] 的 [在您開始前] 頁面上，按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-137">On the Before you begin page of the New Volume Wizard, click **Next**.</span></span>
5. <span data-ttu-id="a7bfa-138">在 [選取伺服器和磁碟] 頁面上，按一下 [磁碟 2]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-138">On the Select the server and disk page, click **Disk 2**, and then click **Next**.</span></span> <span data-ttu-id="a7bfa-139">出現提示時，按一下 [新增功能] 架構藍圖。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-139">When prompted, click **OK**.</span></span>
6. <span data-ttu-id="a7bfa-140">在 [指定磁碟區大小] 頁面上，按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-140">On the Specify the size of the volume page, click **Next**.</span></span>
7. <span data-ttu-id="a7bfa-141">在 [指派成磁碟機代號或資料夾] 頁面上，按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-141">On the Assign to a drive letter or folder page, click **Next**.</span></span>
8. <span data-ttu-id="a7bfa-142">在 [選取檔案系統設定] 頁面上，按 [下一步] 。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-142">On the Select file system settings page, click **Next**.</span></span>
9. <span data-ttu-id="a7bfa-143">在 [確認選取項目] 頁面上，按一下 [建立] 。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-143">On the Confirm selections page, click **Create**.</span></span>
10. <span data-ttu-id="a7bfa-144">完成時，按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-144">When complete, click **Close**.</span></span>

<span data-ttu-id="a7bfa-145">在 SQL1 的 Windows PowerShell 命令提示字元下執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="a7bfa-145">Run these commands at the Windows PowerShell command prompt on SQL1:</span></span>

    md f:\Data
    md f:\Log
    md f:\Backup

<span data-ttu-id="a7bfa-146">接下來，在 SQL1 上的 Windows PowerShell 提示字元中使用下列命令將 SQL1 加入 CORP Windows Server Active Directory 網域中。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-146">Next, join SQL1 to the CORP Windows Server Active Directory domain with these commands at the Windows PowerShell prompt on SQL1.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="a7bfa-147">當系統提示您為 **Add-Computer** 命令提供網域帳戶認證時，請使用 CORP\User1 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-147">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span></span>

<span data-ttu-id="a7bfa-148">重新啟動之後，請使用 Azure 入口網站，利用 SQL1 的本機系統管理員帳戶 連線到 SQL1。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-148">After restarting, use the Azure portal to connect to SQL1 *with the local administrator account of SQL1*.</span></span>

<span data-ttu-id="a7bfa-149">接著，對於新資料庫和使用者帳戶權限設定 SQL Server 2014 使用 F: 磁碟機。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-149">Next, configure SQL Server 2014 to use the F: drive for new databases and for user account permissions.</span></span>

1. <span data-ttu-id="a7bfa-150">從 [開始] 畫面中，輸入 **SQL Server Management**，然後按一下 [SQL Server 2014 Management Studio]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-150">From the Start screen, type **SQL Server Management**, and then click **SQL Server 2014 Management Studio**.</span></span>
2. <span data-ttu-id="a7bfa-151">在 [連線到伺服器] 中按一下 [連線]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-151">In **Connect to Server**, click **Connect**.</span></span>
3. <span data-ttu-id="a7bfa-152">在 [物件總管] 樹狀結構窗格中，以滑鼠右鍵按一下 [SQL1] **SQL1**。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-152">In the Object Explorer tree pane, right-click **SQL1**, and then click **Properties**.</span></span>
4. <span data-ttu-id="a7bfa-153">在 [伺服器內容] 視窗中，按一下 [資料庫設定]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-153">In the **Server Properties** window, click **Database Settings**.</span></span>
5. <span data-ttu-id="a7bfa-154">找出 [資料庫預設位置]  並設定下列值：</span><span class="sxs-lookup"><span data-stu-id="a7bfa-154">Locate the **Database default locations** and set these values:</span></span> 
   * <span data-ttu-id="a7bfa-155">對於 [資料]，輸入路徑 **f:\Data**。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-155">For **Data**, type the path **f:\Data**.</span></span>
   * <span data-ttu-id="a7bfa-156">對於 [記錄]，輸入路徑 **f:\Log**。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-156">For **Log**, type the path **f:\Log**.</span></span>
   * <span data-ttu-id="a7bfa-157">對於 [備份]，輸入路徑 **f:\Backup**。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-157">For **Backup**, type the path **f:\Backup**.</span></span>
   * <span data-ttu-id="a7bfa-158">注意：只有新的資料庫才會使用這些位置。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-158">Note: Only new databases use these locations.</span></span>
6. <span data-ttu-id="a7bfa-159">按一下 [確定]  關閉視窗。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-159">Click the **OK** to close the window.</span></span>
7. <span data-ttu-id="a7bfa-160">在 [物件總管] 樹狀結構窗格中，開啟 [安全性]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-160">In the **Object Explorer** tree pane, open **Security**.</span></span>
8. <span data-ttu-id="a7bfa-161">以滑鼠右鍵按一下 [登入]，然後按一下 [新增登入]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-161">Right-click **Logins** and then click **New Login**.</span></span>
9. <span data-ttu-id="a7bfa-162">在 [登入名稱] 中，輸入 **CORP\User1**。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-162">In **Login name**, type **CORP\User1**.</span></span>
10. <span data-ttu-id="a7bfa-163">在 [伺服器角色] 頁面上，按一下 [sysadmin]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-163">On the **Server Roles** page, click **sysadmin**, and then click **OK**.</span></span>
11. <span data-ttu-id="a7bfa-164">關閉 Microsoft SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-164">Close Microsoft SQL Server Management Studio.</span></span>

<span data-ttu-id="a7bfa-165">這是您目前的組態。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-165">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-the-lob-server-lob1"></a><span data-ttu-id="a7bfa-166">第 3 階段：設定 LOB 伺服器 (LOB1)。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-166">Phase 3: Configure the LOB server (LOB1)</span></span>
<span data-ttu-id="a7bfa-167">首先，在本機電腦的 Azure PowerShell 命令提示字元下，使用下列命令建立 LOB1 的虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-167">First, create a virtual machine for LOB1 with these commands at the Azure PowerShell command prompt on your local computer.</span></span>

    $rgName="<your resource group name>"
    $locName="<your Azure location, such as West US>"
    $saName="<your storage account name>"

    $vnet=Get-AzureRMVirtualNetwork -Name "TestVNET" -ResourceGroupName $rgName
    $subnet=Get-AzureRmVirtualNetworkSubnetConfig -VirtualNetwork $vnet -Name "TestSubnet"
    $pip=New-AzureRMPublicIpAddress -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -AllocationMethod Dynamic
    $nic=New-AzureRMNetworkInterface -Name LOB1-NIC -ResourceGroupName $rgName -Location $locName -Subnet $subnet -PublicIpAddress $pip
    $vm=New-AzureRMVMConfig -VMName LOB1 -VMSize Standard_A2
    $storageAcc=Get-AzureRMStorageAccount -ResourceGroupName $rgName -Name $saName
    $cred=Get-Credential -Message "Type the name and password of the local administrator account for LOB1."
    $vm=Set-AzureRMVMOperatingSystem -VM $vm -Windows -ComputerName LOB1 -Credential $cred -ProvisionVMAgent -EnableAutoUpdate
    $vm=Set-AzureRMVMSourceImage -VM $vm -PublisherName MicrosoftWindowsServer -Offer WindowsServer -Skus 2012-R2-Datacenter -Version "latest"
    $vm=Add-AzureRMVMNetworkInterface -VM $vm -Id $nic.Id
    $osDiskUri=$storageAcc.PrimaryEndpoints.Blob.ToString() + "vhds/LOB1-TestLab-OSDisk.vhd"
    $vm=Set-AzureRMVMOSDisk -VM $vm -Name LOB1-TestVNET-OSDisk -VhdUri $osDiskUri -CreateOption fromImage
    New-AzureRMVM -ResourceGroupName $rgName -Location $locName -VM $vm

<span data-ttu-id="a7bfa-168">接下來，使用 Azure 入口網站，利用 LOB1 的本機系統管理員帳戶的認證連線到 LOB1。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-168">Next, use the Azure portal to connect to LOB1 with the credentials of the local administrator account of LOB1.</span></span>

<span data-ttu-id="a7bfa-169">接著，設定 Windows 防火牆規則，允許基本連線測試的流量。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-169">Next, configure a Windows Firewall rule to allow traffic for basic connectivity testing.</span></span> <span data-ttu-id="a7bfa-170">從 LOB1 的系統管理員層級 Windows PowerShell 命令提示字元下，執行這些命令。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-170">From an administrator-level Windows PowerShell command prompt on LOB1, run these commands.</span></span>

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

<span data-ttu-id="a7bfa-171">Ping 命令應該會收到來自 IP 位址 192.168.0.4 的四次成功回覆。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-171">The ping command should result in four successful replies from IP address 192.168.0.4.</span></span>

<span data-ttu-id="a7bfa-172">接下來，在 Windows PowerShell 提示字元中使用下列命令將 LOB1 加入 CORP Active Directory 網域中。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-172">Next, join LOB1 to the CORP Active Directory domain with these commands at the Windows PowerShell prompt.</span></span>

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

<span data-ttu-id="a7bfa-173">當系統提示您為 **Add-Computer** 命令提供網域帳戶認證時，請使用 CORP\User1 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-173">Use the CORP\User1 account when prompted to supply domain account credentials for the **Add-Computer** command.</span></span>

<span data-ttu-id="a7bfa-174">重新啟動之後，請使用 Azure 入口網站，利用 CORP\User1 帳戶和密碼連線到 LOB1。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-174">After restarting, use the Azure portal to connect to LOB1 with the CORP\User1 account and password.</span></span>

<span data-ttu-id="a7bfa-175">接著，為 IIS 設定 LOB1，並且測試從 CLIENT1 進行的存取。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-175">Next, configure LOB1 for IIS and test access from CLIENT1.</span></span>

1. <span data-ttu-id="a7bfa-176">在 [伺服器管理員] 中，按一下 [新增角色及功能] 。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-176">From Server Manager, click **Add roles and features**.</span></span>
2. <span data-ttu-id="a7bfa-177">在 [開始之前] 頁面中按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-177">On the **Before you begin** page, click **Next**.</span></span>
3. <span data-ttu-id="a7bfa-178">在 [選取安裝類型] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-178">On the **Select installation type** page, click **Next**.</span></span>
4. <span data-ttu-id="a7bfa-179">在 [選取目的地伺服器] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-179">On the **Select destination server** page, click **Next**.</span></span>
5. <span data-ttu-id="a7bfa-180">在 [伺服器角色] 頁面上，按一下 [角色] 清單中的 [網頁伺服器 (IIS)]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-180">On the **Server roles** page, click **Web Server (IIS)** in the list of **Roles**.</span></span>
6. <span data-ttu-id="a7bfa-181">出現提示時，按一下 [新增功能]，然後按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-181">When prompted, click **Add Features**, and then click **Next**.</span></span>
7. <span data-ttu-id="a7bfa-182">在 [選取功能] 頁面上，按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-182">On the **Select features** page, click **Next**.</span></span>
8. <span data-ttu-id="a7bfa-183">在 [網頁伺服器 (IIS)] 頁面上，按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-183">On the **Web Server (IIS)** page, click **Next**.</span></span>
9. <span data-ttu-id="a7bfa-184">在 [選取角色服務] 頁面上，選取或清除測試 LOB 應用程式所需服務的核取方塊，然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-184">On the **Select role services** page, select or clear the check boxes for the services you need for testing your LOB application, and then click **Next**.</span></span>
10. <span data-ttu-id="a7bfa-185">在 [確認安裝選項] 頁面上，按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-185">On the **Confirm installation selections** page, click **Install**.</span></span>
11. <span data-ttu-id="a7bfa-186">等候元件安裝完成，然後按一下 [關閉] 。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-186">Wait until the installation of components has completed and then click **Close**.</span></span>
12. <span data-ttu-id="a7bfa-187">從 Azure 入口網站，以 CORP\User1 帳戶認證登入 CLIENT1 電腦，然後啟動 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-187">From the Azure portal, connect to the CLIENT1 computer with the CORP\User1 account credentials, and then start Internet Explorer.</span></span>
13. <span data-ttu-id="a7bfa-188">在網址列中，輸入 **http://lob1/**，然後按下 ENTER。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-188">In the Address bar, type **http://lob1/** and then press ENTER.</span></span> <span data-ttu-id="a7bfa-189">您應該會看見預設的 IIS 8 網頁。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-189">You should see the default IIS 8 web page.</span></span>

<span data-ttu-id="a7bfa-190">這是您目前的組態。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-190">This is your current configuration.</span></span>

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

<span data-ttu-id="a7bfa-191">這個環境此時即可供您在 LOB1 部署 Web 型應用程式，並且從公司網路子網路上的 CLIENT1 測試功能。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-191">This environment is now ready for you to deploy your web-based application on LOB1 and test functionality from CLIENT1 on the Corpnet subnet.</span></span>

## <a name="next-step"></a><span data-ttu-id="a7bfa-192">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a7bfa-192">Next step</span></span>
* <span data-ttu-id="a7bfa-193">使用 [Azure 入口網站](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)來新增虛擬機器。</span><span class="sxs-lookup"><span data-stu-id="a7bfa-193">Add a new virtual machine using the [Azure portal](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

