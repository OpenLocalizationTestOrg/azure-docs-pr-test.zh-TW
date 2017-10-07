---
title: "在 Azure 中的 Linux Vm 的 aaaOverview |Microsoft 文件"
description: "描述 Azure 計算、儲存體和網路服務與 Linux 虛擬機器。"
services: virtual-machines-linux
documentationcenter: virtual-machines-linux
author: rickstercdn
manager: timlt
editor: 
ms.assetid: 7965a80f-ea24-4cc2-bc43-60b574101902
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 09/14/2016
ms.author: rclaus
ms.custom: H1Hack27Feb2017, mvc
ms.openlocfilehash: 958e219d53026d787a7a41f2fd13c29c739a9238
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-and-linux"></a>Azure 和 Linux
Microsoft Azure 集結了各種整合式公用雲端服務且數量不斷增加，包括分析、虛擬機器、資料庫、行動、網路、儲存體和 Web&mdash;因此很適合用來裝載您的方案。  Microsoft Azure 提供可擴充的運算平台，可讓您的功能，當您想使用它-而不需要在內部部署硬體 tooinvest tooonly 付款。  Azure 還，如果您設定的解決方案是 tooscale 且 toowhatever 標尺出中，您需要 tooservice hello 需求的用戶端。

如果您已熟悉 hello Amazon 的各種功能 AWS，您可以檢查 hello Azure vs AWS[定義對應文件](https://azure.microsoft.com/campaigns/azure-vs-aws/mapping/)。

## <a name="regions"></a>區域
Microsoft Azure 資源會分散到 hello 世界各地的多個地理區域。  「區域」代表單一地理區域中的多個資料中心。  我們有 34 地區上市 hello 世界各地宣布其他 4 個區域。 因為我們會繼續 tooexpand 我們全域的涵蓋範圍-我們維護現有的和新的更新的清單宣布的區域。

* [Azure 區域](https://azure.microsoft.com/regions/)

## <a name="availability"></a>Availability
我們宣佈業界前置單一執行個體的虛擬機器 99.9%的服務等級協定提供部署 hello VM 的所有磁碟的進階儲存體。  為了讓您對我們的標準 99.95%的部署 tooqualify VM 的服務等級協定，您仍然需要 toodeploy 執行您的工作負載的可用性設定組內的兩個或多個 Vm。 這可確保您的 VM 會分散在我們資料中心內的多個容錯網域，以及部署至具有不同維護期間的主機。 完整的 hello [Azure SLA](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_0/)說明 hello 保證整個 Azure 的可用性。

## <a name="managed-disks"></a>受控磁碟

管理的控制代碼 Azure 儲存體帳戶建立與管理 hello 背景中的，並確保您沒有 tooworry hello hello 儲存體帳戶的延展性限制的相關的磁碟。 您只需要指定 hello 磁碟大小和 hello 效能層 （Standard 或 Premium），Azure 會建立，並會為您管理 hello 磁碟。 即使當您新增磁碟或向上和向下調整 hello VM 時，您不需要 tooworry 需 hello 所使用的儲存體。 如果您要建立新的 Vm[使用 hello Azure CLI 2.0](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)或 hello Azure 入口網站 toocreate Vm 與管理作業系統和資料磁碟。 如果您有未受管理磁碟 Vm，您可以[轉換受管理的磁碟備份您的 Vm toobe](convert-unmanaged-to-managed-disks.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

您也可以管理每個 Azure 區域中，一個儲存體帳戶中的自訂映像，並使用它們 toocreate 數以百計的 Vm 中 hello 相同訂用帳戶。 如需有關管理磁碟的詳細資訊，請參閱 hello[受管理的磁碟概觀](../windows/managed-disks-overview.md)。

## <a name="azure-virtual-machines--instances"></a>Azure 虛擬機器和執行個體
Microsoft Azure 支援執行由多家合作夥伴提供和維護的眾多熱門 Linux 散發套件。  您會發現例如 Red Hat Enterprise、 CentOS、 Debian，Ubuntu、 CoreOS、 RancherOS、 FreeBSD 和多 hello Azure Marketplace 中的分佈。 我們目前正在使用的各種 Linux 社群 tooadd 更多的類別 toohello [Azure 背書 Linux 散發版本](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)清單。

如果您選擇的慣用的 Linux distro 不是目前在 hello 組件庫中，您可以 「 攜帶您自己的 Linux 」 的 VM[建立和上傳 Linux VHD 在 Azure 中](create-upload-generic.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

Azure 虛擬機器可讓您 toodeploy 各種敏捷的方式來運算解決方案。 您可以在大部分的作業系統 (Windows、Linux，或來自我們持續增加合作夥伴的自訂建立作業系統)，部署幾乎任何工作負載和任何語言。 還是沒找到您在尋找的映像嗎？  別擔心，您也可以使用您在內部部署中擁有的映像。

## <a name="vm-sizes"></a>VM 大小
當您部署 Azure 中的 VM 時，您將 tooselect 我們系列的大小適合 tooyour 工作負載的其中一個內的 VM 大小。 hello 大小也會影響 hello 處理能力、 記憶體與 hello 虛擬機器的儲存容量。 您需要根據 hello 金額時間 hello VM 正在執行，而且耗用配置的資源付費。 完整的[虛擬機器大小](sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)清單。

以下是一些從我們提供的系列 (A、D、DS、G 和 GS) 中選取一個 VM 大小的基本指導方針。
* A 系列 VM 是物超所值的入門級 VM，適用於輕度工作負載和開發/測試案例。 廣泛適用於所有地區和可以連接並使用所有的標準資源可用 toovirtual 機器。
* A 系列大小 (A8 - A11) 則是特殊的可進行大量運算的組態，適用於高效能的運算叢集應用程式。
* D 系列 Vm 是需要較高運算能力和暫存磁碟效能的設計的 toorun 應用程式。 D 系列 Vm 提供更快的處理器、 記憶體-核心比率較高，以及固態硬碟 (SSD) hello 暫存磁碟。
* Dv2 系列是我們 D 系列 hello 最新版本、 功能更強大的 CPU。 hello Dv2 數列 CPU 大約是 35%速度 hello D 系列 CPU。 它基礎 hello 最新的層代 2.4 GHz Intel Xeon® E5-2673 v3 (Haskell) 處理器，以 hello Intel 快速提升技術 2.0，最高 too3.2 GHz。 hello Dv2 數列有 hello 相同的記憶體和磁碟組態，如 hello D 系列。
* G 系列 Vm 提供 hello 最多記憶體，並在有 Intel Xeon E5 V3 系列處理器的主機上執行。

注意： DS 系列和 GS 系列 Vm 有存取 tooPremium 儲存體-我們 SSD 備份 I/O 密集型工作負載的高效能、 低延遲的儲存體。 僅特定地區可用進階儲存體。 如需詳細資訊，請參閱：

* [進階儲存體：Azure 虛擬機器工作負載適用的高效能儲存體](../../storage/common/storage-premium-storage.md)

## <a name="automation"></a>自動化
tooachieve 適當的 DevOps 文化特性，所有基礎結構必須是程式碼。  當所有 hello 基礎結構的程式碼可輕鬆地重新建立 （in Phoenix 伺服器）。  Azure 會搭配所有 hello 主要自動化 Ansible、 Chef、 SaltStack 和 Puppet 等工具。  Azure 也有自己的自動化工具：

* [Azure 範本](create-ssh-secured-vm-from-template.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Azure VMAccess](using-vmaccess-extension.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

Azure 將針對支援 [cloud-init](http://cloud-init.io/) 的大多數 Linux 散發套件推出 cloud-init 支援。  目前 Canonical 的 Ubuntu VM 部署預設即已啟用 cloud-init。  紅色 Hats RHEL、 CentOS 和支援雲端 init，不過 hello Azure Fedora RedHat 所維護的映像並沒有安裝雲端 init。  toouse 雲端 for-init RedHat 系列作業系統上，您必須建立自訂映像與安裝雲端 init。

* [在 Azure Linux VM 上使用 cloud-init](using-cloud-init.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="quotas"></a>配額
每個 Azure 訂用帳戶有預設配額限制的可能會影響 hello 部署大量的 Vm 為您的專案。 每個訂用帳戶為基礎的 hello 目前限制為 20 的 Vm，每個區域。  只要提出支援票證來要求增加限制，即可快速且輕鬆地提高配額限制。  如需有關配額限制的詳細資料：

* [Azure 訂用帳戶服務限制](../../azure-subscription-service-limits.md)

## <a name="partners"></a>合作夥伴
Microsoft 密切與我們的合作夥伴提供的 tooensure hello 映像會更新，並針對 Azure 的執行階段最佳化。  如需有關我們合作夥伴的詳細資訊，請查看下方他們的市集頁面。

* [Azure 背書散發套件上的 Linux](endorsed-distros.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* SUSE - [Azure Marketplace - SUSE Linux Enterprise Server](https://azuremarketplace.microsoft.com/en-us/marketplace/apps?search=%27SUSE%27)
* Redhat - [Azure Marketplace - RedHat Enterprise Linux 7.2](https://azure.microsoft.com/marketplace/partners/redhat/redhatenterpriselinux72/)
* Canonical - [Azure Marketplace - Ubuntu Server 16.04 LTS](https://azure.microsoft.com/marketplace/partners/canonical/ubuntuserver1604lts/)
* Debian - [Azure Marketplace - Debian 8 "Jessie"](https://azure.microsoft.com/marketplace/partners/credativ/debian8/)
* FreeBSD - [Azure Marketplace - FreeBSD 10.3](https://azure.microsoft.com/marketplace/partners/microsoft/freebsd103/)
* CoreOS - [Azure Marketplace - CoreOS (Stable)](https://azure.microsoft.com/marketplace/partners/coreos/coreosstable/)
* RancherOS - [Azure Marketplace - RancherOS](https://azure.microsoft.com/marketplace/partners/rancher/rancheros/)
* Bitnami - [適用於 Azure 的 Bitnami 程式庫](https://azure.bitnami.com/)
* Mesosphere - [Azure Marketplace - Azure 上的 Mesosphere DC/OS](https://azure.microsoft.com/marketplace/partners/mesosphere/dcosdcos/)
* Docker - [Azure Marketplace - 與 Docker Swarm 搭配使用的 Azure Container Service](https://azure.microsoft.com/marketplace/partners/microsoft/acsswarms/)
* Jenkins - [Azure Marketplace - CloudBees Jenkins Platform](https://azure.microsoft.com/marketplace/partners/cloudbees/jenkins-platformjenkins-platform/)

## <a name="getting-started-with-linux-on-azure"></a>在 Azure 上開始使用 Linux
使用的 Azure 需要 Azure 帳戶、 hello 安裝，Azure CLI 和的 SSH 公開金鑰和私密金鑰的金鑰組 toobegin。

### <a name="sign-up-for-an-account"></a>註冊帳戶
hello 使用 hello Azure 雲端中的第一個步驟是 toosign 註冊 Azure 帳戶。  移 toohello [Azure 帳戶中註冊](https://azure.microsoft.com/pricing/free-trial/)tooget 啟動頁面上。

### <a name="install-hello-cli"></a>安裝 hello CLI
與新的 Azure 帳戶，您可以立即使用開始 hello Azure 入口網站，也就是網頁型管理面板。  透過命令列 hello toomanage hello Azure 雲端，安裝 hello `azure-cli`。  安裝 hello [Azure CLI 2.0](/cli/azure/install-azure-cli) Mac 或 Linux 的工作站上。

### <a name="create-an-ssh-key-pair"></a>建立 SSH 金鑰組
現在您有 Azure 帳戶、 hello Azure 入口網站中，與 hello Azure CLI。  hello 下一個步驟是 toocreate 不使用密碼是使用的 tooSSH 到 Linux 的 SSH 金鑰組。  [建立 Linux 和 Mac 上的 SSH 金鑰](mac-create-ssh-keys.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)tooenable 無密碼登入和更佳的安全性。

### <a name="create-a-vm-using-hello-cli"></a>使用 hello CLI 建立 VM
建立 Linux VM 使用 hello CLI 是快速 toodeploy 不讓 hello 終端機您工作所在的 VM。  您可以指定 hello web 入口網站上的所有項目可透過命令列的旗標或交換器。  

* [建立 Linux VM 使用 hello CLI](quick-create-cli.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="create-a-vm-in-hello-portal"></a>在 hello 入口網站中建立 VM
Hello Azure web 入口網站中建立 Linux VM 是方式 tooeasily 點，並透過按一下 hello 各種選項 tooget tooa 部署。  不使用命令列的旗標或交換器，您就可以 tooview 的各種選項和設定好的 web 版面配置。  可透過 hello 命令列介面使用的所有項目也會提供在 hello 入口網站。

* [建立 Linux VM 使用 hello 入口網站](quick-create-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

### <a name="login-using-ssh-without-a-password"></a>使用 SSH 登入而不提供密碼
hello VM 現在在 Azure 上執行，而且您會在準備好 toolog。  使用透過 SSH 的密碼 toolog 中是不安全且耗時。  使用 SSH 金鑰是 hello 最安全的方式，也是最快方式 toologin hello。  如果您建立 Linux VM 透過 hello 入口網站或 hello CLI，則會有兩個的驗證選項。  如果您選擇密碼 ssh，Azure 會設定密碼透過 hello VM tooallow 登入。  如果您選擇 toouse SSH 公開金鑰，Azure 會設定 hello VM tooonly 允許透過 SSH 登入索引鍵，並停用密碼登入。 允許 SSH 金鑰的登入，使用您的 Linux VM 的唯一 toosecure hello SSH 公用金鑰期間，使用選項 hello CLI hello 入口網站中建立的 VM。

## <a name="related-azure-components"></a>相關的 Azure 元件
## <a name="storage"></a>儲存體
* [簡介 tooMicrosoft Azure 儲存體](../../storage/common/storage-introduction.md)
* [新增磁碟 tooa Linux VM 使用 hello azure cli](add-disk.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [Tooattach 資料磁碟 tooa Linux VM hello Azure 入口網站中的方式](attach-disk-portal.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="networking"></a>網路
* [虛擬網路概觀](../../virtual-network/virtual-networks-overview.md)
* [Azure 中的 IP 位址](../../virtual-network/virtual-network-ip-addresses-overview-arm.md)
* [在 Azure 中開啟連接埠 tooa Linux VM](nsg-quickstart.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)
* [在 hello Azure 入口網站中建立完整網域名稱](portal-create-fqdn.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)

## <a name="containers"></a>容器
* [Azure 中的虛擬機器和容器](containers.md)
* [Azure 容器服務簡介](../../container-service/container-service-intro.md)
* [部署 Azure 容器服務叢集](../../container-service/dcos-swarm/container-service-deployment.md)

## <a name="next-steps"></a>後續步驟
您現在已概略了解 Azure 上的 Linux。  hello 下一個步驟是 toodive 中的，並建立一些 Vm ！

* [探索透過 AzureCLI 執行一般工作的指令碼範例清單 (不斷增加中)](cli-samples.md)
