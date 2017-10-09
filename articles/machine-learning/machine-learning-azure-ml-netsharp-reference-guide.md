---
title: "aaaGuide toohello Net # 類神經網路規格語言 |Microsoft 文件"
description: "語法 hello Net # 類神經網路規格語言，以及在 Microsoft Azure ML 使用 Net # toocreate 自訂類神經網路模型的方式的範例"
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
ms.openlocfilehash: 3493247ecc39ca3a1382510ad520d7017159ff62
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="guide-toonet-neural-network-specification-language-for-azure-machine-learning"></a><span data-ttu-id="203f2-103">Azure 機器學習引導 tooNet # 類神經網路規格語言</span><span class="sxs-lookup"><span data-stu-id="203f2-103">Guide tooNet# neural network specification language for Azure Machine Learning</span></span>
## <a name="overview"></a><span data-ttu-id="203f2-104">概觀</span><span class="sxs-lookup"><span data-stu-id="203f2-104">Overview</span></span>
<span data-ttu-id="203f2-105">Net # 是使用的 toodefine 類神經網路架構，Microsoft 開發的語言。</span><span class="sxs-lookup"><span data-stu-id="203f2-105">Net# is a language developed by Microsoft that is used toodefine neural network architectures.</span></span> <span data-ttu-id="203f2-106">您可以在 Microsoft Azure Machine Learning 的類神經網路模組中使用 Net#。</span><span class="sxs-lookup"><span data-stu-id="203f2-106">You can use Net# in neural network modules in Microsoft Azure Machine Learning.</span></span>

<!-- This function doesn't currentlyappear in hello MicrosoftML documentation. If it is added in a future update, we can uncomment this text.

, or in hello `rxNeuralNetwork()` function in [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml). 

-->

<span data-ttu-id="203f2-107">在本文中，您將了解基本概念所需 toodevelop 自訂類神經網路：</span><span class="sxs-lookup"><span data-stu-id="203f2-107">In this article, you will learn basic concepts needed toodevelop a custom neural network:</span></span> 

* <span data-ttu-id="203f2-108">類神經網路需求及如何 toodefine hello 主要元件</span><span class="sxs-lookup"><span data-stu-id="203f2-108">Neural network requirements and how toodefine hello primary components</span></span>
* <span data-ttu-id="203f2-109">hello 語法和 hello Net # 規格語言關鍵字</span><span class="sxs-lookup"><span data-stu-id="203f2-109">hello syntax and keywords of hello Net# specification language</span></span>
* <span data-ttu-id="203f2-110">使用 Net# 建立的自訂類神經網路範例</span><span class="sxs-lookup"><span data-stu-id="203f2-110">Examples of custom neural networks created using Net#</span></span> 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a><span data-ttu-id="203f2-111">類神經網路基本概念</span><span class="sxs-lookup"><span data-stu-id="203f2-111">Neural network basics</span></span>
<span data-ttu-id="203f2-112">類神經網路結構組成***節點***，都依照***層***，和加權***連線***(或***邊緣***) 之間hello 節點。</span><span class="sxs-lookup"><span data-stu-id="203f2-112">A neural network structure consists of ***nodes*** that are organized in ***layers***, and weighted ***connections*** (or ***edges***) between hello nodes.</span></span> <span data-ttu-id="203f2-113">hello 連線是方向性，且每個連接***來源***節點和***目的地***節點。</span><span class="sxs-lookup"><span data-stu-id="203f2-113">hello connections are directional, and each connection has a ***source*** node and a ***destination*** node.</span></span>  

<span data-ttu-id="203f2-114">每個***可訓練的層*** (隱藏或輸出層) 都有一或多個***連線套組***。</span><span class="sxs-lookup"><span data-stu-id="203f2-114">Each ***trainable layer*** (a hidden or an output layer) has one or more ***connection bundles***.</span></span> <span data-ttu-id="203f2-115">連接配套包含來源層級和 hello 來自該來源層級的規格。</span><span class="sxs-lookup"><span data-stu-id="203f2-115">A connection bundle consists of a source layer and a specification of hello connections from that source layer.</span></span> <span data-ttu-id="203f2-116">中的給定的組合共用的所有都 hello 連接都 hello 相同***來源層級***和都 hello 相同***目的地層***。</span><span class="sxs-lookup"><span data-stu-id="203f2-116">All hello connections in a given bundle share hello same ***source layer*** and hello same ***destination layer***.</span></span> <span data-ttu-id="203f2-117">在 Net # 中，連接組合都會被視為隸屬 toohello 組合的目的地階層。</span><span class="sxs-lookup"><span data-stu-id="203f2-117">In Net#, a connection bundle is considered as belonging toohello bundle's destination layer.</span></span>  

<span data-ttu-id="203f2-118">Net # 支援各種連線組合，可讓您自訂的輸入是對應的 toohidden 圖層的 hello 方式和對應的 toohello 輸出。</span><span class="sxs-lookup"><span data-stu-id="203f2-118">Net# supports various kinds of connection bundles, which lets you customize hello way inputs are mapped toohidden layers and mapped toohello outputs.</span></span>   

<span data-ttu-id="203f2-119">hello 預設或標準的組合是**完整配套**，hello 中的每個節點中來源階層是 hello 目的地階層中的連接的 tooevery 節點。</span><span class="sxs-lookup"><span data-stu-id="203f2-119">hello default or standard bundle is a **full bundle**, in which each node in hello source layer is connected tooevery node in hello destination layer.</span></span>  

<span data-ttu-id="203f2-120">此外，Net # 支援下列四種進階的連線組合 hello:</span><span class="sxs-lookup"><span data-stu-id="203f2-120">Additionally, Net# supports hello following four kinds of advanced connection bundles:</span></span>  

* <span data-ttu-id="203f2-121">**篩選套組**。</span><span class="sxs-lookup"><span data-stu-id="203f2-121">**Filtered bundles**.</span></span> <span data-ttu-id="203f2-122">hello 使用者可以使用 hello hello 來源圖層的節點和 hello 目的地層節點的位置，以定義述詞。</span><span class="sxs-lookup"><span data-stu-id="203f2-122">hello user can define a predicate by using hello locations of hello source layer node and hello destination layer node.</span></span> <span data-ttu-id="203f2-123">每當 hello 述詞為 True 時，都會連線節點。</span><span class="sxs-lookup"><span data-stu-id="203f2-123">Nodes are connected whenever hello predicate is True.</span></span>
* <span data-ttu-id="203f2-124">**迴旋套組**。</span><span class="sxs-lookup"><span data-stu-id="203f2-124">**Convolutional bundles**.</span></span> <span data-ttu-id="203f2-125">hello 使用者可以定義節點的小型公寓 hello 來源層級中。</span><span class="sxs-lookup"><span data-stu-id="203f2-125">hello user can define small neighborhoods of nodes in hello source layer.</span></span> <span data-ttu-id="203f2-126">Hello 目的地階層中的每個節點是連接的 tooone hello 來源層的節點上的芳鄰。</span><span class="sxs-lookup"><span data-stu-id="203f2-126">Each node in hello destination layer is connected tooone neighborhood of nodes in hello source layer.</span></span>
* <span data-ttu-id="203f2-127">**集區套組**和**回應正規化套組**。</span><span class="sxs-lookup"><span data-stu-id="203f2-127">**Pooling bundles** and **Response normalization bundles**.</span></span> <span data-ttu-id="203f2-128">這些是類似 tooconvolutional 組合中的 hello 使用者會定義小公寓 hello 來源層的節點。</span><span class="sxs-lookup"><span data-stu-id="203f2-128">These are similar tooconvolutional bundles in that hello user defines small neighborhoods of nodes in hello source layer.</span></span> <span data-ttu-id="203f2-129">hello 差異是，這些組合中的 hello 邊緣 hello 加權並未 trainable。</span><span class="sxs-lookup"><span data-stu-id="203f2-129">hello difference is that hello weights of hello edges in these bundles are not trainable.</span></span> <span data-ttu-id="203f2-130">相反地，套用預先定義的函式 toohello 來源節點值 toodetermine hello 目的地節點值。</span><span class="sxs-lookup"><span data-stu-id="203f2-130">Instead, a predefined function is applied toohello source node values toodetermine hello destination node value.</span></span>  

<span data-ttu-id="203f2-131">使用 Net # 類神經網路 toodefine hello 結構可讓可能 toodefine 複雜的結構，例如深度類神經網路或迴旋任意的維度，稱為 tooimprove 瞭解資料，例如影像、 音訊或視訊。</span><span class="sxs-lookup"><span data-stu-id="203f2-131">Using Net# toodefine hello structure of a neural network makes it possible toodefine complex structures such as deep neural networks or convolutions of arbitrary dimensions, which are known tooimprove learning on data such as image, audio, or video.</span></span>  

## <a name="supported-customizations"></a><span data-ttu-id="203f2-132">支援的自訂</span><span class="sxs-lookup"><span data-stu-id="203f2-132">Supported customizations</span></span>
<span data-ttu-id="203f2-133">您在 Azure Machine Learning 中建立的類神經網路模型的 hello 架構可以使用 Net # 廣泛地自訂。</span><span class="sxs-lookup"><span data-stu-id="203f2-133">hello architecture of neural network models that you create in Azure Machine Learning can be extensively customized by using Net#.</span></span> <span data-ttu-id="203f2-134">您可以：</span><span class="sxs-lookup"><span data-stu-id="203f2-134">You can:</span></span>  

* <span data-ttu-id="203f2-135">隱藏的層節點的控制項 hello 數目在中建立和每個圖層。</span><span class="sxs-lookup"><span data-stu-id="203f2-135">Create hidden layers and control hello number of nodes in each layer.</span></span>
* <span data-ttu-id="203f2-136">指定圖層的 toobe 連接 tooeach 其他的方式。</span><span class="sxs-lookup"><span data-stu-id="203f2-136">Specify how layers are toobe connected tooeach other.</span></span>
* <span data-ttu-id="203f2-137">定義特殊連線結構，例如迴旋和加權共用套組。</span><span class="sxs-lookup"><span data-stu-id="203f2-137">Define special connectivity structures, such as convolutions and weight sharing bundles.</span></span>
* <span data-ttu-id="203f2-138">指定不同的啟用函數。</span><span class="sxs-lookup"><span data-stu-id="203f2-138">Specify different activation functions.</span></span>  

