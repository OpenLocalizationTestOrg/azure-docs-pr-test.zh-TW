---
title: "從檔案到 Azure Machine Learning Studio aaaImport 資料 |Microsoft 文件"
description: "了解從您的硬碟機 tooAzure Machine Learning Studio tooupload 定型資料檔案的方式。 這會建立資料集模組 hello 工作區。"
keywords: "匯入資料、資料格式、資料類型、資料來源、定型資料"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: c0dd9e90-23c4-4f64-8b8f-489ad79f047b
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye;bradsev
ms.openlocfilehash: 636facd9042145382c953a1c75969149ede6f6fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a>將訓練資料從硬碟上的檔案匯入到 Machine Learning Studio
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

了解從硬碟機 toouse tooupload 資料檔案做為 Azure Machine Learning Studio 中的定型資料方式。 匯入 hello 資料檔，您有可供使用的資料集 」 模組在您的工作區中。

## <a name="steps-tooimport-data-from-a-local-file"></a>步驟 tooimport 資料從本機檔案
tooimport 資料從本機硬碟，請勿 hello 遵循：

1. 按一下**+ 新增**在 hello hello Machine Learning Studio 視窗底部。
2. 選取 [資料集] 和 [從本機檔案]。
3. 在 [hello**上傳新的資料集**] 對話方塊中，瀏覽 toohello 檔想 tooupload
4. 輸入的名稱、 識別 hello 資料型別，並選擇性輸入描述。 描述建議-它可讓您 toorecord hello 未來使用 hello 資料時，想要 tooremember 的 hello 資料相關的任何特性。
5. hello 核取方塊**這是現有的資料集的 hello 新版**可讓您 tooupdate 現有的資料集與新的資料。 按一下此核取方塊，然後輸入 hello 現有的資料集名稱。

![上傳新的資料集](media/machine-learning-import-data-from-local-file/upload-dataset.png)

在上傳期間，您會看見訊息，指出您的檔案正在上傳。 上傳時間取決於您的資料和 hello 速度連線 toohello 服務的 hello 大小。 如果您知道 hello 檔案要花費較長的時間，您可以先做其他事情，Machine Learning Studio 中的，等候期間。 不過，關閉 hello 瀏覽器會導致 hello 資料上傳 toofail。

## <a name="dataset-module-is-ready-for-use"></a>資料集模組已可供使用
一旦上傳您的資料時，它會儲存在資料集的模組中，而且是在您的工作區中的可用 tooany 實驗。

當您編輯的實驗時，您可以找到您已在 hello 建立 hello 資料集**我的資料集**hello 底下清單**儲存的資料集**hello 模組調色盤中的清單。 您可以藉由拖放 hello 資料集拖曳到 hello 實驗畫布上時要用於進一步的分析和機器學習 toouse hello 資料集。
