---
title: "aaaPublish WebApplicationWebSite （Windows PowerShell 指令碼） |Microsoft 文件"
description: "了解如何 toopublish web 專案 tooan Azure 網站。 如果不存在，此指令碼會建立所需的 hello 資源您 Azure 訂用帳戶中。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: 63cfaa2d-f04d-40dc-8677-345385c278d5
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: d46904e30e3c2e040e57888fa31543e8e366527f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationwebsite-windows-powershell-script"></a>Publish-WebApplicationWebSite (Windows PowerShell 指令碼)
## <a name="syntax"></a>語法
發行的 web 專案 tooan Azure 網站。 若不存在，hello 指令碼會建立所需的 hello 資源您 Azure 訂用帳戶中。

    Publish-WebApplicationWebSite
    –Configuration <configuration>
    -SubscriptionName <subscriptionName>
    -WebDeployPackage <packageName>
    -DatabaseServerPassword @{Name = "name"; Password = "password"}
    -SendHostMessagesToOutput
    -Verbose


## <a name="configuration"></a>組態
hello 路徑 toohello JSON 組態檔，描述 hello 部署的 hello 詳細資料。

| 參數 | 預設值 |
| --- | --- |
| 別名 |無 |
| 必要？ |true |
| 位置 |已命名 |
| 預設值 |無 |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

## <a name="subscriptionname"></a>SubscriptionName
hello hello 想 toocreate hello 網站中的 Azure 訂用帳戶名稱。

| 參數 | 預設值 |
| --- | --- |
| 別名 |無 |
| 必要？ |false |
| 位置 |已命名 |
| 預設值 |無 |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

## <a name="webdeploypackage"></a>WebDeployPackage
hello 路徑 toohello web 部署套件 toopublish toohello 網站。 您可以使用 Visual Studio 中的 hello 發行網站精靈來建立此套件。 如需詳細資訊，請參閱 [開始使用 Azure 雲端服務和 ASP.NET](http://go.microsoft.com/fwlink/p/?LinkID=623089)。

| 參數 | 預設值 |
| --- | --- |
| 別名 |無 |
| 必要？ |false |
| 位置 |已命名 |
| 預設值 |無 |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

## <a name="databaseserverpassword"></a>DatabaseServerPassword
hello 使用者名稱和密碼 hello Azure 中的 SQL 資料庫。

| 參數 | 預設值 |
| --- | --- |
| 別名 |無 |
| 必要？ |false |
| 位置 |已命名 |
| 預設值 |無 |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

## <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
如果為 true，列印訊息從 hello 指令碼 toohello 輸出資料流。

| 參數 | 預設值 |
| --- | --- |
| 別名 |無 |
| 必要？ |false |
| 位置 |已命名 |
| 預設值 |false |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

## <a name="remarks"></a>備註
如需如何 toouse hello 指令碼 toocreate 開發人員和測試環境，請參閱完整說明[使用 Windows PowerShell 指令碼 tooPublish tooDev 和測試環境](vs-azure-tools-publishing-using-powershell-scripts.md)。

hello JSON 組態檔指定部署 toobe hello 的細節。 其中包括建立 hello 專案，例如 hello 名稱和 hello 網站的使用者名稱時指定的 hello 資訊。 它也包含 hello 資料庫 tooprovision，如果有的話。 下列程式碼的 hello 顯示 JSON 組態檔範例：

    {
        "environmentSettings": {
            "webSite": {
                "name": "WebApplication10554",
                "location": "West US"
            },
            "databases": [
                {
                    "connectionStringName": "DefaultConnection",
                    "databaseName": "WebApplication10554_db",
                    "serverName": "iss00brc88",
                    "user": "sqluser2",
                    "password": "",
                    "edition": "",
                    "size": "",
                    "collation": "",
                    "location": "West US"
                }
            ]
        }
    }

您可以編輯 hello JSON 組態檔 toochange 部署的內容。 網站區段為必要項，但 hello 資料庫區段為選擇性。

## <a name="next-steps"></a>後續步驟
如需詳細資訊，請參閱 [Publish-WebApplicationVM (Windows PowerShell 指令碼)](vs-azure-tools-publish-webapplicationvm.md)

