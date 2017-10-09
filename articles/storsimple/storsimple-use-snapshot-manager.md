---
title: "aaaStorSimple Snapshot Manager 使用者介面 |Microsoft 文件"
description: "描述 hello StorSimple Snapshot Manager 使用者介面，並說明如何 toouse 它 toomanage，備份作業和 hello 備份類別目錄。"
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: c7d91892-2881-41a2-a7a2-908dc3646493
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.custom: 
ms.openlocfilehash: 865520fdaf1b559714b52b428ad136b084d65c99
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-user-interface-toomanage-backup-jobs-and-backup-catalog"></a>使用 StorSimple Snapshot Manager 使用者介面 toomanage 備份作業和備份類別目錄

## <a name="overview"></a>概觀
hello StorSimple Snapshot Manager 有直覺式使用者介面，您可以使用 tootake 和管理備份。 本教學課程提供簡介 toohello 使用者介面，並接著說明如何 toouse 每個 hello 元件。 Hello StorSimple Snapshot Manager 的詳細說明，請參閱[什麼是 StorSimple Snapshot Manager？](storsimple-what-is-snapshot-manager.md)

### <a name="console-description"></a>主控台說明
tooview hello 使用者介面，請按一下桌面上的 hello StorSimple Snapshot Manager 圖示。 hello 主控台視窗隨即出現，hello 下列圖例所示。

![StorSimple Snapshot Manager 密碼](./media/storsimple-use-snapshot-manager/HCS_SSM_gui_panes.png)

hello 主控台視窗有五個主要元素。 按一下每個元素的完整描述的 hello 適當連結。

