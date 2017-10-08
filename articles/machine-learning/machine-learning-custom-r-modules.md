---
title: "Azure Machine Learning 中的自訂 R 模組 aaaAuthor |Microsoft 文件"
description: "在 Azure Machine Learning 中撰寫自訂 R 模組的快速入門。"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 6cbc628a-7e60-42ce-9f90-20aaea7ba630
ms.service: machine-learning
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 03/24/2017
ms.author: bradsev;ankarlof
ms.openlocfilehash: 8007c2abe20a4ab990f38b6d09bc4e6834ad2082
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="author-custom-r-modules-in-azure-machine-learning"></a>在 Azure Machine Learning 中撰寫自訂 R 模組
本主題描述如何 tooauthor 和部署 Azure Machine Learning 中的自訂 R 模組。 它會說明自訂 R 模組為何，以及哪些檔案是使用的 toodefine 它們。 它會說明如何 tooconstruct hello 定義模組的檔案和 tooregister hello Machine Learning 工作區中的部署模組的方式。 hello 項目和屬性中的 hello 自訂模組的 hello 定義使用然後詳述於更多詳細資料。 如何也討論 toouse 輔助功能以及檔案和多個輸出。 

[!INCLUDE [machine-learning-free-trial](../../includes/machine-learning-free-trial.md)]

## <a name="what-is-a-custom-r-module"></a>什麼是自訂 R 模組？
A**自訂模組**是使用者定義的模組可以上傳 tooyour 工作區及 Azure 機器學習實驗的一部分執行。 **自訂 R 模組** 是執行使用者定義之 R 函數的自訂模組。 **R** 是一種適用於統計運算和圖形的程式設計語言，由實作演算法的統計學家和資料科學家廣泛使用。 目前，R 是 hello 唯一自訂模組，但支援其他語言排程在未來的版本支援的語言。

自訂模組有**第一級狀態**hello 意義而言，它們可以用於就像任何其他模組的 Azure Machine Learning 中。 它們可以與已發行實驗或視覺效果中包含的其他模組一起執行。 您充分掌控 hello 模組所實作的 hello 演算法、 hello 使用輸入和輸出連接埠 toobe、 hello 模型參數和其他各種執行階段行為。 包含自訂模組的實驗也可以發行成 hello Cortana 智慧組件庫以方便共用。

## <a name="files-in-a-custom-r-module"></a>自訂 R 模組中的檔案
自訂 R 模組是由至少包含兩個檔案的 .zip 檔案所定義：

* A**原始程式檔**實作 hello 模組所公開的 hello R 函式
* **XML 定義檔**描述 hello 自訂模組介面

其他的輔助檔案也可以包含在 hello.zip 檔案，提供可以從 hello 自訂模組存取的功能。 此選項會討論 hello**引數**屬於 hello 參考章節**hello XML 定義檔中的項目**下列 hello 快速入門範例。

## <a name="quickstart-example-define-package-and-register-a-custom-r-module"></a>快速入門範例：定義、封裝及註冊自訂 R 模組
此範例說明如何 tooconstruct hello 自訂 R 模組所需的檔案，將它們封裝成 zip 檔案，然後在您的機器學習服務工作區中的暫存器 hello 模組。 hello 範例 zip 封裝檔及範例檔可以從下載[下載 CustomAddRows.zip 檔案](http://go.microsoft.com/fwlink/?LinkID=524916&clcid=0x409)。

## <a name="hello-source-file"></a>hello 原始程式檔
Hello 的範例，請考慮**自訂加入資料列**修改 hello hello 標準實作的模組**加入資料列**使用 tooconcatenate 資料列 （觀察） 從兩個資料集 （資料框架） 的模組。 hello 標準**加入資料列**模組附加 hello 資料列的 hello 第二個輸入資料集 toohello hello 第一個輸入資料集的結尾使用 hello`rbind`演算法。 自訂的 hello`CustomAddRows`函式類似接受兩個資料集，但也接受布林交換做為其他的輸入參數。 如果設定太 hello 交換參數**FALSE**，它傳回 hello 相同的資料集，因為 hello 標準的實作。 但是，如果 hello 交換參數是**TRUE**，hello 函式將改為附加資料列的第一個輸入資料集 toohello 結尾 hello 第二個資料集。 hello CustomAddRows.R 檔案，其中包含實作 hello R hello `CustomAddRows` hello 所公開的函數**自訂加入資料列**模組有 hello 下列 R 程式碼。

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) 
    {
        if (swap)
        {
            return (rbind(dataset2, dataset1));
        }
        else
        {
            return (rbind(dataset1, dataset2));
        } 
    } 

