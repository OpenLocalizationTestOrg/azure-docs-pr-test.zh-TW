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
# <a name="set-up-a-web-based-lob-application-in-a-hybrid-cloud-for-testing"></a>在混合式雲端中設定 Web 型 LOB 應用程式進行測試
本主題將逐步引導您建立模擬混合式雲端環境測試 Microsoft Azure 代管的 Web 型企業營運 (LOB) 應用程式。 以下是 hello 產生的設定。

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

此組態包含下列各項：

* 裝載於 Azure (hello 測試實驗室 VNet) 模擬在內部部署網路。
* Azure (TestVNET) 代管的跨單位部署虛擬網路。
* VNet 對 VNet VPN 連線。
* 網頁型 LOB 伺服器、 SQL server 和 hello TestVNET 虛擬網路中的次要網域控制站。

這個組態一般可供您開始：

* 針對 Azure 中的 SQL Server 2014 資料庫後端開發和測試網際網路資訊服務 (IIS) 代管的 LOB 應用程式。
* 執行此模擬混合式雲端型 IT 工作負載的測試。

有三個主要階段 toosetting 這個混合式雲端測試環境：

1. 設定 hello 模擬的混合式雲端環境。
2. 設定 hello SQL server 電腦 (SQL1)。
3. Hello LOB 伺服器 (LOB1) 設定。

此工作負載需要 Azure 訂用帳戶。 如果您有 MSDN 或 Visual Studio 訂用帳戶，請參閱 [Visual Studio 訂閱者的每月 Azure 點數](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/)。

如需實際執行環境中 Azure 託管的 LOB 應用程式的範例，請參閱 hello**企業營運應用程式**在架構藍圖[Microsoft 軟體架構圖表和藍圖](http://msdn.microsoft.com/dn630664)。

## <a name="phase-1-set-up-hello-simulated-hybrid-cloud-environment"></a>階段 1： 設定 hello 模擬的混合式雲端環境
建立 hello[模擬的混合式雲端測試環境](ps-hybrid-cloud-test-env-sim.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。 因為這個測試環境不需要 hello hello APP1 伺服器 hello Corpnet 子網路上存在，您可以現在將它關機。

這是您目前的組態。

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph1.png)

## <a name="phase-2-configure-hello-sql-server-computer-sql1"></a>階段 2： 設定 hello SQL server 電腦 (SQL1)
如有需要請從 hello Azure 入口網站，開始 hello DC2 電腦。

然後，在本機電腦的 Azure PowerShell 命令提示字元下，使用下列命令建立 SQL1 的虛擬機器。 先前 toorunning 這些命令中，填入 hello 變數值以及移除 hello < 和 > 字元。

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

使用 hello Azure 入口網站 tooconnect tooSQL1 使用 SQL1 的 hello 本機系統管理員帳戶。

接著，設定 Windows 防火牆規則 tooallow 基本連線測試和 SQL Server 流量。 從 SQL1 的系統管理員層級 Windows PowerShell 命令提示字元下，執行這些命令。

    New-NetFirewallRule -DisplayName "SQL Server" -Direction Inbound -Protocol TCP -LocalPort 1433,1434,5022 -Action allow 
    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

四個來自 IP 位址為 192.168.0.4 的成功回覆時產生 hello ping 命令。

接下來，新增 hello 做為新的磁碟區與 hello 磁碟機代號 f： 在 SQL1 上額外的資料磁碟。

1. 在 hello 左窗格的 伺服器管理員中，按一下 **檔案和存放服務**，然後按一下**磁碟**。
2. 在 hello 內容窗格中 hello**磁碟**群組中，按一下**磁碟 2** (以 hello**磁碟分割**設定得**未知**)。
3. 按一下 工作，然後按一下新增磁碟區。
4. 在 hello 開始 hello 新增磁碟區精靈頁面之前，請按一下**下一步**。
5. 在 hello 選取 hello 伺服器及磁碟 頁面上，按一下**磁碟 2**，然後按一下**下一步**。 出現提示時，按一下 [新增功能] 架構藍圖。
6. 在 hello 指定 hello 大小的 hello 磁碟區 頁面，按一下 **下一步**。
7. 在 hello 分派 tooa 磁碟機代號或資料夾 頁面上，按一下 **下一步**。
8. Hello 選取檔案系統設定] 頁面上，按一下 [**下一步**。
9. 在 hello 確認選取項目頁面上，按一下 **建立**。
10. 完成時，按一下 [關閉] 。

在 SQL1 上，在 hello Windows PowerShell 命令提示字元執行下列命令：

    md f:\Data
    md f:\Log
    md f:\Backup

接著，將這些命令 hello 在 SQL1 上的 Windows PowerShell 命令提示字元 SQL1 toohello CORP Windows Server Active Directory 網域。

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

使用 hello CORP\User1 帳戶出現提示時 hello toosupply 網域帳戶認證**Add-computer**命令。

重新啟動之後，使用 hello Azure 入口網站 tooconnect tooSQL1*搭配 SQL1 hello 本機系統管理員帳戶*。

接著，設定 SQL Server 2014 toouse hello f： 磁碟機與使用者帳戶權限的新資料庫。

1. 從 hello [開始] 畫面，輸入**SQL Server Management**，然後按一下 **SQL Server 2014 Management Studio**。
2. 在**連接 tooServer**，按一下 **連接**。
3. 在 hello 物件總管 樹狀目錄窗格中，以滑鼠右鍵按一下**SQL1**，然後按一下**屬性**。
4. 在 hello**伺服器屬性**視窗中，按一下 **資料庫設定**。
5. 找出 hello**資料庫預設位置**和設定這些值： 
   * 如**資料**，型別 hello 路徑**f:\Data**。
   * 如**記錄**，型別 hello 路徑**f:\Log**。
   * 如**備份**，型別 hello 路徑**f:\Backup**。
   * 注意：只有新的資料庫才會使用這些位置。
6. 按一下 hello**確定**tooclose hello 視窗。
7. 在 [hello**物件總管] 中**樹狀目錄窗格中，開啟**安全性**。
8. 以滑鼠右鍵按一下 登入，然後按一下新增登入。
9. 在 [登入名稱] 中，輸入 **CORP\User1**。
10. 在 hello**伺服器角色**頁面上，按一下**sysadmin**，然後按一下 **確定**。
11. 關閉 Microsoft SQL Server Management Studio。

這是您目前的組態。

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph2.png)

