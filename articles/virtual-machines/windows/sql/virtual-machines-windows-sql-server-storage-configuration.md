---
title: "SQL Server Vm 的 aaaStorage 組態 |Microsoft 文件"
description: "本主題說明 Azure 如何在佈建期間針對 SQL Server VM 設定儲存體 (Resource Manager 部署模型)。 它也會說明如何針對現有的 SQL Server VM 設定儲存體。"
services: virtual-machines-windows
documentationcenter: na
author: ninarn
manager: jhubbard
tags: azure-resource-manager
ms.assetid: 169fc765-3269-48fa-83f1-9fe3e4e40947
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: ninarn
ms.openlocfilehash: b50dbd698828780cfc044fa0966e8f4e2f3bb6c6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="storage-configuration-for-sql-server-vms"></a>SQL Server VM 的儲存體組態
當您在 Azure 中設定 SQL Server 虛擬機器映像時，hello 入口網站可協助 tooautomate 存放裝置設定。 這包括附加儲存體 toohello VM，讓該存放裝置可存取 tooSQL 伺服器，並將它設定為 toooptimize 適合您特定的效能需求。

本主題說明 Azure 如何在佈建期間針對 SQL Server VM 及針對現有的 VM 設定儲存體。 此設定根據 hello[效能最佳做法](virtual-machines-windows-sql-performance.md)執行 SQL Server 的 Azure vm。

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-rm-include.md)]

## <a name="prerequisites"></a>必要條件
toouse hello 自動儲存組態設定，您的虛擬機器需要 hello 下列特性：