### <a name="hello-xml-definition-file"></a>hello XML 定義檔
tooexpose 這`CustomAddRows`函式，為 Azure 機器學習模組時，XML 定義檔必須建立 toospecify 如何 hello**自訂加入資料列**模組應該外觀和行為。 

    <!-- Defined a module using an R Script -->
    <Module name="Custom Add Rows">
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother. Dataset 2 is concatenated tooDataset 1 when Swap is FALSE, and vice versa when Swap is TRUE.</Description>

    <!-- Specify hello base language, script file and R function toouse for this module. -->        
        <Language name="R" 
         sourceFile="CustomAddRows.R" 
         entryPoint="CustomAddRows" />  

    <!-- Define module input and output ports -->
    <!-- Note: hello values of hello id attributes in hello Input and Arg elements must match hello parameter names in hello R Function CustomAddRows defined in CustomAddRows.R. -->
        <Ports>
            <Input id="dataset1" name="Dataset 1" type="DataTable">
                <Description>First input dataset</Description>
            </Input>
            <Input id="dataset2" name="Dataset 2" type="DataTable">
                <Description>Second input dataset</Description>
            </Input>
            <Output id="dataset" name="Dataset" type="DataTable">
                <Description>hello combined dataset</Description>
            </Output>
        </Ports>

    <!-- Define module parameters -->
        <Arguments>
            <Arg id="swap" name="Swap" type="bool" >
                <Description>Swap input datasets.</Description>
            </Arg>
        </Arguments>
    </Module>


