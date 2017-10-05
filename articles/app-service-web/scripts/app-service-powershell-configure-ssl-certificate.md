---
title: "Azure PowerShell 指令碼範例 - 將自訂 SSL 憑證繫結至 Web 應用程式 | Microsoft Docs"
description: "Azure PowerShell 指令碼範例 - 將自訂 SSL 憑證繫結至 Web 應用程式"
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
ms.openlocfilehash: de8deccadcd9571be75447a117888bf2b3f571a0
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/18/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="2bcaa-103">將自訂 SSL 憑證繫結至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="2bcaa-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="2bcaa-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關的資源，然後將自訂網域名稱的 SSL 憑證加以繫結。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> 

<span data-ttu-id="2bcaa-105">您可以視需要使用 [Azure PowerShell 指南 (英文)](/powershell/azure/overview) 中的指示來安裝 Azure PowerShell。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-105">If needed, install the Azure PowerShell using the instruction found in the [Azure PowerShell guide](/powershell/azure/overview).</span></span> <span data-ttu-id="2bcaa-106">此外，請確定：</span><span class="sxs-lookup"><span data-stu-id="2bcaa-106">Also, ensure that:</span></span>

- <span data-ttu-id="2bcaa-107">已使用 `az login` 命令建立與 Azure 的連線。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-107">A connection with Azure has been created using the `az login` command.</span></span>
- <span data-ttu-id="2bcaa-108">您可以存取網域註冊機構的 DNS 設定頁面。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-108">You have access to your domain registrar's DNS configuration page.</span></span>
- <span data-ttu-id="2bcaa-109">對於想要上傳並繫結的 SSL 憑證，您具備有效的 .PFX 檔案和其密碼。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-109">You have a valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

## <a name="sample-script"></a><span data-ttu-id="2bcaa-110">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="2bcaa-110">Sample script</span></span>

<span data-ttu-id="2bcaa-111">[!code-powershell[主要](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "將自訂 SSL 憑證繫結至 Web 應用程式")]</span><span class="sxs-lookup"><span data-stu-id="2bcaa-111">[!code-powershell[main](../../../powershell_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.ps1?highlight=1-3 "Bind a custom SSL certificate to a web app")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="2bcaa-112">清除部署</span><span class="sxs-lookup"><span data-stu-id="2bcaa-112">Clean up deployment</span></span> 

<span data-ttu-id="2bcaa-113">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組、Web 應用程式和所有相關資源。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-113">After the script sample has been run, the following command can be used to remove the resource group, web app, and all related resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup -Force
```

## <a name="script-explanation"></a><span data-ttu-id="2bcaa-114">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="2bcaa-114">Script explanation</span></span>

<span data-ttu-id="2bcaa-115">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-115">This script uses the following commands.</span></span> <span data-ttu-id="2bcaa-116">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="2bcaa-117">命令</span><span class="sxs-lookup"><span data-stu-id="2bcaa-117">Command</span></span> | <span data-ttu-id="2bcaa-118">注意事項</span><span class="sxs-lookup"><span data-stu-id="2bcaa-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="2bcaa-119">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="2bcaa-119">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="2bcaa-120">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="2bcaa-121">New-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="2bcaa-121">New-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/new-azurermappserviceplan) | <span data-ttu-id="2bcaa-122">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-122">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="2bcaa-123">New-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="2bcaa-123">New-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/new-azurermwebapp) | <span data-ttu-id="2bcaa-124">建立 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-124">Creates a web app.</span></span> |
| [<span data-ttu-id="2bcaa-125">Set-AzureRmAppServicePlan</span><span class="sxs-lookup"><span data-stu-id="2bcaa-125">Set-AzureRmAppServicePlan</span></span>](/powershell/module/azurerm.websites/set-azurermappserviceplan) | <span data-ttu-id="2bcaa-126">修改 App Service 方案來變更其定價層。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-126">Modifies an App Service plan to change its pricing tier.</span></span> |
| [<span data-ttu-id="2bcaa-127">Set-AzureRmWebApp</span><span class="sxs-lookup"><span data-stu-id="2bcaa-127">Set-AzureRmWebApp</span></span>](/powershell/module/azurerm.websites/set-azurermwebapp) | <span data-ttu-id="2bcaa-128">修改 Web 應用程式的組態。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-128">Modifies a web app's configuration.</span></span> |
| [<span data-ttu-id="2bcaa-129">New-AzureRmWebAppSSLBinding</span><span class="sxs-lookup"><span data-stu-id="2bcaa-129">New-AzureRmWebAppSSLBinding</span></span>](/powershell/module/azurerm.websites/new-azurermwebappsslbinding) | <span data-ttu-id="2bcaa-130">建立 Web 應用程式的 SSL 憑證繫結。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-130">Creates an SSL certificate binding for a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2bcaa-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="2bcaa-131">Next steps</span></span>

<span data-ttu-id="2bcaa-132">如需有關 Azure PowerShell 模組的詳細資訊，請參閱 [Azure PowerShell 文件](/powershell/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-132">For more information on the Azure PowerShell module, see [Azure PowerShell documentation](/powershell/azure/overview).</span></span>

<span data-ttu-id="2bcaa-133">您可以在 [Azure PowerShell 範例](../app-service-powershell-samples.md)中找到適用於 App Service Web Apps 的其他 Azure PowerShell 範例。</span><span class="sxs-lookup"><span data-stu-id="2bcaa-133">Additional Azure Powershell samples for Azure App Service Web Apps can be found in the [Azure PowerShell samples](../app-service-powershell-samples.md).</span></span>
