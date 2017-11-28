---
title: "CLI 範例 - 建立 Azure SQL Database | Microsoft Docs"
description: "建立 SQL Database 的 Azure CLI 範例指令碼"
services: sql-database
documentationcenter: sql-database
author: janeng
manager: jstrauss
editor: carlrab
tags: azure-service-management
ms.assetid: 
ms.service: sql-database
ms.custom: DBs & servers
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: sql-database
ms.workload: database
ms.date: 06/23/2017
ms.author: janeng
ms.openlocfilehash: 908898ca691d2b53b9f54afa60c41e091163bd50
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="use-cli-to-create-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="d952d-103">使用 CLI 建立單一 Azure SQL Database 並設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="d952d-103">Use CLI to create a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="d952d-104">此 CLI 指令碼範例會建立 Azure SQL Database 並設定伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="d952d-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="d952d-105">成功執行指令碼後，即可從所有 Azure 服務和所設定的 IP 位址存取 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="d952d-105">Once the script has been successfully run, the SQL Database can be accessed from all Azure services and the configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="d952d-106">如果您選擇在本機安裝和使用 CLI，本主題會要求您執行 Azure CLI 2.0 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="d952d-106">If you choose to install and use the CLI locally, this topic requires that you are running the Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="d952d-107">執行 `az --version` 以尋找版本。</span><span class="sxs-lookup"><span data-stu-id="d952d-107">Run `az --version` to find the version.</span></span> <span data-ttu-id="d952d-108">如果您需要安裝或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="d952d-108">If you need to install or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="d952d-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="d952d-109">Sample script</span></span>

<span data-ttu-id="d952d-110">[!code-azurecli-interactive[主要](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "建立 SQL Database")]</span><span class="sxs-lookup"><span data-stu-id="d952d-110">[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]</span></span>

## <a name="clean-up-deployment"></a><span data-ttu-id="d952d-111">清除部署</span><span class="sxs-lookup"><span data-stu-id="d952d-111">Clean up deployment</span></span>

<span data-ttu-id="d952d-112">在執行過指令碼範例之後，您可以使用下列命令來移除資源群組和所有與其相關聯的資源。</span><span class="sxs-lookup"><span data-stu-id="d952d-112">After the script sample has been run, the following command can be used to remove the resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="d952d-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="d952d-113">Script explanation</span></span>

<span data-ttu-id="d952d-114">此指令碼會使用下列命令。</span><span class="sxs-lookup"><span data-stu-id="d952d-114">This script uses the following commands.</span></span> <span data-ttu-id="d952d-115">下表中的每個命令都會連結至命令特定的文件。</span><span class="sxs-lookup"><span data-stu-id="d952d-115">Each command in the table links to command specific documentation.</span></span>

| <span data-ttu-id="d952d-116">命令</span><span class="sxs-lookup"><span data-stu-id="d952d-116">Command</span></span> | <span data-ttu-id="d952d-117">注意事項</span><span class="sxs-lookup"><span data-stu-id="d952d-117">Notes</span></span> |
|---|---|
| [<span data-ttu-id="d952d-118">az group create</span><span class="sxs-lookup"><span data-stu-id="d952d-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="d952d-119">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="d952d-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="d952d-120">az sql server create</span><span class="sxs-lookup"><span data-stu-id="d952d-120">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="d952d-121">建立主控 SQL Database 的邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="d952d-121">Creates a logical server that hosts the SQL Database.</span></span> |
| [<span data-ttu-id="d952d-122">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="d952d-122">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="d952d-123">建立防火牆規則以允許從輸入的 IP 位址範圍存取伺服器上的所有 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="d952d-123">Creates a firewall rule to allow access to all SQL Databases on the server from the entered IP address range.</span></span> |
| [<span data-ttu-id="d952d-124">az sql db create</span><span class="sxs-lookup"><span data-stu-id="d952d-124">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="d952d-125">在邏輯伺服器中建立 SQL Database。</span><span class="sxs-lookup"><span data-stu-id="d952d-125">Creates the SQL Database in the logical server.</span></span> |
| [<span data-ttu-id="d952d-126">az group delete</span><span class="sxs-lookup"><span data-stu-id="d952d-126">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="d952d-127">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="d952d-127">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="d952d-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d952d-128">Next steps</span></span>

<span data-ttu-id="d952d-129">如需 Azure CLI 的詳細資訊，請參閱 [Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="d952d-129">For more information on the Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="d952d-130">其他的 SQL Database CLI 指令碼範例可於 [Azure SQL Database 文件](../sql-database-cli-samples.md)中找到。</span><span class="sxs-lookup"><span data-stu-id="d952d-130">Additional SQL Database CLI script samples can be found in the [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

