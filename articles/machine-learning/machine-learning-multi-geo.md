---
title: "aaaMulti 地理說明 」 文件 |Microsoft 文件"
description: "深入了解如何 toocreate 工作區和 hello 南中央 United States (SCUS) 與不同 Azure 區域中發佈 web 服務的 Azure 區域。"
services: machine-learning
documentationcenter: 
author: tedway
manager: jhubbard
editor: rmca14
tags: 
ms.assetid: ed0ca8a8-fa53-4e56-b824-2d7e44641967
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 4/6/2017
ms.author: tedway; neerajkh
ms.openlocfilehash: 77b055950ebfe329131b40e5f0a2f6be1e33c51e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="multi-geo-help-documentation"></a>Multi-Geo 說明文件
本文將說明如何在不同的 Azure 區域中建立工作區及發佈 Web 服務。  hello[逐頁地區的 Azure 產品](https://azure.microsoft.com/en-us/regions/services/)列出 Azure Machine Learning 使用的地區。

## <a name="create-a-workspace"></a>建立工作區
1. 登入 toohello Azure 傳統入口網站。
2. 按一下 [+ 新增] > [資料服務] > [機器學習服務] > [快速建立]。  在 [位置] 選取另一個區域，例如 [東南亞]。
   ![Multi-Geo 說明影像 1][1]
3. 選取 [hello] 工作區，然後再按一下**登入 tooML Studio**。
   ![Multi-Geo 說明影像 2][2]
4. 您現在已於其他地區中建立工作區，您可如同任何其他工作區一樣使用。 tooswitch 之間工作區中，尋找 toohello 右上角螢幕。 按一下 hello 下拉式清單中，選取 hello 區域，然後選取 hello 工作區。 所有項目是本機 toohello 工作區的區域。  例如，所有從工作區中建立 web 服務會的 hello 位於相同的區域 hello 工作區中。
   ![Multi-Geo 說明影像 3][3]

## <a name="open-an-experiment-from-gallery"></a>從 [資源庫] 開啟實驗
如果您從組件庫開啟實驗，您也可以選取您想要的 toocopy hello 實驗的區域。

![Multi-Geo 說明影像 4][4a]

## <a name="web-service-management"></a>Web 服務管理
tooprogrammatically 會管理 web 服務，例如重新定型使用 hello 特定地區的地址：

* https://asiasoutheast.management.azureml.net
* https://europewest.management.azureml.net

### <a name="things-toonote"></a>項目 toonote
1. 您僅能複製實驗工作區屬於 toohello 之間相同區域這種方式。 如果您需要 toocopy 實驗跨越不同地區中的工作區，您可以使用 hello [PowerShell](http://aka.ms/amlps) commandlet [*複製 AmlExperiment* ](https://github.com/hning86/azuremlps/blob/master/README.md#copy-amlexperiment) tooaccomplish 的。 另一個解決方法是至圖庫 toopublish hello 實驗未列出的模式，然後開啟它 hello 工作區中 hello 從其他區域。
2. hello 區域選取器只會顯示一個區域的工作區，一次。  
3. 免費工作區或 [來賓存取] \(匿名) 工作區會在美國中南部建立並裝載。  
4. 從位於東南亞的工作區部署的 Web 服務也會裝載於東南亞。  

## <a name="more-information"></a>詳細資訊
提出 hello [Azure Machine Learning 論壇](https://social.msdn.microsoft.com/Forums/azure/home?forum=MachineLearning)。

<!--Image references-->
[1]: ./media/machine-learning-multi-geo/multi-geo_1.png
[2]: ./media/machine-learning-multi-geo/multi-geo_2.png
[3]: ./media/machine-learning-multi-geo/multi-geo_3.png
[4a]: ./media/machine-learning-multi-geo/multi-geo_4a.png
