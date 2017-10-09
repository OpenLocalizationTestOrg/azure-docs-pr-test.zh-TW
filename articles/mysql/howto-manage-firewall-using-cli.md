---
title: "aaaCreate 和管理 Azure 資料庫的 MySQL 防火牆規則，使用 Azure CLI |Microsoft 文件"
description: "本文說明如何 toocreate 和 MySQL 防火牆規則，使用 Azure CLI 命令列管理 Azure 資料庫。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: b2f0b4ccf34ce88e3a5e72a64d3f8c78a5bc2a54
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="02a4c-103">使用 Azure CLI 建立和管理適用於 MySQL 的 Azure 資料庫防火牆規則</span><span class="sxs-lookup"><span data-stu-id="02a4c-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="02a4c-104">伺服器層級防火牆規則可讓系統管理員 toomanage 存取 tooan Azure 資料庫的 MySQL 伺服器從特定的 IP 位址或 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="02a4c-104">Server-level firewall rules enable administrators toomanage access tooan Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="02a4c-105">您可以使用方便 Azure CLI 命令，來建立、 更新、 刪除、 清單，並顯示您的伺服器防火牆規則 toomanage。</span><span class="sxs-lookup"><span data-stu-id="02a4c-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules toomanage your server.</span></span> <span data-ttu-id="02a4c-106">如需「適用於 MySQL 的 Azure 資料庫」防火牆的概觀，請參閱[適用於 MySQL 的 Azure 資料庫伺服器防火牆規則](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="02a4c-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="02a4c-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="02a4c-107">Prerequisites</span></span>
* [<span data-ttu-id="02a4c-108">安裝 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="02a4c-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="02a4c-109">安裝適用於 PostgreSQL 和 MySQL 服務的 Azure Python SDK</span><span class="sxs-lookup"><span data-stu-id="02a4c-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="02a4c-110">安裝 PostgreSQL 和 MySQL 服務的 hello Azure CLI 元件</span><span class="sxs-lookup"><span data-stu-id="02a4c-110">Install hello Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="02a4c-111">建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="02a4c-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="02a4c-112">防火牆規則的命令︰</span><span class="sxs-lookup"><span data-stu-id="02a4c-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="02a4c-113">hello **az mysql 伺服器防火牆規則**命令用來從 Azure CLI toocreate、 刪除、 清單、 顯示，並更新防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="02a4c-113">hello **az mysql server firewall-rule** command is used from Azure CLI toocreate, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="02a4c-114">命令：</span><span class="sxs-lookup"><span data-stu-id="02a4c-114">Commands:</span></span>
- <span data-ttu-id="02a4c-115">**create**︰建立 Azure MySQL 伺服器防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="02a4c-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="02a4c-116">**delete**︰刪除 Azure MySQL 伺服器防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="02a4c-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="02a4c-117">**清單**: hello Azure MySQL 伺服器防火牆規則的清單。</span><span class="sxs-lookup"><span data-stu-id="02a4c-117">**list** : List hello Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="02a4c-118">**顯示**： 顯示 hello 詳細資料，Azure MySQL 伺服器的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="02a4c-118">**show** : Show hello details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="02a4c-119">**update**：更新 Azure MySQL 伺服器防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="02a4c-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-tooazure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="02a4c-120">登入 tooAzure 和清單 Azure 資料庫的 MySQL 伺服器</span><span class="sxs-lookup"><span data-stu-id="02a4c-120">Login tooAzure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="02a4c-121">安全地連線 Azure CLI 與 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="02a4c-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="02a4c-122">使用 hello **az 登入**toodo 這樣的命令。</span><span class="sxs-lookup"><span data-stu-id="02a4c-122">Use hello **az login** command toodo this.</span></span>

1. <span data-ttu-id="02a4c-123">執行 hello hello 命令列中的下列命令。</span><span class="sxs-lookup"><span data-stu-id="02a4c-123">Run hello following command from hello command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="02a4c-124">此命令會輸出的程式碼 toouse hello 下一個步驟中。</span><span class="sxs-lookup"><span data-stu-id="02a4c-124">This command will output a code toouse in hello next step.</span></span>

2. <span data-ttu-id="02a4c-125">使用網頁瀏覽器 tooopen hello 頁面[https://aka.ms/devicelogin](https://aka.ms/devicelogin)輸入 hello 程式碼。</span><span class="sxs-lookup"><span data-stu-id="02a4c-125">Use a web browser tooopen hello page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter hello code.</span></span>

3. <span data-ttu-id="02a4c-126">在 hello 提示字元中使用登入您的 Azure 認證。</span><span class="sxs-lookup"><span data-stu-id="02a4c-126">At hello prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="02a4c-127">一旦您的登入已獲得授權，將會列印 hello 主控台的訂閱清單。</span><span class="sxs-lookup"><span data-stu-id="02a4c-127">Once your login is authorized, a list of subscriptions will be printed in hello console.</span></span> <span data-ttu-id="02a4c-128">複製 hello 識別碼 hello 的所需的訂用帳戶 tooset hello 目前訂用帳戶 toobe 使用向前移動。</span><span class="sxs-lookup"><span data-stu-id="02a4c-128">Copy hello id of hello desired subscription tooset hello current subscription toobe used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="02a4c-129">如果您不確定的 hello 名稱，清單為您的訂用帳戶和資源群組的 MySQL 伺服器 hello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="02a4c-129">List hello Azure Databases for MySQL servers for your subscription and resource group if you are unsure of hello names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="02a4c-130">請注意 hello 中的 name 屬性，藉以 hello 會使用的 toospecify 上的 MySQL server toowork。</span><span class="sxs-lookup"><span data-stu-id="02a4c-130">Note hello name attribute in hello listing, which will be used toospecify which MySQL server toowork on.</span></span> <span data-ttu-id="02a4c-131">如果需要請確認該伺服器 toousing hello 屬性 tooconfirm 名稱是正確的 hello 詳細資料：</span><span class="sxs-lookup"><span data-stu-id="02a4c-131">If needed, confirm hello details for that server toousing hello name attribute tooconfirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="02a4c-132">在「適用於 MySQL 的 Azure 資料庫」伺服器上列出防火牆規則</span><span class="sxs-lookup"><span data-stu-id="02a4c-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="02a4c-133">使用 hello 伺服器名稱和 hello 資源群組名稱，此清單 hello 現有伺服器上的防火牆規則 hello 伺服器。</span><span class="sxs-lookup"><span data-stu-id="02a4c-133">Using hello server name and hello resource group name, list hello existing server firewall rules on hello server.</span></span> <span data-ttu-id="02a4c-134">請注意該 hello server name 屬性會指定在 hello **-伺服器**切換並不 hello **-名稱**切換。</span><span class="sxs-lookup"><span data-stu-id="02a4c-134">Notice that hello server name attribute is specified in hello **--server** switch and not hello **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="02a4c-135">如果依預設，在 JSON 中的任何格式，hello 輸出會列出 hello 規則。</span><span class="sxs-lookup"><span data-stu-id="02a4c-135">hello output will list hello rules if any, by default in JSON format.</span></span> <span data-ttu-id="02a4c-136">您可以使用 hello 交換器**-輸出資料表**更容易閱讀的表格格式做為 hello 輸出。</span><span class="sxs-lookup"><span data-stu-id="02a4c-136">You may use hello switch **--output table** for a more readable table format as hello output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="02a4c-137">在「適用於 MySQL 的 Azure 資料庫」伺服器上建立防火牆規則</span><span class="sxs-lookup"><span data-stu-id="02a4c-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="02a4c-138">使用 hello Azure MySQL 伺服器名稱和 hello 資源群組名稱，hello 伺服器上建立新的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="02a4c-138">Using hello Azure MySQL server name and hello resource group name, create a new firewall rule on hello server.</span></span> <span data-ttu-id="02a4c-139">提供 hello 規則 toocover 範圍的 IP 位址 tooallow 存取 hello 規則、 hello 開始 IP 和結束 IP 的名稱。</span><span class="sxs-lookup"><span data-stu-id="02a4c-139">Provide a name for hello rule, hello start IP, and end IP for hello rule toocover a range of IP addresses tooallow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="02a4c-140">單數的 ip 位址 toobe 允許存取，請提供 hello 起始 IP 和結束 IP，如此範例所示為 hello 相同的位址。</span><span class="sxs-lookup"><span data-stu-id="02a4c-140">For a singular IP address toobe allowed access, provide hello same address as hello Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="02a4c-141">成功時，hello 命令輸出會列出您已建立，根據預設，在 JSON 格式的 hello 防火牆規則的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="02a4c-141">Upon success, hello command output will list hello details of hello firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="02a4c-142">如果失敗，hello 輸出就會改為顯示錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="02a4c-142">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="02a4c-143">在「適用於 MySQL 的 Azure 資料庫」伺服器上更新防火牆規則</span><span class="sxs-lookup"><span data-stu-id="02a4c-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="02a4c-144">使用 hello Azure MySQL 伺服器名稱和 hello 資源群組名稱，更新現有防火牆規則 hello 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="02a4c-144">Using hello Azure MySQL server name and hello resource group name, update an existing firewall rule on hello server.</span></span> <span data-ttu-id="02a4c-145">提供 hello 做為輸入，而且 hello 起始 IP 和結束 IP 屬性 tooupdate hello 現有防火牆規則名稱。</span><span class="sxs-lookup"><span data-stu-id="02a4c-145">Provide hello name of hello existing firewall rule as input, and hello start IP and end IP attributes tooupdate.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="02a4c-146">成功時，hello 命令輸出會列出您已更新，根據預設，在 JSON 格式的 hello 防火牆規則的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="02a4c-146">Upon success, hello command output will list hello details of hello firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="02a4c-147">如果失敗，hello 輸出就會改為顯示錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="02a4c-147">If there is a failure, hello output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="02a4c-148">如果 hello 防火牆規則不存在，它將會建立 hello 更新命令。</span><span class="sxs-lookup"><span data-stu-id="02a4c-148">If hello firewall rule does not exist, it will be created by hello update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="02a4c-149">在「適用於 MySQL 的 Azure 資料庫」伺服器上顯示防火牆規則詳細資料</span><span class="sxs-lookup"><span data-stu-id="02a4c-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="02a4c-150">使用 hello Azure MySQL 伺服器名稱和 hello 資源群組名稱，顯示 hello 現有防火牆規則詳細資料從伺服器 hello。</span><span class="sxs-lookup"><span data-stu-id="02a4c-150">Using hello Azure MySQL server name and hello resource group name, show hello existing firewall rule details from hello server.</span></span> <span data-ttu-id="02a4c-151">提供 hello hello 現有防火牆規則名稱做為輸入。</span><span class="sxs-lookup"><span data-stu-id="02a4c-151">Provide hello name of hello existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="02a4c-152">成功時，hello 命令輸出會列出您已指定，預設會在 JSON 格式的 hello 防火牆規則的 hello 詳細資料。</span><span class="sxs-lookup"><span data-stu-id="02a4c-152">Upon success, hello command output will list hello details of hello firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="02a4c-153">如果失敗，hello 輸出就會改為顯示錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="02a4c-153">If there is a failure, hello output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="02a4c-154">在「適用於 MySQL 的 Azure 資料庫」伺服器上刪除防火牆規則</span><span class="sxs-lookup"><span data-stu-id="02a4c-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="02a4c-155">使用 hello Azure MySQL 伺服器名稱和 hello 資源群組名稱，從 hello 伺服器移除現有的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="02a4c-155">Using hello Azure MySQL server name and hello resource group name, remove an existing firewall rule from hello server.</span></span> <span data-ttu-id="02a4c-156">提供 hello hello 現有防火牆規則名稱。</span><span class="sxs-lookup"><span data-stu-id="02a4c-156">Provide hello name of hello existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="02a4c-157">成功時，沒有任何輸出。</span><span class="sxs-lookup"><span data-stu-id="02a4c-157">Upon success, there is no output.</span></span> <span data-ttu-id="02a4c-158">在發生錯誤時，將會傳回 hello 錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="02a4c-158">Upon failure, hello error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="02a4c-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="02a4c-159">Next steps</span></span>
- <span data-ttu-id="02a4c-160">進一步了解[適用於 MySQL 的 Azure 資料庫伺服器防火牆規則](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="02a4c-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="02a4c-161">建立和管理 Azure 資料庫的 MySQL 使用 hello Azure 入口網站的防火牆規則</span><span class="sxs-lookup"><span data-stu-id="02a4c-161">Create and manage Azure Database for MySQL firewall rules using hello Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
