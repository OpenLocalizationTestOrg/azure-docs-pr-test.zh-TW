---
title: "aaaManage HPC Pack 叢集計算節點 |Microsoft 文件"
description: "深入了解 PowerShell 指令碼工具 tooadd、 移除、 啟動，以及停止在 Azure 中的 HPC Pack 2012 R2 叢集計算節點"
services: virtual-machines-windows
documentationcenter: 
author: dlepow
manager: timlt
editor: 
tags: azure-service-management,hpc-pack
ms.assetid: 4193f03b-94e9-4704-a7ad-379abde063a9
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-multiple
ms.workload: big-compute
ms.date: 12/29/2016
ms.author: danlep
ms.openlocfilehash: 5ac1142cc5da984020779434fbb7cba5ad7c14bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-hello-number-and-availability-of-compute-nodes-in-an-hpc-pack-cluster-in-azure"></a>管理 hello 數目和計算節點，在 Azure 中部署 HPC Pack 叢集中的可用性
如果您在 Azure Vm 中建立的 HPC Pack 2012 R2 叢集，您可能想 tooeasily 新增、 移除、 啟動 （佈建），或一些停止 （解除佈建） 的方式計算節點 Vm，叢集中。 toodo 這些工作，執行 hello 前端節點 VM 上安裝 Azure PowerShell 指令碼。 這些指令碼可協助您控制 hello 數目和 HPC Pack 叢集資源的可用性，您可以控制成本。

> [!IMPORTANT] 
> 本文適用於僅 tooHPC Pack 2012 R2 中的叢集使用 hello 傳統部署模型所建立的 Azure。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。
> 此外，本文中所述的 hello PowerShell 指令碼中沒有 HPC Pack 2016。

## <a name="prerequisites"></a>必要條件
* **在 Azure Vm 中的 HPC Pack 2012 R2 叢集**: hello 傳統部署模型中建立與 HPC Pack 2012 R2 的叢集。 例如，您可以使用 hello hello Azure Marketplace 中的 HPC Pack 2012 R2 VM 映像和 Azure PowerShell 指令碼自動化 hello 部署。 資訊和必要條件，請參閱[以 hello HPC Pack IaaS 部署指令碼建立 HPC 叢集](hpcpack-cluster-powershell-script.md)。
  
    部署之後，hello 節點管理指令碼中尋找 hello %ccp\_hello 前端節點上的主目錄 %bin 資料夾。 系統管理員身分執行每個 hello 指令碼。
* **Azure 發行設定檔案或管理憑證**： 需要 hello 前端節點上的 toodo hello 下列其中一種：
  
  * **匯入 hello Azure 發行設定檔**。 toodo 下列 Azure PowerShell cmdlet hello 前端節點上，執行的 hello:
    
    ```PowerShell
    Get-AzurePublishSettingsFile
    
    Import-AzurePublishSettingsFile –PublishSettingsFile <publish settings file>
    ```
  * **Hello 前端節點上設定 hello Azure 管理憑證**。 如果您擁有 hello.cer 檔案，它匯入 hello CurrentUser\My 憑證存放區，然後再執行下列 Azure PowerShell cmdlet （AzureCloud 或 AzureChinaCloud） 您 Azure 環境的 hello:
    
    ```PowerShell
    Set-AzureSubscription -SubscriptionName <Sub Name> -SubscriptionId <Sub ID> -Certificate (Get-Item Cert:\CurrentUser\My\<Cert Thrumbprint>) -Environment <AzureCloud | AzureChinaCloud>
    ```

## <a name="add-compute-node-vms"></a>新增計算節點 VM
加入計算節點以 hello **Add-hpciaasnode.ps1**指令碼。

### <a name="syntax"></a>語法
```PowerShell
Add-HPCIaaSNode.ps1 [-ServiceName] <String> [-ImageName] <String>
 [-Quantity] <Int32> [-InstanceSize] <String> [-DomainUserName] <String> [[-DomainUserPassword] <String>]
 [[-NodeNameSeries] <String>] [<CommonParameters>]

```
### <a name="parameters"></a>參數
* **ServiceName**: hello 新增計算節點 Vm 的雲端服務名稱加入。
* **ImageName**: Azure VM 映像名稱，可透過 hello Azure 傳統入口網站或 Azure PowerShell cmdlet 取得**Get-azurevmimage**。 hello 映像必須符合下列需求的 hello:
  
  1. 必須安裝 Windows 作業系統。
  2. 必須安裝 HPC Pack 在 hello 運算節點角色。
  3. hello 映像必須是 hello 使用者分類，不是公用 Azure VM 映像中的私人映像。
* **數量**： 加入計算節點 Vm toobe 數目。
* **InstanceSize**: hello 的大小計算節點 Vm。
* **DomainUserName**： 網域使用者名稱，也就是使用的 toojoin hello 新 Vm toohello 網域。
* **DomainUserPassword**: hello 網域使用者的密碼。
* **NodeNameSeries** （選擇性）： hello 的計算節點命名模式。 hello 格式必須為&lt;*根\_名稱*&gt;&lt;*啟動\_數目*&gt;%。 例如，MyCN %10%表示一系列的 hello 計算從 MyCN11 開始的節點名稱。 如果未指定，則 hello 指令碼會使用 hello 設定 hello HPC 叢集中節點命名序列。

