---
title: "aaaManage 實驗 Machine Learning Studio 中的反覆項目 |Microsoft 文件"
description: "Toomanage 進行反覆項目，Azure Machine Learning Studio 中的實驗"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 6a53530f-20d5-40ae-9b49-7b499ccb44b7
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: bd30c048ce063811b1b2de8ce6d71e99ba975713
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-experiment-iterations-in-azure-machine-learning-studio"></a>在 Azure Machine Learning Studio 中管理實驗逐一查看
當您修改 hello 開發預測分析的模型是反覆的程序-您的結果不同的函式和參數的實驗，聚合直到您滿意您有定型、 有效率的模型。 索引鍵 toothis 程序為追蹤 hello 您實驗參數和組態的各個反覆項目。

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

您可以檢閱先前執行的順序 toochallenge 中隨時將實驗，再次瀏覽，以及最終確認或精簡先前的假設。 當您執行實驗時，Machine Learning Studio 就會保留記錄的 hello 執行，包括資料集、 模組和連接埠的連線和參數。 此歷程記錄也會擷取結果、執行階段資訊，例如開始和停止時間、記錄訊息及執行狀態。 您可以回頭查看以前在任何這些就會在您的實驗和中繼結果的任何時間 tooreview hello 時序。 您甚至可以使用到新的查詢和探索階段的先前執行的實驗 toolaunch 上您路徑 toocreating 簡單、 複雜或甚至集團模型方案。

> [!NOTE]
> 當您檢視先前執行的實驗時，hello 實驗該版本已鎖定且無法編輯。 按一下，您可以不過，儲存一份**SAVE AS**並提供 hello 複製的新名稱。 Machine Learning Studio 中開啟 hello 新的複本，您可以編輯並執行。 這份實驗位於 hello**實驗**清單以及所有您其他實驗。
> 
> 

## <a name="viewing-hello-prior-run"></a>檢視先前執行的 hello
當您有已開啟您已至少一次執行的實驗時，您可以檢視依序按一下之前執行 hello 實驗的 hello**先前執行**hello 屬性 窗格中。

例如，假設您建立實驗並且在下列時間執行其版本：11:23、11:42 及 11:55。 如果您開啟 hello 上次執行 hello 實驗 (11:55)，然後按一下**先前執行**，開啟您執行在 11:42 hello 版本。

## <a name="viewing-hello-run-history"></a>檢視 hello 執行歷程記錄
按一下即可檢視所有的 hello 先前執行的實驗**檢視執行記錄**開啟實驗中。

例如，假設您建立以 hello 的實驗[線性迴歸][ linear-regression]模組，而且您想要變更的 hello 值 tooobserve hello 影響**學習速率**上您的實驗結果。 Hello 實驗多次執行具有不同的值，這個參數，如，如下所示：

| 學習速度值 | 執行開始時間 |
| --- | --- |
| 0.1 |2014/9/11 下午 4:18:58 |
| 0.2 |2014/9/11 下午 4:24:33 |
| 0.4 |2014/9/11 下午 4:28:36 |
| 0.5 |2014/9/11 下午 4:33:31 |

如果您按一下 [ **檢視執行歷程記錄**]，您會看見所有執行的清單：

![範例執行歷程記錄][runhistory]

按一下任何這些執行 tooview，在您執行的 hello 階段實驗 hello 的快照集。 hello 組態、 參數值、 註解，以及結果是所有保留的 toogive 您的實驗執行的完整記錄。

> [!TIP]
> toodocument hello 實驗的反覆項目，您可以修改 hello 標題每次執行它，您可以更新 hello**摘要**hello 的試驗 hello 屬性 窗格中，您可以新增或更新個別的模組上的註解toorecord 您的變更。 hello 標題、 摘要和模組註解會儲存與 hello 實驗每次執行。
> 
> 

hello 的實驗 hello 清單**實驗**Machine Learning Studio 中的索引標籤一律會顯示 hello 的實驗的最新版本。 如果您開啟先前 hello 實驗執行 (使用**先前執行**或**檢視執行記錄**)，您可以按一下傳回 toohello 草稿版本**檢視執行記錄**，然後選取hello 反覆項目具有**狀態**的**編輯**。

## <a name="iterating-on-a-previous-run"></a>逐一查看上一次執行
當您按一下 [上一次執行] 或 [檢視執行歷程記錄]，並且開啟上一次執行時，您可以在唯讀模式中檢視完成的實驗。

如果您想 toobegin 實驗開頭 hello 方式針對先前執行的反覆項目，您可以開啟 hello 執行，然後按一下**SAVE AS**。 這會建立新的實驗中，新的標題、 空的執行歷程記錄，以及所有 hello 元件和執行先前的 hello 參數值。 這個新的實驗會列在 hello**實驗** 索引標籤中 hello Machine Learning Studio 首頁上，而且您可以修改並執行它，初始化新執行實驗此反覆項目歷程記錄。 

例如，假設您有執行歷程記錄顯示 hello 前一節中的 hello 實驗。 要設定 hello 時，會發生什麼事 tooobserve**學習速率**參數 too0.4 和不同的值再試一次 hello**定型 epoch 的數目**參數。

1. 按一下**檢視執行記錄**並開啟 hello 實驗下午 4:28:36 （您在其中設定 hello 參數值 too0.4） 執行您的 hello 反覆項目。
2. 按一下 [ **另存新檔**]。
3. 輸入新的標題，然後按一下 hello**確定**核取記號。 建立 hello 實驗的新複本。
4. 修改 hello**定型 epoch 的數目**參數。
5. 按一下 [ **執行**]。

您現在可以繼續 toomodify 並執行您的經驗，此版本建立新的執行歷程記錄 toorecord 您的工作。

<!-- Images -->
[runhistory]:./media/machine-learning-manage-experiment-iterations/viewrunhistory.jpg


<!-- Module References -->
[linear-regression]: https://msdn.microsoft.com/library/azure/31960a6f-789b-4cf7-88d6-2e1152c0bd1a/
