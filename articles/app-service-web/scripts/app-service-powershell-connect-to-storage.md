---
title: "Azure PowerShell 指令碼範例 - 將 Web 應用程式連線至儲存體帳戶 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 將 Web 應用程式連線至儲存體帳戶"
services: app-service\web
documentationcenter: 
author: syntaxc4
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: e4831bdc-2068-4883-9474-0b34c2e3e255
ms.service: app-service
ms.devlang: multiple
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: web
ms.date: 03/20/2017
ms.author: cfowler
ms.custom: mvc
ms.openlocfilehash: 481f3efdb1cbbeba328183da7e320c7e5b819b3a
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="connect-a-web-app-to-a-storage-account"></a><span data-ttu-id="58121-103">將 Web 應用程式連接至儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="58121-103">Connect a web app to a storage account</span></span>

<span data-ttu-id="58121-104">在此案例中，您會學習如何建立 Azure 儲存體帳戶和 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58121-104">In this scenario you will learn how to create an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="58121-105">然後，您會使用應用程式設定將儲存體帳戶連結到 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58121-105">Then you will link the storage account to the web app using app settings.</span></span>

<span data-ttu-id="58121-106">您可以視需要使用 [Azure PowerShell 指南 (英文)](/powershell/azure/overview) 中的指示來安裝 Azure PowerShell，然後執行 `Login-AzureRmAccount` 來建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="58121-106">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` to create a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="58121-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="58121-107">Sample script</span></span>

<span data-ttu-id="58121-108">[!code-powershell[主要](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "將 Web 應用程式連線至儲存體帳戶")]</span><span class="sxs-lookup"><span data-stu-id="58121-108">[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app to a storage account")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="58121-109">清除部署</span><span class="sxs-lookup"><span data-stu-id="58121-109">Clean up deployment</span></span> 

<span data-ttu-id="58121-110">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、Web 應用程式和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="58121-110">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="58121-111">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="58121-111">Script explanation</span></span>

<span data-ttu-id="58121-112">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="58121-112">This script uses the following commands.</span></span> <span data-ttu-id="58121-113">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="58121-113">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="58121-114">命令</span><span class="sxs-lookup"><span data-stu-id="58121-114">Command</span></span> | <span data-ttu-id="58121-115">注意事項</span><span class="sxs-lookup"><span data-stu-id="58121-115">Notes</span></span> |
|---|---|
| [<span data-ttu-id="58121-116">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="58121-116">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="58121-117">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="58121-117">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="58121-118">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="58121-118">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="58121-119">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="58121-119">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="58121-120">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="58121-120">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="58121-121">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58121-121">Creates a web app.</span></span> |
| [<span data-ttu-id="58121-122">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="58121-122">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="58121-123">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="58121-123">Creates a Storage account.</span></span> |
| [<span data-ttu-id="58121-124">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="58121-124">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="58121-125">取得 Azure 儲存體帳戶的存取金鑰。</span><span class="sxs-lookup"><span data-stu-id="58121-125">Gets the access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="58121-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="58121-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="58121-127">修改 Web 應用程式的組態。</span><span class="sxs-lookup"><span data-stu-id="58121-127">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="58121-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="58121-128">Next steps</span></span>

<span data-ttu-id="58121-129">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="58121-129">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="58121-130">您可以在 [Azure PowerShell 範例](../app-service-powershell-samples.md)中找到適用於 App Service Web Apps 的其他 Azure PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="58121-130">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
