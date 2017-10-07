---
title: "以 Azure 堆疊中的 hello 命令列 aaaDeploy 範本 |Microsoft 文件"
description: "了解如何 toouse hello 跨平台命令列介面 (CLI) toodeploy 範本 tooAzure 堆疊。"
services: azure-stack
documentationcenter: 
author: heathl17
manager: byronr
editor: 
ms.assetid: 9584177f-4af3-4834-864d-930b09ae0995
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/10/2017
ms.author: helaw
ms.openlocfilehash: 6fa6b19ac94d3f020008d04ff07f1ce489aa3418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-templates-in-azure-stack-using-hello-command-line"></a>部署 Azure 堆疊使用 hello 命令列中的範本
使用 hello 命令列 toodeploy Azure Resource Manager 範本 toohello Azure 堆疊開發套件。 Azure 資源管理員範本部署和佈建您的應用程式在單一、 協調作業中的所有 hello 資源。

## <a name="before-you-begin"></a>開始之前
 - [安裝並連接](azure-stack-connect-cli.md)tooAzure 堆疊時會搭配 Azure CLI
 - 下載 hello 檔案*azuredeploy.json*和*azuredeploy.parameters.json*從 hello[建立儲存體帳戶範例範本](https://github.com/Azure/AzureStack-QuickStart-Templates/tree/master/101-create-storage-account)。
 
## <a name="deploy-template"></a>部署範本
瀏覽 toohello 資料夾，其中這些檔案已下載並執行下列命令 toodeploy hello 範本 hello:

    azure group create "cliRG" "local" –f azuredeploy.json –d "testDeploy" –e azuredeploy.parameters.json

此命令會將部署 hello 範本 toohello 資源群組**cliRG** hello Azure 堆疊 POC 的預設位置中。

## <a name="validate-template-deployment"></a>驗證範本部署
toosee 此資源群組和儲存體帳戶時，使用 hello 下列命令：

    azure group list

    azure storage account list

## <a name="next-steps"></a>後續步驟
[管理使用者權限](azure-stack-manage-permissions.md)

