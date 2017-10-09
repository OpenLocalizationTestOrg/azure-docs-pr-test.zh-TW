---
title: "伺服器在 VM 上的 SQL Server 資料庫 tooSQL aaaMigrate |Microsoft 文件"
description: "深入了解如何 toomigrate 在內部部署使用者資料庫 tooSQL 伺服器在 Azure 虛擬機器。"
services: virtual-machines-windows
documentationcenter: 
author: sabotta
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 00fd08c6-98fa-4d62-a3b8-ca20aa5246b1
ms.service: virtual-machines-sql
ms.workload: iaas-sql-server
ms.tgt_pltfrm: vm-windows-sql-server
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: carlasab
ms.openlocfilehash: 9c7aba30304ea40796412d2ddc885f6d4a58be2a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-a-sql-server-database-toosql-server-in-an-azure-vm"></a>移轉 SQL Server 資料庫 tooSQL Azure VM 中的伺服器

有許多方法 toomigrate 在內部部署 SQL Server 使用者資料庫 tooSQL Azure VM 中的伺服器。 這篇文章會簡要討論各種方法，並建議 hello 用於各種案例的最佳方法。

[!INCLUDE [learn-about-deployment-models](../../../../includes/learn-about-deployment-models-both-include.md)]

## <a name="what-are-hello-primary-migration-methods"></a>Hello 主要移轉方法有哪些？
hello 移轉主要方法如下：

