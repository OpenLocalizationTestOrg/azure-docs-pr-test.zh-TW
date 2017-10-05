---
title: "使用 Windows VM 擴充功能編寫範本 | Microsoft Docs"
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
ms.openlocfilehash: 338668df33783d8ef62c6710f4d96ce805296fe5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-windows-vm-extensions"></a><span data-ttu-id="ae219-103">使用 Windows VM 擴充功能編寫 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="ae219-103">Authoring Azure Resource Manager templates with Windows VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="ae219-104">從 Azure PowerShell，執行下列 Azure PowerShell Cmdlet：</span><span class="sxs-lookup"><span data-stu-id="ae219-104">From Azure PowerShell, run the following Azure PowerShell cmdlet:</span></span>

      Get-AzureVMAvailableExtension


<span data-ttu-id="ae219-105">此 Cmdlet 會傳回發行者名稱、擴充功能名稱和版本，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ae219-105">This cmdlet returns the publisher name, extension name, and version as follows:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="ae219-106">這三個屬性分別對應至上述範本程式碼片段中的 "publisher"、"type" 和 "typeHandlerVersion"。</span><span class="sxs-lookup"><span data-stu-id="ae219-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="ae219-107">建議一律使用最新的擴充功能版本，以取得最新的功能。</span><span class="sxs-lookup"><span data-stu-id="ae219-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="ae219-108">識別擴充功能組態參數的結構描述</span><span class="sxs-lookup"><span data-stu-id="ae219-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="ae219-109">編寫擴充功能範本的下一個步驟是識別用於提供組態參數的格式。</span><span class="sxs-lookup"><span data-stu-id="ae219-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="ae219-110">每個延伸模組都支援自己的參數集。</span><span class="sxs-lookup"><span data-stu-id="ae219-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="ae219-111">若要查看 Windows 擴充功能的範例組態，請按一下 [Windows 擴充功能範例](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json)。</span><span class="sxs-lookup"><span data-stu-id="ae219-111">To look at sample configurations for Windows extensions, see [Windows extensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json).</span></span>

<span data-ttu-id="ae219-112">請參閱下列項目以取得 VM 擴充功能的完整範本。</span><span class="sxs-lookup"><span data-stu-id="ae219-112">Please refer to the following to get a fully complete template with VM extensions.</span></span>

[<span data-ttu-id="ae219-113">Windows VM 上的自訂指令碼延伸模組</span><span class="sxs-lookup"><span data-stu-id="ae219-113">Custom Script Extension on a Windows VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/201-list-storage-keys-windows-vm/azuredeploy.json/)

<span data-ttu-id="ae219-114">編寫範本之後，您可以使用 Azure PowerShell 部署它。</span><span class="sxs-lookup"><span data-stu-id="ae219-114">After authoring the template, you can deploy it using Azure PowerShell.</span></span>