它是 hello hello 值的關鍵 toonote**識別碼**hello 屬性**輸入**和**Arg** hello XML 檔案中的項目必須符合 hello R hello 函式參數名稱中的程式碼 hello CustomAddRows.R 檔案完全: (*dataset1*， *dataset2*，和*交換*hello 範例中)。 同樣地，hello 值 hello **entryPoint**屬性 hello**語言**項目必須完全符合 hello hello R 指令碼中的 hello 函式名稱: (*CustomAddRows*在 hello 範例）。 

相反地，hello**識別碼**屬性 hello**輸出**項目沒有對應 tooany hello R 指令碼中的變數。 需要一個以上的輸出時，只傳回清單從 hello R 函式的結果放*hello 中相同的順序*為**輸出**hello XML 檔案中宣告項目。

### <a name="package-and-register-hello-module"></a>封裝和註冊 hello 模組
儲存為這兩個檔案*CustomAddRows.R*和*CustomAddRows.xml* ，然後 zip hello 兩個檔案一起到*CustomAddRows.zip*檔案。

在您機器學習服務工作區中，移 tooyour 工作區中 hello Machine Learning Studio 中，按一下 hello tooregister **+ 新增**hello 下方的按鈕，然後選擇**模組]-> [從 ZIP 封裝**tooupload新的 hello**自訂加入資料列**模組。

![上傳 Zip 檔案](./media/machine-learning-custom-r-modules/upload-from-zip-package.png)

hello**自訂加入資料列**模組現在是透過機器學習實驗的準備 toobe。

## <a name="elements-in-hello-xml-definition-file"></a>Hello XML 定義檔中的項目
### <a name="module-elements"></a>Module 元素
hello**模組**項目，則使用的 toodefine hello XML 檔案中的自訂模組。 您可以在一個 XML 檔案中，使用多個 **Module** 元素來定義多個模組。 工作區中的每個模組都必須有唯一的名稱。 以相同的名稱，為現有的自訂模組的 hello 註冊自訂的模組，並取代 hello 新 hello 現有的模組。 自訂模組，不過，可以使用相同的名稱，為現有的 Azure 機器學習模組的 hello 註冊。 因此，出現在 hello**自訂**hello 模組調色盤的分類。

    <Module name="Custom Add Rows" isDeterministic="false"> 
        <Owner>Microsoft Corporation</Owner>
        <Description>Appends one dataset tooanother...</Description>/> 


在 hello**模組**項目，您可以指定兩個額外的選擇性項目：

* **擁有者**hello 模組將內嵌的項目  
* **描述**包含的文字，會顯示在 hello 模組的快速說明，當您將滑鼠停留在 hello 機器學習 UI 中的 hello 模組項目。

Hello 模組項目中的字元限制的規則：

* hello 值 hello**名稱**中 hello 屬性**模組**項目不能超過 64 個字元的長度。 
* hello 的 hello 內容**描述**項目不能超過 128 個字元的長度。
* hello 的 hello 內容**擁有者**項目不能超過 32 個字元的長度。

模組的結果可以是具決定性或 nondeterministic.* * 依預設，所有模組都視為 toobe 具決定性。 也就是假設不可變的輸入的參數和資料集，hello 模組應該傳回的 hello eacRAND 或 functionh 執行時相同的結果。 指定此行為，Azure Machine Learning Studio 只重新執行標示為具決定性，如果參數的模組，或 hello 輸入的資料已變更。 傳回快取的 hello 結果也會提供實驗多更快地執行。

有不具決定性的例如 RAND 或傳回目前的日期或時間的 hello 函式的函式。 如果您的模組會使用不具決定性的函式，您可以指定該 hello 模組是不具決定性的選擇性設定 hello **isDeterministic**屬性太**FALSE**。 這樣可確保該 hello 模組將會重新執行每次執行 hello 實驗時，即使 hello 模組輸入參數中未變更和複本。 

### <a name="language-definition"></a>語言定義
hello**語言**XML 定義檔中的項目是使用的 toospecify hello 自訂模組語言。 目前，R 是 hello 只支援的語言。 hello 值 hello **sourceFile**屬性必須是 hello hello 模組執行時所在 hello 函式 toocall hello R 檔案名稱。 這個檔案必須是 hello zip 封裝的一部分。 hello 值 hello **entryPoint**屬性是 hello 所呼叫的 hello 函式名稱，且必須符合有效 hello 原始程式檔中定義的函數。

    <Language name="R" sourceFile="CustomAddRows.R" entryPoint="CustomAddRows" />


### <a name="ports"></a>連接埠
hello 自訂模組的輸入和輸出連接埠中指定子項目的 hello**連接埠**hello XML 定義檔的區段。 這些項目 hello 順序決定 hello 配置經驗 (UX) 的使用者。 hello 第一個子系**輸入**或**輸出**列在 hello**連接埠**hello XML 檔案的項目會成為 hello 最左邊的輸入連接埠在 hello 機器學習經驗
每一個輸入和輸出連接埠可能會有一個選擇性**描述**子元素，指定顯示當您 hello 滑鼠游標 hello hello 機器學習 UI 中的連接埠的 hello 文字。

**連接埠規則**：

* **輸入和輸出連接埠** 數目上限各為 8 個。

### <a name="input-elements"></a>Input 元素
輸入連接埠可讓您 toopass 資料 tooyour R 函式和工作區。 hello**資料型別**支援的輸入連接埠，如下所示： 

**DataTable:**這個型別會當做 data.frame 傳遞 tooyour R 函式。 事實上，機器學習和所支援的任何類型 （例如，CSV 檔案或 ARFF 檔案） 是否相容**DataTable**會自動轉換的 tooa data.frame。 

        <Input id="dataset1" name="Input 1" type="DataTable" isOptional="false">
            <Description>Input Dataset 1</Description>
           </Input>

hello**識別碼**每個相關聯的屬性**DataTable**輸入連接埠必須具有唯一值，這個值必須符合其對應的命名您的 R 函數中的參數。
選擇性**DataTable**不會傳遞做為實驗中輸入的連接埠有 hello 值**NULL**傳遞的 toohello R 函式和選擇性 zip 連接埠會忽略如果 hello 輸入未連接。 hello **isOptional**屬性是選擇性的這兩個 hello **DataTable**和**Zip**類型，並為*false*預設。

**Zip：** 自訂模組可以接受 zip 檔案做為輸入。 此輸入會解壓縮到您的函式的 hello R 工作目錄

        <Input id="zippedData" name="Zip Input" type="Zip" IsOptional="false">
            <Description>Zip files toobe extracted toohello R working directory.</Description>
           </Input>

針對自訂 R 模組 Zip 連接埠的 hello 識別碼沒有 toomatch hello R 函式的任何參數。 這是因為 hello zip 檔案是自動解壓縮的 toohello R 工作目錄。

**輸入規則：**

* hello 值 hello**識別碼**屬性 hello**輸入**元素必須是有效的 R 變數名稱。
* hello 值 hello**識別碼**屬性 hello**輸入**項目不能超過 64 個字元。
* hello 值 hello**名稱**屬性 hello**輸入**項目不能超過 64 個字元。
* hello 的 hello 內容**描述**項目不能超過 128 個字元
* hello 值 hello**類型**屬性 hello**輸入**項目必須是*Zip*或*DataTable*。
* hello hello 值**isOptional** hello 屬性**輸入**項目不需要 (且*false*時未指定，預設情況); 但如果有指定，它必須是*true*或*false*。

### <a name="output-elements"></a>Output 元素
**標準輸出連接埠：**輸出連接埠會從您的 R 函數，然後由後續的模組的對應的 toohello 傳回值。 *DataTable*是 hello 目前支援的唯一標準的輸出連接埠類型。 (即將推出 *Learners* 和 *Transforms* 的支援。)*DataTable* 輸出的定義如下：

    <Output id="dataset" name="Dataset" type="DataTable">
        <Description>Combined dataset</Description>
    </Output>

若為自訂 R 模組中的輸出，hello hello 值**識別碼**屬性中並沒有與任何項目 toocorrespond hello R 指令碼，但它必須是唯一的。 Hello hello R 函式傳回值必須是單一模組的輸出， *data.frame*。 在排序 toooutput 支援的資料類型的多個物件、 hello 適當的輸出連接埠需要 toobe hello XML 定義檔中指定與 hello 物件需要 toobe 的清單傳回。 hello 輸出物件會從左 tooright，反映 hello 物件會置於傳回清單中的 hello hello 順序指派 toooutput 連接埠。

例如，如果您想要 toomodify hello**自訂加入資料列**模組 toooutput hello 原始的兩個資料集， *dataset1*和*dataset2*，此外 toohello 新聯結資料集，*資料集*，(順序，從左 tooright，做為：*資料集*， *dataset1*， *dataset2*)，然後定義 hello輸出 hello CustomAddRows.xml 檔案中的連接埠，如下所示：

    <Ports> 
        <Output id="dataset" name="Dataset Out" type="DataTable"> 
            <Description>New Dataset</Description> 
        </Output> 
        <Output id="dataset1_out" name="Dataset 1 Out" type="DataTable"> 
            <Description>First Dataset</Description> 
        </Output> 
        <Output id="dataset2_out" name="Dataset 2 Out" type="DataTable"> 
            <Description>Second Dataset</Description> 
        </Output> 
        <Input id="dataset1" name="Dataset 1" type="DataTable"> 
            <Description>First Input Table</Description>
        </Input> 
        <Input id="dataset2" name="Dataset 2" type="DataTable"> 
            <Description>Second Input Table</Description> 
        </Input> 
    </Ports> 


並在清單中的 hello 物件清單傳回 hello 'CustomAddRows.R' 中的正確順序：

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) { 
        if (swap) { dataset <- rbind(dataset2, dataset1)) } 
        else { dataset <- rbind(dataset1, dataset2)) 
        } 
    return (list(dataset, dataset1, dataset2)) 
    } 

