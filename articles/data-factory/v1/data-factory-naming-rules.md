---
title: "命名 Azure Data Factory 實體的規則 |Microsoft Docs"
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
ms.date: 01/10/2018
ms.author: shlo
robots: noindex
ms.openlocfilehash: a6bb9cc567ac9c9658c18bc20e11a6349ec7b930
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/23/2018
---
# <a name="azure-data-factory---naming-rules"></a>Azure Data Factory - 命名規則
> [!NOTE]
> 本文適用於正式推出 (GA) 的第 1 版 Data Factory。 如果您使用第 2 版 Data Factory 服務 (預覽版)，請參閱 [Data Factory 第 2 版中的命名規則](../naming-rules.md)。

下表提供 Data Factory 購件命名規則。

| Name | 名稱唯一性 | 驗證檢查 |
|:--- |:--- |:--- |
| Data Factory |在 Microsoft Azure 中是唯一的。 名稱不區分大小寫，亦即 `MyDF` 和 `mydf` 會指相同的 Data Factory。 |<ul><li>每個 Data Factory 只會繫結至一個 Azure 訂用帳戶。</li><li>物件名稱必須以字母或數字開頭，並且只能包含字母、數字和虛線 (-) 字元。</li><li>每個虛線 (-) 字元的前面和後面必須緊接字母或數字。 容器名稱中不允許使用連續虛線。</li><li>名稱長度可以介於 3-63 個字元。</li></ul> |
| 連結的服務/資料表/管線 |在 Data Factory 中是唯一的。 名稱不區分大小寫。 |<ul><li>資料表名稱的字元數目上限︰260。</li><li>物件名稱開頭必須為字母、數字或底線 (_)。</li><li>不允許使用下列字元：“.”、“+”、“?”、“/”、“<”、”>”、”*”、”%”、”&”、”:”、”\\”</li></ul> |
| 資源群組 |在 Microsoft Azure 中是唯一的。 名稱不區分大小寫。 |<ul><li>字元數目上限︰1000。</li><li>名稱可包含字母、數字及下列字元：“-”、“_”、“,” 和 “.”。</li></ul> |

