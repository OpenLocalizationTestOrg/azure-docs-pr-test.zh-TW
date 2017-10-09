---
title: "aaaOptimize VM 網路輸送量 |Microsoft 文件"
description: "了解如何 toooptimize Azure 虛擬機器的網路輸送量。"
services: virtual-network
documentationcenter: na
author: steveesp
manager: Gerald DeGrace
editor: 
ms.assetid: 
ms.service: virtual-network
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: infrastructure-services
ms.date: 07/24/2017
ms.author: steveesp
ms.openlocfilehash: a5cff2d0ab6e3553c3f90d99629521a431477de0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-network-throughput-for-azure-virtual-machines"></a>最佳化 Azure 虛擬機器的網路輸送量

Azure 虛擬機器 (VM) 有預設網路設定，可進一步針對網路輸送量進行最佳化。 本文說明如何 toooptimize 適用於 Microsoft Azure Windows 和 Linux Vm，包括主要的分佈，例如 Ubuntu、 CentOS 和 Red Hat 的網路輸送量。

## <a name="windows-vm"></a>Windows VM

如果您的 Windows VM 支援[加速網路](virtual-network-create-vm-accelerated-networking.md)，啟用該功能會 hello 最佳輸送量設定。 針對所有其他的 Windows VM，相較於不使用接收端調整 (RSS) 的 VM，使用 RSS 的 VM 可達到更高的最大輸送量。 根據預設，Windows VM 中可能會停用 RSS。 完成下列步驟 toodetermine 是否已啟用 RSS hello 和 tooenable 它已停用。

1. 輸入 hello `Get-NetAdapterRss` PowerShell 命令 toosee 如果已啟用 RSS 的網路介面卡。 在 hello 下列範例輸出傳回的 hello `Get-NetAdapterRss`，RSS 不會啟用。

    ```powershell
    Name                    : Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : False
    ```
2. 輸入下列命令 tooenable RSS hello:

    ```powershell
    Get-NetAdapter | % {Enable-NetAdapterRss -Name $_.Name}
    ```
    hello 前一個命令沒有輸出。 hello 命令變更 NIC 設定，造成連線暫時中斷約 1 分鐘。 Reconnecting 對話方塊隨即出現在 hello 連線中斷。 連線通常是 hello 第三個嘗試之後還原。
3. 確認 RSS 啟用 hello VM 中，輸入 hello`Get-NetAdapterRss`命令一次。 如果成功，則會傳回 hello 下列範例輸出：

    ```powershell
    Name                    :Ethernet
    InterfaceDescription    : Microsoft Hyper-V Network Adapter
    Enabled              : True
    ```

## <a name="linux-vm"></a>Linux VM

根據預設，Azure Linux VM 中一律會啟用 RSS。 Linux 核心發行之後 2017 年 1 月，包括新的網路最佳化選項，可讓 Linux VM tooachieve 更高的網路輸送量。

### <a name="ubuntu"></a>Ubuntu

順序 tooget hello 最佳化，在第一次更新 toohello 最新支援版本，為準，年 6 月 2017，也就是：
```json
"Publisher": "Canonical",
"Offer": "UbuntuServer",
"Sku": "16.04-LTS",
"Version": "latest"
```
Hello 更新已完成之後，請輸入下列命令 tooget hello 最新的核心 hello:

```bash
apt-get -f install
apt-get --fix-missing install
apt-get clean
apt-get -y update
apt-get -y upgrade
```

選擇性命令︰

`apt-get -y dist-upgrade`
#### <a name="ubuntu-azure-preview-kernel"></a>Ubuntu 的 Azure 預覽版核心
> [!WARNING]
> 核心可能沒有此 Azure Linux 預覽 hello 相同層級的可用性和可靠性 Marketplace 映像以及一般可用性版本的核心。 hello 功能不支援，可能有限制功能，且可能無法 hello 預設核心的可靠。 請勿將此核心使用於生產工作負載。

大幅輸送量效能可藉由安裝 hello 提議 Azure Linux 核心。 tootry 核心中，新增這行 too/etc/apt/sources.list

```bash
#add this toohello end of /etc/apt/sources.list (requires elevation)
deb http://archive.ubuntu.com/ubuntu/ xenial-proposed restricted main multiverse universe
```

然後以 root 身分執行這些命令。
```bash
apt-get update
apt-get install "linux-azure"
reboot
```

### <a name="centos"></a>CentOS

順序 tooget hello 最佳化，在第一次更新 toohello 最新支援版本，為準，年 7 月 2017，也就是：
```json
"Publisher": "OpenLogic",
"Offer": "CentOS",
"Sku": "7.3",
"Version": "latest"
```
Hello 更新已完成之後，安裝 hello 最新的 Linux Integration Services (LIS)。
hello 輸送量最佳化處於 LIS，從 4.2.2-2 開始。 輸入下列命令 tooinstall LIS hello:

```bash
sudo yum update
sudo reboot
sudo yum install microsoft-hyper-v
```

### <a name="red-hat"></a>Red Hat

順序 tooget hello 最佳化，在第一次更新 toohello 最新支援版本，為準，年 7 月 2017，也就是：
```json
"Publisher": "RedHat"
"Offer": "RHEL"
"Sku": "7.3"
"Version": "7.3.2017071923"
```
Hello 更新已完成之後，安裝 hello 最新的 Linux Integration Services (LIS)。
hello 輸送量最佳化處於 LIS，從 4.2 開始。 輸入下列命令 toodownload hello 和安裝 LIS:

```bash
mkdir lis4.2.2-2
cd lis4.2.2-2
wget https://download.microsoft.com/download/6/8/F/68FE11B8-FAA4-4F8D-8C7D-74DA7F2CFC8C/lis-rpms-4.2.2-2.tar.gz
tar xvzf lis-rpms-4.2.2-2.tar.gz
cd LISISO
install.sh #or upgrade.sh if prior LIS was previously installed
```

深入了解 Linux 整合服務版本 4.2 hyper-v 藉由檢視 hello[下載頁面](https://www.microsoft.com/download/details.aspx?id=55106)。

## <a name="next-steps"></a>後續步驟
* 既然 hello VM 會經過最佳化，請參閱 hello 結果與[頻寬/輸送量測試 Azure VM](virtual-network-bandwidth-testing.md)您的案例。
* 深入了解 [Azure 虛擬網路常見問題集 (FAQ)](virtual-networks-faq.md)
