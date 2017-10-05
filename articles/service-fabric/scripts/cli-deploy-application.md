---
title: "Azure Service Fabric CLI 指令碼部署範例"
description: "使用 Azure Service Fabric CLI 將應用程式部署至 Azure Service Fabric 叢集"
services: service-fabric
documentationcenter: 
author: Thraka
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
ms.openlocfilehash: c77ecfccdf7d3e34b0b3133e9c63810a04fb1132
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-application-to-a-service-fabric-cluster"></a>將應用程式部署到 Service Fabric 叢集

這個範例指令碼會將應用程式封裝複製到叢集映像存放區、在叢集中註冊應用程式類型，並從應用程式類型建立應用程式執行個體。 在這個階段，還會建立所有預設的服務。

如有需要，請安裝[ Service Fabric SDK](../service-fabric-cli.md)。

## <a name="sample-script"></a>範例指令碼

[!code-sh[主要](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "將應用程式部署到叢集")]

## <a name="clean-up-deployment"></a>清除部署

完成時，可以使用[移除](cli-remove-application.md)指令碼將應用程式移除。 移除指令碼會刪除應用程式執行個體、將應用程式類型取消登錄，並從映像存放區刪除應用程式套件。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 [Service Fabric CLI 文件](../service-fabric-cli.md)。

您可以在 [Service Fabric CLI 範例](../samples-cli.md)中找到適用於 Azure Service Fabric 的其他 Service Fabric CLI 範例。
