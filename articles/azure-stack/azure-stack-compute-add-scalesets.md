---
title: "設定 Azure 堆疊中可用的 aaaMake 虛擬機器規模"
description: "了解雲端系統管理員可以將虛擬機器規模 toohello Marketplace</堆疊"
services: azure-stack
author: anjayajodha
ms.service: azure-stack
ms.topic: article
ms.date: 8/4/2017
ms.author: anajod
keywords: 
ms.openlocfilehash: 14365d62ac2f2bc453c25ce4769464eb30180ea8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="make-virtual-machine-scale-sets-available-in-azure-stack"></a>在 Azure Stack 中提供虛擬機器擴展集
虛擬機器擴展集是 Azure Stack 計算資源。 您可以使用這些 toodeploy 和管理一組相同的虛擬機器。 設定的所有虛擬機器與 hello 相同，規模集不需要預先佈建虛擬機器。 很容易 toobuild 中大規模服務 big compute、 大型資料，以及進行容器化工作負載為目標。

本主題會引導您完成 hello 程序 toomake 規模集 hello Marketplace</堆疊中提供。 完成此程序之後，使用者可以將虛擬機器規模設定 tootheir 訂用帳戶。

Azure Stack 上的虛擬機器擴展集就像是 Azure 上的虛擬機器擴展集。 如需詳細資訊，請參閱下列影片 hello:
* [Mark Russinovich 講述 Azure 擴展集](https://channel9.msdn.com/Blogs/Regular-IT-Guy/Mark-Russinovich-Talks-Azure-Scale-Sets/)
* [Guy Bowerman 與虛擬機器擴展集](https://channel9.msdn.com/Shows/Cloud+Cover/Episode-191-Virtual-Machine-Scale-Sets-with-Guy-Bowerman)

在 Azure Stack 上，虛擬機器擴展集不支援自動擴展。 您可以新增使用 hello Azure 堆疊入口網站、 資源管理員範本或 PowerShell 設定多個執行個體 tooa 標尺。

## <a name="prerequisites"></a>必要條件
* **Powershell 和工具**

   安裝和設定的 PowerShell for Azure 堆疊和 hello Azure 堆疊工具。 請參閱[在 Azure Stack 使用 PowerShell 啟動和執行](azure-stack-powershell-configure-quickstart.md)。

   您安裝 hello Azure 堆疊工具之後，請確定您匯入下列 PowerShell 模組的 hello (路徑相對 toohello。 \ComputeAdmin 資料夾中的 hello AzureStack 工具主資料夾):

        Import-Module .\AzureStack.ComputeAdmin.psm1

* **作業系統映像**

   如果您沒有加入作業系統映像 tooyour Marketplace</堆疊，請參閱[新增 hello Windows Server 2016 VM 映像 toohello Azure 堆疊 marketplace](azure-stack-add-default-image.md)。

   如需 Linux 支援，下載 Ubuntu Server 16.04，並將它使用```Add-AzsVMImage```以 hello 下列參數： ```-publisher "Canonical" -offer "UbuntuServer" -sku "16.04-LTS"```。

## <a name="add-hello-virtual-machine-scale-set"></a>新增 hello 虛擬機器規模集

編輯下列 PowerShell 指令碼環境，然後加以執行虛擬機器規模集 tooyour Marketplace</堆疊 tooadd hello。 

``$User``這是您使用 tooconnect hello 管理員入口網站的 hello 帳戶。 例如： serviceadmin@contoso.onmicrosoft.com。

```
$Arm = "https://adminmanagement.local.azurestack.external"
$Location = "local"

Add-AzureRMEnvironment -Name AzureStackAdmin -ArmEndpoint $Arm

$Password = ConvertTo-SecureString -AsPlainText -Force "<your Azure Stack administrator password>"

$User = "<your Azure Stack service administrator user name>"

$Creds =  New-Object System.Management.Automation.PSCredential $User, $Password

$AzsEnv = Get-AzureRmEnvironment AzureStackAdmin
$AzsEnvContext = Add-AzureRmAccount -Environment $AzsEnv -Credential $Creds
Select-AzureRmProfile -Profile $AzsEnvContext

Select-AzureRmSubscription -SubscriptionName "Default Provider Subscription"

Add-AzsVMSSGalleryItem -Location $Location
```

## <a name="remove-a-virtual-machine-scale-set"></a>移除虛擬機器擴展集

tooremove 的虛擬機器擴展集主機庫項目，執行下列 PowerShell 命令的 hello:

    Remove-AzsVMSSGalleryItem

> [!NOTE]
> hello 主機庫項目可能不會立即移除。 移除從 hello Marketplace 之前您可能需要指定 toorefresh hello 入口網站數次。


## <a name="next-steps"></a>後續步驟
[Azure Stack 的常見問題集](azure-stack-faq.md)

