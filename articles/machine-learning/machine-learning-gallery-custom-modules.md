---
title: "aaaCortana 智慧組件庫中的自訂模組 |Microsoft 文件"
description: "探索 Cortana Intelligence Gallery 中的自訂機器學習服務模組。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 16037a84-dad0-4a8c-9874-a1d3bd551cf0
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/14/2017
ms.author: roopalik;garye
ms.openlocfilehash: e2a2d39935e6d367eb192de723fb82318d04e2be
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="discover-custom-machine-learning-modules-in-cortana-intelligence-gallery"></a>探索 Cortana Intelligence Gallery 中的自訂機器學習服務模組
[!INCLUDE [machine-learning-gallery-item-selector](../../includes/machine-learning-gallery-item-selector.md)]

## <a name="custom-modules-for-machine-learning-studio"></a>Machine Learning studio 的自訂模組
Cortana 智慧組件庫提供數個[自訂模組](https://gallery.cortanaintelligence.com/customModules)，擴充 hello Azure Machine Learning Studio 功能。 因此您可以開發更進階的預測分析解決方案，您可以將 hello 模組 toouse 匯入您實驗中。

目前，hello 組件庫會提供模組上*時間序列分析*，*關聯規則*，*叢集演算法*（除了 k-means) 和*視覺效果*，和其他 workhorse 公用程式的模組。


## <a name="discover"></a>探索
toobrowse 自訂模組[hello 組件庫中](http://gallery.cortanaintelligence.com)下**詳細**，選取**自訂模組**。

![Hello 組件庫主頁面上選取 自訂模組](media/machine-learning-gallery-custom-modules/select-custom-modules-in-gallery.png)

hello **[自訂模組](https://gallery.cortanaintelligence.com/customModules)**頁面會顯示最近新增且受歡迎的模組清單。 tooview 所有的自訂模組選取 hello**查看所有** 按鈕。 選取特定的自訂模組的 toosearch**查看所有**，，然後選取篩選準則。 您也可以搜尋詞彙在輸入 hello**搜尋**hello hello 圖庫頁頂端的方塊。

![所有的自訂模組選取 「 查看所有"toobrowse](media/machine-learning-gallery-custom-modules/click-see-all-for-all-custom-modules.png)

### <a name="understand"></a>了解

已發行的自訂模組的運作方式，toounderstand 選取 hello 自訂模組 tooopen hello 模組詳細資料頁面。 hello 詳細資料 頁面會提供一致且有用的學習經驗。 例如，hello 詳細資料 頁面會反白顯示 hello 目的 hello 模組，並列出預期的輸入、 輸出和參數。 hello 詳細資料頁面中也有連結 toohello 基礎來源程式碼，您可以檢查和自訂。

### <a name="comment-and-share"></a>註解和共用
在自訂模組詳細資料頁面上，在 hello**註解** 區段中，您可以註解、 提供意見反應，或詢問 hello 模組有關的問題。 您甚至可以與朋友或同事 Twitter 或 LinkedIn 共用 hello 模組。 您也可以用電子郵件連結 toohello 模組詳細資料 頁面，tooinvite 其他使用者 tooview hello 頁面。

![與朋友分享此項目](media/machine-learning-gallery-how-to-use-contribute-publish/share-links.png)

![新增您自己的留言](media/machine-learning-gallery-how-to-use-contribute-publish/comments.png)

## <a name="import"></a>Import
您可以從 hello 圖庫 tooyour 自己實驗來匯入任何自訂的模組。

Cortana 智慧組件庫會提供兩種方式 tooimport hello 模組的複本：

* **從圖庫 hello**。 當您從 hello 資源庫匯入自訂的模組時，您也可以取得範例實驗，可讓您如何 toouse hello 模組的範例。
* **從 Machine Learning Studio 內**。 Machine Learning Studio 中作業時，您可以匯入任何自訂的模組 （在此情況下，就無法取得 hello 範例實驗）。

### <a name="from-hello-gallery"></a>從 hello 組件庫

1. 在 hello 組件庫中，開啟 hello 模組詳細資料頁面。 
2. 選取 [在 Studio 中開啟]。
   
    ![從 hello 圖庫開啟自訂模組](media/machine-learning-gallery-custom-modules/open-custom-module-from-gallery.png)
   
每個自訂的模組包含範例實驗示範如何 toouse hello 模組。 當您選取**在 Studio 中開啟**，開啟 Machine Learning Studio 工作區中的 hello 範例實驗。 (如果您沒有已登入 tooStudio，系統會提示您 toofirst 使用您的 Microsoft 帳戶登入。)

此外 toohello 範例實驗，hello 自訂模組是複製的 tooyour 工作區。 此外，自訂模組會連同所有內建或自訂 Machine Learning Studio 模組一起放在模組選擇區中。 現在，您可以將自訂模組用於您自己的實驗中，就如同工作區中任何其他的模組。

### <a name="from-within-machine-learning-studio"></a>從 Machine Learning Studio 內

1. 在 Machine Learning Studio 中，選取 [新增]。
2. 選取 [模組]。 您可以選擇從資源庫模組的清單，或使用 hello 尋找模組**搜尋**方塊。
3. 將滑鼠指向模組，然後選取 [匯入模組]。 (tooget 模組的相關資訊 hello，選取**組件庫中的檢視**。 這會帶您 toohello 模組詳細資料頁面 hello 組件庫中。）
   
    ![將自訂模組匯入 Machine Learning Studio](media/machine-learning-gallery-custom-modules/add-custom-module-in-studio.png)

hello 自訂模組會複製的 tooyour 工作區，並放置於您與您的內建或自訂 Machine Learning Studio 模組的模組調色盤。 現在，您可以將自訂模組用於您自己的實驗中，就如同工作區中任何其他的模組。

## <a name="use"></a>使用

不論哪一種方法，您會選擇的 tooimport 自訂模組，當您匯入 hello 模組，hello 模組會置於您在 Machine Learning Studio 中的模組調色盤。 從您模組的調色盤，您可以使用任何實驗中 hello 自訂模組中工作區中，就像任何其他模組。

toouse 匯入的模組：

1. 建立實驗，或開啟現有的實驗。
2. tooexpand hello 清單中的 hello 模組調色盤中的工作區中的自訂模組選取**自訂**。 hello 模組調色盤是 toohello hello 實驗畫布左邊。
   
    ![Studio 調色盤中的自訂模組清單](media/machine-learning-gallery-custom-modules/custom-module-in-studio-palette.png)
3. 選取您要匯入，hello 模組，並將它拖曳 tooyour 實驗。


**[移 toohello 組件庫](http://gallery.cortanaintelligence.com)**

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