* [功能表列](#menu-bar) 
* [工具列](#tool-bar) 
* [範圍窗格](#scope-pane) 
* [結果窗格](#results-pane) 
* [動作窗格](#actions-pane) 

此外，StorSimple Snapshot Manager 支援的 hello[鍵盤導覽和快速鍵數](#keyboard-navigation-and-shortcuts)。

### <a name="console-accessibility"></a>主控台協助工具
hello StorSimple Snapshot Manager 使用者介面支援 hello hello Windows 作業系統和 hello Microsoft Management Console (MMC)，以及某些特定 StorSimple Snapshot Manager 鍵盤快速鍵所提供的協助工具功能。 

* 如需 hello Windows 協助工具功能的說明，請移至太[Windows 的鍵盤快速鍵](https://support.microsoft.com/kb/126449)。 
* 如需 hello MMC 協助工具功能的說明，請移至太[MMC 3.0 協助工具](https://technet.microsoft.com/library/cc766075.aspx)
* 如需 hello StorSimple Snapshot Manager 協助工具功能的說明，請移至太[鍵盤導覽和快速鍵](#keyboard-navigation-and-shortcuts)。

## <a name="menu-bar"></a>功能表列
hello hello hello 主控台視窗上方的功能表列包含[檔案](#file-menu)，[動作](#action-menu)，[檢視](#view-menu)，[我的最愛](#favorites-menu)，[視窗](#window-menu)，和[協助](#help-menu)功能表。

按一下 hello 功能表列 toosee 清單上可用的命令，該功能表上的任何項目。 hello 下列範例顯示 hello**檢視**hello 功能表列上選取的功能表。

![已選取 [檢視] 功能表](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png)

### <a name="file-menu"></a>[檔案] 功能表
hello**檔案**功能表包含標準的 Microsoft Management Console (MMC) 命令。

#### <a name="menu-access"></a>功能表存取
tooview hello**檔案**功能表上，按一下 **檔案**hello 功能表列上。 hello 下列功能表隨即出現。

![StorSimple Snapshot Manager 檔案功能表](./media/storsimple-use-snapshot-manager/HCS_SSM_FileMenu.png) 

#### <a name="menu-description"></a>功能表說明
hello 下表描述出現的項目 hello**檔案**功能表。

| 功能表項目 | 說明 |
|:--- |:--- |
| 新增 |按一下**新增**toocreate hello StorSimple Snapshot Manager 以新的主控台。 |
| 開啟 |按一下**開啟**tooopen 現有的主控台。 |
| 儲存 |按一下**儲存**toosave hello 目前的主控台。 |
| 另存新檔 |按一下**存**toocreate hello 目前主控台的新、 重新命名執行個體。 使用 hello**存**選項 toocustomize 檢視並儲存起來供日後擷取。 例如，您可以建立 StorSimple Snapshot Manager 嵌入式管理單元該點 toospecific 伺服器。 |
| 新增/移除嵌入式管理單元 |按一下**新增/移除嵌入式管理單元**tooadd 或移除嵌入式管理單元和 tooorganize 節點在 hello**範圍**窗格。 如需詳細資訊，請移至太[新增、 移除及組織嵌入式管理單元和 MMC 3.0 中的延伸模組](https://technet.microsoft.com/library/cc722035.aspx)。 |
| 選項 |按一下**選項**toochange hello 主控台圖示，請指定使用者存取模式和權限，或刪除主控台檔案 tooincrease 可用磁碟空間。 |
| 檔案路徑的清單 |按一下 hello 編號清單 tooreopen 最近開啟的檔案中的路徑。 |
| 結束 |按一下**結束**tooclose hello**檔案**功能表。 |

### <a name="action-menu"></a>動作功能表
使用 hello**動作**功能表 tooselect 從可用的動作。 hello 項目可用 tooyou 取決於您在 hello 的 hello 選擇**範圍**窗格或**結果**窗格。

#### <a name="menu-access"></a>功能表存取
tooview hello**動作**功能表中，執行 hello 下列其中一種：

* 以滑鼠右鍵按一下項目在 hello**範圍**窗格或**結果**窗格。
* 選取的項目在 hello**範圍**窗格或**結果** 窗格中，然後再按一下**動作**hello 功能表列上。 

例如，如果您選取 hello 最上層節點在 hello**範圍** 窗格中，然後以滑鼠右鍵按一下**動作**hello 功能表列中，hello 會出現下列功能表。

![StorSimple Snapshot Manager 動作功能表](./media/storsimple-use-snapshot-manager/HCS_SSM_Action_menu.png)

hello**動作**（在 hello hello 主控台的右) 窗格包含 hello hello 為相同的動作清單**動作**功能表。 此外，hello**動作**窗格包含 hello**檢視**功能表選項，可讓您 toocreate hello 的自訂檢視**結果**窗格。

![已開啟 [檢視] 功能表的 [動作] 窗格](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

#### <a name="menu-description"></a>功能表說明
下表中的 hello 包含 StorSimple Snapshot Manager 動作的字母順序排列。 

* hello**動作**欄會列出您可以在節點和結果執行的動作。 
* hello**瀏覽**資料行會說明如何 toodisplay hello 適當**動作**功能表，讓您可以選取 hello 動作。 有些動作會出現在多個 [ **動作** ] 功能表中。 這些動作中，選取其中一個**瀏覽**hello 項目符號清單中的選項。 
* hello**描述**資料行描述如何 toouse hello 上的每個動作**動作**功能表或 [動作] 窗格中，並說明其用途。

> [!NOTE]
> hello**動作**窗格和**動作**功能表包含其他選項，例如**檢視**，**從這裡開啟新視窗**， **重新整理**，**匯出清單**，和**協助**。 這些選項可提供 hello MMC 的一部分，而且不是特定 tooStorSimple Snapshot Manager。 hello 資料表包含這些選項的描述。
> 
> 

| 動作 | 導覽 | 說明 |
|:--- |:--- |:--- |
| 驗證 |按一下 hello**裝置**節點，然後以滑鼠右鍵按一下裝置，以在 hello**結果**窗格。 |按一下**驗證**tooenter hello 密碼為 hello 裝置所設定。 |
| 複製 |展開**備份類別目錄**，依序展開**雲端快照**，按一下 帶有的備份，然後選取磁碟區在 hello**結果**窗格。 |按一下**複製**toocreate 一份雲端快照集，並將它儲存在您指定的位置。 |
| 設定裝置 |以滑鼠右鍵按一下 hello**裝置**節點。 |按一下**設定裝置**tooconfigure 單一裝置或多個裝置 tooconnect toohello Windows 主機。 |
| 建立備份原則 |執行 hello 下列其中一種動作：<ul><li>以滑鼠右鍵按一下 [備份原則]。</li><li>按一下或展開**磁碟區群組**，然後以滑鼠右鍵按一下磁碟區群組。</li><li>按一下或展開**備份目錄**，然後以滑鼠右鍵按一下磁碟區群組。</li></ul> |按一下**建立備份原則**tooconfigure 排定的備份磁碟區群組。 |
| 建立磁碟區群組 |執行 hello 下列其中一種動作：<ul><li>按一下 hello**磁碟區**節點，然後再以滑鼠右鍵按一下磁碟區在 hello**結果**窗格。</li><li>以滑鼠右鍵按一下 hello**磁碟區群組**節點。</li></ul> |按一下**建立磁碟區群組**tooassign 磁碟區 tooa 磁碟區群組。 |
| 刪除 |按一下節點或結果 (此項目出現在許多 [動作] 功能表和 [動作] 窗格上。) |按一下**刪除**toodelete hello 節點或您所選取的結果。 Hello 確認對話方塊出現時，請確認或取消 hello 刪除。 |
| 詳細資料 |按一下 hello**裝置**節點，然後再以滑鼠右鍵按一下裝置，以在 hello**結果**窗格。 |按一下**詳細資料**toosee 裝置 hello 設定詳細資料。 |
| Edit |按一下**備份原則**，然後以滑鼠右鍵按一下 [hello] 中的原則**結果**窗格。 |按一下**編輯**toochange hello 備份排程為磁碟區群組。 |
| 匯出清單 |按一下任何節點或結果 (此項目出現在所有 [動作] 功能表和 [動作] 窗格上。) |按一下**匯出清單**toosave 逗點分隔值 (CSV) 檔案中的清單。 然後，您可以將這個檔案匯入試算表應用程式進行分析。 |
| 說明 |按一下任何節點或結果。 (此項目出現在所有 [動作] 功能表和 [動作] 窗格上。) |按一下**協助**tooopen 線上說明中另一個瀏覽器視窗。 |
| 從這裡開啟新視窗 |按一下任何節點或結果 (此項目出現在所有 [動作] 功能表和 [動作] 窗格上。) |按一下**從這裡開啟新視窗**tooopen 新的 StorSimple Snapshot Manager 視窗。 |
| 重新整理 |按一下任何節點或結果 (此項目出現在所有 [動作] 功能表和 [動作] 窗格上。) |按一下**重新整理**tooupdate 目前顯示的 hello StorSimple Snapshot Manager 視窗。 |
| 重新整理裝置 |按一下 hello**裝置**節點，然後以滑鼠右鍵按一下裝置，以在 hello**結果**窗格。 |按一下**重新整理裝置**toosynchronize 特定連接的裝置與 StorSimple Snapshot Manager。 |
| 重新整理裝置 |以滑鼠右鍵按一下 hello**裝置**節點。 |按一下**重新整理裝置**toosynchronize 您連接的裝置與 StorSimple Snapshot Manager 的清單。 |
| 重新掃描磁碟區 |以滑鼠右鍵按一下 hello**磁碟區**節點。 |按一下**重新掃描磁碟區**tooupdate hello 的磁碟區清單會出現在 hello**結果**窗格。 |
| 還原 |依序展開 [備份目錄]、磁碟區群組和[本機快照] 或 [雲端快照]，然後以滑鼠右鍵按一下備份。 |按一下**還原**tooreplace hello 目前磁碟區群組資料與 hello 資料從 hello 選備份。 |
| 進行備份 |執行 hello 下列其中一種動作：<ul><li>展開**磁碟區群組**，然後以滑鼠右鍵按一下磁碟區群組。</li><li>展開**備份目錄**，然後以滑鼠右鍵按一下磁碟區群組。</li></ul> |按一下**取得備份**toostart 立即備份工作。 |
| 切換匯入顯示 |以滑鼠右鍵按一下 hello 中的最上層節點 hello**範圍**窗格 (hello **StorSimple Snapshot Manager** hello 範例中的節點)。 |按一下**切換匯入顯示**tooshow 或隱藏 hello 磁碟區群組及相關聯的備份從匯入 hello StorSimple 裝置管理員服務儀表板。 |

### <a name="view-menu"></a>檢視功能表
使用 hello**檢視**功能表 toocreate hello 的自訂檢視**結果**窗格內容。 hello**檢視**功能表包含**新增/移除欄位**和**自訂**選項。

#### <a name="menu-access"></a>功能表存取
您可以存取 hello**檢視**功能表 hello 功能表列上或在 hello**動作**窗格。

![StorSimple Snapshot Manager 檢視功能表](./media/storsimple-use-snapshot-manager/HCS_SSM_View_menu.png) 

#### <a name="menu-description"></a>功能表說明
hello 下表描述出現的項目 hello**檢視**功能表。

| 功能表項目 | 說明 |
|:--- |:--- |
| 新增/移除資料行 |按一下**新增/移除欄位**hello tooadd 或移除資料行**結果**窗格。 |
| 自訂 |按一下**自訂**tooshow 或隱藏 hello StorSimple Snapshot Manager 主控台視窗中的項目。 |

### <a name="favorites-menu"></a>我的最愛功能表
使用 hello**我的最愛**功能表 tooadd 移除及組織檢視的網頁和您經常使用的工作。 

#### <a name="menu-access"></a>功能表存取
您可以存取 hello**我的最愛**hello 功能表列。

![StorSimple Snapshot Manager 我的最愛功能表](./media/storsimple-use-snapshot-manager/HCS_SSM_FavoritesMenu.png)

#### <a name="menu-description"></a>功能表說明
hello 下表描述出現的項目 hello**我的最愛**功能表。

| 功能表項目 | 說明 |
|:--- |:--- |
| 新增 tooFavorites |按一下**新增 tooFavorites** tooadd hello 目前檢視 tooyour 我的最愛清單。 |
| 組織我的最愛 |按一下**組織我的最愛** tooorganize hello 內容的 我的最愛 資料夾。 |

### <a name="window-menu"></a>視窗功能表
使用 hello**視窗**功能表 tooadd 和重新整理 StorSimple Snapshot Manager 主控台視窗。

#### <a name="menu-access"></a>功能表存取
您可以存取 hello**視窗**hello 功能表列。

![StorSimple Snapshot Manager 視窗功能表](./media/storsimple-use-snapshot-manager/HCS_SSM_WindowMenu.png)

hello hello hello 功能表底部的編號的清單顯示目前的 hello 視窗開啟。 按一下該清單 toobring hello 視窗中的任何視窗到 hello 前景。 

#### <a name="menu-description"></a>功能表說明
hello 下表描述 hello 的項目會顯示 hello [視窗] 功能表上。

| 功能表項目 | 說明 |
|:--- |:--- |
| 開新視窗 |按一下**新視窗**tooopen 新的主控台視窗 （在加法 toohello 現有視窗）。 |
| 重疊顯示 |按一下**Cascade** toodisplay hello 開啟的主控台視窗中的階層式樣式。 |
| 水平並排顯示 |按一下**水平並排**toodisplay hello 開啟的主控台視窗中並排顯示 （或方格） 格式。 |
| 排列圖示 |如果您有多個主控台視窗開啟和散落於整個桌面上，將其降至最低，然後按一下**排列圖示**tooarrange hello 螢幕底部的水平資料列中。 |

### <a name="help-menu"></a>說明功能表
使用 hello**協助**功能表 tooview 可用線上說明 StorSimple Snapshot Manager 和 hello MMC。 您也可以檢視 hello MMC 與 StorSimple Snapshot Manager 軟體版本，您的系統上目前安裝的相關資訊。 

您可以存取 hello**協助**hello 功能表列。 您也可以從 hello 存取 StorSimple Snapshot Manager [說明] 主題**動作**窗格。

![StorSimple Snapshot Manager 說明功能表](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpMenu.png)

#### <a name="menu-description"></a>功能表說明
hello 下表描述 hello 說明 功能表中出現的項目。

| 功能表項目 | 說明 |
|:--- |:--- |
| StorSimple Snapshot Manager 的相關說明 |按一下**協助在 StorSimple Snapshot Manager** tooopen StorSimple Snapshot Manager 說明中另一個視窗。 |
| 說明主題 |按一下**說明主題**tooopen MMC 線上說明中另一個視窗。 |
| TechCenter 網站 |按一下**TechCenter 網站**tooopen hello Microsoft TechNet 技術中心首頁個別視窗中。 |
| 關於 Microsoft Management Console |按一下**關於 Microsoft Management Console** toosee 哪個版本的 hello Microsoft Management Console 安裝在您的系統上。 |
| 關於 StorSimple Snapshot Manager |按一下**關於 StorSimple Snapshot Manager** toosee hello 嵌入式管理單元的版本已安裝在您的系統。 |

## <a name="tool-bar"></a>工具列
hello 工具列上，位於下方 hello 功能表列包含瀏覽和工作的圖示。 每個圖示是捷徑 tooa 特定工作。

### <a name="icon-descriptions"></a>圖示說明
hello 下表描述 hello 圖示會出現在 hello 工具列上。 

| 圖示 | 說明 |
|:--- |:--- |
| ![向左箭號](./media/storsimple-use-snapshot-manager/HCS_SSM_LeftArrow.png) |按一下 hello 向左箭號圖示 tooreturn toohello 前一頁。 |
| ![向右箭號](./media/storsimple-use-snapshot-manager/HCS_SSM_RightArrow.png) |按一下 hello 向右箭號 toogo toohello 下一頁 （如果 hello 箭頭呈現灰色，hello 動作是無法使用）。 |
| ![向上圖示](./media/storsimple-use-snapshot-manager/HCS_SSM_Up.png) |按一下 上移一層 hello 主控台樹狀目錄中的圖示 toogo hello (hello**範圍**窗格)。 |
| ![顯示/隱藏主控台樹狀目錄](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowConsoleTree.png) |按一下 hello 顯示/隱藏主控台樹狀目錄圖示 tooshow 或隱藏 hello**範圍**窗格。 |
| ![匯出清單](./media/storsimple-use-snapshot-manager/HCS_SSM_ExportListIcon.png) |按一下 hello 匯出清單圖示 tooexport 您指定的清單 tooa CSV 檔案。 |
| ![説明圖示](./media/storsimple-use-snapshot-manager/HCS_SSM_HelpIcon.png) |按一下 hello 說明圖示 tooopen 線上 MMC 說明主題。 |
| ![顯示/隱藏動作窗格](./media/storsimple-use-snapshot-manager/HCS_SSM_ShowAction.png) |按一下 顯示/隱藏 hello**動作**窗格圖示 tooshow 或隱藏 hello**動作**窗格。 |

## <a name="scope-pane"></a>範圍窗格
hello**範圍**hello hello StorSimple Snapshot Manager UI 中的最左邊窗格。 它包含 hello 主控台 （或節點） 樹狀目錄，而且是 hello 主要瀏覽機制 StorSimple Snapshot Manager。 

### <a name="scope-pane-structure"></a>範圍窗格結構
hello**範圍**窗格包含一系列可點選物件 （節點） 組織成樹狀結構。 

![範圍窗格](./media/storsimple-use-snapshot-manager/HCS_SSM_Scope_pane.png) 

* tooexpand 或摺疊節點，按一下 hello 箭號圖示 下一步 toohello 節點名稱。
* tooview hello 狀態或內容節點中，按一下 hello 節點名稱。 hello 資訊會出現在 hello**結果**窗格。 

hello**範圍**窗格包含 hello 下列節點： 

* [裝置節點](#devices-node) 
* [磁碟區節點](#volumes-node) 
* [磁碟區群組節點](#volume-groups-node) 
* [備份原則節點](#backup-policies-node) 
* [備份目錄節點](#backup-catalog-node) 
* [作業節點](#jobs-node) 

### <a name="scope-pane-tasks"></a>範圍窗格工作
您可以使用 hello**範圍**窗格 toocomplete 特定節點上的動作。 tooselect 項工作中，執行 hello 下列其中一種動作：

* Hello 節點上按一下滑鼠右鍵，然後從出現的 hello 功能表中選取 hello 工作。
* 按一下 [hello] 節點，然後按一下**動作**hello 功能表列上。 從出現的 hello 功能表選取 hello 工作。
* 按一下 hello 節點，然後再選取 hello 動作在 hello**動作**窗格。

當您選取的節點，並使用任何這些方法 toosee 工作清單中時，會顯示只可以在該節點執行的動作。

### <a name="devices-node"></a>裝置節點
hello**裝置**節點代表 hello StorSimple 裝置和 StorSimple 虛擬裝置的連線的 tooStorSimple Snapshot Manager。 選取此節點 tooconnect 和設定裝置，並匯入其相關聯的磁碟區、 磁碟區群組和現有的備份複本。 多個裝置可以是連線的 tooa 單一主機。

* tooexpand hello 節點中，按一下 hello 箭號圖示下一步太**裝置**。
* toosee 功能表可用的動作，以滑鼠右鍵按一下 hello**裝置**節點或以滑鼠右鍵按一下任何出現在 hello 的 hello 節點展開檢視。
* toosee 設定裝置清單，按一下**裝置**在 hello**範圍**窗格。 hello 的裝置清單，以及每個裝置的相關資訊會出現在 hello**結果**窗格。

### <a name="volumes-node"></a>磁碟區節點
hello**磁碟區**節點代表對應 toohello 所 hello 主機，包括透過 iSCSI 和探索到的裝置探索到掛接的磁碟區的 hello 磁碟機。 使用此節點 tooview hello 清單可用的磁碟區，並且將 toovolume 群組指派個別磁碟區。

* tooexpand hello 節點中，按一下 hello 箭號圖示下一步太**磁碟區**。
* toosee 功能表可用的動作，以滑鼠右鍵按一下 hello**磁碟區**節點或以滑鼠右鍵按一下任何出現在 hello 的 hello 節點展開檢視。
* toosee 一份磁碟區，按一下**磁碟區**在 hello**範圍**窗格。 磁碟區，以及每個磁碟區的相關資訊的 hello 清單會出現在 hello**結果**窗格。

### <a name="volume-groups-node"></a>磁碟區群組節點
磁碟區群組也稱為一致性群組。 每個磁碟區群組是在備份作業期間協助 tooensure 應用程式一致性的應用程式相關的磁碟區的集區。 使用 hello**磁碟區群組**節點 tooconfigure 這些群組與 tootake 互動式備份或建立備份排程。 

* tooexpand hello 節點中，按一下 hello 箭號圖示下一步太**磁碟區群組**。
* toosee 功能表可用的動作，以滑鼠右鍵按一下 hello**磁碟區群組**節點或以滑鼠右鍵按一下任何出現在 hello 的 hello 節點展開檢視。
* toosee 一份磁碟區群組，按一下**磁碟區群組**在 hello**範圍**窗格。 hello 磁碟區群組，以及每個磁碟區群組的相關資訊清單會出現在 hello**結果**窗格。

### <a name="backup-policies-node"></a>備份原則節點
備份原則是本機和雲端快照的作業排程。 使用 hello**備份原則**節點 toospecify 建立備份的頻率以及備份應該多久保留。 

* tooexpand hello 節點中，按一下 hello 箭號圖示下一步太**備份原則**。
* toosee 功能表可用的動作，以滑鼠右鍵按一下 hello**備份原則**節點或以滑鼠右鍵按一下任何出現在 hello 的 hello 節點展開檢視。
* toosee 一份備份原則，按一下**備份原則**在 hello**範圍**窗格。 hello 備份原則，以及每個原則的相關資訊清單會出現在 hello**結果**窗格。

> [!NOTE]
> 您最多可以保留 64 個備份。


### <a name="backup-catalog-node"></a>備份目錄節點
hello**備份類別目錄**節點包含的站上與離站備份的 Azure StorSimple 磁碟區清單。 此節點依磁碟區群組，以及每個磁碟區群組容器包含不同的結構，本機快照 (hello**本機快照**s 節點) 和雲端快照集 (hello**雲端快照**節點). 展開時，每個磁碟區群組容器會列出所有 hello 成功的備份以互動方式或依據設定的原則所執行的。

* tooexpand hello 節點中，按一下 hello 箭號圖示下一步太**備份類別目錄**。
* toosee 功能表可用的動作，以滑鼠右鍵按一下 hello**備份類別目錄**節點或以滑鼠右鍵按一下任何出現在 hello 的 hello 節點展開檢視。
* toosee 一份備份快照集，按一下**備份類別目錄**在 hello**範圍**窗格。 hello 快照清單會連同每個快照集的相關資訊會出現在 hello**結果**窗格。

### <a name="local-snapshots-node"></a>本機快照節點
hello**本機快照**節點會列出特定磁碟區群組的本機快照。 hello 節點位於 hello**備份類別目錄**節點 hello**範圍**窗格。 本機快照集是儲存在 hello Azure StorSimple 裝置的磁碟區資料的時間點副本。 一般而言，可以快速建立和還原這種類型的備份。 您可以如同使用本機備份複本一般使用本機快照。

* tooexpand hello 節點中，按一下 hello 箭號圖示下一步太**本機快照**。
* toosee 功能表可用的動作，以滑鼠右鍵按一下 hello**本機快照**節點或以滑鼠右鍵按一下任何出現在 hello 的 hello 節點展開檢視。
* 按一下 toosee 本機快照集，一份**本機快照**在 hello**範圍**窗格。 hello 快照清單會連同每個快照集的相關資訊會出現在 hello**結果**窗格。

### <a name="cloud-snapshots-node"></a>雲端快照節點
hello**雲端快照**節點會列出特定磁碟區群組的雲端快照。 hello 節點位於 hello**備份類別目錄**節點 hello**範圍**窗格。 雲端快照集是儲存在 hello 雲端中的磁碟區資料的時間點複本。 雲端快照相當 tooa 快照式複寫不同的異地儲存系統上。 雲端快照在災害復原案例中特別有用。

* tooexpand hello 節點中，按一下 hello 箭號圖示下一步太**雲端快照**。
* toosee 功能表可用的動作，以滑鼠右鍵按一下 hello**雲端快照**節點或以滑鼠右鍵按一下任何出現在 hello 的 hello 節點展開檢視。
* toosee 一份雲端快照集，按一下**雲端快照**在 hello**範圍**窗格。 hello 快照清單會連同每個快照集的相關資訊會出現在 hello**結果**窗格。

### <a name="jobs-node"></a>作業節點
hello**作業**節點，包含已排程、 執行中和最近完成的備份工作的相關資訊。 

* tooexpand hello 節點中，按一下 hello 箭號圖示下一步太**作業**。
* toosee 功能表可用的動作，以滑鼠右鍵按一下 hello**作業**節點或以滑鼠右鍵按一下任何出現在 hello 的 hello 節點展開檢視。
* toosee 一份排程工作中，展開 hello**作業**節點，然後再按一下**排程**。 hello 先前設定的作業和每個工作的相關資訊的清單會出現在 hello**結果**窗格。 
* toosee 最近完成的工作清單展開 hello**作業**節點，然後再按一下**過去 24 小時**。 過去 24 小時 hello 中已完成的工作清單會出現在 hello**結果**窗格。 hello**結果**窗格也包含每個已完成工作的相關資訊。
* toosee 的目前執行的工作清單展開 hello**作業**節點，然後再按一下**執行**。 hello 清單目前正在執行工作和每個工作的相關資訊會出現在 hello**結果**窗格。

## <a name="results-pane"></a>結果窗格
hello**結果**hello StorSimple Snapshot Manager UI 中的 hello 中心窗格。 它包含清單和詳細的狀態資訊在 hello 中選取的 hello 節點**範圍**窗格。

### <a name="example"></a>範例
toosee hello 遵循範例中，按一下 hello**磁碟區群組**節點 hello**範圍**窗格。 hello**結果** 窗格會顯示每個群組的相關詳細資料的磁碟區群組的清單。

![結果窗格](./media/storsimple-use-snapshot-manager/HCS_SSM_Results_pane.png) 

您可以設定 hello 詳細資料顯示 hello**結果**窗格： hello 中的節點上按一下滑鼠右鍵**範圍** 窗格中，按一下**檢視**，然後按一下**新增/移除資料行**。

## <a name="actions-pane"></a>動作窗格
hello**動作**hello hello StorSimple Snapshot Manager UI 中的右窗格。 它包含您可以在 hello 節點、 檢視表或您在 hello 中選取的資料執行的操作功能表**範圍**窗格或**結果**窗格。 hello**動作**窗格包含相同的命令為 hello hello**動作**功能表可供 hello 中的項目**範圍**窗格和**結果**窗格。 如需每個動作的說明，請參閱 hello 中的 hello 資料表**動作**功能表區段。

### <a name="examples"></a>範例
下列範例中的，在 hello toosee hello**範圍** 窗格中，展開 hello**作業**節點，然後按一下**排程**。 hello**動作** 窗格會顯示 hello hello 可用動作**排程**節點。

![動作窗格的已排程作業範例](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane.png) 

toosee 其他選項，在 hello**範圍** 窗格中，展開 hello**作業** 節點，按一下 **排程**，然後按一下排定的工作在 hello**結果**窗格。 hello**動作**hello 下列範例所示，窗格會顯示 hello 的 hello 排程工作，可用的動作。

![動作窗格的作業動作範例](./media/storsimple-use-snapshot-manager/HCS_SSM_ActionsPane_Results.png)

## <a name="keyboard-navigation-and-shortcuts"></a>鍵盤瀏覽和快速鍵
StorSimple Snapshot Manager 可讓 hello hello Windows 作業系統與 hello Microsoft Management Console (MMC) 的協助工具功能。 它也包含一些鍵盤導覽功能和特定 toohello StorSimple Snapshot Manager，快速鍵 hello 下列各節中所述。

* [鍵盤導覽鍵](#keyboard-navigation-keys) 
* [功能表列快速鍵](#menu-bar-shortcut-keys) 
* [範圍窗格快速鍵](#scope-pane-shortcut-keys) 

### <a name="keyboard-navigation-keys"></a>鍵盤導覽鍵
hello 下表描述您可以使用 toonavigate hello StorSimple Snapshot Manager 使用者介面的 hello 索引鍵。 

| 導覽鍵 | 動作 |
|:--- |:--- |
| 向下鍵 |使用向下箭號鍵 toomove hello 垂直 toohello 功能表或窗格中的下一個項目。 |
| Enter |按下 hello Enter 鍵 toocomplete 動作，然後繼續執行 toohello 下一個步驟。 例如，您可以按下 Enter tooselect**下一步**，**確定**，或**建立**，並前往 toohello 精靈中的下一個步驟。 |
| Esc |按 hello Esc 鍵 tooclose 功能表或 toocancel 並關閉頁面。 |
| F1 |Hello 目前作用中視窗，請按 hello F1 鍵 tooview 說明主題。 |
| F5 |按 hello F5 鍵 toorefresh 節點。 |
| F6 |按下從 hello hello F6 鍵 toomove**範圍**窗格 toohello**結果**窗格。 |
| F10 |按 hello F10 鍵 toogo toohello 功能表列。 |
| 向左鍵 |使用從功能表列選項 toohello 先前選項水平左箭號鍵 toomove hello。 當您移動 toohello 先前會出現 hello 上一個項目 hello 功能表列、 hello 動作 （或內容） 上的項目功能表。 |
| 向右鍵 |接下來使用水平從一個功能表列選項 toohello hello 向右箭號鍵 toomove。 當您移動 toohello 下一步 hello 功能表列、 hello 動作 （或內容） 上的項目 hello 新項目會出現功能表。 |
| Tab 鍵 |使用 hello 主控台或 toohello 下一個選取項目或文字方塊在網頁中的 hello 索引標籤索引鍵 toomove toohello 下一步 窗格。 |
| 向上鍵 |使用向上箭號鍵 toomove hello 垂直 toohello 功能表或窗格上的一個項目。 |

### <a name="menu-bar-shortcut-keys"></a>功能表列快速鍵
hello 以下表格說明 hello 的快速鍵組合 hello 功能表列。 按 hello 攠摝坫 hello 功能表開啟後，您可以使用功能表快速鍵 (hello hello 功能表上附有底線的按鍵)。 如需 hello 功能表列的詳細資訊，請移至太[功能表列](#menu-bar)。

| 快速鍵 | 結果 | 功能表快速鍵 | 結果 |
|:--- |:--- |:--- |:--- |
| ALT+F |開啟 hello**檔案**功能表。 |N |開啟新的主控台執行個體。 |
|  |O |開啟 hello**系統管理工具**頁面。 | |
|  |S |儲存 hello StorSimple Snapshot Manager 主控台。 | |
|  |A |開啟 hello**存**頁面。 | |
|  |M |開啟 hello**新增/移除嵌入式管理單元**頁面。 | |
|  |P |開啟 hello**選項**頁面。 | |
|  |H |開啟線上說明。 | |
| ALT+A |開啟 hello**動作**功能表。 |I |開啟和關閉的 hello 匯入顯示選項。 |
|  |W |開啟新的 StorSimple Snapshot Manager 主控台。 | |
|  |F |更新 hello StorSimple Snapshot Manager 主控台。 | |
|  |L |開啟 hello**匯出清單**頁面。 | |
|  |H |開啟線上說明。 | |
| ALT+V |開啟 hello**檢視**功能表。 |A |開啟 hello**新增/移除欄位**頁面。 |
|  |U |開啟 hello**自訂檢視**頁面。 | |
| ALT+O |開啟 hello**我的最愛**功能表。 |A |開啟 hello**新增 tooFavorites**頁面。 |
|  |O |開啟 hello**組織我的最愛**頁面。 | |
| ALT+W |開啟 hello**視窗**功能表。 |N |開啟另一個 StorSimple Snapshot Manager 視窗。 |
|  |C |以重疊顯示樣式顯示所有開啟的主控台視窗。 | |
|  |T |以格線模式顯示所有開啟的主控台視窗。 | |
|  |I |排列在 hello 螢幕底部的水平列中的圖示。 | |
| ALT+H |開啟 hello**協助**功能表。 |H |開啟線上說明。 |
|  |T |開啟 Microsoft TechNet 技術中心網頁 hello。 | |
|  |A |開啟 hello**關於 Microsoft Management Console**頁面。 | |

### <a name="scope-pane-shortcut-keys"></a>範圍窗格快速鍵
hello 下列資料表顯示 hello 快顯的每個節點組合 hello**範圍**窗格。 

* [裝置節點快速鍵](#devices-node-shortcut-keys)
* [磁碟區節點快速鍵](#volumes-node-shortcut-keys)
* [磁碟區群組節點快速鍵](#volume-groups-node-shortcut-keys)
* [備份原則節點快速鍵](#backup-policies-node-shortcut-keys)
* [備份目錄節點快速鍵](#backup-catalog-node-shortcut-keys)
* [作業節點快速鍵](#jobs-node-shortcut-keys)

#### <a name="devices-node-shortcut-keys"></a>裝置節點快速鍵
| 功能表快速鍵 | 結果 |
|:--- |:--- |
| C |開啟 hello**設定裝置**頁面。 |
| D |重新整理 hello 的裝置清單以及裝置詳細資料。 |
| V |開啟 hello**檢視**功能表。 |
| W |開啟新的 StorSimple Snapshot Manager 主控台將焦點放在 hello**詳細資料**節點。 |
| F |更新 hello StorSimple Snapshot Manager 主控台。 |
| L |開啟 hello**匯出清單**頁面。 |
| H |開啟線上說明。 |

#### <a name="volumes-node-shortcut-keys"></a>磁碟區節點快速鍵
| 功能表快速鍵 | 結果 |
|:--- |:--- |
| V |更新 hello 的磁碟區清單。 |
| V (按兩次) |開啟 hello**檢視**功能表。 |
| W |開啟新的 StorSimple Snapshot Manager 主控台將焦點放在 hello**磁碟區**節點。 |
| F |更新 hello StorSimple Snapshot Manager 主控台。 |
| L |開啟 hello**匯出清單**頁面。 |
| H |開啟線上說明。 |

#### <a name="volume-groups-node-shortcut-keys"></a>磁碟區群組節點快速鍵
| 功能表快速鍵 | 結果 |
|:--- |:--- |
| G |開啟 hello**建立磁碟區群組**頁面。 |
| V |開啟 hello**檢視**功能表。 |
| W |開啟新的 StorSimple Snapshot Manager 主控台將焦點放在 hello**磁碟區群組**節點。 |
| F |更新 hello StorSimple Snapshot Manager 主控台。 |
| L |開啟 hello**匯出清單**頁面。 |
| H |開啟線上說明。 |

#### <a name="backup-policies-node-shortcut-keys"></a>備份原則節點快速鍵
| 功能表快速鍵 | 結果 |
|:--- |:--- |
| B |開啟 hello**建立原則**頁面。 |
| V |開啟 hello**檢視**功能表。 |
| W |開啟新的 StorSimple Snapshot Manager 主控台將焦點放在 hello**磁碟區群組**節點。 |
| F |更新 hello StorSimple Snapshot Manager 主控台。 |
| L |開啟 hello * * 匯出清單 * * 頁面。 |
| H |開啟線上說明。 |

#### <a name="backup-catalog-node-shortcut-keys"></a>備份目錄節點快速鍵
| 功能表快速鍵 | 結果 |
|:--- |:--- |
| W |開啟新的 StorSimple Snapshot Manager 主控台將焦點放在 hello**磁碟區群組**節點。 |
| F |更新 hello StorSimple Snapshot Manager 主控台。 |
| H |開啟線上說明。 |

#### <a name="jobs-node-shortcut-keys"></a>作業節點快速鍵
| 功能表快速鍵 | 結果 |
|:--- |:--- |
| V |開啟 hello**檢視**功能表。 |
| W |開啟新的 StorSimple Snapshot Manager 主控台將焦點放在 hello**作業**節點。 |
| F |更新 hello StorSimple Snapshot Manager 主控台。 |
| L |開啟 hello**匯出清單**頁面。 |
| H |開啟線上說明 |

## <a name="next-steps"></a>後續步驟
* 了解如何太[使用您的 StorSimple 解決方案的 StorSimple Snapshot Manager tooadminister](storsimple-snapshot-manager-admin.md)。
* 了解如何太[使用 StorSimple Snapshot Manager tooconnect 和管理裝置](storsimple-snapshot-manager-manage-devices.md)。