**視覺效果輸出：**您也可以指定類型的輸出連接埠*視覺效果*，這會顯示 hello hello R 圖形裝置主控台輸出和輸出。 此連接埠不是 hello R 函式輸出的一部分，並不會干擾其他 hello hello 順序輸出連接埠類型。 tooadd 視覺效果的連接埠 toohello 自訂模組，新增**輸出**值的項目*視覺效果*針對其**類型**屬性：

    <Output id="deviceOutput" name="View Port" type="Visualization">
      <Description>View hello R console graphics device output.</Description>
    </Output>

**輸出規則：**

* hello 值 hello**識別碼**屬性 hello**輸出**元素必須是有效的 R 變數名稱。
* hello 值 hello**識別碼**屬性 hello**輸出**項目不能超過 32 個字元。
* hello 值 hello**名稱**屬性 hello**輸出**項目不能超過 64 個字元。
* hello 值 hello**類型**屬性 hello**輸出**項目必須是*視覺效果*。

### <a name="arguments"></a>引數
其他資料可以透過 hello 中定義的模組參數傳遞 toohello R 函式**引數**項目。 選取 hello 模組時，這些參數會顯示 hello 機器學習 UI hello 最右邊的屬性 窗格中。 引數可以是任何支援的 hello 類型，或者您可以建立時所需的自訂列舉型別。 類似 toohello**連接埠**項目，**引數**項目可以有選擇性**描述**項目，指定顯示 hello 滑鼠暫留時的 hello 文字透過 hello 參數名稱。
選擇性的模組，例如 defaultValue、 minValue 和 maxValue 屬性加入 tooany 引數屬性 tooa**屬性**項目。 有效的屬性，如 hello**屬性**元素 hello 引數型別而定，並且會描述 hello 下一節中的 hello 支援的引數類型。 引數以 hello **isOptional**屬性設定太**"true"**不需要 hello 使用者 tooenter 值。 如果未提供值 toohello 引數，然後 hello 引數不會傳遞 toohello 進入點函式。 是選擇性需要 toobe hello 函式，明確處理 hello 進入點函式的引數例如指派預設值是 NULL hello 進入點函式定義中。 選擇性引數只會強制執行 hello 其他引數的限制，也就是最小值或最大值，如果 hello 使用者所提供的值。
與輸入和輸出，很重要的每一個 hello 參數有與其相關聯的唯一識別碼值。 在快速入門中的 hello 相關聯的識別碼/參數的範例是*交換*。

