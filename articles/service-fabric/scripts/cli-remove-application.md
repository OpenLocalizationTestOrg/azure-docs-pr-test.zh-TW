---
title: "aaaAzure 服務網狀架構 CLI 指令碼中移除的範例"
description: "從使用 Azure Service Fabric CLI hello Azure Service Fabric 叢集中移除應用程式"
services: service-fabric
documentationcenter: 
author: thraka
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 08/22/2017
ms.author: adegeo
ms.custom: mvc
ms.openlocfilehash: 3ccefd4a04c5b7af71a2f959e11da6e402f25881
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>從 Service Fabric 叢集移除應用程式

這個範例指令碼執行的 Service Fabric 應用程式執行個體中刪除、 取消登錄的應用程式類型和從 hello 叢集的版本。  正在刪除 hello 應用程式執行個體也會刪除所有 hello 執行該應用程式相關聯的服務執行個體。 接下來，就會從 hello 映像存放區刪除 hello 應用程式檔案。 

如有需要安裝 hello[服務網狀架構 CLI](../service-fabric-cli.md)。

## <a name="sample-script"></a>範例指令碼

[!code-sh[main](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "Remove an application from a cluster")]

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 hello[服務網狀架構 CLI 文件](../service-fabric-cli.md)。

適用於 Azure Service Fabric 的其他服務網狀架構 CLI 範例可以在 hello[服務網狀架構 CLI 範例](../samples-cli.md)。
