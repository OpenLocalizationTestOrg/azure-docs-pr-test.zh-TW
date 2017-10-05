---
title: "使用 CLI 2.0 建立 Azure AD 應用程式，並設定它以存取 Azure 媒體服務 API | Microsoft Docs"
description: "本主題示範如何使用 CLI 2.0 建立 Azure AD 應用程式，並設定它以存取 Azure 媒體服務 API。"
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
ms.openlocfilehash: 01a2bb6d99776feec936315bc882c3097ce832d4
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="use-cli-20-to-create-an-aad-app-and-configure-it-to-access-azure-media-services-api"></a><span data-ttu-id="63137-103">使用 CLI 2.0 建立 AAD 應用程式，並設定它以存取 Azure 媒體服務 API</span><span class="sxs-lookup"><span data-stu-id="63137-103">Use CLI 2.0 to create an AAD app and configure it to access Azure Media Services API</span></span>

<span data-ttu-id="63137-104">本主題示範如何使用 CLI 2.0 建立 Azure Active Directory (Azure AD) 應用程式和服務主體，以存取 Azure 媒體服務資源。</span><span class="sxs-lookup"><span data-stu-id="63137-104">This topic shows you how to use CLI 2.0 to create an Azure Active Directory (Azure AD) application and service principal to access Azure Media Services resources.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="63137-105">必要條件</span><span class="sxs-lookup"><span data-stu-id="63137-105">Prerequisites</span></span>

- <span data-ttu-id="63137-106">一個 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="63137-106">An Azure account.</span></span> <span data-ttu-id="63137-107">如需詳細資訊，請參閱 [Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/)。</span><span class="sxs-lookup"><span data-stu-id="63137-107">For details, see [Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span> 
- <span data-ttu-id="63137-108">媒體服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="63137-108">A Media Services account.</span></span> <span data-ttu-id="63137-109">如需詳細資訊，請參閱[使用 Azure 入口網站建立 Azure 媒體服務帳戶](media-services-portal-create-account.md)。</span><span class="sxs-lookup"><span data-stu-id="63137-109">For more information, see [Create an Azure Media Services account using the Azure portal](media-services-portal-create-account.md).</span></span>

## <a name="use-the-azure-cloud-shell"></a><span data-ttu-id="63137-110">使用 Azure Cloud Shell</span><span class="sxs-lookup"><span data-stu-id="63137-110">Use the Azure Cloud Shell</span></span>

1. <span data-ttu-id="63137-111">登入 [Azure 入口網站](https://portal.azure.com/)。</span><span class="sxs-lookup"><span data-stu-id="63137-111">Sign in to the [Azure portal](https://portal.azure.com/).</span></span>
2. <span data-ttu-id="63137-112">從入口網站上方的瀏覽窗格啟動 Cloud Shell。</span><span class="sxs-lookup"><span data-stu-id="63137-112">Launch the Cloud Shell from the upper navigation pane of the portal.</span></span>

    ![Cloud Shell](./media/media-services-cli-create-and-configure-aad-app/media-services-cli-create-and-configure-aad-app01.png) 

<span data-ttu-id="63137-114">如需詳細資訊，請參閱 [Azure Cloud Shell 概觀](../cloud-shell/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="63137-114">For more information, see [Overview of Azure Cloud Shell](../cloud-shell/overview.md).</span></span>

## <a name="create-an-azure-ad-app-and-configure-access-to-the-media-account-with-cli-20"></a><span data-ttu-id="63137-115">建立 Azure AD 應用程式，並使用 CLI 2.0 設定媒體帳戶的存取權</span><span class="sxs-lookup"><span data-stu-id="63137-115">Create an Azure AD app and configure access to the media account with CLI 2.0</span></span>
 
```azurecli
az login
az ad sp create-for-rbac --name <appName> --password <strong password>
az role assignment create -- assignee < user/app id> --role Contributor --scope <subscription/subscription id>
```

<span data-ttu-id="63137-116">例如：</span><span class="sxs-lookup"><span data-stu-id="63137-116">For example:</span></span>

```azurecli
az role assignment create --assignee a3e068fa-f739-44e5-ba4d-ad57866e25a1 --role Contributor --scope /subscriptions/0b65e280-7917-4874-9fed-1307f2615ea2/resourceGroups/Default-AzureBatch-SouthCentralUS/providers/microsoft.media/mediaservices/sbbash
```

<span data-ttu-id="63137-117">在此範例中，**scope** 是媒體服務帳戶的完整資源路徑。</span><span class="sxs-lookup"><span data-stu-id="63137-117">In this example, the **scope** is the full resource path for the media services account.</span></span> <span data-ttu-id="63137-118">不過，**scope** 可以是任何層級。</span><span class="sxs-lookup"><span data-stu-id="63137-118">However, the **scope** can be at any level.</span></span>

<span data-ttu-id="63137-119">例如，它可以是下列層級之一：</span><span class="sxs-lookup"><span data-stu-id="63137-119">For example, it could be one of the following levels:</span></span>
 
* <span data-ttu-id="63137-120">**訂用帳戶**層級。</span><span class="sxs-lookup"><span data-stu-id="63137-120">The **subscription** level.</span></span>
* <span data-ttu-id="63137-121">**資源群組**層級。</span><span class="sxs-lookup"><span data-stu-id="63137-121">The **resource group** level.</span></span>
* <span data-ttu-id="63137-122">**資源**層級 (例如，媒體帳戶)。</span><span class="sxs-lookup"><span data-stu-id="63137-122">The **resource** level (for example, a Media account).</span></span>

<span data-ttu-id="63137-123">如需詳細資訊，請參閱[使用 Azure CLI 2.0 建立 Azure 服務主體](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="63137-123">For more information, see [Create an Azure service principal with Azure CLI 2.0](https://docs.microsoft.com/cli/azure/create-an-azure-service-principal-azure-cli)</span></span>

<span data-ttu-id="63137-124">另請參閱[使用 Azure 命令列介面管理角色型存取控制](../active-directory/role-based-access-control-manage-access-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="63137-124">Also see [Manage Role-Based Access Control with the Azure command-line interface](../active-directory/role-based-access-control-manage-access-azure-cli.md).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="63137-125">後續步驟</span><span class="sxs-lookup"><span data-stu-id="63137-125">Next steps</span></span>

<span data-ttu-id="63137-126">開始使用[上傳檔案至您的帳戶](media-services-portal-upload-files.md)。</span><span class="sxs-lookup"><span data-stu-id="63137-126">Get started with [uploading files to your account](media-services-portal-upload-files.md).</span></span>
