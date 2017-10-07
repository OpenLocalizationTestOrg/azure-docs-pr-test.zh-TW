---
title: "aaaConfigure hello Always On 可用性群組使用 PowerShell 的 Azure VM 上 |Microsoft 文件"
description: "本教學課程會使用與 hello 傳統部署模型所建立的資源。 您可以在 Azure 中使用 PowerShell toocreate Always On 可用性群組。"
services: virtual-machines-windows
documentationcenter: na
author: MikeRayMSFT
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: a4e2f175-fe56-4218-86c7-a43fb916cc64
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 03/17/2017
ms.author: mikeray
ms.openlocfilehash: d4a27e203b2ff299adebec2b010c03422459b3c3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-hello-always-on-availability-group-on-an-azure-vm-with-powershell"></a>使用 PowerShell 的 Azure VM 上設定 hello Always On 可用性群組
> [!div class="op_single_selector"]
> * [傳統：UI](../classic/portal-sql-alwayson-availability-groups.md)
> * [傳統：PowerShell](../classic/ps-sql-alwayson-availability-groups.md)
<br/>

在開始之前，請考量您現在可以在 Azure Resource Manager 模型中完成這項工作。 我們建議針對新的部署使用 Azure Resource Manager 模型。 請參閱 [Azure 虛擬機器上的 SQL Server Always On 可用性群組](../sql/virtual-machines-windows-portal-sql-availability-group-overview.md)。

> [!IMPORTANT]
> 建議最新的部署使用 hello 資源管理員的模型。 Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文說明如何使用 hello 傳統部署模型。

Azure 虛擬機器 (Vm) 可協助資料庫的高可用性 SQL Server 系統管理員 toolower hello 成本。 本教學課程會示範如何 tooimplement 可用性群組使用 SQL Server Alwayson 端對端在 Azure 環境。 結尾 hello hello 教學課程中，在 Azure 中的 SQL Server Alwayson 方案將會包含下列項目 hello:

* 包含多個子網路 (前端和後端子網路) 的虛擬網路。
* 具有 Active Directory 網域的網域控制站。
* 兩個 SQL Server Vm 已部署的 toohello 後端子和聯結的 toohello Active Directory 網域。
* Hello 節點多數 仲裁模型具有三個節點 Windows 容錯移轉叢集。
* 具有兩份可用性資料庫同步認可複本的可用性群組。

此案例在 Azure 中是好選擇的原因是其單純性，而非因為其具有成本效益或其他因素。 例如，您也可以使用 hello 網域控制站為 hello 雙節點容錯移轉叢集中仲裁檔案共用見證，以減少 hello Vm 數目的兩個複本的可用性群組 toosave 在 Azure 中的計算時數。 這個方法可以減少從 hello 組態之上一個 hello VM 計數。

這個教學課程被專門 tooshow hello 必要的 tooset hello 註冊的步驟所述但不會闡述每個步驟的 hello 詳細資料的上述方案。 因此，而不是它會使用 PowerShell 指令碼 tootake hello GUI 設定步驟，提供您快速地透過每個步驟。 本教學課程假設 hello 下列：

