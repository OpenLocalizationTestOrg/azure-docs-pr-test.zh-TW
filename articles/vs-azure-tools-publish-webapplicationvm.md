---
title: "aaaPublish WebApplicationVM |Microsoft 文件"
description: "深入了解如何 toodeploy web 應用程式 tooa 虛擬機器。 如果不存在，此指令碼會建立所需的 hello 資源您 Azure 訂用帳戶中。"
services: visual-studio-online
documentationcenter: na
author: kraigb
manager: ghogen
editor: 
ms.assetid: de4cec95-f73f-44d9-babd-9f47f2633cdb
ms.service: multiple
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: multiple
ms.date: 11/11/2016
ms.author: kraigb
ms.openlocfilehash: e4b52b620bebf44b87ddfc3b19c155bb65111814
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-webapplicationvm-windows-powershell-script"></a>Publish-WebApplicationVM (Windows PowerShell 指令碼)
部署 web 應用程式 tooa 虛擬機器。 若不存在，hello 指令碼會建立所需的 hello 資源您 Azure 訂用帳戶中。

```
Publish-WebApplicationVM
–Configuration <configuration>
-SubscriptionName <subscriptionName>
-WebDeployPackage <packageName>
-VMPassword @{Name = "name"; Password = "password")
-DatabaseServerPassword @{Name = "name"; Password = "password"}
-SendHostMessagesToOutput
-Verbose
```

### <a name="configuration"></a>組態
hello 路徑 toohello JSON 組態檔，描述 hello 部署的 hello 詳細資料。

| 別名 | 無 |
| --- | --- |
| 必要？ |true |
| 位置 |已命名 |
| 預設值 |無 |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

### <a name="subscriptionname"></a>SubscriptionName
hello 名稱 hello 想 toocreate hello 虛擬機器的 Azure 訂用帳戶。

| 別名 | 無 |
| --- | --- |
| 必要？ |false |
| 位置 |已命名 |
| 預設值 |在 hello 訂用帳戶檔案中使用 hello 第一個訂用帳戶 |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

### <a name="webdeploypackage"></a>WebDeployPackage
hello 路徑 toohello web 部署套件 toopublish toohello 虛擬機器。 您可以使用 Visual Studio 中的 hello 發行網站精靈來建立此套件。 請參閱 [如何：在 Visual Studio 中建立 Web 部署封裝](https://msdn.microsoft.com/library/dd465323.aspx)。

| 別名 | 無 |
| --- | --- |
| 必要？ |false |
| 位置 |已命名 |
| 預設值 |無 |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

### <a name="allowuntrusted"></a>AllowUntrusted
如果為 true，允許 hello 使用的不由受信任的根授權單位簽署的憑證。

| 別名 | 無 |
| --- | --- |
| 必要？ |false |
| 位置 |已命名 |
| 預設值 |false |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

### <a name="vmpassword"></a>VMPassword
hello hello 虛擬機器帳戶的認證。 範例： VMPassword @{Name ="admin";密碼 ="password"}

| 別名 | 無 |
| --- | --- |
| 必要？ |false |
| 位置 |已命名 |
| 預設值 |無 |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

### <a name="databaseserverpassword"></a>DatabaseServerPassword
在 Azure 中的 hello SQL database 的 hello 認證。 範例： DatabaseServerPassword @{Name ="admin";密碼 ="password"}

| 別名 | 無 |
| --- | --- |
| 必要？ |false |
| 位置 |已命名 |
| 預設值 |無 |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

### <a name="sendhostmessagestooutput"></a>SendHostMessagesToOutput
如果為 true，列印訊息從 hello 指令碼 toohello 輸出資料流。

| 別名 | 無 |
| --- | --- |
| 必要？ |false |
| 位置 |已命名 |
| 預設值 |false |
| 接受管線輸入？ |false |
| 接受萬用字元？ |false |

## <a name="remarks"></a>備註
如需如何 toouse hello 指令碼 toocreate 開發人員和測試環境，請參閱完整說明[使用 Windows PowerShell 指令碼 tooPublish tooDev 和測試環境](vs-azure-tools-publishing-using-powershell-scripts.md)。

hello JSON 組態檔指定部署 toobe hello 的細節。 其中包括建立 hello 專案，例如 hello、 同質群組、 VHD 映像的名稱和大小 hello 虛擬機器時指定的 hello 資訊。 它也包括 hello hello 資料庫 tooprovision，hello 虛擬機器上的端點，如果有的話，，和 web 部署參數。 下列程式碼的 hello 顯示 JSON 組態檔範例：

```
{
    "environmentSettings": {
        "cloudService": {
            "name": "myvmname",
            "affinityGroup": "",
            "location": "West US",
            "virtualNetwork": "",
            "subnet": "",
            "availabilitySet": "",
            "virtualMachine": {
                "name": "myvmname",
                "vhdImage": "a699494373c04fc0bc8f2bb1389d6106__Windows-Server-2012-R2-201404.01-en.us-127GB.vhd",
                "size": "Small",
                "user": "vmuser1",
                "password": "",
                "enableWebDeployExtension": true,
                "endpoints": [
                    {
                        "name": "Http",
                        "protocol": "TCP",
                        "publicPort": "80",
                        "privatePort": "80"
                    },
                    {
                        "name": "Https",
                        "protocol": "TCP",
                        "publicPort": "443",
                        "privatePort": "443"
                    },
                    {
                        "name": "WebDeploy",
                        "protocol": "TCP",
                        "publicPort": "8172",
                        "privatePort": "8172"
                    },
                    {
                        "name": "Remote Desktop",
                        "protocol": "TCP",
                        "publicPort": "3389",
                        "privatePort": "3389"
                    },
                    {
                        "name": "Powershell",
                        "protocol": "TCP",
                        "publicPort": "5986",
                        "privatePort": "5986"
                    }
                ]
            }
        },
        "databases": [
            {
                "connectionStringName": "",
                "databaseName": "",
                "serverName": "",
                "user": "",
                "password": ""
            }
        ],
        "webDeployParameters": {
            "iisWebApplicationName": "Default Web Site"
        }
    }
}
```

您可以編輯 hello JSON 組態檔 toochange 要佈建。 虛擬機器和雲端服務是必要的但是 hello 資料庫區段為選擇性。

