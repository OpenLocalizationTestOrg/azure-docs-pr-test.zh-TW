---
title: "Azure 記錄分析 aaaTrack 變更 |Microsoft 文件"
description: "hello 變更追蹤解決方案中記錄分析可協助您識別軟體及您環境中發生的 Windows 服務變更。"
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: f8040d5d-3c89-4f0c-8520-751c00251cb7
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/11/2017
ms.author: banders
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 2bb1938caad25101e167927200ac3ef495120fe0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="track-software-changes-in-your-environment-with-hello-change-tracking-solution"></a>追蹤您的環境以 hello 變更追蹤解決方案中的軟體變更

![變更追蹤符號](./media/log-analytics-change-tracking/change-tracking-symbol.png)

這篇文章可協助您使用 hello 變更追蹤解決方案中記錄分析 tooeasily 識別您的環境中的變更。 hello 解決方案會追蹤變更 tooWindows 和 Linux 軟體、 Windows 檔案和登錄機碼、 Windows 服務，以及 Linux 精靈。 識別組態變更可協助您找出操作問題。

您安裝 hello 解決方案 tooupdate hello 類型的已安裝的代理程式。 變更 tooinstalled 軟體、 Windows 服務，以及 hello 監視伺服器上的 Linux 精靈會讀取。 然後，hello 資料處理的 hello 雲端中傳送 toohello 記錄分析服務。 邏輯是套用的 toohello 接收資料，而 hello 雲端服務會記錄 hello 資料。 使用 hello 資訊 hello 變更追蹤儀表板上，您可以輕鬆地查看 hello 伺服器基礎結構中所做的變更。

## <a name="installing-and-configuring-hello-solution"></a>安裝和設定 hello 方案
使用下列資訊 tooinstall hello 並設定 hello 方案。

* 您必須擁有[Windows](log-analytics-windows-agents.md)， [Operations Manager](log-analytics-om-agents.md)，或[Linux](log-analytics-linux-agents.md)想 toomonitor 變更每部電腦上的代理程式。
* 加入 hello 變更追蹤解決方案 tooyour OMS 工作區從 hello [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ChangeTrackingOMS?tab=Overview)。 或者，您可以加入使用中的 hello 資訊 hello 解決方案[hello 解決方案資源庫中的新增記錄分析解決方案](log-analytics-add-solutions.md)。 不需要進一步設定。

### <a name="configure-linux-files-tootrack"></a>設定 Linux 檔案 tootrack
使用下列步驟 tooconfigure 檔案 tootrack 在 Linux 電腦上的 hello。

1. 在 hello OMS 入口網站中，按一下 **設定**（hello 齒輪符號）。
2. 在 hello**設定**頁面上，按一下**資料**，然後按一下 **Linux 檔案追蹤**。
3. 在 Linux 檔案變更追蹤，輸入 hello 完整路徑，包括您想 tootrack，，然後按一下hello 的 hello 檔 hello 檔案名稱**新增**符號。 例如："/etc/*.conf"
4. 按一下 [儲存] 。  

> [!NOTE]
> Linux 檔案追蹤具有其他功能，包括目錄追蹤、透過目錄遞迴以及萬用字元追蹤。

### <a name="configure-windows-files-tootrack"></a>設定 Windows 檔案 tootrack
使用下列步驟 tooconfigure 檔案 tootrack Windows 電腦上的 hello。

1. 在 hello OMS 入口網站中，按一下 **設定**（hello 齒輪符號）。
2. 在 hello**設定**頁面上，按一下**資料**，然後按一下**Windows 檔案追蹤**。
3. 在 [Windows 檔案變更追蹤] 下輸入 hello 完整路徑，包括您想 tootrack，，然後按一下hello 的 hello 檔 hello 檔案名稱**新增**符號。 例如：C:\Program Files (x86)\Internet Explorer\iexplore.exe 或 C:\Windows\System32\drivers\etc\hosts。
4. 按一下 [儲存] 。  
   ![Windows 檔案變更追蹤](./media/log-analytics-change-tracking/windows-file-change-tracking.png)

### <a name="configure-windows-registry-keys-tootrack"></a>設定 Windows 登錄機碼 tootrack
使用下列步驟 tooconfigure 登錄機碼 tootrack Windows 電腦上的 hello。

1. 在 hello OMS 入口網站中，按一下 **設定**（hello 齒輪符號）。
2. 在 hello**設定**頁面上，按一下**資料**，然後按一下**Windows 登錄追蹤**。
3. 在 Windows 登錄變更追蹤，輸入您想 tootrack，，然後按一下hello hello 整個金鑰**新增**符號。
4. 按一下 [儲存] 。  
   ![Windows 登錄變更追蹤](./media/log-analytics-change-tracking/windows-registry-change-tracking.png)

