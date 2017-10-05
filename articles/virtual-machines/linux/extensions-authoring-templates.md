---
title: "使用 Linux VM 擴充功能編寫範本 | Microsoft Docs"
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
ms.openlocfilehash: 8b017306474670bf8dde1440128e16ec35146f24
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="authoring-azure-resource-manager-templates-with-linux-vm-extensions"></a><span data-ttu-id="ca290-103">使用 Linux VM 擴充功能編寫 Azure Resource Manager 範本</span><span class="sxs-lookup"><span data-stu-id="ca290-103">Authoring Azure Resource Manager templates with Linux VM extensions</span></span>
[!INCLUDE [virtual-machines-common-extensions-authoring-templates](../../../includes/virtual-machines-common-extensions-authoring-templates.md)]

<span data-ttu-id="ca290-104">從 Azure CLI，執行下列命令︰</span><span class="sxs-lookup"><span data-stu-id="ca290-104">From Azure CLI, run the following commnad:</span></span>

      Azure VM extension list

<span data-ttu-id="ca290-105">此命令會傳回發行者名稱、擴充功能名稱和版本，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ca290-105">This command returns the publisher name, extension name and version as following:</span></span>

      Publisher                   : Microsoft.Azure.Extensions  
      ExtensionName               : DockerExtension
      Version                     : 1.0

<span data-ttu-id="ca290-106">這三個屬性分別對應至上述範本程式碼片段中的 "publisher"、"type" 和 "typeHandlerVersion"。</span><span class="sxs-lookup"><span data-stu-id="ca290-106">These three properties map to "publisher", "type", and "typeHandlerVersion" respectively in the above template snippet.</span></span>

> [!NOTE]
> <span data-ttu-id="ca290-107">建議一律使用最新的擴充功能版本，以取得最新的功能。</span><span class="sxs-lookup"><span data-stu-id="ca290-107">It's always recommended to use the latest extension version to get the most updated functionality.</span></span>
> 
> 

## <a name="identifying-the-schema-for-the-extension-configuration-parameters"></a><span data-ttu-id="ca290-108">識別擴充功能組態參數的結構描述</span><span class="sxs-lookup"><span data-stu-id="ca290-108">Identifying the schema for the extension configuration parameters</span></span>
<span data-ttu-id="ca290-109">編寫擴充功能範本的下一個步驟是識別用於提供組態參數的格式。</span><span class="sxs-lookup"><span data-stu-id="ca290-109">The next step with authoring an extension template is to identify the format for providing configuration parameters.</span></span> <span data-ttu-id="ca290-110">每個延伸模組都支援自己的參數集。</span><span class="sxs-lookup"><span data-stu-id="ca290-110">Each extension supports its own set of parameters.</span></span>

<span data-ttu-id="ca290-111">若要查看 Linux 擴充功能的範例組態，請按一下 [Linux 擴充功能範例](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json)文件。</span><span class="sxs-lookup"><span data-stu-id="ca290-111">To look at sample configurations for Linux extensions, click the documentation for see [Linux eExtensions samples](extensions-configuration-samples.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json).</span></span>

<span data-ttu-id="ca290-112">請參閱下列項目以取得 VM 擴充功能的完整範本。</span><span class="sxs-lookup"><span data-stu-id="ca290-112">Please refer to the following to get a fully complete template with VM Extensions.</span></span>

[<span data-ttu-id="ca290-113">Linux VM 上的自訂指令碼擴充功能。</span><span class="sxs-lookup"><span data-stu-id="ca290-113">Custom script extension on a Linux VM</span></span>](https://github.com/Azure/azure-quickstart-templates/blob/b1908e74259da56a92800cace97350af1f1fc32b/mongodb-on-ubuntu/azuredeploy.json/)

<span data-ttu-id="ca290-114">編寫範本之後，您可以使用 Azure CLI 部署它。</span><span class="sxs-lookup"><span data-stu-id="ca290-114">After authoring the template, you can deploy it using the Azure CLI.</span></span>

