---
title: "透過 R 擴展您的經驗 | Microsoft Docs"
description: "如何利用「執行 R 指令碼」模組，透過 R 語言擴充 Azure Machine Learning Studio 的功能。"
services: machine-learning
documentationcenter: 
author: garyericson
manager: jhubbard
editor: cgronlun
ms.assetid: 2c038a45-ba4d-42ea-9a88-e67391ef8c0a
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/20/2017
ms.author: garye
ms.openlocfilehash: fe207ef917980be8b554ad9c08176d108b19fb71
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="3e411-103">透過 R 擴展您的經驗</span><span class="sxs-lookup"><span data-stu-id="3e411-103">Extend your experiment with R</span></span>
<span data-ttu-id="3e411-104">您可以利用[執行 R 指令碼][execute-r-script]模組，透過 R 語言擴充 Azure Machine Learning Studio 的功能。</span><span class="sxs-lookup"><span data-stu-id="3e411-104">You can extend the functionality of Azure Machine Learning Studio through the R language by using the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="3e411-105">此模組接受多個輸入資料集，並產生單一資料集作為輸出。</span><span class="sxs-lookup"><span data-stu-id="3e411-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="3e411-106">您可以將 R 指令碼輸入[執行 R 指令碼][execute-r-script]模組的 **R 指令碼**參數中。</span><span class="sxs-lookup"><span data-stu-id="3e411-106">You can type an R script into the **R Script** parameter of the [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="3e411-107">您可使用類似下面的程式碼，存取模組的每個輸入連接埠：</span><span class="sxs-lookup"><span data-stu-id="3e411-107">You access each input port of the module by using code similar to the following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="3e411-108">列出所有目前安裝的封裝</span><span class="sxs-lookup"><span data-stu-id="3e411-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="3e411-109">可以變更已安裝的封裝清單。</span><span class="sxs-lookup"><span data-stu-id="3e411-109">The list of installed packages can change.</span></span> <span data-ttu-id="3e411-110">目前已安裝套件的清單位於 [Azure Machine Learning 支援的 R 套件](https://msdn.microsoft.com/library/azure/mt741980.aspx)中。</span><span class="sxs-lookup"><span data-stu-id="3e411-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="3e411-111">請將下列程式碼輸入[執行 R 指令碼][execute-r-script]模組，取得目前已安裝套件的最新完整清單︰</span><span class="sxs-lookup"><span data-stu-id="3e411-111">You also can get the complete, current list of installed packages by entering the following code into the [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="3e411-112">這會將套件的清單傳送至[執行 R 指令碼][execute-r-script]模組的輸出連接埠。</span><span class="sxs-lookup"><span data-stu-id="3e411-112">This sends the list of packages to the output port of the [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="3e411-113">若要檢視套件清單，請將轉換模組 (例如[轉換為 CSV][convert-to-csv]) 連接至[執行 R 指令碼][execute-r-script]模組的左輸出，執行實驗，然後按一下轉換模組的輸出並選取 [下載]。</span><span class="sxs-lookup"><span data-stu-id="3e411-113">To view the package list, connect a conversion module such as [Convert to CSV][convert-to-csv] to the left output of the [Execute R Script][execute-r-script] module, run the experiment, then click the output of the conversion module and select **Download**.</span></span> 

![下載「轉換為 CSV」模組的輸出](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is the [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="3e411-115">匯入封裝</span><span class="sxs-lookup"><span data-stu-id="3e411-115">Importing packages</span></span>
<span data-ttu-id="3e411-116">您可以在[執行 R 指令碼][execute-r-script] 模組中使用下列命令，匯入尚未安裝的套件：</span><span class="sxs-lookup"><span data-stu-id="3e411-116">You can import packages that are not already installed by using the following commands in the [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="3e411-117">其中 `my_favorite_package.zip` 檔案包含您的套件。</span><span class="sxs-lookup"><span data-stu-id="3e411-117">where the `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
