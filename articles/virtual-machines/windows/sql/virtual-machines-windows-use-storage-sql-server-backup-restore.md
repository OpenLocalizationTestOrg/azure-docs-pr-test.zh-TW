---
title: "aaaHow toouse SQL Server 備份和還原的 Azure 儲存體 |Microsoft 文件"
description: "深入了解如何註冊 SQL Server tooAzure 儲存體 tooback。 說明備份 SQL 資料庫 tooAzure 儲存體的 hello 優點。"
services: virtual-machines-windows
documentationcenter: 
author: MikeRayMSFT
manager: jhubbard
tags: azure-service-management
ms.assetid: 0db7667d-ef63-4e2b-bd4d-574802090f8b
ms.service: virtual-machines-sql
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows-sql-server
ms.workload: iaas-sql-server
ms.date: 01/31/2017
ms.author: mikeray
ms.openlocfilehash: 67ebe8377be97df1312f8c1345e23576aabe0c4c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-storage-for-sql-server-backup-and-restore"></a>使用 Azure 儲存體進行 SQL Server 備份與還原
## <a name="overview"></a>概觀
從 SQL Server 2012 SP1 CU2 開始，您可以現在 SQL Server 備份直接寫入 toohello Azure Blob 儲存體服務。 您可以使用此功能 tooback，向上 tooand 還原自 hello Azure Blob 服務與內部部署 SQL Server 資料庫或 Azure 的虛擬機器中 SQL Server 資料庫。 備份 toocloud 優點的可用性、 無限制進行地理複寫異地儲存體和簡化移轉的資料 tooand 從 hello 雲端。 您可以使用 Transact-SQL 或 SMO 發出 BACKUP 或 RESTORE 陳述式。

