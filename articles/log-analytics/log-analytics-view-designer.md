---
title: "OMS 記錄分析 aaaCreate 檢視 tooanalyze 資料 |Microsoft 文件"
description: "檢視表設計工具中記錄分析可讓您 toocreate 自訂檢視會顯示在 hello OMS 和 Azure 入口網站，並包含不同的視覺效果 hello OMS 儲存機制中的資料。 本文包含檢視設計工具的概觀以及建立和編輯自訂檢視的程序。"
services: log-analytics
documentationcenter: 
author: bwren
manager: jwhit
editor: 
ms.assetid: ce41dc30-e568-43c1-97fa-81e5997c946a
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/17/2017
ms.author: bwren
ms.openlocfilehash: 40b4bfef50d70e4479b6cae16abfa8ec33d1a2f1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-view-designer-toocreate-custom-views-in-log-analytics"></a>在 記錄分析中使用檢視表設計工具 toocreate 自訂檢視
hello 檢視表設計工具中[記錄分析](log-analytics-overview.md)可讓您 toocreate 自訂檢視 hello OMS 主控台中包含不同的視覺效果 hello OMS 儲存機制中的資料。 本文包含檢視設計工具的概觀以及建立和編輯自訂檢視的程序。

其他與檢視設計工具相關的文章︰

* [磚參考](log-analytics-view-designer-tiles.md)-參考的每一個 hello hello 設定磚可用 toouse 中自訂檢視。
* [視覺效果部分參考](log-analytics-view-designer-parts.md)-參考的每一個 hello hello 設定磚可用 toouse 中自訂檢視。

