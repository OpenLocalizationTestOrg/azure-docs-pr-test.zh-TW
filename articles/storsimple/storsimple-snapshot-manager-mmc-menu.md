---
title: "aaaStorSimple 快照集管理員 MMC 功能表動作 |Microsoft 文件"
description: "描述如何 toouse hello 標準的 Microsoft Management Console (MMC) 功能表動作中 StorSimple Snapshot Manager。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 78ef81af-0d3a-4802-be54-ad192f9ac8a6
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: e7ba42cf2086c552bcc06b528abdead8fe4534d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-mmc-menu-actions-in-storsimple-snapshot-manager"></a>StorSimple Snapshot Manager 中使用 hello MMC 功能表動作

## <a name="overview"></a>概觀
在 StorSimple Snapshot Manager 中，您會看到下列所有動作功能表和 hello 的所有變化所列的動作的 hello**動作**窗格。

* 檢視
* 從這裡開啟新視窗 
* 重新整理 
* 匯出清單 
* 說明 

這些動作是 hello Microsoft Management Console (MMC) 的一部分，並不是特定 tooStorSimple Snapshot Manager。 本教學課程描述這些動作，並說明如何 toouse 每個這些 StorSimple Snapshot Manager 中。

## <a name="view"></a>檢視
您可以使用 hello**檢視**選項 toochange hello**結果**窗格檢視及 toochange hello 主控台視窗檢視。 

#### <a name="toochange-hello-results-pane-view"></a>toochange hello 結果 窗格檢視
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 hello**範圍** 窗格中，以滑鼠右鍵按一下任何節點或展開 hello 節點，然後以滑鼠右鍵按一下 hello 中的項目**結果** 窗格中，然後按一下hello**檢視**選項。 
3. tooadd 或移除 hello 資料行出現在 hello**結果**] 窗格中，按一下 [**新增/移除欄位**。 hello**新增/移除欄位** 對話方塊隨即出現。
   
    ![新增或移除 [結果] 窗格中的資料行](./media/storsimple-snapshot-manager-mmc-menu/HCS_SSM_Add_remove_columns.png) 
4. 完成 hello 表單，如下所示：
   
   * 選取的項目從 hello**可用**資料行清單，然後按一下**新增**tooadd 它們 toohello**顯示資料行**清單。 
   * 按一下項目在 hello**顯示資料行**清單，然後按**移除**tooremove 其 hello 清單。 
   * 選取項目 hello**顯示**資料行清單，然後按一下**移**或**下移**toomove hello 項目向上或向下 hello 清單中的。 
   * 按一下**還原成預設值**tooreturn toohello 預設**結果**窗格組態。 
5. 當完成您的選擇時，請按一下 [ **確定**]。 

#### <a name="toochange-hello-console-window-view"></a>toochange hello 主控台視窗檢視
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 [hello**範圍**] 窗格中，以滑鼠右鍵按一下任何節點，按一下**檢視**，然後按一下**自訂**。 hello**自訂** 對話方塊隨即出現。
   
    ![自訂 hello 主控台視窗](./media/storsimple-snapshot-manager-mmc-menu/HCS_SSM_Customize.png) 
3. 選取或清除 [hello] 核取方塊 tooshow 或隱藏 hello 主控台視窗中的項目。 當完成您的選擇時，請按一下 [ **確定**]。

## <a name="new-window-from-here"></a>從這裡開啟新視窗
您可以使用 hello**從這裡開啟新視窗**選項 tooopen 新的主控台視窗。

#### <a name="tooopen-a-new-console-window"></a>tooopen 新的主控台視窗
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 [hello**範圍**] 窗格中，以滑鼠右鍵按一下任何節點，然後**從這裡開啟新視窗**。 
   
    新視窗隨即出現，顯示您選取 hello 範圍。 比方說，如果您以滑鼠右鍵按一下 hello**備份原則** 節點，hello 新視窗會顯示只有 hello**備份原則**節點 hello**範圍**窗格以及一份定義備份原則中 hello**結果**窗格。 請參閱下列範例中的 hello。
   
    ![從這裡開啟新視窗](./media/storsimple-snapshot-manager-mmc-menu/HCS_SSM_NewWindow.png) 

## <a name="refresh"></a>重新整理
您可以使用 hello**重新整理**動作 tooupdate hello 主控台視窗。

#### <a name="tooupdate-hello-console-window"></a>tooupdate hello 主控台視窗
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 hello**範圍** 窗格中，以滑鼠右鍵按一下任何節點或展開 hello 節點，然後以滑鼠右鍵按一下 hello 中的項目**結果** 窗格中，然後再按一下**重新整理**。 

## <a name="export-list"></a>匯出清單
您可以使用 hello**匯出清單**動作 toosave 逗點分隔值 (CSV) 檔案中的清單。 例如，您可以匯出備份原則或 hello 備份類別目錄的 hello 清單。 您接著可以將 hello CSV 檔案匯入試算表應用程式進行分析。

#### <a name="toosave-a-list-in-a-comma-separated-value-csv-file"></a>toosave 逗點分隔值 (CSV) 檔案中的清單
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。 
2. 在 hello**範圍** 窗格中，以滑鼠右鍵按一下任何節點或展開 hello 節點，然後以滑鼠右鍵按一下 hello 中的項目**結果** 窗格中，然後再按一下**匯出清單**。 
3. hello**匯出清單** 對話方塊隨即出現。 完成 hello 表單，如下所示： 
   
   1. 在 hello**檔案名稱**方塊中，輸入 hello CSV 檔案的名稱或按一下 hello 箭號 tooselect hello 下拉式清單中的。
   2. 在 hello**存檔類型**方塊，按一下 hello 箭號，從 hello 下拉式清單中選取檔案類型。
   3. toosave 只選取項目，選取 hello 資料列，然後按一下 hello**只儲存選取的列**核取方塊。 匯出 toosave 所有清單清除 hello**只儲存選取的列**核取方塊。
   4. 按一下 [儲存] 。
      
      ![將清單匯出成逗號分隔值檔案](./media/storsimple-snapshot-manager-mmc-menu/HCS_SSM_Export_List.png) 

## <a name="help"></a>說明
您可以使用 hello**協助**功能表 tooview 可用線上說明 StorSimple Snapshot Manager 和 hello MMC。

#### <a name="tooview-available-online-help"></a>tooview 可用的線上說明
1. 按一下 hello 桌面圖示 toostart StorSimple Snapshot Manager。
2. 在 hello**範圍** 窗格中，以滑鼠右鍵按一下任何節點或展開 hello 節點，然後以滑鼠右鍵按一下 hello 中的項目**結果** 窗格中，然後再按一下**協助**。 

## <a name="next-steps"></a>後續步驟
* 深入了解 hello [StorSimple Snapshot Manager 使用者介面](storsimple-use-snapshot-manager.md)。
* 深入了解[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。

