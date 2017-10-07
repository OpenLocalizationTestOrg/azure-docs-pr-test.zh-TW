---
title: "PowerShell 指令碼範例-aaaAzure 連接 web 應用程式 tooa 儲存體帳戶 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例-連接 web 應用程式 tooa 儲存體帳戶"
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
ms.openlocfilehash: 07693366d32fbaefe92c18df67ded81661e1a2df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-a-web-app-tooa-storage-account"></a><span data-ttu-id="07a6c-103">連接 web 應用程式 tooa 儲存體帳戶</span><span class="sxs-lookup"><span data-stu-id="07a6c-103">Connect a web app tooa storage account</span></span>

<span data-ttu-id="07a6c-104">在此案例中，您將學習如何 toocreate Azure 儲存體帳戶和 Azure web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="07a6c-104">In this scenario you will learn how toocreate an Azure storage account and an Azure web app.</span></span> <span data-ttu-id="07a6c-105">然後，您將連結 hello 儲存體帳戶 toohello web 應用程式使用應用程式設定。</span><span class="sxs-lookup"><span data-stu-id="07a6c-105">Then you will link hello storage account toohello web app using app settings.</span></span>

<span data-ttu-id="07a6c-106">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="07a6c-106">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="07a6c-107">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="07a6c-107">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/connect-to-storage/connect-to-storage.ps1 "Connect a web app tooa storage account")]

## <a name="clean-up-deployment"></a><span data-ttu-id="07a6c-108">清除部署</span><span class="sxs-lookup"><span data-stu-id="07a6c-108">Clean up deployment</span></span> 

<span data-ttu-id="07a6c-109">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 web 應用程式和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="07a6c-109">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="07a6c-110">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="07a6c-110">Script explanation</span></span>

<span data-ttu-id="07a6c-111">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="07a6c-111">This script uses hello following commands.</span></span> <span data-ttu-id="07a6c-112">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="07a6c-112">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="07a6c-113">命令</span><span class="sxs-lookup"><span data-stu-id="07a6c-113">Command</span></span> | <span data-ttu-id="07a6c-114">注意事項</span><span class="sxs-lookup"><span data-stu-id="07a6c-114">Notes</span></span> |
|---|---|
| [<span data-ttu-id="07a6c-115">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="07a6c-115">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="07a6c-116">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="07a6c-116">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="07a6c-117">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="07a6c-117">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="07a6c-118">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="07a6c-118">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="07a6c-119">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="07a6c-119">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="07a6c-120">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="07a6c-120">Creates a web app.</span></span> |
| [<span data-ttu-id="07a6c-121">New-AzureRMStorageAccount</span><span class="sxs-lookup"><span data-stu-id="07a6c-121">New-AzureRMStorageAccount</span></span>](/powershell/module/azurerm.storage/new-azurermstorageaccount) | <span data-ttu-id="07a6c-122">建立儲存體帳戶。</span><span class="sxs-lookup"><span data-stu-id="07a6c-122">Creates a Storage account.</span></span> |
| [<span data-ttu-id="07a6c-123">Get-AzureRMStorageAccountKey</span><span class="sxs-lookup"><span data-stu-id="07a6c-123">Get-AzureRMStorageAccountKey</span></span>](/powershell/module/azurerm.storage/get-azurermstorageaccountkey) | <span data-ttu-id="07a6c-124">取得 Azure 儲存體帳戶的 hello 便捷鍵。</span><span class="sxs-lookup"><span data-stu-id="07a6c-124">Gets hello access keys for an Azure Storage account.</span></span> |
| [<span data-ttu-id="07a6c-125">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="07a6c-125">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="07a6c-126">修改 Web 應用程式的組態。</span><span class="sxs-lookup"><span data-stu-id="07a6c-126">Modifies a web app's configuration.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="07a6c-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="07a6c-127">Next steps</span></span>

<span data-ttu-id="07a6c-128">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="07a6c-128">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="07a6c-129">Azure App Service Web 應用程式的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../app-service-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="07a6c-129">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
