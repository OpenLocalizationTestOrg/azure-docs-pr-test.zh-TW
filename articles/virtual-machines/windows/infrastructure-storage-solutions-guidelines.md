---
title: "適用於 Windows Vm 在 Azure 中的 aaaStorage 解決方案 |Microsoft 文件"
description: "深入了解 hello 金鑰設計和實作部署的指導方針 Azure 基礎結構服務中的儲存解決方案。"
documentationcenter: 
services: virtual-machines-windows
author: iainfoulds
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 4ceb7d32-7a0d-4004-b701-c2bbcaff6b0b
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: na
ms.topic: article
ms.date: 06/26/2017
ms.author: iainfou
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 57c27a7305964a56e6b2d1e73dee8e7da19fa8f8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-storage-infrastructure-guidelines-for-windows-vms"></a>適用於 Windows VM 的 Azure 儲存體基礎結構指導方針

[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-intro](../../../includes/virtual-machines-windows-infrastructure-guidelines-intro.md)]

本文著重於了解達成最佳虛擬機器 (VM) 效能的儲存體需求及設計考量。

## <a name="implementation-guidelines-for-storage"></a>儲存體的實作指導方針
决策：

* 您將要 toouse Azure 受管理的磁碟或未受管理的磁碟嗎？
* 您是否有您的工作負載需要 toouse Standard 或 Premium 儲存體？
* 您是否需要磁碟條狀配置 toocreate 磁碟超過 4 TB？
* 您是否有您的工作負載需要磁碟條狀配置 tooachieve 最佳 I/O 效能？
* 哪些設定的儲存體帳戶是否需要 toohost 您的 IT 工作負載或基礎結構？

工作：

* 檢查 I/O 要求的 hello 應用程式部署，並規劃 hello 適當數目和類型的儲存體帳戶。
* 建立儲存體帳戶使用您的命名慣例 hello 組。 您可以使用 Azure PowerShell 或 hello 入口網站。

## <a name="storage"></a>儲存體
Azure 儲存體是部署和管理虛擬機器 (VM) 和應用程式的重要部分。 Azure 儲存體提供服務，用於儲存檔案資料、 非結構化的資料，以及訊息，而且它也支援 Vm 的 hello 基礎結構的一部分。

[受管理的 azure 磁碟](../../storage/storage-managed-disks-overview.md)hello 幕後為您處理儲存體。 使用 unmanaged 磁碟時，您建立儲存體帳戶 toohold hello 磁碟 （VHD 檔案） 為您的 Azure Vm。 當向上擴充，您必須確定您沒有任何磁碟超過儲存體的 hello IOPS 限制，因此，建立額外的儲存體帳戶。 使用受管理磁碟時處理儲存體，您都不會再受到 hello 儲存體帳戶限制 (例如 20000 IOPS / 帳戶)。 您也不再有 toocopy 您自訂映像 （VHD 檔案） toomultiple 儲存體帳戶。 您可以在中央位置 – 一個儲存體帳戶每個 Azure 區域 – 中管理它們，並用 toocreate 數百個 Vm 的訂用帳戶中。 我們建議您針對新的部署使用受控磁碟。

有兩種可供支援 VM 使用的儲存體帳戶：

* 標準儲存體帳戶提供您存取 tooblob （用來儲存 Azure VM 磁碟） 的儲存體，資料表儲存體，佇列儲存體和檔案儲存體。
* [進階儲存體](../../storage/storage-premium-storage.md) 帳戶可針對 I/O 密集的工作負載提供高效能且低延遲的磁碟支援 (例如 AlwaysOn 叢集中的 SQL Server)。 進階儲存體目前僅支援 Azure VM 磁碟。

Azure 會建立含有一個作業系統磁碟、一個暫存磁碟，以及零或多個選用資料磁碟的 VM。 hello 作業系統磁碟和資料磁碟會 Azure 分頁 blob，而 hello 暫存磁碟儲存在本機上 hello hello 機器所在的節點中。 請小心設計 tooonly 作為此暫存磁碟的非永續性資料 hello VM 可能會維護事件期間的主機之間移轉應用程式時。 Hello 暫存磁碟上儲存的任何資料將會遺失。