### <a name="arg-element"></a>Arg 元素
模組參數定義使用 hello **Arg** hello 子項目**引數**hello XML 定義檔的區段。 如同在 hello hello 子項目**連接埠**區段中，hello hello 中參數的順序**引數**區段會定義在 hello UX 中遇到的 hello 版面配置 hello 參數會出現從上往下在 hello UI 中相同訂單在其定義所在的 hello hello XML 檔案中。 以下列出 hello Machine learning 支援參數的型別。 

**int** ：整數 (32 位元) 類型的參數。

    <Arg id="intValue1" name="Int Param" type="int">
        <Properties min="0" max="100" default="0" />
        <Description>Integer Parameter</Description>
    </Arg>


* *選擇性屬性*：**min**、**max**、**default** 和 **isOptional**

**double** ：double 類型的參數。

    <Arg id="doubleValue1" name="Double Param" type="double">
        <Properties min="0.000" max="0.999" default="0.3" />
        <Description>Double Parameter</Description>
    </Arg>


* *選擇性屬性*：**min**、**max**、**default** 和 **isOptional**

**bool** ：在 UX 中以核取方塊代表的布林值參數。

    <Arg id="boolValue1" name="Boolean Param" type="bool">
        <Properties default="true" />
        <Description>Boolean Parameter</Description>
    </Arg>



* *選擇性屬性*： **default** - 如果未設定，則為 false

**string**：標準字串

    <Arg id="stringValue1" name="My string Param" type="string">
        <Properties isOptional="true" />
        <Description>String Parameter 1</Description>
    </Arg>    

* *選擇性屬性*：**default** 和 **isOptional**

**ColumnPicker**：資料行選取參數。 此類型會在 hello UX 成活欄位選擇器。 hello**屬性**項目是使用這裡 toospecify hello 識別碼 hello 從中選取資料行，必須 hello 目標連接埠類型的連接埠*DataTable*。 hello 資料行選取範圍的 hello 結果會傳遞 toohello R 函式，以包含 hello 選取資料行名稱的字串清單。 

        <Arg id="colset" name="Column set" type="ColumnPicker">      
          <Properties portId="datasetIn1" allowedTypes="Numeric" default="NumericAll"/>
          <Description>Column set</Description>
        </Arg>