### <a name="example"></a>範例
hello 下列範例會將 20 大型運算節點 Vm hello 雲端服務中*hpcservice1 中新增*根據 hello VM 映像， *hpccnimage1*。

```PowerShell
Add-HPCIaaSNode.ps1 –ServiceName hpcservice1 –ImageName hpccniamge1
–Quantity 20 –InstanceSize Large –DomainUserName <username>
-DomainUserPassword <password>
```


## <a name="remove-compute-node-vms"></a>移除計算節點 VM
移除計算節點以 hello **Remove-hpciaasnode.ps1**指令碼。

### <a name="syntax"></a>語法
```PowerShell
Remove-HPCIaaSNode.ps1 -Name <String[]> [-DeleteVHD] [-Force] [-WhatIf] [-Confirm] [<CommonParameters>]

Remove-HPCIaaSNode.ps1 -Node <Object> [-DeleteVHD] [-Force] [-Confirm] [<CommonParameters>]
```

### <a name="parameters"></a>參數
* **名稱**： 移除叢集節點 toobe 的名稱。 支援萬用字元。 hello 參數集名稱為 Name。 您不能指定兩個 hello**名稱**和**節點**參數。
* **節點**: hello HpcNode 物件物件 hello 節點 toobe 移除，可以透過 hello HPC PowerShell cmdlet 取得[Get-hpcnode 取得](https://technet.microsoft.com/library/dn887927.aspx)。 hello 參數集名稱為節點。 您不能指定兩個 hello**名稱**和**節點**參數。
* **DeleteVHD** （選擇性）： 設定 toodelete 相關聯的 hello hello 會移除的 Vm 磁碟。
* **強制**（選擇性）： 移除之前，先設定 tooforce HPC 節點離線。
* **確認**（選擇性）： hello 命令在執行之前確認提示。
* **WhatIf**： 如果您執行 hello 命令，而不實際執行 hello 命令設定 toodescribe 什麼會發生。

### <a name="example"></a>範例
hello 下列範例會強制離線 hello 節點名稱開頭*為 Hpcnode-cn-CN-*並加以移除 hello 節點和其相關聯的磁碟。

```PowerShell
Remove-HPCIaaSNode.ps1 –Name HPCNodeCN-* –DeleteVHD -Force
```

## <a name="start-compute-node-vms"></a>啟動計算節點 VM
開始計算節點以 hello **Start-hpciaasnode.ps1**指令碼。

### <a name="syntax"></a>語法
```PowerShell
Start-HPCIaaSNode.ps1 -Name <String[]> [<CommonParameters>]

Start-HPCIaaSNode.ps1 -Node <Object> [<CommonParameters>]
```
### <a name="parameters"></a>參數
* **名稱**: hello 叢集節點 toobe 名稱開始。 支援萬用字元。 hello 參數集名稱為 Name。 您不能指定兩個 hello**名稱**和**節點**參數。
* **節點**-hello HpcNode 物件物件 hello 節點 toobe 啟動，可以透過 hello HPC PowerShell cmdlet 取得[Get-hpcnode 取得](https://technet.microsoft.com/library/dn887927.aspx)。 hello 參數集名稱為節點。 您不能指定兩個 hello**名稱**和**節點**參數。

### <a name="example"></a>範例
hello 下列範例會啟動節點名稱開頭*為 Hpcnode-cn-CN-*。

```PowerShell
Start-HPCIaaSNode.ps1 –Name HPCNodeCN-*
```

## <a name="stop-compute-node-vms"></a>停止計算節點 VM
停止運算節點以 hello **Stop-hpciaasnode.ps1**指令碼。

### <a name="syntax"></a>語法
```PowerShell
Stop-HPCIaaSNode.ps1 -Name <String[]> [-Force] [<CommonParameters>]

Stop-HPCIaaSNode.ps1 -Node <Object> [-Force] [<CommonParameters>]
```

### <a name="parameters"></a>參數
* **名稱**-停止 hello 叢集節點 toobe 的名稱。 支援萬用字元。 hello 參數集名稱為 Name。 您不能指定兩個 hello**名稱**和**節點**參數。
* **節點**: hello HpcNode 物件物件 hello 節點 toobe 停止，可以透過 hello HPC PowerShell cmdlet 取得[Get-hpcnode 取得](https://technet.microsoft.com/library/dn887927.aspx)。 hello 參數集名稱為節點。 您不能指定兩個 hello**名稱**和**節點**參數。
* **強制**（選擇性）： 設定 tooforce HPC 節點離線之前加以停止。

### <a name="example"></a>範例
hello 下列範例會強制離線的節點名稱開頭*為 Hpcnode-cn-CN-*和停駐點然後 hello 節點。

```PowerShell
Stop-HPCIaaSNode.ps1 –Name HPCNodeCN-* -Force
```

## <a name="next-steps"></a>後續步驟
* tooautomatically 成長或壓縮 hello 根據目前的工作負載 hello 工作及工作 hello 叢集上的叢集節點，請參閱[自動擴增和縮減 Azure 相應 toohello 叢集工作負載中helloHPCPack叢集資源](hpcpack-cluster-node-autogrowshrink.md).

