---
title: "aaa\"Azure CLI 指令碼-建立 Azure 的資料庫，PostgreSQL |Microsoft 文件 」"
description: "Azure CLI 指令碼範例 - 建立「適用於 PostgreSQL 的 Azure 資料庫」伺服器，並設定伺服器等級防火牆規則。"
services: postgresql
author: salonisonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.custom: mvc
ms.devlang: azure-cli
ms.topic: sample
ms.date: 05/31/2017
ms.openlocfilehash: bbe31f77283aa4a3bb36d1fd9171c280594a8267
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-database-for-postgresql-server-and-configure-a-firewall-rule-using-hello-azure-cli"></a><span data-ttu-id="41fdc-103">建立 Azure Database PostgreSQL 伺服器及設定使用 Azure CLI hello 的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="41fdc-103">Create an Azure Database for PostgreSQL server and configure a firewall rule using hello Azure CLI</span></span>
<span data-ttu-id="41fdc-104">此範例 CLI 指令碼會建立「適用於 PostgreSQL 的 Azure 資料庫」伺服器，並設定伺服器等級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="41fdc-104">This sample CLI script creates an Azure Database for PostgreSQL server and configures a server-level firewall rule.</span></span> <span data-ttu-id="41fdc-105">一旦 hello 指令碼順利執行之後，可以從所有 Azure 服務存取 hello PostgreSQL 伺服器，而且 hello 設定 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="41fdc-105">Once hello script has been successfully run, hello PostgreSQL server can be accessed from all Azure services and hello configured IP address.</span></span>

[!INCLUDE [cloud-shell-try-it](../../../includes/cloud-shell-try-it.md)]

<span data-ttu-id="41fdc-106">如果您選擇 tooinstall，並在本機上使用 hello CLI，本主題會需要您執行 hello Azure CLI 版本 2.0 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="41fdc-106">If you choose tooinstall and use hello CLI locally, this topic requires that you are running hello Azure CLI version 2.0 or later.</span></span> <span data-ttu-id="41fdc-107">執行`az --version`toofind hello 版本。</span><span class="sxs-lookup"><span data-stu-id="41fdc-107">Run `az --version` toofind hello version.</span></span> <span data-ttu-id="41fdc-108">如果您需要 tooinstall 或升級，請參閱[安裝 Azure CLI 2.0]( /cli/azure/install-azure-cli)。</span><span class="sxs-lookup"><span data-stu-id="41fdc-108">If you need tooinstall or upgrade, see [Install Azure CLI 2.0]( /cli/azure/install-azure-cli).</span></span> 

## <a name="sample-script"></a><span data-ttu-id="41fdc-109">範例指令碼</span><span class="sxs-lookup"><span data-stu-id="41fdc-109">Sample script</span></span>
<span data-ttu-id="41fdc-110">在這個範例指令碼中，編輯 hello 反白顯示線條 toocustomize hello 管理員使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="41fdc-110">In this sample script, edit hello highlighted lines toocustomize hello admin username and password.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/create-postgresql-server-and-firewall-rule.sh?highlight=15-16 "Create an Azure Database for PostgreSQL, and server-level firewall rule.")]

## <a name="clean-up-deployment"></a><span data-ttu-id="41fdc-111">清除部署</span><span class="sxs-lookup"><span data-stu-id="41fdc-111">Clean up deployment</span></span>
<span data-ttu-id="41fdc-112">Hello 指令碼範例執行後，下列命令的 hello 可以使用的 tooremove hello 資源群組和與其相關聯的所有資源。</span><span class="sxs-lookup"><span data-stu-id="41fdc-112">After hello script sample has been run, hello following command can be used tooremove hello resource group and all resources associated with it.</span></span>
[!code-azurecli-interactive[main](../../../cli_scripts/postgresql/create-postgresql-server-and-firewall-rule/delete-postgresql.sh "Delete hello resource group.")]

## <a name="script-explanation"></a><span data-ttu-id="41fdc-113">指令碼說明</span><span class="sxs-lookup"><span data-stu-id="41fdc-113">Script explanation</span></span>
<span data-ttu-id="41fdc-114">此指令碼會使用下列命令的 hello。</span><span class="sxs-lookup"><span data-stu-id="41fdc-114">This script uses hello following commands.</span></span> <span data-ttu-id="41fdc-115">Hello 資料表連結 toocommand 特定文件中的每個命令。</span><span class="sxs-lookup"><span data-stu-id="41fdc-115">Each command in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="41fdc-116">**命令**</span><span class="sxs-lookup"><span data-stu-id="41fdc-116">**Command**</span></span> | <span data-ttu-id="41fdc-117">**注意事項**</span><span class="sxs-lookup"><span data-stu-id="41fdc-117">**Notes**</span></span> |
|---|---|
| [<span data-ttu-id="41fdc-118">az group create</span><span class="sxs-lookup"><span data-stu-id="41fdc-118">az group create</span></span>](/cli/azure/group#create) | <span data-ttu-id="41fdc-119">建立用來存放所有資源的資源群組。</span><span class="sxs-lookup"><span data-stu-id="41fdc-119">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="41fdc-120">az postgres server create</span><span class="sxs-lookup"><span data-stu-id="41fdc-120">az postgres server create</span></span>](/cli/azure/postgres/server#create) | <span data-ttu-id="41fdc-121">建立 PostgreSQL 伺服器主控 hello 資料庫。</span><span class="sxs-lookup"><span data-stu-id="41fdc-121">Creates a PostgreSQL server that hosts hello databases.</span></span> |
| [<span data-ttu-id="41fdc-122">az postgres server firewall create</span><span class="sxs-lookup"><span data-stu-id="41fdc-122">az postgres server firewall create</span></span>](/cli/azure/postgres/server/firewall-rule#create) | <span data-ttu-id="41fdc-123">來自 hello 輸入 IP 位址範圍建立防火牆規則 tooallow 存取 toohello 伺服器和其下的資料庫。</span><span class="sxs-lookup"><span data-stu-id="41fdc-123">Creates a firewall rule tooallow access toohello server and databases under it from hello entered IP address range.</span></span> |
| [<span data-ttu-id="41fdc-124">az group delete</span><span class="sxs-lookup"><span data-stu-id="41fdc-124">az group delete</span></span>](/cli/azure/group#delete) | <span data-ttu-id="41fdc-125">刪除資源群組，包括所有的巢狀資源。</span><span class="sxs-lookup"><span data-stu-id="41fdc-125">Deletes a resource group including all nested resources.</span></span> |

## <a name="next-steps"></a><span data-ttu-id="41fdc-126">後續步驟</span><span class="sxs-lookup"><span data-stu-id="41fdc-126">Next steps</span></span>
- <span data-ttu-id="41fdc-127">閱讀更多有關 hello Azure CLI: [Azure CLI 文件](/cli/azure/overview)</span><span class="sxs-lookup"><span data-stu-id="41fdc-127">Read more information on hello Azure CLI: [Azure CLI documentation](/cli/azure/overview)</span></span>
- <span data-ttu-id="41fdc-128">嘗試其他指令碼：[「適用於 PostgreSQL 的 Azure 資料庫」的 Azure CLI 範例](../sample-scripts-azure-cli.md)</span><span class="sxs-lookup"><span data-stu-id="41fdc-128">Try additional scripts: [Azure CLI samples for Azure Database for PostgreSQL](../sample-scripts-azure-cli.md)</span></span>
