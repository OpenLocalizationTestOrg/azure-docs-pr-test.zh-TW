---
title: "使用 Linux VM 擴充功能的 aaaAuthoring 範本 |Microsoft 文件"
description: "了解如何使用 Linux VM 擴充功能編寫 Azure Resource Manager 範本"
services: virtual-machines-linux
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 322f8f0b-6697-4acb-b5f3-b3f58d28358b
ms.service: virtual-machines-linux
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: b797e442d8706956bbc06c5be611a2b0119055d3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a>使用 Linux VM 擴充功能編寫 Azure Resource Manager 範本
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

從 Azure CLI，執行下列達 hello:

      Azure VM extension list

此命令傳回 hello 發行者名稱、 延伸模組名稱和版本，如下所示：

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

這三個屬性對應太 「 發行者 」、 「 型別 」 和 「 typeHandlerVersion"，分別在 hello 上述範本程式碼片段。

> [!NOTE]
> 永遠是建議的 toouse hello 最新延伸模組版本 tooget hello 最更新功能。
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a>識別 hello hello 延伸模組組態參數的結構描述
hello 與撰寫擴充範本的下一個步驟是 tooidentify hello 格式提供組態參數。 每個延伸模組都支援自己的參數集。

在 Linux 延伸的範例組態 toolook 按一下 hello 文件集，請參閱[Linux eExtensions 範例](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)。

請參閱 toohello 遵循 tooget VM 擴充功能的全部完成範本。

[Linux VM 上的自訂指令碼擴充功能。](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

之後撰寫 hello 範本，您可以部署使用 Azure CLI hello。

