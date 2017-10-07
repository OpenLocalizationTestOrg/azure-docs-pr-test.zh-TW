---
title: "在 Azure PowerShell （傳統） 中的 SQL Server 虛擬機器 aaaCreate |Microsoft 文件"
description: "提供使用 SQL Server 虛擬機器資源庫映像建立 Azure VM 的步驟和 PowerShell 指令碼。 本主題使用 hello 傳統部署模式。"
services: virtual-machines-windows
documentationcenter: na
author: rothja
manager: jhubbard
tags: azure-service-management
ms.assetid: b73be387-9323-4e08-be53-6e5928e3786e
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 08/07/2017
ms.author: jroth
ms.openlocfilehash: b14d5d9bc192fa0a21126395ee20ffd06b3bf47d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="provision-a-sql-server-virtual-machine-using-azure-powershell-classic"></a>使用 Azure PowerShell 佈建 SQL Server 虛擬機器 (傳統)

這篇文章提供如何在 Azure 中使用 SQL Server 虛擬機器 toocreate hello PowerShell 指令程式的步驟。

> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../azure-resource-manager/resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

本主題的 hello 資源管理員版本，請參閱[佈建 SQL Server 虛擬機器使用 Azure PowerShell 資源管理員](../sql/virtual-machines-windows-ps-sql-create.md)。

### <a name="install-and-configure-powershell"></a>安裝並設定 PowerShell：
1. 如果您沒有 Azure 帳戶，請造訪 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。
2. [下載並安裝最新 Azure PowerShell 命令 hello](/powershell/azure/overview)。
3. 啟動 Windows PowerShell，並將它連接 tooyour Azure 訂用帳戶以 hello **Add-azureaccount**命令。

   ```powershell
   Add-AzureAccount
   ```

## <a name="determine-your-target-azure-region"></a>決定您的目標 Azure 區域

您的 SQL Server 虛擬機器將託管於存放在特定 Azure 區域的雲端服務。 hello 下列步驟幫助您 toodetermine 您地區、 儲存體帳戶和雲端服務，用於 hello hello 教學課程的其餘部分。

1. 決定您想 toouse toohost SQL Server VM 的 hello 資料中心。 hello 下列 PowerShell 命令會顯示一份可用的地區名稱。

   ```powershell
   (Get-AzureLocation).Name
   ```

2. 一旦您已經識別您想要的位置，設定變數，名為**$dcLocation** toothat 區域。 比方說，hello 下列命令集 hello 區太 「 美國東部":

   ```powershell
   $dcLocation = "East US"
   ```

## <a name="set-your-subscription-and-storage-account"></a>設定您的訂閱和儲存體帳戶

1. 判斷 hello hello 新虛擬機器，您將使用的 Azure 訂用帳戶。

   ```powershell
   (Get-AzureSubscription).SubscriptionName
   ```

2. 指定您的目標 Azure 訂用帳戶 toohello **$subscr**變數。 然後將此設為目前的 Azure 訂用帳戶。

   ```powershell
   $subscr="<subscription name>"
   Select-AzureSubscription -SubscriptionName $subscr –Current
   ```

3. 然後檢查現有的儲存體帳戶。 hello 下列指令碼會顯示存在於您所選擇的地區中的所有儲存體帳戶：

   ```powershell
   (Get-AzureStorageAccount | where { $_.GeoPrimaryLocation -eq $dcLocation }).StorageAccountName
   ```

   > [!NOTE]
   > 如果您需要新的儲存體帳戶，請先使用如 hello 下列範例所示的 hello 新增 AzureStorageAccount 命令建立全部小寫的儲存體帳戶名稱：`New-AzureStorageAccount -StorageAccountName "<storage account name>" -Location $dcLocation`

4. 指派 hello 目標儲存體帳戶名稱 toohello **$staccount**。 然後使用**組 AzureSubscription** tooset hello 訂用帳戶和目前的儲存體帳戶。

   ```powershell
   $staccount="<storage account name>"
   Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount
   ```

## <a name="select-a-sql-server-virtual-machine-image"></a>選取 SQL Server 虛擬機器映像

1. 找出可用的 SQL Server 虛擬機器映像從 hello 組件庫的 hello 清單。 這些映像都有以「SQL」開頭的 **ImageFamily** 屬性。 hello 下列查詢會顯示 hello 映像系列可用 tooyou 具有預先安裝的 SQL Server。

   ```powershell
   Get-AzureVMImage | where { $_.ImageFamily -like "SQL*" } | select ImageFamily -Unique | Sort-Object -Property ImageFamily
   ```

2. 當您找到 hello 虛擬機器映像系列時，此系列中可能有多個已發行的映像。 使用 hello 下列指令碼 toofind hello 最新發行的虛擬機器映像您選取的映像系列名稱 (例如**SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**):

   ```powershell
   $family="<ImageFamily value>"
   $image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

   echo "Selected SQL Server image name:"
   echo "   $image"
   ```

## <a name="create-hello-virtual-machine"></a>建立 hello 的虛擬機器

最後，使用 PowerShell 建立 hello 虛擬機器：

1. 建立雲端服務 toohost hello 新的 VM。 請注意，它也可能 toouse 現有的雲端服務而。 建立新的變數**$svcname** hello hello 雲端服務的簡短名稱。

   ```powershell
   $svcname = "<cloud service name>"
   New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation
   ```

