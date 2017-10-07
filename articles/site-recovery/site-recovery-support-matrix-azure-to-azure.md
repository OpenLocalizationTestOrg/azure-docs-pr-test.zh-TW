---
title: "aaaAzure 站台復原支援比對從 Azure tooAzure 複寫 |Microsoft 文件"
description: "摘要說明支援 hello 作業系統及設定 Azure Site Recovery 的 Azure 虛擬機器 (Vm) 的複寫從嚴重損壞修復 (DR) 所需的一個區域 tooanother。"
services: site-recovery
documentationcenter: 
author: sujayt
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/10/2017
ms.author: sujayt
ms.openlocfilehash: 75b2451b4c2069ca4b11deb0efe1329d43879eb8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-site-recovery-support-matrix-for-replicating-from-azure-tooazure"></a>從 Azure tooAzure 伺服器複寫的 azure Site Recovery 支援矩陣


>[!NOTE]
>
> Azure 虛擬機器的 Site Recovery 複寫目前為預覽狀態。

本文摘要說明支援的設定和元件複寫和復原 Azure 虛擬機器從一個區域 tooanother 區域時，Azure Site recovery。

## <a name="user-interface-options"></a>使用者介面選項

**使用者介面** |  **支援 / 不支援**
--- | ---
**Azure 入口網站** | 支援
**傳統入口網站** | 不支援
**PowerShell** | 目前不支援
**REST API** | 目前不支援
**CLI** | 目前不支援


## <a name="resource-move-support"></a>資源移動支援

**資源移動類型** | **支援 / 不支援** | **備註**  
--- | --- | ---
**在資源群組間移動保存庫** | 不支援 |您無法跨越資源群組移動 hello 復原服務保存庫。
**跨越資源群組移動運算、 儲存體和網路** | 不支援 |如果您在啟用複寫之後移動虛擬機器 （或其相關聯的元件，例如儲存體和網路），您會需要 toodisable 複寫，及啟用的 hello 虛擬機器複寫一次。


## <a name="support-for-deployment-models"></a>部署模型的支援

**部署模型** | **支援 / 不支援** | **備註**  
--- | --- | ---
**傳統** | 支援 | 您只能複寫傳統的虛擬機器，並將它復原為傳統的虛擬機器。 您無法將它復原為資源管理員虛擬機器。 如果您部署的傳統的 VM，而不需要虛擬網路並直接 tooan Azure 區域，它不支援。
**資源管理員** | 支援 |

## <a name="support-for-replicated-machine-os-versions"></a>支援多種複寫機器作業系統版本

hello 支援以下是適用 hello 上執行任何工作負載所述的作業系統。

#### <a name="windows"></a>Windows

- Windows Server 2016 (伺服器核心和含有桌面體驗的伺服器)*
- Windows Server 2012 R2
- Windows Server 2012
- Windows Server 2008 R2 (至少加裝 SP1)

>[!NOTE]
>
> 不支援 \* Windows Server 2016 Nano Server。

#### <a name="linux"></a>Linux

