---
title: "aaaCLI 範例建立 Azure SQL database |Microsoft 文件"
description: "Azure CLI 範例指令碼 toocreate SQL 資料庫"
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
ms.openlocfilehash: 0d54e284e19f16387813e24d7beb7ab048a39263
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-cli-toocreate-a-single-azure-sql-database-and-configure-a-firewall-rule"></a><span data-ttu-id="036fc-103">使用 CLI toocreate 單一 Azure SQL 資料庫並設定防火牆規則</span><span class="sxs-lookup"><span data-stu-id="036fc-103">Use CLI toocreate a single Azure SQL database and configure a firewall rule</span></span>

<span data-ttu-id="036fc-104">此 CLI 指令碼範例會建立 Azure SQL Database 並設定伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="036fc-104">This Azure CLI script example creates an Azure SQL database and configure a server-level firewall rule.</span></span> <span data-ttu-id="036fc-105">一旦 hello 指令碼順利執行之後，您可以從所有 Azure 服務存取 SQL Database 的 hello 與 hello 設定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="036fc-105">Once hello script has been successfully run, hello SQL Database can be accessed from all Azure services and hello configured IP address.</span></span> 

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

[!INCLUDE [cloud-shell-try-it.md](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="036fc-106">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="036fc-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="036fc-107">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="036fc-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="036fc-108">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="036fc-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="036fc-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="036fc-109">Sample script</span></span>

[!code-azurecli-interactive[main](../../../cli_scripts/sql-database/create-and-configure-database/create-and-configure-database.sh?highlight=9-10 "Create SQL Database")]

## <a name="clean-up-deployment"></a><span data-ttu-id="036fc-110">清除部署</span><span class="sxs-lookup"><span data-stu-id="036fc-110">Clean up deployment</span></span>

<span data-ttu-id="036fc-111">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="036fc-111">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="036fc-112">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="036fc-112">Script explanation</span></span>

<span data-ttu-id="036fc-113">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="036fc-113">This script uses hello following commands.</span></span> <span data-ttu-id="036fc-114">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="036fc-114">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="036fc-115">命令</span><span class="sxs-lookup"><span data-stu-id="036fc-115">Command</span></span> | <span data-ttu-id="036fc-116">注意事項</span><span class="sxs-lookup"><span data-stu-id="036fc-116">Notes</span></span> |
|---|---|
| [<span data-ttu-id="036fc-117">az group create</span><span class="sxs-lookup"><span data-stu-id="036fc-117">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="036fc-118">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="036fc-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="036fc-119">az sql server create</span><span class="sxs-lookup"><span data-stu-id="036fc-119">az sql server create</span></span>](/cli/azure/sql/server#create) | <span data-ttu-id="036fc-120">建立主機 hello SQL Database 邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="036fc-120">Creates a logical server that hosts hello SQL Database.</span></span> |
| [<span data-ttu-id="036fc-121">az sql server firewall create</span><span class="sxs-lookup"><span data-stu-id="036fc-121">az sql server firewall create</span></span>](/cli/azure/sql/server/firewall-rule#create) | <span data-ttu-id="036fc-122">Hello hello 輸入 IP 位址範圍內的伺服器上建立防火牆規則 tooallow 存取 tooall SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="036fc-122">Creates a firewall rule tooallow access tooall SQL Databases on hello server from hello entered IP address range.</span></span> |
| [<span data-ttu-id="036fc-123">az sql db create</span><span class="sxs-lookup"><span data-stu-id="036fc-123">az sql db create</span></span>](/cli/azure/sql/db#create) | <span data-ttu-id="036fc-124">建立 hello 邏輯伺服器中的 hello SQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="036fc-124">Creates hello SQL Database in hello logical server.</span></span> |
| [<span data-ttu-id="036fc-125">az group delete</span><span class="sxs-lookup"><span data-stu-id="036fc-125">az group delete</span></span>](/cli/azure/resource#delete) | <span data-ttu-id="036fc-126">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="036fc-126">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="036fc-127">後續步驟</span><span class="sxs-lookup"><span data-stu-id="036fc-127">Next steps</span></span>

<span data-ttu-id="036fc-128">如需有關 Azure CLI hello 的詳細資訊，請參閱[Azure CLI 文件](https://docs.microsoft.com/cli/azure/overview)。</span><span class="sxs-lookup"><span data-stu-id="036fc-128">For more information on hello Azure CLI, see [Azure CLI documentation](https://docs.microsoft.com/cli/azure/overview).</span></span>

<span data-ttu-id="036fc-129">其他的 SQL 資料庫 CLI 指令碼範例可以在 hello [Azure SQL Database 文件](../sql-database-cli-samples.md)。</span><span class="sxs-lookup"><span data-stu-id="036fc-129">Additional SQL Database CLI script samples can be found in hello [Azure SQL Database documentation](../sql-database-cli-samples.md).</span></span>

