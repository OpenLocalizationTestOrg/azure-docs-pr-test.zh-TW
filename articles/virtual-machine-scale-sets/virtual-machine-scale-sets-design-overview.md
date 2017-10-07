---
title: "Azure 虛擬機器規模集的考量 aaaDesign |Microsoft 文件"
description: "深入了解 Azure 虛擬機器擴展集的設計考量"
keywords: "linux 虛擬機器, 虛擬機器擴展集"
services: virtual-machine-scale-sets
documentationcenter: 
author: gatneil
manager: madhana
editor: tysonn
tags: azure-resource-manager
ms.assetid: c27c6a59-a0ab-4117-a01b-42b049464ca1
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 06/01/2017
ms.author: negat
ms.openlocfilehash: f8644d36fe5903bd4b74df26dca5dc3211ee3516
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="design-considerations-for-scale-sets"></a>擴展集的設計考量
本主題會討論虛擬機器擴展集的設計考量。 如需虛擬機器擴展集為何，請參閱太[虛擬機器規模集概觀](virtual-machine-scale-sets-overview.md)。

## <a name="when-toouse-scale-sets-instead-of-virtual-machines"></a>當 toouse 小數位數設定而不是虛擬機器嗎？
一般而言，擴展集適用於部署高可用性的基礎結構，其中會有一組電腦具備類似的組態。 不過，部分功能僅適用於擴展集，而其他功能僅適用於 VM。 若要 toomake 明智的決策時 toouse 每種技術，我們應該先看一下的一些常用的 hello 功能只能在擴展集而不是 Vm:

### <a name="scale-set-specific-features"></a>擴展集特定的功能

- 一旦您指定 hello 小數位數組設定，您可以只更新 「 容量 」 屬性 toodeploy hello 平行的多個 Vm。 這是比撰寫指令碼 tooorchestrate 部署許多個別的 Vm，以平行方式更簡單。
- 您可以[使用 Azure 自動調整規模 tooautomatically 調整規模集](./virtual-machine-scale-sets-autoscale-overview.md)但不是個別的 Vm。
- 您可以[重新安裝擴展集 VM 的映像](https://docs.microsoft.com/rest/api/virtualmachinescalesets/manage-a-vm)，但[無法針對個別 VM](https://docs.microsoft.com/rest/api/compute/virtualmachines) 執行。
- 您可以[過度佈建](./virtual-machine-scale-sets-design-overview.md)擴展集 VM，以提高可靠性並加快部署速度。 您無法這樣做與個別 Vm 除非您撰寫自訂程式碼 toodo 這。
- 您可以指定[升級原則](./virtual-machine-scale-sets-upgrade-scale-set.md)toomake 它輕鬆 tooroll 出在擴展集 Vm 之間的升級。 使用個別的 VM，您必須自行協調更新。

### <a name="vm-specific-features"></a>VM 特定的功能

在 hello 另一方面，某些功能僅可用於在 Vm 中 (至少的 hello 時間):

- 您可以將附加資料磁碟 toospecific 個別 Vm，但連接的資料磁碟的所有 Vm 規模集中的設定。
- 您可以將非空白的資料磁碟 tooindividual Vm 但不是 Vm 規模集中的附加。
- 您可以擷取個別 VM 的快照集，但無法針對擴展集中的 VM 執行。
- 您可以擷取個別 VM 的映像，但無法擴展集中的 VM 執行。
- 您可以從原生磁碟 toomanaged 磁碟，來移轉個別的 VM，但您無法這樣做為 Vm 規模集中的。
- 您可以指派 tooindividual VM nic IPv6 公用 IP 位址，但無法完成這項工作 Vm 規模集中的。 請注意，您可以將 IPv6 公用 IP 位址指派任一個別 Vm 前面 tooload 平衡器或擴展集 Vm。

## <a name="storage"></a>儲存體

### <a name="scale-sets-with-azure-managed-disks"></a>包含 Azure 受控磁碟的擴展集
擴展集可以使用 [Azure 受控磁碟](../virtual-machines/windows/managed-disks-overview.md)來建立，而不是傳統的 Azure 儲存體帳戶。 受管理的磁碟可提供下列優點 hello:
- 您不需要 toopre-hello 擴展集 Vm 建立一組 Azure 儲存體帳戶。
- 您可以定義[附加資料磁碟](virtual-machine-scale-sets-attached-disks.md)hello Vm 在您的標尺的設定。
- 您可以設定規模集太[支援註冊 too1，集中 000 Vm](virtual-machine-scale-sets-placement-groups.md)。 

如果您有現有的範本，您也可以[更新 hello 範本 toouse 受管理磁碟](virtual-machine-scale-sets-convert-template-to-md.md)。

### <a name="user-managed-storage"></a>使用者管理的儲存體
Azure 受管理的磁碟未定義擴展集依賴使用者建立的儲存體帳戶 toostore hello OS 磁碟的 hello 集合中的 hello Vm。 每個儲存體帳戶，或小於 20 的 Vm 的比例，建議使用 tooachieve 最大 IO 也利用_過度佈建_（請參閱下文）。 也建議 hello 字母分散 hello 起始字元的 hello 儲存體帳戶名稱。 這樣做有助於將負載分散到不同的內部系統。 


## <a name="overprovisioning"></a>過度佈建
小數位數設定目前預設太 「 過度佈建 」 的 Vm。 與過度佈建為開啟，hello 小數位數會設定實際旋轉啟動比系統要求您提供，多個 Vm，然後刪除的 hello 成功佈建額外的 Vm，一旦 hello 要求的 Vm 數目。 過度佈建可改善佈建成功率並縮短部署時間。 您就不需付費的 hello 額外的 Vm，而且它們不會計配額限制。

儘管過度佈建並改善佈建的成功率，它可能會導致應用程式產生混淆的行為，是不設計的 toohandle 額外的 Vm 出現，然後消失。 tooturn 過度佈建，請確定您有下列字串在範本中的 hello: `"overprovision": "false"`。 更多詳細資料位於 hello[小數位數設定的 REST API 文件](/rest/api/virtualmachinescalesets/create-or-update-a-set)。

如果小數位數組會使用受使用者管理的存放裝置，而且您關閉過度佈建，您可以有 20 個以上的 Vm，每個儲存體帳戶，但不是建議 toogo 上方 40 的 IO 效能的考量。 

## <a name="limits"></a>限制
擴展集建立 Marketplace 映像 （也稱為平台映像），並設定的 toouse Azure 受管理磁碟支援 too1，000 Vm 的總容量。 如果您設定您的小數位數組 toosupport 100 個以上的 Vm，並非所有的情況下工作 hello 相同 （適用於負載平衡的範例）。 如需詳細資訊，請參閱[使用大型的虛擬機器擴展集](virtual-machine-scale-sets-placement-groups.md)。 

在擴展集與使用者管理的儲存體帳戶設定為目前限制的 too100 Vm （和這個標尺的建議使用 5 個儲存體帳戶）。

建置的自訂映像 （一個由您所建立） 上的小數位數集可以有啟動 too100 Vm 時設定了 Azure 受管理的磁碟容量。 如果 hello 規模集與使用者管理的儲存體帳戶設定，就必須建立一個儲存體帳戶內的所有作業系統磁碟 Vhd。 如此一來，hello 最大建議數目的 Vm 規模集中的自訂映像上建置，使用者管理的儲存體是 20。 如果您關閉過度佈建，您可以向上 too40。

適用於多個 Vm 超過這些限制允許，您需要多個小數位數設定中所示的 toodeploy[此範本](https://github.com/Azure/azure-quickstart-templates/tree/master/301-custom-images-at-scale)。