<span data-ttu-id="203f2-139">如需 hello 規格語言語法的詳細資訊，請參閱[結構規格](#Structure-specifications)。</span><span class="sxs-lookup"><span data-stu-id="203f2-139">For details of hello specification language syntax, see [Structure Specification](#Structure-specifications).</span></span>  

<span data-ttu-id="203f2-140">如需定義為某些常見的機器學習服務工作，從 simplex toocomplex，類神經網路的範例，請參閱[範例](#Examples-of-Net#-usage)。</span><span class="sxs-lookup"><span data-stu-id="203f2-140">For examples of defining neural networks for some common machine learning tasks, from simplex toocomplex, see [Examples](#Examples-of-Net#-usage).</span></span>  

## <a name="general-requirements"></a><span data-ttu-id="203f2-141">一般需求</span><span class="sxs-lookup"><span data-stu-id="203f2-141">General requirements</span></span>
* <span data-ttu-id="203f2-142">必須只能有一個輸出層，和至少一個輸入層，以及零或多個隱藏層。</span><span class="sxs-lookup"><span data-stu-id="203f2-142">There must be exactly one output layer, at least one input layer, and zero or more hidden layers.</span></span> 
* <span data-ttu-id="203f2-143">每一層都有固定的節點數目，在概念上會以任意維度的矩形陣列編排。</span><span class="sxs-lookup"><span data-stu-id="203f2-143">Each layer has a fixed number of nodes, conceptually arranged in a rectangular array of arbitrary dimensions.</span></span> 
* <span data-ttu-id="203f2-144">輸入的層沒有相關聯的定型參數，而且代表 hello 點位置執行個體資料會進入 hello 網路。</span><span class="sxs-lookup"><span data-stu-id="203f2-144">Input layers have no associated trained parameters and represent hello point where instance data enters hello network.</span></span> 
* <span data-ttu-id="203f2-145">Trainable (hello 隱藏和輸出層) 的圖層有關聯的定型的參數，稱為加權和徵才偏差。</span><span class="sxs-lookup"><span data-stu-id="203f2-145">Trainable layers (hello hidden and output layers) have associated trained parameters, known as weights and biases.</span></span> 
* <span data-ttu-id="203f2-146">hello 來源和目的地節點必須在個別的圖層。</span><span class="sxs-lookup"><span data-stu-id="203f2-146">hello source and destination nodes must be in separate layers.</span></span> 
* <span data-ttu-id="203f2-147">連接必須為非循環。也就是說，不能有前置反 toohello 初始來源節點連接的鏈結。</span><span class="sxs-lookup"><span data-stu-id="203f2-147">Connections must be acyclic; in other words, there cannot be a chain of connections leading back toohello initial source node.</span></span>
* <span data-ttu-id="203f2-148">hello 輸出層不能連接組合的來源層級。</span><span class="sxs-lookup"><span data-stu-id="203f2-148">hello output layer cannot be a source layer of a connection bundle.</span></span>  

## <a name="structure-specifications"></a><span data-ttu-id="203f2-149">結構規格</span><span class="sxs-lookup"><span data-stu-id="203f2-149">Structure specifications</span></span>
<span data-ttu-id="203f2-150">類神經網路結構規格由三個區段組成： hello**常數宣告**，hello**層級宣告**，hello**連線宣告**。</span><span class="sxs-lookup"><span data-stu-id="203f2-150">A neural network structure specification is composed of three sections: hello **constant declaration**, hello **layer declaration**, hello **connection declaration**.</span></span> <span data-ttu-id="203f2-151">另外還有一個選擇性的**共用宣告**區段。</span><span class="sxs-lookup"><span data-stu-id="203f2-151">There is also an optional **share declaration** section.</span></span> <span data-ttu-id="203f2-152">hello 區段可以任何順序指定。</span><span class="sxs-lookup"><span data-stu-id="203f2-152">hello sections can be specified in any order.</span></span>  

## <a name="constant-declaration"></a><span data-ttu-id="203f2-153">常數宣告</span><span class="sxs-lookup"><span data-stu-id="203f2-153">Constant declaration</span></span>
<span data-ttu-id="203f2-154">常數宣告是選擇性宣告。</span><span class="sxs-lookup"><span data-stu-id="203f2-154">A constant declaration is optional.</span></span> <span data-ttu-id="203f2-155">它會提供表示 toodefine hello 類神經網路定義中的其他位置所使用的值。</span><span class="sxs-lookup"><span data-stu-id="203f2-155">It provides a means toodefine values used elsewhere in hello neural network definition.</span></span> <span data-ttu-id="203f2-156">hello 宣告陳述式所組成的識別碼後面接著等號和值運算式。</span><span class="sxs-lookup"><span data-stu-id="203f2-156">hello declaration statement consists of an identifier followed by an equal sign and a value expression.</span></span>   

<span data-ttu-id="203f2-157">例如，陳述式之後的 hello 定義常數**x**:</span><span class="sxs-lookup"><span data-stu-id="203f2-157">For example, hello following statement defines a constant **x**:</span></span>  

    Const X = 28;  

<span data-ttu-id="203f2-158">toodefine 兩個或多個常數，同時，hello 識別項名稱和值大括弧括住，並使用分號分隔。</span><span class="sxs-lookup"><span data-stu-id="203f2-158">toodefine two or more constants simultaneously, enclose hello identifier names and values in braces, and separate them by using semicolons.</span></span> <span data-ttu-id="203f2-159">例如：</span><span class="sxs-lookup"><span data-stu-id="203f2-159">For example:</span></span>  

    Const { X = 28; Y = 4; }  

<span data-ttu-id="203f2-160">hello 右手邊的每個指派運算式可以是整數、 實數、 布林值 （True 或 False） 或數學運算式。</span><span class="sxs-lookup"><span data-stu-id="203f2-160">hello right-hand side of each assignment expression can be an integer, a real number, a Boolean value (True or False), or a mathematical expression.</span></span> <span data-ttu-id="203f2-161">例如：</span><span class="sxs-lookup"><span data-stu-id="203f2-161">For example:</span></span>  

    Const { X = 17 * 2; Y = true; }  

## <a name="layer-declaration"></a><span data-ttu-id="203f2-162">層宣告</span><span class="sxs-lookup"><span data-stu-id="203f2-162">Layer declaration</span></span>
<span data-ttu-id="203f2-163">需要 hello 層宣告。</span><span class="sxs-lookup"><span data-stu-id="203f2-163">hello layer declaration is required.</span></span> <span data-ttu-id="203f2-164">它會定義 hello 大小及來源的 hello 圖層，包括其連線組合和屬性。</span><span class="sxs-lookup"><span data-stu-id="203f2-164">It defines hello size and source of hello layer, including its connection bundles and attributes.</span></span> <span data-ttu-id="203f2-165">hello hello hello 層 （輸入、 隱藏的或輸出） 名稱的宣告陳述式開頭，後面接著 hello 維度的 hello 層 (tuple 的正整數)。</span><span class="sxs-lookup"><span data-stu-id="203f2-165">hello declaration statement starts with hello name of hello layer (input, hidden, or output), followed by hello dimensions of hello layer (a tuple of positive integers).</span></span> <span data-ttu-id="203f2-166">例如：</span><span class="sxs-lookup"><span data-stu-id="203f2-166">For example:</span></span>  

    input Data auto;
    hidden Hidden[5,20] from Data all;
    output Result[2] from Hidden all;  

* <span data-ttu-id="203f2-167">hello 產品的 hello 維度是 hello hello 層的節點數目。</span><span class="sxs-lookup"><span data-stu-id="203f2-167">hello product of hello dimensions is hello number of nodes in hello layer.</span></span> <span data-ttu-id="203f2-168">在此範例中，有兩個維度 [5,20]，這表示在 hello 層有 100 個節點。</span><span class="sxs-lookup"><span data-stu-id="203f2-168">In this example, there are two dimensions [5,20], which means there are  100 nodes in hello layer.</span></span>
* <span data-ttu-id="203f2-169">hello 圖層可以宣告任何順序，但有一個例外： 如果已定義多個輸入的層，在宣告的 hello 順序必須符合 hello 順序 hello 輸入資料中的功能。</span><span class="sxs-lookup"><span data-stu-id="203f2-169">hello layers can be declared in any order, with one exception: If more than one input layer is defined, hello order in which they are declared must match hello order of features in hello input data.</span></span>  

<span data-ttu-id="203f2-170">toospecify hello 層的節點數目是自動，決定使用 hello**自動**關鍵字。</span><span class="sxs-lookup"><span data-stu-id="203f2-170">toospecify that hello number of nodes in a layer be determined automatically, use hello **auto** keyword.</span></span> <span data-ttu-id="203f2-171">hello**自動**關鍵字有不同的效果，視 hello 層而定：</span><span class="sxs-lookup"><span data-stu-id="203f2-171">hello **auto** keyword has different effects, depending on hello layer:</span></span>  

* <span data-ttu-id="203f2-172">在輸入的層宣告中，節點的 hello 數目是 hello hello 輸入資料中的功能數目。</span><span class="sxs-lookup"><span data-stu-id="203f2-172">In an input layer declaration, hello number of nodes is hello number of features in hello input data.</span></span>
* <span data-ttu-id="203f2-173">在隱藏的層的宣告中，節點的 hello 數目是 hello hello 參數值所指定的數字**隱藏節點的數目**。</span><span class="sxs-lookup"><span data-stu-id="203f2-173">In a hidden layer declaration, hello number of nodes is hello number that is specified by hello parameter value for **Number of hidden nodes**.</span></span> 
* <span data-ttu-id="203f2-174">在輸出層宣告中，hello 節點數目是 2 的二級分類，1 代表迴歸，並等於 toohello 多級分類的輸出節點的數目。</span><span class="sxs-lookup"><span data-stu-id="203f2-174">In an output layer declaration, hello number of nodes is 2 for two-class classification, 1 for regression, and equal toohello number of output nodes for multiclass classification.</span></span>   

<span data-ttu-id="203f2-175">例如，hello 下列網路定義允許 hello 大小的所有圖層 toobe 自動決定：</span><span class="sxs-lookup"><span data-stu-id="203f2-175">For example, hello following network definition allows hello size of all layers toobe automatically determined:</span></span>  

    input Data auto;
    hidden Hidden auto from Data all;
    output Result auto from Hidden all;  


<span data-ttu-id="203f2-176">Trainable 圖層的層級宣告 (hello 隱藏或輸出層級) 可以選擇性地包含 hello 輸出函式 （也稱為啟用函式），其預設太**sigmoid**分類模型和**線性**迴歸模型。</span><span class="sxs-lookup"><span data-stu-id="203f2-176">A layer declaration for a trainable layer (hello hidden or output layers) can optionally include hello output function (also called an activation function), which defaults too**sigmoid** for classification models, and **linear** for regression models.</span></span> <span data-ttu-id="203f2-177">（即使您使用 hello 預設，您可以明確陳述 hello 啟用函式，如果為了避免混淆。）</span><span class="sxs-lookup"><span data-stu-id="203f2-177">(Even if you use hello default, you can explicitly state hello activation function, if desired for clarity.)</span></span>

<span data-ttu-id="203f2-178">hello 輸出支援下列函數：</span><span class="sxs-lookup"><span data-stu-id="203f2-178">hello following output functions are supported:</span></span>  

* <span data-ttu-id="203f2-179">sigmoid</span><span class="sxs-lookup"><span data-stu-id="203f2-179">sigmoid</span></span>
* <span data-ttu-id="203f2-180">linear</span><span class="sxs-lookup"><span data-stu-id="203f2-180">linear</span></span>
* <span data-ttu-id="203f2-181">softmax</span><span class="sxs-lookup"><span data-stu-id="203f2-181">softmax</span></span>
* <span data-ttu-id="203f2-182">rlinear</span><span class="sxs-lookup"><span data-stu-id="203f2-182">rlinear</span></span>
* <span data-ttu-id="203f2-183">square</span><span class="sxs-lookup"><span data-stu-id="203f2-183">square</span></span>
* <span data-ttu-id="203f2-184">sqrt</span><span class="sxs-lookup"><span data-stu-id="203f2-184">sqrt</span></span>
* <span data-ttu-id="203f2-185">srlinear</span><span class="sxs-lookup"><span data-stu-id="203f2-185">srlinear</span></span>
* <span data-ttu-id="203f2-186">abs</span><span class="sxs-lookup"><span data-stu-id="203f2-186">abs</span></span>
* <span data-ttu-id="203f2-187">tanh</span><span class="sxs-lookup"><span data-stu-id="203f2-187">tanh</span></span> 
* <span data-ttu-id="203f2-188">brlinear</span><span class="sxs-lookup"><span data-stu-id="203f2-188">brlinear</span></span>  

<span data-ttu-id="203f2-189">例如，hello 宣告之後使用 hello **softmax**函式：</span><span class="sxs-lookup"><span data-stu-id="203f2-189">For example, hello following declaration uses hello **softmax** function:</span></span>  

    output Result [100] softmax from Hidden all;  

## <a name="connection-declaration"></a><span data-ttu-id="203f2-190">連線宣告</span><span class="sxs-lookup"><span data-stu-id="203f2-190">Connection declaration</span></span>
<span data-ttu-id="203f2-191">之後立即定義 hello trainable 圖層，您必須宣告在您已定義的 hello 圖層間的連線。</span><span class="sxs-lookup"><span data-stu-id="203f2-191">Immediately after defining hello trainable layer, you must declare connections among hello layers you have defined.</span></span> <span data-ttu-id="203f2-192">hello 連接配套宣告的開頭 hello 關鍵字**從**，後面接著 hello 種類的名稱 hello 配套來源圖層與 hello 連接配套 toocreate。</span><span class="sxs-lookup"><span data-stu-id="203f2-192">hello connection bundle declaration starts with hello keyword **from**, followed by hello name of hello bundle's source layer and hello kind of connection bundle toocreate.</span></span>   

<span data-ttu-id="203f2-193">目前支援五種連線套組：</span><span class="sxs-lookup"><span data-stu-id="203f2-193">Currently, five kinds of connection bundles are supported:</span></span>  

* <span data-ttu-id="203f2-194">**完整**組合，以 hello 關鍵字**所有**</span><span class="sxs-lookup"><span data-stu-id="203f2-194">**Full** bundles, indicated by hello keyword **all**</span></span>
* <span data-ttu-id="203f2-195">**篩選**組合，以 hello 關鍵字**其中**，後面接著述詞的運算式</span><span class="sxs-lookup"><span data-stu-id="203f2-195">**Filtered** bundles, indicated by hello keyword **where**, followed by a predicate expression</span></span>
* <span data-ttu-id="203f2-196">**Convolutional**組合，以 hello 關鍵字**convolve**，後面接著 hello convolution 屬性</span><span class="sxs-lookup"><span data-stu-id="203f2-196">**Convolutional** bundles, indicated by hello keyword **convolve**, followed by hello convolution attributes</span></span>
* <span data-ttu-id="203f2-197">**共用**組合，以 hello 關鍵字**最大集區**或**表示集區**</span><span class="sxs-lookup"><span data-stu-id="203f2-197">**Pooling** bundles, indicated by hello keywords **max pool** or **mean pool**</span></span>
* <span data-ttu-id="203f2-198">**回應正規化**組合，以 hello 關鍵字**回應範數**</span><span class="sxs-lookup"><span data-stu-id="203f2-198">**Response normalization** bundles, indicated by hello keyword **response norm**</span></span>      

## <a name="full-bundles"></a><span data-ttu-id="203f2-199">完整套組</span><span class="sxs-lookup"><span data-stu-id="203f2-199">Full bundles</span></span>
<span data-ttu-id="203f2-200">完整連接配套 hello 來源層 tooeach 節點 hello 目的地階層中包含來自每個節點的連接。</span><span class="sxs-lookup"><span data-stu-id="203f2-200">A full connection bundle includes a connection from each node in hello source layer tooeach node in hello destination layer.</span></span> <span data-ttu-id="203f2-201">這是 hello 預設網路連線類型。</span><span class="sxs-lookup"><span data-stu-id="203f2-201">This is hello default network connection type.</span></span>  

## <a name="filtered-bundles"></a><span data-ttu-id="203f2-202">篩選套組</span><span class="sxs-lookup"><span data-stu-id="203f2-202">Filtered bundles</span></span>
<span data-ttu-id="203f2-203">篩選連線套組規格包含一個述詞，此述詞在語法上的表示方式非常類似 C# lambda 運算式。</span><span class="sxs-lookup"><span data-stu-id="203f2-203">A filtered connection bundle specification includes a predicate, expressed syntactically, much like a C# lambda expression.</span></span> <span data-ttu-id="203f2-204">hello 下列範例定義兩個篩選的組合：</span><span class="sxs-lookup"><span data-stu-id="203f2-204">hello following example defines two filtered bundles:</span></span>  

    input Pixels [10, 20];
    hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  

* <span data-ttu-id="203f2-205">Hello 的述詞中*ByRow*， **s**是以參數為 hello 矩形陣列 hello 輸入圖層的節點代表索引*像素為單位*，和**d**是參數表示成 hello hello 隱藏圖層之節點的陣列索引*ByRow*。</span><span class="sxs-lookup"><span data-stu-id="203f2-205">In hello predicate for *ByRow*, **s** is a parameter representing an index into hello rectangular array of nodes of hello input layer, *Pixels*, and **d** is a parameter representing an index into hello array of nodes of hello hidden layer, *ByRow*.</span></span> <span data-ttu-id="203f2-206">hello 這兩種**s**和**d**是長度為兩個整數的 tuple。</span><span class="sxs-lookup"><span data-stu-id="203f2-206">hello type of both **s** and **d** is a tuple of integers of length two.</span></span> <span data-ttu-id="203f2-207">在概念上，**s** 的範圍介於所有 *0 <= s[0] < 10* 與 *0 <= s[1] < 20* 的整數對之間，而且 **d** 的範圍介於所有 *0 <= d[0] < 10* 與 *0 <= d[1] < 12* 的整數對之間。</span><span class="sxs-lookup"><span data-stu-id="203f2-207">Conceptually, **s** ranges over all pairs of integers with *0 <= s[0] < 10* and *0 <= s[1] < 20*, and **d** ranges over all pairs of integers, with *0 <= d[0] < 10* and *0 <= d[1] < 12*.</span></span> 
* <span data-ttu-id="203f2-208">Hello hello 述詞運算式的右側，在沒有條件。</span><span class="sxs-lookup"><span data-stu-id="203f2-208">On hello right-hand side of hello predicate expression, there is a condition.</span></span> <span data-ttu-id="203f2-209">在此範例中，每個值**s**和**d**使得 hello 條件為 True 時，會從 hello 來源圖層節點 toohello 目的圖層節點的邊緣。</span><span class="sxs-lookup"><span data-stu-id="203f2-209">In this example, for every value of **s** and **d** such that hello condition is True, there is an edge from hello source layer node toohello destination layer node.</span></span> <span data-ttu-id="203f2-210">因此，這個篩選條件運算式，表示該 hello 配套所包含的連接所定義的 hello 節點**s** toohello 節點所定義**d**在所有情況下，其中 s [0] 是等於 tood [0]。</span><span class="sxs-lookup"><span data-stu-id="203f2-210">Thus, this filter expression indicates that hello bundle includes a connection from hello node defined by **s** toohello node defined by **d** in all cases where s[0] is equal tood[0].</span></span>  

<span data-ttu-id="203f2-211">您可以選擇性地為篩選套組指定一組加權。</span><span class="sxs-lookup"><span data-stu-id="203f2-211">Optionally, you can specify a set of weights for a filtered bundle.</span></span> <span data-ttu-id="203f2-212">hello 值 hello**加權**屬性必須是 tuple 的浮點值的長度符合 hello hello 組合所定義的連接數目。</span><span class="sxs-lookup"><span data-stu-id="203f2-212">hello value for hello **Weights** attribute must be a tuple of floating point values with a length that matches hello number of connections defined by hello bundle.</span></span> <span data-ttu-id="203f2-213">依預設會隨機產生加權。</span><span class="sxs-lookup"><span data-stu-id="203f2-213">By default, weights are randomly generated.</span></span>  

<span data-ttu-id="203f2-214">加權值被分組 hello 目的節點的索引。</span><span class="sxs-lookup"><span data-stu-id="203f2-214">Weight values are grouped by hello destination node index.</span></span> <span data-ttu-id="203f2-215">亦即，如果第一個目的地節點 hello 連接花費了來源節點，第一次 hello *K* hello 的項目**加權**tuple 會 hello 第一個目的地節點，在來源索引順序中的 hello 加權。</span><span class="sxs-lookup"><span data-stu-id="203f2-215">That is, if hello first destination node is connected tooK source nodes, hello first *K* elements of hello **Weights** tuple are hello weights for hello first destination node, in source index order.</span></span> <span data-ttu-id="203f2-216">這同樣適用於 hello 其餘目的地節點的 hello。</span><span class="sxs-lookup"><span data-stu-id="203f2-216">hello same applies for hello remaining destination nodes.</span></span>  

<span data-ttu-id="203f2-217">很可能 toospecify 加權做為常數值。</span><span class="sxs-lookup"><span data-stu-id="203f2-217">It's possible toospecify weights directly as constant values.</span></span> <span data-ttu-id="203f2-218">例如，如果您先前所學 hello 加權，您可以指定它們為使用此語法的常數：</span><span class="sxs-lookup"><span data-stu-id="203f2-218">For example, if you learned hello weights previously, you can specify them as constants using this syntax:</span></span>

    const Weights_1 = [0.0188045055, 0.130500451, ...]


## <a name="convolutional-bundles"></a><span data-ttu-id="203f2-219">迴旋套組</span><span class="sxs-lookup"><span data-stu-id="203f2-219">Convolutional bundles</span></span>
<span data-ttu-id="203f2-220">Hello 定型資料具有同質性結構時，convolutional 連線是常用的 toolearn hello 資料的高層級的功能。</span><span class="sxs-lookup"><span data-stu-id="203f2-220">When hello training data has a homogeneous structure, convolutional connections are commonly used toolearn high-level features of hello data.</span></span> <span data-ttu-id="203f2-221">例如，在影像、音訊或視訊資料中，空間或暫時維度可能會相當一致。</span><span class="sxs-lookup"><span data-stu-id="203f2-221">For example, in image, audio, or video data, spatial or temporal dimensionality can be fairly uniform.</span></span>  

<span data-ttu-id="203f2-222">Convolutional 組合運用矩形**核心**，slid hello 維度。</span><span class="sxs-lookup"><span data-stu-id="203f2-222">Convolutional bundles employ rectangular **kernels** that are slid through hello dimensions.</span></span> <span data-ttu-id="203f2-223">基本上，每個核心定義一組的本機公寓，參照 tooas 中套用的權數**核心應用程式**。</span><span class="sxs-lookup"><span data-stu-id="203f2-223">Essentially, each kernel defines a set of weights applied in local neighborhoods, referred tooas **kernel applications**.</span></span> <span data-ttu-id="203f2-224">每個核心應用程式對應 hello 來源層級，也就是參考的 tooas hello tooa 節點**中央節點**。</span><span class="sxs-lookup"><span data-stu-id="203f2-224">Each kernel application corresponds tooa node in hello source layer, which is referred tooas hello **central node**.</span></span> <span data-ttu-id="203f2-225">核心 hello 加權會共用連線數目。</span><span class="sxs-lookup"><span data-stu-id="203f2-225">hello weights of a kernel are shared among many connections.</span></span> <span data-ttu-id="203f2-226">在 convolutional 的組合，每個核心是矩形，而所有的核心應用程式都 hello 相同大小。</span><span class="sxs-lookup"><span data-stu-id="203f2-226">In a convolutional bundle, each kernel is rectangular and all kernel applications are hello same size.</span></span>  

<span data-ttu-id="203f2-227">Convolutional 組合支援 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="203f2-227">Convolutional bundles support hello following attributes:</span></span>

<span data-ttu-id="203f2-228">**InputShape**定義 hello 這個 convolutional 配套 hello 基於 hello 來源層級的維度性。</span><span class="sxs-lookup"><span data-stu-id="203f2-228">**InputShape** defines hello dimensionality of hello source layer for hello purposes of this convolutional bundle.</span></span> <span data-ttu-id="203f2-229">hello 值必須是正整數的 tuple。</span><span class="sxs-lookup"><span data-stu-id="203f2-229">hello value must be a tuple of positive integers.</span></span> <span data-ttu-id="203f2-230">hello 產品的 hello 整數必須等於 hello hello 來源圖層中的節點數目，但反之則不需要為 hello 來源層級宣告的 toomatch hello 維度性。</span><span class="sxs-lookup"><span data-stu-id="203f2-230">hello product of hello integers must equal hello number of nodes in hello source layer, but otherwise, it does not need toomatch hello dimensionality declared for hello source layer.</span></span> <span data-ttu-id="203f2-231">這個 tuple 的 hello 長度會變成 hello **arity** hello convolutional 組合的值。</span><span class="sxs-lookup"><span data-stu-id="203f2-231">hello length of this tuple becomes hello **arity** value for hello convolutional bundle.</span></span> <span data-ttu-id="203f2-232">（通常 arity 參照 toohello 數目之引數或函式可以接受的運算元）。</span><span class="sxs-lookup"><span data-stu-id="203f2-232">(Typically arity refers toohello number of arguments or operands that a function can take.)</span></span>  

<span data-ttu-id="203f2-233">toodefine hello 圖形和位置 hello 核心使用 hello 屬性**KernelShape**， **Stride**，**填補**， **LowerPad**，和**UpperPad**:</span><span class="sxs-lookup"><span data-stu-id="203f2-233">toodefine hello shape and locations of hello kernels, use hello attributes **KernelShape**, **Stride**, **Padding**, **LowerPad**, and **UpperPad**:</span></span>   

* <span data-ttu-id="203f2-234">**KernelShape**: hello convolutional 組合的每個核心的 （必要） 定義 hello 維度性。</span><span class="sxs-lookup"><span data-stu-id="203f2-234">**KernelShape**: (required) Defines hello dimensionality of each kernel for hello convolutional bundle.</span></span> <span data-ttu-id="203f2-235">hello 值必須是正整數長度等於 hello arity hello 組合的 tuple。</span><span class="sxs-lookup"><span data-stu-id="203f2-235">hello value must be a tuple of positive integers with a length that equals hello arity of hello bundle.</span></span> <span data-ttu-id="203f2-236">這個 tuple 的每個元件必須等於或小於 hello 對應元件的**InputShape**。</span><span class="sxs-lookup"><span data-stu-id="203f2-236">Each component of this tuple must be no greater than hello corresponding component of **InputShape**.</span></span> 
* <span data-ttu-id="203f2-237">**Stride**: （選擇性） 定義 hello 滑動 hello hello 中央節點之間的距離 hello convolution （每個維度的一個步驟大小） 的步驟大小。</span><span class="sxs-lookup"><span data-stu-id="203f2-237">**Stride**: (optional) Defines hello sliding step sizes of hello convolution (one step size for each dimension), that is hello distance between hello central nodes.</span></span> <span data-ttu-id="203f2-238">hello 值必須是正整數 hello 組合的 hello arity 長度的 tuple。</span><span class="sxs-lookup"><span data-stu-id="203f2-238">hello value must be a tuple of positive integers with a length that is hello arity of hello bundle.</span></span> <span data-ttu-id="203f2-239">這個 tuple 的每個元件必須等於或小於 hello 對應元件的**KernelShape**。</span><span class="sxs-lookup"><span data-stu-id="203f2-239">Each component of this tuple must be no greater than hello corresponding component of **KernelShape**.</span></span> <span data-ttu-id="203f2-240">hello 預設值是與所有元件等於 tooone tuple。</span><span class="sxs-lookup"><span data-stu-id="203f2-240">hello default value is a tuple with all components equal tooone.</span></span> 
* <span data-ttu-id="203f2-241">**共用**: （選擇性） 的定義 hello 權數分享 hello convolution 的每個維度。</span><span class="sxs-lookup"><span data-stu-id="203f2-241">**Sharing**: (optional) Defines hello weight sharing for each dimension of hello convolution.</span></span> <span data-ttu-id="203f2-242">hello 值可以是單一的布林值或長度是 hello arity hello 組合的布林值的 tuple。</span><span class="sxs-lookup"><span data-stu-id="203f2-242">hello value can be a single Boolean value or a tuple of Boolean values with a length that is hello arity of hello bundle.</span></span> <span data-ttu-id="203f2-243">單一布林值是擴充的 toobe hello 與所有元件的正確長度的 tuple toohello 等於指定的值。</span><span class="sxs-lookup"><span data-stu-id="203f2-243">A single Boolean value is extended toobe a tuple of hello correct length with all components equal toohello specified value.</span></span> <span data-ttu-id="203f2-244">hello 預設值是 tuple 所組成，則為 True 的所有值。</span><span class="sxs-lookup"><span data-stu-id="203f2-244">hello default value is a tuple that consists of all True values.</span></span> 
* <span data-ttu-id="203f2-245">**MapCount**: hello convolutional 組合對應 （選擇性） 定義 hello 數項功能。</span><span class="sxs-lookup"><span data-stu-id="203f2-245">**MapCount**: (optional) Defines hello number of feature maps for hello convolutional bundle.</span></span> <span data-ttu-id="203f2-246">hello 值可以是單一的正整數或 tuple 的長度是 hello arity hello 組合的正整數。</span><span class="sxs-lookup"><span data-stu-id="203f2-246">hello value can be a single positive integer or a tuple of positive integers with a length that is hello arity of hello bundle.</span></span> <span data-ttu-id="203f2-247">一個整數值擴充 toobe hello 與 hello 第一個元件等於 toohello 的正確長度的 tuple 指定值與所有 hello 其餘元件等於 tooone。</span><span class="sxs-lookup"><span data-stu-id="203f2-247">A single integer value is extended toobe a tuple of hello correct length with hello first components equal toohello specified value and all hello remaining components equal tooone.</span></span> <span data-ttu-id="203f2-248">hello 預設值為 1。</span><span class="sxs-lookup"><span data-stu-id="203f2-248">hello default value is one.</span></span> <span data-ttu-id="203f2-249">hello 總數的對應功能是 hello 產品的 hello tuple 的 hello 元件。</span><span class="sxs-lookup"><span data-stu-id="203f2-249">hello total number of feature maps is hello product of hello components of hello tuple.</span></span> <span data-ttu-id="203f2-250">此總數的分解 hello 元件之間的 hello 決定 hello 功能對應值 hello 目的地節點中分組的方式。</span><span class="sxs-lookup"><span data-stu-id="203f2-250">hello factoring of this total number across hello components determines how hello feature map values are grouped in hello destination nodes.</span></span> 
* <span data-ttu-id="203f2-251">**加權**: （選擇性） 定義 hello 初始的加權 hello 組合。</span><span class="sxs-lookup"><span data-stu-id="203f2-251">**Weights**: (optional) Defines hello initial weights for hello bundle.</span></span> <span data-ttu-id="203f2-252">hello 值必須是 tuple 的浮點值是核心時間的每個核心，加權 hello 數目的 hello 數目，如本文稍後所定義的長度。</span><span class="sxs-lookup"><span data-stu-id="203f2-252">hello value must be a tuple of floating point values with a length that is hello number of kernels times hello number of weights per kernel, as defined later in this article.</span></span> <span data-ttu-id="203f2-253">隨機產生的 hello 預設權數。</span><span class="sxs-lookup"><span data-stu-id="203f2-253">hello default weights are randomly generated.</span></span>  

<span data-ttu-id="203f2-254">有兩個集合的控制與邊框距離 hello 屬性正在互斥的屬性：</span><span class="sxs-lookup"><span data-stu-id="203f2-254">There are two sets of properties that control padding, hello properties being mutually exclusive:</span></span>

* <span data-ttu-id="203f2-255">**填補**: （選擇性） 決定應該湊足 hello 的輸入是否使用**預設填補配置**。</span><span class="sxs-lookup"><span data-stu-id="203f2-255">**Padding**: (optional) Determines whether hello input should be padded by using a **default padding scheme**.</span></span> <span data-ttu-id="203f2-256">hello 值可以是單一的布林值，或長度是 hello arity hello 組合的布林值的 tuple。</span><span class="sxs-lookup"><span data-stu-id="203f2-256">hello value can be a single Boolean value, or it can be a tuple of Boolean values with a length that is hello arity of hello bundle.</span></span> <span data-ttu-id="203f2-257">單一布林值是擴充的 toobe hello 與所有元件的正確長度的 tuple toohello 等於指定的值。</span><span class="sxs-lookup"><span data-stu-id="203f2-257">A single Boolean value is extended toobe a tuple of hello correct length with all components equal toohello specified value.</span></span> <span data-ttu-id="203f2-258">如果維度 hello 值為 True，hello 來源邏輯填補與零值資料格 toosupport 額外的核心應用程式，該維度中的 hello 的 hello 該維度中的第一個和最後一個核心的中央節點 hello 第一個和最後一個節點hello 來源層級中的維度。</span><span class="sxs-lookup"><span data-stu-id="203f2-258">If hello value for a dimension is True, hello source is logically padded in that dimension with zero-valued cells toosupport additional kernel applications, such that hello central nodes of hello first and last kernels in that dimension are hello first and last nodes in that dimension in hello source layer.</span></span> <span data-ttu-id="203f2-259">因此，每個維度中的"dummy"節點的 hello 數目不會自動決定，toofit 完全*(InputShape [d]-1) / Stride [d] + 1*到 hello 填補來源層級的核心。</span><span class="sxs-lookup"><span data-stu-id="203f2-259">Thus, hello number of "dummy" nodes in each dimension is determined automatically, toofit exactly *(InputShape[d] - 1) / Stride[d] + 1* kernels into hello padded source layer.</span></span> <span data-ttu-id="203f2-260">如果維度 hello 值為 False，hello 核心定義，因此 hello 中省略了每一端上的節點數目是 hello 相同 （向上 tooa 差異為 1）。</span><span class="sxs-lookup"><span data-stu-id="203f2-260">If hello value for a dimension is False, hello kernels are defined so that hello number of nodes on each side that are left out is hello same (up tooa difference of 1).</span></span> <span data-ttu-id="203f2-261">hello 這個屬性的預設值是與所有元件等於 tooFalse tuple。</span><span class="sxs-lookup"><span data-stu-id="203f2-261">hello default value of this attribute is a tuple with all components equal tooFalse.</span></span>
* <span data-ttu-id="203f2-262">**UpperPad**和**LowerPad**: （選擇性） 提供較大的控制權 hello 填補 toouse 數量。</span><span class="sxs-lookup"><span data-stu-id="203f2-262">**UpperPad** and **LowerPad**: (optional) Provide greater control over hello amount of padding toouse.</span></span> <span data-ttu-id="203f2-263">**重要事項：**可以定義這些屬性，並且在 hello**填補**上述的屬性是***不***定義。</span><span class="sxs-lookup"><span data-stu-id="203f2-263">**Important:** These attributes can be defined if and only if hello **Padding** property above is ***not*** defined.</span></span> <span data-ttu-id="203f2-264">hello 值應該是整數值 tuple 的 hello arity hello 組合的長度。</span><span class="sxs-lookup"><span data-stu-id="203f2-264">hello values should be integer-valued tuples with lengths that are hello arity of hello bundle.</span></span> <span data-ttu-id="203f2-265">當指定這些屬性時，"dummy"節點可加入 toohello 較低，與 hello 的每個維度的上限結束輸入層。</span><span class="sxs-lookup"><span data-stu-id="203f2-265">When these attributes are specified, "dummy" nodes are added toohello lower and upper ends of each dimension of hello input layer.</span></span> <span data-ttu-id="203f2-266">hello 的節點數目加入 toohello 較低而且在每個維度中的上方結束由**LowerPad**[i] 和**UpperPad**[i] 分別。</span><span class="sxs-lookup"><span data-stu-id="203f2-266">hello number of nodes added toohello lower and upper ends in each dimension is determined by **LowerPad**[i] and **UpperPad**[i] respectively.</span></span> <span data-ttu-id="203f2-267">必須符合 tooensure 的核心對應至僅太 「 實際的 「 節點與不太"dummy"的節點，hello 下列條件：</span><span class="sxs-lookup"><span data-stu-id="203f2-267">tooensure that kernels correspond only too"real" nodes and not too"dummy" nodes, hello following conditions must be met:</span></span>
  * <span data-ttu-id="203f2-268">**LowerPad** 的每個元件皆務必小於 KernelShape[d]/2。</span><span class="sxs-lookup"><span data-stu-id="203f2-268">Each component of **LowerPad** must be strictly less than KernelShape[d]/2.</span></span> 
  * <span data-ttu-id="203f2-269">**UpperPad** 的每個元件皆不可大於 KernelShape[d]/2。</span><span class="sxs-lookup"><span data-stu-id="203f2-269">Each component of **UpperPad** must be no greater than KernelShape[d]/2.</span></span> 
  * <span data-ttu-id="203f2-270">這些屬性的 hello 預設值是與所有元件等於 too0 tuple。</span><span class="sxs-lookup"><span data-stu-id="203f2-270">hello default value of these attributes is a tuple with all components equal too0.</span></span> 

<span data-ttu-id="203f2-271">hello 設定**填補**= true 可讓多填補現狀視 tookeep hello"center"hello 核心的"real"輸入 hello 內。</span><span class="sxs-lookup"><span data-stu-id="203f2-271">hello setting **Padding** = true allows as much padding as is needed tookeep hello "center" of hello kernel inside hello "real" input.</span></span> <span data-ttu-id="203f2-272">這樣會變更 hello 數學運算 hello 輸出大小的位元。</span><span class="sxs-lookup"><span data-stu-id="203f2-272">This changes hello math a bit for computing hello output size.</span></span> <span data-ttu-id="203f2-273">一般而言，hello 輸出大小*D*計算方式為*D = (I-K) / S + 1*，其中*我*hello 輸入大小， *K* hello 核心大小， *S*是 hello 分散和 */* 是整數除法 （圓趨近於零）。</span><span class="sxs-lookup"><span data-stu-id="203f2-273">Generally, hello output size *D* is computed as *D = (I - K) / S + 1*, where *I* is hello input size, *K* is hello kernel size, *S* is hello stride, and */* is integer division (round toward zero).</span></span> <span data-ttu-id="203f2-274">如果您設定 UpperPad = [1，1] hello 輸入大小*我*實際上是 29，因此*D = (29-5) / 2 + 1 = 13*。</span><span class="sxs-lookup"><span data-stu-id="203f2-274">If you set UpperPad = [1, 1], hello input size *I* is effectively 29, and thus *D = (29 - 5) / 2 + 1 = 13*.</span></span> <span data-ttu-id="203f2-275">不過，當 **Padding** = true 時，基本上 *I* 會藉由 *K - 1* 而提高；因此 *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*。</span><span class="sxs-lookup"><span data-stu-id="203f2-275">However, when **Padding** = true, essentially *I* gets bumped up by *K - 1*; hence *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*.</span></span> <span data-ttu-id="203f2-276">藉由指定的值**UpperPad**和**LowerPad**取得更多控制權填補比您剛才設定的 hello**填補**= true。</span><span class="sxs-lookup"><span data-stu-id="203f2-276">By specifying values for **UpperPad** and **LowerPad** you get much more control over hello padding than if you just set **Padding** = true.</span></span>

<span data-ttu-id="203f2-277">如需迴旋網路及其應用程式的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="203f2-277">For more information about convolutional networks and their applications, see these articles:</span></span>  

* [<span data-ttu-id="203f2-278">http://deeplearning.net/tutorial/lenet.html </span><span class="sxs-lookup"><span data-stu-id="203f2-278">http://deeplearning.net/tutorial/lenet.html </span></span>](http://deeplearning.net/tutorial/lenet.html)
* [<span data-ttu-id="203f2-279">http://research.microsoft.com/pubs/68920/icdar03.pdf</span><span class="sxs-lookup"><span data-stu-id="203f2-279">http://research.microsoft.com/pubs/68920/icdar03.pdf</span></span>](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
* [<span data-ttu-id="203f2-280">http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf</span><span class="sxs-lookup"><span data-stu-id="203f2-280">http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf</span></span>](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a><span data-ttu-id="203f2-281">集區套組</span><span class="sxs-lookup"><span data-stu-id="203f2-281">Pooling bundles</span></span>
<span data-ttu-id="203f2-282">A**共用配套**適用於幾何類似 tooconvolutional 連線，但是它會使用預先定義的函式 toosource 節點值 tooderive hello 目的地節點值。</span><span class="sxs-lookup"><span data-stu-id="203f2-282">A **pooling bundle** applies geometry similar tooconvolutional connectivity, but it uses predefined functions toosource node values tooderive hello destination node value.</span></span> <span data-ttu-id="203f2-283">因此，集區套組並沒有可訓練的狀態 (加權或偏差)。</span><span class="sxs-lookup"><span data-stu-id="203f2-283">Hence, pooling bundles have no trainable state (weights or biases).</span></span> <span data-ttu-id="203f2-284">共用組合支援所有 hello convolutional 屬性除了**共用**， **MapCount**，和**加權**。</span><span class="sxs-lookup"><span data-stu-id="203f2-284">Pooling bundles support all hello convolutional attributes except **Sharing**, **MapCount**, and **Weights**.</span></span>  

<span data-ttu-id="203f2-285">一般而言，相鄰的集區單元的摘要 hello 核心不會重疊。</span><span class="sxs-lookup"><span data-stu-id="203f2-285">Typically, hello kernels summarized by adjacent pooling units do not overlap.</span></span> <span data-ttu-id="203f2-286">如果每個維度中的相等 tooKernelShape [d] [d] 的分散，取得 hello 層是 hello 傳統本機共用層，其通常會採用 convolutional 類神經網路。</span><span class="sxs-lookup"><span data-stu-id="203f2-286">If Stride[d] is equal tooKernelShape[d] in each dimension, hello layer obtained is hello traditional local pooling layer, which is commonly employed in convolutional neural networks.</span></span> <span data-ttu-id="203f2-287">每個目的地節點計算最大的 hello 或 hello 活動，其核心 hello 來源層級中的 hello 平均值。</span><span class="sxs-lookup"><span data-stu-id="203f2-287">Each destination node computes hello maximum or hello mean of hello activities of its kernel in hello source layer.</span></span>  

<span data-ttu-id="203f2-288">hello 下列範例將說明共用的組合：</span><span class="sxs-lookup"><span data-stu-id="203f2-288">hello following example illustrates a pooling bundle:</span></span> 

    hidden P1 [5, 12, 12]
      from C1 max pool {
        InputShape  = [ 5, 24, 24];
        KernelShape = [ 1,  2,  2];
        Stride      = [ 1,  2,  2];
      }  

* <span data-ttu-id="203f2-289">hello 組合的 hello arity 為 3 (hello 長度的 hello tuple **InputShape**， **KernelShape**，和**Stride**)。</span><span class="sxs-lookup"><span data-stu-id="203f2-289">hello arity of hello bundle is 3 (hello length of hello tuples **InputShape**, **KernelShape**, and **Stride**).</span></span> 
* <span data-ttu-id="203f2-290">hello hello 來源層的節點數目是*5 * 24 * 24 = 2880*。</span><span class="sxs-lookup"><span data-stu-id="203f2-290">hello number of nodes in hello source layer is *5 * 24 * 24 = 2880*.</span></span> 
* <span data-ttu-id="203f2-291">這是傳統本端集區層，因為 **KernelShape** 和 **Stride** 是相等的。</span><span class="sxs-lookup"><span data-stu-id="203f2-291">This is a traditional local pooling layer because **KernelShape** and **Stride** are equal.</span></span> 
* <span data-ttu-id="203f2-292">hello hello 目的地層的節點數目是*5 * 12 * 12 = 1440*。</span><span class="sxs-lookup"><span data-stu-id="203f2-292">hello number of nodes in hello destination layer is *5 * 12 * 12 = 1440*.</span></span>  

<span data-ttu-id="203f2-293">如需集區層的詳細資訊，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="203f2-293">For more information about pooling layers, see these articles:</span></span>  

* <span data-ttu-id="203f2-294">[http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (3.4 小節)</span><span class="sxs-lookup"><span data-stu-id="203f2-294">[http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (Section 3.4)</span></span>
* [<span data-ttu-id="203f2-295">http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf</span><span class="sxs-lookup"><span data-stu-id="203f2-295">http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf</span></span>](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
* [<span data-ttu-id="203f2-296">http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf</span><span class="sxs-lookup"><span data-stu-id="203f2-296">http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf</span></span>](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a><span data-ttu-id="203f2-297">回應正規化套組</span><span class="sxs-lookup"><span data-stu-id="203f2-297">Response normalization bundles</span></span>
<span data-ttu-id="203f2-298">**回應正規化**是首次推出的 Geoffrey Hinton 本機正規化配置 box hello 份文件中[深層 Convolutional 的類神經網路與 ImageNet Classiﬁcation](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf)。</span><span class="sxs-lookup"><span data-stu-id="203f2-298">**Response normalization** is a local normalization scheme that was first introduced by Geoffrey Hinton, et al, in hello paper [ImageNet Classiﬁcation with Deep Convolutional Neural Networks](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf).</span></span> <span data-ttu-id="203f2-299">回應 「 正規化 」 是在類神經網路使用的 tooaid 一般化。</span><span class="sxs-lookup"><span data-stu-id="203f2-299">Response normalization is used tooaid generalization in neural nets.</span></span> <span data-ttu-id="203f2-300">當另一個神經會引發在極高的啟用層級時，本機回應正規化圖層會隱藏周圍神經 hello hello 啟用層級。</span><span class="sxs-lookup"><span data-stu-id="203f2-300">When one neuron is firing at a very high activation level, a local response normalization layer suppresses hello activation level of hello surrounding neurons.</span></span> <span data-ttu-id="203f2-301">此動作會使用三個參數 (***α***、***β*** 和 ***k***) 與迴旋結構 (或鄰區分布型態) 來完成。</span><span class="sxs-lookup"><span data-stu-id="203f2-301">This is done by using three parameters (***α***, ***β***, and ***k***) and a convolutional structure (or neighborhood shape).</span></span> <span data-ttu-id="203f2-302">Hello 目的地階層中的每一個神經***y***對應 tooa 神經***x*** hello 來源層級中。</span><span class="sxs-lookup"><span data-stu-id="203f2-302">Every neuron in hello destination layer ***y*** corresponds tooa neuron ***x*** in hello source layer.</span></span> <span data-ttu-id="203f2-303">hello 的啟用層級***y*** hello 下列公式，就會提供其中***f*** hello 啟用層級的神經，以及***Nx*** hello 核心 （或 hello 集，其中包含 hello中的 hello 鄰居神經***x***)，如下列 convolutional 結構 hello 所定義：</span><span class="sxs-lookup"><span data-stu-id="203f2-303">hello activation level of ***y*** is given by hello following formula, where ***f*** is hello activation level of a neuron, and ***Nx*** is hello kernel (or hello set that contains hello neurons in hello neighborhood of ***x***), as defined by hello following convolutional structure:</span></span>  

![][1]  

<span data-ttu-id="203f2-304">回應正規化組合支援所有的 hello convolutional 屬性除了**共用**， **MapCount**，和**加權**。</span><span class="sxs-lookup"><span data-stu-id="203f2-304">Response normalization bundles support all hello convolutional attributes except **Sharing**, **MapCount**, and **Weights**.</span></span>  

* <span data-ttu-id="203f2-305">如果 hello 核心包含神經 hello 相同將對應為***x***，hello 正規化配置是參照的 tooas**相同對應正規化**。</span><span class="sxs-lookup"><span data-stu-id="203f2-305">If hello kernel contains neurons in hello same map as ***x***, hello normalization scheme is referred tooas **same map normalization**.</span></span> <span data-ttu-id="203f2-306">toodefine 相同對應中的 hello 第一個座標的正規化**InputShape**必須 hello 值 1。</span><span class="sxs-lookup"><span data-stu-id="203f2-306">toodefine same map normalization, hello first coordinate in **InputShape** must have hello value 1.</span></span>
* <span data-ttu-id="203f2-307">如果 hello 核心包含神經 hello 相同空間位置***x***，但 hello 神經位於其他對應，稱為 hello 正規化配置**透過對應正規化**。</span><span class="sxs-lookup"><span data-stu-id="203f2-307">If hello kernel contains neurons in hello same spatial position as ***x***, but hello neurons are in other maps, hello normalization scheme is called **across maps normalization**.</span></span> <span data-ttu-id="203f2-308">這類回應正規化會實作一種橫向 inhibition hello 類型中實際的神經，找到建立大啟用層級，在計算的不同對應的神經輸出之間的競爭所啟發。</span><span class="sxs-lookup"><span data-stu-id="203f2-308">This type of response normalization implements a form of lateral inhibition inspired by hello type found in real neurons, creating competition for big activation levels amongst neuron outputs computed on different maps.</span></span> <span data-ttu-id="203f2-309">跨 toodefine 對應正規化、 hello 第一個座標必須是大於 1 且不大於對應的 hello 數目的整數和 hello 座標 hello 其餘部分都必須有 hello 值 1。</span><span class="sxs-lookup"><span data-stu-id="203f2-309">toodefine across maps normalization, hello first coordinate must be an integer greater than one and no greater than hello number of maps, and hello rest of hello coordinates must have hello value 1.</span></span>  

<span data-ttu-id="203f2-310">回應正規化組合套用預先定義的函式 toosource 節點值 toodetermine hello 目的地節點值，因為它們會有任何 trainable 的狀態 （「 加權 」 或 「 徵才偏差 」）。</span><span class="sxs-lookup"><span data-stu-id="203f2-310">Because response normalization bundles apply a predefined function toosource node values toodetermine hello destination node value, they have no trainable state (weights or biases).</span></span>   

<span data-ttu-id="203f2-311">**警示**: hello 目的地階層中的 hello 節點對應 tooneurons 屬於 hello 的 hello 核心的中央節點。</span><span class="sxs-lookup"><span data-stu-id="203f2-311">**Alert**: hello nodes in hello destination layer correspond tooneurons that are hello central nodes of hello kernels.</span></span> <span data-ttu-id="203f2-312">例如，如果 KernelShape [d] 是奇數，則*KernelShape [d] / 2*對應 toohello 中央核心節點。</span><span class="sxs-lookup"><span data-stu-id="203f2-312">For example, if KernelShape[d] is odd, then *KernelShape[d]/2* corresponds toohello central kernel node.</span></span> <span data-ttu-id="203f2-313">如果*KernelShape [d]*是奇數，hello 中央節點位於*KernelShape [d] / [2-1*。</span><span class="sxs-lookup"><span data-stu-id="203f2-313">If *KernelShape[d]* is even, hello central node is at *KernelShape[d]/2 - 1*.</span></span> <span data-ttu-id="203f2-314">因此，如果**填補**[d] 為 False 時，第一次 hello 和上次 hello *KernelShape [d] / 2*節點 hello 目的圖層中沒有對應的節點。</span><span class="sxs-lookup"><span data-stu-id="203f2-314">Therefore, if **Padding**[d] is False, hello first and hello last *KernelShape[d]/2* nodes do not have corresponding nodes in hello destination layer.</span></span> <span data-ttu-id="203f2-315">tooavoid 這種情況下，定義**填補**做為 [為 true，true，...，true]。</span><span class="sxs-lookup"><span data-stu-id="203f2-315">tooavoid this situation, define **Padding** as [true, true, …, true].</span></span>  

<span data-ttu-id="203f2-316">此外 toohello 四個屬性稍早所述，回應正規化組合也支援 hello 下列屬性：</span><span class="sxs-lookup"><span data-stu-id="203f2-316">In addition toohello four attributes described earlier, response normalization bundles also support hello following attributes:</span></span>  

* <span data-ttu-id="203f2-317">**Alpha**: （必要） 指定浮點值，對應太***α*** hello 先前公式中。</span><span class="sxs-lookup"><span data-stu-id="203f2-317">**Alpha**: (required) Specifies a floating-point value that corresponds too***α*** in hello previous formula.</span></span> 
* <span data-ttu-id="203f2-318">**Beta**: （必要） 指定浮點值，對應太***β*** hello 先前公式中。</span><span class="sxs-lookup"><span data-stu-id="203f2-318">**Beta**: (required) Specifies a floating-point value that corresponds too***β*** in hello previous formula.</span></span> 
* <span data-ttu-id="203f2-319">**位移**: （選擇性） 指定浮點值，對應太***k*** hello 先前公式中。</span><span class="sxs-lookup"><span data-stu-id="203f2-319">**Offset**: (optional) Specifies a floating-point value that corresponds too***k*** in hello previous formula.</span></span> <span data-ttu-id="203f2-320">預設 too1。</span><span class="sxs-lookup"><span data-stu-id="203f2-320">It defaults too1.</span></span>  

<span data-ttu-id="203f2-321">hello 下列範例會定義使用這些屬性的回應正規化組合：</span><span class="sxs-lookup"><span data-stu-id="203f2-321">hello following example defines a response normalization bundle using these attributes:</span></span>  

    hidden RN1 [5, 10, 10]
      from P1 response norm {
        InputShape  = [ 5, 12, 12];
        KernelShape = [ 1,  3,  3];
        Alpha = 0.001;
        Beta = 0.75;
      }  

* <span data-ttu-id="203f2-322">hello 來源圖層都包含五個對應，各有很少維度為 12 x 12，加總 1440年節點中。</span><span class="sxs-lookup"><span data-stu-id="203f2-322">hello source layer includes five maps, each with aof dimension of 12x12, totaling in 1440 nodes.</span></span> 
* <span data-ttu-id="203f2-323">hello 值**KernelShape**指出這是相同的對應正規化層，其中 hello 上的芳鄰 是 3x3 矩形。</span><span class="sxs-lookup"><span data-stu-id="203f2-323">hello value of **KernelShape** indicates that this is a same map normalization layer, where hello neighborhood is a 3x3 rectangle.</span></span> 
* <span data-ttu-id="203f2-324">hello 預設值是**填補**為 False，因此 hello 目的圖層的每個維度中的 10 個節點。</span><span class="sxs-lookup"><span data-stu-id="203f2-324">hello default value of **Padding** is False, thus hello destination layer has only 10 nodes in each dimension.</span></span> <span data-ttu-id="203f2-325">tooinclude 對應 tooevery 節點在 hello 來源層中，加入填補的 hello 目的地層中的一個節點 = [為 true，true，true]。和太變更 RN1 hello 大小 [5、 12、 12]。</span><span class="sxs-lookup"><span data-stu-id="203f2-325">tooinclude one node in hello destination layer that corresponds tooevery node in hello source layer, add Padding = [true, true, true]; and change hello size of RN1 too[5, 12, 12].</span></span>  

## <a name="share-declaration"></a><span data-ttu-id="203f2-326">共用宣告</span><span class="sxs-lookup"><span data-stu-id="203f2-326">Share declaration</span></span>
<span data-ttu-id="203f2-327">Net# 可選擇性地支援以共用加權定義多個套組的作業。</span><span class="sxs-lookup"><span data-stu-id="203f2-327">Net# optionally supports defining multiple bundles with shared weights.</span></span> <span data-ttu-id="203f2-328">如果其結構是 hello 相同，您可以共用任何兩個組合的 hello 加權。</span><span class="sxs-lookup"><span data-stu-id="203f2-328">hello weights of any two bundles can be shared if their structures are hello same.</span></span> <span data-ttu-id="203f2-329">hello，請使用下列語法會定義使用共用的加權的組合：</span><span class="sxs-lookup"><span data-stu-id="203f2-329">hello following syntax defines bundles with shared weights:</span></span>  

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

<span data-ttu-id="203f2-330">例如，hello 下列共用宣告指定 hello 圖層名稱，表示應該共用加權和徵才偏差：</span><span class="sxs-lookup"><span data-stu-id="203f2-330">For example, hello following share-declaration specifies hello layer names, indicating that both weights and biases should be shared:</span></span>  

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

* <span data-ttu-id="203f2-331">hello 的輸入的特徵會分割成兩個相等大小輸入層。</span><span class="sxs-lookup"><span data-stu-id="203f2-331">hello input features are partitioned into two equal sized input layers.</span></span> 
* <span data-ttu-id="203f2-332">hello 隱藏圖層計算 hello 兩個輸入的圖層上更高的層級功能。</span><span class="sxs-lookup"><span data-stu-id="203f2-332">hello hidden layers then compute higher level features on hello two input layers.</span></span> 
* <span data-ttu-id="203f2-333">hello 共用宣告指定*H1*和*H2*必須計算 hello 中相同的方式，從其個別的輸入。</span><span class="sxs-lookup"><span data-stu-id="203f2-333">hello share-declaration specifies that *H1* and *H2* must be computed in hello same way from their respective inputs.</span></span>  

<span data-ttu-id="203f2-334">或者，這也可以用兩個不同的共用宣告來指定，如下所示：</span><span class="sxs-lookup"><span data-stu-id="203f2-334">Alternatively, this could be specified with two separate share-declarations as follows:</span></span>  

    share { Data1 => H1, Data2 => H2 } // share weights  

<!-- -->

    share { 1 => H1, 1 => H2 } // share biases  

<span data-ttu-id="203f2-335">您可以在 hello 圖層包含單一配套時，才使用 hello 簡短形式。</span><span class="sxs-lookup"><span data-stu-id="203f2-335">You can use hello short form only when hello layers contain a single bundle.</span></span> <span data-ttu-id="203f2-336">一般情況下，共用時，可能只 hello 相關的結構完全相同，這表示它們有相同的大小相同 convolutional geometry、 和等的 hello。</span><span class="sxs-lookup"><span data-stu-id="203f2-336">In general, sharing is possible only when hello relevant structure is identical, meaning that they have hello same size, same convolutional geometry, and so forth.</span></span>  

## <a name="examples-of-net-usage"></a><span data-ttu-id="203f2-337">Net# 的使用範例</span><span class="sxs-lookup"><span data-stu-id="203f2-337">Examples of Net# usage</span></span>
<span data-ttu-id="203f2-338">本節提供一些範例，告訴您可以使用 Net # tooadd 隱藏圖層上，定義 hello 方式隱藏的層互動的其他圖層，並建置 convolutional 網路。</span><span class="sxs-lookup"><span data-stu-id="203f2-338">This section provides some examples of how you can use Net# tooadd hidden layers, define hello way that hidden layers interact with other layers, and build convolutional networks.</span></span>   

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a><span data-ttu-id="203f2-339">定義簡易的自訂類神經網路："Hello World" 範例</span><span class="sxs-lookup"><span data-stu-id="203f2-339">Define a simple custom neural network: "Hello World" example</span></span>
<span data-ttu-id="203f2-340">這個簡單的範例示範如何 toocreate 的類神經網路模型有單一隱藏的層。</span><span class="sxs-lookup"><span data-stu-id="203f2-340">This simple example demonstrates how toocreate a neural network model that has a single hidden layer.</span></span>  

    input Data auto;
    hidden H [200] from Data all;
    output Out [10] sigmoid from H all;  

<span data-ttu-id="203f2-341">hello 範例將說明一些基本命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="203f2-341">hello example illustrates some basic commands as follows:</span></span>  

* <span data-ttu-id="203f2-342">hello 第一行定義 hello 輸入的層 (名為*資料*)。</span><span class="sxs-lookup"><span data-stu-id="203f2-342">hello first line defines hello input layer (named *Data*).</span></span> <span data-ttu-id="203f2-343">當您使用 hello**自動**關鍵字，hello 類神經網路會自動在 hello 輸入範例中包含所有特徵資料行。</span><span class="sxs-lookup"><span data-stu-id="203f2-343">When you use hello  **auto** keyword, hello neural network automatically includes all feature columns in hello input examples.</span></span> 
* <span data-ttu-id="203f2-344">hello 第二行建立 hello 隱藏圖層。</span><span class="sxs-lookup"><span data-stu-id="203f2-344">hello second line creates hello hidden layer.</span></span> <span data-ttu-id="203f2-345">hello 名稱*H*指派 toohello 隱藏的層，其具有 200 的節點。</span><span class="sxs-lookup"><span data-stu-id="203f2-345">hello name *H* is assigned toohello hidden layer, which has 200 nodes.</span></span> <span data-ttu-id="203f2-346">此圖層是完全連接的 toohello 輸入的層。</span><span class="sxs-lookup"><span data-stu-id="203f2-346">This layer is fully connected toohello input layer.</span></span>
* <span data-ttu-id="203f2-347">hello 第三行定義 hello 輸出層 (名為*O*)，其中包含 10 個輸出節點。</span><span class="sxs-lookup"><span data-stu-id="203f2-347">hello third line defines hello output layer (named *O*), which contains 10 output nodes.</span></span> <span data-ttu-id="203f2-348">如果 hello 類神經網路會用於分類，則每個類別的一個輸出節點。</span><span class="sxs-lookup"><span data-stu-id="203f2-348">If hello neural network is used for classification, there is one output node per class.</span></span> <span data-ttu-id="203f2-349">hello 關鍵字**sigmoid**表示 hello 輸出函式是套用的 toohello 輸出層。</span><span class="sxs-lookup"><span data-stu-id="203f2-349">hello keyword **sigmoid** indicates that hello output function is applied toohello output layer.</span></span>   

### <a name="define-multiple-hidden-layers-computer-vision-example"></a><span data-ttu-id="203f2-350">定義多個隱藏層：電腦願景範例</span><span class="sxs-lookup"><span data-stu-id="203f2-350">Define multiple hidden layers: computer vision example</span></span>
<span data-ttu-id="203f2-351">hello 下列範例會示範如何 toodefine 稍微更為複雜的類神經網路，具有多個自訂的隱藏層。</span><span class="sxs-lookup"><span data-stu-id="203f2-351">hello following example demonstrates how toodefine a slightly more complex neural network, with multiple custom hidden layers.</span></span>  

    // Define hello input layers 
    input Pixels [10, 20];
    input MetaData [7];

    // Define hello first two hidden layers, using data only from hello Pixels input
    hidden ByRow [10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol [5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;

    // Define hello third hidden layer, which uses as source hello hidden layers ByRow and ByCol
    hidden Gather [100] 
    {
      from ByRow all;
      from ByCol all;
    }

    // Define hello output layer and its sources
    output Result [10]  
    {
      from Gather all;
      from MetaData all;
    }  

<span data-ttu-id="203f2-352">這個範例將說明 hello 類神經網路規格語言的數個功能：</span><span class="sxs-lookup"><span data-stu-id="203f2-352">This example illustrates several features of hello neural networks specification language:</span></span>  

* <span data-ttu-id="203f2-353">hello 結構有兩個輸入的圖層，*像素為單位*和*中繼資料*。</span><span class="sxs-lookup"><span data-stu-id="203f2-353">hello structure has two input layers, *Pixels* and *MetaData*.</span></span>
* <span data-ttu-id="203f2-354">hello*像素為單位*層是兩個連線組合，來源層級與目的地層*ByRow*和*ByCol*。</span><span class="sxs-lookup"><span data-stu-id="203f2-354">hello *Pixels* layer is a source layer for two connection bundles, with destination layers, *ByRow* and *ByCol*.</span></span>
* <span data-ttu-id="203f2-355">hello 層*收集*和*結果*目的地層中多個連接的組合。</span><span class="sxs-lookup"><span data-stu-id="203f2-355">hello layers *Gather* and *Result* are destination layers in multiple connection bundles.</span></span>
* <span data-ttu-id="203f2-356">hello 輸出層中，*結果*，目的地階層中兩個連線組合，則為其中一個 hello 與第二層做為目的圖層的 隱藏 （收集） 和其他 hello 輸入層 （中繼資料） 與 hello 做為目的地階層。</span><span class="sxs-lookup"><span data-stu-id="203f2-356">hello output layer, *Result*, is a destination layer in two connection bundles; one with hello second level hidden (Gather) as a destination layer, and hello other with hello input layer (MetaData) as a destination layer.</span></span>
* <span data-ttu-id="203f2-357">hello 隱藏的層， *ByRow*和*ByCol*，已篩選的連線使用指定的述詞運算式。</span><span class="sxs-lookup"><span data-stu-id="203f2-357">hello hidden layers, *ByRow* and *ByCol*, specify filtered connectivity by using predicate expressions.</span></span> <span data-ttu-id="203f2-358">更明確地說，在 hello 節點*ByRow*在 [x，y] 是在連接的 toohello 節點*像素為單位*具有 hello 第一個索引座標等於 toohello 節點的第一個座標，x。</span><span class="sxs-lookup"><span data-stu-id="203f2-358">More precisely, hello node in *ByRow* at [x, y] is connected toohello nodes in *Pixels* that have hello first index coordinate equal toohello node's first coordinate, x.</span></span> <span data-ttu-id="203f2-359">同樣地，在 hello 節點*ByCol 在 [x，y] 是在 _Pixels 連接的 toohello 節點*hello 第二個索引座標的 hello 節點的第二個座標，其中一個內有 y。</span><span class="sxs-lookup"><span data-stu-id="203f2-359">Similarly, hello node in *ByCol at [x, y] is connected toohello nodes in _Pixels* that have hello second index coordinate within one of hello node's second coordinate, y.</span></span>  

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a><span data-ttu-id="203f2-360">定義多類別分類的迴旋網路：數字辨識範例</span><span class="sxs-lookup"><span data-stu-id="203f2-360">Define a convolutional network for multiclass classification: digit recognition example</span></span>
<span data-ttu-id="203f2-361">hello hello 遵循網路定義是設計的 toorecognize 數字，它會說明一些進階的技術，用於自訂類神經網路。</span><span class="sxs-lookup"><span data-stu-id="203f2-361">hello definition of hello following network is designed toorecognize numbers, and it illustrates some advanced techniques for customizing a neural network.</span></span>  

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


* <span data-ttu-id="203f2-362">hello 結構具有單一輸入的層中，*映像*。</span><span class="sxs-lookup"><span data-stu-id="203f2-362">hello structure has a single input layer, *Image*.</span></span>
* <span data-ttu-id="203f2-363">hello 關鍵字**convolve**指出 hello 圖層命名*Conv1*和*Conv2* convolutional 層。</span><span class="sxs-lookup"><span data-stu-id="203f2-363">hello keyword **convolve** indicates that hello layers named *Conv1* and *Conv2* are convolutional layers.</span></span> <span data-ttu-id="203f2-364">每個這些圖層的宣告後面的 hello convolution 屬性清單。</span><span class="sxs-lookup"><span data-stu-id="203f2-364">Each of these layer declarations is followed by a list of hello convolution attributes.</span></span>
* <span data-ttu-id="203f2-365">hello net 有第三個隱藏層， *Hid3*，也就是完全連接 toohello 第二個隱藏的層， *Conv2*。</span><span class="sxs-lookup"><span data-stu-id="203f2-365">hello net has a third hidden layer, *Hid3*, which is fully connected toohello second hidden layer, *Conv2*.</span></span>
* <span data-ttu-id="203f2-366">hello 輸出層中，*位數*，是連接的唯一 toohello 第三個隱藏的層， *Hid3*。</span><span class="sxs-lookup"><span data-stu-id="203f2-366">hello output layer, *Digit*, is connected only toohello third hidden layer, *Hid3*.</span></span> <span data-ttu-id="203f2-367">hello 關鍵字**所有**指出該 hello 輸出層完全連接太*Hid3*。</span><span class="sxs-lookup"><span data-stu-id="203f2-367">hello keyword **all** indicates that hello output layer is fully connected too*Hid3*.</span></span>
* <span data-ttu-id="203f2-368">hello 的 hello convolution arity 是三 (hello 長度的 hello tuple **InputShape**， **KernelShape**， **Stride**，和**共用**)。</span><span class="sxs-lookup"><span data-stu-id="203f2-368">hello arity of hello convolution is three (hello length of hello tuples **InputShape**, **KernelShape**, **Stride**, and **Sharing**).</span></span> 
* <span data-ttu-id="203f2-369">每個核心的加權的 hello 數目是*1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape** \[2] = 1 + 1 * 5 * 5 = 26。或是 26 * 50 = 1300*。</span><span class="sxs-lookup"><span data-stu-id="203f2-369">hello number of weights per kernel is *1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape**\[2] = 1 + 1 * 5 * 5 = 26. Or 26 * 50 = 1300*.</span></span>
* <span data-ttu-id="203f2-370">您可以計算每個隱藏層中的 hello 節點，如下所示：</span><span class="sxs-lookup"><span data-stu-id="203f2-370">You can calculate hello nodes in each hidden layer as follows:</span></span>
  * <span data-ttu-id="203f2-371">**NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.</span><span class="sxs-lookup"><span data-stu-id="203f2-371">**NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.</span></span>
  * <span data-ttu-id="203f2-372">**NodeCount**\[1] = (13 - 5) / 2 + 1 = 5。</span><span class="sxs-lookup"><span data-stu-id="203f2-372">**NodeCount**\[1] = (13 - 5) / 2 + 1 = 5.</span></span> 
  * <span data-ttu-id="203f2-373">**NodeCount**\[2] = (13 - 5) / 2 + 1 = 5。</span><span class="sxs-lookup"><span data-stu-id="203f2-373">**NodeCount**\[2] = (13 - 5) / 2 + 1 = 5.</span></span> 
* <span data-ttu-id="203f2-374">hello 的節點總數計算方式是使用宣告的 hello 維度 hello 圖層，[50，5，5]，如下所示：  ***MapCount** * **NodeCount** \[0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*</span><span class="sxs-lookup"><span data-stu-id="203f2-374">hello total number of nodes can be calculated by using hello declared dimensionality of hello layer, [50, 5, 5], as follows: ***MapCount** * **NodeCount**\[0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*</span></span>
* <span data-ttu-id="203f2-375">因為**共用**[d] 設為 False 僅適用於*d = = 0*，hello 核心的數目是 ***MapCount** * **NodeCount** \[0] = 10 * 5 = 50*。</span><span class="sxs-lookup"><span data-stu-id="203f2-375">Because **Sharing**[d] is False only for *d == 0*, hello number of kernels is ***MapCount** * **NodeCount**\[0] = 10 * 5 = 50*.</span></span> 

## <a name="acknowledgements"></a><span data-ttu-id="203f2-376">通知</span><span class="sxs-lookup"><span data-stu-id="203f2-376">Acknowledgements</span></span>
<span data-ttu-id="203f2-377">hello Net # 自訂類神經網路的 hello 架構的語言是由 Shon Katzenberger （架構設計人員、 機器學習） 和 Alexey Kamenev （軟體工程師，Microsoft Research） 開發在 Microsoft。</span><span class="sxs-lookup"><span data-stu-id="203f2-377">hello Net# language for customizing hello architecture of neural networks was developed at Microsoft by Shon Katzenberger (Architect, Machine Learning) and Alexey Kamenev (Software Engineer, Microsoft Research).</span></span> <span data-ttu-id="203f2-378">它供內部進行機器學習服務專案和應用程式，從映像偵測 tootext 分析。</span><span class="sxs-lookup"><span data-stu-id="203f2-378">It is used internally for machine learning projects and applications ranging from image detection tootext analytics.</span></span> <span data-ttu-id="203f2-379">如需詳細資訊，請參閱[在 Azure ML-簡介 tooNet # 類神經網路](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)</span><span class="sxs-lookup"><span data-stu-id="203f2-379">For more information, see [Neural Nets in Azure ML - Introduction tooNet#](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)</span></span>

[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif

