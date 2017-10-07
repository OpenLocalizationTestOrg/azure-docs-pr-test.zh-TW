---
title: "aaaAzure 服務網狀架構 CLI 指令碼部署的範例"
description: "部署應用程式 tooan Azure Service Fabric 叢集使用 hello Azure Service Fabric CLI"
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
ms.openlocfilehash: aaec7042a4fd7ed32ad706cde70361f23d18fb48
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-application-tooa-service-fabric-cluster"></a>部署應用程式 tooa Service Fabric 叢集

這個範例指令碼複製應用程式封裝 tooa 叢集映像存放區、 hello 叢集中註冊 hello 應用程式類型和建立應用程式執行個體從 hello 應用程式類型。 在這個階段，還會建立所有預設的服務。

如有需要安裝 hello[服務網狀架構 CLI](../service-fabric-cli.md)。

## <a name="sample-script"></a>範例指令碼

[!code-sh[main](../../../cli_scripts/service-fabric/deploy-application/deploy-application.sh "Deploy an application tooa cluster")]

## <a name="clean-up-deployment"></a>清除部署

當完成時，hello[移除](cli-remove-application.md)指令碼可以使用的 tooremove hello 應用程式。 hello 移除指令碼刪除 hello 應用程式執行個體、 取消登錄 hello 應用程式類型，並刪除映像存放區中的 hello 應用程式套件。

## <a name="next-steps"></a>後續步驟

如需詳細資訊，請參閱 hello[服務網狀架構 CLI 文件](../service-fabric-cli.md)。

適用於 Azure Service Fabric 的其他服務網狀架構 CLI 範例可以在 hello[服務網狀架構 CLI 範例](../samples-cli.md)。