2. 指定 hello 虛擬機器名稱和大小。 如需關於虛擬機器大小的詳細資訊，請參閱 [Azure 的虛擬機器大小](../sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。

   ```powershell
   $vmname="<machine name>"
   $vmsize="<Specify one: Large, ExtraLarge, A5, A6, A7, A8, A9, or see hello link toohello other VM sizes>"
   $vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image
   ```

3. 指定 hello 本機系統管理員帳戶和密碼。

   ```powershell
   $cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
   $vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password
   ```

4. 執行下列指令碼 toocreate hello 虛擬機器的 hello。

   ```powershell
   New-AzureVM –ServiceName $svcname -VMs $vm1
   ```

> [!NOTE]
> 其他說明及組態選項，請參閱 hello**建置命令集**一節中[使用 Azure PowerShell toocreate 並預先設定 Windows 型虛擬機器](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

## <a name="example-powershell-script"></a>PowerShell 指令碼範例

hello 下列指令碼提供一個範例的完整的指令碼會建立**SQL Server 2016 RTM Enterprise on Windows Server 2012 R2**虛擬機器。 如果您使用此指令碼，您必須自訂 hello hello 本主題中的上一個步驟為基礎的初始變數。

```powershell
# Customize these variables based on your settings and requirements:
$dcLocation = "East US"
$subscr="mysubscription"
$staccount="mystorageaccount"
$family="SQL Server 2016 RTM Enterprise on Windows Server 2012 R2"
$svcname = "mycloudservice"
$vmname="myvirtualmachine"
$vmsize="A5"

# Set hello current subscription and storage account
# Comment out hello New-AzureStorageAccount line if hello account already exists
Select-AzureSubscription -SubscriptionName $subscr –Current
New-AzureStorageAccount -StorageAccountName $staccount -Location $dcLocation
Set-AzureSubscription -SubscriptionName $subscr -CurrentStorageAccountName $staccount

# Select hello most recent VM image in this image family:
$image=Get-AzureVMImage | where { $_.ImageFamily -eq $family } | sort PublishedDate -Descending | select -ExpandProperty ImageName -First 1

# Create hello new cloud service; comment out this line if cloud service exists already:
New-AzureService -ServiceName $svcname -Label $svcname -Location $dcLocation

# Create hello VM config:
$vm1=New-AzureVMConfig -Name $vmname -InstanceSize $vmsize -ImageName $image

# Set administrator credentials:
$cred=Get-Credential -Message "Type hello name and password of hello local administrator account."
$vm1 | Add-AzureProvisioningConfig -Windows -AdminUsername $cred.GetNetworkCredential().Username -Password $cred.GetNetworkCredential().Password

# Create hello SQL Server VM:
New-AzureVM –ServiceName $svcname -VMs $vm1
```

## <a name="connect-with-remote-desktop"></a>使用遠端桌面連線

1. 建立 hello RDP 檔案中 hello 目前使用者的文件資料夾 toolaunch 這些虛擬機器 toocomplete 安裝程式：

   ```powershell
   $documentspath = [environment]::getfolderpath("mydocuments")
   Get-AzureRemoteDesktopFile -ServiceName $svcname -Name $vmname -LocalPath "$documentspath\vm1.rdp"
   ```

2. 在 hello 文件目錄中，啟動 hello RDP 檔案。 連接 hello 系統管理員使用者名稱與先前提供的密碼 （例如，如果您的使用者名稱是 VMAdmin，指定"\VMAdmin"hello 使用者身分，並提供 hello 密碼）。

   ```powershell
   cd $documentspath
   .\vm1.rdp
   ```

## <a name="complete-hello-configuration-of-hello-sql-server-machine-for-remote-access"></a>Hello 遠端存取的 SQL Server 電腦的完整 hello 組態

登入與遠端桌面 toohello 機器之後，設定 SQL Server 中的 hello 指示[Azure VM 中設定 SQL Server 連接的步驟](virtual-machines-windows-classic-sql-connect.md#steps-for-configuring-sql-server-connectivity-in-an-azure-vm)。

## <a name="next-steps"></a>後續步驟

您可以找到的佈建 hello 中的虛擬機器使用 PowerShell 的其他指示[虛擬機器文件](../classic/create-powershell.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fclassic%2ftoc.json)。

在許多情況下，hello 下一個步驟是 toomigrate 資料庫 toothis 新的 SQL Server VM。 如需資料庫移轉指引，請參閱[移轉資料庫 tooSQL Azure VM 上的 Server](../sql/virtual-machines-windows-migrate-sql.md?toc=%2fazure%2fvirtual-machines%2fwindows%2fsqlclassic%2ftoc.json)。

如果您也想使用 hello Azure 入口網站 toocreate SQL 虛擬機器，請參閱[佈建在 Azure 上的 SQL Server 虛擬機器](../sql/virtual-machines-windows-portal-sql-server-provision.md)。 請注意該 hello 教學課程會逐步引導您透過 hello 入口網站建立 Vm 使用 hello 建議的資源管理員模型，而不是使用此 PowerShell 主題中的 hello 傳統模型。

此外 toothese 資源，我們建議您檢閱[相關 toorunning Azure 虛擬機器中 SQL Server 的其他主題](../sql/virtual-machines-windows-sql-server-iaas-overview.md)。
