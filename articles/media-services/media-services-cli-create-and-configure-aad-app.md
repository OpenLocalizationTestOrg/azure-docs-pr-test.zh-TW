---
title: "aaaUse CLI 2.0 toocreate Azure AD 應用程式並將它設定為 Azure 媒體服務 API tooaccess |Microsoft 文件"
description: "本主題說明如何 toouse CLI 2.0 toocreate Azure AD 應用程式並將它設定 tooaccess Azure 媒體服務 API。"
services: media-services
documentationcenter: 
author: Juliako
manager: cfowler
editor: 
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/17/2017
ms.author: juliako
ms.openlocfilehash: c865e2701722374b5dd17b0e20fa848c07065006
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-20-toocreate-an-aad-app-and-configure-it-tooaccess-azure-media-services-api"></a><span data-ttu-id="695e3-103">使用 CLI 2.0 toocreate AAD 應用程式，並將它設定 tooaccess Azure 媒體服務 API</span><span class="sxs-lookup"><span data-stu-id="695e3-103">Use CLI 2.0 toocreate an AAD app and configure it tooaccess Azure Media Services API</span></span>

<span data-ttu-id="695e3-104">本主題說明您如何 toouse CLI 2.0 toocreate Azure Active Directory (Azure AD) 應用程式和服務主體 tooaccess Azure 媒體服務資源。</span><span class="sxs-lookup"><span data-stu-id="695e3-104">This topic shows you how toouse CLI 2.0 toocreate an Azure Active Directory (Azure AD) application and service principal tooaccess Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="695e3-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="695e3-105">Prerequisites</span></span>

- <span data-ttu-id="695e3-106">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="695e3-106">An Azure account.</span></span> <span data-ttu-id="695e3-107">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="695e3-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="695e3-108">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="695e3-108">A Media Services account.</span></span> <span data-ttu-id="695e3-109">如需詳細資訊，請參閱[建立 Azure 媒體服務帳戶使用 Azure 入口網站 hello](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="695e3-109">For more information, see [Create an Azure Media Services account using hello Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-hello-azure-cloud-shell"></a><span data-ttu-id="695e3-110">使用 Azure 雲端殼層 hello</span><span class="sxs-lookup"><span data-stu-id="695e3-110">Use hello Azure Cloud Shell</span></span>

1. <span data-ttu-id="695e3-111">登入 toohello [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="695e3-111">Sign in toohello [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="695e3-112">啟動 hello 雲端殼層從 hello 上方瀏覽 窗格中的 hello 入口網站。</span><span class="sxs-lookup"><span data-stu-id="695e3-112">Launch hello Cloud Shell from hello upper navigation pane of hello portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="695e3-114">如需詳細資訊，請參閱 [Azure Cloud Shell 概觀](../cloud-shell/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="695e3-114">For more information, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-toohello-media-account-with-cli-20"></a><span data-ttu-id="695e3-115">建立 Azure AD 應用程式並使用 CLI 2.0 設定存取 toohello 媒體帳戶</span><span class="sxs-lookup"><span data-stu-id="695e3-115">Create an Azure AD app and configure access toohello media account with CLI 2.0</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="695e3-116">例如：</span><span class="sxs-lookup"><span data-stu-id="695e3-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="695e3-117">在此範例中，hello**範圍**是 hello 完整資源路徑 hello media services 帳戶。</span><span class="sxs-lookup"><span data-stu-id="695e3-117">In this example, hello **scope** is hello full resource path for hello media services account.</span></span> <span data-ttu-id="695e3-118">不過，hello**範圍**可以是任何層級。</span><span class="sxs-lookup"><span data-stu-id="695e3-118">However, hello **scope** can be at any level.</span></span>

<span data-ttu-id="695e3-119">例如，它可以是 hello 的下列層級的其中一個：</span><span class="sxs-lookup"><span data-stu-id="695e3-119">For example, it could be one of hello following levels:</span></span>
 
* <span data-ttu-id="695e3-120">hello**訂用帳戶**層級。</span><span class="sxs-lookup"><span data-stu-id="695e3-120">hello **subscription** level.</span></span>
* <span data-ttu-id="695e3-121">hello**資源群組**層級。</span><span class="sxs-lookup"><span data-stu-id="695e3-121">hello **resource group** level.</span></span>
* <span data-ttu-id="695e3-122">hello**資源**層級 （例如，媒體帳戶）。</span><span class="sxs-lookup"><span data-stu-id="695e3-122">hello **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="695e3-123">如需詳細資訊，請參閱[使用 Azure CLI 2.0 建立 Azure 服務主體](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="695e3-123">For more information, see [Create an Azure service principal with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="695e3-124">另請參閱[Manage Role-Based 以 hello Azure 命令列介面的存取控制](../active-directory/role-based-access-control-manage-access-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="695e3-124">Also see [Manage Role-Based Access Control with hello Azure command-line interface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="695e3-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="695e3-125">Next steps</span></span>

<span data-ttu-id="695e3-126">開始使用[上傳檔案 tooyour 帳戶](media-services-portal-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="695e3-126">Get started with [uploading files tooyour account](media-services-portal-upload-files.md).</span></span>