### <a name="explanation-of-linux-file-collection-properties"></a>Linux 檔案收集屬性的說明
1. **類型**
   * **檔案** (報告檔案中繼資料 - 大小、修改日期、雜湊等)
   * **目錄** (報告目錄中繼資料 -大小、修改日期等)
2. **連結**（處理 Linux 符號連結參考 tooother 檔案或目錄）
   * **忽略**（忽略符號連結期間 recurions toonot 包含 hello 檔案/目錄參考）
   * **請遵循**（遞迴 tooalso 期間的後續 hello symlink 包含 hello 檔案/目錄參考）
   * **管理**（遵循 hello 符號連結和 alter hello 傳回內容的處理方式）

   > [!NOTE]   
   > 不建議 hello 「 管理 」 連結選項。 不支援檔案內容擷取。

3. **Recurse** （遞迴所有資料夾層級和追蹤會議 hello 路徑陳述式中的所有檔案）
4. **Sudo** (能夠存取需要 sudo 權限的檔案或目錄)

### <a name="limitations"></a>限制
hello 變更追蹤解決方案目前不支援下列項目 hello:

* Windows 檔案追蹤的資料夾 (目錄)
* Windows 檔案追蹤的遞迴
* Windows 檔案追蹤的萬用字元
* 路徑變數
* 網路檔案系統
* 檔案內容

其他限制：

* hello**最大檔案大小**資料行和值都是 hello 目前實作中未使用。
* 如果您在 hello 30 分鐘收集週期中收集超過 2500年的檔案，解決方案的效能可能會下降。
* 網路流量高時，異動記錄可能會佔用 tooa toodisplay 六小時的最大值。
* 如果在電腦關閉時，您可以修改 hello 組態，hello 電腦可能會張貼所屬 toohello 先前設定的檔案變更。

## <a name="change-tracking-data-collection-details"></a>「變更追蹤」資料收集詳細資訊
變更追蹤收集軟體清查和使用您已啟用的 hello 代理程式的 Windows 服務中繼資料。

hello 下表顯示資料收集方法，以及如何針對變更追蹤收集資料的其他詳細資料。

| 平台 | 直接代理程式 | Operations Manager 代理程式 | Linux 代理程式 | Azure 儲存體 | 是否需要 Operations Manager？ | 透過管理群組傳送的 Operations Manager 代理程式資料 | 收集頻率 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| Windows 和 Linux | &#8226; | &#8226; | &#8226; |  |  | &#8226; | 5 分鐘的時間 too50 分鐘，視 hello 變更類型而定。 Hello 下列資料表的詳細資訊，請參閱。 |


hello 下表顯示 hello hello 變更類型的資料收集頻率。

| **變更類型** | **頻率** | **代理程式****是否會傳送所找到的差異？** |
| --- | --- | --- |
| Windows 登錄 | 50 分鐘 | 否 |
| Windows 檔案 | 30 分鐘 | 是。 如果 24 小時內沒有任何變更，則會傳送快照集。 |
| Linux 檔案 | 15 分鐘 | 是。 如果 24 小時內沒有任何變更，則會傳送快照集。 |
| Windows 服務 | 30 分鐘 | 是，找到變更時，每隔 30 分鐘傳送一次。 每隔 24 小時傳送一次快照集 (不論是否有變更)。 Hello 快照集，即使傳送其中沒有任何變更。 |
| Linux 精靈 | 5 分鐘 | 是。 如果 24 小時內沒有任何變更，則會傳送快照集。 |
| Windows 軟體 | 30 分鐘 | 是，找到變更時，每隔 30 分鐘傳送一次。 每隔 24 小時傳送一次快照集 (不論是否有變更)。 Hello 快照集，即使傳送其中沒有任何變更。 |
| Linux 軟體軟體 | 5 分鐘 | 是。 如果 24 小時內沒有任何變更，則會傳送快照集。 |

### <a name="registry-key-change-tracking"></a>登錄機碼變更追蹤

記錄分析會執行監視及追蹤以 hello 變更追蹤解決方案的 Windows 登錄。 hello 用途監視變更 tooregistry 索引鍵是協力廠商程式碼和惡意程式碼可以啟用其中 toopinpoint 擴充點。 hello 下列清單顯示 hello 預設登錄機碼，追蹤由 hello 解決方案，並且每個追蹤的原因。

- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Startup
    - 監視在啟動時執行的指令碼。
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Group Policy\Scripts\Shutdown
    - 監視在關機時執行的指令碼。
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Wow6432Node\Microsoft\Windows\CurrentVersion\Run
    - 監視 hello 使用者登入時 tootheir Windows 帳戶之前載入的索引鍵。 hello 金鑰用於 64 位元電腦上執行的 32 位元程式。
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Active Setup\Installed Components
    - 監視變更 tooapplication 設定。
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\ShellEx\ContextMenuHandlers
    - 監視一般自動啟動項目，而這些項目直接連結到 Windows 檔案總管，而且通常會使用 Explorer.exe 以內含方式執行。
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Shellex\CopyHookHandlers
    - 監視一般自動啟動項目，而這些項目直接連結到 Windows 檔案總管，而且通常會使用 Explorer.exe 以內含方式執行。
- HKEY\_LOCAL\_MACHINE\Software\Classes\Directory\Background\ShellEx\ContextMenuHandlers
    - 監視一般自動啟動項目，而這些項目直接連結到 Windows 檔案總管，而且通常會使用 Explorer.exe 以內含方式執行。
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - 監視圖示覆疊處理常式註冊。
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\ShellIconOverlayIdentifiers
    - 針對在 64 位元電腦上執行的 32 位元程式，監視圖示覆疊處理常式註冊。
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Internet Explorer 之新瀏覽器協助程式物件外掛程式的監視器。 使用的 tooaccess hello 文件物件模型 (DOM) 的 hello 目前頁面和 toocontrol 導覽。
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows\CurrentVersion\Explorer\Browser Helper Objects
    - Internet Explorer 之新瀏覽器協助程式物件外掛程式的監視器。 使用的 tooaccess hello 文件物件模型 (DOM) 的 hello 目前頁面和 toocontrol 巡覽的 64 位元電腦上執行的 32 位元程式。
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Internet Explorer\Extensions
    - 監視新的 Internet Explorer 擴充功能，例如自訂工具功能表和自訂工具列按鈕。
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Internet Explorer\Extensions
    - 針對在 64 位元電腦上執行的 32 位元程式，監視新的 Internet Explorer 擴充功能，例如自訂工具功能表和自訂工具列按鈕。
- HKEY\_LOCAL\_MACHINE\Software\Microsoft\Windows NT\CurrentVersion\Drivers32
    - 監視 wavemapper、 wave1 wave2、 msacm.imaadpcm、.msadpcm、.msgsm610 和與 vidc 相關聯的 hello 32 位元驅動程式。 Hello 系統中的類似 toohello [驅動程式] 區段。INI 檔案。
- HKEY\_LOCAL\_MACHINE\Software\Wow6432Node\Microsoft\Windows NT\CurrentVersion\Drivers32
    - 監視 hello 32 位元驅動程式與相關 wavemapper、 wave1 和 wave2、 msacm.imaadpcm、.msadpcm、.msgsm610，vidc 的 64 位元電腦上執行的 32 位元程式。 Hello 系統中的類似 toohello [驅動程式] 區段。INI 檔案。
- HKEY\_LOCAL\_MACHINE\System\CurrentControlSet\Control\Session Manager\KnownDlls
    - 監視 hello 已知或常用系統 Dll; 的清單此系統可防止特洛伊木馬病毒版本系統 Dll 中卸除利用弱式應用程式目錄的權限的人員。
- HKEY\_LOCAL\_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Winlogon\Notify
    - 監視 hello 從 Winlogon，hello Windows 作業系統的 hello 互動式登入支援模型的封裝無法 tooreceive 事件通知的清單。


## <a name="use-change-tracking"></a>使用變更追蹤
安裝 hello 解決方案後，您可以使用 hello 受監視伺服器檢視變更 hello 摘要**變更追蹤**磚 hello**概觀**在 OMS 中的頁面。

![變更追蹤磚的影像](./media/log-analytics-change-tracking/change-tracking-tile.png)

您可以檢視變更 tooyour 基礎結構然後鑽研的詳細資訊 hello 下列類別：

* 軟體和 Windows 服務的組態類型所做的變更
* 軟體變更 tooapplications 和個別伺服器的更新
* 每個應用程式的軟體變更總數
* Linux 套件
* 個別伺服器的 Windows 服務變更
* Linux 精靈變更

![變更追蹤儀表板的影像](./media/log-analytics-change-tracking/change-tracking-dash01.png)

![變更追蹤儀表板的影像](./media/log-analytics-change-tracking/change-tracking-dash02.png)

### <a name="tooview-changes-for-any-change-type"></a>tooview 任何變更的變更類型
1. 在 hello**概觀**頁面上，按一下 hello**變更追蹤**磚。
2. 在 hello**變更追蹤**儀表板，檢閱 hello 其中一種 hello 變更類型刀鋒的摘要資訊，然後按一下其中一個 tooview 的詳細資訊，請參閱 hello 中的資訊**記錄搜尋**頁面。
3. 在任何 hello 記錄搜尋 頁面中，您可以按時間、 詳細的結果和您的記錄搜尋記錄來檢視結果。 您也可以篩選由 facet toonarrow hello 結果。

## <a name="next-steps"></a>後續步驟
* 使用[記錄中記錄分析搜尋](log-analytics-log-searches.md)tooview 詳細的變更追蹤資料。
