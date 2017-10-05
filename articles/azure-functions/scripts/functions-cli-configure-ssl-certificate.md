---
title: "Azure CLI 指令碼範例 - 將自訂 SSL 憑證繫結至函式應用程式 | Microsoft Docs"
description: "Azure CLI 指令碼範例 - 在 Azure 中將自訂 SSL 憑證繫結至函式應用程式"
services: functions
documentationcenter: 
author: ggailey777
manager: erikre
editor: 
tags: azure-service-management
ms.assetid: eb95d350-81ea-4145-a1e2-6eea3b7469b2
ms.service: functions
ms.workload: na
ms.devlang: azurecli
ms.tgt_pltfrm: na
ms.topic: sample
ms.date: 04/10/2017
ms.author: glenga
ms.custom: mvc
ms.openlocfilehash: ddabb701d7d5615232d1f6163aa6fb166efe5cb0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="bind-a-custom-ssl-certificate-to-a-function-app"></a><span data-ttu-id="5bc30-103">將自訂 SSL 憑證繫結至函式應用程式</span><span class="sxs-lookup"><span data-stu-id="5bc30-103">Bind a custom SSL certificate to a function app</span></span>

<span data-ttu-id="5bc30-104">此範例指令碼會在 App Service 中建立函式應用程式及其相關資源，然後將自訂網域名稱的 SSL 憑證與其繫結。</span><span class="sxs-lookup"><span data-stu-id="5bc30-104">This sample script creates a function app in App Service with its related resources, then binds the SSL certificate of a custom domain name to it.</span></span> <span data-ttu-id="5bc30-105">針對此範例，您需要：</span><span class="sxs-lookup"><span data-stu-id="5bc30-105">For this sample, you need:</span></span>

* <span data-ttu-id="5bc30-106">存取網域註冊機構的 DNS 設定頁面。</span><span class="sxs-lookup"><span data-stu-id="5bc30-106">Access to your domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="5bc30-107">對於想要上傳並繫結的 SSL 憑證，您具備有效的 .PFX 檔案和其密碼。</span><span class="sxs-lookup"><span data-stu-id="5bc30-107">A valid .PFX file and its password for the SSL certificate you want to upload and bind.</span></span>

<span data-ttu-id="5bc30-108">若要繫結 SSL 憑證，必須在 App Service 方案中建立函式應用程式，而不是在取用方案中建立。</span><span class="sxs-lookup"><span data-stu-id="5bc30-108">To bind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="5bc30-109">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="5bc30-109">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="5bc30-110">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="5bc30-110">Run `az --version` to find the version.</span></span> <span data-ttu-id="5bc30-111">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="5bc30-111">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="5bc30-112">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="5bc30-112">Sample script</span></span>

<span data-ttu-id="5bc30-113">[!code-azurecli-interactive[主要](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "將自訂 SSL 憑證繫結至 Web 應用程式")]</span><span class="sxs-lookup"><span data-stu-id="5bc30-113">[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate to a web app")]</span></span>

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="5bc30-114">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="5bc30-114">Script explanation</span></span>

<span data-ttu-id="5bc30-115">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="5bc30-115">This script uses the following commands.</span></span> <span data-ttu-id="5bc30-116">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="5bc30-116">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="5bc30-117">命令</span><span class="sxs-lookup"><span data-stu-id="5bc30-117">Command</span></span> | <span data-ttu-id="5bc30-118">注意事項</span><span class="sxs-lookup"><span data-stu-id="5bc30-118">Notes</span></span> |
|---|---|
| [<span data-ttu-id="5bc30-119">az group create</span><span class="sxs-lookup"><span data-stu-id="5bc30-119">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="5bc30-120">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="5bc30-120">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="5bc30-121">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="5bc30-121">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="5bc30-122">建立繫結 SSL 憑證所需的 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="5bc30-122">Creates an App Service plan required to bind SSL certificates.</span></span> |
| [<span data-ttu-id="5bc30-123">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="5bc30-123">az functionapp create</span></span>]() | <span data-ttu-id="5bc30-124">建立函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bc30-124">Creates a function app.</span></span> |
| [<span data-ttu-id="5bc30-125">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="5bc30-125">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="5bc30-126">將自訂網域對應至函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bc30-126">Maps a custom domain to the function app.</span></span> |
| [<span data-ttu-id="5bc30-127">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="5bc30-127">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="5bc30-128">將 SSL 憑證上傳至函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bc30-128">Uploads an SSL certificate to a function app.</span></span> |
| [<span data-ttu-id="5bc30-129">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="5bc30-129">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="5bc30-130">將上傳的 SSL 憑證繫結至函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="5bc30-130">Binds an uploaded SSL certificate to a function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5bc30-131">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5bc30-131">Next steps</span></span>

<span data-ttu-id="5bc30-132">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="5bc30-132">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="5bc30-133">您可以在 [Azure App Service 文件]()中找到其他的 App Service CLI 指令碼範例。</span><span class="sxs-lookup"><span data-stu-id="5bc30-133">Additional App Service CLI script samples can be found in the [Azure App Service documentation]().</span></span>
