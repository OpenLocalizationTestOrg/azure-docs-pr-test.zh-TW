---
title: "aaaMicrosoft 威脅模型化工具-Azure |Microsoft 文件"
description: "深入了解 hello 威脅模型化工具中可用的所有 hello 功能"
services: security
documentationcenter: na
author: RodSan
manager: RodSan
editor: RodSan
ms.assetid: na
ms.service: security
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: rodsan
ms.openlocfilehash: f9ad5e623e7758063084cb7fc723c5735161a846
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="threat-modeling-tool-feature-overview"></a>威脅模型化工具功能概觀

我們很高興您威脅分析模型的需求選擇 toouse hello 威脅模型化工具 ！ 如果您尚未這麼做，請瀏覽 **[hello 威脅模型化工具使用者入門](./azure-security-threat-modeling-tool-getting-started.md)** toolearn hello 基本概念。

> 我們的工具會經常更新，因此請查看這引導通常 toosee 我們最新功能和增強功能。

按一下 hello 「 建立新模型 」 按鈕會開啟空白起始頁下, 面類似的 toohello 影像：

![空白起始分頁](./media/azure-security-threat-modeling-tool/tmtstart.png)

使用 hello 威脅模型由我們的團隊在 hello **[入門](./azure-security-threat-modeling-tool-getting-started.md)**範例中，讓我們今天簽出 hello 工具中可用的所有 hello 功能。

![基本威脅模型](./media/azure-security-threat-modeling-tool/basictmt.png)

## <a name="navigation"></a>導覽

一頭栽進 hello 內建功能，再看一下 hello hello 工具中找到的主要元件

### <a name="menu-items"></a>功能表項目

hello 體驗應該類似 tooother Microsoft 產品。 讓我們先經過 hello 最上層功能表項目：

![功能表項目](./media/azure-security-threat-modeling-tool/menuitems.png)

| 標籤                               | 詳細資料      |
| --------------------------------------- | ------------ |
| **檔案** | <ul><li>開啟、儲存並關閉檔案</li><li>登入/登出 OneDrive 帳戶</li><li>共用連結 (檢視 + 編輯)</li><li>檢視檔案資訊</li><li>套用新的範本 tooExisting 模型</li></ul> |
| **編輯** | 復原/重做動作，以及複製、貼上和刪除 |
| **檢視** | <ul><li>在**分析**和**設計**檢視之間切換</li><li>開啟已關閉的視窗 (例如，樣板、元素屬性和訊息)</li><li>重設配置 toodefault 設定</li></ul> |
| **圖表** | 新增/刪除圖表並且瀏覽圖表的「索引標籤」 |
| **報告** | 與其他人建立 HTML 報表 tooshare |
| **說明** | 引導您使用 hello 工具 toohelp |

hello 圖示是捷徑 hello 的最上層功能表：

| 圖示                               | 詳細資料      |
| --------------------------------------- | ------------ |
| **開啟** | 開啟新的檔案 |
| **儲存** | 儲存目前的檔案 |
| **設計** | 便會進入設計檢視，您可以在其中建立模型 |
| **分析** | 顯示產生的威脅和其屬性 |
| **新增圖表** | 加入新的圖表 （類似 toonew 索引標籤在 Excel 中） |
| **刪除圖表** | 刪除目前的圖表 |
| **複製/剪下/貼上** | 複製/剪下/貼上元素 |
| **復原/重做** | 復原/重做動作 |
| **放大/縮小** | 拉出 hello 圖表更好的檢視 |
| **意見反應** | 開啟 hello MSDN 論壇 |

### <a name="canvas"></a>畫布

hello 空間其中您拖放到的項目。 拖放是最快的 hello 和最有效率的方式 toobuild 模型。 您也可以以滑鼠右鍵按一下，並選取從 hello 功能表中，這會將泛型版本的 hello 項目使用，如下所示。

#### <a name="dropping-hello-stencil-on-hello-canvas"></a>Hello 畫布上的卸除 hello 樣板

![畫布置放](./media/azure-security-threat-modeling-tool/canvasdrop1.png)

