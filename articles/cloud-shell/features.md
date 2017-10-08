---
title: "aaaAzure 雲端殼層 （預覽） 功能 |Microsoft 文件"
description: "Azure Cloud Shell 的功能概觀"
services: 
documentationcenter: 
author: jluk
manager: timlt
tags: azure-resource-manager
ms.assetid: 
ms.service: azure
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-linux
ms.devlang: na
ms.topic: article
ms.date: 08/21/2017
ms.author: juluk
ms.openlocfilehash: 65482ca6caeac01dda18a6b12eabe943e3d68a96
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="features-and-tools-for-azure-cloud-shell"></a>Azure Cloud Shell 的功能和工具
Azure 雲端殼層瀏覽器為基礎的殼層經驗 toomanage 且開發的 Azure 資源。

雲端殼層，提供存取瀏覽器預先設定的管理不需要安裝、 版本控制，與自行維護電腦的 hello 成本的 Azure 資源的殼層經驗。

Cloud Shell 依照要求而佈建電腦，因此，不會在工作階段之間保存電腦狀態。 由於 Cloud Shell 是針對互動式工作階段而建置，所以殼層會在殼層閒置 20 分鐘後自動終止。

## <a name="bash-in-cloud-shell"></a>Cloud Shell 中的 Bash
### <a name="tools"></a>工具
|類別   |名稱   |
|---|---|
|Linux 殼層直譯器|Bash<br> sh               |
|Azure 工具            |[Azure CLI 2.0](https://github.com/Azure/azure-cli) \(英文\) 和 [1.0](https://github.com/Azure/azure-xplat-cli) \(英文\)<br> [AzCopy](https://docs.microsoft.com/azure/storage/storage-use-azcopy)<br> [Batch Shipyard](https://github.com/Azure/batch-shipyard)     |
|文字編輯器           |vim<br> nano<br> emacs       |
|原始檔控制         |git                    |
|建置工具            |make<br> maven<br> npm<br> pip         |
|容器             |[Docker CLI](https://github.com/docker/cli) \(英文\)/[Docker Machine](https://github.com/docker/machine) \(英文\)<br> [Kubectl](https://kubernetes.io/docs/user-guide/kubectl-overview/) \(英文\)<br> [Draft](https://github.com/Azure/draft)(英文\)<br> [DC/OS CLI](https://github.com/dcos/dcos-cli) \(英文\)         |
|資料庫              |MySQL 用戶端<br> PostgreSql 用戶端<br> [sqlcmd 公用程式](https://docs.microsoft.com/sql/tools/sqlcmd-utility) \(英文\)<br> [mssql-scripter](https://github.com/Microsoft/sql-xplat-cli) |
|其他                  |iPython 用戶端<br> [Cloud Foundry CLI](https://github.com/cloudfoundry/cli) \(英文\)<br> |

### <a name="language-support"></a>語言支援
|語言   |版本   |
|---|---|
|.NET       |1.01       |
|Go         |1.7        |
|Java       |1.8        |
|Node.js    |6.9.4      |
|Python     |2.7 和 3.5 (預設)|

## <a name="secure-automatic-authentication"></a>安全的自動驗證
雲端殼層安全地自動驗證 hello Azure CLI 2.0 的帳戶存取權。

## <a name="azure-files-persistence"></a>Azure 檔案持續性
因為 Cloud Shell 會依照要求而使用暫時電腦來配置，所以不會在工作階段之間保存位於您 $Home 外面的檔案和電腦狀態。
跨工作階段，雲端殼層會逐步引導您透過附加 Azure 的檔案共用上第一次啟動 toopersist 檔案。
完成後，Cloud Shell 會自動連結儲存體，供所有未來的工作階段使用。

[深入了解附加 Azure 檔案共用 tooCloud 殼層。](persisting-shell-storage.md)

## <a name="next-steps"></a>後續步驟
[Cloud Shell 快速入門](quickstart.md) <br>
[了解 Azure CLI 2.0](https://docs.microsoft.com/cli/azure/) \(英文\) <br>