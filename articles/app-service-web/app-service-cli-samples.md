---
title: "aaaAzure CLI 範例-應用程式服務 |Microsoft 文件"
description: "Azure CLI 範例 - App Service"
services: app-service
documentationcenter: app-service
author: syntaxc4
manager: erikre
editor: ggailey777
tags: azure-service-management
ms.assetid: 53e6a15a-370a-48df-8618-c6737e26acec
ms.service: app-service
ms.devlang: na
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: app-service
ms.date: 03/08/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: a943ccffb59c5d30a44cf1ce513fd2eac46101f7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-cli-samples"></a>Azure CLI 範例

hello 下表包含使用 Azure CLI hello 建置連結 toobash 指令碼。

| | |
|-|-|
|**建立應用程式**||
| [建立 Web 應用程式並從 從 GitHub 部署程式碼](./scripts/app-service-cli-deploy-github.md?toc=%2fcli%2fazure%2ftoc.json)| 建立 Azure Web 應用程式和從公用 GitHub 存放庫部署程式碼。 |
| [建立可從 GitHub 連續部署的 Web 應用程式](./scripts/app-service-cli-continuous-deployment-github.md?toc=%2fcli%2fazure%2ftoc.json)| 建立可從您擁有的 GitHub 存放庫連續發佈的 Azure Web 應用程式。 |
| [建立 Web 應用程式並從本機 Git 存放庫部署程式碼](./scripts/app-service-cli-deploy-local-git.md?toc=%2fcli%2fazure%2ftoc.json) | 建立 Azure Web 應用程式並設定從本機 Git 存放庫推送程式碼的作業。 |
| [建立 web 應用程式和部署程式碼 tooa 預備環境](./scripts/app-service-cli-deploy-staging-environment.md?toc=%2fcli%2fazure%2ftoc.json) | 建立具有部署位置以供放置預備程式碼變更的 Azure Web 應用程式。 |
| [在 Docker 容器中建立 ASP.NET 核心 Web 應用程式](./scripts/app-service-cli-linux-docker-aspnetcore.md?toc=%2fcli%2fazure%2ftoc.json)| 在 Linux 上建立 Azure Web 應用程式，並從 Docker Hub 載入 Docker 映像。 |
|**設定應用程式**||
| [對應的自訂網域 tooa web 應用程式](./scripts/app-service-cli-configure-custom-domain.md?toc=%2fcli%2fazure%2ftoc.json)| 建立 Azure web 應用程式，並將對應的自訂網域名稱 tooit。 |
| [繫結的自訂 SSL 憑證 tooa web 應用程式](./scripts/app-service-cli-configure-ssl-certificate.md?toc=%2fcli%2fazure%2ftoc.json)| 建立 Azure web 應用程式，並繫結的自訂網域名稱 tooit hello SSL 憑證。 |
|**調整應用程式**||
| [手動調整 Web 應用程式](./scripts/app-service-cli-scale-manual.md?toc=%2fcli%2fazure%2ftoc.json) | 建立 Azure Web 應用程式，並將它調整到 2 個執行個體中。 |
| [透過高可用性架構將 Web 應用程式調整為全球可用](./scripts/app-service-cli-scale-high-availability.md?toc=%2fcli%2fazure%2ftoc.json) | 在兩個不同的地理區域中建立兩個 Azure Web 應用程式，並使用 Azure 流量管理員讓它們可透過單一端點來使用。 |
|**連接應用程式 tooresources**||
| [連接 web 應用程式 tooa SQL 資料庫](./scripts/app-service-cli-app-service-sql.md?toc=%2fcli%2fazure%2ftoc.json)| 建立 Azure web 應用程式和 SQL 資料庫，然後加入 hello 資料庫連線字串 toohello 應用程式的設定。 |
| [連接 web 應用程式 tooa 儲存體帳戶](./scripts/app-service-cli-app-service-storage.md?toc=%2fcli%2fazure%2ftoc.json)| 建立 Azure web 應用程式和儲存體帳戶，然後新增 hello 儲存體連接字串 toohello 應用程式設定。 |
| [連接 web 應用程式 tooa redis 快取](./scripts/app-service-cli-app-service-redis.md?toc=%2fcli%2fazure%2ftoc.json) | 建立 Azure web 應用程式與 redis 快取，然後將 hello redis 連線詳細資料 toohello 應用程式設定）。 |
| [連接 web 應用程式 tooCosmos DB](./scripts/app-service-cli-app-service-documentdb.md?toc=%2fcli%2fazure%2ftoc.json) | 建立 Azure web 應用程式和 Cosmos DB 中，然後加入 hello Cosmos DB 連線詳細資料 toohello 應用程式的設定。 |
|**監視應用程式**||
| [使用 Web 伺服器記錄監視 Web 應用程式](./scripts/app-service-cli-monitor.md?toc=%2fcli%2fazure%2ftoc.json) | 建立 Azure web 應用程式、 啟用記錄，並下載 hello 記錄 tooyour 本機電腦。 |
| | |