>[!NOTE]
> 如果您的工作區已升級的 toohello[新的記錄分析查詢語言](log-analytics-log-search-upgrade.md)，則必須寫入所有檢視中的查詢中 hello[新的查詢語言](https://go.microsoft.com/fwlink/?linkid=856078)。  Hello 工作區已升級之前建立的任何檢視會 automtically 轉換。

## <a name="concepts"></a>概念
建立以 hello 檢視表設計工具檢視包含 hello hello 下表中的項目。

| 部分 | 說明 |
|:--- |:--- |
| 圖格 |顯示在 hello 主要記錄檔分析概觀儀表板上。  包含 hello 所包含的 hello 視覺化摘要自訂檢視。  不同類型的磚會提供不同的視覺效果 hello OMS 儲存機制中的記錄。  按一下 hello 磚 tooopen hello 的自訂檢視。 |
| 自訂檢視 |當 hello 使用者在 hello 並排顯示。  包含一或多個視覺效果組件。 |
| 視覺效果組件 |Hello OMS 儲存機制中的資料視覺效果是根據一或多個[記錄搜尋](log-analytics-log-searches.md)。  大部分的組件會包含提供高層級的視覺效果的標頭以及一份 hello 前的結果。  不同的組件類型提供不同的視覺效果 hello OMS 儲存機制中的記錄。  按一下 hello 一部分 tooperform 中的項目提供詳細的記錄的記錄搜尋。 |

![檢視設計工具概觀](media/log-analytics-view-designer/overview.png)

## <a name="add-view-designer-tooyour-workspace"></a>加入檢視表設計工具 tooyour 工作區
在預覽中檢視表設計工具時，您必須將它加入 tooyour 工作區選取**預覽功能**在 hello**設定**hello OMS 入口網站的區段。

![啟用預覽](media/log-analytics-view-designer/preview.png)

## <a name="creating-and-editing-views"></a>建立和編輯檢視
### <a name="create-a-new-view"></a>建立新的檢視
開啟新的檢視中 hello**檢視表設計工具**hello 檢視表設計工具上的 並排顯示 hello 主要 OMS 儀表板中。

![檢視設計工具圖格](media/log-analytics-view-designer/view-designer-tile.png)

### <a name="edit-an-existing-view"></a>編輯現有檢視
tooedit hello 檢視設計工具中，按一下其 hello 主要 OMS 儀表板磚上開啟 hello 檢視中現有的檢視。  然後按一下 hello**編輯**按鈕 tooopen hello 檢視表設計工具中的 hello 檢視。

![編輯檢視](media/log-analytics-view-designer/menu-edit.png)

### <a name="clone-an-existing-view"></a>複製現有檢視
當您複製檢視時，它會建立新的檢視，並且在 hello 檢視表設計工具中開啟。  hello 新檢視會有相同的名稱，為 「 複製 」 附加的 toohello 結尾它與原始的 hello hello。  tooclone] 檢視中，開啟 hello hello 主要 OMS 儀表板中的磚上的 [現有的檢視。  然後按一下 hello**複製**按鈕 tooopen hello 檢視表設計工具中的 hello 檢視。

![複製檢視](media/log-analytics-view-designer/edit-menu-clone.png)

### <a name="delete-an-existing-view"></a>刪除現有檢視
toodelete 現有的檢視，開啟 hello 檢視其 hello 主要 OMS 儀表板磚上按一下。  然後按一下 hello**編輯**按鈕 tooopen hello 檢視在 hello 檢視表設計工具，然後按一下**刪除檢視**。

![刪除檢視](media/log-analytics-view-designer/edit-menu-delete.png)

### <a name="export-an-existing-view"></a>匯出現有檢視
您可以匯出檢視 tooa JSON 檔案，您可以匯入至另一個工作區，或在使用[Azure Resource Manager 範本](../azure-resource-manager/resource-group-authoring-templates.md)。  tooexport 現有的檢視，開啟 hello 檢視其 hello 主要 OMS 儀表板磚上按一下。  然後按一下 hello**匯出**按鈕 toocreate hello 瀏覽器的下載資料夾中的檔案。  hello hello 檔案名稱會是副檔名為 hello hello 檢視 hello 名稱*omsview*。

![匯出檢視](media/log-analytics-view-designer/edit-menu-export.png)

### <a name="import-an-existing-view"></a>匯入現有檢視
您可以匯入您從其他管理群組匯出的 omsview 檔案。  tooimport 現有的檢視，第一次建立新的檢視。  然後按一下 hello**匯入**按鈕並選取 hello *omsview*檔案。  hello 檔案中的 hello 組態將會複製到 hello 現有檢視。

![匯出檢視](media/log-analytics-view-designer/edit-menu-import.png)

## <a name="working-with-view-designer"></a>使用檢視設計工具
hello 檢視表設計工具有三個窗格。  hello**設計**窗格代表 hello 自訂檢視。  當您將加入圖格和組件從 hello**控制項**窗格 toohello**設計**它們的窗格加入 toohello 檢視。  hello**屬性**窗格會顯示 hello 屬性 hello 磚或選取的組件。

![[檢視設計工具]](media/log-analytics-view-designer/view-designer-screenshot.png)

### <a name="configure-view-tile"></a>設定檢視圖格
自訂檢視可以只有單一圖格。  選取 hello**磚** 索引標籤中 hello**控制項**窗格 tooview hello 目前磚，或選取替代的那一個。  hello**屬性**窗格會顯示 hello 目前 tile hello 屬性。  設定 hello 圖格屬性，根據 toohello 詳細的資訊在 hello[磚參考](log-analytics-view-designer-tiles.md)按一下**套用**toosave 變更。

### <a name="configure-visualization-parts"></a>設定視覺效果組件
檢視可以包含任意數目的視覺效果組件。  選取 hello**檢視**索引標籤，然後視覺效果部分 tooadd toohello 檢視。  hello**屬性**窗格會顯示 hello hello 選取組件的屬性。  設定 hello 檢視根據 toohello 屬性的詳細資訊，在 hello[視覺效果部分參考](log-analytics-view-designer-parts.md)按一下**套用**toosave 變更。

### <a name="delete-a-visualization-part"></a>刪除視覺效果組件
您可以從 hello 檢視移除視覺效果的一部分，依序按一下 hello **X** hello 右上角的 hello 組件中的按鈕。

### <a name="rearrange-visualization-parts"></a>重新整理視覺效果組件
檢視只有一列視覺效果組件。  按一下並拖曳它們 tooa 新位置，重新排列在檢視中的現有組件。

## <a name="next-steps"></a>後續步驟
* 新增[磚](log-analytics-view-designer-tiles.md)tooyour 自訂檢視。
* 新增[視覺效果部分](log-analytics-view-designer-parts.md)tooyour 自訂檢視。
