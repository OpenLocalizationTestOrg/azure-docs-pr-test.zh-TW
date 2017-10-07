---
title: "命名 Azure Data Factory 實體 aaaRules |Microsoft 文件"
description: "描述 Data Factory 實體的命名規則。"
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: monicar
ms.assetid: bc5e801d-0b3b-48ec-9501-bb4146ea17f1
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/14/2017
ms.author: shlo
ms.openlocfilehash: 98c5fc5fc932b72b65894afad438b4dc321c8aca
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-data-factory---naming-rules"></a>Azure Data Factory - 命名規則
hello 下表提供 Data Factory 成品的命名規則。

| 名稱 | 名稱唯一性 | 驗證檢查 |
|:--- |:--- |:--- |
| Data Factory |在 Microsoft Azure 中是唯一的。 名稱不區分大小寫，也就是`MyDF`和`mydf`參考 toohello 相同的 data factory。 |<ul><li>每個 data factory 是繫結的 tooexactly 一個 Azure 訂閱。</li><li>物件名稱必須以字母或數字開頭，而且只能包含字母、 數字和 hello 虛線 （-） 字元。</li><li>每個虛線 (-) 字元的前面和後面必須緊接字母或數字。 容器名稱中不允許使用連續虛線。</li><li>名稱長度可以介於 3-63 個字元。</li></ul> |
| 連結的服務/資料表/管線 |在 Data Factory 中是唯一的。 名稱不區分大小寫。 |<ul><li>資料表名稱的字元數目上限︰260。</li><li>物件名稱開頭必須為字母、數字或底線 (_)。</li><li>不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</li></ul> |
| 資源群組 |在 Microsoft Azure 中是唯一的。 名稱不區分大小寫。 |<ul><li>字元數目上限︰1000。</li><li>名稱只能包含字母、 數字及下列字元的 hello:"-"，"_"，"，"和"。"</li></ul> |