* 您已經有 Azure 帳戶與 hello 虛擬機器的訂用帳戶。
* 您已安裝 hello [Azure PowerShell cmdlet](/powershell/azure/overview)。
* 您已非常熟悉內部部署解決方案的 Always On 可用性群組的功能。 如需詳細資訊，請參閱 [Always On 可用性群組 (SQL Server)](https://msdn.microsoft.com/library/hh510230.aspx)。

## <a name="connect-tooyour-azure-subscription-and-create-hello-virtual-network"></a>連接 tooyour Azure 訂用帳戶，並建立 hello 虛擬網路
1. 在 PowerShell 視窗中本機電腦上，匯入 hello Azure 模組，請下載 hello 發行設定檔案 tooyour 電腦，並連接您的 PowerShell 工作階段 tooyour Azure 訂用帳戶匯入 hello 下載發行設定。

        Import-Module "C:\Program Files (x86)\Microsoft SDKs\Azure\PowerShell\Azure\Azure.psd1"
        Get-AzurePublishSettingsFile
        Import-AzurePublishSettingsFile <publishsettingsfilepath>

    hello **Get-azurepublishsettingsfile**命令自動產生與 Azure 管理憑證，並將它下載 tooyour 機器。 瀏覽器會自動開啟，而且您所在的 Azure 訂用帳戶的提示的 tooenter hello Microsoft 帳戶認證。 下載的 hello **.publishsettings**檔案包含所有您需要 toomanage 您 Azure 訂用帳戶的 hello 資訊。 儲存這個檔案 tooa 本機目錄之後, 將它匯入使用 hello **Import-azurepublishsettingsfile**命令。

   > [!NOTE]
   > hello.publishsettings 檔案包含的認證 （未編碼） 會使用的 tooadminister 您的 Azure 訂用帳戶和服務。 這個檔案的 hello 安全性最佳作法是 toostore 暫時在來源目錄之外 （例如，在 hello Libraries\Documents 資料夾），它和 hello 匯入已完成後再刪除它。 取得存取 toohello.publishsettings 檔案的惡意使用者可以編輯、 建立，並刪除您的 Azure 服務。

2. 定義一系列您將使用 toocreate 您的雲端 IT 基礎結構的變數。

        $location = "West US"
        $affinityGroupName = "ContosoAG"
        $affinityGroupDescription = "Contoso SQL HADR Affinity Group"
        $affinityGroupLabel = "IaaS BI Affinity Group"
        $networkConfigPath = "C:\scripts\Network.netcfg"
        $virtualNetworkName = "ContosoNET"
        $storageAccountName = "<uniquestorageaccountname>"
        $storageAccountLabel = "Contoso SQL HADR Storage Account"
        $storageAccountContainer = "https://" + $storageAccountName + ".blob.core.windows.net/vhds/"
        $winImageName = (Get-AzureVMImage | where {$_.Label -like "Windows Server 2008 R2 SP1*"} | sort PublishedDate -Descending)[0].ImageName
        $sqlImageName = (Get-AzureVMImage | where {$_.Label -like "SQL Server 2012 SP1 Enterprise*"} | sort PublishedDate -Descending)[0].ImageName
        $dcServerName = "ContosoDC"
        $dcServiceName = "<uniqueservicename>"
        $availabilitySetName = "SQLHADR"
        $vmAdminUser = "AzureAdmin"
        $vmAdminPassword = "Contoso!000"
        $workingDir = "c:\scripts\"

    請特別注意 toohello 遵循您的命令稍後不會失敗的 tooensure:

   * 變數**$storageAccountName**和**$dcServiceName**必須是唯一的因為它們使用 tooidentify 您的雲端儲存體帳戶和雲端伺服器，分別在 hello 網際網路上。
   * 您指定的變數名稱的 hello **$affinityGroupName**和**$virtualNetworkName** hello 虛擬網路組態文件中稍後會使用設定。
   * **$sqlImageName**指定 hello 更新包含 SQL Server 2012 Service Pack 1 Enterprise Edition 的 hello VM 映像的名稱。
   * 為了簡單起見， **Contoso ！ 000** hello 相同整個 hello 整個教學課程所使用的密碼。

3. 建立同質群組。

        New-AzureAffinityGroup `
            -Name $affinityGroupName `
            -Location $location `
            -Description $affinityGroupDescription `
            -Label $affinityGroupLabel

4. 匯入組態檔以建立虛擬網路。

        Set-AzureVNetConfig `
            -ConfigurationPath $networkConfigPath

    hello 設定檔包含下列 XML 文件的 hello。 簡單地說，它會指定虛擬網路稱為**ContosoNET**呼叫 hello 同質群組中**ContosoAG**。 它有 hello 位址空間**10.10.0.0/16**兩個子網路，且**10.10.1.0/24**和**10.10.2.0/24**，這分別是 hello 前端網路和背景的子網路。 hello 前端子網路是您可以在其中放置 Microsoft SharePoint 之類的用戶端應用程式。 hello 端網路是您將放置 hello SQL Server Vm。 如果您變更 hello **$affinityGroupName**和**$virtualNetworkName**變數，您也必須變更對應下列名稱的 hello。

        <NetworkConfiguration xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.microsoft.com/ServiceHosting/2011/07/NetworkConfiguration">
          <VirtualNetworkConfiguration>
            <Dns />
            <VirtualNetworkSites>
              <VirtualNetworkSite name="ContosoNET" AffinityGroup="ContosoAG">
                <AddressSpace>
                  <AddressPrefix>10.10.0.0/16</AddressPrefix>
                </AddressSpace>
                <Subnets>
                  <Subnet name="Front">
                    <AddressPrefix>10.10.1.0/24</AddressPrefix>
                  </Subnet>
                  <Subnet name="Back">
                    <AddressPrefix>10.10.2.0/24</AddressPrefix>
                  </Subnet>
                </Subnets>
              </VirtualNetworkSite>
            </VirtualNetworkSites>
          </VirtualNetworkConfiguration>
        </NetworkConfiguration>

5. 建立與您建立，並將它設為 hello 目前的儲存體帳戶中，您的訂用帳戶中的 hello 同質群組相關聯的儲存體帳戶。

        New-AzureStorageAccount `
            -StorageAccountName $storageAccountName `
            -Label $storageAccountLabel `
            -AffinityGroup $affinityGroupName
        Set-AzureSubscription `
            -SubscriptionName (Get-AzureSubscription).SubscriptionName `
            -CurrentStorageAccount $storageAccountName

6. 建立 hello 新雲端服務和可用性設定組中的 hello 網域控制站伺服器。

        New-AzureVMConfig `
            -Name $dcServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$dcServerName.vhd" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -Windows `
                -DisableAutomaticUpdates `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword |
                New-AzureVM `
                    -ServiceName $dcServiceName `
                    –AffinityGroup $affinityGroupName `
                    -VNetName $virtualNetworkName

    這些管道的命令 hello 下列事項：

   * **New-AzureVMConfig** 可建立 VM 組態。
   * **新增 AzureProvisioningConfig**提供 hello 的獨立 Windows 伺服器的組態參數。
   * **新增 AzureDataDisk**加入您將用於儲存 Active Directory 資料，以快取選項集 tooNone hello 的 hello 資料磁碟。
   * **New-azurevm**建立新的雲端服務，並建立 hello hello 新的雲端服務中新的 Azure VM。

7. 等候 hello 完整佈建，新 VM toobe 並下載 hello 遠端桌面檔案 tooyour 工作目錄。 因為 hello 新的 Azure VM 需要很長的時間 tooprovision，hello`while`迴圈會繼續 toopoll hello 新的 VM，直到它可供使用。

        $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName

        While ($VMStatus.InstanceStatus -ne "ReadyRole")
        {
            write-host "Waiting for " $VMStatus.Name "... Current Status = " $VMStatus.InstanceStatus
            Start-Sleep -Seconds 15
            $VMStatus = Get-AzureVM -ServiceName $dcServiceName -Name $dcServerName
        }

        Get-AzureRemoteDesktopFile `
            -ServiceName $dcServiceName `
            -Name $dcServerName `
            -LocalPath "$workingDir$dcServerName.rdp"

hello 網域控制站伺服器現在已成功佈建。 接下來，您需要在此網域控制站伺服器上設定 hello Active Directory 網域。 在本機電腦上保持 hello PowerShell 視窗中開啟。 您將使用它一次更新 toocreate hello 兩個 SQL Server Vm。

## <a name="configure-hello-domain-controller"></a>設定 hello 網域控制站
1. 透過啟動 hello 遠端桌面檔案連接 toohello 網域控制站伺服器。 使用 hello 電腦系統管理員的 AzureAdmin 的使用者名稱和密碼**Contoso ！ 000**，這是您指定當您建立 hello 新的 VM。
2. 在系統管理員模式下開啟 [Azure PowerShell] 視窗。
3. 執行下列 hello **DCPROMO。EXE**向上 hello 命令 tooset **corp.contoso.com**含有 hello M 磁碟機上的資料目錄。

        dcpromo.exe `
            /unattend `
            /ReplicaOrNewDomain:Domain `
            /NewDomain:Forest `
            /NewDomainDNSName:corp.contoso.com `
            /ForestLevel:4 `
            /DomainNetbiosName:CORP `
            /DomainLevel:4 `
            /InstallDNS:Yes `
            /ConfirmGc:Yes `
            /CreateDNSDelegation:No `
            /DatabasePath:"C:\Windows\NTDS" `
            /LogPath:"C:\Windows\NTDS" `
            /SYSVOLPath:"C:\Windows\SYSVOL" `
            /SafeModeAdminPassword:"Contoso!000"

    Hello 命令執行完成之後，hello VM 會自動重新啟動。

4. 透過啟動 hello 遠端桌面檔案再次連接 toohello 網域控制站伺服器。 這次，改用 **CORP\Administrator** 身分登入。
5. 以系統管理員模式開啟 PowerShell 視窗，並使用下列命令的 hello 匯入 hello Active Directory PowerShell 模組：

        Import-Module ActiveDirectory

6. 執行下列命令 tooadd 三個使用者 toohello 網域 hello。

        $pwd = ConvertTo-SecureString "Contoso!000" -AsPlainText -Force
        New-ADUser `
            -Name 'Install' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc1' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true
        New-ADUser `
            -Name 'SQLSvc2' `
            -AccountPassword  $pwd `
            -PasswordNeverExpires $true `
            -ChangePasswordAtLogon $false `
            -Enabled $true

    **CORP\Install**都是使用的 tooconfigure 相關 toohello SQL Server 服務執行個體、 hello 容錯移轉叢集，以及 hello 可用性群組。 **CORP\SQLSvc1**和**CORP\SQLSvc2**作為 hello 兩個 SQL Server Vm 的 hello SQL Server 服務帳戶。
7. Hello 接下來，執行下列命令 toogive **CORP\Install** hello hello 網域中的權限 toocreate 電腦物件。

        Cd ad:
        $sid = new-object System.Security.Principal.SecurityIdentifier (Get-ADUser "Install").SID
        $guid = new-object Guid bf967a86-0de6-11d0-a285-00aa003049e2
        $ace1 = new-object System.DirectoryServices.ActiveDirectoryAccessRule $sid,"CreateChild","Allow",$guid,"All"
        $corp = Get-ADObject -Identity "DC=corp,DC=contoso,DC=com"
        $acl = Get-Acl $corp
        $acl.AddAccessRule($ace1)
        Set-Acl -Path "DC=corp,DC=contoso,DC=com" -AclObject $acl

    hello 上述指定的 GUID 是 hello GUID hello 電腦物件類型。 hello **CORP\Install**帳戶需要 hello**讀取全部內容**和**建立電腦物件**hello 容錯移轉的物件權限 toocreate hello Active Directory叢集。 hello**讀取全部內容**權限已被 tooCORP\Install 根據預設，因此您不需要 toogrant 它明確。 如需資訊的權限需要 toocreate hello 容錯移轉叢集，請參閱 <<c0> [ 容錯移轉叢集逐步指南： 設定 Active Directory 中的帳戶](https://technet.microsoft.com/library/cc731002%28v=WS.10%29.aspx)。

    既然您已經完成設定 Active Directory 與 hello 使用者物件，您將建立兩個 SQL Server Vm，並將它們 toothis 網域。

## <a name="create-hello-sql-server-vms"></a>建立 hello SQL Server Vm
1. 繼續已在本機電腦上開啟的 toouse hello PowerShell 視窗。 定義下列其他變數的 hello:

        $domainName= "corp"
        $FQDN = "corp.contoso.com"
        $subnetName = "Back"
        $sqlServiceName = "<uniqueservicename>"
        $quorumServerName = "ContosoQuorum"
        $sql1ServerName = "ContosoSQL1"
        $sql2ServerName = "ContosoSQL2"
        $availabilitySetName = "SQLHADR"
        $dataDiskSize = 100
        $dnsSettings = New-AzureDns -Name "ContosoBackDNS" -IPAddress "10.10.0.4"

    hello IP 位址**10.10.0.4**通常會指派 toohello hello 中建立的第一個 VM **10.10.0.0/16** Azure 虛擬網路的子網路。 您應該確認這是您的網域控制站伺服器 hello 位址，藉由執行**IPCONFIG**。
2. 執行下列管道的命令 toocreate hello 第一次的 hello VM 在 hello 容錯移轉叢集中，名為**ContosoQuorum**:

        New-AzureVMConfig `
            -Name $quorumServerName `
            -InstanceSize Medium `
            -ImageName $winImageName `
            -MediaLocation "$storageAccountContainer$quorumServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    New-AzureVM `
                        -ServiceName $sqlServiceName `
                        –AffinityGroup $affinityGroupName `
                        -VNetName $virtualNetworkName `
                        -DnsSettings $dnsSettings

    請注意上述的 hello 命令相關的 hello 下列：

   * **New-azurevmconfig**與 hello 所需的可用性設定組名稱建立 VM 組態。 hello 後續 Vm 將會建立以 hello 相同可用性設定組名稱，使其正在加入 toohello 相同可用性設定組。
   * **新增 AzureProvisioningConfig**聯結 hello 您所建立的 VM toohello Active Directory 網域。
   * **Set-azuresubnet**數位 hello hello 後的子網路中的 VM。
   * **New-azurevm**建立新的雲端服務，並建立 hello hello 新的雲端服務中新的 Azure VM。 hello **DnsSettings**參數指定該 hello DNS 伺服器 hello hello 新的雲端服務中的伺服器具有 hello IP 位址**10.10.0.4**。 這是 hello hello 網域控制站伺服器的 IP 位址。 需要這個參數 tooenable hello hello 雲端服務 toojoin toohello Active Directory 網域中的新 Vm 成功。 如果沒有這個參數，您必須手動設定 hello IPv4 設定 VM toouse hello 網域控制站伺服器中的主要 DNS 伺服器 hello 之後 hello VM 已佈建，然後再將 hello VM toohello Active Directory 網域。
3. 執行的 hello 下列管道命令 toocreate hello SQL Server Vm，名為**ContosoSQL1**和**ContosoSQL2**。

        # Create ContosoSQL1...
        New-AzureVMConfig `
            -Name $sql1ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql1ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 1 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

        # Create ContosoSQL2...
        New-AzureVMConfig `
            -Name $sql2ServerName `
            -InstanceSize Large `
            -ImageName $sqlImageName `
            -MediaLocation "$storageAccountContainer$sql2ServerName.vhd" `
            -AvailabilitySetName $availabilitySetName `
            -HostCaching "ReadOnly" `
            -DiskLabel "OS" |
            Add-AzureProvisioningConfig `
                -WindowsDomain `
                -AdminUserName $vmAdminUser `
                -Password $vmAdminPassword `
                -DisableAutomaticUpdates `
                -Domain $domainName `
                -JoinDomain $FQDN `
                -DomainUserName $vmAdminUser `
                -DomainPassword $vmAdminPassword |
                Set-AzureSubnet `
                    -SubnetNames $subnetName |
                    Add-AzureEndpoint `
                        -Name "SQL" `
                        -Protocol "tcp" `
                        -PublicPort 2 `
                        -LocalPort 1433 |
                        New-AzureVM `
                            -ServiceName $sqlServiceName

    請注意上述的 hello 命令相關的 hello 下列：

   * **New-azurevmconfig**使用 hello hello 網域控制站伺服器，為相同可用性設定組名稱，並使用 hello hello 虛擬機器映像庫中的 SQL Server 2012 Service Pack 1 Enterprise Edition 映像。 它也會設定 hello 操作系統磁碟 tooread 快取 （無寫入快取）。 我們建議您移轉 hello 資料庫檔案 tooa 個別資料磁碟您附加 toohello VM，並將它設定為無讀取或寫入快取。 不過，hello 求其次的 tooremove 寫入快取 hello 作業系統磁碟上因為您無法移除讀取 hello 作業系統磁碟的快取。
   * **新增 AzureProvisioningConfig**聯結 hello 您所建立的 VM toohello Active Directory 網域。
   * **Set-azuresubnet**數位 hello hello 後的子網路中的 VM。
   * **新增 AzureEndpoint**會加入存取端點，讓用戶端應用程式可以存取 hello 網際網路上的這些 SQL Server 服務執行個體。 TooContosoSQL1 和 ContosoSQL2，會提供不同的通訊埠。
   * **New-azurevm**會建立新的 SQL Server VM 的 hello hello 在相同雲端 ContosoQuorum 為服務。 您必須將 hello Vm 放在相同雲端服務如果您想要它們在 toobe hello hello 相同可用性設定組。
4. 等候每個完整佈建的 VM toobe 且每個 VM toodownload 其遠端桌面檔案 tooyour 工作目錄。 hello`for`迴圈逐一循環顯示 hello 三個新的 Vm，並為每個執行 hello hello 最上層大括號內的命令。

        Foreach ($VM in $VMs = Get-AzureVM -ServiceName $sqlServiceName)
        {
            write-host "Waiting for " $VM.Name "..."

            # Loop until hello VM status is "ReadyRole"
            While ($VM.InstanceStatus -ne "ReadyRole")
            {
                write-host "  Current Status = " $VM.InstanceStatus
                Start-Sleep -Seconds 15
                $VM = Get-AzureVM -ServiceName $VM.ServiceName -Name $VM.InstanceName
            }

            write-host "  Current Status = " $VM.InstanceStatus

            # Download remote desktop file
            Get-AzureRemoteDesktopFile -ServiceName $VM.ServiceName -Name $VM.InstanceName -LocalPath "$workingDir$($VM.InstanceName).rdp"
        }

    hello SQL Server Vm 現在已佈建並執行，但它們隨 SQL Server 安裝使用預設選項。

## <a name="initialize-hello-failover-cluster-vms"></a>初始化 hello 容錯移轉叢集的 Vm
在本節中，您會需要 toomodify hello 三部伺服器，您將使用在 hello 容錯移轉叢集與 hello SQL Server 安裝。 具體而言：

* 所有伺服器： 您需要 tooinstall hello**容錯移轉叢集**功能。
* 所有伺服器： 您需要 tooadd **CORP\Install**為 hello 機器**管理員**。
* 僅 ContosoSQL1 和 ContosoSQL2： 需要 tooadd **CORP\Install**為**sysadmin** hello 預設資料庫中的角色。
* 僅 ContosoSQL1 和 ContosoSQL2： 需要 tooadd **NT AUTHORITY\System**做為登入，以下列權限的 hello:

  * 更改所有可用性群組
  * 連接 SQL
  * 檢視伺服器狀態
* 僅 ContosoSQL1 和 ContosoSQL2: hello **TCP** hello SQL Server VM 上的通訊協定已啟用。 不過，您仍然需要 tooopen hello 防火牆供 SQL server 的遠端存取。

現在，您已準備好 toostart。 開頭為**ContosoQuorum**，依照下列步驟執行 hello:

1. 連接太**ContosoQuorum**透過啟動 hello 遠端桌面檔案。 使用 hello 電腦系統管理員的使用者名稱**AzureAdmin**和密碼**Contoso ！ 000**，這是您指定當您建立 hello Vm。
2. 請確認該 hello 電腦已成功加入太**corp.contoso.com**。
3. 等候 hello SQL Server 安裝 toofinish 執行 hello 自動初始化工作，再繼續進行。
4. 在系統管理員模式下開啟 [Azure PowerShell] 視窗。
5. 安裝 hello Windows 容錯移轉叢集功能。

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. 以本機系統管理員的身分新增 **CORP\Install**。

        net localgroup administrators "CORP\Install" /Add
7. 登出 ContosoQuorum。 此伺服器的相關作業完成。

        logoff.exe

接下來，初始化 **ContosoSQL1** 和 **ContosoSQL2**。 請遵循下列 hello 步驟，也就是相同的兩個 SQL Server Vm。

1. 透過啟動 hello 遠端桌面檔案連接 toohello 兩個 SQL Server Vm。 使用 hello 電腦系統管理員的使用者名稱**AzureAdmin**和密碼**Contoso ！ 000**，這是您指定當您建立 hello Vm。
2. 請確認該 hello 電腦已成功加入太**corp.contoso.com**。
3. 等候 hello SQL Server 安裝 toofinish 執行 hello 自動初始化工作，再繼續進行。
4. 在系統管理員模式下開啟 [Azure PowerShell] 視窗。
5. 安裝 hello Windows 容錯移轉叢集功能。

        Import-Module ServerManager
        Add-WindowsFeature Failover-Clustering
6. 以本機系統管理員的身分新增 **CORP\Install**。

        net localgroup administrators "CORP\Install" /Add
7. 匯入 hello SQL Server PowerShell 提供者。

        Set-ExecutionPolicy -Execution RemoteSigned -Force
        Import-Module -Name "sqlps" -DisableNameChecking
8. 新增**CORP\Install** hello hello 預設 SQL Server 執行個體的 sysadmin 角色。

        net localgroup administrators "CORP\Install" /Add
        Invoke-SqlCmd -Query "EXEC sp_addsrvrolemember 'CORP\Install', 'sysadmin'" -ServerInstance "."
9. 新增**NT AUTHORITY\System**做為登入，以上面所述的 hello 三個權限。

        Invoke-SqlCmd -Query "CREATE LOGIN [NT AUTHORITY\SYSTEM] FROM WINDOWS" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT ALTER ANY AVAILABILITY GROUP too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT CONNECT SQL too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
        Invoke-SqlCmd -Query "GRANT VIEW SERVER STATE too[NT AUTHORITY\SYSTEM] AS SA" -ServerInstance "."
10. 開啟 SQL server 的遠端存取的 hello 防火牆。

         netsh advfirewall firewall add rule name='SQL Server (TCP-In)' program='C:\Program Files\Microsoft SQL Server\MSSQL11.MSSQLSERVER\MSSQL\Binn\sqlservr.exe' dir=in action=allow protocol=TCP
11. 登出兩個 VM。

         logoff.exe

最後，您已準備好 tooconfigure hello 可用性群組。 您將使用 hello hello 的所有工作的 SQL Server PowerShell 提供者 tooperform **ContosoSQL1**。

## <a name="configure-hello-availability-group"></a>Hello 可用性群組設定
1. 連接太**ContosoSQL1**透過啟動 hello 遠端桌面檔案再次。 而不是使用 hello 機器帳戶登入，使用登入**CORP\Install**。
2. 在系統管理員模式下開啟 [Azure PowerShell] 視窗。
3. 定義下列變數的 hello:

        $server1 = "ContosoSQL1"
        $server2 = "ContosoSQL2"
        $serverQuorum = "ContosoQuorum"
        $acct1 = "CORP\SQLSvc1"
        $acct2 = "CORP\SQLSvc2"
        $password = "Contoso!000"
        $clusterName = "Cluster1"
        $timeout = New-Object System.TimeSpan -ArgumentList 0, 0, 30
        $db = "MyDB1"
        $backupShare = "\\$server1\backup"
        $quorumShare = "\\$server1\quorum"
        $ag = "AG1"
4. 匯入 hello SQL Server PowerShell 提供者。

        Set-ExecutionPolicy RemoteSigned -Force
        Import-Module "sqlps" -DisableNameChecking
5. ContosoSQL1 tooCORP\SQLSvc1 hello SQL Server 服務帳戶變更。

        $wmi1 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server1
        $wmi1.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct1,$password)}
        $svc1 = Get-Service -ComputerName $server1 -Name 'MSSQLSERVER'
        $svc1.Stop()
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc1.Start();
        $svc1.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
6. ContosoSQL2 tooCORP\SQLSvc2 hello SQL Server 服務帳戶變更。

        $wmi2 = new-object ("Microsoft.SqlServer.Management.Smo.Wmi.ManagedComputer") $server2
        $wmi2.services | where {$_.Type -eq 'SqlServer'} | foreach{$_.SetServiceAccount($acct2,$password)}
        $svc2 = Get-Service -ComputerName $server2 -Name 'MSSQLSERVER'
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
7. 下載**CreateAzureFailoverCluster.ps1**從[Alwayson 可用性群組的 Azure VM 中建立容錯移轉叢集](http://gallery.technet.microsoft.com/scriptcenter/Create-WSFC-Cluster-for-7c207d3a)toohello 本機工作目錄。 您將使用此指令碼 toohelp，建立運作的容錯移轉叢集。 如需 Windows 容錯移轉叢集的互動方式 hello Azure 的重要資訊網路，請參閱[Azure 虛擬機器中 SQL Server 的高可用性和災害復原](../sql/virtual-machines-windows-sql-high-availability-dr.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)。
8. 變更 tooyour 工作目錄，並建立 hello 容錯移轉叢集與 hello 下載指令碼。

        Set-ExecutionPolicy Unrestricted -Force
        .\CreateAzureFailoverCluster.ps1 -ClusterName "$clusterName" -ClusterNode "$server1","$server2","$serverQuorum"
9. 啟用 Alwayson 可用性群組 hello 預設 SQL Server 執行個體上**ContosoSQL1**和**ContosoSQL2**。

        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server1\Default `
            -Force
        Enable-SqlAlwaysOn `
            -Path SQLSERVER:\SQL\$server2\Default `
            -NoServiceRestart
        $svc2.Stop()
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Stopped,$timeout)
        $svc2.Start();
        $svc2.WaitForStatus([System.ServiceProcess.ServiceControllerStatus]::Running,$timeout)
