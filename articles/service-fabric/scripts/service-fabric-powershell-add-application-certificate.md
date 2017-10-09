---
title: "aaaAzure PowerShell 指令碼範例-新增應用程式憑證 tooa 叢集 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例-新增應用程式憑證 tooa Service Fabric 叢集。"
services: service-fabric
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-service-management
ms.assetid: 
ms.service: service-fabric
ms.workload: multiple
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: ryanwi
ms.custom: mvc
ms.openlocfilehash: aba62598e2e4775012f89b5070bef5e61aec64f6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-an-application-certificate-tooa-service-fabric-cluster"></a>新增應用程式憑證 tooa Service Fabric 叢集

這個範例指令碼 hello 指定 Azure 金鑰保存庫中建立的自我簽署的憑證，並將它安裝 tooall hello Service Fabric 叢集節點。 hello 憑證也會下載 tooa 本機資料夾。 hello hello 下載憑證名稱是 hello 與 hello hello 金鑰保存庫中的 hello 憑證名稱相同。 視需要自訂 hello 參數。

如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。 

## <a name="sample-script"></a>範例指令碼

[!code-powershell[main](../../../powershell_scripts/service-fabric/add-application-certificate/add-new-application-certificate.ps1 "Add an application certificate tooa cluster")]

## <a name="script-explanation"></a>指令碼說明

此指令碼會使用下列命令的 hello: hello 資料表中的每個命令連結 toocommand 特定文件。

| 命令 | 注意事項 |
|---|---|
| [Add-AzureRmServiceFabricApplicationCertificate](/powershell/module/azurerm.servicefabric/Add-AzureRmServiceFabricApplicationCertificate) | 加入新的應用程式憑證 toohello 虛擬機器規模集 hello 叢集構成。  |

## <a name="next-steps"></a>後續步驟

如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。

適用於 Azure Service Fabric 的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../service-fabric-powershell-samples.md)。
