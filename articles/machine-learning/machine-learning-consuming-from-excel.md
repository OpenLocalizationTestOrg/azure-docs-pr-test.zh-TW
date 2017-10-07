---
title: "機器學習 Web 服務，從 Excel aaaConsume |Microsoft 文件"
description: "從 Excel 使用 Azure Machine Learning Web 服務"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: cgronlun
ms.assetid: 3f3cdd2f-1816-487e-ab78-530e01e9788f
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 2/13/2017
ms.author: tedway
ms.openlocfilehash: e2e8bbf7ba75b6618a0285539555ce175ec03c1a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="consuming-an-azure-machine-learning-web-service-from-excel"></a>從 Excel 使用 Azure Machine Learning Web 服務
 Azure Machine Learning Studio 可讓您輕鬆 toocall web 服務，直接從 Excel 而 hello 需要 toowrite 任何程式碼。

如果您使用 Excel 2013 （或更新版本） 或 Excel Online，則我們建議您使用 hello Excel [Excel 增益集](machine-learning-excel-add-in-for-web-services.md)。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="steps"></a>步驟
發佈 Web 服務。 [此頁面](machine-learning-walkthrough-5-publish-web-service.md)說明如何 toodo 它。 目前具有單一輸出 （也就是單一計分標籤） 的要求/回應服務只支援 hello Excel 活頁簿的功能。 

Web 服務之後，按一下 hello **WEB 服務**左邊的 hello studio hello 區段，然後選取 從 Excel 的 hello web 服務 tooconsume。

**傳統 Web 服務**

1. 在 hello**儀表板**hello web 服務是為 hello 的資料列索引標籤**要求/回應**服務。 如果此服務會在單一輸出，您應該會看見 hello**下載 Excel 活頁簿**該資料列中的連結。
   
    ![][1]
2. 按一下 [下載 Excel 活頁簿] 。

**新的 Web 服務**

1. 在 hello Azure Machine Learning Web 服務入口網站中，選取 **取用**。
2. 在 hello 取用頁面 hello **Web 服務耗用量選項**區段中，按一下 hello Excel 圖示。

**使用 hello 活頁簿**

1. 開啟 hello 活頁簿。
2. 此時會出現安全性警告。按一下 hello**啟用編輯** 按鈕。
   
    ![][2]
3. 此時會出現安全性警告。 按一下 hello**啟用內容**按鈕在試算表的 toorun 巨集。
   
    ![][3]
4. 啟用巨集之後，就會產生表格。 藍色是中的資料行作為輸入 hello RR web 服務，需要或**參數**。 請注意 hello RR 服務的 hello 輸出**PREDICTED VALUES**以綠色。 對於給定的資料列的所有資料行已滿時，hello 活頁簿將會自動呼叫 hello 計分 API，並顯示 hello 計分結果。
   
    ![][4]
5. tooscore 超過一個資料列，填滿 hello 第二個資料列資料與 hello 預測所產生的值。 您甚至可以一次貼上多列。

您可以使用任何 hello Excel 功能圖形、 電源對應 （條件式格式化等） 與 hello 預測值 toohelp hello 資料視覺化。    

## <a name="sharing-your-workbook"></a>共用活頁簿
Hello 巨集 toowork，您的 API 金鑰必須是 hello 試算表的一部分。 這表示您應該只與實體/您信任的人共用 hello 活頁簿。

## <a name="automatic-updates"></a>自動更新
下列兩種情況會產生 RRS 呼叫：

1. hello 第一次資料列都有內容中的所有其**參數**
2. 每當任何 hello**參數**中資料列時，所有的變更其**參數**輸入。

[1]: ./media/machine-learning-consuming-from-excel/excellink.png
[2]: ./media/machine-learning-consuming-from-excel/enableeditting.png
[3]: ./media/machine-learning-consuming-from-excel/enablecontent.png
[4]: ./media/machine-learning-consuming-from-excel/sampletable.png
