---
title: "aaaAzure CLI 指令碼範例-將繫結的自訂 SSL 憑證 tooa web 應用程式 |Microsoft 文件"
description: "Azure CLI 指令碼範例-繫結的自訂 SSL 憑證 tooa web 應用程式"
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
ms.openlocfilehash: 2fec2db84a2007fa6b005776c84d4f8cba392b46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-web-app"></a><span data-ttu-id="4b4f9-103">繫結的自訂 SSL 憑證 tooa web 應用程式</span><span class="sxs-lookup"><span data-stu-id="4b4f9-103">Bind a custom SSL certificate tooa web app</span></span>

<span data-ttu-id="4b4f9-104">這個範例指令碼應用程式服務中建立 web 應用程式及其相關資源，然後將自訂網域名稱 tooit 的 hello SSL 憑證繫結。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-104">This sample script creates a web app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="4b4f9-105">針對此範例，您將需要：</span><span class="sxs-lookup"><span data-stu-id="4b4f9-105">For this sample, you will need:</span></span>

* <span data-ttu-id="4b4f9-106">存取 tooyour 網域註冊機構的 DNS 設定 頁面。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="4b4f9-107">有效。PFX 檔案並將其密碼的 hello SSL 憑證想 tooupload 並繫結。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="4b4f9-108">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-108">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="4b4f9-109">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-109">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="4b4f9-110">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-110">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 


## <a name="sample-script"></a><span data-ttu-id="4b4f9-111">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="4b4f9-111">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/app-service/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="4b4f9-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="4b4f9-112">Script explanation</span></span>

<span data-ttu-id="4b4f9-113">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-113">This script uses hello following commands.</span></span> <span data-ttu-id="4b4f9-114">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="4b4f9-115">命令</span><span class="sxs-lookup"><span data-stu-id="4b4f9-115">Command</span></span> | <span data-ttu-id="4b4f9-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="4b4f9-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="4b4f9-117">az group create</span><span class="sxs-lookup"><span data-stu-id="4b4f9-117">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="4b4f9-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="4b4f9-119">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="4b4f9-119">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="4b4f9-120">建立 App Service 方案。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-120">Creates an App Service plan.</span></span> |
| [<span data-ttu-id="4b4f9-121">az webapp create</span><span class="sxs-lookup"><span data-stu-id="4b4f9-121">az webapp create</span></span>](https://docs.microsoft.com/cli/azure/webapp#create) | <span data-ttu-id="4b4f9-122">建立 Azure Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-122">Creates an Azure web app.</span></span> |
| [<span data-ttu-id="4b4f9-123">az webapp config hostname add</span><span class="sxs-lookup"><span data-stu-id="4b4f9-123">az webapp config hostname add</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/hostname#add) | <span data-ttu-id="4b4f9-124">將自訂網域 tooa web 應用程式的對應。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-124">Maps a custom domain tooa web app.</span></span> |
| [<span data-ttu-id="4b4f9-125">az webapp config ssl upload</span><span class="sxs-lookup"><span data-stu-id="4b4f9-125">az webapp config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#upload) | <span data-ttu-id="4b4f9-126">上傳 SSL 憑證 tooa web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-126">Uploads an SSL certificate tooa web app.</span></span> |
| [<span data-ttu-id="4b4f9-127">az webapp config ssl bind</span><span class="sxs-lookup"><span data-stu-id="4b4f9-127">az webapp config ssl bind</span></span>](https://docs.microsoft.com/cli/azure/webapp/config/ssl#bind) | <span data-ttu-id="4b4f9-128">將繫結上傳的 SSL 憑證 tooa web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-128">Binds an uploaded SSL certificate tooa web app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="4b4f9-129">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4b4f9-129">Next steps</span></span>

<span data-ttu-id="4b4f9-130">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-130">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="4b4f9-131">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件](../app-service-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="4b4f9-131">Additional App Service CLI script samples can be found in hello [Azure App Service documentation](../app-service-cli-samples.md).</span></span>
