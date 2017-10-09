---
title: "aaaExtend 以 R 實驗 |Microsoft 文件"
description: "如何 tooextend hello 透過 hello R 語言的功能的 Azure Machine Learning Studio 使用 hello 執行 R 指令碼模組。"
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
ms.openlocfilehash: 396489f26f367a744922af65e04f056c7afa1399
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="extend-your-experiment-with-r"></a><span data-ttu-id="afaf8-103">透過 R 擴展您的經驗</span><span class="sxs-lookup"><span data-stu-id="afaf8-103">Extend your experiment with R</span></span>
<span data-ttu-id="afaf8-104">您可以透過 hello R 語言的 hello 功能的 Azure Machine Learning Studio 使用擴充程式 hello[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="afaf8-104">You can extend hello functionality of Azure Machine Learning Studio through hello R language by using hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="afaf8-105">此模組接受多個輸入資料集，並產生單一資料集作為輸出。</span><span class="sxs-lookup"><span data-stu-id="afaf8-105">This module accepts multiple input datasets and yields a single dataset as output.</span></span> <span data-ttu-id="afaf8-106">您可以將 R 指令碼輸入 hello **R 指令碼**hello 參數[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="afaf8-106">You can type an R script into hello **R Script** parameter of hello [Execute R Script][execute-r-script] module.</span></span>

<span data-ttu-id="afaf8-107">您可以使用類似 toohello 後面的程式碼，以存取 hello 模組的每個輸入連接埠：</span><span class="sxs-lookup"><span data-stu-id="afaf8-107">You access each input port of hello module by using code similar toohello following:</span></span>

    dataset1 <- maml.mapInputPort(1)

## <a name="listing-all-currently-installed-packages"></a><span data-ttu-id="afaf8-108">列出所有目前安裝的封裝</span><span class="sxs-lookup"><span data-stu-id="afaf8-108">Listing all currently-installed packages</span></span>
<span data-ttu-id="afaf8-109">已安裝的封裝 hello 清單可以變更。</span><span class="sxs-lookup"><span data-stu-id="afaf8-109">hello list of installed packages can change.</span></span> <span data-ttu-id="afaf8-110">目前已安裝套件的清單位於 [Azure Machine Learning 支援的 R 套件](https://msdn.microsoft.com/library/azure/mt741980.aspx)中。</span><span class="sxs-lookup"><span data-stu-id="afaf8-110">A list of currently installed packages can be found in [R Packages Supported by Azure Machine Learning](https://msdn.microsoft.com/library/azure/mt741980.aspx).</span></span>

<span data-ttu-id="afaf8-111">您也可以取得已安裝的封裝的 hello 完整的目前清單輸入 hello hello 成下列程式碼[執行 R 指令碼][ execute-r-script]模組：</span><span class="sxs-lookup"><span data-stu-id="afaf8-111">You also can get hello complete, current list of installed packages by entering hello following code into hello [Execute R Script][execute-r-script] module:</span></span>

    out <- data.frame(installed.packages(,,,fields="Description"))
    maml.mapOutputPort("out")

<span data-ttu-id="afaf8-112">這樣做會傳送 hello 份封裝 toohello 輸出連接埠 hello[執行 R 指令碼][ execute-r-script]模組。</span><span class="sxs-lookup"><span data-stu-id="afaf8-112">This sends hello list of packages toohello output port of hello [Execute R Script][execute-r-script] module.</span></span>
<span data-ttu-id="afaf8-113">tooview hello 封裝清單中，例如連接轉換模組[轉換 tooCSV] [ convert-to-csv] toohello 剩餘輸出的 hello[執行 R 指令碼][ execute-r-script]模組，執行 hello 實驗中，然後按一下 [hello 輸出 hello 轉換模組，然後選取**下載**。</span><span class="sxs-lookup"><span data-stu-id="afaf8-113">tooview hello package list, connect a conversion module such as [Convert tooCSV][convert-to-csv] toohello left output of hello [Execute R Script][execute-r-script] module, run hello experiment, then click hello output of hello conversion module and select **Download**.</span></span> 

![下載 「 轉換 tooCSV 」 模組的輸出](./media/machine-learning-extend-your-experiment-with-r/download-package-list.png)


<!--
For convenience, here is hello [current full list with version numbers in Excel format](http://az754797.vo.msecnd.net/docs/RPackages.xlsx).
-->

## <a name="importing-packages"></a><span data-ttu-id="afaf8-115">匯入封裝</span><span class="sxs-lookup"><span data-stu-id="afaf8-115">Importing packages</span></span>
<span data-ttu-id="afaf8-116">您可以匯入封裝尚未安裝使用下列命令在 hello hello[執行 R 指令碼][ execute-r-script]模組：</span><span class="sxs-lookup"><span data-stu-id="afaf8-116">You can import packages that are not already installed by using hello following commands in hello [Execute R Script][execute-r-script] module:</span></span>

    install.packages("src/my_favorite_package.zip", lib = ".", repos = NULL, verbose = TRUE)
    success <- library("my_favorite_package", lib.loc = ".", logical.return = TRUE, verbose = TRUE)

<span data-ttu-id="afaf8-117">其中 hello`my_favorite_package.zip`檔案包含您的封裝。</span><span class="sxs-lookup"><span data-stu-id="afaf8-117">where hello `my_favorite_package.zip` file contains your package.</span></span>

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]


<!-- Module References -->
[execute-r-script]: https://msdn.microsoft.com/library/azure/30806023-392b-42e0-94d6-6b775a6e0fd5/
[convert-to-csv]: https://msdn.microsoft.com/library/azure/faa6ba63-383c-4086-ba58-7abf26b85814/