SQL Server 2016 引進新功能。您可以使用[檔案快照集備份](http://msdn.microsoft.com/library/mt169363.aspx)tooperform 幾乎即時的備份和非常快速的還原。

本主題說明為什麼您可能會選擇 toouse SQL 備份的 Azure 儲存體，並接著說明所涉及的 hello 元件。 您可以使用提供的 hello 文章 tooaccess 逐步解說和使用此服務和 SQL Server 備份的其他資訊 toostart hello 結尾的 hello 資源。

## <a name="benefits-of-using-hello-azure-blob-service-for-sql-server-backups"></a>使用 hello Azure Blob 服務進行 SQL Server 備份的優點
備份 SQL Server 時，您會面臨數個挑戰。 這些挑戰包含儲存體管理，存放裝置故障的風險，存取 toooff 網站儲存體和硬體組態。 許多這些挑戰會使用 SQL Server 備份 hello Azure Blob 儲存服務來定址。 請考慮 hello 下列優點：

* **使用方便**： 將您的備份儲存在 Azure blob 可以是方便、 彈性且容易 tooaccess 的異地選項。 建立異地儲存體，您的 SQL Server 備份可以簡單，只要修改現有的指令碼/作業 toouse hello**備份 tooURL**語法。 異地儲存體通常應該遠離 hello 實際執行資料庫位置 tooprevent hello 異地和實際執行資料庫位置，可能會影響單一災害。 藉由選擇太[地理複寫您的 Azure blob](../../../storage/common/storage-redundancy.md)，您可能影響整個地區的 hello 災害 hello 事件中有一層額外的保護。
* **備份封存**: hello Azure Blob 儲存體服務提供更好的替代 toohello 常用磁帶選項 tooarchive 備份。 磁帶儲存體可能需要實際運輸採取 tooan 異地設施和量值 tooprotect hello 媒體。 將備份存放在 Azure Blob 儲存體提供了立即、高度可用且持久的封存選項。
* **受管理的硬體**：使用 Azure 服務時，沒有硬體管理的額外負荷。 Azure 服務管理 hello 硬體，並提供備援，防止硬體故障的地理複寫。
* **無限制的儲存體**： 只要啟用直接備份 tooAzure blob，您有存取 toovirtually 無限制的儲存體。 或者，tooan Azure 虛擬機器磁碟備份已根據機器大小的限制。 沒有限制 toohello 數目的磁碟中，您可以附加 tooan Azure 虛擬機器進行備份。 超大型執行個體的限制為 16 個磁碟，較小的執行個體則更少。
* **備份可用性**： 在 Azure blob 儲存的備份可提供從任何地方，並在任何時間，而且可以輕鬆地存取進行還原 tooeither 在內部部署 SQL Server 或另一個 SQL Server 在 Azure 虛擬機器中，執行而需要 hello資料庫附加/卸離或下載並附加 hello VHD。
* **成本**： 只支付 hello 服務，可使用。 可以作為具成本效益的異地及備份封存選項。 請參閱 hello [Azure 定價計算機](http://go.microsoft.com/fwlink/?LinkId=277060 "定價計算機")，和 hello [Azure 定價的發行項](http://go.microsoft.com/fwlink/?LinkId=277059 "定價文章")如需詳細資訊資訊。
* **儲存快照集**： 當資料庫檔案會儲存在 Azure blob，而且您使用 SQL Server 2016 時，您可以使用[檔案快照集備份](http://msdn.microsoft.com/library/mt169363.aspx)tooperform 幾乎即時的備份和非常快速的還原。

如需詳細資訊，請參閱 [SQL Server 備份及還原與 Azure Blob 儲存體服務](http://go.microsoft.com/fwlink/?LinkId=271617)。

下列兩個區段的 hello 導入 hello Azure Blob 儲存體服務，包括所需的 hello SQL Server 元件。 它是重要 toounderstand hello 元件及其互動 toosuccessfully 使用備份和還原自 hello Azure Blob 儲存體服務。

## <a name="azure-blob-storage-service-components"></a>Azure Blob 儲存體服務元件
hello 下列 Azure 元件會使用備份 toohello Azure Blob 儲存體服務時。

| 元件 | 說明 |
| --- | --- |
| **儲存體帳戶** |所有儲存體服務的起點的 hello hello 儲存體帳戶。 tooaccess Azure Blob 儲存體服務，會先建立 Azure 儲存體帳戶。 如需有關 Azure Blob 儲存體服務的詳細資訊，請參閱[toouse hello Azure Blob 儲存體服務的方式](https://azure.microsoft.com/develop/net/how-to-guides/blob-storage/) |
| **容器** |容器可提供一組 Blob 的分組，並可存放不限數目的 Blob。 toowrite SQL Server 備份 tooan Azure Blob 服務，您至少必須有建立 hello 根容器。 |
| **Blob** |任何類型和大小的檔案。 使用 hello 下列 URL 格式來定址 blob: **https://[storage account].blob.core.windows.net/[container]/[blob]**。 如需有關分頁 Blob 的詳細資訊，請參閱 [了解區塊 Blob 和分頁 Blob](http://msdn.microsoft.com/library/azure/ee691964.aspx) |

## <a name="sql-server-components"></a>SQL Server 元件
hello 下列 SQL Server 元件的用途備份 toohello Azure Blob 儲存體服務時。

| 元件 | 說明 |
| --- | --- |
| **URL** |URL 指定統一資源識別元 (URI) tooa 唯一備份檔案。 hello URL 是使用的 tooprovide hello 位置和 hello SQL Server 備份檔案的名稱。 hello URL 必須指向 tooan 實際的 blob，不只是容器。 如果 hello blob 不存在，則會建立它。 如果現有的 blob 指定，則備份失敗，除非 hello > 指定了 WITH FORMAT 選項。 hello 以下是您可以在 hello BACKUP 命令中指定的 hello URL 的範例： **http[s]://[storageaccount].blob.core.windows.net/[container]/[FILENAME.bak]**。 建議使用 HTTPS，但並非必要。 |
| **認證** |是必要的 tooconnect 並驗證 tooAzure Blob 儲存體服務的 hello 資訊會儲存為認證。  為了讓 SQL Server toowrite 備份 tooan Azure Blob 或從中還原，必須建立 SQL Server 認證。 如需詳細資訊，請參閱 [SQL Server 認證](https://msdn.microsoft.com/library/ms189522.aspx)。 |

> [!NOTE]
> 如果您選擇 toocopy 並上傳備份檔案 toohello Azure Blob 儲存體服務時，您必須使用分頁 blob 類型，為您的儲存體選項如果您計劃 toouse 這個檔案的還原作業即可。 從區塊 Blob 類型進行 RESTORE 會失敗並發生錯誤。
> 
> 

## <a name="next-steps"></a>後續步驟
1. 建立 Azure 訂用帳戶 (如果您還沒有帳戶的話)。 如果您要評估 Azure，請考慮 hello[免費試用版](https://azure.microsoft.com/free/)。
2. 請透過下列教學課程會逐步引導您建立儲存體帳戶和執行還原的 hello 的其中一個。
   
   * **SQL Server 2014**:[教學課程： SQL Server 2014 備份及還原 tooMicrosoft Azure Blob 儲存體服務](https://msdn.microsoft.com/library/jj720558\(v=sql.120\).aspx)。
   * **SQL Server 2016**:[教學課程： 搭配使用 hello Microsoft Azure Blob 儲存體服務和 SQL Server 2016 資料庫](https://msdn.microsoft.com/library/dn466438.aspx)
3. 檢閱其他文件，從 [使用 Microsoft Azure Blob 儲存體服務進行 SQL Server 備份及還原](https://msdn.microsoft.com/library/jj919148.aspx)開始。

如果您有任何問題，請檢閱 hello 主題[SQL Server 備份 tooURL 最佳作法和疑難排解](https://msdn.microsoft.com/library/jj919149.aspx)。

如需其他 SQL Server 備份與還原選項，請參閱 [Azure 虛擬機器中的 SQL Server 備份和還原](virtual-machines-windows-sql-backup-recovery.md)。

