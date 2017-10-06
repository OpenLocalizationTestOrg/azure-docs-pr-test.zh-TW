---
title: "aaaAzure Analysis Services 資料庫備份和還原 |Microsoft 文件"
description: "描述如何 toobackup 和還原 Azure Analysis Services 資料庫。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
ms.assetid: 
ms.service: analysis-services
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: cf0a782d237a95fdfa5ef628f998bd053aac0d9f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="backup-and-restore"></a>備份與還原

備份 Azure Analysis Services 中的表格式模型資料庫是大部分相同 hello 與內部部署 Analysis Services。 hello 的主要差異是您用來儲存備份檔案。 備份檔案必須儲存在 tooa 容器[Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)。 您可以使用您已經有的儲存體帳戶和容器，或是在為您的伺服器設定儲存體設定時再建立帳戶和容器。

> [!NOTE]
> 建立儲存體帳戶會導致產生新的可計費服務。 詳細資訊，請參閱 toolearn [Azure 儲存體定價](https://azure.microsoft.com/pricing/details/storage/blobs/)。
> 
> 

備份會以 .abf 副檔名儲存。 針對記憶體內表格式模型，會同時儲存模型資料和中繼資料。 針對 DirectQuery 表格式模型，則只會儲存模型中繼資料。 備份可以壓縮和加密，依據您選擇的 hello 選項。 



## <a name="configure-storage-settings"></a>設定儲存體設定
之前備份，您會需要 tooconfigure 存放裝置設定為您的伺服器。


### <a name="tooconfigure-storage-settings"></a>tooconfigure 存放裝置設定
1.  在 Azure 入口網站 > [設定] 中，按一下 [備份]。

    ![[設定] 中的 [備份]](./media/analysis-services-backup/aas-backup-backups.png)

2.  按一下 [已啟用]，然後按一下 [儲存體設定]。

    ![啟用](./media/analysis-services-backup/aas-backup-enable.png)

3. 選取您的儲存體帳戶，或建立新帳戶。

4. 選取容器，或建立新容器。

    ![選取容器](./media/analysis-services-backup/aas-backup-container.png)

5. 儲存您的備份設定。

    ![儲存備份設定](./media/analysis-services-backup/aas-backup-save.png)

## <a name="backup"></a>備份

### <a name="toobackup-by-using-ssms"></a>使用 SSMS toobackup

1. 在 SSMS 中，於資料庫上按一下滑鼠右鍵 > [備份]。

2. 在 [備份資料庫] > [備份檔案] 中，按一下 [瀏覽]。

3. 在 [hello**另存新檔**] 對話方塊中，確認 hello 資料夾路徑，，，然後輸入 hello 備份檔案的名稱。 

4. 在 hello **Backup Database**對話方塊中，選取選項。

    **允許檔案覆寫**-選取 hello 這個選項 toooverwrite 備份檔案相同的名稱。 如果未選取此選項，您所儲存的 hello 檔案不能有名稱相同的 hello 做為檔案已存在於 hello 相同的位置。

    **套用壓縮**-選取這個選項 toocompress hello 備份檔案。 壓縮過的備份檔案可節省磁碟空間，但需要使用稍微多一點的 CPU 資源。 

    **加密備份檔案**-選取這個選項 tooencrypt hello 備份檔案。 此選項需要使用者提供的密碼 toosecure hello 備份檔案。 hello 密碼可防止讀取 hello 備份資料的還原作業以外的任何其他方式。 如果您選擇 tooencrypt 備份，請將 hello 密碼儲存在安全的位置。

5. 按一下**確定**toocreate 儲存 hello 備份檔案。


### <a name="powershell"></a>PowerShell
使用 [Backup-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/backup-asdatabase-cmdlet) Cmdlet。

## <a name="restore"></a>還原
還原時，您的備份檔案必須是您已設定為您的伺服器 hello 儲存體帳戶中。 如果您需要 toomove 備份檔案從內部部署位置 tooyour 儲存體帳戶，請使用[Microsoft Azure 儲存體總管](https://docs.microsoft.com/azure/vs-azure-tools-storage-manage-with-storage-explorer)或 hello [AzCopy](../storage/common/storage-use-azcopy.md)命令列公用程式。 



> [!NOTE]
> 如果您正在從內部部署伺服器中還原，您必須從 hello 模型的角色中移除所有的 hello 網域使用者，並將其加入回 toohello 角色做為 Azure Active Directory 的使用者。
> 
> 

### <a name="toorestore-by-using-ssms"></a>使用 SSMS toorestore

1. 在 SSMS 中，於資料庫上按一下滑鼠右鍵 > [還原]。

2. 在 hello **Backup Database**對話方塊，請在**備份檔案**，按一下 **瀏覽**。

3. 在 hello**尋找資料庫檔案**對話方塊中，您想要 toorestore 選取 hello 檔案。

4. 在**還原資料庫**，選取 hello 資料庫。

5. 指定選項。 安全性選項必須符合 hello 備份時所使用的備份選項。


### <a name="powershell"></a>PowerShell

使用 [Restore-ASDatabase](https://docs.microsoft.com/sql/analysis-services/powershell/restore-asdatabase-cmdlet) Cmdlet。


## <a name="related-information"></a>相關資訊

[Azure 儲存體帳戶](../storage/common/storage-create-storage-account.md)  
[高可用性](analysis-services-bcdr.md)     
[管理 Azure Analysis Services](analysis-services-manage.md)