## <a name="phase-3-configure-hello-lob-server-lob1"></a>階段 3： 設定 hello LOB 伺服器 (LOB1)
使用這些命令在本機電腦上的 hello Azure PowerShell 命令提示字元，如 LOB1 首先，建立虛擬機器。

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

接下來，使用 hello Azure 入口網站 tooconnect tooLOB1 hello LOB1 hello 本機系統管理員帳戶認證。

接著，設定基本連線測試的 Windows 防火牆規則 tooallow 的流量。 從 LOB1 的系統管理員層級 Windows PowerShell 命令提示字元下，執行這些命令。

    Set-NetFirewallRule -DisplayName "File and Printer Sharing (Echo Request - ICMPv4-In)" -enabled True
    ping dc2.corp.contoso.com

四個來自 IP 位址為 192.168.0.4 的成功回覆時產生 hello ping 命令。

接著，將這些命令在 Windows PowerShell 提示字元中 hello LOB1 toohello CORP Active Directory 網域。

    Add-Computer -DomainName corp.contoso.com
    Restart-Computer

使用 hello CORP\User1 帳戶出現提示時 hello toosupply 網域帳戶認證**Add-computer**命令。

重新啟動之後，使用 hello Azure 入口網站 tooconnect tooLOB1 hello CORP\User1 帳戶與密碼。

接著，為 IIS 設定 LOB1，並且測試從 CLIENT1 進行的存取。

1. 在 [伺服器管理員] 中，按一下 [新增角色及功能] 。
2. 在 hello**開始之前**頁面上，按一下**下一步**。
3. 在 hello**選取安裝類型**頁面上，按一下**下一步**。
4. 在 hello**選取目的地伺服器**頁面上，按一下**下一步**。
5. 在 hello**伺服器角色**頁面上，按一下**網頁伺服器 (IIS)** hello 清單中**角色**。
6. 出現提示時，按一下 [新增功能]，然後按 [下一步]。
7. 在 hello**選取功能**頁面上，按一下**下一步**。
8. 在 hello**網頁伺服器 (IIS)**頁面上，按一下**下一步**。
9. 在 hello**選取角色服務**頁面上，選取或清除您測試您的 LOB 應用程式，您需要的 hello 服務的 hello 核取方塊，然後按一下**下一步**。
10. 在 hello**確認安裝選項**頁面上，按一下**安裝**。
11. 等候 hello 元件的安裝已完成，然後按一下**關閉**。
12. Hello Azure 入口網站，從連接 toohello CLIENT1 電腦 hello CORP\User1 帳戶的認證，然後再啟動 Internet Explorer。
13. 在 hello 網址列中輸入**http://lob1/**然後按 ENTER 鍵。 您應該會看到 hello 預設 IIS 8 網頁。

這是您目前的組態。

![](./media/ps-hybrid-cloud-test-env-lob/virtual-machines-windows-ps-hybrid-cloud-test-env-lob-ph3.png)

此環境便已準備好您 toodeploy web 應用程式 LOB1 和測試功能從 CLIENT1 hello Corpnet 子網路上的。

## <a name="next-step"></a>後續步驟
* 加入新的虛擬機器使用 hello [Azure 入口網站](../virtual-machines-windows-hero-tutorial.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

