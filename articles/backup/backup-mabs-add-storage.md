---
title: "Azure 備份伺服器 v2 aaaUse 現代的備份儲存體 |Microsoft 文件"
description: "深入了解 Azure 備份伺服器 v2 中的 hello 新功能。 本文說明如何 tooupgrade 備份伺服器安裝。"
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/15/2017
ms.author: masaran;markgal
ms.openlocfilehash: b2a1ed27a6a682bd611fea1d2df9ef93314404e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-storage-tooazure-backup-server-v2"></a>新增儲存體 tooAzure 備份伺服器 v2

Azure 備份伺服器 v2 隨附 System Center 2016 Data Protection Manager 新式備份儲存體。 新式備份儲存體可節省 50% 的儲存空間、備份速度快三倍，且更具儲存效率。 它也提供可感知工作負載的儲存體。 

> [!NOTE]
> toouse 現代的備份儲存體，您必須在 Windows Server 2016 上執行備份伺服器 v2。 如果您在舊版 Windows Server 上執行備份伺服器 v2，Azure 備份伺服器將無法利用新式備份儲存體。 相反地，它保護工作負載的方式會和備份伺服器 v1 一樣。 如需詳細資訊，請參閱 hello 備份伺服器版本[保護矩陣](backup-mabs-protection-matrix.md)。

## <a name="volumes-in-backup-server-v2"></a>備份伺服器 v2 中的磁碟區

備份伺服器 v2 接受儲存體磁碟區。 當您將磁碟區時，備份伺服器將會格式化 hello 磁碟區 tooResilient 檔案系統 (ReFS)、 現代的備份儲存體需要。 tooadd 磁碟區，和 tooexpand 於稍後如果您需要我們建議您使用此工作流程：

1.  在 VM 上設定備份伺服器 v2。
2.  在儲存集區的虛擬磁碟上建立磁碟區：
    1.  新增磁碟 tooa 存放集區並將虛擬磁碟以建立簡單的版面配置。
    2.  新增任何額外的磁碟，並擴充 hello 虛擬磁碟。
    3.  Hello 虛擬磁碟上建立磁碟區。
3.  新增 hello 磁碟區 tooBackup 伺服器。
4.  設定可感知工作負載的儲存體。

## <a name="create-a-volume-for-modern-backup-storage"></a>為新式備份儲存體建立磁碟區

以磁碟區作為磁碟儲存體來使用備份伺服器 v2 可協助您掌控儲存體。 磁碟區可以是單一磁碟。 不過，如果您想在 hello tooextend 儲存體未來，建立使用儲存空間建立磁碟的磁碟區。 這可協助您是否 tooexpand hello 磁碟區備份存放區。 本節會提供最佳做法，讓您了解如何建立具有此設定的磁碟區。

1. 在 [伺服器管理員] 中，選取 [檔案和存放服務] > [磁碟區] > [儲存集區]。 在 [實體磁碟] 底下，選取 [新增儲存集區]。 

    ![建立新的儲存集區](./media/backup-mabs-add-storage/mabs-add-storage-1.png)

2. 在 hello**工作**下拉式清單方塊中，選取**新虛擬磁碟**。

    ![新增虛擬磁碟](./media/backup-mabs-add-storage/mabs-add-storage-2.png)

3. 選取 hello 儲存集區，然後再選取**新增實體磁碟**。

    ![新增實體磁碟](./media/backup-mabs-add-storage/mabs-add-storage-3.png)

4. 選取 hello 實體磁碟，然後選取**擴充虛擬磁碟**。

    ![擴充 hello 虛擬磁碟](./media/backup-mabs-add-storage/mabs-add-storage-4.png)

5. 選取 hello 虛擬磁碟，然後選取**新的磁碟區**。

    ![建立新的磁碟區](./media/backup-mabs-add-storage/mabs-add-storage-5.png)

6. 在 hello**選取 hello 伺服器和磁碟**對話方塊中，選取 hello 伺服器和 hello 新磁碟。 然後，選取 [下一步]。

    ![選取 hello 伺服器和磁碟](./media/backup-mabs-add-storage/mabs-add-storage-6.png)

## <a name="add-volumes-toobackup-server-disk-storage"></a>新增磁碟區 tooBackup 伺服器磁碟儲存體

tooadd hello 中的磁碟區 tooBackup 伺服器**管理** 窗格中，掃描 hello 存放裝置，然後選取**新增**。 所有 hello 磁碟區可用 toobe 加入備份伺服器存放裝置的清單隨即出現。 可用的磁碟區加入選取的磁碟區 toohello 清單之後，您可以讓您管理這些易記名稱 toohelp。 這些磁碟區 tooReFS，因此備份伺服器可以使用現代的備份儲存體的 hello 優點選取的 tooformat**確定**。

![新增可用的磁碟區](./media/backup-mabs-add-storage/mabs-add-storage-7.png)

## <a name="set-up-workload-aware-storage"></a>設定可感知工作負載的儲存體

使用可感知工作負載的儲存體，您可以選取 hello 儲存磁碟區的優先特定種類的工作負載。 例如，您可以設定昂貴支援大量輸入/輸出作業每個第二個 (IOPS) toostore hello 工作負載，需要大量的頻繁備份的磁碟區。 舉例來說，具有交易記錄的 SQL Server。 備份頻率，像是 Vm，其他工作負載可以備份 toolow 成本磁碟區。

### <a name="update-dpmdiskstorage"></a>Update-DPMDiskStorage

您可以設定工作負載感知儲存區，使用 hello PowerShell 指令程式更新-DPMDiskStorage，就會更新 hello hello Data Protection Manager 伺服器上的存放集區中的磁碟區的屬性。

語法：

`Parameter Set: Volume`

```
Update-DPMDiskStorage [-Volume] <Volume> [[-FriendlyName] <String> ] [[-DatasourceType] <VolumeTag[]> ] [-Confirm] [-WhatIf] [ <CommonParameters>]
```
hello 下列螢幕擷取畫面顯示 hello 更新 DPMDiskStorage cmdlet hello PowerShell 視窗中。

![hello hello PowerShell 視窗中的更新 DPMDiskStorage 命令](./media/backup-mabs-add-storage/mabs-add-storage-8.png)

使用 PowerShell 的 hello 變更會反映在 hello 備份伺服器系統管理員主控台。

![磁碟與 hello 系統管理員主控台中的磁碟區](./media/backup-mabs-add-storage/mabs-add-storage-9.png)

## <a name="next-steps"></a>後續步驟
安裝備份伺服器之後，了解如何 tooprepare 您的伺服器，或開始進行保護工作負載。

- [準備備份伺服器工作負載](backup-azure-microsoft-azure-backup.md)
- [使用 VMware 伺服器的備份伺服器 tooback](backup-azure-backup-server-vmware.md)
- [使用 SQL server 備份伺服器 tooback](backup-azure-sql-mabs.md)

