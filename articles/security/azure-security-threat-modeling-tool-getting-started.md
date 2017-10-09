---
title: "已啟動-Microsoft 威脅模型化工具-Azure aaaGetting |Microsoft 文件"
description: "這是反白顯示 hello 威脅模型化工具中動作的深入概觀。"
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
ms.openlocfilehash: 75ef139071e8abd0e743aa17b443a6e353f29372
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-hello-threat-modeling-tool"></a>Hello 威脅模型化工具使用者入門

hello 雲端和企業的安全性工具小組今年 hello 威脅模型化工具預覽為可用**[按一下若要下載](https://aka.ms/tmtpreview)**。 hello 變更傳遞機制可讓我們 toopush hello 最新改良功能和 bug 修正 toocustomers 每次開啟 hello 工具，讓您更輕鬆 toomaintain 和使用。
這篇文章會引導您完成 hello 的入門 hello Microsoft SDL 威脅模型化方法的程序，並顯示為您的安全性程序的骨幹 toouse hello 工具 toodevelop 絕佳威脅模型的方式。

這篇文章是根據現有知識的 hello SDL 威脅模型化方法。 如需快速檢閱，請參閱太**[威脅模型化的 Web 應用程式](https://msdn.microsoft.com/library/ms978516.aspx)**和封存的新版**[發現安全性缺陷使用 hello STRIDE 方法](https://docs.google.com/viewer?a=v&pid=sites&srcid=ZGVmYXVsdGRvbWFpbnxzZWN1cmVwcm9ncmFtbWluZ3xneDo0MTY1MmM0ZDI0ZjQ4ZDMy)** 2006年中發佈的 MSDN 文件。

tooquickly 摘述，hello 種方法牽涉到建立圖表、 識別潛在威脅、 減輕這些及驗證每個防護。 以下反白顯示此程序的圖表：

![SDL 程序](./media/azure-security-threat-modeling-tool/sdlapproach.png)

## <a name="starting-hello-threat-modeling-process"></a>啟動 hello 威脅模型程序

當您啟動 hello 威脅模型化工具時，您會發現一些事情，hello 圖片所示：

![空白起始分頁](./media/azure-security-threat-modeling-tool/tmtstart.png)

### <a name="threat-model-section"></a>威脅模型區段

| 元件                                   | 詳細資料                                                                                                                                                                                                                                                                                                                                                                                                                                                                                       |
| ------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **意見反應、建議和問題按鈕** | 會採用您 hello  **[MSDN 論壇](https://social.msdn.microsoft.com/Forums/en-US/home?forum=sdlprocess)** SDL 中的所有物件。 它可讓您有機會 tooread，透過其他使用者所做什麼，以及因應措施和建議。 如果您仍然找不到您要尋找，電子郵件傳送tmtextsupport@microsoft.com針對我們的支援團隊 toohelp 您                                                                                                                            |
| **建立模型**                          | 開啟空白的畫布您 toodraw 的圖表。 請確定 tooselect 哪一個範本適用於您機型希望 toouse                                                                                                                                                                                                                                                                                                                                                                       |
| **新模型的範本**                 | 您必須選取哪一個範本 toouse 才能建立模型。 我們的主要範本為 hello Azure 威脅模型範本，其中包含 Azure 特有的樣板、 威脅與降低。 一般模型，請從 hello 下拉式選單選取 hello SDL TM 知識庫。 想 toocreate 您自己的範本，或送出用於所有使用者的新帳戶嗎？ 請查看我們**[範本儲存機制](https://github.com/Microsoft/threat-modeling-templates)**更多的 GitHub 頁面 toolearn                              |
| **開啟模型**                            | <p>會開啟先前儲存的威脅模型。 hello 最近開啟的模型功能是很好，如果您需要 tooopen 最新的檔案。 當您將滑鼠停留在 hello 選取項目時，您會發現 2 方式 tooopen 模型：</p><p><ul><li>從這部電腦開啓 – 使用本機儲存體開啟檔案的傳統方法</li><li>開啟從 OneDrive – 小組可以使用 OneDrive toosave 中的資料夾，並共用其所有的威脅模型中的單一位置 toohelp 提高產能和共同作業</li></ul></p> |
| **使用者入門指南**                   | 開啟 hello  **[Microsoft 威脅模型化工具](./azure-security-threat-modeling-tool.md)**主頁面                                                                                                                                                                                                                                                                                                                                                                                            |

### <a name="template-section"></a>範本區段

| 元件               | 詳細資料                                                                                                                                                          |
| ----------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| **建立新的範本** | 會開啟您 toobuild 的空白範本。 除非您有建立範本，從可用的廣泛知識，我們建議您從現有的項目 toobuild |
| **開啟範本**       | 開啟過您 toomake 變更現有範本                                                                                                             |

hello 威脅模型化工具小組經常處理 tooimprove 工具功能和體驗。 一些微幅變更可能會接管 hello 課程 hello 年中的位置，但所有的重大變更要求 hello 指南中的撰寫。 請參閱 tooit 通常 tooensure 取得最新的 hello 公告。

## <a name="building-a-model"></a>建置模型

在本節中，我們會跟隨：

- Cristina (開發人員)
- Ricardo (程式經理) 和
- Ashish (測試人員)

它們會透過開發其第一個威脅模型的 hello 程序。

> Ricardo: Hi Cristina，我 hello 威脅模型圖表上運作正常，而且想 toomake 確定我們答對 hello 詳細資料。 您可以協助查看嗎？
> Cristina：當然。 讓我看看。
> Ricardo hello 工具隨即開啟，並共用 Cristina 他螢幕。

![基本威脅模型](./media/azure-security-threat-modeling-tool/basictmt.png)

> Cristina：好的，看起來直接明瞭，但是可以為我逐步示範嗎？
> Ricardo：當然！ 以下是 hello 分解：
> - 我們的人類使用者是繪製為外部實體 — 正方形
> - 它們傳送命令 tooour 網頁伺服器 — hello 圓形
> - hello Web 伺服器已判定資料庫 （兩個平行的行）

Ricardo 剛剛為 Cristina 顯示的是 DFD，**[資料流程圖表](https://en.wikipedia.org/wiki/Data_flow_diagram)**的簡稱。 hello 威脅模型化工具可讓使用者 toospecify 信任界限 hello 紅色虛線的 tooshow 不同實體所在控制項中所指定。 例如，IT 系統管理員需要有 Active Directory 系統進行驗證目的，因此 hello Active Directory 會在其控制項之外。

> 看起來正確 toome Cristina:。 Hello 威脅呢？
> Ricardo：我來示範給您看。

## <a name="analyzing-threats"></a>分析威脅

一旦使用者按一下 hello 圖示功能表選取項目 （檔案與放大鏡），他會採取依據 hello 預設範本，產生的潛在威脅 hello 找到的威脅模型化工具 tooa 清單使用 hello SDL 方法稱為 hello 分析檢視 **[STRIDE （詐騙、 竄改、 資訊洩漏、 阻絕服務以及提高權限）](https://en.wikipedia.org/wiki/STRIDE_(security))**。 hello 概念是軟體是在可預測您可以使用這些 6 的類別目錄找到的威脅下。

這種方式就像就地保護您的房子確保每個媒體櫃門，以及視窗具有的鎖定機制新增警報系統或追趕之後 hello 竊賊之前一樣。

![基本威脅](./media/azure-security-threat-modeling-tool/basicthreats.png)

Ricardo 一開始會選取 hello hello 清單上的第一個項目。 排程狀況如下：

首先，已增強 hello hello 兩個樣板之間的互動

![互動](./media/azure-security-threat-modeling-tool/interaction.png)

Hello 威脅的第二個、 其他資訊隨即顯示在 hello 威脅屬性 視窗

![互動資訊](./media/azure-security-threat-modeling-tool/interactioninfo.png)

產生的 hello 威脅可幫助他了解可能的設計有缺陷。 hello STRIDE 分類可讓他了解上潛在的攻擊誘因，同時 hello 詳細描述，告訴他到底是什麼有錯誤，以及潛在方式 toomitigate 它。 他可以使用可編輯的欄位 toowrite 備忘稿 hello 理由的詳細資料，或變更優先順序分級，根據其組織的 bug 列。

Azure 範本具有其他詳細資料 toohelp 使用者了解不僅什麼是錯誤的但也如何 toofix 它藉由新增描述、 範例和超連結 tooAzure 特定文件。

hello 描述做，他了解 hello 重要性的驗證機制 tooprevent 將使用者新增從詐騙，以免洩露 hello 第一個威脅 toobe 處理。 幾分鐘的時間與 Cristina，hello 討論到他們了解 hello 重要性的實作存取控制和角色。 確定這些實作了一些快速重點 toomake Ricardo 填入。

Ricardo 進入 hello 下資訊洩漏的威脅，因為他實現 hello 存取控制計劃所需的稽核和產生報表的部分唯讀狀態的帳戶。 他想要知道是否這應該是新的威脅，但 hello 防護功能已 hello 相同，所以他附 hello 威脅。
他也思考資訊洩漏的位元更，實現 hello 備份磁帶當初 tooneed 加密，hello 作業小組的工作。

不適用 toohello 到期 tooexisting 防護或安全性的設計可保證可以變更太威脅 「 不適用 」 從 hello 狀態的下拉式清單。 有其他三個選擇： 未啟動 – 預設選項，需要調查 – 用盡 toofollow 項目和降低 – 一旦完全處理。

## <a name="reports--sharing"></a>報告與共用

一旦 Ricardo 經歷 Cristina hello 清單，並新增重要注意事項，只要有防護 /、 優先順序和狀態變更時，他選取報表]-> [的建立完整的報表]-> [儲存報告，很棒的列印報告他 toogo 透過使用實作同事 tooensure hello 適當的安全性工作。

![互動資訊](./media/azure-security-threat-modeling-tool/report.png)

如果 Ricardo 改用想 tooshare hello 檔案，他可以輕鬆地進行儲存其組織的 OneDrive 帳戶中。 一旦執行動作，，他可以複製 hello 文件連結，並與同事共用。 

## <a name="threat-modeling-meetings"></a>威脅模型化會議

當 Ricardo 傳送他使用 OneDrive、 愛希斯 hello 軟體測試人員的威脅模型 toohis 同事時，已 underwhelmed。 Ricardo 和 Cristina 似乎遺漏一些重要的極端案例，這些案例很容易遭到入侵。 他態度為補數 toothreat 模型。

在此案例中，愛希斯花費 hello 威脅模型，透過後他呼叫兩個威脅模型會議： 一個會議 toosynchronize hello 程序和逐步 hello 圖表，然後第二個會議威脅檢閱和登出。

在第一個會議 hello，愛希斯花在查核 everyone 透過 hello SDL 威脅模型程序的 10 分鐘。 然後，他會提取向上 hello 威脅模型圖表並啟動說明詳細。 五分鐘內就識別重要的遺漏元件。

幾分鐘的時間以後，愛希斯和 Ricardo 進入 hello Web 伺服器的建置方式的擴充討論。 未 hello 的會議 tooproceed，最理想的方式，但是 everyone 最終同意早期探索 hello 差異當時正在的 toosave 它們 hello 未來時間。

在 hello 第二個會議，逐步進行 hello 威脅作業 hello 小組討論，以及簽署某些方式 tooaddress 關閉 hello 威脅模型。 這些簽入原始檔控制的 hello 文件，並繼續進行開發。

## <a name="thinking-about-assets"></a>思考資產

某些有威脅模型化的讀者可能會注意到，我們完全未討論到資產。 我們發現了許多軟體工程師，比他們了解 hello 概念的資產的資產，攻擊者可能會想要更進一步了解他們軟體。

如果您打算 toothreat 一棟房子的模型，您可能一開始會考慮您的家族、 無法取代的相片或重要的圖檔。 可能是您可能一開始會考慮人員可能會中斷與 hello 目前的安全性系統。 或者，您可能一開始會考慮 hello 實體的功能，例如 hello 集區或 hello 前端看。 這些是類似 toothinking 資產、 攻擊者或軟體設計相關。 三種方法的任何一個都有作用。

我們在此處提供的 hello 方法 toothreat 模型化作業會比 Microsoft 已在過去的 hello 簡單多了。 我們發現 hello 軟體設計方法適用於許多小組。 我們希望這也包括您。

## <a name="next-steps"></a>後續步驟

傳送您的問題、 意見與想法tootmtextsupport@microsoft.com。**[下載](https://aka.ms/tmtpreview)** hello 威脅模型化工具 tooget 啟動。
