---
title: "aaaAzure 堆疊開發套件的部署必要條件 |Microsoft 文件"
description: "檢視 Azure 堆疊開發套件 （雲端操作員） 的 hello 環境和硬體需求。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: byronr
editor: 
ms.assetid: 32a21d9b-ee42-417d-8e54-98a7f90f7311
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/11/2017
ms.author: erikje
ms.openlocfilehash: 126c851651354b6f3d61c4627ab0c1de9da12ba9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stack-deployment-prerequisites"></a>Azure Stack 部署先決條件
部署 Azure 堆疊之前[開發套件](azure-stack-poc.md)，請確定您的電腦符合下列需求的 hello:


## <a name="hardware"></a>硬體
| 元件 | 最小值 | 建議 |
| --- | --- | --- |
| 磁碟機：作業系統 |1 個 OS 磁碟 (SSD 或 HDD)，最少有 200 GB 供系統磁碟分割使用 |1 個 OS 磁碟 (SSD 或 HDD)，最少有 200 GB 供系統磁碟分割使用 |
| 磁碟機：一般開發套件資料* |4 個磁碟。 每個磁碟 (SSD 或 HDD) 提供最少 140 GB 的容量。 將會使用所有可用的磁碟。 |4 個磁碟。 每個磁碟 (SSD 或 HDD) 至少提供 250 GB 的容量。 將會使用所有可用的磁碟。 |
| 計算：CPU |雙插槽：12 個實體核心 (總計) |雙插槽：16 個實體核心 (總計) |
| 計算：記憶體 |96 GB RAM |128 GB 的 RAM （這是 hello 最小 toosupport PaaS 資源提供者）。|
| 計算：BIOS |啟用 Hyper-V (支援 SLAT) |啟用 Hyper-V (支援 SLAT) |
| 網路：NIC |NIC 所需的 Windows Server 2012 R2 憑證；不需特殊的功能 |NIC 所需的 Windows Server 2012 R2 憑證；不需特殊的功能 |
| HW 標誌憑證 |[Windows Server 2012 R2 認證](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |[Windows Server 2012 R2 認證](http://windowsservercatalog.com/results.aspx?&chtext=&cstext=&csttext=&chbtext=&bCatID=1333&cpID=0&avc=79&ava=0&avq=0&OR=1&PGS=25&ready=0) |

\*您將需要一個以上這建議容量，如果您計劃新增許多 hello [marketplace 項目](azure-stack-download-azure-marketplace-item.md)從 Azure。

**資料磁碟機組態：**所有資料磁碟機必須是都 hello 相同類型 （所有 SAS 或 SATA 所有） 和容量。 如果使用 SAS 磁碟機，hello 磁碟機必須連接透過 （提供任何的 MPIO 支援多重路徑） 的單一路徑。

**HBA 組態選項**

* (慣用) 簡單 HBA
* RAID HBA – 介面卡必須設定為「穿通」模式
* RAID HBA – 磁碟應設定為單一磁碟、RAID 0

**支援的匯流排和媒體類型組合**

* SATA HDD
* SAS HDD
* RAID HDD
* RAID SSD (如果 hello 媒體類型為 unknown 未指定\*)
* SATA SSD + SATA HDD
* SAS SSD + SAS HDD

\*不具備傳遞功能的 RAID 控制器無法辨識 hello 媒體類型。 這類控制站會將 SSD 和 HDD，皆標示為未指定。 在此情況下，hello SSD 將當做永續性儲存體，而不是快取的裝置。 因此，您可以部署在這些 Ssd 上的 hello 開發套件。

**範例 HBA**：傳遞模式中的 LSI 9207-8i、LSI-9300-8i 或 LSI-9265-8i

範例 OEM 設定可供使用。

## <a name="operating-system"></a>作業系統
|  | **需求** |
| --- | --- |
| **作業系統版本** |Windows Server 2012 R2 或更新版本。 hello 作業系統版本不是那麼重要之前 hello 部署開始，當您將 hello 主機電腦開機成 hello hello Azure 堆疊安裝中包含的 VHD。 hello 作業系統和所有必要的修補程式已整合至 hello 映像中。 請勿使用任何 Windows Server 的執行個體使用 hello 開發套件中的任何索引鍵 tooactivate。 |

## <a name="deployment-requirements-check-tool"></a>部署需求檢查工具
安裝之後 hello 作業系統，您可以使用 hello[部署適用於 Azure 堆疊檢查程式](https://gallery.technet.microsoft.com/Deployment-Checker-for-50e0f51b)tooconfirm 硬體是否符合所有 hello 需求。

## <a name="account-requirements"></a>帳戶需求
一般而言，您會透過網際網路連線，您可以在此連接 tooMicrosoft Azure 部署 hello 開發套件。 在此情況下，您必須設定 Azure Active Directory (Azure AD) 帳戶 toodeploy hello 開發套件。

如果您的環境不是連接的 toohello 網際網路或您不想 toouse Azure AD，您也可以使用 Active Directory Federation Services (AD FS) 來部署 「 Azure 堆疊。 hello 開發套件包含它自己的 AD FS 與 Active Directory 網域服務執行個體。 如果您部署使用此選項，您不需要事先帳戶 tooset。

>[!NOTE]
如果您部署使用 hello AD FS 選項，您必須重新部署 Azure 堆疊 tooswitch tooAzure AD。

### <a name="azure-active-directory-accounts"></a>Azure Active Directory 帳戶
toodeploy Azure 堆疊使用的 Azure AD 帳戶，執行 hello 部署 PowerShell 指令碼之前，您必須準備好 Azure AD 帳戶。 這個帳戶會成為 hello Azure AD 租用戶的全域管理員 hello。 它已與 Azure Active Directory 和 Graph API 的互動的所有 Azure 堆疊服務都使用 tooprovision 和委派的應用程式和服務主體。 它也會使用做為 hello hello 預設提供者訂用帳戶 （您之後可以變更） 擁有者。 您可以使用此帳戶，就可登入 tooyour Azure 堆疊系統的系統管理員入口網站。

1. 建立 Azure AD 帳戶，至少一個 Azure AD 的 hello 目錄管理員。 如果您已經有一個這樣的帳戶，則可以使用該帳戶。 否則，您可以到下列網址免費建立一個帳戶：[http://azure.microsoft.com/en-us/pricing/free-trial/](http://azure.microsoft.com/pricing/free-trial/) (如果在中國，請改為前往 <http://go.microsoft.com/fwlink/?LinkID=717821>)。 如果您計劃 toolater[向 Azure 註冊 Azure 堆疊](azure-stack-register.md)，您也必須擁有訂用帳戶中新建立的帳戶。
   
    儲存的步驟 6 中使用這些認證[部署 hello 開發套件](azure-stack-run-powershell-script.md#deploy-the-development-kit)。 這個「服務管理員」帳戶可以設定和管理資源雲端、使用者帳戶、租用戶方案、配額及價格。 在 hello 入口網站建立網站雲端、 虛擬機器私人雲端、 建立方案，便能管理使用者訂用帳戶。
2. [建立](azure-stack-add-new-user-aad.md)至少一個帳戶，讓您可以登入租用戶身分 toohello 開發套件。
   
   | **Azure Active Directory 帳戶** | **是否支援？** |
   | --- | --- |
   | 具備有效公用 Azure 訂用帳戶的公司或學校帳戶 |是 |
   | 具備有效的公用 Azure 訂用帳戶之 Microsoft 帳戶 |是 |
   | 具備有效中國 Azure 訂用帳戶的公司或學校帳戶 |是 |
   | 具備有效美國政府 Azure 訂用帳戶的公司或學校帳戶 |是 |

## <a name="network"></a>網路
### <a name="switch"></a>Switch
一個可用的通訊埠的交換器 hello 開發套件的電腦上。  

hello 開發套件的電腦支援連接 tooa 交換器存取連接埠或主幹連接埠。 Hello 交換器上所不需的任何特殊的功能。 如果您使用主幹連接埠，或者如果您需要 tooconfigure VLAN ID，您有 tooprovide hello 做為部署參數的 VLAN ID。 您可以看到在 hello 範例[部署參數清單](azure-stack-run-powershell-script.md)。

### <a name="subnet"></a>子網路
不會連接 hello 開發套件機器 toohello 下列子網路：

* 192.168.200.0/24
* 192.168.100.0/27
* 192.168.101.0/26
* 192.168.102.0/24
* 192.168.103.0/25
* 192.168.104.0/25

這些子網路會保留給 hello hello 開發套件環境內的內部網路。

### <a name="ipv4ipv6"></a>IPv4/IPv6
僅支援 IPv4。 您無法建立 IPv6 網路。

### <a name="dhcp"></a>DHCP
請確定有為 NIC 連線到該 hello hello 網路上可用的 DHCP 伺服器。 如果 DHCP 無法使用，您必須準備其他除了 hello 其中一個主機使用靜態 IPv4 網路。 您必須提供該 IP 位址和閘道作為部署參數。 您可以看到在 hello 範例[部署參數清單](azure-stack-run-powershell-script.md)。

### <a name="internet-access"></a>網際網路存取
Azure 堆疊需要存取 toohello 網際網路，直接或透過 transparent proxy。 Azure 堆疊不支援 web proxy tooenable 網際網路存取的 hello 的組態。 Hello 主機 IP 和 hello 新的 IP 指派的 toohello MA-BGPNAT01 （透過 DHCP 或靜態 IP） 必須能夠 tooaccess 網際網路。 Hello graph.windows.net 和 login.microsoftonline.com 網域下使用連接埠 80 和 443。

## <a name="telemetry"></a>遙測

遙測可協助我們打造未來的 Azure Stack 版本。 它可讓我們快速回應 toofeedback、 提供新功能，並改善品質。 Microsoft Azure Stack 包含 Windows Server 2016 和 SQL Server 2014。 這些產品都不會變更預設值，並 hello Microsoft 企業隱私權聲明會說明這兩。 Azure 堆疊也會包含已修改過的 toosend 遙測 tooMicrosoft 開放原始碼軟體。 以下是一些 Azure Stack 遙測資料範例：

- 部署註冊資訊
- 開啟和關閉警示時
- 網路資源的 hello 數目

toosupport 遙測資料流程中，連接埠 443 (HTTPS) 必須在您的網路中開啟。 https://vortex-win.data.microsoft.com hello 用戶端端點。

如果您不想要 Azure 堆疊 tooprovide 遙測，您可以在 hello 開發套件主機和 hello 的基礎結構虛擬機器如下所述將它關閉。

### <a name="turn-off-telemetry-on-hello-development-kit-host-optional"></a>關閉 hello 開發套件主機上的遙測 （選擇性）

>[!NOTE]
如果您想要關閉遙測 tooturn hello 開發套件主應用程式，您必須執行之前執行 hello 部署指令碼。

之前[執行 hello asdk installer.ps1 指令碼]()toodeploy hello 開發套件主應用程式、 開機進入 hello CloudBuilder.vhdx 和 hello 執行的下列指令碼在提升權限的 PowerShell 視窗中：
```powershell
### Get current AllowTelmetry value on DVM Host
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
### Set & Get updated AllowTelemetry value for ASDK-Host 
Set-ItemProperty-Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name "AllowTelemetry" -Value '0'  
(Get-ItemProperty -Path "HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" `
-Name AllowTelemetry).AllowTelemetry
```

設定**AllowTelemetry** too0 關閉 Windows 和 Azure 堆疊部署的遙測。 只有關鍵的安全性事件 hello 作業系統會傳送。 hello 設定的所有主機和基礎結構的 Vm，都控制 Windows 遙測，並向外延展作業發生時，會重新套用 toonew 節點/Vm。


### <a name="turn-off-telemetry-on-hello-infrastructure-virtual-machines-optional"></a>關閉 hello 基礎結構的虛擬機器上的遙測 （選擇性）

Hello 部署後成功，請執行下列指令碼在提升權限的 PowerShell 視窗中 （如 hello AzureStack\AzureStackAdmin 使用者) hello 開發套件主機上的 hello:

```powershell
$AzSVMs= get-vm |  where {$_.Name -like "AzS-*"}
### Show current AllowTelemetry value for all AzS-VMs
invoke-command -computername $AzSVMs.name {(Get-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name AllowTelemetry).AllowTelemetry}
### Set & Get updated AllowTelemetry value for all AzS-VMs
invoke-command -computername $AzSVMs.name {Set-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name "AllowTelemetry" -Value '0'}
invoke-command -computername $AzSVMs.name {(Get-ItemProperty -Path `
"HKLM:\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\DataCollection" -Name AllowTelemetry).AllowTelemetry}
```

請參閱 SQL Server 遙測 tooconfigure[如何 tooconfigure SQL Server 2016](https://support.microsoft.com/en-us/help/3153756/how-to-configure-sql-server-2016-to-send-feedback-to-microsoft)。

### <a name="usage-reporting"></a>使用量回報

透過註冊，Azure 堆疊也是設定的 tooforward 使用量資訊 tooAzure。 使用量回報是與遙測分別控制的。 您可以關閉使用方式報告時[註冊](azure-stack-register.md)Github 上使用 hello 指令碼。 只要組 hello **$reportUsage**參數太**$false**。

使用量資料會格式化為中所述的 hello[報表 Azure 堆疊使用方式資料 tooAzure](https://docs.microsoft.com/en-us/azure/azure-stack/azure-stack-usage-reporting)。 「Azure Stack 開發套件」使用者實際上無須付費。 此功能包含在 hello 開發套件，以便您可以測試的 toosee 使用方式報表的運作方式。 


## <a name="next-steps"></a>後續步驟
[下載 hello Azure 堆疊開發套件部署套件](https://azure.microsoft.com/overview/azure-stack/try/?v=try)

[部署 Azure Stack 開發套件](azure-stack-run-powershell-script.md)

