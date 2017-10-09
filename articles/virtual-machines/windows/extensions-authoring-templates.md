---
title: "aaaAuthoring 範本具有 Windows VM 擴充功能 |Microsoft 文件"
description: "了解如何使用 Windows VM 擴充功能編寫 Azure Resource Manager 範本"
services: virtual-machines-windows
documentationcenter: 
author: kundanap
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 418dd1f7-ded8-45ab-9a5a-a59d245e2555
ms.service: virtual-machines-windows
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 03/29/2016
ms.author: kundanap
ms.openlocfilehash: c5156cb3859f7ff86bebda942150d268e57d6486
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="c372f-103">使用 Windows VM 擴充功能編寫 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="c372f-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="c372f-104">從 Azure PowerShell，執行下列 Azure PowerShell cmdlet 的 hello:</span><span class="sxs-lookup"><span data-stu-id="c372f-104">From Azure PowerShell, run hello following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="c372f-105">這個指令程式傳回 hello 發行者名稱、 延伸模組名稱和版本，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c372f-105">This cmdlet returns hello publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="c372f-106">這三個屬性對應太 「 發行者 」、 「 型別 」 和 「 typeHandlerVersion"，分別在 hello 上述範本程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="c372f-106">These three properties map too"publisher", "type", and "typeHandlerVersion" respectively in hello above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="c372f-107">永遠是建議的 toouse hello 最新延伸模組版本 tooget hello 最更新功能。</span><span class="sxs-lookup"><span data-stu-id="c372f-107">It's always recommended toouse hello latest extension version tooget hello most updated functionality.</span></span>
> 
> 

## <a name="identifying-hello-schema-for-hello-extension-configuration-parameters"></a><span data-ttu-id="c372f-108">識別 hello hello 延伸模組組態參數的結構描述</span><span class="sxs-lookup"><span data-stu-id="c372f-108">Identifying hello schema for hello extension configuration parameters</span></span>
<span data-ttu-id="c372f-109">hello 與撰寫擴充範本的下一個步驟是 tooidentify hello 格式提供組態參數。</span><span class="sxs-lookup"><span data-stu-id="c372f-109">hello next step with authoring an extension template is tooidentify hello format for providing configuration parameters.</span></span> <span data-ttu-id="c372f-110">每個延伸模組都支援自己的參數集。</span><span class="sxs-lookup"><span data-stu-id="c372f-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="c372f-111">請參閱 < 在 Windows 擴充功能，如範例設定 toolook [Windows 擴充功能範例](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="c372f-111">toolook at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="c372f-112">請參閱 toohello 遵循 tooget VM 擴充功能的全部完成範本。</span><span class="sxs-lookup"><span data-stu-id="c372f-112">Please refer toohello following tooget a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="c372f-113">Windows VM 上的自訂指令碼延伸模組</span><span class="sxs-lookup"><span data-stu-id="c372f-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="c372f-114">之後撰寫 hello 範本，您可以部署它使用 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="c372f-114">After authoring hello template, you can deploy it using Azure PowerShell.</span></span>

