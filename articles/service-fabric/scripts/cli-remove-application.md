---
title: "Azure Service Fabric CLI 指令碼移除範例"
description: "使用 Azure Service Fabric CLI 將應用程式從 Azure Service Fabric 叢集中移除"
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
ms.openlocfilehash: d86f195d2c37a71e476c5ba4eec040dd46931d23
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="remove-an-application-from-a-service-fabric-cluster"></a>從 Service Fabric 叢集移除應用程式

這個範例指令碼會刪除執行中的 Service Fabric 應用程式執行個體，並從叢集取消註冊應用程式類型和版本。  刪除應用程式執行個體也會刪除應用程式相關聯的所有執行中服務執行個體。 接下來，系統會從映像存放區刪除應用程式檔案。 

如有需要，請安裝[ Service Fabric SDK](../service-fabric-cli.md)。

## <a name="sample-script"></a>範例指令碼

[!code-sh[主要](../../../cli_scripts/service-fabric/remove-application/remove-application.sh "從叢集移除應用程式")]

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [Service Fabric CLI 文件](../service-fabric-cli.md)。

您可以在 [Service Fabric CLI 範例](../samples-cli.md)中找到適用於 Azure Service Fabric 的其他 Service Fabric CLI 範例。
