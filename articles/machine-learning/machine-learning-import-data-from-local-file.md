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
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="b1db0-105">將訓練資料從硬碟上的檔案匯入到 Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="b1db0-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="b1db0-106">了解從硬碟機 toouse tooupload 資料檔案做為 Azure Machine Learning Studio 中的定型資料方式。</span><span class="sxs-lookup"><span data-stu-id="b1db0-106">Learn how tooupload a data file from your hard drive toouse as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="b1db0-107">匯入 hello 資料檔，您有可供使用的資料集 」 模組在您的工作區中。</span><span class="sxs-lookup"><span data-stu-id="b1db0-107">By importing hello data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-tooimport-data-from-a-local-file"></a><span data-ttu-id="b1db0-108">步驟 tooimport 資料從本機檔案</span><span class="sxs-lookup"><span data-stu-id="b1db0-108">Steps tooimport data from a local file</span></span>
<span data-ttu-id="b1db0-109">tooimport 資料從本機硬碟，請勿 hello 遵循：</span><span class="sxs-lookup"><span data-stu-id="b1db0-109">tooimport data from a local hard drive, do hello following:</span></span>

1. <span data-ttu-id="b1db0-110">按一下**+ 新增**在 hello hello Machine Learning Studio 視窗底部。</span><span class="sxs-lookup"><span data-stu-id="b1db0-110">Click **+NEW** at hello bottom of hello Machine Learning Studio window.</span></span>
2. <span data-ttu-id="b1db0-111">選取 [資料集] 和 [從本機檔案]。</span><span class="sxs-lookup"><span data-stu-id="b1db0-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="b1db0-112">在 [hello**上傳新的資料集**] 對話方塊中，瀏覽 toohello 檔想 tooupload</span><span class="sxs-lookup"><span data-stu-id="b1db0-112">In hello **Upload a new dataset** dialog, browse toohello file you want tooupload</span></span>
4. <span data-ttu-id="b1db0-113">輸入的名稱、 識別 hello 資料型別，並選擇性輸入描述。</span><span class="sxs-lookup"><span data-stu-id="b1db0-113">Enter a name, identify hello data type, and optionally enter a description.</span></span> <span data-ttu-id="b1db0-114">描述建議-它可讓您 toorecord hello 未來使用 hello 資料時，想要 tooremember 的 hello 資料相關的任何特性。</span><span class="sxs-lookup"><span data-stu-id="b1db0-114">A description is recommended - it allows you toorecord any characteristics about hello data that you want tooremember when using hello data in hello future.</span></span>
5. <span data-ttu-id="b1db0-115">hello 核取方塊**這是現有的資料集的 hello 新版**可讓您 tooupdate 現有的資料集與新的資料。</span><span class="sxs-lookup"><span data-stu-id="b1db0-115">hello checkbox **This is hello new version of an existing dataset** allows you tooupdate an existing dataset with new data.</span></span> <span data-ttu-id="b1db0-116">按一下此核取方塊，然後輸入 hello 現有的資料集名稱。</span><span class="sxs-lookup"><span data-stu-id="b1db0-116">Click this checkbox and then enter hello name of an existing dataset.</span></span>

![上傳新的資料集](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="b1db0-118">在上傳期間，您會看見訊息，指出您的檔案正在上傳。</span><span class="sxs-lookup"><span data-stu-id="b1db0-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="b1db0-119">上傳時間取決於您的資料和 hello 速度連線 toohello 服務的 hello 大小。</span><span class="sxs-lookup"><span data-stu-id="b1db0-119">Upload time depends on hello size of your data and hello speed of your connection toohello service.</span></span> <span data-ttu-id="b1db0-120">如果您知道 hello 檔案要花費較長的時間，您可以先做其他事情，Machine Learning Studio 中的，等候期間。</span><span class="sxs-lookup"><span data-stu-id="b1db0-120">If you know hello file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="b1db0-121">不過，關閉 hello 瀏覽器會導致 hello 資料上傳 toofail。</span><span class="sxs-lookup"><span data-stu-id="b1db0-121">However, closing hello browser causes hello data upload toofail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="b1db0-122">資料集模組已可供使用</span><span class="sxs-lookup"><span data-stu-id="b1db0-122">Dataset module is ready for use</span></span>
<span data-ttu-id="b1db0-123">一旦上傳您的資料時，它會儲存在資料集的模組中，而且是在您的工作區中的可用 tooany 實驗。</span><span class="sxs-lookup"><span data-stu-id="b1db0-123">Once your data is uploaded, it's stored in a dataset module and is available tooany experiment in your workspace.</span></span>

<span data-ttu-id="b1db0-124">當您編輯的實驗時，您可以找到您已在 hello 建立 hello 資料集**我的資料集**hello 底下清單**儲存的資料集**hello 模組調色盤中的清單。</span><span class="sxs-lookup"><span data-stu-id="b1db0-124">When you're editing an experiment, you can find hello datasets you've created in hello **My Datasets** list under hello **Saved Datasets** list in hello module palette.</span></span> <span data-ttu-id="b1db0-125">您可以藉由拖放 hello 資料集拖曳到 hello 實驗畫布上時要用於進一步的分析和機器學習 toouse hello 資料集。</span><span class="sxs-lookup"><span data-stu-id="b1db0-125">You can drag and drop hello dataset onto hello experiment canvas when you want toouse hello dataset for further analytics and machine learning.</span></span>