* 使用 [SQL Server 資源庫映像](virtual-machines-windows-sql-server-iaas-overview.md#option-1-create-a-sql-vm-with-per-minute-licensing)佈建。
* 使用 hello [Resource Manager 部署模型](../../../azure-resource-manager/resource-manager-deployment-model.md)。
* 使用 [進階儲存體](../../../storage/common/storage-premium-storage.md)。

## <a name="new-vms"></a>新的 VM
hello 下列各節說明如何為新的 SQL Server 虛擬機器的 tooconfigure 儲存體。

### <a name="azure-portal"></a>Azure 入口網站
當佈建 Azure VM 使用 SQL Server 資源庫映像，您可以選擇 tooautomatically 設定 hello 儲存新的 vm。 指定 hello 儲存體大小、 效能限制，以及工作負載類型。 hello 下列螢幕擷取畫面顯示 hello 儲存體組態刀鋒視窗中的 SQL VM 期間使用佈建。

![佈建期間的 SQL Server VM 儲存體設定](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-provisioning.png)

根據您的選擇，Azure 會執行下列存放裝置設定工作之後建立 hello VM hello:

* 建立並附加 premium 儲存體的資料磁碟 toohello 虛擬機器。
* 設定 hello 資料磁碟 toobe 存取 tooSQL 伺服器。
* 設定 hello 資料磁碟到儲存體集區根據 hello 指定大小和效能 （IOPS 及輸送量） 的需求。
* 將 hello 存放集區與 hello 虛擬機器上的新磁碟機產生關聯。
* 根據您指定的工作負載類型 (資料倉儲、交易式處理或一般)，最佳化這個新的磁碟機。

如需有關 Azure 會儲存設定的設定，請參閱 hello[儲存體組態區段](#storage-configuration)。 如需完整的逐步解說如何 toocreate hello Azure 入口網站中的 SQL Server VM 看到的[佈建教學課程中的 hello](virtual-machines-windows-portal-sql-server-provision.md)。

### <a name="resource-manage-templates"></a>Resource Manager 範本
如果您使用下列資源管理員範本 hello，兩個高階資料磁碟附加根據預設，不需要儲存體集區組態。 不過，您可以自訂這些範本 toochange hello 的高階資料磁碟數目的附加的 toohello 虛擬機器。

* [使用自動備份建立 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autobackup)
* [使用自動修補建立 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-autopatching)
* [使用自 AKV 整合建立 VM](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vm-sql-full-keyvault)

## <a name="existing-vms"></a>現有的 VM
對於現有 SQL Server Vm，您可以修改某些 hello Azure 入口網站中的儲存體設定。 選取您的 VM，請 toohello 設定] 區域中，然後選取 [SQL Server 組態。 hello SQL Server 組態刀鋒視窗會顯示您的 VM hello 目前儲存體使用量。 下圖顯示您的 VM 上存在的所有磁碟機。 每個磁碟機，hello 儲存空間會顯示四個區段：

* SQL 資料
* SQL 記錄檔
* 其他 (非 SQL 儲存體)
* 可用

![設定現有 SQL Server VM 的儲存體](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-existing.png)

tooconfigure hello 儲存體 tooadd 新磁碟機或擴充現有的磁碟機，按一下 hello hello 圖表之上的編輯連結。

您會看到您是否使用之前的這項功能而異的 hello 組態選項。 當使用 hello 第一次，您可以指定新的磁碟機的儲存需求。 如果您先前使用此功能 toocreate 磁碟機，您可以選擇 tooextend 該磁碟機的儲存體。

### <a name="use-for-hello-first-time"></a>Hello 第一次使用
如果是您第一次使用這項功能，您可以指定 hello 新磁碟機的儲存體大小和效能限制。 此體驗會是您在佈建時間將會看到類似 toowhat。 hello 主要差異是不允許 toospecify hello 工作負載類型。 這項限制可避免中斷 hello 虛擬機器上任何現有的 SQL Server 組態。

![設定 SQL Server 儲存體滑桿](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-usage-sliders.png)

Azure 會根據您的規格建立新的磁碟機。 在此案例中，Azure 會執行下列存放裝置設定工作的 hello:

* 建立並附加 premium 儲存體的資料磁碟 toohello 虛擬機器。
* 設定 hello 資料磁碟 toobe 存取 tooSQL 伺服器。
* 設定 hello 資料磁碟到儲存體集區根據 hello 指定大小和效能 （IOPS 及輸送量） 的需求。
* 將 hello 存放集區與 hello 虛擬機器上的新磁碟機產生關聯。

如需有關 Azure 會儲存設定的設定，請參閱 hello[儲存體組態區段](#storage-configuration)。

### <a name="add-a-new-drive"></a>加入新的磁碟機
如果您已在 SQL Server VM 上設定儲存體，展開儲存體會顯示兩個新選項。 hello 第一個選項是 tooadd 新的磁碟機，可以提高您的 VM hello 效能層級。

![加入新的磁碟機 tooa SQL VM](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-configuration-add-new-drive.png)

不過，加入之後 hello 磁碟機，您必須執行一些額外的手動組態 tooachieve hello 提升效能。

### <a name="extend-hello-drive"></a>擴充 hello 磁碟機
hello 擴充儲存體的其他選項為 tooextend hello 現有的磁碟機。 此選項會增加您的磁碟機的 hello 可用的存放裝置，但不會提高效能。 使用儲存集區，您無法在 hello 存放集區建立之後改變 hello 的資料行的數目。 資料行的 hello 數目決定局部寫入，可以顆 hello 資料磁碟的 hello 數目。 因此，任何加入的資料磁碟均無法提升效能。 它們只可以提供更多存放裝置 hello 正在寫入的資料。 這項限制也表示，在擴充 hello 磁碟機，資料行的 hello 數目會決定 hello，您可以加入資料磁碟數目下限。 因此如果您有四個資料磁碟建立存放集區，資料行的 hello 數目也是四個。 每當您擴充 hello 存放裝置，您必須新增至少四個資料磁碟。

![延伸 SQL VM 的磁碟機](./media/virtual-machines-windows-sql-storage-configuration/sql-vm-storage-extend-a-drive.png)

## <a name="storage-configuration"></a>儲存體組態
本節提供的參考 hello SQL VM 佈建或 hello Azure 入口網站中的組態期間自動執行 Azure 儲存體組態變更。

* 如果您為 VM 選取了小於兩個 TB 的儲存體，則 Azure 不會建立存放集區。
* 如果您為 VM 選取了至少兩個 TB 的儲存體，則 Azure 會設定存放集區。 本主題的 hello 下一節提供 hello 存放集區設定的 hello 詳細的資料。
* 自動儲存體設定一律使用 [儲存體](../../../storage/common/storage-premium-storage.md) P30 資料磁碟。 因此，沒有 1:1 之間的對應您選取的數字的 Tb，而且資料磁碟數目 hello 附加 tooyour VM。

如需定價資訊，請參閱 hello[儲存體定價](https://azure.microsoft.com/pricing/details/storage)頁面 hello**磁碟儲存體** 索引標籤。

### <a name="creation-of-hello-storage-pool"></a>建立 hello 存放集區
Azure 會使用下列設定 toocreate hello 存放集區上的 SQL Server Vm 的 hello。

| 設定 | 值 |
| --- | --- |
| 等量大小 |256 KB (資料倉儲)；64 KB (交易式) |
| 磁碟大小 |每個磁碟 1 TB |
| 快取 |讀取 |
| 配置大小 |64 KB NTFS 配置單位大小 |
| 立即檔案初始化 |已啟用 |
| 在記憶體中鎖定頁面 |已啟用 |
| 復原 |簡單復原 (無恢復功能) |
| 資料行數目 |資料磁碟數量<sup>1</sup> |
| TempDB 位置 |儲存在資料磁碟上<sup>2</sup> |

<sup>1</sup> hello 存放集區建立之後，您無法改變 hello hello 存放集區中的資料行數目。

<sup>2</sup>此設定僅適用於您建立使用 hello 儲存體組態功能 toohello 第一個磁碟機。

## <a name="workload-optimization-settings"></a>工作負載最佳化設定
hello 下表描述 hello 三個工作負載類型可用的選項以及其對應的最佳化：

| 工作負載類型 | 說明 | 最佳化 |
| --- | --- | --- |
| **一般** |支援大多數工作負載的預設設定 |None |
| **交易式處理** |Hello 儲存體的傳統資料庫 OLTP 工作負載最佳化 |追蹤旗標 1117<br/>追蹤旗標 1118 |
| **資料倉儲** |Hello 儲存體分析和報告工作負載最佳化 |追蹤旗標 610<br/>追蹤旗標 1117 |

> [!NOTE]
> 您可以在 hello 儲存體組態步驟中選取佈建 SQL 虛擬機器時，您可以只指定 hello 工作負載類型。
>
>

## <a name="next-steps"></a>後續步驟
如 toorunning Azure Vm 中的 SQL Server 相關的其他主題，請參閱 < [Azure 虛擬機器上的 SQL Server](virtual-machines-windows-sql-server-iaas-overview.md)。
