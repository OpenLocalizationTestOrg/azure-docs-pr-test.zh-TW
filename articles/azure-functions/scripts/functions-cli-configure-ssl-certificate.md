---
title: "aaaAzure CLI 指令碼範例-將繫結的自訂 SSL 憑證 tooa 函式應用程式 |Microsoft 文件"
description: "Azure CLI 指令碼範例-繫結的自訂 SSL 憑證 tooa 函式應用程式在 Azure 中"
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
ms.openlocfilehash: 692dbc03583f2978131823083f1bfd257882664c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="bind-a-custom-ssl-certificate-tooa-function-app"></a><span data-ttu-id="90f09-103">繫結的自訂 SSL 憑證 tooa 函式應用程式</span><span class="sxs-lookup"><span data-stu-id="90f09-103">Bind a custom SSL certificate tooa function app</span></span>

<span data-ttu-id="90f09-104">這個範例指令碼應用程式服務中建立函數應用程式及其相關資源，然後將自訂網域名稱 tooit 的 hello SSL 憑證繫結。</span><span class="sxs-lookup"><span data-stu-id="90f09-104">This sample script creates a function app in App Service with its related resources, then binds hello SSL certificate of a custom domain name tooit.</span></span> <span data-ttu-id="90f09-105">針對此範例，您需要：</span><span class="sxs-lookup"><span data-stu-id="90f09-105">For this sample, you need:</span></span>

* <span data-ttu-id="90f09-106">存取 tooyour 網域註冊機構的 DNS 設定 頁面。</span><span class="sxs-lookup"><span data-stu-id="90f09-106">Access tooyour domain registrar's DNS configuration page.</span></span>
* <span data-ttu-id="90f09-107">有效。PFX 檔案並將其密碼的 hello SSL 憑證想 tooupload 並繫結。</span><span class="sxs-lookup"><span data-stu-id="90f09-107">A valid .PFX file and its password for hello SSL certificate you want tooupload and bind.</span></span>

<span data-ttu-id="90f09-108">toobind SSL 憑證，必須建立函式應用程式，App Service 方案中，而不是在耗用量計劃。</span><span class="sxs-lookup"><span data-stu-id="90f09-108">toobind an SSL certificate, your function app must be created in an App Service plan and not in a consumption plan.</span></span>

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="90f09-109">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="90f09-109">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="90f09-110">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="90f09-110">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="90f09-111">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="90f09-111">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="90f09-112">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="90f09-112">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/azure-functions/configure-ssl-certificate/configure-ssl-certificate.sh?highlight=3-5 "Bind a custom SSL certificate tooa web app")]

[!INCLUDE [cli-script-clean-up](../../../includes/cli-script-clean-up.md)]

## <a name="script-explanation"></a><span data-ttu-id="90f09-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="90f09-113">Script explanation</span></span>

<span data-ttu-id="90f09-114">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="90f09-114">This script uses hello following commands.</span></span> <span data-ttu-id="90f09-115">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="90f09-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="90f09-116">命令</span><span class="sxs-lookup"><span data-stu-id="90f09-116">Command</span></span> | <span data-ttu-id="90f09-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="90f09-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="90f09-118">az group create</span><span class="sxs-lookup"><span data-stu-id="90f09-118">az group create</span></span>](https://docs.microsoft.com/cli/azure/group#create) | <span data-ttu-id="90f09-119">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="90f09-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="90f09-120">az appservice plan create</span><span class="sxs-lookup"><span data-stu-id="90f09-120">az appservice plan create</span></span>](https://docs.microsoft.com/cli/azure/appservice/plan#create) | <span data-ttu-id="90f09-121">建立應用程式服務計劃所需 toobind SSL 憑證。</span><span class="sxs-lookup"><span data-stu-id="90f09-121">Creates an App Service plan required toobind SSL certificates.</span></span> |
| [<span data-ttu-id="90f09-122">az functionapp create</span><span class="sxs-lookup"><span data-stu-id="90f09-122">az functionapp create</span></span>]() | <span data-ttu-id="90f09-123">建立函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="90f09-123">Creates a function app.</span></span> |
| [<span data-ttu-id="90f09-124">az appservice web config hostname add</span><span class="sxs-lookup"><span data-stu-id="90f09-124">az appservice web config hostname add</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/hostname#add) | <span data-ttu-id="90f09-125">將對應的自訂網域 toohello 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="90f09-125">Maps a custom domain toohello function app.</span></span> |
| [<span data-ttu-id="90f09-126">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="90f09-126">az appservice web config ssl upload</span></span>](https://docs.microsoft.com/cli/azure/appservice/web/config/ssl#upload) | <span data-ttu-id="90f09-127">上傳 SSL 憑證 tooa 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="90f09-127">Uploads an SSL certificate tooa function app.</span></span> |
| [<span data-ttu-id="90f09-128">az appservice web config ssl upload</span><span class="sxs-lookup"><span data-stu-id="90f09-128">az appservice web config ssl bind</span></span>](https://docs.microsoft.com/en-us/cli/azure/appservice/web/config/ssl#bind) | <span data-ttu-id="90f09-129">將繫結上傳的 SSL 憑證 tooa 函式應用程式。</span><span class="sxs-lookup"><span data-stu-id="90f09-129">Binds an uploaded SSL certificate tooa function app.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="90f09-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="90f09-130">Next steps</span></span>

<span data-ttu-id="90f09-131">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="90f09-131">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="90f09-132">其他應用程式服務 CLI 指令碼範例可以在 hello [Azure 應用程式服務文件]()。</span><span class="sxs-lookup"><span data-stu-id="90f09-132">Additional App Service CLI script samples can be found in hello [Azure App Service documentation]().</span></span>