10. 建立備份目錄，並授與 hello SQL Server 服務帳戶的權限。 Hello 次要複本上，您將使用此目錄 tooprepare hello 可用性資料庫。

         $backup = "C:\backup"
         New-Item $backup -ItemType directory
         net share backup=$backup "/grant:$acct1,FULL" "/grant:$acct2,FULL"
         icacls.exe "$backup" /grant:r ("$acct1" + ":(OI)(CI)F") ("$acct2" + ":(OI)(CI)F")
11. 上建立資料庫**ContosoSQL1**呼叫**MyDB1**、 需要完整備份和記錄備份，並在進行還原**ContosoSQL2**以 hello **WITHNORECOVERY**選項。

         Invoke-SqlCmd -Query "CREATE database $db"
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server1
         Backup-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server1 -BackupAction Log
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.bak" -ServerInstance $server2 -NoRecovery
         Restore-SqlDatabase -Database $db -BackupFile "$backupShare\db.log" -ServerInstance $server2 -RestoreAction Log -NoRecovery
12. Hello SQL Server Vm 上建立 hello 可用性群組端點，hello 端點上設定 hello 適當的權限。

         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server1\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"
         $endpoint =
             New-SqlHadrEndpoint MyMirroringEndpoint `
             -Port 5022 `
             -Path "SQLSERVER:\SQL\$server2\Default"
         Set-SqlHadrEndpoint `
             -InputObject $endpoint `
             -State "Started"

         Invoke-SqlCmd -Query "CREATE LOGIN [$acct2] FROM WINDOWS" -ServerInstance $server1
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct2]" -ServerInstance $server1
         Invoke-SqlCmd -Query "CREATE LOGIN [$acct1] FROM WINDOWS" -ServerInstance $server2
         Invoke-SqlCmd -Query "GRANT CONNECT ON ENDPOINT::[MyMirroringEndpoint] too[$acct1]" -ServerInstance $server2
