---
title: "使用 Azure CLI 建立和管理適用於 MySQL 的 Azure 資料庫防火牆規則 | Microsoft Docs"
description: "本文描述如何使用 Azure CLI 命令列，建立和管理適用於 MySQL 的 Azure 資料庫防火牆規則。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.devlang: azure-cli
ms.topic: article
ms.date: 06/13/2017
ms.openlocfilehash: 9a03722e9f71be307bdbf0b846a4cbf7b34cd7ff
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-manage-azure-database-for-mysql-firewall-rules-using-azure-cli"></a><span data-ttu-id="a0a99-103">使用 Azure CLI 建立和管理適用於 MySQL 的 Azure 資料庫防火牆規則</span><span class="sxs-lookup"><span data-stu-id="a0a99-103">Create and manage Azure Database for MySQL firewall rules using Azure CLI</span></span>
<span data-ttu-id="a0a99-104">伺服器等級防火牆規則可讓系統管理員從特定的 IP 位址或 IP 位址範圍，管理和存取適用於 MySQL 的 Azure 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="a0a99-104">Server-level firewall rules enable administrators to manage access to an Azure Database for MySQL Server from a specific IP address or range of IP addresses.</span></span> <span data-ttu-id="a0a99-105">透過方便的 Azure CLI 命令，您可以建立、更新、刪除、列出及顯示防火牆規則，以管理您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="a0a99-105">Using convenient Azure CLI commands, you can create, update, delete, list, and show firewall rules to manage your server.</span></span> <span data-ttu-id="a0a99-106">如需「適用於 MySQL 的 Azure 資料庫」防火牆的概觀，請參閱[適用於 MySQL 的 Azure 資料庫伺服器防火牆規則](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="a0a99-106">For an overview of Azure Database for MySQL firewalls, see [Azure Database for MySQL server firewall rules](./concepts-firewall-rules.md)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a0a99-107">必要條件</span><span class="sxs-lookup"><span data-stu-id="a0a99-107">Prerequisites</span></span>
* [<span data-ttu-id="a0a99-108">安裝 Azure CLI 2.0</span><span class="sxs-lookup"><span data-stu-id="a0a99-108">Install Azure CLI 2.0</span></span>](https://docs.microsoft.com/cli/azure/install-azure-cli)
* <span data-ttu-id="a0a99-109">安裝適用於 PostgreSQL 和 MySQL 服務的 Azure Python SDK</span><span class="sxs-lookup"><span data-stu-id="a0a99-109">Install Azure Python SDK for PostgreSQL and MySQL Services</span></span>
* <span data-ttu-id="a0a99-110">安裝適用於 PostgreSQL 和 MySQL 服務的 Azure CLI 元件</span><span class="sxs-lookup"><span data-stu-id="a0a99-110">Install the Azure CLI component for PostgreSQL and MySQL services</span></span>
* <span data-ttu-id="a0a99-111">建立適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="a0a99-111">Create an Azure Database for MySQL server</span></span>

## <a name="firewall-rule-commands"></a><span data-ttu-id="a0a99-112">防火牆規則的命令︰</span><span class="sxs-lookup"><span data-stu-id="a0a99-112">Firewall-Rule Commands:</span></span>
<span data-ttu-id="a0a99-113">**az mysql server firewall-rule** 命令是從 Azure CLI 中用來建立、刪除、列出、顯示及更新防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a0a99-113">The **az mysql server firewall-rule** command is used from Azure CLI to create, delete, list, show, and update firewall rules.</span></span>

<span data-ttu-id="a0a99-114">命令：</span><span class="sxs-lookup"><span data-stu-id="a0a99-114">Commands:</span></span>
- <span data-ttu-id="a0a99-115">**create**︰建立 Azure MySQL 伺服器防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a0a99-115">**create**: Create an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="a0a99-116">**delete**︰刪除 Azure MySQL 伺服器防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a0a99-116">**delete**: Delete an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="a0a99-117">**list**：列出 Azure MySQL 伺服器防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a0a99-117">**list** : List the Azure MySQL server firewall rules.</span></span>
- <span data-ttu-id="a0a99-118">**show**︰顯示 Azure MySQL 伺服器防火牆規則的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a0a99-118">**show** : Show the details of an Azure MySQL server firewall rule.</span></span>
- <span data-ttu-id="a0a99-119">**update**：更新 Azure MySQL 伺服器防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a0a99-119">**update**: Update an Azure MySQL server firewall rule.</span></span>

## <a name="login-to-azure-and-list-your-azure-database-for-mysql-servers"></a><span data-ttu-id="a0a99-120">登入 Azure 和列出適用於 MySQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="a0a99-120">Login to Azure and List your Azure Database for MySQL Servers</span></span>
<span data-ttu-id="a0a99-121">安全地連線 Azure CLI 與 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="a0a99-121">Securely connect Azure CLI with your Azure account.</span></span> <span data-ttu-id="a0a99-122">使用 **az login** 命令來執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="a0a99-122">Use the **az login** command to do this.</span></span>

1. <span data-ttu-id="a0a99-123">從命令列執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="a0a99-123">Run the following command from the command line.</span></span>
```azurecli
az login
```
<span data-ttu-id="a0a99-124">此命令會輸出下一個步驟中要使用的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a0a99-124">This command will output a code to use in the next step.</span></span>

2. <span data-ttu-id="a0a99-125">使用網頁瀏覽器開啟 [https://aka.ms/devicelogin](https://aka.ms/devicelogin) 頁面並輸入程式碼。</span><span class="sxs-lookup"><span data-stu-id="a0a99-125">Use a web browser to open the page [https://aka.ms/devicelogin](https://aka.ms/devicelogin) and enter the code.</span></span>

3. <span data-ttu-id="a0a99-126">出現提示時，使用您的 Azure 認證登入。</span><span class="sxs-lookup"><span data-stu-id="a0a99-126">At the prompt, log in using your Azure credentials.</span></span>

4. <span data-ttu-id="a0a99-127">您的登入獲得授權之後，主控台就會列印訂用帳戶清單。</span><span class="sxs-lookup"><span data-stu-id="a0a99-127">Once your login is authorized, a list of subscriptions will be printed in the console.</span></span> <span data-ttu-id="a0a99-128">複製所需訂用帳戶的識別碼，以設定目前的訂用帳戶供未來使用。</span><span class="sxs-lookup"><span data-stu-id="a0a99-128">Copy the id of the desired subscription to set the current subscription to be used moving forward.</span></span>
   ```azurecli-interactive
   az account set --subscription {your subscription id}
   ```

5. <span data-ttu-id="a0a99-129">如果您不確定名稱，請列出您的訂用帳戶和資源群組的「適用於 MySQL 的 Azure 資料庫」伺服器。</span><span class="sxs-lookup"><span data-stu-id="a0a99-129">List the Azure Databases for MySQL servers for your subscription and resource group if you are unsure of the names.</span></span>

   ```azurecli-interactive
   az mysql server list --resource-group myResourceGroup
   ```

   <span data-ttu-id="a0a99-130">請注意清單中的名稱屬性，這將用來指定要使用的 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="a0a99-130">Note the name attribute in the listing, which will be used to specify which MySQL server to work on.</span></span> <span data-ttu-id="a0a99-131">如有需要，請確認該伺服器的詳細資料，使用名稱屬性確認名稱正確︰</span><span class="sxs-lookup"><span data-stu-id="a0a99-131">If needed, confirm the details for that server to using the name attribute to confirm name is correct:</span></span>

   ```azurecli-interactive
   az mysql server show --resource-group myResourceGroup --name mysqlserver4demo
   ```

## <a name="list-firewall-rules-on-azure-database-for-mysql-server"></a><span data-ttu-id="a0a99-132">在「適用於 MySQL 的 Azure 資料庫」伺服器上列出防火牆規則</span><span class="sxs-lookup"><span data-stu-id="a0a99-132">List Firewall Rules on Azure Database for MySQL Server</span></span> 
<span data-ttu-id="a0a99-133">使用伺服器名稱和資源群組名稱，列出伺服器上現有的伺服器防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a0a99-133">Using the server name and the resource group name, list the existing server firewall rules on the server.</span></span> <span data-ttu-id="a0a99-134">請注意，伺服器名稱屬性是在 **--server** 參數中指定，而不是 **--name** 參數。</span><span class="sxs-lookup"><span data-stu-id="a0a99-134">Notice that the server name attribute is specified in the **--server** switch and not the **--name** switch.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo
```
<span data-ttu-id="a0a99-135">根據預設，輸出會以 JSON 格式列出規則 (若有的話)。</span><span class="sxs-lookup"><span data-stu-id="a0a99-135">The output will list the rules if any, by default in JSON format.</span></span> <span data-ttu-id="a0a99-136">您可以使用參數 **--output table**，以更容易閱讀的資料表格式呈現輸出。</span><span class="sxs-lookup"><span data-stu-id="a0a99-136">You may use the switch **--output table** for a more readable table format as the output.</span></span>
```azurecli-interactive
az mysql server firewall-rule list --resource-group myResourceGroup --server mysqlserver4demo --output table
```
## <a name="create-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="a0a99-137">在「適用於 MySQL 的 Azure 資料庫」伺服器上建立防火牆規則</span><span class="sxs-lookup"><span data-stu-id="a0a99-137">Create Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="a0a99-138">使用 Azure MySQL 伺服器名稱和資源群組名稱，在伺服器上建立新的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a0a99-138">Using the Azure MySQL server name and the resource group name, create a new firewall rule on the server.</span></span> <span data-ttu-id="a0a99-139">提供規則的名稱、規則的起始 IP 和結束 IP，以涵蓋允許存取的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="a0a99-139">Provide a name for the rule, the start IP, and end IP for the rule to cover a range of IP addresses to allow access.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.15
```
<span data-ttu-id="a0a99-140">若要允許存取單一 IP 位址，請在 [起始 IP] 和 [結束 IP] 中提供相同的位址，如這個範例所示。</span><span class="sxs-lookup"><span data-stu-id="a0a99-140">For a singular IP address to be allowed access, provide the same address as the Start IP and End IP, as in this example.</span></span>
```azurecli-interactive
az mysql server firewall-rule create --resource-group myResourceGroup  
--server mysql --name "Firewall Rule with a Single Address" --start-ip-address 1.1.1.1 --end-ip-address 1.1.1.1
```
<span data-ttu-id="a0a99-141">成功時，命令輸出會列出您已建立之防火牆規則的詳細資料，預設為 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="a0a99-141">Upon success, the command output will list the details of the firewall rule you have created, by default in JSON format.</span></span> <span data-ttu-id="a0a99-142">如果失敗，輸出就會改為顯示錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="a0a99-142">If there is a failure, the output will show error message text instead.</span></span>

## <a name="update-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="a0a99-143">在「適用於 MySQL 的 Azure 資料庫」伺服器上更新防火牆規則</span><span class="sxs-lookup"><span data-stu-id="a0a99-143">Update Firewall Rule on Azure Database for MySQL server</span></span> 
<span data-ttu-id="a0a99-144">使用 Azure MySQL 伺服器名稱和資源群組名稱，在伺服器上更新現有的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a0a99-144">Using the Azure MySQL server name and the resource group name, update an existing firewall rule on the server.</span></span> <span data-ttu-id="a0a99-145">提供現有防火牆規則的名稱作為輸入，以及要更新的起始 IP 和結束 IP 屬性。</span><span class="sxs-lookup"><span data-stu-id="a0a99-145">Provide the name of the existing firewall rule as input, and the start IP and end IP attributes to update.</span></span>
```azurecli-interactive
az mysql server firewall-rule update --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1" --start-ip-address 13.83.152.0 --end-ip-address 13.83.152.1
```
<span data-ttu-id="a0a99-146">成功時，命令輸出會列出您已更新之防火牆規則的詳細資料，預設為 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="a0a99-146">Upon success, the command output will list the details of the firewall rule you have updated, by default in JSON format.</span></span> <span data-ttu-id="a0a99-147">如果失敗，輸出就會改為顯示錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="a0a99-147">If there is a failure, the output will show error message text instead.</span></span>

> [!NOTE]
> <span data-ttu-id="a0a99-148">如果防火牆規則不存在，更新命令會建立它。</span><span class="sxs-lookup"><span data-stu-id="a0a99-148">If the firewall rule does not exist, it will be created by the update command.</span></span>

## <a name="show-firewall-rule-details-on-azure-database-for-mysql-server"></a><span data-ttu-id="a0a99-149">在「適用於 MySQL 的 Azure 資料庫」伺服器上顯示防火牆規則詳細資料</span><span class="sxs-lookup"><span data-stu-id="a0a99-149">Show Firewall Rule Details on Azure Database for MySQL Server</span></span>
<span data-ttu-id="a0a99-150">使用 Azure MySQL 伺服器名稱和資源群組名稱，顯示伺服器上現有的防火牆規則詳細資料。</span><span class="sxs-lookup"><span data-stu-id="a0a99-150">Using the Azure MySQL server name and the resource group name, show the existing firewall rule details from the server.</span></span> <span data-ttu-id="a0a99-151">提供現有防火牆規則的名稱作為輸入。</span><span class="sxs-lookup"><span data-stu-id="a0a99-151">Provide the name of the existing firewall rule as input.</span></span>
```azurecli-interactive
az mysql server firewall-rule show --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="a0a99-152">成功時，命令輸出會列出您已指定之防火牆規則的詳細資料，預設為 JSON 格式。</span><span class="sxs-lookup"><span data-stu-id="a0a99-152">Upon success, the command output will list the details of the firewall rule you have specified, by default in JSON format.</span></span> <span data-ttu-id="a0a99-153">如果失敗，輸出就會改為顯示錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="a0a99-153">If there is a failure, the output will show error message text instead.</span></span>

## <a name="delete-firewall-rule-on-azure-database-for-mysql-server"></a><span data-ttu-id="a0a99-154">在「適用於 MySQL 的 Azure 資料庫」伺服器上刪除防火牆規則</span><span class="sxs-lookup"><span data-stu-id="a0a99-154">Delete Firewall Rule on Azure Database for MySQL Server</span></span>
<span data-ttu-id="a0a99-155">使用 Azure MySQL 伺服器名稱和資源群組名稱，從伺服器上移除現有的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="a0a99-155">Using the Azure MySQL server name and the resource group name, remove an existing firewall rule from the server.</span></span> <span data-ttu-id="a0a99-156">提供現有防火牆規則的名稱。</span><span class="sxs-lookup"><span data-stu-id="a0a99-156">Provide the name of the existing firewall rule.</span></span>
```azurecli-interactive
az mysql server firewall-rule delete --resource-group myResourceGroup --server mysqlserver4demo --name "Firewall Rule 1"
```
<span data-ttu-id="a0a99-157">成功時，沒有任何輸出。</span><span class="sxs-lookup"><span data-stu-id="a0a99-157">Upon success, there is no output.</span></span> <span data-ttu-id="a0a99-158">發生錯誤時，就會傳回錯誤訊息文字。</span><span class="sxs-lookup"><span data-stu-id="a0a99-158">Upon failure, the error message text will be returned.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a0a99-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="a0a99-159">Next steps</span></span>
- <span data-ttu-id="a0a99-160">進一步了解[適用於 MySQL 的 Azure 資料庫伺服器防火牆規則](./concepts-firewall-rules.md)</span><span class="sxs-lookup"><span data-stu-id="a0a99-160">Understand more about [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md)</span></span>
- [<span data-ttu-id="a0a99-161">使用 Azure 入口網站建立和管理適用於 MySQL 的 Azure 資料庫防火牆規則</span><span class="sxs-lookup"><span data-stu-id="a0a99-161">Create and manage Azure Database for MySQL firewall rules using the Azure portal</span></span>](./howto-manage-firewall-using-portal.md)