持續性和高可用性是由提供 hello 基礎的 Azure 儲存體環境 tooensure 您資料會保持保護以防止未規劃的維護或硬體失敗。 當您設計您的 Azure 儲存體環境，您可以選擇 tooreplicate VM 儲存體：

* 在指定 Azure 資料中心的本機上
* 在指定區域內跨 Azure 資料中心
* 跨不同區域內且跨 Azure 資料中心

您可以閱讀[更多關於高可用性的 hello 複寫選項](../../storage/storage-introduction.md#replication-for-durability-and-high-availability)。

作業系統磁碟和資料磁碟具有 4TB 的大小上限。 您可以一起共用的資料磁碟 toopresent 邏輯磁碟區大於 4 TB tooyour VM 所使用儲存空間的 Windows Server 2012 或更新版本的 toosurpass 這項限制。

設計 Azure 儲存體部署時有幾個延展性的限制 - 如需詳細資訊，請參閱 [Microsoft Azure 訂用帳戶和服務限制、配額與限制](../../azure-subscription-service-limits.md#storage-limits)。 另請參閱〈 [Azure 儲存體的延展性與效能目標](../../storage/storage-scalability-targets.md)〉。

針對應用程式儲存體，您可以儲存非結構化的物件資料，例如文件、影像、備份、設定資料、記錄檔等等。 使用 Blob 儲存體。 而不是您的應用程式撰寫 tooa 連接的虛擬磁碟 toohello VM hello 應用程式可以直接寫入 tooAzure blob 儲存體。 Blob 儲存體也會提供 hello 選項[熱和冷卻儲存層](../../storage/storage-blob-storage-tiers.md)視您的可用性需求和成本條件約束。

## <a name="striped-disks"></a>等量磁碟
除了可讓您 toocreate 磁碟超過 4 TB，在許多情況下，使用針對資料磁碟條狀配置可提高效能，藉由允許多個 blob tooback hello 儲存體的單一磁碟區。 使用等量，hello I/O 需要 toowrite，然後從單一的邏輯磁碟讀取的資料進行以平行方式。

Azure 會加諸限制 hello 資料磁碟數目和 hello VM 大小而定，可用的頻寬量。 如需詳細資訊，請參閱 [虛擬機器的大小](sizes.md)。

如果您使用 Azure 資料磁碟的磁碟條狀配置，請考慮下列指導方針的 hello:

* 附加 hello hello VM 大小所允許的最大的資料磁碟。
* 使用儲存空間。
* 避免使用 Azure 資料磁碟快取選項 (快取原則 = 無)。

如需詳細資訊，請參閱〈 [儲存體空間 - 適用於效能的設計](http://social.technet.microsoft.com/wiki/contents/articles/15200.storage-spaces-designing-for-performance.aspx)〉。

## <a name="multiple-storage-accounts"></a>多個儲存體帳戶
本節不適太[Azure 受管理磁碟](../../storage/storage-managed-disks-overview.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)，因為您不會建立個別的儲存體帳戶。 

在設計您的 Azure 儲存體環境未受管理的磁碟時，您可以使用多個儲存體帳戶做為 Vm 的 hello 數部署會增加。 這種方式有助於分散出 hello I/O 跨 hello 基礎 Azure 儲存體基礎結構 toomaintain 最佳效能的 Vm 和應用程式。 當您設計要部署的 hello 應用程式，請考慮 hello I/O 的需求，每個 VM 並平衡這些 Vm 出跨 Azure 儲存體帳戶。 分組所有 Vm 要求 (demand) toojust 一或兩個儲存體帳戶中的 hello 高 I/O tooavoid 再試一次。

如需 hello I/O 功能 hello 不同的 Azure 儲存體選項的詳細資訊，以及一些建議的最大值，請參閱 < [Azure 儲存體延展性和效能目標](../../storage/storage-scalability-targets.md)。

## <a name="next-steps"></a>後續步驟
[!INCLUDE [virtual-machines-windows-infrastructure-guidelines-next-steps](../../../includes/virtual-machines-windows-infrastructure-guidelines-next-steps.md)]

