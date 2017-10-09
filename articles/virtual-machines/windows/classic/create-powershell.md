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
# <a name="create-a-windows-virtual-machine-with-powershell-and-hello-classic-deployment-model"></a>使用 PowerShell 和 hello 傳統部署模型中建立 Windows 虛擬機器
> [!div class="op_single_selector"]
> * [Azure 入口網站 - Windows](tutorial.md)
> * [PowerShell - Windows](create-powershell.md)
> 
> 

<br>

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。 了解如何太[使用 hello 資源管理員的模型執行這些步驟](../../virtual-machines-windows-ps-create.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

這些步驟顯示如何 toocustomize 一組的 Azure PowerShell 命令，建立並預先設定 windows Azure 虛擬機器使用的建置組塊方法。 您可以使用此程序 tooquickly 建立新的 windows 虛擬機器的一組命令，並擴充現有的部署一或多個命令會將設定的快速 toocreate 建置自訂的開發/測試或 IT 專業人員的環境。

這些步驟遵循建立 Azure PowerShell 命令集合的填空方法。 如果您是新 tooPowerShell 或只是想 tooknow 哪些值 toospecify 成功的組態，這種方法十分有用。 進階的 PowerShell 使用者可以採取 hello 命令，並以取代其值為 hello 變數 （hello 行開頭為"$"）。

如果還沒有這麼做，使用中的 hello 指示[如何 tooinstall 和設定 Azure PowerShell](/powershell/azure/overview) tooinstall Azure PowerShell，在本機電腦上的。 然後，開啟 Windows PowerShell 命令提示字元。

## <a name="step-1-add-your-account"></a>步驟 1︰加入您的帳戶
1. 在 hello PowerShell 提示字元中輸入**Add-azureaccount**按一下**Enter**。 
2. 輸入您 Azure 訂用帳戶相關聯的 hello 電子郵件地址，然後按一下**繼續**。 
3. 輸入 hello 您帳戶的密碼。 
4. 按一下 [ **登入**]。

## <a name="step-2-set-your-subscription-and-storage-account"></a>步驟 2：設定您的訂用帳戶和儲存體帳戶
Hello Windows PowerShell 命令提示字元中執行這些命令來設定您的 Azure 訂用帳戶和儲存體帳戶。 Hello 括在引號，包括 hello < 和 > 字元內的所有項目取代 hello 正確名稱。

    $subscr="<subscription name>"
    $staccount="<storage account name>"
    Select-AzureSubscription -SubscriptionName $subscr –Current
    Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

您可以從 hello 的 hello hello 輸出的訂用帳戶名稱屬性來取得 hello 正確的訂用帳戶名稱**Get-azuresubscription**命令。 您可以從 hello Label 屬性的 hello hello 輸出取得 hello 正確的儲存體帳戶名稱**Get AzureStorageAccount**命令之後執行 hello **Select-azuresubscription**命令。

## <a name="step-3-determine-hello-imagefamily"></a>步驟 3： 決定 hello ImageFamily
接下來，您需要 toodetermine hello ImageFamily 或標籤值 hello 特定映像對應 toohello 想 toocreate 的 Azure 虛擬機器。 您可以取得 hello 可用 ImageFamily 值，這個命令的清單。

    Get-AzureVMImage | select ImageFamily -Unique

以下是以 Windows 為基礎的電腦本身 ImageFamily 值的一些範例：

* Windows Server 2012 R2 Datacenter
* Windows Server 2008 R2 SP1
* Windows Server 2016 Technical Preview 4
* SQL Server 2012 SP1 Enterprise on Windows Server 2012

如果您發現您所需的 hello 映像，請開啟 選擇或 hello PowerShell 整合式指令碼環境 (ISE) 的 hello 文字編輯器的新執行個體。 將下列 hello 複製到新文字檔 hello 或 hello PowerShell ISE 中，以取代 hello ImageFamily 值。

    $family="<ImageFamily value>"
    $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

在某些情況下，hello 映像名稱已在 hello Label 屬性，而不是 hello ImageFamily 值。 如果找不到想要使用 hello ImageFamily 屬性的 hello 映像，會依其 Label 屬性，此命令列出 hello 映像。

    Get-AzureVMImage | select Label -Unique

如果您發現 hello 這個命令的正確映像，請開啟 hello 文字編輯器選項或 hello PowerShell ISE 的新執行的個體。 將下列 hello 複製到新文字檔 hello 或 hello PowerShell ISE 中，以取代 hello 標籤值。

    $label="<Label value>"
    $image = Get-AzureVMImage | where { $_.Label -eq $label } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

## <a name="step-4-build-your-command-set"></a>步驟 4：建置命令集
建置 hello 其餘部分將 hello 適當的一組區塊下方複製到您新的文字檔或 hello ISE 然後填入 hello 變數值並移除 hello < 和 > 字元來設定您的命令。 請參閱 hello 兩[範例](#examples)hello 以了解 hello 最終結果的這篇文章結尾處。

選擇兩個命令區塊的其中一個，啟動命令集 (必要)。

選項 1：指定虛擬機器名稱和大小。

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

選項 2：指定名稱、大小和可用性設定組名稱。

    $vmname="<machine name>"
    $vmsize="<Specify one: Small, Medium, Large, ExtraLarge, A5, A6, A7, A8, A9>"
    $availset="<set name>"
    $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image -AvailabilitySetName $availset

D、 DS 或 G 系列虛擬機器的 hello InstanceSize 值，請參閱[虛擬機器和 Azure 的雲端服務大小](https://msdn.microsoft.com/library/azure/dn197896.aspx)。

> [!NOTE]
> 如果您有 Enterprise 合約附有軟體保證，而想 tootake 利用 Windows Server hello[混合使用權益](https://azure.microsoft.com/pricing/hybrid-use-benefit/)，新增**-LicenseType**參數 toohello **New-azurevmconfig** cmdlet，將傳遞 hello 值**Windows_Server** hello 一般使用案例。  請務必使用您已上傳; 映像您無法使用從 hello 組件庫的標準映像以 hello 混合使用好處。
> 
> 

（選擇性） 針對獨立 Windows 電腦，指定 hello 本機系統管理員帳戶和密碼。

    $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
    $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.Username -Password $cred.GetNetworkCredential().Password

選擇強式密碼。 toocheck 其強度，請參閱[密碼檢查程式： 使用強式密碼](https://www.microsoft.com/security/pc-security/password-checker.aspx)。

（選擇性） tooadd hello Windows 電腦 tooan 現有 Active Directory 網域，指定 hello 本機系統管理員帳戶和密碼、 hello 網域以及 hello 名稱和密碼的網域帳戶。

    $cred1=Get-Credential –Message "Type hello name and password of hello local administrator account."
    $cred2=Get-Credential –Message "Now type hello name (not including hello domain) and password of an account that has permission tooadd hello machine toohello domain."
    $domaindns="<FQDN of hello domain that hello machine is joining>"
    $domacctdomain="<domain of hello account that has permission tooadd hello machine toohello domain>"
    $vm1 | Add-AzureProvisioningConfig -AdminUsername $cred1.Username -Password $cred1.GetNetworkCredential().Password -WindowsDomain -Domain $domacctdomain -DomainUserName $cred2.Username -DomainPassword $cred2.GetNetworkCredential().Password -JoinDomain $domaindns

Windows 型虛擬機器的其他預先設定選項，請參閱 hello hello 語法**Windows**和**WindowsDomain**參數會設定[新增 AzureProvisioningConfig](/powershell/module/azure/add-azureprovisioningconfig)。

選擇性地指派特定的 IP 位址，稱為靜態 DIP hello 虛擬機器。

    $vm1 | Set-AzureStaticVNetIP -IPAddress <IP address>

您可以確認特定 IP 位址可用於：

    Test-AzureStaticVNetIP –VNetName <VNet name> –IPAddress <IP address>

選擇性地指派 hello 虛擬機器 tooa 特定子網路中的 Azure 虛擬網路。

    $vm1 | Set-AzureSubnet -SubnetNames "<name of hello subnet>"

（選擇性） 加入單一資料磁碟 toohello 虛擬機器。

    $disksize=<size of hello disk in GB>
    $disklabel="<hello label on hello disk>"
    $lun=<Logical Unit Number (LUN) of hello disk>
    $hcaching="<Specify one: ReadOnly, ReadWrite, None>"
    $vm1 | Add-AzureDataDisk -CreateNew -DiskSizeInGB $disksize -DiskLabel $disklabel -LUN $lun -HostCaching $hcaching

Active Directory 網域控制站設定 $hcaching 太"None"。

（選擇性） 加入 hello 虛擬機器 tooan 現有負載平衡集外部流量。

    $protocol="<Specify one: tcp, udp>"
    $localport=<port number of hello internal port>
    $pubport=<port number of hello external port>
    $endpointname="<name of hello endpoint>"
    $lbsetname="<name of hello existing load-balanced set>"
    $probeprotocol="<Specify one: tcp, http>"
    $probeport=<TCP or HTTP port number of probe traffic>
    $probepath="<URL path for probe traffic>"
    $vm1 | Add-AzureEndpoint -Name $endpointname -Protocol $protocol -LocalPort $localport -PublicPort $pubport -LBSetName $lbsetname -ProbeProtocol $probeprotocol -ProbePort $probeport -ProbePath $probepath

最後，選擇其中一個這些必要的命令區塊，如建立 hello 的虛擬機器。

選項 1： 建立現有的雲端服務中的 hello 虛擬機器。

    New-AzureVM –ServiceName "<short name of hello cloud service>" -VMs $vm1

hello hello 雲端服務的簡短名稱是出現在 hello 清單的雲端服務或資源群組的 hello Azure 入口網站中的 hello 清單 hello Azure 入口網站中的 hello 名稱。

選項 2： 建立在現有的雲端服務和虛擬網路中的 hello 虛擬機器。

    $svcname="<short name of hello cloud service>"
    $vnetname="<name of hello virtual network>"
    New-AzureVM –ServiceName $svcname -VMs $vm1 -VNetName $vnetname

## <a name="step-5-run-your-command-set"></a>步驟 5：執行命令集
檢閱您在文字編輯器中建立 hello Azure PowerShell 命令集，或 hello 步驟 4 中的命令的多個區塊所組成的 PowerShell ISE。 請確定您已指定所有必要的 hello 變數，而且它們有 hello 正確的值。 也請確定您已移除所有 hello < 和 > 字元。

如果您使用文字編輯器，複製 hello 命令設定 toohello 剪貼簿，然後以滑鼠右鍵按一下 開啟 Windows PowerShell 命令提示字元。 這會為一系列的 PowerShell 命令發出 hello 命令集，並建立 Azure 虛擬機器。 或者，執行設定 hello PowerShell ISE 中的 hello 命令。

如果您將再次建立這個虛擬機器或類似的虛擬機器，您可以：

* 將此命令集儲存為 PowerShell 指令碼檔案 (*.ps1)。
* 儲存此設定為在 hello Azure 自動化 runbook 的命令**自動化帳戶**hello Azure 入口網站的區段。

## <a id="examples"></a>範例
以下是兩個範例使用 hello 上方建立 windows Azure 虛擬機器的 toobuild Azure PowerShell 命令集的步驟。

### <a name="example-1"></a>範例 1
我需要 PowerShell 命令集 toocreate hello 初始虛擬機器的 Active Directory 網域控制站：

* 使用 hello Windows Server 2012 R2 Datacenter 映像。
* 具有 hello AZDC1 的名稱。
* 屬於獨立電腦。
* 有 20 GB 的額外資料磁碟。
* 具有靜態 IP 位址 hello 192.168.244.4。
* Hello 後端 hello AZDatacenter 虛擬網路子網路內。
* Hello Azure TailspinToys 雲端服務內。

以下是 hello 對應 Azure PowerShell 命令集 toocreate 之間可讀性的每個區塊的空白行與此虛擬機器。

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

### <a name="example-2"></a>範例 2
我需要 PowerShell 命令設定 toocreate 業務的伺服器虛擬機器的：

* 使用 hello Windows Server 2012 R2 Datacenter 映像。
* 具有 hello LOB1 的名稱。
* 是 hello corp.contoso.com 網域的成員。
* 具有 200 GB 的額外資料磁碟。
* Hello AZDatacenter 虛擬網路的 hello FrontEnd 子網路內。
* Hello Azure TailspinToys 雲端服務內。

以下是 hello 對應 Azure PowerShell 命令集 toocreate 此虛擬機器。

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


## <a name="next-steps"></a>後續步驟
如果您需要大於 127 GB 的作業系統磁碟，您可以[展開 hello 作業系統磁碟機](../../virtual-machines-windows-expand-os-disk.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

