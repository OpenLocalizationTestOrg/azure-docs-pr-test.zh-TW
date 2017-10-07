---
title: "aaaUse Azure Backup tooreplace 磁帶基礎結構 |Microsoft 文件"
description: "了解如何 Azure Backup 會提供可讓您的磁帶類似的語意 toobackup 和還原在 Azure 中的資料"
services: backup
documentationcenter: 
author: trinadhk
manager: vijayts
editor: 
ms.assetid: 2e1bb67d-986c-4437-8056-3a63169b4214
ms.service: backup
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 1/10/2017
ms.author: saurse;trinadhk;markgal
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 4c5b095d95d39267c54b1eed9427bda09658bb94
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="move-your-long-term-storage-from-tape-toohello-azure-cloud"></a>移動您的長期存放裝置從磁帶 toohello Azure 雲端
使用 Azure 備份和 System Center Data Protection Manager 的客戶可以進行下列操作：

* 備份在其最符合組織需求的 hello 排程中的資料。
* 較長時間保留 hello 備份資料
* 讓 Azure (而非磁帶) 成為長期保留需求的一部分。

此文章說明客戶如何啟用備份和保留原則。 使用磁帶 tooaddress 客戶現在有功能強大且可行的替代方式，與 hello 可用性，這項功能需要其長期-長期保留。 hello 功能在 hello 最新版本中的 hello Azure Backup (所提供[這裡](http://aka.ms/azurebackup_agent))。 System Center DPM 客戶必須更新，才能使用 DPM 和 DPM 2012 R2 UR5 至少 hello Azure 備份服務。

## <a name="what-is-hello-backup-schedule"></a>Hello 備份排程是什麼？
hello 備份排程指出 hello hello 備份作業頻率。 例如，hello 遵循螢幕中的 hello 設定會指出備份會執行每日下午 6 點，並在午夜。

![每日排程](./media/backup-azure-backup-cloud-as-tape/dailybackupschedule.png)

客戶也可以排程每週備份。 比方說，hello 設定在 hello 遵循螢幕指示，備份每個替代星期日 & 星期三上午 9:30 和 1:00 AM。

![每週排程](./media/backup-azure-backup-cloud-as-tape/weeklybackupschedule.png)

## <a name="what-is-hello-retention-policy"></a>Hello 保留原則是什麼？
hello 保留原則會指定必須儲存 hello 備份 hello 持續時間。 而不是只指定 「 一般原則 」 的所有備份點時，客戶可以指定不同的保留原則以 hello 備份時。 例如，hello 備份點採取，每天會做為操作的復原點，會保留 90 天。 在 hello 基於稽核目的每季結束時採取的 hello 備份點保留較長時間。

![保留原則](./media/backup-azure-backup-cloud-as-tape/retentionpolicy.png)

hello 的此原則中指定 「 保留點 」 總數是 90 （每日點） 加上 40 (分別指派 10 年的季) = 130。

## <a name="example--putting-both-together"></a>範例 – 將兩者綜合比較
![範例畫面](./media/backup-azure-backup-cloud-as-tape/samplescreen.png)

1. **每日的保留原則**：每日所進行的備份會儲存 7 天。
2. **每週的保留原則**：每天午夜和星期六下午 6 點所進行的備份會保留 4 週
3. **每月保留原則**： 在午夜到下午 6 hello 上每個月的最後一個星期六的備份會保留 12 個月
4. **每年保留原則**: hello 午夜建立的每年 3 月的最後一個星期六的備份會保留為 10 年

hello 「 保留點 」 的總數 （客戶可以還原資料點） hello 在上圖的計算方式如下：

* 7 天中每天 2 個保留點 = 14 個復原點
* 4 週中每週 2 個保留點 = 8 個復原點
* 12 個月中每月 2 個保留點 = 24 個復原點
* 10 年中每年 1 個保留點 = 10 個復原點

hello 總數的復原點是 56。

> [!NOTE]
> Azure 備份對於復原點數目沒有限制。
>
>

## <a name="advanced-configuration"></a>進階組態
依序按一下**修改**hello 前面螢幕，在客戶會有進一步彈性，指定保留排程。

![修改](./media/backup-azure-backup-cloud-as-tape/modify.png)

## <a name="next-steps"></a>後續步驟
如需有關 Azure Backup 的詳細資訊，請參閱：

* [簡介 tooAzure 備份](backup-introduction-to-azure-backup.md)
* [試用 Azure 備份](backup-try-azure-backup-in-10-mins.md)
