---
title: "aaaMicrosoft Power BI Embedded-連線 tooa 資料來源"
description: "Power BI Embedded，連接 toodata 來源"
services: power-bi-embedded
documentationcenter: 
author: guyinacube
manager: erikre
editor: 
tags: 
ms.assetid: 2a4caeb3-255d-4215-9554-0ca8e3568c13
ms.service: power-bi-embedded
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: powerbi
ms.date: 01/06/2017
ms.author: asaxton
ms.openlocfilehash: b1aad6e638104716d90f7e1d060eefcbc9daedbc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-tooa-data-source"></a>Tooa 資料來源連接
使用 **Power BI Embedded**可以將報表內嵌到您自己的應用程式。 當您將 Power BI 報表內嵌到應用程式時，hello 報表連接基礎資料的 toohello**匯入**hello 資料，或是藉由複製**直接連接**toohello 資料來源使用**DirectQuery**。

以下是使用的 hello 差異**匯入**和**DirectQuery**。

| Import | DirectQuery |
| --- | --- |
| 資料表、 資料行，*和資料*匯入或複製到 hello 報表資料集。 toosee 變更發生的 toohello 基礎資料，您必須重新整理，或匯入完成，目前資料集一次。 |只有*資料表和資料行*匯入或複製到 hello 報表資料集。 您一律檢視 hello 最新的資料。 |

有了 Power BI Embedded，您就可以使用 DirectQuery 搭配雲端資料來源，但目前無法使用內部部署資料來源。

> [!NOTE]
> hello 在內部部署資料閘道不支援使用 Power BI Embedded 這一次。 這表示您無法在 DirectQuery 使用內部部署資料來源。

## <a name="supported-data-sources"></a>支援的資料來源

**DirectQuery**
* Azure SQL Database
* Azure SQL 資料倉儲

**匯入**

您可以使用所有可用的 hello 在 Power BI Desktop 中的資料來源匯入。 您將**不**是無法 toorefresh 內嵌 Power BI 的資料。 您必須變更 tooupload tooyour PBIX 檔案 tooPower BI Embedded。 這是因為 toono 可用的閘道。 

## <a name="benefits-of-using-directquery"></a>使用 DirectQuery 的優點
使用 **DirectQuery**有兩項主要優點：

* **DirectQuery**可讓您透過建立視覺效果的地方，否則會有並不可行 toofirst 匯入的極大型資料集的所有 hello 資料。
* 基礎資料變更可能需要重新整理資料，並針對某些報表，hello 需要 toodisplay 目前資料可能會需要大型資料傳輸，造成重新匯入資料並不可行。 相較之下， **DirectQuery** 報表一律使用目前的資料。

## <a name="limitations-of-directquery"></a>DirectQuery 的限制
   有一些限制 toousing **DirectQuery**:

* 所有資料表必須全都來自單一資料庫。
* 如果 hello 查詢過於複雜時，會發生錯誤。 tooremedy hello 錯誤，您必須重構 hello 查詢是較不複雜。 如果 hello 查詢必須很複雜，您將需要 tooimport hello 資料，而不是使用**DirectQuery**。
* 關聯性篩選為有限的 tooa 單一方向，而不是兩個方向。
* 您無法變更資料行 hello 資料類型。
* 根據預設，限制是置於量值允許的 DAX 運算式中。 請參閱 [DirectQuery 和量值](#measures)。

<a name="measures"/>

## <a name="directquery-and-measures"></a>DirectQuery 和量值
傳送 toohello 基礎資料來源的 tooensure 查詢可接受的效能，限制加諸於量值。 當使用**Power BI Desktop**進階使用者可以選擇 toobypass 這項限制選擇**檔案 > 選項和設定 > 選項**。 在 [hello**選項**] 對話方塊中，選擇**DirectQuery**，並選取 hello 選項**允許在 DirectQuery 模式中使用不受限制的量值**。 選取該選項後，即可使用對量值有效的任何 DAX 運算式。 使用者必須知道;但是，某些運算式的效能很好匯入 hello 資料時可能會導致查詢速度緩慢 toohello 後端來源在**DirectQuery**模式。 

## <a name="see-also"></a>另請參閱
* [開始使用 Microsoft Power BI Embedded](power-bi-embedded-get-started.md)
* [Power BI Desktop](https://powerbi.microsoft.com/documentation/powerbi-desktop-get-the-desktop/)

有其他疑問？ [再試一次 hello Power BI 社群](http://community.powerbi.com/)