- Red Hat Enterprise Linux 6.7、6.8、7.0、7.1、7.2、7.3
- CentOS 6.5、6.6、6.7、6.8、7.0、7.1、7.2、7.3
- Ubuntu 14.04 LTS 伺服器 [(支援的核心版本)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Ubuntu 16.04 LTS 伺服器 [(支援的核心版本)](#supported-ubuntu-kernel-versions-for-azure-virtual-machines)
- Oracle Enterprise Linux 6.4，6.5 執行 hello Red Hat 相容核心或以企業核心的第 3 版 (UEK3)
- SUSE Linux Enterprise Server 11 SP3

>[!NOTE]
>
> Ubuntu 伺服器使用的密碼驗證和登入，與使用 hello 雲端 init 封裝 tooconfigure 雲端虛擬機器，可能有密碼在容錯移轉 （取決於 hello cloudinit 組態。） 時停用的登入密碼型登入可以是 hello 的藉由重設 hello 設定 功能表中 （在 hello 支援 + 疑難排解 > 一節） 的容錯移轉 hello Azure 入口網站上的虛擬機器 hello 密碼 hello 虛擬機器上重新啟用。

### <a name="supported-ubuntu-kernel-versions-for-azure-virtual-machines"></a>Azure 虛擬機器支援的 Ubuntu 核心版本

**版本** | **行動服務版本** | **核心版本** |
--- | --- | --- |
14.04 LTS | 9.9 | 3.13.0-24-generic too3.13.0 117-泛型，<br/>3.16.0-25-generic too3.16.0-77-一般<br/>3.19.0-18-generic too3.19.0-80-一般<br/>4.2.0-18-generic too4.2.0-42-一般<br/>4.4.0-21-generic too4.4.0 75 泛型 |
14.04 LTS | 9.10 | 3.13.0-24-generic too3.13.0 121-泛型，<br/>3.16.0-25-generic too3.16.0-77-一般<br/>3.19.0-18-generic too3.19.0-80-一般<br/>4.2.0-18-generic too4.2.0-42-一般<br/>4.4.0-21-generic too4.4.0 81 泛型 |
16.04 LTS | 9.10 | 4.4.0-21-generic too4.4.0 81-泛型，<br/>4.8.0-34-generic too4.8.0-56-一般<br/>4.10.0-14-generic too4.10.0 24 泛型 |

## <a name="supported-file-systems-and-guest-storage-configurations-on-azure-virtual-machines-running-linux-os"></a>Azure 虛擬機器 (執行 Linux OS) 上的支援檔案系統與客體儲存體組態

* 檔案系統：ext3、ext4、ReiserFS (僅 Suse Linux Enterprise Server)、XFS
* 磁碟區管理員：LVM2
* 多重路徑軟體：裝置對應程式

## <a name="region-support"></a>區域支援

您可以複製和復原 Vm hello 任何兩個區域間相同地理叢集。

**地理叢集** | **Azure 區域**
-- | --
美洲 | 加拿大東部、加拿大中部、美國中南部、美國中西部、美國東部、美國東部 2、美國西部、美國西部 2、美國中部、美國中北部
歐洲 | 英國西部、英國南部、北歐、西歐
亞洲 | 印度南部、印度中部、東南亞、東亞、日本東部、日本西部、韓國中部、韓國南部
澳大利亞   | 澳大利亞東部、澳大利亞東南部

>[!NOTE]
>
> 巴西南部區域，您只能複寫和容錯移轉 tooone 美國中南部、 美國西部、 美國東部、 美國東部 2、 美國西部、 美國西部 2 和美國中北部地區和失敗的備份。


## <a name="support-for-compute-configuration"></a>計算設定的支援

**組態** | **支援/不支援** | **備註**
--- | --- | ---
大小 | 至少 2 顆 CPU 核心和 1 GB RAM 的任何 Azure VM 大小 | 請參閱太[Azure 虛擬機器大小](../virtual-machines/windows/sizes.md)
可用性集合 | 支援 | 如果您在入口網站中使用 hello '啟用複寫 步驟期間的預設選項，hello 可用性設定組是自動建立根據來源的地區設定。 您可以變更 hello 目標可用性設定組 '複寫項目 > 設定 > 計算與網路 > 可用性設定組' 任何時間。
Hybrid Use Benefit | 支援 | 如果 hello 來源 VM 已啟用的中樞授權，hello 測試容錯移轉或容錯移轉 VM 也會使用 hello 中樞授權。
虛擬機器擴展集 | 不支援 |
Azure 資源庫映像 - Microsoft 發行 | 支援 | 只要 hello VM 在支援的作業系統上執行站台復原支援
Azure 資源庫映像 - 第三方發行 | 支援 | 只要 hello VM 在支援的作業系統上執行站台復原支援。
自訂映像 - 第三方發行 | 支援 | 只要 hello VM 在支援的作業系統上執行站台復原支援。
使用 Site Recovery 移轉 VM | 支援 | 如果它是 VMware/實體機器遷移 tooAzure 使用站台復原，您需要 toouninstall hello 較舊版本的行動服務，並重新啟動 hello 機器，再將它複寫 tooanother Azure 區域。

## <a name="support-for-storage-configuration"></a>儲存體設定的支援

**組態** | **支援/不支援** | **備註**
--- | --- | ---
最大的作業系統磁碟大小 | 1023 GB | 請參閱太[Vm 所使用的磁碟。](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
最大的資料磁碟大小 | 1023 GB | 請參閱太[Vm 所使用的磁碟。](../virtual-machines/windows/about-disks-and-vhds.md#disks-used-by-vms)
資料磁碟數量 | 特定 Azure VM 大小支援多達 64 個 | 請參閱太[Azure 虛擬機器大小](../virtual-machines/windows/sizes.md)
暫存磁碟 | 一律排除在複寫之外 | 暫存磁碟排除在複寫之外。 根據 Azure 指引，您不應該在暫存磁碟上放置任何持續性資料。 請參閱太[Azure Vm 上的暫存磁碟](../virtual-machines/windows/about-disks-and-vhds.md#temporary-disk)如需詳細資訊。
資料變更率 hello 磁碟上 | 各磁碟資料變更率最高達 6 MBps | 如果 hello 平均資料變更率上 hello 磁碟超出 6 MBps 持續，複寫會趕上。 不過，如果它是偶爾資料高載而且 hello 資料變更速率大於 6 MBps 段時間，這時候您就要，複寫會趕上進度。 在此情況下，您可能會發現復原點稍微延遲。
標準儲存體帳戶上的磁碟 | 支援 |
進階儲存體帳戶上的磁碟 | 支援 | 如果 VM 有分散 premium 和標準儲存體帳戶的磁碟，您可以選取不同的目標儲存體帳戶的每個磁碟 tooensure 您擁有 hello 目標區域中的相同儲存體設定
標準受控磁碟 | 不支援 |  
進階受控磁碟 | 不支援 |
儲存體空間 | 支援 |         
待用加密 (SSE) | 支援 | 對於快取和目標儲存體帳戶，您可以選取 SSE 啟用的儲存體帳戶。     
Azure 磁碟加密 (ADE) | 不支援 |
熱新增/移除磁碟 | 不支援 | 如果您新增或移除 hello VM 上的資料磁碟時，您需要 toodisable 複寫並啟用一次複寫 hello VM。
排除磁碟 | 不支援|   預設排除暫存磁碟。
LRS | 支援 |
GRS | 支援 |
RA-GRS | 支援 |
ZRS | 不支援 |  
非經常性和經常性儲存體 | 不支援 | 非經常性和經常性儲存體不支援虛擬機器磁碟

>[!IMPORTANT]
> 請確定您遵循 hello[儲存體指引](../storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks)針對您的來源 Azure 虛擬機器 tooavoid 任何效能問題。 如果您遵循 hello 預設設定，站台復原就會建立所需的 hello hello 來源設定為基礎的儲存體帳戶。 如果您自訂，並選取您自己的設定，請確定您遵循 hello (../ storage/common/storage-scalability-targets.md#scalability-targets-for-virtual-machine-disks） 做為來源的 Vm。

## <a name="support-for-network-configuration"></a>網路組態的支援
**組態** | **支援/不支援** | **備註**
--- | --- | ---
網路介面 (NIC) | 特定 Azure VM 大小支援的 NIC 數目上限 | Hello VM 建立的測試容錯移轉或容錯移轉作業時，會建立 Nic。 hello hello hello Nic hello 來源 VM 已啟用複寫的 hello 次的數目取決於 VM 的容錯移轉的 Nic 數目。 如果您新增/移除 NIC 啟用複寫後，它不會影響在 hello 容錯移轉 VM NIC 計數。
網際網路負載平衡器 | 支援 | 您需要 tooassociate hello 預先設定復原方案中使用 azure 自動化指令碼的負載平衡器。
內部負載平衡器 | 支援 | 您需要 tooassociate hello 預先設定復原方案中使用 azure 自動化指令碼的負載平衡器。
公用 IP| 支援 | 您需要 tooassociate 現有公用 IP toohello NIC 或建立並關聯 toohello NIC 復原方案中使用 azure 自動化指令碼。
NIC 上的 NSG (資源管理員)| 支援 | 您需要 tooassociate hello NSG toohello NIC 復原方案中使用 azure 自動化指令碼。  
子網路上的 NSG (資源管理員與傳統)| 支援 | 您需要 tooassociate hello NSG toohello NIC 復原方案中使用 azure 自動化指令碼。
VM 上的 NSG (傳統)| 支援 | 您需要 tooassociate hello NSG toohello NIC 復原方案中使用 azure 自動化指令碼。
保留的 IP (靜態 IP) / 保留來源 IP | 支援 | 如果 hello hello 來源 VM 上的 NIC 具有靜態 IP 組態和 hello 目標子網路具有 hello 相同 IP 可用，它會指派 toohello 容錯移轉 VM。 如果 hello 目標子網路沒有相同的 IP，其中一個 hello 中的可用 Ip hello hello 子網路被保留供此 VM。 您可以在 [複寫項目] > [設定] > [計算與網路] > [網路介面] 中指定選擇的固定 IP。 您可以選取 hello NIC，並指定 hello 子網路和您選擇的 IP。
動態 IP| 支援 | 如果 hello NIC hello 來源 VM 上的動態 IP 組態，hello hello 容錯移轉的 NIC VM 也是動態預設。 您可以在 [複寫項目] > [設定] > [計算與網路] > [網路介面] 中指定選擇的固定 IP。 您可以選取 hello NIC，並指定 hello 子網路和您選擇的 IP。
流量管理員整合 | 支援 | 您可以預先設定您的流量管理員的方式 hello 流量會容錯移轉時的目標區域中的規則而 toohello 端點上的來源地區中的路由的 toohello 端點。
Azure 受管理 DNS | 支援 |
自訂 DNS  | 支援 |    
未經驗證的 Proxy | 支援 | 請參閱太[網路指引文件。](site-recovery-azure-to-azure-networking-guidance.md)    
經驗證的 Proxy | 不支援 | 如果 hello VM 的傳出連線使用已驗證的 proxy，它不能使用 Azure Site Recovery 會複寫。  
在內部部署 （不論有無 ExpressRoute） 的站台 tooSite VPN| 支援 | 請確定設定 hello UDRs 和 Nsg hello 站台復原的資料流不是路由的 tooon 內部部署的方式。 請參閱太[網路指引文件。](site-recovery-azure-to-azure-networking-guidance.md)  
VNET tooVNET 連線 | 支援 | 請參閱太[網路指引文件。](site-recovery-azure-to-azure-networking-guidance.md)  


## <a name="next-steps"></a>後續步驟
- 深入了解[複寫 Azure VM 的網路指引](site-recovery-azure-to-azure-networking-guidance.md)
- [複寫 Azure VM](site-recovery-azure-to-azure.md) 開始保護您的工作負載
