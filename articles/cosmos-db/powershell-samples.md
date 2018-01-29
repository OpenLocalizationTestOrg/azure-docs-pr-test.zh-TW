---
title: "適用於 Azure Cosmos DB 的 Azure PowerShell 範例 | Microsoft Docs"
description: "Azure PowerShell 範例：協助您建立和管理 Azure Cosmos DB 帳戶的指令碼。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 10/16/2017
ms.author: mimig
ms.openlocfilehash: de892cc631585c55b0c15f4efe1e06ad55afdce5
ms.sourcegitcommit: a5f16c1e2e0573204581c072cf7d237745ff98dc
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/11/2017
---
# <a name="azure-powershell-samples-for-azure-cosmos-db"></a>適用於 Azure Cosmos DB 的 Azure PowerShell 範例

[!INCLUDE [cosmos-db-sql-api](../../includes/cosmos-db-sql-api.md)]

下表包含適用於 Azure Cosmos DB 之範例 Azure PowerShell 指令碼的連結。 目前您只能透過 PowerShell 管理 Azure Cosmos DB 帳戶層；無法透過 PowerShell 管理諸如資料庫和集合等其他資源。

| |  |
|---|---|
|**建立 Azure Cosmos DB 帳戶**||
|[建立 SQL API 帳戶](scripts/create-database-account-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 建立單一 Azure Cosmos DB 帳戶以搭配 SQL API。 |
|**調整 Azure Cosmos DB**||
|[複寫多個區域中的 Azure Cosmos DB 帳戶和設定容錯移轉優先順序](scripts/scale-multiregion-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|使用指定的容錯移轉優先順序，將帳戶資料複寫到全球多個區域中。|
|**保護 Azure Cosmos DB**||
| [取得帳戶金鑰](scripts/secure-get-account-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 取得帳戶主要和次要的主要 (master) 寫入金鑰，以及主要和次要唯讀金鑰。|
| [取得 MongoDB 連接字串](scripts/secure-mongo-connection-string-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json) | 取得連接字串以將您的 MongoDB 應用程式連線到 Azure Cosmos DB 帳戶。|
|[重新產生帳戶金鑰](scripts/secure-regenerate-key-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|重新產生帳戶的主要或唯讀金鑰。|
|[建立防火牆](scripts/create-firewall-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)| 建立輸入 IP 存取控制原則，以限制從核准的電腦集合和/或雲端服務存取帳戶。|
|**高可用性、災害復原、備份和還原**||
|[設定容錯移轉原則](scripts/ha-failover-policy-powershell.md?toc=%2fpowershell%2fmodule%2ftoc.json)|針對要在其中複寫帳戶的每個區域，設定容錯移轉優先順序。|
|||
