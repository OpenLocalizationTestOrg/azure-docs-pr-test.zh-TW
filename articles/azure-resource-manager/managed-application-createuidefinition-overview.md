---
title: "建立 Azure 受管理的應用程式的 UI 定義 aaaUnderstand |Microsoft 文件"
description: "描述如何將 UI 定義 toocreate Azure 受管理的應用程式"
services: azure-resource-manager
documentationcenter: na
author: tabrezm
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/11/2017
ms.author: tabrezm;tomfitz
ms.openlocfilehash: d53ddf438c24d5a6cb8dd53ca0b4694ab0462515
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-createuidefinition"></a>開始使用 CreateUiDefinition
本文件介紹 hello 的 CreateUiDefinition，hello Azure 入口網站 toogenerate hello 使用者介面會用它來建立受管理的應用程式的核心概念。

```json
{
   "$schema": "https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json",
   "handler": "Microsoft.Compute.MultiVm",
   "version": "0.1.2-preview",
   "parameters": {
      "basics": [ ],
      "steps": [ ],
      "outputs": { }
   }
}
```

CreateUiDefinition 一律會包含三個屬性︰ 

* 處理常式
* 版本
* 參數

受管理的應用程式的處理常式應一律`Microsoft.Compute.MultiVm`，且最新支援的 hello 版本`0.1.2-preview`。

hello 結構描述的 hello 參數屬性取決於 hello hello 指定的處理常式和版本組合。 對於受管理的應用程式，支援的 hello 屬性是`basics`， `steps`，和`outputs`。 hello 基本概念和步驟的屬性包含 hello_元素_-例如文字方塊和下拉式清單-toobe 中顯示 hello Azure 入口網站。 屬性是使用的 toomap hello 輸出值的 hello 輸出 hello hello Azure Resource Manager 部署範本指定的項目 toohello 參數。

建議包含 `$schema`，但是為選用。 如果指定，hello 值`version`必須符合 hello 版本內 hello `$schema` URI。

## <a name="basics"></a>基本概念
hello 基本步驟永遠是 hello hello 精靈時 hello Azure 入口網站會剖析 CreateUiDefinition 產生第一個步驟。 此外 toodisplaying hello 元素指定`basics`，hello 入口網站會插入使用者 toochoose hello 訂用帳戶、 資源群組和 hello 部署位置的項目。 通常，查詢整個部署的參數，如叢集或系統管理員認證，hello 名稱的項目應該在此步驟。

如果項目的行為會取決於 hello 使用者訂用帳戶、 資源群組或位置，然後該元素不能在基本概念。 例如， **Microsoft.Compute.SizeSelector** hello 使用者的訂用帳戶和位置 toodetermine hello 清單可用的大小而定。 因此，**Microsoft.Compute.SizeSelector** 只能用於步驟中。 一般而言，只有中的項目 hello **Microsoft.Common**命名空間可用於基本概念。 雖然某些其他命名空間中的項目 (例如**Microsoft.Compute.Credentials**)，不需依賴 hello 使用者的內容，仍允許。

## <a name="steps"></a>步驟
hello 步驟屬性可以包含零或多個額外的步驟 toodisplay 基本概念，其中每一個都包含一個或多個項目之後。 請考慮將每個角色或部署的 hello 應用程式層的步驟。 例如，在叢集中加入 hello 主要節點中，輸入步驟與 hello 背景工作角色節點的步驟。

## <a name="outputs"></a>輸出
hello Azure 入口網站會使用 hello`outputs`屬性 toomap 項目從`basics`和`steps`toohello hello Azure Resource Manager 部署範本參數。 hello 索引鍵，此字典的 hello hello 範本參數，名稱，而 hello 值從 hello 參考項目 hello 輸出物件的屬性。

## <a name="functions"></a>Functions
類似太[樣板函式](resource-group-template-functions.md)Azure 資源管理員 中 （兩者皆語法和功能），CreateUiDefinition 提供函數來處理項目的輸入和輸出，以及條件 等功能。

## <a name="next-steps"></a>後續步驟
CreateUiDefinition 本身有簡單的結構描述。 它的 hello 真實深度來自所有 hello 支援項目和函式，下列文件的 hello 驚人的詳細說明：

- [元素](managed-application-createuidefinition-elements.md)
- [函式](managed-application-createuidefinition-functions.md)

以下可取得 CreateUiDefinition 目前的 JSON 結構描述︰https://schema.management.azure.com/schemas/0.1.2-preview/CreateUIDefinition.MultiVm.json。 

更新的版本將會位於 hello 相同的位置。 取代 hello`0.1.2-preview`部分 hello URL 和 hello`version`值想 toouse 與 hello 版本識別項。 目前支援的 hello 版本識別項是`0.0.1-preview`， `0.1.0-preview`， `0.1.1-preview`，和`0.1.2-preview`。
