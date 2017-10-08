---
title: "aaaAzure 小組資料科學程序概觀 |Microsoft 文件"
description: "提供資料科學方法 toodeliver 預測分析解決方案和智慧型應用程式。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: b1f677bb-eef5-4acb-9b3b-8a5819fb0e78
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2017
ms.author: bradsev;
ms.openlocfilehash: 2ba03585a6f6f855faaa3b5c0c75149cad0a88bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="team-data-science-process-overview"></a>Team Data Science Process 概觀

hello 小組資料科學程序 (TDSP) 會是 agile 反覆資料科學方法 toodeliver 預測性分析方案和智慧型應用程式有效。 TDSP 有助於改善團隊共同作業和學習。 它包含 hello 最佳作法和結構的 Microsoft 和其他 hello 產業中，以便資料科學開發案的 hello 成功實作提煉過程中若是。 hello 目標是 toohelp 公司完全了解的分析程式的 hello 優點。

本文提供 TDSP 和其主要元件的概觀。 我們可以實作的 hello 程序的一般描述提供各種工具。 其他連結的主題提供的 hello 專案工作和角色 hello hello 程序生命週期中所涉及的更詳細的描述。 指引也提供 tooimplement hello TDSP 使用一組特定的 Microsoft 工具與基礎結構，我們會在我們的團隊使用 tooimplement hello TDSP 的方式。

## <a name="key-components-of-hello-tdsp"></a>Hello TDSP 的重要元件

TDSP 共有的 hello 下列主要元件：

- **資料科學生命週期**定義
- **標準化專案結構**
- 資料科學專案的**基礎結構和資源**
- 專案執行的**工具和公用程式**


## <a name="data-science-lifecycle"></a>資料科學生命週期

hello 小組資料科學程序 (TDSP) 提供資料科學專案的生命週期 toostructure hello 的開發。 hello 生命週期概述 hello 步驟，從開始 toofinish 專案通常會遵循在執行時。

