---
title: "Net# 類神經規格語言指南 | Microsoft Docs"
description: "語法 Net # 類神經網路規格語言，以及如何建立 Microsoft Azure ML 使用 Net # 自訂類神經網路模型的範例"
services: machine-learning
documentationcenter: 
author: jeannt
manager: jhubbard
editor: cgronlun
ms.assetid: cfd1454b-47df-4745-b064-ce5f9b3be303
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: jeannt
ms.openlocfilehash: 965c60ffde55041cc3864d06d81f5590c7ea1c11
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="guide-to-net-neural-network-specification-language-for-azure-machine-learning"></a><span data-ttu-id="8cf77-103">適用於 Azure Machine Learning 的 Net# 類神經規格語言指南</span><span class="sxs-lookup"><span data-stu-id="8cf77-103">Guide to Net# neural network specification language for Azure Machine Learning</span></span>
## <a name="overview"></a><span data-ttu-id="8cf77-104">概觀</span><span class="sxs-lookup"><span data-stu-id="8cf77-104">Overview</span></span>
<span data-ttu-id="8cf77-105">Net# 是由 Microsoft 所開發的語言，可用來定義類神經網路架構。</span><span class="sxs-lookup"><span data-stu-id="8cf77-105">Net# is a language developed by Microsoft that is used to define neural network architectures.</span></span> <span data-ttu-id="8cf77-106">您可以在 Microsoft Azure Machine Learning 的類神經網路模組中使用 Net#。</span><span class="sxs-lookup"><span data-stu-id="8cf77-106">You can use Net# in neural network modules in Microsoft Azure Machine Learning.</span></span>

<!-- This function doesn't currentlyappear in the MicrosoftML documentation. If it is added in a future update, we can uncomment this text.

, or in the `rxNeuralNetwork()` function in [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml). 

-->

<span data-ttu-id="8cf77-107">在本文中，您將了解開發自訂類神經網路所需的基本概念︰</span><span class="sxs-lookup"><span data-stu-id="8cf77-107">In this article, you will learn basic concepts needed to develop a custom neural network:</span></span> 

* <span data-ttu-id="8cf77-108">類神經網路的需求和主要元件的定義方式</span><span class="sxs-lookup"><span data-stu-id="8cf77-108">Neural network requirements and how to define the primary components</span></span>
* <span data-ttu-id="8cf77-109">Net# 規格語言的語法和關鍵字</span><span class="sxs-lookup"><span data-stu-id="8cf77-109">The syntax and keywords of the Net# specification language</span></span>
* <span data-ttu-id="8cf77-110">建立使用 Net # 自訂類神經網路的範例</span><span class="sxs-lookup"><span data-stu-id="8cf77-110">Examples of custom neural networks created using Net#</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a><span data-ttu-id="8cf77-111">類神經網路基本概念</span><span class="sxs-lookup"><span data-stu-id="8cf77-111">Neural network basics</span></span>
<span data-ttu-id="8cf77-112">類神經網路的組成結構，包含以***層***組織的***節點***，和節點之間的加權***連線*** (或***邊緣***)。</span><span class="sxs-lookup"><span data-stu-id="8cf77-112">A neural network structure consists of ***nodes*** that are organized in ***layers***, and weighted ***connections*** (or ***edges***) between the nodes.</span></span> <span data-ttu-id="8cf77-113">這些連線是雙向的，且每個連線都有***來源***節點和***目的地***節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-113">The connections are directional, and each connection has a ***source*** node and a ***destination*** node.</span></span>  

<span data-ttu-id="8cf77-114">每個***可訓練的層*** (隱藏或輸出層) 都有一或多個***連線套組***。</span><span class="sxs-lookup"><span data-stu-id="8cf77-114">Each ***trainable layer*** (a hidden or an output layer) has one or more ***connection bundles***.</span></span> <span data-ttu-id="8cf77-115">連線套組由來源層和來自該來源層之連線的規格所組成。</span><span class="sxs-lookup"><span data-stu-id="8cf77-115">A connection bundle consists of a source layer and a specification of the connections from that source layer.</span></span> <span data-ttu-id="8cf77-116">一個套組中的所有連線會共用相同的***來源層***和相同的***目的地層***。</span><span class="sxs-lookup"><span data-stu-id="8cf77-116">All the connections in a given bundle share the same ***source layer*** and the same ***destination layer***.</span></span> <span data-ttu-id="8cf77-117">在 Net# 中，連線套組會被視為由套組的目的地層所屬。</span><span class="sxs-lookup"><span data-stu-id="8cf77-117">In Net#, a connection bundle is considered as belonging to the bundle's destination layer.</span></span>  

<span data-ttu-id="8cf77-118">Net# 支援多種不同的連線套組，可讓您自訂輸入對應至隱藏層和對應至輸出的方式。</span><span class="sxs-lookup"><span data-stu-id="8cf77-118">Net# supports various kinds of connection bundles, which lets you customize the way inputs are mapped to hidden layers and mapped to the outputs.</span></span>   

<span data-ttu-id="8cf77-119">預設或標準套組為**完整套組**；在此類套組中，來源層中的每個節點會分別連接到目的地層中的各個節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-119">The default or standard bundle is a **full bundle**, in which each node in the source layer is connected to every node in the destination layer.</span></span>  

<span data-ttu-id="8cf77-120">此外，Net# 也支援下列四種進階連線套組：</span><span class="sxs-lookup"><span data-stu-id="8cf77-120">Additionally, Net# supports the following four kinds of advanced connection bundles:</span></span>  

* <span data-ttu-id="8cf77-121">**篩選套組**。</span><span class="sxs-lookup"><span data-stu-id="8cf77-121">**Filtered bundles**.</span></span> <span data-ttu-id="8cf77-122">使用者可使用來源層節點和目的地層節點的位置來定義述詞。</span><span class="sxs-lookup"><span data-stu-id="8cf77-122">The user can define a predicate by using the locations of the source layer node and the destination layer node.</span></span> <span data-ttu-id="8cf77-123">只要述詞為 True，即會連接節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-123">Nodes are connected whenever the predicate is True.</span></span>
* <span data-ttu-id="8cf77-124">**迴旋套組**。</span><span class="sxs-lookup"><span data-stu-id="8cf77-124">**Convolutional bundles**.</span></span> <span data-ttu-id="8cf77-125">使用者可在來源層中定義小型的節點臨近地區。</span><span class="sxs-lookup"><span data-stu-id="8cf77-125">The user can define small neighborhoods of nodes in the source layer.</span></span> <span data-ttu-id="8cf77-126">目的地層中的每個節點都會連接到來源層中的一個節點鄰區。</span><span class="sxs-lookup"><span data-stu-id="8cf77-126">Each node in the destination layer is connected to one neighborhood of nodes in the source layer.</span></span>
* <span data-ttu-id="8cf77-127">**集區套組**和**回應正規化套組**。</span><span class="sxs-lookup"><span data-stu-id="8cf77-127">**Pooling bundles** and **Response normalization bundles**.</span></span> <span data-ttu-id="8cf77-128">這些套組類似於可供使用者在來源層中定義小型節點臨近地區的迴旋套組。</span><span class="sxs-lookup"><span data-stu-id="8cf77-128">These are similar to convolutional bundles in that the user defines small neighborhoods of nodes in the source layer.</span></span> <span data-ttu-id="8cf77-129">差別在於這些套組中的邊緣加權無法訓練。</span><span class="sxs-lookup"><span data-stu-id="8cf77-129">The difference is that the weights of the edges in these bundles are not trainable.</span></span> <span data-ttu-id="8cf77-130">因此會將預先定義的函數套用至來源節點值來判斷目的地節點值。</span><span class="sxs-lookup"><span data-stu-id="8cf77-130">Instead, a predefined function is applied to the source node values to determine the destination node value.</span></span>  

<span data-ttu-id="8cf77-131">使用 Net# 定義類神經網路的結構，可讓您定義如深度類神經網路或任意維度的迴旋，而這些項目都可改善影像、音訊或視訊等資料的學習。</span><span class="sxs-lookup"><span data-stu-id="8cf77-131">Using Net# to define the structure of a neural network makes it possible to define complex structures such as deep neural networks or convolutions of arbitrary dimensions, which are known to improve learning on data such as image, audio, or video.</span></span>  

## <a name="supported-customizations"></a><span data-ttu-id="8cf77-132">支援的自訂</span><span class="sxs-lookup"><span data-stu-id="8cf77-132">Supported customizations</span></span>
<span data-ttu-id="8cf77-133">您在 Azure Machine Learning 中建立的類神經網路模型架構，可以使用 Net# 廣泛地進行自訂。</span><span class="sxs-lookup"><span data-stu-id="8cf77-133">The architecture of neural network models that you create in Azure Machine Learning can be extensively customized by using Net#.</span></span> <span data-ttu-id="8cf77-134">您可以：</span><span class="sxs-lookup"><span data-stu-id="8cf77-134">You can:</span></span>  

* <span data-ttu-id="8cf77-135">建立隱藏層及控制每一層中的節點數目。</span><span class="sxs-lookup"><span data-stu-id="8cf77-135">Create hidden layers and control the number of nodes in each layer.</span></span>
* <span data-ttu-id="8cf77-136">指定各層彼此連接的方式。</span><span class="sxs-lookup"><span data-stu-id="8cf77-136">Specify how layers are to be connected to each other.</span></span>
* <span data-ttu-id="8cf77-137">定義特殊連線結構，例如迴旋和加權共用套組。</span><span class="sxs-lookup"><span data-stu-id="8cf77-137">Define special connectivity structures, such as convolutions and weight sharing bundles.</span></span>
* <span data-ttu-id="8cf77-138">指定不同的啟用函數。</span><span class="sxs-lookup"><span data-stu-id="8cf77-138">Specify different activation functions.</span></span>  

