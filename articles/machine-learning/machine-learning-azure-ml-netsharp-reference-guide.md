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
# <a name="guide-toonet-neural-network-specification-language-for-azure-machine-learning"></a>Azure 機器學習引導 tooNet # 類神經網路規格語言
## <a name="overview"></a>概觀
Net # 是使用的 toodefine 類神經網路架構，Microsoft 開發的語言。 您可以在 Microsoft Azure Machine Learning 的類神經網路模組中使用 Net#。

<!-- This function doesn't currentlyappear in hello MicrosoftML documentation. If it is added in a future update, we can uncomment this text.

, or in hello `rxNeuralNetwork()` function in [MicrosoftML](https://msdn.microsoft.com/microsoft-r/microsoftml/microsoftml). 

-->

在本文中，您將了解基本概念所需 toodevelop 自訂類神經網路： 

* 類神經網路需求及如何 toodefine hello 主要元件
* hello 語法和 hello Net # 規格語言關鍵字
* 使用 Net# 建立的自訂類神經網路範例 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="neural-network-basics"></a>類神經網路基本概念
類神經網路結構組成***節點***，都依照***層***，和加權***連線***(或***邊緣***) 之間hello 節點。 hello 連線是方向性，且每個連接***來源***節點和***目的地***節點。  

每個***可訓練的層*** (隱藏或輸出層) 都有一或多個***連線套組***。 連接配套包含來源層級和 hello 來自該來源層級的規格。 中的給定的組合共用的所有都 hello 連接都 hello 相同***來源層級***和都 hello 相同***目的地層***。 在 Net # 中，連接組合都會被視為隸屬 toohello 組合的目的地階層。  

Net # 支援各種連線組合，可讓您自訂的輸入是對應的 toohidden 圖層的 hello 方式和對應的 toohello 輸出。   

hello 預設或標準的組合是**完整配套**，hello 中的每個節點中來源階層是 hello 目的地階層中的連接的 tooevery 節點。  

此外，Net # 支援下列四種進階的連線組合 hello:  

* **篩選套組**。 hello 使用者可以使用 hello hello 來源圖層的節點和 hello 目的地層節點的位置，以定義述詞。 每當 hello 述詞為 True 時，都會連線節點。
* **迴旋套組**。 hello 使用者可以定義節點的小型公寓 hello 來源層級中。 Hello 目的地階層中的每個節點是連接的 tooone hello 來源層的節點上的芳鄰。
* **集區套組**和**回應正規化套組**。 這些是類似 tooconvolutional 組合中的 hello 使用者會定義小公寓 hello 來源層的節點。 hello 差異是，這些組合中的 hello 邊緣 hello 加權並未 trainable。 相反地，套用預先定義的函式 toohello 來源節點值 toodetermine hello 目的地節點值。  

使用 Net # 類神經網路 toodefine hello 結構可讓可能 toodefine 複雜的結構，例如深度類神經網路或迴旋任意的維度，稱為 tooimprove 瞭解資料，例如影像、 音訊或視訊。  

## <a name="supported-customizations"></a>支援的自訂
您在 Azure Machine Learning 中建立的類神經網路模型的 hello 架構可以使用 Net # 廣泛地自訂。 您可以：  

* 隱藏的層節點的控制項 hello 數目在中建立和每個圖層。
* 指定圖層的 toobe 連接 tooeach 其他的方式。
* 定義特殊連線結構，例如迴旋和加權共用套組。
* 指定不同的啟用函數。  

如需 hello 規格語言語法的詳細資訊，請參閱[結構規格](#Structure-specifications)。  

如需定義為某些常見的機器學習服務工作，從 simplex toocomplex，類神經網路的範例，請參閱[範例](#Examples-of-Net#-usage)。  

## <a name="general-requirements"></a>一般需求
* 必須只能有一個輸出層，和至少一個輸入層，以及零或多個隱藏層。 
* 每一層都有固定的節點數目，在概念上會以任意維度的矩形陣列編排。 
* 輸入的層沒有相關聯的定型參數，而且代表 hello 點位置執行個體資料會進入 hello 網路。 
* Trainable (hello 隱藏和輸出層) 的圖層有關聯的定型的參數，稱為加權和徵才偏差。 
* hello 來源和目的地節點必須在個別的圖層。 
* 連接必須為非循環。也就是說，不能有前置反 toohello 初始來源節點連接的鏈結。
* hello 輸出層不能連接組合的來源層級。  

## <a name="structure-specifications"></a>結構規格
類神經網路結構規格由三個區段組成： hello**常數宣告**，hello**層級宣告**，hello**連線宣告**。 另外還有一個選擇性的**共用宣告**區段。 hello 區段可以任何順序指定。  

## <a name="constant-declaration"></a>常數宣告
常數宣告是選擇性宣告。 它會提供表示 toodefine hello 類神經網路定義中的其他位置所使用的值。 hello 宣告陳述式所組成的識別碼後面接著等號和值運算式。   

例如，陳述式之後的 hello 定義常數**x**:  

    Const X = 28;  

toodefine 兩個或多個常數，同時，hello 識別項名稱和值大括弧括住，並使用分號分隔。 例如：  

    Const { X = 28; Y = 4; }  

hello 右手邊的每個指派運算式可以是整數、 實數、 布林值 （True 或 False） 或數學運算式。 例如：  

    Const { X = 17 * 2; Y = true; }  

## <a name="layer-declaration"></a>層宣告
需要 hello 層宣告。 它會定義 hello 大小及來源的 hello 圖層，包括其連線組合和屬性。 hello hello hello 層 （輸入、 隱藏的或輸出） 名稱的宣告陳述式開頭，後面接著 hello 維度的 hello 層 (tuple 的正整數)。 例如：  

    input Data auto;
    hidden Hidden[5,20] from Data all;
    output Result[2] from Hidden all;  

* hello 產品的 hello 維度是 hello hello 層的節點數目。 在此範例中，有兩個維度 [5,20]，這表示在 hello 層有 100 個節點。
* hello 圖層可以宣告任何順序，但有一個例外： 如果已定義多個輸入的層，在宣告的 hello 順序必須符合 hello 順序 hello 輸入資料中的功能。  

toospecify hello 層的節點數目是自動，決定使用 hello**自動**關鍵字。 hello**自動**關鍵字有不同的效果，視 hello 層而定：  

* 在輸入的層宣告中，節點的 hello 數目是 hello hello 輸入資料中的功能數目。
* 在隱藏的層的宣告中，節點的 hello 數目是 hello hello 參數值所指定的數字**隱藏節點的數目**。 
* 在輸出層宣告中，hello 節點數目是 2 的二級分類，1 代表迴歸，並等於 toohello 多級分類的輸出節點的數目。   

例如，hello 下列網路定義允許 hello 大小的所有圖層 toobe 自動決定：  

    input Data auto;
    hidden Hidden auto from Data all;
    output Result auto from Hidden all;  


Trainable 圖層的層級宣告 (hello 隱藏或輸出層級) 可以選擇性地包含 hello 輸出函式 （也稱為啟用函式），其預設太**sigmoid**分類模型和**線性**迴歸模型。 （即使您使用 hello 預設，您可以明確陳述 hello 啟用函式，如果為了避免混淆。）

hello 輸出支援下列函數：  

* sigmoid
* linear
* softmax
* rlinear
* square
* sqrt
* srlinear
* abs
* tanh 
* brlinear  

例如，hello 宣告之後使用 hello **softmax**函式：  

    output Result [100] softmax from Hidden all;  

## <a name="connection-declaration"></a>連線宣告
之後立即定義 hello trainable 圖層，您必須宣告在您已定義的 hello 圖層間的連線。 hello 連接配套宣告的開頭 hello 關鍵字**從**，後面接著 hello 種類的名稱 hello 配套來源圖層與 hello 連接配套 toocreate。   

目前支援五種連線套組：  

* **完整**組合，以 hello 關鍵字**所有**
* **篩選**組合，以 hello 關鍵字**其中**，後面接著述詞的運算式
* **Convolutional**組合，以 hello 關鍵字**convolve**，後面接著 hello convolution 屬性
* **共用**組合，以 hello 關鍵字**最大集區**或**表示集區**
* **回應正規化**組合，以 hello 關鍵字**回應範數**      

## <a name="full-bundles"></a>完整套組
完整連接配套 hello 來源層 tooeach 節點 hello 目的地階層中包含來自每個節點的連接。 這是 hello 預設網路連線類型。  

## <a name="filtered-bundles"></a>篩選套組
篩選連線套組規格包含一個述詞，此述詞在語法上的表示方式非常類似 C# lambda 運算式。 hello 下列範例定義兩個篩選的組合：  

    input Pixels [10, 20];
    hidden ByRow[10, 12] from Pixels where (s,d) => s[0] == d[0];
    hidden ByCol[5, 20] from Pixels where (s,d) => abs(s[1] - d[1]) <= 1;  

* Hello 的述詞中*ByRow*， **s**是以參數為 hello 矩形陣列 hello 輸入圖層的節點代表索引*像素為單位*，和**d**是參數表示成 hello hello 隱藏圖層之節點的陣列索引*ByRow*。 hello 這兩種**s**和**d**是長度為兩個整數的 tuple。 在概念上，**s** 的範圍介於所有 *0 <= s[0] < 10* 與 *0 <= s[1] < 20* 的整數對之間，而且 **d** 的範圍介於所有 *0 <= d[0] < 10* 與 *0 <= d[1] < 12* 的整數對之間。 
* Hello hello 述詞運算式的右側，在沒有條件。 在此範例中，每個值**s**和**d**使得 hello 條件為 True 時，會從 hello 來源圖層節點 toohello 目的圖層節點的邊緣。 因此，這個篩選條件運算式，表示該 hello 配套所包含的連接所定義的 hello 節點**s** toohello 節點所定義**d**在所有情況下，其中 s [0] 是等於 tood [0]。  

您可以選擇性地為篩選套組指定一組加權。 hello 值 hello**加權**屬性必須是 tuple 的浮點值的長度符合 hello hello 組合所定義的連接數目。 依預設會隨機產生加權。  

加權值被分組 hello 目的節點的索引。 亦即，如果第一個目的地節點 hello 連接花費了來源節點，第一次 hello *K* hello 的項目**加權**tuple 會 hello 第一個目的地節點，在來源索引順序中的 hello 加權。 這同樣適用於 hello 其餘目的地節點的 hello。  

很可能 toospecify 加權做為常數值。 例如，如果您先前所學 hello 加權，您可以指定它們為使用此語法的常數：

    const Weights_1 = [0.0188045055, 0.130500451, ...]


## <a name="convolutional-bundles"></a>迴旋套組
Hello 定型資料具有同質性結構時，convolutional 連線是常用的 toolearn hello 資料的高層級的功能。 例如，在影像、音訊或視訊資料中，空間或暫時維度可能會相當一致。  

Convolutional 組合運用矩形**核心**，slid hello 維度。 基本上，每個核心定義一組的本機公寓，參照 tooas 中套用的權數**核心應用程式**。 每個核心應用程式對應 hello 來源層級，也就是參考的 tooas hello tooa 節點**中央節點**。 核心 hello 加權會共用連線數目。 在 convolutional 的組合，每個核心是矩形，而所有的核心應用程式都 hello 相同大小。  

Convolutional 組合支援 hello 下列屬性：

**InputShape**定義 hello 這個 convolutional 配套 hello 基於 hello 來源層級的維度性。 hello 值必須是正整數的 tuple。 hello 產品的 hello 整數必須等於 hello hello 來源圖層中的節點數目，但反之則不需要為 hello 來源層級宣告的 toomatch hello 維度性。 這個 tuple 的 hello 長度會變成 hello **arity** hello convolutional 組合的值。 （通常 arity 參照 toohello 數目之引數或函式可以接受的運算元）。  

toodefine hello 圖形和位置 hello 核心使用 hello 屬性**KernelShape**， **Stride**，**填補**， **LowerPad**，和**UpperPad**:   

* **KernelShape**: hello convolutional 組合的每個核心的 （必要） 定義 hello 維度性。 hello 值必須是正整數長度等於 hello arity hello 組合的 tuple。 這個 tuple 的每個元件必須等於或小於 hello 對應元件的**InputShape**。 
* **Stride**: （選擇性） 定義 hello 滑動 hello hello 中央節點之間的距離 hello convolution （每個維度的一個步驟大小） 的步驟大小。 hello 值必須是正整數 hello 組合的 hello arity 長度的 tuple。 這個 tuple 的每個元件必須等於或小於 hello 對應元件的**KernelShape**。 hello 預設值是與所有元件等於 tooone tuple。 
* **共用**: （選擇性） 的定義 hello 權數分享 hello convolution 的每個維度。 hello 值可以是單一的布林值或長度是 hello arity hello 組合的布林值的 tuple。 單一布林值是擴充的 toobe hello 與所有元件的正確長度的 tuple toohello 等於指定的值。 hello 預設值是 tuple 所組成，則為 True 的所有值。 
* **MapCount**: hello convolutional 組合對應 （選擇性） 定義 hello 數項功能。 hello 值可以是單一的正整數或 tuple 的長度是 hello arity hello 組合的正整數。 一個整數值擴充 toobe hello 與 hello 第一個元件等於 toohello 的正確長度的 tuple 指定值與所有 hello 其餘元件等於 tooone。 hello 預設值為 1。 hello 總數的對應功能是 hello 產品的 hello tuple 的 hello 元件。 此總數的分解 hello 元件之間的 hello 決定 hello 功能對應值 hello 目的地節點中分組的方式。 
* **加權**: （選擇性） 定義 hello 初始的加權 hello 組合。 hello 值必須是 tuple 的浮點值是核心時間的每個核心，加權 hello 數目的 hello 數目，如本文稍後所定義的長度。 隨機產生的 hello 預設權數。  

有兩個集合的控制與邊框距離 hello 屬性正在互斥的屬性：

* **填補**: （選擇性） 決定應該湊足 hello 的輸入是否使用**預設填補配置**。 hello 值可以是單一的布林值，或長度是 hello arity hello 組合的布林值的 tuple。 單一布林值是擴充的 toobe hello 與所有元件的正確長度的 tuple toohello 等於指定的值。 如果維度 hello 值為 True，hello 來源邏輯填補與零值資料格 toosupport 額外的核心應用程式，該維度中的 hello 的 hello 該維度中的第一個和最後一個核心的中央節點 hello 第一個和最後一個節點hello 來源層級中的維度。 因此，每個維度中的"dummy"節點的 hello 數目不會自動決定，toofit 完全*(InputShape [d]-1) / Stride [d] + 1*到 hello 填補來源層級的核心。 如果維度 hello 值為 False，hello 核心定義，因此 hello 中省略了每一端上的節點數目是 hello 相同 （向上 tooa 差異為 1）。 hello 這個屬性的預設值是與所有元件等於 tooFalse tuple。
* **UpperPad**和**LowerPad**: （選擇性） 提供較大的控制權 hello 填補 toouse 數量。 **重要事項：**可以定義這些屬性，並且在 hello**填補**上述的屬性是***不***定義。 hello 值應該是整數值 tuple 的 hello arity hello 組合的長度。 當指定這些屬性時，"dummy"節點可加入 toohello 較低，與 hello 的每個維度的上限結束輸入層。 hello 的節點數目加入 toohello 較低而且在每個維度中的上方結束由**LowerPad**[i] 和**UpperPad**[i] 分別。 必須符合 tooensure 的核心對應至僅太 「 實際的 「 節點與不太"dummy"的節點，hello 下列條件：
  * **LowerPad** 的每個元件皆務必小於 KernelShape[d]/2。 
  * **UpperPad** 的每個元件皆不可大於 KernelShape[d]/2。 
  * 這些屬性的 hello 預設值是與所有元件等於 too0 tuple。 

hello 設定**填補**= true 可讓多填補現狀視 tookeep hello"center"hello 核心的"real"輸入 hello 內。 這樣會變更 hello 數學運算 hello 輸出大小的位元。 一般而言，hello 輸出大小*D*計算方式為*D = (I-K) / S + 1*，其中*我*hello 輸入大小， *K* hello 核心大小， *S*是 hello 分散和 */* 是整數除法 （圓趨近於零）。 如果您設定 UpperPad = [1，1] hello 輸入大小*我*實際上是 29，因此*D = (29-5) / 2 + 1 = 13*。 不過，當 **Padding** = true 時，基本上 *I* 會藉由 *K - 1* 而提高；因此 *D = ((28 + 4) - 5) / 2 + 1 = 27 / 2 + 1 = 13 + 1 = 14*。 藉由指定的值**UpperPad**和**LowerPad**取得更多控制權填補比您剛才設定的 hello**填補**= true。

如需迴旋網路及其應用程式的詳細資訊，請參閱下列文章：  

* [http://deeplearning.net/tutorial/lenet.html ](http://deeplearning.net/tutorial/lenet.html)
* [http://research.microsoft.com/pubs/68920/icdar03.pdf](http://research.microsoft.com/pubs/68920/icdar03.pdf) 
* [http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf](http://people.csail.mit.edu/jvb/papers/cnn_tutorial.pdf)  

## <a name="pooling-bundles"></a>集區套組
A**共用配套**適用於幾何類似 tooconvolutional 連線，但是它會使用預先定義的函式 toosource 節點值 tooderive hello 目的地節點值。 因此，集區套組並沒有可訓練的狀態 (加權或偏差)。 共用組合支援所有 hello convolutional 屬性除了**共用**， **MapCount**，和**加權**。  

一般而言，相鄰的集區單元的摘要 hello 核心不會重疊。 如果每個維度中的相等 tooKernelShape [d] [d] 的分散，取得 hello 層是 hello 傳統本機共用層，其通常會採用 convolutional 類神經網路。 每個目的地節點計算最大的 hello 或 hello 活動，其核心 hello 來源層級中的 hello 平均值。  

hello 下列範例將說明共用的組合： 

    hidden P1 [5, 12, 12]
      from C1 max pool {
        InputShape  = [ 5, 24, 24];
        KernelShape = [ 1,  2,  2];
        Stride      = [ 1,  2,  2];
      }  

* hello 組合的 hello arity 為 3 (hello 長度的 hello tuple **InputShape**， **KernelShape**，和**Stride**)。 
* hello hello 來源層的節點數目是*5 * 24 * 24 = 2880*。 
* 這是傳統本端集區層，因為 **KernelShape** 和 **Stride** 是相等的。 
* hello hello 目的地層的節點數目是*5 * 12 * 12 = 1440*。  

如需集區層的詳細資訊，請參閱下列文章：  

* [http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf) (3.4 小節)
* [http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf](http://cs.nyu.edu/~koray/publis/lecun-iscas-10.pdf) 
* [http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf](http://cs.nyu.edu/~koray/publis/jarrett-iccv-09.pdf)

## <a name="response-normalization-bundles"></a>回應正規化套組
**回應正規化**是首次推出的 Geoffrey Hinton 本機正規化配置 box hello 份文件中[深層 Convolutional 的類神經網路與 ImageNet Classiﬁcation](http://www.cs.toronto.edu/~hinton/absps/imagenet.pdf)。 回應 「 正規化 」 是在類神經網路使用的 tooaid 一般化。 當另一個神經會引發在極高的啟用層級時，本機回應正規化圖層會隱藏周圍神經 hello hello 啟用層級。 此動作會使用三個參數 (***α***、***β*** 和 ***k***) 與迴旋結構 (或鄰區分布型態) 來完成。 Hello 目的地階層中的每一個神經***y***對應 tooa 神經***x*** hello 來源層級中。 hello 的啟用層級***y*** hello 下列公式，就會提供其中***f*** hello 啟用層級的神經，以及***Nx*** hello 核心 （或 hello 集，其中包含 hello中的 hello 鄰居神經***x***)，如下列 convolutional 結構 hello 所定義：  

![][1]  

回應正規化組合支援所有的 hello convolutional 屬性除了**共用**， **MapCount**，和**加權**。  

* 如果 hello 核心包含神經 hello 相同將對應為***x***，hello 正規化配置是參照的 tooas**相同對應正規化**。 toodefine 相同對應中的 hello 第一個座標的正規化**InputShape**必須 hello 值 1。
* 如果 hello 核心包含神經 hello 相同空間位置***x***，但 hello 神經位於其他對應，稱為 hello 正規化配置**透過對應正規化**。 這類回應正規化會實作一種橫向 inhibition hello 類型中實際的神經，找到建立大啟用層級，在計算的不同對應的神經輸出之間的競爭所啟發。 跨 toodefine 對應正規化、 hello 第一個座標必須是大於 1 且不大於對應的 hello 數目的整數和 hello 座標 hello 其餘部分都必須有 hello 值 1。  

回應正規化組合套用預先定義的函式 toosource 節點值 toodetermine hello 目的地節點值，因為它們會有任何 trainable 的狀態 （「 加權 」 或 「 徵才偏差 」）。   

**警示**: hello 目的地階層中的 hello 節點對應 tooneurons 屬於 hello 的 hello 核心的中央節點。 例如，如果 KernelShape [d] 是奇數，則*KernelShape [d] / 2*對應 toohello 中央核心節點。 如果*KernelShape [d]*是奇數，hello 中央節點位於*KernelShape [d] / [2-1*。 因此，如果**填補**[d] 為 False 時，第一次 hello 和上次 hello *KernelShape [d] / 2*節點 hello 目的圖層中沒有對應的節點。 tooavoid 這種情況下，定義**填補**做為 [為 true，true，...，true]。  

此外 toohello 四個屬性稍早所述，回應正規化組合也支援 hello 下列屬性：  

* **Alpha**: （必要） 指定浮點值，對應太***α*** hello 先前公式中。 
* **Beta**: （必要） 指定浮點值，對應太***β*** hello 先前公式中。 
* **位移**: （選擇性） 指定浮點值，對應太***k*** hello 先前公式中。 預設 too1。  

hello 下列範例會定義使用這些屬性的回應正規化組合：  

    hidden RN1 [5, 10, 10]
      from P1 response norm {
        InputShape  = [ 5, 12, 12];
        KernelShape = [ 1,  3,  3];
        Alpha = 0.001;
        Beta = 0.75;
      }  

* hello 來源圖層都包含五個對應，各有很少維度為 12 x 12，加總 1440年節點中。 
* hello 值**KernelShape**指出這是相同的對應正規化層，其中 hello 上的芳鄰 是 3x3 矩形。 
* hello 預設值是**填補**為 False，因此 hello 目的圖層的每個維度中的 10 個節點。 tooinclude 對應 tooevery 節點在 hello 來源層中，加入填補的 hello 目的地層中的一個節點 = [為 true，true，true]。和太變更 RN1 hello 大小 [5、 12、 12]。  

## <a name="share-declaration"></a>共用宣告
Net# 可選擇性地支援以共用加權定義多個套組的作業。 如果其結構是 hello 相同，您可以共用任何兩個組合的 hello 加權。 hello，請使用下列語法會定義使用共用的加權的組合：  

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

例如，hello 下列共用宣告指定 hello 圖層名稱，表示應該共用加權和徵才偏差：  

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

* hello 的輸入的特徵會分割成兩個相等大小輸入層。 
* hello 隱藏圖層計算 hello 兩個輸入的圖層上更高的層級功能。 
* hello 共用宣告指定*H1*和*H2*必須計算 hello 中相同的方式，從其個別的輸入。  

或者，這也可以用兩個不同的共用宣告來指定，如下所示：  

    share { Data1 => H1, Data2 => H2 } // share weights  

<!-- -->

    share { 1 => H1, 1 => H2 } // share biases  

您可以在 hello 圖層包含單一配套時，才使用 hello 簡短形式。 一般情況下，共用時，可能只 hello 相關的結構完全相同，這表示它們有相同的大小相同 convolutional geometry、 和等的 hello。  

## <a name="examples-of-net-usage"></a>Net# 的使用範例
本節提供一些範例，告訴您可以使用 Net # tooadd 隱藏圖層上，定義 hello 方式隱藏的層互動的其他圖層，並建置 convolutional 網路。   

### <a name="define-a-simple-custom-neural-network-hello-world-example"></a>定義簡易的自訂類神經網路："Hello World" 範例
這個簡單的範例示範如何 toocreate 的類神經網路模型有單一隱藏的層。  

    input Data auto;
    hidden H [200] from Data all;
    output Out [10] sigmoid from H all;  

hello 範例將說明一些基本命令，如下所示：  

* hello 第一行定義 hello 輸入的層 (名為*資料*)。 當您使用 hello**自動**關鍵字，hello 類神經網路會自動在 hello 輸入範例中包含所有特徵資料行。 
* hello 第二行建立 hello 隱藏圖層。 hello 名稱*H*指派 toohello 隱藏的層，其具有 200 的節點。 此圖層是完全連接的 toohello 輸入的層。
* hello 第三行定義 hello 輸出層 (名為*O*)，其中包含 10 個輸出節點。 如果 hello 類神經網路會用於分類，則每個類別的一個輸出節點。 hello 關鍵字**sigmoid**表示 hello 輸出函式是套用的 toohello 輸出層。   

### <a name="define-multiple-hidden-layers-computer-vision-example"></a>定義多個隱藏層：電腦願景範例
hello 下列範例會示範如何 toodefine 稍微更為複雜的類神經網路，具有多個自訂的隱藏層。  

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

這個範例將說明 hello 類神經網路規格語言的數個功能：  

* hello 結構有兩個輸入的圖層，*像素為單位*和*中繼資料*。
* hello*像素為單位*層是兩個連線組合，來源層級與目的地層*ByRow*和*ByCol*。
* hello 層*收集*和*結果*目的地層中多個連接的組合。
* hello 輸出層中，*結果*，目的地階層中兩個連線組合，則為其中一個 hello 與第二層做為目的圖層的 隱藏 （收集） 和其他 hello 輸入層 （中繼資料） 與 hello 做為目的地階層。
* hello 隱藏的層， *ByRow*和*ByCol*，已篩選的連線使用指定的述詞運算式。 更明確地說，在 hello 節點*ByRow*在 [x，y] 是在連接的 toohello 節點*像素為單位*具有 hello 第一個索引座標等於 toohello 節點的第一個座標，x。 同樣地，在 hello 節點*ByCol 在 [x，y] 是在 _Pixels 連接的 toohello 節點*hello 第二個索引座標的 hello 節點的第二個座標，其中一個內有 y。  

### <a name="define-a-convolutional-network-for-multiclass-classification-digit-recognition-example"></a>定義多類別分類的迴旋網路：數字辨識範例
hello hello 遵循網路定義是設計的 toorecognize 數字，它會說明一些進階的技術，用於自訂類神經網路。  

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


* hello 結構具有單一輸入的層中，*映像*。
* hello 關鍵字**convolve**指出 hello 圖層命名*Conv1*和*Conv2* convolutional 層。 每個這些圖層的宣告後面的 hello convolution 屬性清單。
* hello net 有第三個隱藏層， *Hid3*，也就是完全連接 toohello 第二個隱藏的層， *Conv2*。
* hello 輸出層中，*位數*，是連接的唯一 toohello 第三個隱藏的層， *Hid3*。 hello 關鍵字**所有**指出該 hello 輸出層完全連接太*Hid3*。
* hello 的 hello convolution arity 是三 (hello 長度的 hello tuple **InputShape**， **KernelShape**， **Stride**，和**共用**)。 
* 每個核心的加權的 hello 數目是*1 + **KernelShape**\[0] * **KernelShape**\[1] * **KernelShape** \[2] = 1 + 1 * 5 * 5 = 26。或是 26 * 50 = 1300*。
* 您可以計算每個隱藏層中的 hello 節點，如下所示：
  * **NodeCount**\[0] = (5 - 1) / 1 + 1 = 5.
  * **NodeCount**\[1] = (13 - 5) / 2 + 1 = 5。 
  * **NodeCount**\[2] = (13 - 5) / 2 + 1 = 5。 
* hello 的節點總數計算方式是使用宣告的 hello 維度 hello 圖層，[50，5，5]，如下所示：  ***MapCount** * **NodeCount** \[0] * **NodeCount**\[1] * **NodeCount**\[2] = 10 * 5 * 5 * 5*
* 因為**共用**[d] 設為 False 僅適用於*d = = 0*，hello 核心的數目是 ***MapCount** * **NodeCount** \[0] = 10 * 5 = 50*。 

## <a name="acknowledgements"></a>通知
hello Net # 自訂類神經網路的 hello 架構的語言是由 Shon Katzenberger （架構設計人員、 機器學習） 和 Alexey Kamenev （軟體工程師，Microsoft Research） 開發在 Microsoft。 它供內部進行機器學習服務專案和應用程式，從映像偵測 tootext 分析。 如需詳細資訊，請參閱[在 Azure ML-簡介 tooNet # 類神經網路](http://blogs.technet.com/b/machinelearning/archive/2015/02/16/neural-nets-in-azure-ml-introduction-to-net.aspx)

[1]:./media/machine-learning-azure-ml-netsharp-reference-guide/formula_large.gif