如果您使用另一個資料科學生命週期，例如[CRISP-DM](https://wikipedia.org/wiki/Cross_Industry_Standard_Process_for_Data_Mining)， [KDD](https://wikipedia.org/wiki/Data_mining#Process)或您組織本身的自訂程序，您仍然可以使用以工作為基礎的 TDSP，這些開發 hello 內容中的 hello生命週期。 大致而言，這些不同的方法有許多共通點。 

此生命週期是針對在智慧型應用程式中隨附的資料科學專案所設計。 這些應用程式會部署機器學習服務或人工智慧模型來做預測性分析。 探勘資料科學專案或臨機操作分析專案也可以從使用此程序而獲益。 但是，在這種情況下的部分所述的 hello 步驟可能不需要。    

hello TDSP 生命週期包含會反覆執行的五個主要階段：

* **了解商務**
* **資料取得與認知**
* **模型化**
* **部署**
* **客戶接受度**

以下是 hello 的視覺表示法**小組資料科學程序生命週期**。 

![TDSP-Lifecycle](./media/data-science-process-overview/tdsp-lifecycle.png) 

hello 目標、 工作和文件的成品以利在 TDSP hello 生命週期的每個階段所述 hello[小組資料科學程序生命週期](data-science-process-lifecycle.md)主題。 這些工作和構件與專案角色相關聯：

- 解決方案架構師
- 專案經理
- 資料科學家
- 專案負責人 

hello 下列圖表提供 hello 工作 （以藍色） 和 （在 hello 垂直軸） 上的這些角色相關聯 （在 hello 水平軸） 的 hello 生命週期的每個階段 （以綠色） 成品的方格檢視。 

![TDSP - 角色和工作](./media/data-science-process-overview/tdsp-tasks-by-roles.png)

## <a name="standardized-project-structure"></a>標準化專案結構

具有共用的目錄結構，並使用適用於專案文件範本的所有專案，可輕鬆有關 hello 小組成員 toofind 其專案。 所有的程式碼和文件會儲存在版本控制系統，(VC) 例如 Git、 TFS 或 Subversion tooenable 小組共同作業。 追蹤工作和功能追蹤系統，例如 Jira 敏捷式軟體開發專案中的，集結，Visual Studio Team Services 可讓更接近追蹤 hello 個別功能的程式碼。 這類追蹤也可讓您小組 tooobtain 更好的成本估計值。 TDSP 建議 hello VC 版本控制、 資訊安全和共同作業上建立個別的儲存機制，每個專案。 hello 標準化 hello 組織內的所有專案有助於建置機構知識的結構。

我們 hello 資料夾結構和必要的文件標準位置中提供的範本。 此資料夾結構會組織 hello 檔案包含程式碼進行資料探索和擷取特徵，並會記錄模型反覆項目。 這些範本可讓您更容易為其他人所完成的小組成員 toounderstand 工作及新成員 tooteams tooadd。 它是簡單 tooview 和更新文件範本 markdown 格式。 重要的問題與用於每個專案 tooinsure hello 問題妥善定義，而且該交付項目符合預期的 hello 品質範本 tooprovide 檢查清單。 範例包括：

- 專案教授 toodocument hello 商務問題和 hello 專案的範圍
- 資料會報告 toodocument hello 結構和 hello 原始資料的統計資料
- 模型報表 toodocument hello 衍生功能
- 模型效能計量，例如 ROC 曲線或 MSE


![TDSP 目錄](./media/data-science-process-overview/tdsp-dir-structure.png)

hello 目錄結構可以被複製從[Github](https://github.com/Azure/Azure-TDSP-ProjectTemplate)。

## <a name="infrastructure-and-resources-for-data-science-projects"></a>資料科學專案的基礎結構和資源

TDSP 提供管理共用分析和儲存體基礎結構的建議，例如：

- 儲存資料集的雲端檔案系統、 
- 資料庫
- 巨量資料 (Hadoop 或 Spark) 叢集 
- 機器學習服務。 

hello 分析和儲存體基礎結構可以在 hello 雲端或內部部署中。 這裡儲存著原始資料集和處理後的資料集。 這個基礎架構能夠進行可重現的分析。 它也可避免重複，這可能會導致 tooinconsistencies 及不必要的基礎結構成本。 工具會提供 tooprovision hello 共用的資源、 追蹤，並允許每個小組成員 tooconnect toothose 資源安全。 讓專案成員建立一致的運算環境也是個不錯的做法。 不同的小組成員可以複寫和驗證實驗。

以下是小組處理多個專案並共用各種雲端分析基礎結構元件的範例。

![TDSP 基礎結構](./media/data-science-process-overview/tdsp-analytics-infra.png)


## <a name="tools-and-utilities-for-project-execution"></a>專案執行的工具和公用程式

在大部分的組織中引進流程是相當有挑戰性。 所提供的工具 tooimplement hello 資料科學程序和生命週期協助較低的 hello 障礙 tooand 增加其採用的 hello 一致性。 TDSP 在團隊內 TDSP toojump 開始採用提供一組初始的工具和指令碼。 這也有助於將部分 hello hello 資料科學生命週期，例如資料探索和基準模型中的常見工作自動化。 提供的個人 toocontribute 共用工具和公用程式到他們的小組共用的程式碼儲存機制，沒有正確定義的結構。 這些資源可以加以利用 hello 小組或 hello 組織內的其他專案。 TDSP 也計劃工具和公用程式 toohello 整個社群的 tooenable hello 比重。 hello TDSP 公用程式可以複製從[Github](https://github.com/Azure/Azure-TDSP-Utilities)。


## <a name="next-steps"></a>後續步驟

[小組資料科學程序： 角色和工作](https://github.com/Azure/Microsoft-TDSP/blob/master/Docs/roles-tasks.md)概述 hello 金鑰的人員角色，以及如需這個程序標準化資料科學團隊及其相關的工作。 