#### <a name="clicking-on-hello-stencil"></a>按一下 hello 樣板

![元素屬性](./media/azure-security-threat-modeling-tool/canvasdrop2.png)

### <a name="stencils"></a>樣板

您可以找到其中所有樣板可用 toouse hello 選取的範本為基礎。 如果找不到 hello 右項目，請嘗試使用其他範本，或修改一個 toofit 您的需求。 一般而言，您應該要能夠 toofind 像 hello 的以下類別的組合：

| 樣板名稱                               | 詳細資料      |
| --------------------------------------- | ------------ |
| **處理程序** | 應用程式、瀏覽器外掛程式、執行緒、虛擬機器 |
| **外部互動者** | 驗證提供者、瀏覽器、使用者、Web 應用程式 |
| **資料存放區** | 快取、儲存體、設定檔、資料庫、登錄 |
| **資料流程** | 二進位、ALPC、HTTP、HTTPS/TLS/SSL、IOCTL、IPSec、具名管道、DCOM、SMB、UDP |
| **信任線條/框線界限** | 公司網路、網際網路、機器、沙箱、使用者/核心模式 |

### <a name="notesmessages"></a>附註/訊息

| 元件                               | 詳細資料      |
| --------------------------------------- | ------------ |
| **訊息** | 每當發生錯誤時 (例如元素之間沒有資料流程) 警示使用者的內部工具邏輯 |
| **注意事項** | 手動加入的 toohello 檔案由工程小組整個 hello 設計，並檢閱程序 |

### <a name="element-properties"></a>元素屬性

這些會因選取的 hello 項目。 除了信任界限，其他所有元素會包含 3 個一般選取項目：

| 元素屬性                               | 詳細資料      |
| --------------------------------------- | ------------ |
| **名稱** | 適用於命名易於辨識您的處理序、 儲存、 互動及流量 toobe |
| **超出範圍** | 如果選取，hello 項目是取自 hello 威脅產生矩陣 （不建議） |
| **超出範圍原因** | 對齊欄位 toolet 使用者知道為什麼不在範圍已選取 |

每個元素類別下的屬性都會變更。 按一下每個項目 tooinspect hello 可用的選項，或開啟多個 hello 範本 toolearn。 讓我們先進入 hello 功能。

## <a name="welcome-screen"></a>歡迎使用畫面

hello 歡迎畫面 是當您開啟 hello 應用程式時，您會看到 hello 第一件事。

### <a name="open-a-model"></a>開啟模型

將游標移到 [開啟模型] 按鈕會為您顯示 2 個隱藏選項：[從這部電腦開啟] 和 [從 OneDrive 開啟]。 hello 第一次開啟 hello 開啟舊檔 畫面上，雖然 hello 第二個會引導您完成 hello 登入程序為 OneDrive，可讓您 toopick 資料夾和檔案成功驗證之後。

![開啟模型](./media/azure-security-threat-modeling-tool/openmodel.png)

![從電腦或 OneDrive 開啟](./media/azure-security-threat-modeling-tool/openmodel2.png)

### <a name="feedback-suggestions-and-issues"></a>意見反應、建議和問題

選取此選項會帶您 toohello MSDN 論壇 SDL 工具。 它是很好的方法 toocheck 出看其他人對 hello 工具，包括因應措施和新的想法。

![意見反應](./media/azure-security-threat-modeling-tool/feedback.png)

## <a name="design-view"></a>設計檢視

每當您開啟或建立新的模型，您將會進入 toohello [設計] 檢視。

### <a name="adding-elements"></a>新增元素

有 2 種 tooadd 項目在 hello 方格上：

- **將拖放**– 拖曳 hello 所需的項目 toohello 方格中，然後使用 hello 項目屬性 tooprovide 其他資訊。
- **以滑鼠右鍵按一下**– hello 方格上以滑鼠右鍵按一下任何位置，然後從 hello 下拉式功能表中選取。 泛型的表示法，該元素會出現在囉 」 畫面。

### <a name="connecting-elements"></a>連線元素

有 2 種方式 tooconnect 項目在 hello 工具：