* *必要屬性*: **portId** -比對 hello 輸入項目的 id 與型別*DataTable*。
* *選擇性屬性*：
  
  * **allowedTypes** -您可以挑選篩選 hello 資料行類型。 有效值包含： 
    
    * 數值
    * Boolean
    * 類別
    * string
    * 標籤
    * 功能
    * 分數
    * 全部
  * **預設**-hello 資料行選擇器的有效預設選取項目包括： 
    
    * None
    * NumericFeature
    * NumericLabel
    * NumericScore
    * NumericAll
    * BooleanFeature
    * BooleanLabel
    * BooleanScore
    * BooleanAll
    * CategoricalFeature
    * CategoricalLabel
    * CategoricalScore
    * CategoricalAll
    * StringFeature
    * StringLabel
    * StringScore
    * StringAll
    * AllLabel
    * AllFeature
    * AllScore
    * 全部

**DropDown**：使用者指定的列舉 (下拉式) 清單。 hello 下拉式清單中的項目指定在 hello**屬性**項目使用**項目**項目。 hello**識別碼**每個**項目**必須是唯一的以及有效的 R 變數。 hello 值 hello**名稱**的**項目**做為您所看到的 hello 文字和傳遞 toohello R 函式的 hello 值。

    <Arg id="color" name="Color" type="DropDown">
      <Properties default="red">
        <Item id="red" name="Red Value"/>
        <Item id="green" name="Green Value"/>
        <Item id="blue" name="Blue Value"/>
      </Properties>
      <Description>Select a color.</Description>
    </Arg>    

* *選擇性屬性*：
  * **預設**-hello hello 預設屬性必須對應於從 hello 的其中一個識別碼值的值**項目**項目。

### <a name="auxiliary-files"></a>輔助檔案
將自訂模組 ZIP 檔案中放置任何檔案在執行階段是持續 toobe 可供使用。 所有存在的目錄結構皆會保留。 這表示檔案來源 works hello 相同本機及 Azure 機器學習服務執行中。 

> [!NOTE]
> 請注意，所有檔案解壓縮的 too'src' directory，讓所有路徑應該都有 ' src /' 前置詞。
> 
> 

例如，假設您想 tooremove NAs hello 資料集，從任何資料列也之前輸出到 CustomAddRows，移除任何重複的資料列，並已撰寫的也 RemoveDupNARows.R 檔案中的 R 函數：

    RemoveDupNARows <- function(dataFrame) {
        #Remove Duplicate Rows:
        dataFrame <- unique(dataFrame)
        #Remove Rows with NAs:
        finalDataFrame <- dataFrame[complete.cases(dataFrame),]
        return(finalDataFrame)
    }
您可以來源 hello 輔助檔案 RemoveDupNARows.R，hello CustomAddRows 函式中：

    CustomAddRows <- function(dataset1, dataset2, swap=FALSE) {
        source("src/RemoveDupNARows.R")
            if (swap) { 
                dataset <- rbind(dataset2, dataset1))
             } else { 
                  dataset <- rbind(dataset1, dataset2)) 
             } 
        dataset <- removeDupNARows(dataset)
        return (dataset)
    }

接著，上傳包含 ‘CustomAddRows.R’、‘CustomAddRows.xml’ 和 ‘RemoveDupNARows.R’ 的 zip 檔案，做為自訂 R 模組。

## <a name="execution-environment"></a>執行環境
hello 執行環境的 hello R 指令碼會使用 hello 相同版本的 R hello**執行 R 指令碼**模組和使用可以 hello 相同預設封裝。 您也可以包含在 hello 自訂模組 zip 套件，以加入其他 R 封裝 tooyour 自訂模組。 只要在您的 R 指令碼中載入它們，就像在您自己的 R 環境中一樣。 

**Hello 執行環境的限制**包括：

* 非持續的檔案系統： hello 自訂模組執行時，寫入的檔案不會保存跨多個回合的 hello 相同的模組。
* 無法存取網路