* 執行內部部署備份使用壓縮，並手動複製 hello 備份檔案到 hello Azure 虛擬機器
* 執行備份 tooURL 和還原成 hello hello URL 從 Azure 虛擬機器
* 卸離然後複製 hello 資料和記錄檔 tooAzure blob 儲存體，並從 URL 將 tooSQL Azure VM 中的伺服器
* 轉換在內部部署實體機器 tooHyper V VHD、 上傳 tooAzure Blob 儲存體，並再部署新的 VM 使用上傳 VHD
* 使用 Windows 匯入/匯出服務寄送硬碟機
* 如果您有 AlwaysOn 部署內部部署，請使用 hello[加入 Azure 複本精靈](../classic/sql-onprem-availability.md)toocreate Azure，然後容錯移轉，指向使用者 toohello Azure 的資料庫執行個體的複本
* 使用 SQL Server[異動複寫](https://msdn.microsoft.com/library/ms151176.aspx)tooconfigure hello Azure SQL Server 執行個體標示為 「 訂閱者 」，然後再停用複寫，指向使用者 toohello Azure 的資料庫執行個體

> [!TIP]
> 您也可以使用 Azure 中的 SQL Server Vm 之間的這些相同的技巧 toomove 資料庫。 例如，沒有任何支援的方法 tooupgrade 從一個版本/版 tooanother 的 SQL Server 資源庫映像 VM。 在此情況下，您應該使用 hello 新版本/版時，建立新的 SQL Server VM，然後使用 hello 移轉技術在此發行項 toomove 您的資料庫。 

## <a name="choosing-your-migration-method"></a>選擇您的移轉方法
最佳的資料傳輸效能，如 hello 將資料庫檔案移轉到 hello Azure VM 使用壓縮的備份檔案。

toominimize hello 資料庫移轉程序期間的停機時間使用 hello AlwaysOn 選項或 hello 異動複寫選項。

如果不可能 toouse hello 上述方法，以手動方式移轉您的資料庫。 使用此方法，您將通常開頭後面接著一份 hello 資料庫備份至 Azure 的資料庫備份，並執行資料庫還原。 您可以也將本身 hello 資料庫檔案複製到 Azure，然後將其連接。 若要將資料庫移轉到 Azure VM，有數種方法可以完成此手動程序。

> [!NOTE]
> 當您從舊版 SQL Server 升級 tooSQL Server 2014 或 SQL Server 2016 時，您應該考慮是否需要變更。 我們建議您解決所有功能的相依性不支援 hello 新版本的 SQL Server 移轉專案的一部分。 如需支援的 hello 版本和案例的詳細資訊，請參閱[升級 tooSQL 伺服器](https://msdn.microsoft.com/library/bb677622.aspx)。

hello 下表列出每個 hello 主要移轉方法，並討論 hello 使用每一種方法最適合。

| 方法 | 來源資料庫版本 | 目的地資料庫版本 | 來源資料庫備份的大小條件約束 | 注意事項 |
| --- | --- | --- | --- | --- |
| [執行內部部署備份使用壓縮，並手動複製 hello 備份檔案到 hello Azure 虛擬機器](#backup-and-restore) |SQL Server 2005 或更新版本 |SQL Server 2005 或更新版本 |[Azure VM 儲存體限制](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) | 對於在電腦之間移動資料庫，這是非常簡單且通過完善測試的技術。 |
| [執行備份 tooURL 和還原成 hello hello URL 從 Azure 虛擬機器](#backup-to-url-and-restore) |SQL Server 2012 SP1 CU2 或更新版本 |SQL Server 2012 SP1 CU2 或更新版本 |< 12.8 TB 適用於 SQL Server 2016，否則為 < 1 TB | 這個方法是只是另一個方式 toomove hello 備份檔案 toohello VM 使用 Azure 儲存體。 |
| [卸離然後複製 hello 資料和記錄檔 tooAzure blob 儲存體，並從 URL 將 Azure 虛擬機器中的 tooSQL 伺服器](#detach-and-attach-from-url) |SQL Server 2005 或更新版本 |SQL Server 2014 或更新版本 |[Azure VM 儲存體限制](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |使用這個方法，當您計劃太[儲存這些檔案的使用 hello Azure Blob 儲存體服務](https://msdn.microsoft.com/library/dn385720.aspx)並且將它們附加 tooSQL 伺服器執行於 Azure VM，特別是使用非常龐大的資料庫 |
| [轉換在內部部署機器 tooHyper V Vhd 上傳 tooAzure Blob 儲存體，，然後部署新的虛擬機器使用上傳的 VHD](#convert-to-vm-and-upload-to-url-and-deploy-as-new-vm) |SQL Server 2005 或更新版本 |SQL Server 2005 或更新版本 |[Azure VM 儲存體限制](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |使用時機[攜帶您自己的 SQL Server 授權](../../../sql-database/sql-database-paas-vs-sql-server-iaas.md)，當您將較舊版本的 SQL Server 執行的資料庫移轉時，或移轉的系統和使用者資料庫的一部分的方式一起 hello 相依於其他資料庫的移轉使用者資料庫和/或系統資料庫。 |
| [使用 Windows 匯入/匯出服務寄送硬碟機](#ship-hard-drive) |SQL Server 2005 或更新版本 |SQL Server 2005 或更新版本 |[Azure VM 儲存體限制](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |使用 hello [Windows 匯入/匯出服務](../../../storage/common/storage-import-export-service.md)時速度太慢，例如非常大型的資料庫手動複製方法 |
| [使用 hello 加入 Azure 複本精靈](../classic/sql-onprem-availability.md) |SQL Server 2012 或更新版本 |SQL Server 2012 或更新版本 |[Azure VM 儲存體限制](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |可將停機時間縮到最短，請在您有內部部署的 AlwaysOn 部署時使用 |
| [使用 SQL Server 異動複寫](https://msdn.microsoft.com/library/ms151176.aspx) |SQL Server 2005 或更新版本 |SQL Server 2005 或更新版本 |[Azure VM 儲存體限制](https://azure.microsoft.com/documentation/articles/azure-subscription-service-limits/) |當您需要 toominimize 停機時間，而且沒有 AlwaysOn 之內部部署的使用 |

## <a name="backup-and-restore"></a>備份與還原
備份壓縮資料庫，複製 hello 備份 toohello VM，並再還原 hello 資料庫。 如果您的備份檔案是大於 1 TB，您必須等量分割它因為 hello VM 磁碟的大小上限為 1 TB。 使用下列一般步驟 toomigrate 使用者資料庫，使用此手動方法的 hello:

1. 執行完整資料庫備份 tooan 在內部部署位置。
2. 建立或上傳具有 hello 版本的 SQL Server 所需的虛擬機器。
3. 根據您的需求設定連線。 請參閱[連接 tooa Azure （資源管理員） 上的 SQL Server 虛擬機器](virtual-machines-windows-sql-connect.md)。
4. 複製您的備份檔案 tooyour VM 使用遠端桌面、 Windows 檔案總管或 hello 複製命令的命令提示字元。

## <a name="backup-toourl-and-restore"></a>TooURL 備份與還原
而不是備份 tooa 本機檔案，您可以使用 hello[備份 tooURL](https://msdn.microsoft.com/library/dn435916.aspx)然後從 URL toohello VM 還原。 SQL Server 2016，等量備份組、 的效能，建議使用和支援所需的每個 blob tooexceed hello 大小限制。 對於大型資料庫，hello 使用 hello [Windows 匯入/匯出服務](../../../storage/common/storage-import-export-service.md)建議。

## <a name="detach-and-attach-from-url"></a>從 URL 中斷連結和從 URL 連結
卸離您的資料庫和記錄檔，並將它們傳送到太[Azure Blob 儲存體](https://msdn.microsoft.com/library/dn385720.aspx)。 從 Azure VM 上的 hello URL，然後附加 hello 資料庫。 如果您想要在 Blob 儲存體中的 hello 實體資料庫檔案 tooreside，請使用此選項。 這對於非常大型的資料庫很實用。 使用下列一般步驟 toomigrate 使用者資料庫，使用此手動方法的 hello:

1. 卸離 hello hello 在內部部署資料庫執行個體中的資料庫檔案。
2. Hello 卸離資料庫檔案複製到 Azure blob 儲存體使用 hello [AZCopy 命令列公用程式](../../../storage/common/storage-use-azcopy.md)。
3. 附加從 hello Azure URL toohello SQL Server 執行個體 hello Azure VM 中的 hello 資料庫檔案。

## <a name="convert-toovm-and-upload-toourl-and-deploy-as-new-vm"></a>轉換 tooVM 並上傳 tooURL 以及部署為新的 VM
在內部部署 SQL Server 執行個體 tooAzure 虛擬機器中使用此方法 toomigrate 所有系統和使用者資料庫。 使用下列一般步驟 toomigrate 整個 SQL Server 執行個體使用此手動方法的 hello:

1. 轉換實體或虛擬機器使用 tooHyper V Vhd [Microsoft 虛擬機器轉換器](https://technet.microsoft.com/library/dn874008(v=ws.11).aspx)。
2. 上傳 VHD 檔案 tooAzure 儲存體使用 hello [Add-azurevhd cmdlet](https://msdn.microsoft.com/library/windowsazure/dn495173.aspx)。
3. 部署新虛擬機器使用 hello 上傳 VHD。

> [!NOTE]
> toomigrate 整個應用程式，請考慮使用[Azure Site Recovery](../../../site-recovery/site-recovery-overview.md)]。

## <a name="ship-hard-drive"></a>寄送硬碟機
使用 hello [Windows 匯入/匯出服務方法](../../../storage/common/storage-import-export-service.md)tootransfer 大量檔案資料 tooAzure Blob 儲存體中的情況下透過 hello 網路上傳極為耗費資源或不可行。 與此服務，您將一或多個硬碟機，包含該資料 tooan Azure 資料中心，將您的資料上傳 tooyour 儲存體帳戶。

## <a name="next-steps"></a>後續步驟
如需在 Azure 虛擬機器上執行 SQL Server 的詳細資訊，請參閱 [Azure 虛擬機器上的 SQL Server 概觀](virtual-machines-windows-sql-server-iaas-overview.md)。

如需從擷取的映像建立 Azure SQL Server 虛擬機器的指示，請參閱[秘訣和訣竅上複製 Azure SQL 虛擬機器擷取映像從](https://blogs.msdn.microsoft.com/psssql/2016/07/06/tips-tricks-on-cloning-azure-sql-virtual-machines-from-captured-images/)hello CSS SQL Server 工程師部落格上。

