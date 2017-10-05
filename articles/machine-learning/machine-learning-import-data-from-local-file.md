---
title: "將資料從檔案匯入到 Azure Machine Learning Studio | Microsoft Docs"
description: "了解如何將訓練資料檔案從硬碟上傳到 Azure Machine Learning Studio。 這樣會在工作區中建立資料集模組。"
keywords: "匯入資料,資料格式,資料類型,資料來源,定型資料"
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
ms.openlocfilehash: 18010864160ceb2d76aea37196e6944bbe426457
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="import-training-data-from-a-file-on-your-hard-drive-into-machine-learning-studio"></a><span data-ttu-id="31030-105">將訓練資料從硬碟上的檔案匯入到 Machine Learning Studio</span><span class="sxs-lookup"><span data-stu-id="31030-105">Import training data from a file on your hard drive into Machine Learning Studio</span></span>
[!INCLUDE [import-data-into-aml-studio-selector](../../includes/machine-learning-import-data-into-aml-studio.md)]

<span data-ttu-id="31030-106">了解如何上傳硬碟上的資料檔案，以在 Azure Machine Learning Studio 中做為訓練資料使用。</span><span class="sxs-lookup"><span data-stu-id="31030-106">Learn how to upload a data file from your hard drive to use as training data in Azure Machine Learning Studio.</span></span> <span data-ttu-id="31030-107">透過匯入資料檔案，您就有可在工作區中使用的資料集模組。</span><span class="sxs-lookup"><span data-stu-id="31030-107">By importing the data file, you have a dataset module ready for use in your workspace.</span></span>

## <a name="steps-to-import-data-from-a-local-file"></a><span data-ttu-id="31030-108">從本機檔案匯入資料的步驟</span><span class="sxs-lookup"><span data-stu-id="31030-108">Steps to import data from a local file</span></span>
<span data-ttu-id="31030-109">若要從本機硬碟匯入資料，請執行下列作業︰</span><span class="sxs-lookup"><span data-stu-id="31030-109">To import data from a local hard drive, do the following:</span></span>

1. <span data-ttu-id="31030-110">在 [Machine Learning Studio] 視窗底部，按一下 [ **+新增** ]。</span><span class="sxs-lookup"><span data-stu-id="31030-110">Click **+NEW** at the bottom of the Machine Learning Studio window.</span></span>
2. <span data-ttu-id="31030-111">選取 [資料集] 和 [從本機檔案]。</span><span class="sxs-lookup"><span data-stu-id="31030-111">Select **DATASET** and **FROM LOCAL FILE**.</span></span>
3. <span data-ttu-id="31030-112">在 [ **上傳新的資料集** ] 對話方塊中，瀏覽至您要上傳的檔案。</span><span class="sxs-lookup"><span data-stu-id="31030-112">In the **Upload a new dataset** dialog, browse to the file you want to upload</span></span>
4. <span data-ttu-id="31030-113">輸入名稱、識別資料類型，然後選擇性地輸入說明。</span><span class="sxs-lookup"><span data-stu-id="31030-113">Enter a name, identify the data type, and optionally enter a description.</span></span> <span data-ttu-id="31030-114">建議輸入說明 - 它可以讓您記錄資料的任何特性，您會希望在未來使用資料時記住這些特性。</span><span class="sxs-lookup"><span data-stu-id="31030-114">A description is recommended - it allows you to record any characteristics about the data that you want to remember when using the data in the future.</span></span>
5. <span data-ttu-id="31030-115">核取方塊 [ **這是現有資料集的新版本** ] 可讓您使用新資料更新現有資料集。</span><span class="sxs-lookup"><span data-stu-id="31030-115">The checkbox **This is the new version of an existing dataset** allows you to update an existing dataset with new data.</span></span> <span data-ttu-id="31030-116">按一下此核取方塊然後輸入現有資料集的名稱即可。</span><span class="sxs-lookup"><span data-stu-id="31030-116">Click this checkbox and then enter the name of an existing dataset.</span></span>

![上傳新的資料集](media/machine-learning-import-data-from-local-file/upload-dataset.png)

<span data-ttu-id="31030-118">在上傳期間，您會看見訊息，指出您的檔案正在上傳。</span><span class="sxs-lookup"><span data-stu-id="31030-118">During upload, you'll see a message that your file is being uploaded.</span></span> <span data-ttu-id="31030-119">上傳時間取決於資料大小和連接至服務的速度。</span><span class="sxs-lookup"><span data-stu-id="31030-119">Upload time depends on the size of your data and the speed of your connection to the service.</span></span> <span data-ttu-id="31030-120">如果您知道上傳檔案將耗費很長的時間，您可以在等待時在 ML Studio 中執行其他動作。</span><span class="sxs-lookup"><span data-stu-id="31030-120">If you know the file will take a long time, you can do other things inside Machine Learning Studio while you wait.</span></span> <span data-ttu-id="31030-121">但是，關閉瀏覽器會導致資料上傳失敗。</span><span class="sxs-lookup"><span data-stu-id="31030-121">However, closing the browser causes the data upload to fail.</span></span>

## <a name="dataset-module-is-ready-for-use"></a><span data-ttu-id="31030-122">資料集模組已可供使用</span><span class="sxs-lookup"><span data-stu-id="31030-122">Dataset module is ready for use</span></span>
<span data-ttu-id="31030-123">資料上傳之後，會儲存在資料集模組中，並且可供工作區中的任何實驗使用。</span><span class="sxs-lookup"><span data-stu-id="31030-123">Once your data is uploaded, it's stored in a dataset module and is available to any experiment in your workspace.</span></span>

<span data-ttu-id="31030-124">當您在編輯實驗時，您可以在模組調色盤的 [儲存的資料集] 清單底下的 [我的資料集] 清單內，找到您所建立的資料集。</span><span class="sxs-lookup"><span data-stu-id="31030-124">When you're editing an experiment, you can find the datasets you've created in the **My Datasets** list under the **Saved Datasets** list in the module palette.</span></span> <span data-ttu-id="31030-125">當您想將資料集用於進一步的分析和機器學習時，可以在實驗畫布上拖放資料集。</span><span class="sxs-lookup"><span data-stu-id="31030-125">You can drag and drop the dataset onto the experiment canvas when you want to use the dataset for further analytics and machine learning.</span></span>
