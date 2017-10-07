---
title: "aaaClean 及準備資料的 Azure Machine Learning |Microsoft 文件"
description: "前置處理和清除資料 tooprepare 它機器學習。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: bdf659ec-4881-4324-8b9c-747cbfa0c3cd
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: 3e3c3e4b0cfb9187f5820d7165e6ee1ea013ba02
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="tasks-tooprepare-data-for-enhanced-machine-learning"></a>增強的機器學習工作 tooprepare 資料
 前置處理和清除資料是很重要的工作，必須先執行這些工作，才能有效地將資料集用於機器學習服務。 未經處理的資料通常會有雜訊且不可靠，還可能會有遺漏值。 使用這類資料進行模型化可能會產生誤導的結果。 這些工作是 hello 小組資料科學程序 (TDSP) 的一部分，且通常執行初始資料集使用 toodiscover 和計劃 hello 前置處理所需的探索。 如需詳細指示 hello TDSP 程序，請參閱 hello 中所述的 hello 步驟[資料科學的小組流程](https://azure.microsoft.com/documentation/learning-paths/cortana-analytics-process/)。

前置處理和清除工作，例如 hello 資料瀏覽工作，可實行在各種不同的環境，例如 SQL 或登錄區或 Azure Machine Learning Studio，以及各種工具和語言，例如 R 或 Python，根據資料的位置儲存並格式化的方式。 由於 TDSP 反覆的本質，這些工作可能需要在 hello hello 程序工作流程中的各種步驟。

本文將介紹各種不同的資料處理概念和工作，讓您可以在將資料擷取到 Azure Machine Learning 前後執行這些工作。

如需資料探索和 Azure Machine Learning studio 內執行的前置處理的範例，請參閱 hello[前置處理 Azure Machine Learning Studio 中的資料](https://azure.microsoft.com/documentation/videos/preprocessing-data-in-azure-ml-studio/)視訊。

## <a name="why-pre-process-and-clean-data"></a>為何要前置處理和清除資料？
從各種來源收集真實世界的資料和處理程序，它可能包含審查或洩露 hello 品質 hello 資料集的資料損毀。 hello 典型的資料品質所導致的問題是：

* **不完整**：資料缺少屬性或包含遺漏值。
* **雜訊**：資料包含錯誤的記錄或極端值。
* **不一致**：資料包含衝突的記錄或不一致之處。

資料品質是品質預測模型的必要條件。 在外的記憶體回收的 tooavoid 「 垃圾 」 和改善資料品質，便會因此模型效能，它是命令式 tooconduct 資料健全狀況螢幕 toospot 資料發出早期，並決定 hello 對應資料處理和清理步驟。

## <a name="what-are-some-typical-data-health-screens-that-are-employed"></a>哪些是要採用的典型資料健康狀態畫面？
我們可以藉由檢查來檢查 hello 一般品質的資料：

* hello 數目**記錄**。
* hello 數目**屬性**(或**功能**)。
* hello 屬性**資料型別**（表面，序數，或連續）。
* hello 數目**遺漏值**。
* **語式**的 hello 資料。
  * 如果 hello 資料是 TSV 或 CSV，請檢查確認 hello 的資料行分隔符號，行分隔符號一定會正確地分隔資料行和線條。
  * 如果 hello 資料是 HTML 或 XML 格式，請檢查是否 hello 資料的正確性根據其各自的標準。
  * 剖析也可能需要半結構化或非結構化資料的順序 tooextract 結構化資訊。
* **不一致的資料記錄**。 允許的值的核取 hello 範圍。 例如如果 hello 資料包含學生 GPA，檢查是否已在 hello 指定範圍中的 hello GPA 說 0 ~ 4。

當您找到問題的資料，**處理步驟**這通常牽涉到清除遺漏值、 資料標準化、 離散化、 文字處理 tooremove 必要和/或取代這可能會影響內嵌的字元資料對齊混合的資料類型在一般欄位，以及其他項目。

**Azure Machine Learning 會取用正確格式的表格式資料**。  Hello 資料便已經在表格式表單中，如果資料前置處理可以直接與 Azure Machine Learning hello Machine Learning Studio 中執行。  如果資料不是在表格式表單中，可能需要的說，它是在 XML 中，剖析 tooconvert hello 資料 tootabular 在表單中。  

## <a name="what-are-some-of-hello-major-tasks-in-data-pre-processing"></a>有哪些資料前置處理中的 hello 主要工作？
* **資料清除**：填入值或遺漏值，偵測並移除雜訊資料和極端值。
* **資料轉換**： 標準化資料 tooreduce 維度與雜訊。
* **資料縮減**：取樣資料記錄或屬性，以進行較簡單的資料處理。
* **資料離散化**： 轉換連續屬性以方便使用的 toocategorical 屬性與特定的機器學習方法。
* **文字清除**：移除可能造成資料對齊錯誤的內嵌字元，例如，定位鍵分隔的資料檔中的內嵌定位鍵、可能中斷記錄的內嵌新行等。

hello 的以下各節詳細說明部分這些資料處理步驟。

## <a name="how-toodeal-with-missing-values"></a>如何使用遺漏的 toodeal 值嗎？
toodeal 有遺漏值，建議您最好 toofirst 辨認 hello 原因 hello 遺漏值 toobetter 控制代碼 hello 問題。 典型的遺漏值處理方法如下：

* **刪除**：移除具有遺漏值的記錄。
* **虛擬替代**：使用虛擬值來取代遺漏值，例如，對類別值使用 *unknown* ，或對數值使用 0。
* **表示替代**： 如果 hello 遺失的資料是數值，平均值來取代遺漏值的 hello hello。
* **常見的替代**： 如果 hello 遺漏資料類別，則將 hello 遺漏值取代 hello 最常出現的項目
* **迴歸替代**： 使用迴歸方法 tooreplace 遺漏值與迴歸值。  

## <a name="how-toonormalize-data"></a>如何 toonormalize 資料嗎？
資料正規化重新調整數值 tooa 指定範圍。 常用的資料正規化方法包括：

* **Min-max 正規化**： 線性轉換 hello 資料 tooa 範圍，請說出介於 0 和 1，其中 hello 最小值是縮放的 too0 和最大值 too1。
* **Z-score 正規化**： 調整資料是根據平均和標準差： hello hello 資料與 hello 平均值之間的差異除以 hello 標準差。
* **十進位調整**: hello 屬性值的移動 hello 小數點縮放 hello 資料。  

## <a name="how-toodiscretize-data"></a>如何 toodiscretize 資料嗎？
轉換連續值 toonominal 屬性或間隔可以離散化資料。 以下提供一些執行此動作的方法：

* **相等寬度分類收納**: hello 範圍的所有可能值的屬性分成的 hello 相同大小及指派 hello 的值落在 bin hello 分類收納數字的 N 個群組。
* **相同的高度分類收納**： 分割 hello 範圍的屬性 N 分組的所有可能的值，每個都包含 hello 相同數目的執行個體，然後指派 hello 值落在 hello 的分類收納中分類收納數字。  

## <a name="how-tooreduce-data"></a>如何 tooreduce 資料嗎？
有各種方法 tooreduce 資料更容易處理的資料大小。 根據資料大小和 hello 網域，您可以套用 hello 下列方法：

* **記錄取樣**： 範例 hello 資料記錄，並只從 hello 資料選擇 hello 代表性。
* **屬性取樣**: hello 資料從選取的 hello 最重要的屬性子集。  
* **彙總**: hello 資料分成群組，並儲存每個群組的 hello 數字。 例如，hello 每日的營收數字的餐廳鏈結透過 hello 過去 20 年可以是彙總 toomonthly 營收 tooreduce hello hello 資料大小。  

## <a name="how-tooclean-text-data"></a>如何 tooclean 文字資料嗎？
**表格式資料中的文字欄位** 可能包含影響資料行對齊和 (或) 記錄界限的字元。 例如，定位鍵分隔檔案的內嵌定位鍵可能導致資料行對齊錯誤，而內嵌的新行字元會中斷記錄行。 不正確的文字編碼方式寫入/讀取文字時的處理會導致 tooinformation 遺失、 意外引進的無法讀取的字元，例如，設為 null，並可能也會影響文字剖析。 可能需要仔細剖析和編輯為適當對齊和/或 tooextract 結構化資料與非結構化或半結構化文字資料的順序 tooclean 文字欄位中。

**資料瀏覽**提供早期 hello 資料檢視。 在此步驟中，大量資料問題，可以是未涵蓋範圍和對應的方法可以是套用的 tooaddress 這些問題。  它是什麼是 hello hello 問題來源，以及如何 hello 問題可能已引進的重要 tooask 問題。 這也可協助您決定採取 tooresolve 該需要 toobe hello 資料處理步驟它們。 hello 種類型的其中一個打算 tooderive hello 資料也可以使用的 tooprioritize hello 資料處理工作的深入資訊。

## <a name="references"></a>參考
> *Data Mining: Concepts and Techniques*(資料採礦：觀念與技術)，第三版，Morgan Kaufmann，2011，Jiawei Han、Micheline Kamber 及 Jian Pei
> 
> 