- **將拖放**– 拖曳 hello 所需的資料流程 toohello 方格中，並連接這兩個 ends toohello 適當的項目。
- **按一下 + 移位**– 按一下 hello （傳送資料） 的第一個項目，請按住 hello Shift 鍵，然後選取 hello （接收資料） 的第二個元素。 按一下滑鼠右鍵，然後選取 [連接]。 如果您使用雙向資料流程，hello 順序並不重要。

### <a name="properties"></a>屬性

顯示所有可修改的 hello 屬性放在 hello 圖表中的 hello 樣板上。 hello 樣板，只要按一下 toosee hello 屬性，並將據此擴展 hello 資訊。 hello 下面範例會顯示之前和之後樣板拖曳 hello 圖表 「 資料庫 」:

#### <a name="before"></a>先前

![先前](./media/azure-security-threat-modeling-tool/properties1.png)

#### <a name="after"></a>後續

![後續](./media/azure-security-threat-modeling-tool/properties2.png)

### <a name="messages"></a>訊息

如果您建立的威脅模型，忘記 tooconnect 資料流程 tooelements hello 訊息視窗會通知您 tooact。 您可以選擇 tooignore，它或後續 hello 指示 toofix hello 問題。 

![訊息](./media/azure-security-threat-modeling-tool/messages.png)

### <a name="notes"></a>注意事項

切換索引標籤，從訊息 tooNotes 可讓您 tooadd 備忘稿 tooyour 圖表 toocapture 您的想法

## <a name="analysis-view"></a>分析檢視

一旦您完成建置您的圖表，tooanalysis 檢視切換移 toohello 上方功能表選取項目，然後選擇 hello 放大鏡下一步 toohello 小畫家調色盤。

![分析檢視](./media/azure-security-threat-modeling-tool/analysisview.png)

### <a name="generated-threat-selection"></a>產生的威脅選取項目

當您按一下威脅時，您可以利用三個唯一的函式：

| 功能                               | 資訊      |
| --------------------------------------- | ------------ |
| **讀取指標** | <p>威脅現在標示成已閱讀，輕鬆地可協助您追蹤您已經瀏覽的 hello 項目</p><p>![讀取/未讀取指標](./media/azure-security-threat-modeling-tool/readmode.png)</p> |
| **互動焦點** | <p>在屬於 toothat 威脅的 hello 圖表互動會反白顯示</p><p>![互動焦點](./media/azure-security-threat-modeling-tool/interactionfocus.png)</p> |
| **威脅屬性** | <p>Hello 威脅屬性 視窗中已填入 hello 威脅的其他資訊</p><p>![威脅屬性](./media/azure-security-threat-modeling-tool/threatproperties.png)</p> |

### <a name="priority-change"></a>優先順序變更

變更每個產生的威脅的 hello 優先權層級也會變更其色彩 toomake 它輕鬆 tooidentify 高、 中度與低優先權的威脅。

![優先順序變更](./media/azure-security-threat-modeling-tool/prioritychange.png)

### <a name="threat-properties-editable-fields"></a>威脅屬性可編輯欄位

如同上面的 hello 影像，使用者可以變更 hello 工具所產生的 hello 資訊也會加入資訊 toocertain 欄位，例如對齊。 這些欄位所產生 hello 範本，因此如果您需要每個威脅的詳細資訊，您已經鼓勵的 toomake 修改。

![威脅屬性](./media/azure-security-threat-modeling-tool/threatproperties.png)

## <a name="reports"></a>報告

一旦您完成時變更的優先順序，且每個更新 hello 狀態產生威脅，您可以儲存 hello 檔案及/或列印報表移過 「 報告 」，然後再 「 建立完整報告。 」 系統會詢問 tooname hello 報表，一旦您這樣做，您應該會看到類似下面的 toohello 影像：

![報告](./media/azure-security-threat-modeling-tool/report.png)

## <a name="next-steps"></a>後續步驟

toocontribute hello 社群的範本，請移 tooour  **[GitHub](https://github.com/Microsoft/threat-modeling-templates)** 頁面。 **[下載](https://aka.ms/tmtpreview)** hello 工具 tooget 立即開始使用。