<span data-ttu-id="8cf77-139">如需規格語言語法的詳細資訊，請參閱[結構規格](#Structure-specifications)。</span><span class="sxs-lookup"><span data-stu-id="8cf77-139">For details of the specification language syntax, see [Structure Specification](#Structure-specifications).</span></span>  

<span data-ttu-id="8cf77-140">如需為某些一般機器學習工作定義類神經網路的範例 (包括簡單與複雜)，請參閱[範例](#Examples-of-Net#-usage)。</span><span class="sxs-lookup"><span data-stu-id="8cf77-140">For examples of defining neural networks for some common machine learning tasks, from simplex to complex, see [Examples](#Examples-of-Net#-usage).</span></span>  

## <a name="general-requirements"></a><span data-ttu-id="8cf77-141">一般需求</span><span class="sxs-lookup"><span data-stu-id="8cf77-141">General requirements</span></span>
* <span data-ttu-id="8cf77-142">必須只能有一個輸出層，和至少一個輸入層，以及零或多個隱藏層。</span><span class="sxs-lookup"><span data-stu-id="8cf77-142">There must be exactly one output layer, at least one input layer, and zero or more hidden layers.</span></span> 
* <span data-ttu-id="8cf77-143">每一層都有固定的節點數目，在概念上會以任意維度的矩形陣列編排。</span><span class="sxs-lookup"><span data-stu-id="8cf77-143">Each layer has a fixed number of nodes, conceptually arranged in a rectangular array of arbitrary dimensions.</span></span> 
* <span data-ttu-id="8cf77-144">輸入層沒有相關聯的訓練參數，而會顯示執行個體資料進入網路的點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-144">Input layers have no associated trained parameters and represent the point where instance data enters the network.</span></span> 
* <span data-ttu-id="8cf77-145">可訓練層 (隱藏層和輸出層) 具有相關聯的訓練參數，一般稱之為加權和偏差。</span><span class="sxs-lookup"><span data-stu-id="8cf77-145">Trainable layers (the hidden and output layers) have associated trained parameters, known as weights and biases.</span></span> 
* <span data-ttu-id="8cf77-146">來源和目的地節點必須位於不同層內。</span><span class="sxs-lookup"><span data-stu-id="8cf77-146">The source and destination nodes must be in separate layers.</span></span> 
* <span data-ttu-id="8cf77-147">連線必須是非循環的，換句話說，連線不可以有往回導向至初始來源節點的鏈結。</span><span class="sxs-lookup"><span data-stu-id="8cf77-147">Connections must be acyclic; in other words, there cannot be a chain of connections leading back to the initial source node.</span></span>
* <span data-ttu-id="8cf77-148">輸出層不可以是連線套組的來源層。</span><span class="sxs-lookup"><span data-stu-id="8cf77-148">The output layer cannot be a source layer of a connection bundle.</span></span>  

## <a name="structure-specifications"></a><span data-ttu-id="8cf77-149">結構規格</span><span class="sxs-lookup"><span data-stu-id="8cf77-149">Structure specifications</span></span>
<span data-ttu-id="8cf77-150">類神經網路結構規格由三個區段所組成：**常數宣告**、**層宣告**和**連線宣告**。</span><span class="sxs-lookup"><span data-stu-id="8cf77-150">A neural network structure specification is composed of three sections: the **constant declaration**, the **layer declaration**, the **connection declaration**.</span></span> <span data-ttu-id="8cf77-151">另外還有一個選擇性的**共用宣告**區段。</span><span class="sxs-lookup"><span data-stu-id="8cf77-151">There is also an optional **share declaration** section.</span></span> <span data-ttu-id="8cf77-152">這幾個部分可依任意順序指定。</span><span class="sxs-lookup"><span data-stu-id="8cf77-152">The sections can be specified in any order.</span></span>  

## <a name="constant-declaration"></a><span data-ttu-id="8cf77-153">常數宣告</span><span class="sxs-lookup"><span data-stu-id="8cf77-153">Constant declaration</span></span>
<span data-ttu-id="8cf77-154">常數宣告是選擇性宣告。</span><span class="sxs-lookup"><span data-stu-id="8cf77-154">A constant declaration is optional.</span></span> <span data-ttu-id="8cf77-155">它提供的機制可用來定義在類神經網路定義中使用的值。</span><span class="sxs-lookup"><span data-stu-id="8cf77-155">It provides a means to define values used elsewhere in the neural network definition.</span></span> <span data-ttu-id="8cf77-156">宣告陳述式的組成元素是識別碼之後尾隨加號和值運算式。</span><span class="sxs-lookup"><span data-stu-id="8cf77-156">The declaration statement consists of an identifier followed by an equal sign and a value expression.</span></span>   

<span data-ttu-id="8cf77-157">例如，下列陳述式會定義常數 **x**：</span><span class="sxs-lookup"><span data-stu-id="8cf77-157">For example, the following statement defines a constant **x**:</span></span>  

    Const X = 28;  

<span data-ttu-id="8cf77-158">若要同時定義兩個或更多常數，請將識別碼名稱和值放在大括號中，並使用分號分隔。</span><span class="sxs-lookup"><span data-stu-id="8cf77-158">To define two or more constants simultaneously, enclose the identifier names and values in braces, and separate them by using semicolons.</span></span> <span data-ttu-id="8cf77-159">例如：</span><span class="sxs-lookup"><span data-stu-id="8cf77-159">For example:</span></span>  

    Const { X = 28; Y = 4; }  

<span data-ttu-id="8cf77-160">各個指派運算式的右側可以是整數、實數、布林值 (True/False) 或數學運算式。</span><span class="sxs-lookup"><span data-stu-id="8cf77-160">The right-hand side of each assignment expression can be an integer, a real number, a Boolean value (True or False), or a mathematical expression.</span></span> <span data-ttu-id="8cf77-161">例如：</span><span class="sxs-lookup"><span data-stu-id="8cf77-161">For example:</span></span>  

    Const { X = 17 * 2; Y = true; }  

## <a name="layer-declaration"></a><span data-ttu-id="8cf77-162">層宣告</span><span class="sxs-lookup"><span data-stu-id="8cf77-162">Layer declaration</span></span>
<span data-ttu-id="8cf77-163">層宣告是必要宣告。</span><span class="sxs-lookup"><span data-stu-id="8cf77-163">The layer declaration is required.</span></span> <span data-ttu-id="8cf77-164">它定義層的大小和來源，包括層的連線套組和屬性。</span><span class="sxs-lookup"><span data-stu-id="8cf77-164">It defines the size and source of the layer, including its connection bundles and attributes.</span></span> <span data-ttu-id="8cf77-165">宣告陳述式以層的名稱開頭 (輸入、隱藏或輸出)，其後是層的維度 (正整數的 Tuple)。</span><span class="sxs-lookup"><span data-stu-id="8cf77-165">The declaration statement starts with the name of the layer (input, hidden, or output), followed by the dimensions of the layer (a tuple of positive integers).</span></span> <span data-ttu-id="8cf77-166">例如：</span><span class="sxs-lookup"><span data-stu-id="8cf77-166">For example:</span></span>  

    input Data auto;
    hidden Hidden[5,20] from Data all;
    output Result[2] from Hidden all;  

* <span data-ttu-id="8cf77-167">維度的乘積為層中的節點數目。</span><span class="sxs-lookup"><span data-stu-id="8cf77-167">The product of the dimensions is the number of nodes in the layer.</span></span> <span data-ttu-id="8cf77-168">此範例中有兩個維度 [5,20]，這表示層中有 100 個節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-168">In this example, there are two dimensions [5,20], which means there are  100 nodes in the layer.</span></span>
* <span data-ttu-id="8cf77-169">層能以任何順序宣告，僅有一項例外：如果定義了多個輸入層，則這些層的宣告順序必須符合輸入資料中各項特性的順序。</span><span class="sxs-lookup"><span data-stu-id="8cf77-169">The layers can be declared in any order, with one exception: If more than one input layer is defined, the order in which they are declared must match the order of features in the input data.</span></span>  

<span data-ttu-id="8cf77-170">若要指定讓系統自動決定層中的節點數目，請使用 **auto** 關鍵字。</span><span class="sxs-lookup"><span data-stu-id="8cf77-170">To specify that the number of nodes in a layer be determined automatically, use the **auto** keyword.</span></span> <span data-ttu-id="8cf77-171">**auto** 關鍵字的效果會隨著層而不同：</span><span class="sxs-lookup"><span data-stu-id="8cf77-171">The **auto** keyword has different effects, depending on the layer:</span></span>  

* <span data-ttu-id="8cf77-172">在輸入層宣告中，節點數目是輸入資料中的特性數目。</span><span class="sxs-lookup"><span data-stu-id="8cf77-172">In an input layer declaration, the number of nodes is the number of features in the input data.</span></span>
* <span data-ttu-id="8cf77-173">在隱藏層宣告中，節點數目是**隱藏節點數目**的參數值所指定的數目。</span><span class="sxs-lookup"><span data-stu-id="8cf77-173">In a hidden layer declaration, the number of nodes is the number that is specified by the parameter value for **Number of hidden nodes**.</span></span> 
* <span data-ttu-id="8cf77-174">在輸出層宣告中，雙類別分類的節點數目是 2 個 (1 個用於迴歸)，且等於多類別分類的輸出節點數目。</span><span class="sxs-lookup"><span data-stu-id="8cf77-174">In an output layer declaration, the number of nodes is 2 for two-class classification, 1 for regression, and equal to the number of output nodes for multiclass classification.</span></span>   

<span data-ttu-id="8cf77-175">例如，下列網路定義會讓系統自動決定所有層的大小：</span><span class="sxs-lookup"><span data-stu-id="8cf77-175">For example, the following network definition allows the size of all layers to be automatically determined:</span></span>  

    input Data auto;
    hidden Hidden auto from Data all;
    output Result auto from Hidden all;  


<span data-ttu-id="8cf77-176">可訓練層 (隱藏層或輸出層) 的層宣告可選擇性地包含輸出函數 (也稱為啟用函數)，其預設值為適用於分類模型的 **sigmoid** 以及適用於迴歸模型的 **linear**。</span><span class="sxs-lookup"><span data-stu-id="8cf77-176">A layer declaration for a trainable layer (the hidden or output layers) can optionally include the output function (also called an activation function), which defaults to **sigmoid** for classification models, and **linear** for regression models.</span></span> <span data-ttu-id="8cf77-177">(即使您使用預設值，您也可以在需要釐清時明確陳述啟用函數。)</span><span class="sxs-lookup"><span data-stu-id="8cf77-177">(Even if you use the default, you can explicitly state the activation function, if desired for clarity.)</span></span>

<span data-ttu-id="8cf77-178">支援的輸出函數如下：</span><span class="sxs-lookup"><span data-stu-id="8cf77-178">The following output functions are supported:</span></span>  

* <span data-ttu-id="8cf77-179">sigmoid</span><span class="sxs-lookup"><span data-stu-id="8cf77-179">sigmoid</span></span>
* <span data-ttu-id="8cf77-180">linear</span><span class="sxs-lookup"><span data-stu-id="8cf77-180">linear</span></span>
* <span data-ttu-id="8cf77-181">softmax</span><span class="sxs-lookup"><span data-stu-id="8cf77-181">softmax</span></span>
* <span data-ttu-id="8cf77-182">rlinear</span><span class="sxs-lookup"><span data-stu-id="8cf77-182">rlinear</span></span>
* <span data-ttu-id="8cf77-183">square</span><span class="sxs-lookup"><span data-stu-id="8cf77-183">square</span></span>
* <span data-ttu-id="8cf77-184">sqrt</span><span class="sxs-lookup"><span data-stu-id="8cf77-184">sqrt</span></span>
* <span data-ttu-id="8cf77-185">srlinear</span><span class="sxs-lookup"><span data-stu-id="8cf77-185">srlinear</span></span>
* <span data-ttu-id="8cf77-186">abs</span><span class="sxs-lookup"><span data-stu-id="8cf77-186">abs</span></span>
* <span data-ttu-id="8cf77-187">tanh</span><span class="sxs-lookup"><span data-stu-id="8cf77-187">tanh</span></span> 
* <span data-ttu-id="8cf77-188">brlinear</span><span class="sxs-lookup"><span data-stu-id="8cf77-188">brlinear</span></span>  

<span data-ttu-id="8cf77-189">例如，下列宣告將使用 **softmax** 函數：</span><span class="sxs-lookup"><span data-stu-id="8cf77-189">For example, the following declaration uses the **softmax** function:</span></span>  

    output Result [100] softmax from Hidden all;  

## <a name="connection-declaration"></a><span data-ttu-id="8cf77-190">連線宣告</span><span class="sxs-lookup"><span data-stu-id="8cf77-190">Connection declaration</span></span>
<span data-ttu-id="8cf77-191">在定義可訓練層之後，您必須隨即宣告您所定義的層之間的連線。</span><span class="sxs-lookup"><span data-stu-id="8cf77-191">Immediately after defining the trainable layer, you must declare connections among the layers you have defined.</span></span> <span data-ttu-id="8cf77-192">連線套組宣告以關鍵字 **from** 開頭，其後是套組的來源層名稱和所要建立的連線套組類型。</span><span class="sxs-lookup"><span data-stu-id="8cf77-192">The connection bundle declaration starts with the keyword **from**, followed by the name of the bundle's source layer and the kind of connection bundle to create.</span></span>   

<span data-ttu-id="8cf77-193">目前支援五種連線套組：</span><span class="sxs-lookup"><span data-stu-id="8cf77-193">Currently, five kinds of connection bundles are supported:</span></span>  

* <span data-ttu-id="8cf77-194">**完整**套組，以關鍵字 **all** 指出</span><span class="sxs-lookup"><span data-stu-id="8cf77-194">**Full** bundles, indicated by the keyword **all**</span></span>
* <span data-ttu-id="8cf77-195">**篩選**套組，以關鍵字 **where** 指出，其後接著述詞運算式</span><span class="sxs-lookup"><span data-stu-id="8cf77-195">**Filtered** bundles, indicated by the keyword **where**, followed by a predicate expression</span></span>
* <span data-ttu-id="8cf77-196">**迴旋**套組，以關鍵字 **convolve** 指出，其後接著迴旋屬性</span><span class="sxs-lookup"><span data-stu-id="8cf77-196">**Convolutional** bundles, indicated by the keyword **convolve**, followed by the convolution attributes</span></span>
* <span data-ttu-id="8cf77-197">**集區**套組，以關鍵字 **max pool** 或 **mean pool** 指出</span><span class="sxs-lookup"><span data-stu-id="8cf77-197">**Pooling** bundles, indicated by the keywords **max pool** or **mean pool**</span></span>
* <span data-ttu-id="8cf77-198">**回應正規化**套組，以關鍵字 **response norm** 指出。</span><span class="sxs-lookup"><span data-stu-id="8cf77-198">**Response normalization** bundles, indicated by the keyword **response norm**</span></span>      

## <a name="full-bundles"></a><span data-ttu-id="8cf77-199">完整套組</span><span class="sxs-lookup"><span data-stu-id="8cf77-199">Full bundles</span></span>
<span data-ttu-id="8cf77-200">完整連線套組包含從來源層中的每個節點連至目的地層中各個節點的連線。</span><span class="sxs-lookup"><span data-stu-id="8cf77-200">A full connection bundle includes a connection from each node in the source layer to each node in the destination layer.</span></span> <span data-ttu-id="8cf77-201">這是預設的網路連線類型。</span><span class="sxs-lookup"><span data-stu-id="8cf77-201">This is the default network connection type.</span></span>  

## <a name="filtered-bundles"></a><span data-ttu-id="8cf77-202">篩選套組</span><span class="sxs-lookup"><span data-stu-id="8cf77-202">Filtered bundles</span></span>
<span data-ttu-id="8cf77-203">篩選連線套組規格包含一個述詞，此述詞在語法上的表示方式非常類似 C# lambda 運算式。</span><span class="sxs-lookup"><span data-stu-id="8cf77-203">A filtered connection bundle specification includes a predicate, expressed syntactically, much like a C# lambda expression.</span></span> <span data-ttu-id="8cf77-204">以下範例將定義兩個篩選套組：</span><span class="sxs-lookup"><span data-stu-id="8cf77-204">The following example defines two filtered bundles:</span></span>  

    input Pixels [10, 20];
    hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  

* <span data-ttu-id="8cf77-205">在 *ByRow* 的述詞中 **s** 參數代表輸入層 *Pixels* 之節點矩形陣列的索引，而 **d** 參數代表隱藏層 *ByRow* 之節點陣列的索引。</span><span class="sxs-lookup"><span data-stu-id="8cf77-205">In the predicate for *ByRow*, **s** is a parameter representing an index into the rectangular array of nodes of the input layer, *Pixels*, and **d** is a parameter representing an index into the array of nodes of the hidden layer, *ByRow*.</span></span> <span data-ttu-id="8cf77-206">**s** 和 **d** 的類型為長度二之整數的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-206">The type of both **s** and **d** is a tuple of integers of length two.</span></span> <span data-ttu-id="8cf77-207">在概念上，**s** 的範圍介於所有 *0 <= s[0] < 10* 與 *0 <= s[1] < 20* 的整數對之間，而且 **d** 的範圍介於所有 *0 <= d[0] < 10* 與 *0 <= d[1] < 12* 的整數對之間。</span><span class="sxs-lookup"><span data-stu-id="8cf77-207">Conceptually, **s** ranges over all pairs of integers with *0 <= s[0] < 10* and *0 <= s[1] < 20*, and **d** ranges over all pairs of integers, with *0 <= d[0] < 10* and *0 <= d[1] < 12*.</span></span> 
* <span data-ttu-id="8cf77-208">述詞運算式右側會有一個條件。</span><span class="sxs-lookup"><span data-stu-id="8cf77-208">On the right-hand side of the predicate expression, there is a condition.</span></span> <span data-ttu-id="8cf77-209">在此範例中，每個條件為 True 的 **s** 值和 **d** 值都會有一個從來源層節點到目的地層節點的邊緣。</span><span class="sxs-lookup"><span data-stu-id="8cf77-209">In this example, for every value of **s** and **d** such that the condition is True, there is an edge from the source layer node to the destination layer node.</span></span> <span data-ttu-id="8cf77-210">因此，此篩選運算式表示在 s[0] 等於 d[0] 的所有情況下，套組都會包含從 **s** 所定義的節點到 **d** 所定義之節點的連線。</span><span class="sxs-lookup"><span data-stu-id="8cf77-210">Thus, this filter expression indicates that the bundle includes a connection from the node defined by **s** to the node defined by **d** in all cases where s[0] is equal to d[0].</span></span>  

<span data-ttu-id="8cf77-211">您可以選擇性地為篩選套組指定一組加權。</span><span class="sxs-lookup"><span data-stu-id="8cf77-211">Optionally, you can specify a set of weights for a filtered bundle.</span></span> <span data-ttu-id="8cf77-212">**Weights** 屬性的值必須是長度與套組所定義的連線數目相符之浮點值的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-212">The value for the **Weights** attribute must be a tuple of floating point values with a length that matches the number of connections defined by the bundle.</span></span> <span data-ttu-id="8cf77-213">依預設會隨機產生加權。</span><span class="sxs-lookup"><span data-stu-id="8cf77-213">By default, weights are randomly generated.</span></span>  

<span data-ttu-id="8cf77-214">加權值會依目的地節點索引分組。</span><span class="sxs-lookup"><span data-stu-id="8cf77-214">Weight values are grouped by the destination node index.</span></span> <span data-ttu-id="8cf77-215">也就是說，如果第一個目的地節點連接到 *K* 個來源節點，則**加權** Tuple 的前 K 個項目將會是第一個目的地節點的加權 (依來源索引順序)。</span><span class="sxs-lookup"><span data-stu-id="8cf77-215">That is, if the first destination node is connected to K source nodes, the first *K* elements of the **Weights** tuple are the weights for the first destination node, in source index order.</span></span> <span data-ttu-id="8cf77-216">其餘目的地節點也適用相同的原則。</span><span class="sxs-lookup"><span data-stu-id="8cf77-216">The same applies for the remaining destination nodes.</span></span>  

<span data-ttu-id="8cf77-217">可以直接指定加權當做常數值。</span><span class="sxs-lookup"><span data-stu-id="8cf77-217">It's possible to specify weights directly as constant values.</span></span> <span data-ttu-id="8cf77-218">比方說，如果您先前已了解比重，您可以使用此語法將它們指定為常數：</span><span class="sxs-lookup"><span data-stu-id="8cf77-218">For example, if you learned the weights previously, you can specify them as constants using this syntax:</span></span>

    const Weights_1 = [0.0188045055, 0.130500451, ...]


## <a name="convolutional-bundles"></a><span data-ttu-id="8cf77-219">迴旋套組</span><span class="sxs-lookup"><span data-stu-id="8cf77-219">Convolutional bundles</span></span>
<span data-ttu-id="8cf77-220">當訓練資料具有同質結構時，迴旋連線通常會用來學習資料的高階特性。</span><span class="sxs-lookup"><span data-stu-id="8cf77-220">When the training data has a homogeneous structure, convolutional connections are commonly used to learn high-level features of the data.</span></span> <span data-ttu-id="8cf77-221">例如，在影像、音訊或視訊資料中，空間或暫時維度可能會相當一致。</span><span class="sxs-lookup"><span data-stu-id="8cf77-221">For example, in image, audio, or video data, spatial or temporal dimensionality can be fairly uniform.</span></span>  

<span data-ttu-id="8cf77-222">迴旋套組採用滑經維度的矩形**核心**。</span><span class="sxs-lookup"><span data-stu-id="8cf77-222">Convolutional bundles employ rectangular **kernels** that are slid through the dimensions.</span></span> <span data-ttu-id="8cf77-223">基本上，每個核心會定義一組在本端鄰區中套用的加權，稱為**核心應用程式**。</span><span class="sxs-lookup"><span data-stu-id="8cf77-223">Essentially, each kernel defines a set of weights applied in local neighborhoods, referred to as **kernel applications**.</span></span> <span data-ttu-id="8cf77-224">每個核心應用程式都會對應至來源層中名為**中心節點**的節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-224">Each kernel application corresponds to a node in the source layer, which is referred to as the **central node**.</span></span> <span data-ttu-id="8cf77-225">一個核心的加權會在許多連線間共用。</span><span class="sxs-lookup"><span data-stu-id="8cf77-225">The weights of a kernel are shared among many connections.</span></span> <span data-ttu-id="8cf77-226">在迴旋套組中，每個核心都是矩形，且所有核心應用程式的大小皆相同。</span><span class="sxs-lookup"><span data-stu-id="8cf77-226">In a convolutional bundle, each kernel is rectangular and all kernel applications are the same size.</span></span>  

<span data-ttu-id="8cf77-227">迴旋套組支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="8cf77-227">Convolutional bundles support the following attributes:</span></span>

<span data-ttu-id="8cf77-228">**InputShape** 會針對此迴旋套組的用途，定義來源層的維度。</span><span class="sxs-lookup"><span data-stu-id="8cf77-228">**InputShape** defines the dimensionality of the source layer for the purposes of this convolutional bundle.</span></span> <span data-ttu-id="8cf77-229">其值必須是正整數的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-229">The value must be a tuple of positive integers.</span></span> <span data-ttu-id="8cf77-230">整數的乘積必須等於來源層中的節點數目，但另一方面並不需要符合為來源層宣告的維度。</span><span class="sxs-lookup"><span data-stu-id="8cf77-230">The product of the integers must equal the number of nodes in the source layer, but otherwise, it does not need to match the dimensionality declared for the source layer.</span></span> <span data-ttu-id="8cf77-231">此 Tuple 的長度會成為迴旋套組的 **Arity** 值。</span><span class="sxs-lookup"><span data-stu-id="8cf77-231">The length of this tuple becomes the **arity** value for the convolutional bundle.</span></span> <span data-ttu-id="8cf77-232">(Arity 通常會參照一個函數可取用的引數或運算元數目。)</span><span class="sxs-lookup"><span data-stu-id="8cf77-232">(Typically arity refers to the number of arguments or operands that a function can take.)</span></span>  

<span data-ttu-id="8cf77-233">若要定義核心的形狀和位置，請使用 **KernelShape**、**Stride**、**Padding**、**LowerPad** 和 **UpperPad** 等屬性：</span><span class="sxs-lookup"><span data-stu-id="8cf77-233">To define the shape and locations of the kernels, use the attributes **KernelShape**, **Stride**, **Padding**, **LowerPad**, and **UpperPad**:</span></span>   

* <span data-ttu-id="8cf77-234">**KernelShape**：(必要) 定義迴旋套組各個核心的維度。</span><span class="sxs-lookup"><span data-stu-id="8cf77-234">**KernelShape**: (required) Defines the dimensionality of each kernel for the convolutional bundle.</span></span> <span data-ttu-id="8cf77-235">其值必須是長度等於套組 Arity 之正整數的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-235">The value must be a tuple of positive integers with a length that equals the arity of the bundle.</span></span> <span data-ttu-id="8cf77-236">此 Tuple 的每個元件皆不可大於 **InputShape** 的對應元件。</span><span class="sxs-lookup"><span data-stu-id="8cf77-236">Each component of this tuple must be no greater than the corresponding component of **InputShape**.</span></span> 
* <span data-ttu-id="8cf77-237">**Stride**：(選用) 定義迴旋的滑動步階大小 (每個維度的步階大小)，即中心節點之間的距離。</span><span class="sxs-lookup"><span data-stu-id="8cf77-237">**Stride**: (optional) Defines the sliding step sizes of the convolution (one step size for each dimension), that is the distance between the central nodes.</span></span> <span data-ttu-id="8cf77-238">其值必須是長度為套組 Arity 之正整數的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-238">The value must be a tuple of positive integers with a length that is the arity of the bundle.</span></span> <span data-ttu-id="8cf77-239">此 Tuple 的每個元件皆不可大於 **KernelShape** 的對應元件。</span><span class="sxs-lookup"><span data-stu-id="8cf77-239">Each component of this tuple must be no greater than the corresponding component of **KernelShape**.</span></span> <span data-ttu-id="8cf77-240">預設值是所有元件皆等於一的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-240">The default value is a tuple with all components equal to one.</span></span> 
* <span data-ttu-id="8cf77-241">**Sharing**：(選用) 為迴旋的每個維度定義加權共用。</span><span class="sxs-lookup"><span data-stu-id="8cf77-241">**Sharing**: (optional) Defines the weight sharing for each dimension of the convolution.</span></span> <span data-ttu-id="8cf77-242">其值可以是單一布林值，或是長度為套組 Arity 之布林值的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-242">The value can be a single Boolean value or a tuple of Boolean values with a length that is the arity of the bundle.</span></span> <span data-ttu-id="8cf77-243">單一布林值可擴充為具有正確長度、所有元件皆等於指定值的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-243">A single Boolean value is extended to be a tuple of the correct length with all components equal to the specified value.</span></span> <span data-ttu-id="8cf77-244">預設值是全部由 True 值組成的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-244">The default value is a tuple that consists of all True values.</span></span> 
* <span data-ttu-id="8cf77-245">**MapCount**：(選用) 定義迴旋套組的特性對應數目。</span><span class="sxs-lookup"><span data-stu-id="8cf77-245">**MapCount**: (optional) Defines the number of feature maps for the convolutional bundle.</span></span> <span data-ttu-id="8cf77-246">其值可以是單一正整數，或是長度為套組 Arity 之正整數的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-246">The value can be a single positive integer or a tuple of positive integers with a length that is the arity of the bundle.</span></span> <span data-ttu-id="8cf77-247">單一整數值可擴充為具有正確長度、第一個元件皆等於指定值且其餘元件皆等於一的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-247">A single integer value is extended to be a tuple of the correct length with the first components equal to the specified value and all the remaining components equal to one.</span></span> <span data-ttu-id="8cf77-248">預設值為一。</span><span class="sxs-lookup"><span data-stu-id="8cf77-248">The default value is one.</span></span> <span data-ttu-id="8cf77-249">特性對應的總數是 Tuple 元件的乘積。</span><span class="sxs-lookup"><span data-stu-id="8cf77-249">The total number of feature maps is the product of the components of the tuple.</span></span> <span data-ttu-id="8cf77-250">各個元件的此一總數經過因式分解後，將決定特性對應值在目的地節點中的分組方式。</span><span class="sxs-lookup"><span data-stu-id="8cf77-250">The factoring of this total number across the components determines how the feature map values are grouped in the destination nodes.</span></span> 
* <span data-ttu-id="8cf77-251">**Weights**：(選用) 定義套組的初始加權。</span><span class="sxs-lookup"><span data-stu-id="8cf77-251">**Weights**: (optional) Defines the initial weights for the bundle.</span></span> <span data-ttu-id="8cf77-252">其值必須是長度為核心數目乘以每個核心的加權數目之浮點值的 Tuple，如本文稍後的定義。</span><span class="sxs-lookup"><span data-stu-id="8cf77-252">The value must be a tuple of floating point values with a length that is the number of kernels times the number of weights per kernel, as defined later in this article.</span></span> <span data-ttu-id="8cf77-253">預設加權會隨機產生。</span><span class="sxs-lookup"><span data-stu-id="8cf77-253">The default weights are randomly generated.</span></span>  

<span data-ttu-id="8cf77-254">有兩組屬性控制填補，這些屬性互斥：</span><span class="sxs-lookup"><span data-stu-id="8cf77-254">There are two sets of properties that control padding, the properties being mutually exclusive:</span></span>

* <span data-ttu-id="8cf77-255">**Padding**：(選用) 決定是否應使用**預設的填補配置**填補輸入。</span><span class="sxs-lookup"><span data-stu-id="8cf77-255">**Padding**: (optional) Determines whether the input should be padded by using a **default padding scheme**.</span></span> <span data-ttu-id="8cf77-256">其值可以是單一布林值，或是長度為套組 Arity 之布林值的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-256">The value can be a single Boolean value, or it can be a tuple of Boolean values with a length that is the arity of the bundle.</span></span> <span data-ttu-id="8cf77-257">單一布林值可擴充為具有正確長度、所有元件皆等於指定值的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-257">A single Boolean value is extended to be a tuple of the correct length with all components equal to the specified value.</span></span> <span data-ttu-id="8cf77-258">如果維度的值為 True，則來源在邏輯上會以零值儲存格在該維度中進行填補，以支援其他核心應用程式，使該維度中第一個和最後一個核心的中心節點成為該維度在來源層中的第一個和最後一個節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-258">If the value for a dimension is True, the source is logically padded in that dimension with zero-valued cells to support additional kernel applications, such that the central nodes of the first and last kernels in that dimension are the first and last nodes in that dimension in the source layer.</span></span> <span data-ttu-id="8cf77-259">據此將會自動產生每個維度中的「虛擬」節點數目，以將 *(InputShape[d] - 1) / Stride[d] + 1* 個核心配適到已填補的來源層中。</span><span class="sxs-lookup"><span data-stu-id="8cf77-259">Thus, the number of "dummy" nodes in each dimension is determined automatically, to fit exactly *(InputShape[d] - 1) / Stride[d] + 1* kernels into the padded source layer.</span></span> <span data-ttu-id="8cf77-260">如果維度的值為 False，則在定義核心時，會使每一端排除的節點數目保持相同 (差距不會超過 1 個)。</span><span class="sxs-lookup"><span data-stu-id="8cf77-260">If the value for a dimension is False, the kernels are defined so that the number of nodes on each side that are left out is the same (up to a difference of 1).</span></span> <span data-ttu-id="8cf77-261">此屬性的預設值是所有元件皆為 False 的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-261">The default value of this attribute is a tuple with all components equal to False.</span></span>
* <span data-ttu-id="8cf77-262">**UpperPad** 和 **LowerPad**：(選用) 更能控制所要使用的填補量。</span><span class="sxs-lookup"><span data-stu-id="8cf77-262">**UpperPad** and **LowerPad**: (optional) Provide greater control over the amount of padding to use.</span></span> <span data-ttu-id="8cf77-263">**重要事項：**只有在***未***定義上述的 **Padding** 屬性時，才能定義這些屬性。</span><span class="sxs-lookup"><span data-stu-id="8cf77-263">**Important:** These attributes can be defined if and only if the **Padding** property above is ***not*** defined.</span></span> <span data-ttu-id="8cf77-264">其值應為長度為套組 Arity 的整數值 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-264">The values should be integer-valued tuples with lengths that are the arity of the bundle.</span></span> <span data-ttu-id="8cf77-265">在指定這些屬性時，將會在輸入層各個維度的下端和上端新增「虛擬」節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-265">When these attributes are specified, "dummy" nodes are added to the lower and upper ends of each dimension of the input layer.</span></span> <span data-ttu-id="8cf77-266">在每個維度中的下端和上端新增的節點數目，分別取決於 **LowerPad**[i] 和 **UpperPad**[i]。</span><span class="sxs-lookup"><span data-stu-id="8cf77-266">The number of nodes added to the lower and upper ends in each dimension is determined by **LowerPad**[i] and **UpperPad**[i] respectively.</span></span> <span data-ttu-id="8cf77-267">若要確定核心只會對應至「實際」節點而非「虛擬」節點，必須要符合下列條件：</span><span class="sxs-lookup"><span data-stu-id="8cf77-267">To ensure that kernels correspond only to "real" nodes and not to "dummy" nodes, the following conditions must be met:</span></span>
  * <span data-ttu-id="8cf77-268">**LowerPad** 的每個元件皆務必小於 KernelShape[d]/2。</span><span class="sxs-lookup"><span data-stu-id="8cf77-268">Each component of **LowerPad** must be strictly less than KernelShape[d]/2.</span></span> 
  * <span data-ttu-id="8cf77-269">**UpperPad** 的每個元件皆不可大於 KernelShape[d]/2。</span><span class="sxs-lookup"><span data-stu-id="8cf77-269">Each component of **UpperPad** must be no greater than KernelShape[d]/2.</span></span> 
  * <span data-ttu-id="8cf77-270">這些屬性的預設值是所有元件皆等於 0 的 Tuple。</span><span class="sxs-lookup"><span data-stu-id="8cf77-270">The default value of these attributes is a tuple with all components equal to 0.</span></span> 

<span data-ttu-id="8cf77-271">**Padding** = true 設定允許可將核心的「中心」保持在「真實」輸入內所需的填補量。</span><span class="sxs-lookup"><span data-stu-id="8cf77-271">The setting **Padding** = true allows as much padding as is needed to keep the "center" of the kernel inside the "real" input.</span></span> <span data-ttu-id="8cf77-272">這麼做會略為改變輸出大小的計算方式。</span><span class="sxs-lookup"><span data-stu-id="8cf77-272">This changes the math a bit for computing the output size.</span></span> <span data-ttu-id="8cf77-273">一般而言，輸出大小 *D* 的計算方式為 *D = (I - K) / S + 1*，其中 *I* 是輸入大小，*K* 是核心大小，*S* 是分散，而 */* 是整數除法 (趨近於零)。</span><span class="sxs-lookup"><span data-stu-id="8cf77-273">Generally, the output size *D* is computed as *D = (I - K) / S + 1*, where *I* is the input size, *K* is the kernel size, *S* is the stride, and */* is integer division (round toward zero).</span></span> <span data-ttu-id="8cf77-274">如果您設定 UpperPad = [1, 1]，輸入大小 *I* 實際上是 29，因此 *D = (29 - 5) / 2 + 1 = 13*。</span><span class="sxs-lookup"><span data-stu-id="8cf77-274">If you set UpperPad = [1, 1], the input size *I* is effectively 29, and thus *D = (29 - 5) / 2 + 1 = 13*.</span></span> <span data-ttu-id="8cf77-275">不過，當 **Padding** = true 時，基本上 *I* 會藉由 *K - 1* 而提高；因此 *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*。</span><span class="sxs-lookup"><span data-stu-id="8cf77-275">However, when **Padding** = true, essentially *I* gets bumped up by *K - 1*; hence *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*.</span></span> <span data-ttu-id="8cf77-276">藉由指定 **UpperPad** 和 **LowerPad** 的值，您對填補的控制權會遠遠超過只設定 **Padding** = true。</span><span class="sxs-lookup"><span data-stu-id="8cf77-276">By specifying values for **UpperPad** and **LowerPad** you get much more control over the padding than if you just set **Padding** = true.</span></span>

<span data-ttu-id="8cf77-277">如需迴旋網路及其應用程式的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="8cf77-277">For more information about convolutional networks and their applications, see these articles:</span></span>  

* [<span data-ttu-id="8cf77-278">http://deeplearning.net/tutorial/lenet.html </span><span class="sxs-lookup"><span data-stu-id="8cf77-278">http://deeplearning.net/tutorial/lenet.html </span></span>](http://deeplearning.net/tutorial/lenet.html)
* [<span data-ttu-id="8cf77-279">http://research.microsoft.com/pubs/68920/icdar03.pdf</span><span class="sxs-lookup"><span data-stu-id="8cf77-279">http://research.microsoft.com/pubs/68920/icdar03.pdf</span></span>](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
* [<span data-ttu-id="8cf77-280">http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf</span><span class="sxs-lookup"><span data-stu-id="8cf77-280">http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf</span></span>](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a><span data-ttu-id="8cf77-281">集區套組</span><span class="sxs-lookup"><span data-stu-id="8cf77-281">Pooling bundles</span></span>
<span data-ttu-id="8cf77-282">**集區套組**會套用類似於迴旋連線的幾何圖形，但會對來源節點值使用預先定義的函數，以衍生目的地節點值。</span><span class="sxs-lookup"><span data-stu-id="8cf77-282">A **pooling bundle** applies geometry similar to convolutional connectivity, but it uses predefined functions to source node values to derive the destination node value.</span></span> <span data-ttu-id="8cf77-283">因此，集區套組並沒有可訓練的狀態 (加權或偏差)。</span><span class="sxs-lookup"><span data-stu-id="8cf77-283">Hence, pooling bundles have no trainable state (weights or biases).</span></span> <span data-ttu-id="8cf77-284">集區套組支援 **Sharing**、**MapCount** 和 **Weights** 以外的所有迴旋屬性。</span><span class="sxs-lookup"><span data-stu-id="8cf77-284">Pooling bundles support all the convolutional attributes except **Sharing**, **MapCount**, and **Weights**.</span></span>  

<span data-ttu-id="8cf77-285">一般而言，以相鄰集區單元彙總的核心並不會重疊。</span><span class="sxs-lookup"><span data-stu-id="8cf77-285">Typically, the kernels summarized by adjacent pooling units do not overlap.</span></span> <span data-ttu-id="8cf77-286">如果每個維度中的 Stride[d] 皆等於 KernelShape[d]，則取得的層將會是傳統本端集區層，這通常運用在迴旋類神經網路中。</span><span class="sxs-lookup"><span data-stu-id="8cf77-286">If Stride[d] is equal to KernelShape[d] in each dimension, the layer obtained is the traditional local pooling layer, which is commonly employed in convolutional neural networks.</span></span> <span data-ttu-id="8cf77-287">每個目的地節點都會計算其核心在來源層中的活動數上限或平均值。</span><span class="sxs-lookup"><span data-stu-id="8cf77-287">Each destination node computes the maximum or the mean of the activities of its kernel in the source layer.</span></span>  

<span data-ttu-id="8cf77-288">以下透過範例說明集區套組：</span><span class="sxs-lookup"><span data-stu-id="8cf77-288">The following example illustrates a pooling bundle:</span></span> 

    hidden P1 [5, 12, 12]
      from C1 max pool {
        InputShape  = [ 5, 24, 24];
        KernelShape = [ 1,  2,  2];
        Stride      = [ 1,  2,  2];
      }  

* <span data-ttu-id="8cf77-289">套組的 Arity 為 3 (Tuple **InputShape**、**KernelShape** 和 **Stride** 的長度)。</span><span class="sxs-lookup"><span data-stu-id="8cf77-289">The arity of the bundle is 3 (the length of the tuples **InputShape**, **KernelShape**, and **Stride**).</span></span> 
* <span data-ttu-id="8cf77-290">來源層中的節點數目為 *5 * 24 * 24 = 2880*。</span><span class="sxs-lookup"><span data-stu-id="8cf77-290">The number of nodes in the source layer is *5 * 24 * 24 = 2880*.</span></span> 
* <span data-ttu-id="8cf77-291">這是傳統本端集區層，因為 **KernelShape** 和 **Stride** 是相等的。</span><span class="sxs-lookup"><span data-stu-id="8cf77-291">This is a traditional local pooling layer because **KernelShape** and **Stride** are equal.</span></span> 
* <span data-ttu-id="8cf77-292">目的地層中的節點數目為 *5 * 12 * 12 = 1440*。</span><span class="sxs-lookup"><span data-stu-id="8cf77-292">The number of nodes in the destination layer is *5 * 12 * 12 = 1440*.</span></span>  

<span data-ttu-id="8cf77-293">如需集區層的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="8cf77-293">For more information about pooling layers, see these articles:</span></span>  

* <span data-ttu-id="8cf77-294">[http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (3.4 小節)</span><span class="sxs-lookup"><span data-stu-id="8cf77-294">[http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (Section 3.4)</span></span>
* [<span data-ttu-id="8cf77-295">http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf</span><span class="sxs-lookup"><span data-stu-id="8cf77-295">http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf</span></span>](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
* [<span data-ttu-id="8cf77-296">http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf</span><span class="sxs-lookup"><span data-stu-id="8cf77-296">http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf</span></span>](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a><span data-ttu-id="8cf77-297">回應正規化套組</span><span class="sxs-lookup"><span data-stu-id="8cf77-297">Response normalization bundles</span></span>
<span data-ttu-id="8cf77-298">**回應正規化**是一種本端正規化配置，最早是由 Geoffrey Hinton 等人發表於 [ImageNet Classiﬁcation with Deep Convolutional Neural Networks](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) 報告中。</span><span class="sxs-lookup"><span data-stu-id="8cf77-298">**Response normalization** is a local normalization scheme that was first introduced by Geoffrey Hinton, et al, in the paper [ImageNet Classiﬁcation with Deep Convolutional Neural Networks](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf).</span></span> <span data-ttu-id="8cf77-299">回應正規化可用來輔助類神經網路中的一般化。</span><span class="sxs-lookup"><span data-stu-id="8cf77-299">Response normalization is used to aid generalization in neural nets.</span></span> <span data-ttu-id="8cf77-300">當一個神經元在非常高的啟動層級上引發時，本端回應正規化層將會抑制周遭神經元的啟動層級。</span><span class="sxs-lookup"><span data-stu-id="8cf77-300">When one neuron is firing at a very high activation level, a local response normalization layer suppresses the activation level of the surrounding neurons.</span></span> <span data-ttu-id="8cf77-301">此動作會使用三個參數 (***α***、***β*** 和 ***k***) 與迴旋結構 (或鄰區分布型態) 來完成。</span><span class="sxs-lookup"><span data-stu-id="8cf77-301">This is done by using three parameters (***α***, ***β***, and ***k***) and a convolutional structure (or neighborhood shape).</span></span> <span data-ttu-id="8cf77-302">目的地層中的每個神經元 ***y***，會分別對應至來源層中的一個神經元 ***x***。</span><span class="sxs-lookup"><span data-stu-id="8cf77-302">Every neuron in the destination layer ***y*** corresponds to a neuron ***x*** in the source layer.</span></span> <span data-ttu-id="8cf77-303">***y*** 的啟用層級來自於下列公式，其中，***f*** 是神經元的啟用層級，***Nx*** 是核心 (或是包含 ***x*** 的鄰區中各神經元的集合)，如下列迴旋結構所定義：</span><span class="sxs-lookup"><span data-stu-id="8cf77-303">The activation level of ***y*** is given by the following formula, where ***f*** is the activation level of a neuron, and ***Nx*** is the kernel (or the set that contains the neurons in the neighborhood of ***x***), as defined by the following convolutional structure:</span></span>  

![][1]  

<span data-ttu-id="8cf77-304">回應正規化套組支援 **Sharing**、**MapCount** 和 **Weights** 以外的所有迴旋屬性。</span><span class="sxs-lookup"><span data-stu-id="8cf77-304">Response normalization bundles support all the convolutional attributes except **Sharing**, **MapCount**, and **Weights**.</span></span>  

* <span data-ttu-id="8cf77-305">如果核心包含與 ***x*** 位於相同對應中的神經元，則正規化配置稱為**相同對應正規化**。</span><span class="sxs-lookup"><span data-stu-id="8cf77-305">If the kernel contains neurons in the same map as ***x***, the normalization scheme is referred to as **same map normalization**.</span></span> <span data-ttu-id="8cf77-306">若要定義相同對應正規化，**InputShape** 中的第一個座標必須具有值 1。</span><span class="sxs-lookup"><span data-stu-id="8cf77-306">To define same map normalization, the first coordinate in **InputShape** must have the value 1.</span></span>
* <span data-ttu-id="8cf77-307">如果核心包含與 ***x*** 位於相同空間位置中的神經元，但這些神經元位於其他對應中，則此正規化配置稱為**跨對應正規化**。</span><span class="sxs-lookup"><span data-stu-id="8cf77-307">If the kernel contains neurons in the same spatial position as ***x***, but the neurons are in other maps, the normalization scheme is called **across maps normalization**.</span></span> <span data-ttu-id="8cf77-308">這種類型的回應正規化會實作實際神經元的類型所衍生出來的一種橫向抑制，而在不同對應上運算的神經元輸出之間產生對大量啟用層級的競用。</span><span class="sxs-lookup"><span data-stu-id="8cf77-308">This type of response normalization implements a form of lateral inhibition inspired by the type found in real neurons, creating competition for big activation levels amongst neuron outputs computed on different maps.</span></span> <span data-ttu-id="8cf77-309">若要定義跨對應正規化，第一個座標必須是大於一、且不大於對應數的整數，而其餘座標必須具有值 1。</span><span class="sxs-lookup"><span data-stu-id="8cf77-309">To define across maps normalization, the first coordinate must be an integer greater than one and no greater than the number of maps, and the rest of the coordinates must have the value 1.</span></span>  

<span data-ttu-id="8cf77-310">回應正規化套組會將預先定義的函數套用至來源節點值以決定目的地節點值，因此並不具有可訓練的狀態 (加權或偏差)。</span><span class="sxs-lookup"><span data-stu-id="8cf77-310">Because response normalization bundles apply a predefined function to source node values to determine the destination node value, they have no trainable state (weights or biases).</span></span>   

<span data-ttu-id="8cf77-311">**警示**：目的地層中的節點會對應至在核心中作為中心節點的神經元。</span><span class="sxs-lookup"><span data-stu-id="8cf77-311">**Alert**: The nodes in the destination layer correspond to neurons that are the central nodes of the kernels.</span></span> <span data-ttu-id="8cf77-312">例如，如果 KernelShape[d] 為奇數，則 *KernelShape[d]/2* 會對應至中心核心節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-312">For example, if KernelShape[d] is odd, then *KernelShape[d]/2* corresponds to the central kernel node.</span></span> <span data-ttu-id="8cf77-313">如果 *KernelShape[d]* 為偶數，則中央節點位於 *KernelShape[d]/2 - 1*。</span><span class="sxs-lookup"><span data-stu-id="8cf77-313">If *KernelShape[d]* is even, the central node is at *KernelShape[d]/2 - 1*.</span></span> <span data-ttu-id="8cf77-314">因此，如果 **Padding**[d] 為 False，則第一個和最後一個 *KernelShape[d]/2* 的節點在目的地層中沒有對應的節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-314">Therefore, if **Padding**[d] is False, the first and the last *KernelShape[d]/2* nodes do not have corresponding nodes in the destination layer.</span></span> <span data-ttu-id="8cf77-315">若要避免發生此狀況，請將 **Padding** 定義為 [true, true, …, true]。</span><span class="sxs-lookup"><span data-stu-id="8cf77-315">To avoid this situation, define **Padding** as [true, true, …, true].</span></span>  

<span data-ttu-id="8cf77-316">除了前述的四個屬性以外，回應正規化套組也支援下列屬性：</span><span class="sxs-lookup"><span data-stu-id="8cf77-316">In addition to the four attributes described earlier, response normalization bundles also support the following attributes:</span></span>  

* <span data-ttu-id="8cf77-317">**Alpha**：(必要) 指定在前述公式中對應至 ***α*** 的浮點值。</span><span class="sxs-lookup"><span data-stu-id="8cf77-317">**Alpha**: (required) Specifies a floating-point value that corresponds to ***α*** in the previous formula.</span></span> 
* <span data-ttu-id="8cf77-318">**Beta**：(必要) 指定在前述公式中對應至 ***β*** 的浮點值。</span><span class="sxs-lookup"><span data-stu-id="8cf77-318">**Beta**: (required) Specifies a floating-point value that corresponds to ***β*** in the previous formula.</span></span> 
* <span data-ttu-id="8cf77-319">**Offset**：(選用) 指定在前述公式中對應至 ***k*** 的浮點值。</span><span class="sxs-lookup"><span data-stu-id="8cf77-319">**Offset**: (optional) Specifies a floating-point value that corresponds to ***k*** in the previous formula.</span></span> <span data-ttu-id="8cf77-320">其預設值為 1。</span><span class="sxs-lookup"><span data-stu-id="8cf77-320">It defaults to 1.</span></span>  

<span data-ttu-id="8cf77-321">下列範例將定義使用這些屬性的回應正規化套組：</span><span class="sxs-lookup"><span data-stu-id="8cf77-321">The following example defines a response normalization bundle using these attributes:</span></span>  

    hidden RN1 [5, 10, 10]
      from P1 response norm {
        InputShape  = [ 5, 12, 12];
        KernelShape = [ 1,  3,  3];
        Alpha = 0.001;
        Beta = 0.75;
      }  

* <span data-ttu-id="8cf77-322">來源層包含五個對應，每個對應有 12x12 的維度，共計有 1440 個節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-322">The source layer includes five maps, each with aof dimension of 12x12, totaling in 1440 nodes.</span></span> 
* <span data-ttu-id="8cf77-323">**KernelShape** 的值指出這是相同對應正規化層，其中，鄰區為 3x3 矩形。</span><span class="sxs-lookup"><span data-stu-id="8cf77-323">The value of **KernelShape** indicates that this is a same map normalization layer, where the neighborhood is a 3x3 rectangle.</span></span> 
* <span data-ttu-id="8cf77-324">**Padding** 的預設值為 False，因此目的地層的每個維度中只有 10 個節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-324">The default value of **Padding** is False, thus the destination layer has only 10 nodes in each dimension.</span></span> <span data-ttu-id="8cf77-325">若要在目的地層中加入一個與來源層中的每個節點相對應的節點，請新增 Padding = [true, true, true]，並將 RN1 的大小變更為 [5, 12, 12]。</span><span class="sxs-lookup"><span data-stu-id="8cf77-325">To include one node in the destination layer that corresponds to every node in the source layer, add Padding = [true, true, true]; and change the size of RN1 to [5, 12, 12].</span></span>  

## <a name="share-declaration"></a><span data-ttu-id="8cf77-326">共用宣告</span><span class="sxs-lookup"><span data-stu-id="8cf77-326">Share declaration</span></span>
<span data-ttu-id="8cf77-327">Net# 可選擇性地支援以共用加權定義多個套組的作業。</span><span class="sxs-lookup"><span data-stu-id="8cf77-327">Net# optionally supports defining multiple bundles with shared weights.</span></span> <span data-ttu-id="8cf77-328">任何兩個套組如果具有相同的結構，即可共用加權。</span><span class="sxs-lookup"><span data-stu-id="8cf77-328">The weights of any two bundles can be shared if their structures are the same.</span></span> <span data-ttu-id="8cf77-329">下列語法定義使用共用加權的套組：</span><span class="sxs-lookup"><span data-stu-id="8cf77-329">The following syntax defines bundles with shared weights:</span></span>  

    share-declaration:
        share    {    layer-list    }
        share    {    bundle-list    }
       share    {    bias-list    }

    layer-list:
        layer-name    ,    layer-name
        layer-list    ,    layer-name

    bundle-list:
       bundle-spec    ,    bundle-spec
        bundle-list    ,    bundle-spec

    bundle-spec:
       layer-name    =>     layer-name

    bias-list:
        bias-spec    ,    bias-spec
        bias-list    ,    bias-spec

    bias-spec:
        1    =>    layer-name

    layer-name:
        identifier  

<span data-ttu-id="8cf77-330">例如，下列共用宣告會指定層名稱，指出應同時共用加權和偏差：</span><span class="sxs-lookup"><span data-stu-id="8cf77-330">For example, the following share-declaration specifies the layer names, indicating that both weights and biases should be shared:</span></span>  

    Const {
      InputSize = 37;
      HiddenSize = 50;
    }
    input {
      Data1 [InputSize];
      Data2 [InputSize];
    }
    hidden {
      H1 [HiddenSize] from Data1 all;
      H2 [HiddenSize] from Data2 all;
    }
    output Result [2] {
      from H1 all;
      from H2 all;
    }
    share { H1, H2 } // share both weights and biases  

* <span data-ttu-id="8cf77-331">輸入特性會分割為兩個大小相等的輸入層。</span><span class="sxs-lookup"><span data-stu-id="8cf77-331">The input features are partitioned into two equal sized input layers.</span></span> 
* <span data-ttu-id="8cf77-332">接著，隱藏層會對兩個輸入層計算層級較高的特性。</span><span class="sxs-lookup"><span data-stu-id="8cf77-332">The hidden layers then compute higher level features on the two input layers.</span></span> 
* <span data-ttu-id="8cf77-333">共用宣告會指定 *H1* 和 *H2* 必須由其各自的輸入以相同方式計算。</span><span class="sxs-lookup"><span data-stu-id="8cf77-333">The share-declaration specifies that *H1* and *H2* must be computed in the same way from their respective inputs.</span></span>  

<span data-ttu-id="8cf77-334">或者，這也可以用兩個不同的共用宣告來指定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8cf77-334">Alternatively, this could be specified with two separate share-declarations as follows:</span></span>  

    share { Data1 => H1, Data2 => H2 } // share weights  

<!-- -->

    share { 1 => H1, 1 => H2 } // share biases  

<span data-ttu-id="8cf77-335">只有當層中包含單一套組時，才可以使用速記格式。</span><span class="sxs-lookup"><span data-stu-id="8cf77-335">You can use the short form only when the layers contain a single bundle.</span></span> <span data-ttu-id="8cf77-336">一般而言，只有在相關結構完全相同，也就是具有相同大小、相同迴旋幾何等等時，才能使用共用。</span><span class="sxs-lookup"><span data-stu-id="8cf77-336">In general, sharing is possible only when the relevant structure is identical, meaning that they have the same size, same convolutional geometry, and so forth.</span></span>  

## <a name="examples-of-net-usage"></a><span data-ttu-id="8cf77-337">Net# 的使用範例</span><span class="sxs-lookup"><span data-stu-id="8cf77-337">Examples of Net# usage</span></span>
<span data-ttu-id="8cf77-338">本節將透過幾個範例，說明如何使用 Net# 來新增隱藏層、定義隱藏層與其他層的互動方式，以及建置迴旋網路。</span><span class="sxs-lookup"><span data-stu-id="8cf77-338">This section provides some examples of how you can use Net# to add hidden layers, define the way that hidden layers interact with other layers, and build convolutional networks.</span></span>   

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a><span data-ttu-id="8cf77-339">定義簡易的自訂類神經網路："Hello World" 範例</span><span class="sxs-lookup"><span data-stu-id="8cf77-339">Define a simple custom neural network: "Hello World" example</span></span>
<span data-ttu-id="8cf77-340">這個簡易範例將說明如何建立具有單一隱藏層的類神經網路模型。</span><span class="sxs-lookup"><span data-stu-id="8cf77-340">This simple example demonstrates how to create a neural network model that has a single hidden layer.</span></span>  

    input Data auto;
    hidden H [200] from Data all;
    output Out [10] sigmoid from H all;  

<span data-ttu-id="8cf77-341">此範例說明某些基本命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8cf77-341">The example illustrates some basic commands as follows:</span></span>  

* <span data-ttu-id="8cf77-342">第一行會定義輸入層 (名為*資料*)。</span><span class="sxs-lookup"><span data-stu-id="8cf77-342">The first line defines the input layer (named *Data*).</span></span> <span data-ttu-id="8cf77-343">當您使用**自動**關鍵字，類神經網路會自動包含輸入範例中的所有功能資料行。</span><span class="sxs-lookup"><span data-stu-id="8cf77-343">When you use the  **auto** keyword, the neural network automatically includes all feature columns in the input examples.</span></span> 
* <span data-ttu-id="8cf77-344">第二行會建立隱藏層。</span><span class="sxs-lookup"><span data-stu-id="8cf77-344">The second line creates the hidden layer.</span></span> <span data-ttu-id="8cf77-345">隱藏層會被指派名稱 *H*，其中包含 200 個節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-345">The name *H* is assigned to the hidden layer, which has 200 nodes.</span></span> <span data-ttu-id="8cf77-346">此層會與輸入層完全相連。</span><span class="sxs-lookup"><span data-stu-id="8cf77-346">This layer is fully connected to the input layer.</span></span>
* <span data-ttu-id="8cf77-347">第三行定義輸出層 (名為 *O*)，其中包含 10 個輸出節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-347">The third line defines the output layer (named *O*), which contains 10 output nodes.</span></span> <span data-ttu-id="8cf77-348">如果類神經網路用於分類，每個類別會有一個輸出節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-348">If the neural network is used for classification, there is one output node per class.</span></span> <span data-ttu-id="8cf77-349">關鍵字 **sigmoid** 指出套用至輸出層的輸出函數。</span><span class="sxs-lookup"><span data-stu-id="8cf77-349">The keyword **sigmoid** indicates that the output function is applied to the output layer.</span></span>   

### <a name="define-multiple-hidden-layers-computer-vision-example"></a><span data-ttu-id="8cf77-350">定義多個隱藏層：電腦願景範例</span><span class="sxs-lookup"><span data-stu-id="8cf77-350">Define multiple hidden layers: computer vision example</span></span>
<span data-ttu-id="8cf77-351">下列範例說明如何定義略為複雜、具有多個自訂隱藏層的類神經網路。</span><span class="sxs-lookup"><span data-stu-id="8cf77-351">The following example demonstrates how to define a slightly more complex neural network, with multiple custom hidden layers.</span></span>  

    // Define the input layers 
    input Pixels [10, 20];
    input MetaData [7];

    // Define the first two hidden layers, using data only from the Pixels input
    hidden ByRow [10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol [5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;

    // Define the third hidden layer, which uses as source the hidden layers ByRow and ByCol
    hidden Gather [100] 
    {
      from ByRow all;
      from ByCol all;
    }

    // Define the output layer and its sources
    output Result [10]  
    {
      from Gather all;
      from MetaData all;
    }  

<span data-ttu-id="8cf77-352">此範例說明類神經網路規格語言的幾項特性：</span><span class="sxs-lookup"><span data-stu-id="8cf77-352">This example illustrates several features of the neural networks specification language:</span></span>  

* <span data-ttu-id="8cf77-353">此結構具有兩個輸入層：*Pixels* 和 *MetaData*。</span><span class="sxs-lookup"><span data-stu-id="8cf77-353">The structure has two input layers, *Pixels* and *MetaData*.</span></span>
* <span data-ttu-id="8cf77-354">*Pixels* 層是兩個連線套組的來源層，其目的地層為 *ByRow* 和 *ByCol*。</span><span class="sxs-lookup"><span data-stu-id="8cf77-354">The *Pixels* layer is a source layer for two connection bundles, with destination layers, *ByRow* and *ByCol*.</span></span>
* <span data-ttu-id="8cf77-355">*Gather* 層和 *Result* 層是多個連線套組中的目的地層。</span><span class="sxs-lookup"><span data-stu-id="8cf77-355">The layers *Gather* and *Result* are destination layers in multiple connection bundles.</span></span>
* <span data-ttu-id="8cf77-356">輸出層 *Result* 是兩個連線套組中的目的地層；一個套組以第二層級的隱藏層 (Gather) 作為目的地層，另一個套組以輸入層 MetaData 作為目的地層。</span><span class="sxs-lookup"><span data-stu-id="8cf77-356">The output layer, *Result*, is a destination layer in two connection bundles; one with the second level hidden (Gather) as a destination layer, and the other with the input layer (MetaData) as a destination layer.</span></span>
* <span data-ttu-id="8cf77-357">隱藏層 *ByRow* 和 *ByCol* 使用述詞運算式指定篩選連線。</span><span class="sxs-lookup"><span data-stu-id="8cf77-357">The hidden layers, *ByRow* and *ByCol*, specify filtered connectivity by using predicate expressions.</span></span> <span data-ttu-id="8cf77-358">更精確地說，在 [x, y] 上，*ByRow* 中的節點會連接到 *Pixels* 中第一個索引座標等於節點的第一個座標 x 的節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-358">More precisely, the node in *ByRow* at [x, y] is connected to the nodes in *Pixels* that have the first index coordinate equal to the node's first coordinate, x.</span></span> <span data-ttu-id="8cf77-359">同樣地，*在 [x, y] 上，ByCol 中的節點會連接到 _Pixels* 中在其中一個節點的第二個座標 y 內具有第二個索引座標的節點。</span><span class="sxs-lookup"><span data-stu-id="8cf77-359">Similarly, the node in *ByCol at [x, y] is connected to the nodes in _Pixels* that have the second index coordinate within one of the node's second coordinate, y.</span></span>  

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a><span data-ttu-id="8cf77-360">定義多類別分類的迴旋網路：數字辨識範例</span><span class="sxs-lookup"><span data-stu-id="8cf77-360">Define a convolutional network for multiclass classification: digit recognition example</span></span>
<span data-ttu-id="8cf77-361">下列網路的定義設計來辨識數字，說明自訂類神經網路的某些進階技術。</span><span class="sxs-lookup"><span data-stu-id="8cf77-361">The definition of the following network is designed to recognize numbers, and it illustrates some advanced techniques for customizing a neural network.</span></span>  

    input Image [29, 29];
    hidden Conv1 [5, 13, 13] from Image convolve 
    {
       InputShape  = [29, 29];
       KernelShape = [ 5,  5];
       Stride      = [ 2,  2];
       MapCount    = 5;
    }
    hidden Conv2 [50, 5, 5]
    from Conv1 convolve 
    {
       InputShape  = [ 5, 13, 13];
       KernelShape = [ 1,  5,  5];
       Stride      = [ 1,  2,  2];
       Sharing     = [false, true, true];
       MapCount    = 10;
    }
    hidden Hid3 [100] from Conv2 all;
    output Digit [10] from Hid3 all;  


* <span data-ttu-id="8cf77-362">此結構具有單一輸入層：*Image*。</span><span class="sxs-lookup"><span data-stu-id="8cf77-362">The structure has a single input layer, *Image*.</span></span>
* <span data-ttu-id="8cf77-363">關鍵字 **convolve** 指出名為 *Conv1* 和 *Conv2* 的層為迴旋層。</span><span class="sxs-lookup"><span data-stu-id="8cf77-363">The keyword **convolve** indicates that the layers named *Conv1* and *Conv2* are convolutional layers.</span></span> <span data-ttu-id="8cf77-364">這些層宣告的後面分別會加上一份迴旋屬性清單。</span><span class="sxs-lookup"><span data-stu-id="8cf77-364">Each of these layer declarations is followed by a list of the convolution attributes.</span></span>
* <span data-ttu-id="8cf77-365">網路具有第三個隱藏層 *Hid3*，與第二個隱藏層 *Conv2* 完全相連。</span><span class="sxs-lookup"><span data-stu-id="8cf77-365">The net has a third hidden layer, *Hid3*, which is fully connected to the second hidden layer, *Conv2*.</span></span>
* <span data-ttu-id="8cf77-366">輸出層 *Digit* 僅連接到第三個隱藏層 *Hid3*。</span><span class="sxs-lookup"><span data-stu-id="8cf77-366">The output layer, *Digit*, is connected only to the third hidden layer, *Hid3*.</span></span> <span data-ttu-id="8cf77-367">關鍵字 **all** 指出輸出層與 *Hid3* 完全相連。</span><span class="sxs-lookup"><span data-stu-id="8cf77-367">The keyword **all** indicates that the output layer is fully connected to *Hid3*.</span></span>
* <span data-ttu-id="8cf77-368">迴旋的 Arity 為三 (Tuple **InputShape**、**KernelShape**、**Stride** 和 **Sharing** 的長度)。</span><span class="sxs-lookup"><span data-stu-id="8cf77-368">The arity of the convolution is three (the length of the tuples **InputShape**, **KernelShape**, **Stride**, and **Sharing**).</span></span> 
* <span data-ttu-id="8cf77-369">每個核心的加權數目為 *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape**\[2] = 1 + 1 * 5 * 5 = 26。或是 26 * 50 = 1300*。</span><span class="sxs-lookup"><span data-stu-id="8cf77-369">The number of weights per kernel is *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape**\[2] = 1 + 1 * 5 * 5 = 26. Or 26 * 50 = 1300*.</span></span>
* <span data-ttu-id="8cf77-370">您可以用下列方式計算每個隱藏層中的節點數：</span><span class="sxs-lookup"><span data-stu-id="8cf77-370">You can calculate the nodes in each hidden layer as follows:</span></span>
  * <span data-ttu-id="8cf77-371">**NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.</span><span class="sxs-lookup"><span data-stu-id="8cf77-371">**NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.</span></span>
  * <span data-ttu-id="8cf77-372">**NodeCount**\[1] = (13 - 5) / 2 + 1 = 5。</span><span class="sxs-lookup"><span data-stu-id="8cf77-372">**NodeCount**\[1] = (13 - 5) / 2 + 1 = 5.</span></span> 
  * <span data-ttu-id="8cf77-373">**NodeCount**\[2] = (13 - 5) / 2 + 1 = 5。</span><span class="sxs-lookup"><span data-stu-id="8cf77-373">**NodeCount**\[2] = (13 - 5) / 2 + 1 = 5.</span></span> 
* <span data-ttu-id="8cf77-374">節點總數可使用該層的宣告維度 [50, 5, 5] 來計算，如下所示：***MapCount** * **NodeCount**\[0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*</span><span class="sxs-lookup"><span data-stu-id="8cf77-374">The total number of nodes can be calculated by using the declared dimensionality of the layer, [50, 5, 5], as follows: ***MapCount** * **NodeCount**\[0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*</span></span>
* <span data-ttu-id="8cf77-375">由於只有 *d == 0* 時，**Sharing**[d] 才會是 False，因此核心數為 ***MapCount** * **NodeCount**\[0] = 10 * 5 = 50*。</span><span class="sxs-lookup"><span data-stu-id="8cf77-375">Because **Sharing**[d] is False only for *d == 0*, the number of kernels is ***MapCount** * **NodeCount**\[0] = 10 * 5 = 50*.</span></span> 

## <a name="acknowledgements"></a><span data-ttu-id="8cf77-376">通知</span><span class="sxs-lookup"><span data-stu-id="8cf77-376">Acknowledgements</span></span>
<span data-ttu-id="8cf77-377">自訂類神經網路架構的 Net# 語言是由 Shon Katzenberger (架構、機器學習服務) 和 Alexey Kamenev (軟體工程師、Microsoft Research) 在 Microsoft 開發。</span><span class="sxs-lookup"><span data-stu-id="8cf77-377">The Net# language for customizing the architecture of neural networks was developed at Microsoft by Shon Katzenberger (Architect, Machine Learning) and Alexey Kamenev (Software Engineer, Microsoft Research).</span></span> <span data-ttu-id="8cf77-378">它在內部用於機器學習服務專案與應用程式，範圍從映像偵測到文字分析。</span><span class="sxs-lookup"><span data-stu-id="8cf77-378">It is used internally for machine learning projects and applications ranging from image detection to text analytics.</span></span> <span data-ttu-id="8cf77-379">如需詳細資訊，請參閱 [Azure ML 中的類神經網路 - Net# 簡介](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)</span><span class="sxs-lookup"><span data-stu-id="8cf77-379">For more information, see [Neural Nets in Azure ML - Introduction to Net#](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)</span></span>

<span data-ttu-id="8cf77-380">[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif</span><span class="sxs-lookup"><span data-stu-id="8cf77-380">[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif</span></span>