13. 建立 hello 可用性複本。

         $primaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server1 `
             -EndpointURL "TCP://$server1.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
         $secondaryReplica =
             New-SqlAvailabilityReplica `
             -Name $server2 `
             -EndpointURL "TCP://$server2.corp.contoso.com:5022" `
             -AvailabilityMode "SynchronousCommit" `
             -FailoverMode "Automatic" `
             -Version 11 `
             -AsTemplate
14. 最後，建立 hello 可用性群組和聯結 hello 次要複本 toohello 可用性群組。

         New-SqlAvailabilityGroup `
             -Name $ag `
             -Path "SQLSERVER:\SQL\$server1\Default" `
             -AvailabilityReplica @($primaryReplica,$secondaryReplica) `
             -Database $db
         Join-SqlAvailabilityGroup `
             -Path "SQLSERVER:\SQL\$server2\Default" `
             -Name $ag
         Add-SqlAvailabilityDatabase `
             -Path "SQLSERVER:\SQL\$server2\Default\AvailabilityGroups\$ag" `
             -Database $db

## <a name="next-steps"></a>後續步驟
現在，您已透過在 Azure 中建立可用性群組的方式，成功實作 SQL Server Always On。 tooconfigure 這個可用性群組接聽程式，請參閱[在 Azure 中設定 Alwayson 可用性群組的 ILB 接聽程式](../classic/ps-sql-int-listener.md)。

如需在 Azure 中使用 SQL Server 的其他資訊，請參閱 [Azure 虛擬機器上的 SQL Server](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。
