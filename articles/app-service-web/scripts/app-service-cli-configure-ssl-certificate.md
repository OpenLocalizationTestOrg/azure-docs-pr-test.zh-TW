---
title: "Azure CLI 指令碼範例 - 將自訂 SSL 憑證繫結至 Web 應用程式 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 將自訂 SSL 憑證繫結至 Web 應用程式"
services: app-service\web
documentationcenter: 
author: cephalin
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: app-service-web
ms.workload: web
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 06/19/2017
ms.author: cephalin
ms.custom: mvc
ms.openlocfilehash: d4fab3fb2c297bf5f498b63bee46692febb9180b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-web-app"></a><span data-ttu-id="6c59e-103">將自訂 SSL 憑證繫結至 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="6c59e-103">Bind a custom SSL certificate to a web app</span></span>

<span data-ttu-id="6c59e-104">此範例指令碼會在 App Service 中建立 Web 應用程式及其相關的資源，然後將自訂網域名稱的 SSL 憑證加以繫結。</span><span class="sxs-lookup"><span data-stu-id="6c59e-104">This sample script creates a web app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="6c59e-105">針對此範例，您將需要：</span><span class="sxs-lookup"><span data-stu-id="6c59e-105">For this sample, you will need:</span></span>

* <span data-ttu-id="6c59e-106">存取網域註冊機構的 DNS 設定頁面。</span><span class="sxs-lookup"><span data-stu-id="6c59e-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="6c59e-107">對於想要上傳並繫結的 SSL 憑證，您具備有效的 .PFX 檔案和其密碼。</span><span class="sxs-lookup"><span data-stu-id="6c59e-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="6c59e-108">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="6c59e-108">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="6c59e-109">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="6c59e-109">Run `az --version` to find the version.</span></span> <span data-ttu-id="6c59e-110">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="6c59e-110">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="6c59e-111">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="6c59e-111">Sample script</span></span>

<span data-ttu-id="6c59e-112">[!code-azurecli-interactive[主要](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "將自訂 SSL 憑證繫結至 Web 應用程式")]</span><span class="sxs-lookup"><span data-stu-id="6c59e-112">[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="6c59e-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="6c59e-113">Script explanation</span></span>

<span data-ttu-id="6c59e-114">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="6c59e-114">This script uses the following commands.</span></span> <span data-ttu-id="6c59e-115">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="6c59e-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="6c59e-116">命令</span><span class="sxs-lookup"><span data-stu-id="6c59e-116">Command</span></span> | <span data-ttu-id="6c59e-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="6c59e-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="6c59e-118">az group create</span><span class="sxs-lookup"><span data-stu-id="6c59e-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="6c59e-119">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="6c59e-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="6c59e-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="6c59e-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="6c59e-121">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="6c59e-121">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="6c59e-122">az webapp create</span><span class="sxs-lookup"><span data-stu-id="6c59e-122">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="6c59e-123">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c59e-123">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="6c59e-124">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="6c59e-124">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="6c59e-125">將自訂網域對應至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c59e-125">Maps a custom domain to a web app.</span></span> |
| [<span data-ttu-id="6c59e-126">az webapp config ssl upload</span><span class="sxs-lookup"><span data-stu-id="6c59e-126">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="6c59e-127">將 SSL 憑證上傳至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c59e-127">Uploads an SSL certificate to a web app.</span></span> |
| [<span data-ttu-id="6c59e-128">az webapp config ssl bind</span><span class="sxs-lookup"><span data-stu-id="6c59e-128">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="6c59e-129">將上傳的 SSL 憑證繫結至 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6c59e-129">Binds an uploaded SSL certificate to a web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="6c59e-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6c59e-130">Next steps</span></span>

<span data-ttu-id="6c59e-131">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="6c59e-131">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="6c59e-132">您可以在 [Azure App Service 文件](../app-service-cli-samples.md)中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="6c59e-132">Additional App Service CLI script samples can be found in the [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
