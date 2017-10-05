---
title: "複製 StorSimple 磁碟區 | Microsoft Docs"
description: "說明不同的複製類型以及使用時機，並說明如何使用備份組來複製個別磁碟區。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b5d615f2-02a7-4222-9867-6c0385ce748c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 8f1936fac543f559a44ad0f9c35b30d1a92dce68
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-manager-service-to-clone-a-volume"></a>使用 StorSimple Manager 服務來複製磁碟區
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a>Overview
StorSimple Manager 服務 [備份類別目錄]  頁面會顯示在進行手動或自動備份時所建立的所有備份組。 您可以使用此頁面來列出備份原則或磁碟區的所有備份、選取或刪除備份，或是使用備份來還原或複製磁碟區。

![備份類別目錄頁面](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

本教學課程說明如何使用備份組來複製個別磁碟區。 它也會說明「暫時性」與「永久」複製之間的差異。 

## <a name="create-a-clone-of-a-volume"></a>建立磁碟區複製
您可以使用本機或雲端快照，在相同的裝置、 另一個裝置或甚至虛擬機器上建立複製。

#### <a name="to-clone-a-volume"></a>若要複製磁碟區
1. 在 StorSimple Manager 服務頁面上，按一下  [備份類別目錄]  索引標籤，然後選取備份組。
2. 展開備份組以檢視相關聯的磁碟區。 從備份組中按一下並選取磁碟區。
   
     ![複製磁碟區](./media/storsimple-clone-volume/HCS_Clone.png) 
3. 按一下 [複製]  ，以開始複製選取的磁碟區。
4. 在 [複製磁碟區精靈] 的 [指定名稱和位置] 下：
   
   1. 識別目標裝置。 這是即將建立複製的位置。 您可以選擇相同的裝置，或指定另一個裝置。 如果您選擇與其他雲端服務提供者相關的磁碟區 (非 Azure)，目標裝置的下拉式清單將只會顯示實體裝置。 您無法在虛擬裝置上複製與其他雲端服務提供者相關聯的磁碟區。
      
      > [!NOTE]
      > 確定要複製的容量小於目標裝置中可用的容量。
      > 
      > 
   2. 為複製指定唯一的磁碟區名稱。 此名稱必須包含 3 到 127 個字元。
   3. 按一下箭頭圖示  ![arrow-icon](./media/storsimple-clone-volume/HCS_ArrowIcon.png) ，繼續前往下一頁。
5. 在 [指定可以使用此磁碟區的主機] 下：
   
   1. 指定該複製的存取控制記錄 (ACR)。 您可以加入新的 ACR，或從現有清單中選擇。
   2. 按一下核取圖示  ![核取圖示](./media/storsimple-clone-volume/HCS_CheckIcon.png)完成操作。
6. 複製工作隨即起始並在成功建立複製時通知您。 按一下 [檢視工作]，在 [工作] 頁面上監視複製工作。
7. 複製工作完成後：
   
   1. 移至 [裝置] 頁面，然後選取 [磁碟區容器] 索引標籤。 
   2. 選取與複製的來源磁碟區相關聯的磁碟區容器。 您應該會在磁碟區清單中看到剛才建立的複製。

> [!NOTE]
> 複製的磁碟區上會自動停用監視和預設備份。
> 
> 

以這種方式建立的複製就是暫時性複製。 如需複製類型的詳細資訊，請參閱 [暫時性與永久複製](#transient-vs-permanent-clones)。

此複製現在是一般的磁碟區，可在磁碟區進行的任何操作都能在此複製進行。 您必須設定此磁碟區以進行任何備份。

## <a name="transient-vs-permanent-clones"></a>暫時性與永久複製
只有在您複製到不同裝置時才會建立暫時性和永久複製。 您可以從備份組複製特定磁碟區到不同裝置。 以這種方式建立的複製就是「暫時性」  複製。 暫時性複製會有原始磁碟區的參考，並在本機寫入時使用該磁碟區來讀取。 

在建立暫時性複製的雲端快照之後，產生的複製就是「永久」  複製。 永久複製獨立且沒有所複製原始磁碟區的任何參考。  

## <a name="scenarios-for-transient-and-permanent-clones"></a>暫時性複製與永久複製的案例
下列各節將說明可使用暫時性複製與永久複製的範例情況。

### <a name="item-level-recovery-with-a-transient-clone"></a>使用暫時性複製復原項目層級
您要復原過去一年的 Microsoft PowerPoint 簡報檔案。 IT 系統管理員辨識該時間範圍內的特定備份，然後篩選磁碟區。 系統管理員接著再複製磁碟區，找出您要找的檔案再提供給您。 在此案例中，使用的是暫時性複製。 

![提供的影片](./media/storsimple-clone-volume/Video_icon.png) **提供的影片**

若要觀看影片示範如何使用 StorSimple 的複製和還原功能來復原已刪除的檔案，請按一下 [這裡](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/)。

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a>利用永久複製在實際執行環境中進行測試
您需要確認生產環境中的測試錯誤。 您要使用複製的雲端快照，在生產環境中建立磁碟區的複製。 複製的磁碟區現在是獨立的。 在此案例中，使用的是永久複製。

## <a name="next-steps"></a>後續步驟
* 了解如何 [從備份組還原 StorSimple 磁碟區](storsimple-restore-from-backup-set.md)。
* 了解如何 [使用 StorSimple Manager 服務管理 StorSimple 裝置](storsimple-manager-service-administration.md)。

