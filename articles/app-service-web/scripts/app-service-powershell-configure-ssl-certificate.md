---
title: "aaaAzure PowerShell 指令碼範例-將繫結的自訂 SSL 憑證 tooa web 應用程式 |Microsoft 文件"
description: "Azure PowerShell 指令碼範例-繫結的自訂 SSL 憑證 tooa web 應用程式"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: 23e83b74-614a-49a0-bc08-7542120eeec5
ms.service: app-service-web
ms.workload: web
ms.devlang: na
ms.topic: sample
ms.date: 03/20/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: 6e249ceedb9e2b8872dd0bc8b0aea0d718b28dab
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="17c5e-103">繫結的自訂 SSL 憑證 tooa web 應用程式</span><span class="sxs-lookup"><span data-stu-id="17c5e-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="17c5e-104">這個範例指令碼應用程式服務中建立 web 應用程式及其相關資源，然後將自訂網域名稱 tooit 的 hello SSL 憑證繫結。</span><span class="sxs-lookup"><span data-stu-id="17c5e-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> 

<span data-ttu-id="17c5e-105">如有需要安裝 Azure PowerShell 中使用 hello 指令位於 hello hello [Azure PowerShell 指南](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="17c5e-105">If needed, install hello Azure PowerShell using hello instruction found in hello [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="17c5e-106">此外，請確定：</span><span class="sxs-lookup"><span data-stu-id="17c5e-106">Also, ensure that:</span></span>

- <span data-ttu-id="17c5e-107">已建立與 Azure 的連線使用 hello`az login`命令。</span><span class="sxs-lookup"><span data-stu-id="17c5e-107">A connection with Azure has been created using hello `az login` command.</span></span>
- <span data-ttu-id="17c5e-108">您必須存取 tooyour 網域註冊機構的 DNS 設定 頁面。</span><span class="sxs-lookup"><span data-stu-id="17c5e-108">You have access tooyour domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="17c5e-109">您必須是有效的。PFX 檔案並將其密碼的 hello SSL 憑證想 tooupload 並繫結。</span><span class="sxs-lookup"><span data-stu-id="17c5e-109">You have a valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="17c5e-110">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="17c5e-110">Sample script</span></span>

[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate tooa web app")]

## <a name="clean-up-deployment"></a><span data-ttu-id="17c5e-111">清除部署</span><span class="sxs-lookup"><span data-stu-id="17c5e-111">Clean up deployment</span></span> 

<span data-ttu-id="17c5e-112">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組、 web 應用程式和所有相關的資源。</span><span class="sxs-lookup"><span data-stu-id="17c5e-112">After hello script sample has been run, hello following command can be used tooremove hello resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="17c5e-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="17c5e-113">Script explanation</span></span>

<span data-ttu-id="17c5e-114">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="17c5e-114">This script uses hello following commands.</span></span> <span data-ttu-id="17c5e-115">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="17c5e-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="17c5e-116">命令</span><span class="sxs-lookup"><span data-stu-id="17c5e-116">Command</span></span> | <span data-ttu-id="17c5e-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="17c5e-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="17c5e-118">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="17c5e-118">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="17c5e-119">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="17c5e-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="17c5e-120">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="17c5e-120">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="17c5e-121">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="17c5e-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="17c5e-122">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="17c5e-122">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="17c5e-123">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="17c5e-123">Creates a web app.</span></span> |
| [<span data-ttu-id="17c5e-124">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="17c5e-124">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="17c5e-125">修改應用程式服務計劃 toochange 其定價層。</span><span class="sxs-lookup"><span data-stu-id="17c5e-125">Modifies an App Service plan toochange its pricing tier.</span></span> |
| [<span data-ttu-id="17c5e-126">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="17c5e-126">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="17c5e-127">修改 Web 應用程式的組態。</span><span class="sxs-lookup"><span data-stu-id="17c5e-127">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="17c5e-128">New-AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="17c5e-128">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="17c5e-129">建立 Web 應用程式的 SSL 憑證繫結。</span><span class="sxs-lookup"><span data-stu-id="17c5e-129">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="17c5e-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="17c5e-130">Next steps</span></span>

<span data-ttu-id="17c5e-131">如需有關 hello Azure PowerShell 模組的詳細資訊，請參閱[Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="17c5e-131">For more information on hello Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="17c5e-132">Azure App Service Web 應用程式的其他 Azure Powershell 範例可以在 hello [Azure PowerShell 範例](../app-service-powershell-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="17c5e-132">Additional Azure Powershell samples for Azure App Service Web Apps can be found in hello [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
