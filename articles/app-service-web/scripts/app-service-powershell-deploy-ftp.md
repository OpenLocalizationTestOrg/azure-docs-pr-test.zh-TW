---
title: "PowerShell 指令碼範例上傳檔案 tooa web 應用程式使用 FTP aaaAzure |Microsoft 文件"
description: "Azure PowerShell 指令碼範例-上傳檔案 tooa web 應用程式使用 FTP"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: b7d46d6f-44fd-454c-8008-87dab6eefbc1
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 32a0a529e94c1315cc6730faf23fca2693c50ffb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="upload-files-tooa-web-app-using-ftp"></a><span data-ttu-id="adae1-103">上傳檔案 tooa web 應用程式使用 FTP</span><span class="sxs-lookup"><span data-stu-id="adae1-103">Upload files tooa web app using FTP</span></span>

<span data-ttu-id="adae1-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關資源，然後使用 FTP 部署您的 Web 應用程式程式碼 (透過 [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx))。</span><span class="sxs-lookup"><span data-stu-id="adae1-104">This sample script creates a web app in App Service with its related resources, and then deploys your web app code using FTP (via [WebClient.UploadFile()](https://msdn.microsoft.com/library/ms144229.aspx)).</span></span>

<span data-ttu-id="adae1-105">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)，然後執行`Login-AzureRmAccount`toocreate 與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="adae1-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview), and then run `Login-AzureRmAccount` toocreate a connection with Azure.</span></span>

## <a name="sample-script"></a><span data-ttu-id="adae1-106">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="adae1-106">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/deploy-ftp/deploy-ftp.ps1?highlight=1 "Upload files tooa web app using FTP")]

## <a name="clean-up-deployment"></a><span data-ttu-id="adae1-107">清除部署</span><span class="sxs-lookup"><span data-stu-id="adae1-107">Clean up deployment</span></span> 

<span data-ttu-id="adae1-108">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 web 應用程式和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="adae1-108">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name $webappname -Force
```

## <a name="script-explanation"></a><span data-ttu-id="adae1-109">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="adae1-109">Script explanation</span></span>

<span data-ttu-id="adae1-110">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="adae1-110">This script uses hello following commands.</span></span> <span data-ttu-id="adae1-111">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="adae1-111">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="adae1-112">命令</span><span class="sxs-lookup"><span data-stu-id="adae1-112">Command</span></span> | <span data-ttu-id="adae1-113">注意事項</span><span class="sxs-lookup"><span data-stu-id="adae1-113">Notes</span></span> |
|---|---|
| [<span data-ttu-id="adae1-114">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="adae1-114">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="adae1-115">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="adae1-115">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="adae1-116">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="adae1-116">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="adae1-117">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="adae1-117">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="adae1-118">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="adae1-118">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="adae1-119">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="adae1-119">Creates a web app.</span></span> |
| [<span data-ttu-id="adae1-120">Get-AzureRmWebAppPublishingProfile</span><span class="sxs-lookup"><span data-stu-id="adae1-120">Get-AzureRmWebAppPublishingProfile</span></span>](/powershell/module/azurerm.websites/get-azurermwebapppublishingprofile) | <span data-ttu-id="adae1-121">取得 Web 應用程式的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="adae1-121">Get a web app's publishing profile.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="adae1-122">後續步驟</span><span class="sxs-lookup"><span data-stu-id="adae1-122">Next steps</span></span>

<span data-ttu-id="adae1-123">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="adae1-123">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="adae1-124">Azure App Service Web 應用程式的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../app-service-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="adae1-124">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
