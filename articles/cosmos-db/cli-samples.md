---
title: "適用於 Azure Cosmos DB 的 CLI 範例 aaaAzure |Microsoft 文件"
description: "Azure CLI 範例：建立及管理 Azure Cosmos DB 帳戶、資料庫、容器、區域和防火牆。"
services: cosmos-db
author: mimig1
manager: jhubbard
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: cosmos-db
ms.custom: mvc
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: database
ms.date: 06/07/2017
ms.author: mimig
ms.openlocfilehash: d6eefc3274e0b66eec4e69166bb7d4ddd58a522e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples-for-azure-cosmos-db"></a>適用於 Azure Cosmos DB 的 Azure CLI 範例

hello 下表包含連結 toosample Azure CLI 指令碼的 Azure Cosmos DB。 所有 Azure Cosmos DB CLI 命令的參考頁面都使用 hello [Azure CLI 2.0 參考](https://docs.microsoft.com/cli/azure/cosmosdb)。

| |  |
|---|---|
|**建立 Azure Cosmos DB 帳戶、資料庫和容器**||
|[建立 DocumentDB API、圖形或資料表 API 帳戶](scripts/create-database-account-collections-cli.md?toc=%2fcli%2fazure%2ftoc.json)| 以 hello DocumentDB、 圖表或資料表的應用程式開發介面，會建立單一 Azure Cosmos DB API 帳戶、 資料庫和使用的容器。 |
| [建立 MongoDB API 帳戶](scripts/create-mongodb-database-account-cli.md?toc=%2fcli%2fazure%2ftoc.json) | 建立單一 Azure Cosmos DB MongoDB API 帳戶、資料庫和集合。 |
|**調整 Azure Cosmos DB**||
| [調整容器輸送量](scripts/scale-collection-throughput-cli.md?toc=%2fcli%2fazure%2ftoc.json) | 變更 hello 佈建 througput 在容器上。|
|[複寫多個區域中的 Azure Cosmos DB 資料庫帳戶和設定容錯移轉優先順序](scripts/scale-multiregion-cli.md?toc=%2fcli%2fazure%2ftoc.json)|使用指定的容錯移轉優先順序，將帳戶資料複寫到全球多個區域中。|
|**保護 Azure Cosmos DB**||
| [取得帳戶金鑰](scripts/secure-get-account-key-cli.md?toc=%2fcli%2fazure%2ftoc.json) | 取得 hello 主要和次要的主要寫入索引鍵和主要和次要唯讀金鑰 hello 帳戶。|
| [取得 MongoDB 連接字串](scripts/secure-mongo-connection-string-cli.md?toc=%2fcli%2fazure%2ftoc.json) | 取得 hello 連接字串 tooconnect 您 MongoDB 應用程式 tooyour Azure Cosmos DB 帳戶。|
|[重新產生帳戶金鑰](scripts/secure-regenerate-key-cli.md?toc=%2fcli%2fazure%2ftoc.json)|重新產生 hello 主要或唯讀 hello 帳戶金鑰。|
|[建立防火牆](scripts/create-firewall-cli.md?toc=%2fcli%2fazure%2ftoc.json)| 從機器及/或雲端服務的核准設定組中建立輸入的 IP 存取控制原則 toolimit 存取 toohello 帳戶。|
|**高可用性、災害復原、備份和還原**||
|[設定容錯移轉原則](scripts/ha-failover-policy-cli.md?toc=%2fcli%2fazure%2ftoc.json)|設定 hello hello 帳戶複寫所在的每個區域的容錯移轉優先權。|
|**將 Azure Cosmos DB 連線到資源**||
|[連接 web 應用程式 tooAzure Cosmos DB](https://docs.microsoft.com/azure/app-service-web/scripts/app-service-cli-app-service-documentdb?toc=%2fcli%2fazure%2ftoc.json)|建立 Azure Cosmos DB 資料庫和 Azure Web 應用程式並將兩者連線。|
|||
