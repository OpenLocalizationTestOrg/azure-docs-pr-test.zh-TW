---
title: "將現有的 Azure App Service 連線到適用於 MySQL 的 Azure 資料庫 | Microsoft Docs"
description: "說明如何將現有的 Azure App Service 正確地連線到適用於 MySQL 的 Azure 資料庫"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 735e21e8135d67405ec6b88d75be1711a2f071f0
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="connect-an-existing-azure-app-service-to-azure-database-for-mysql-server"></a><span data-ttu-id="c4759-103">將現有的 Azure App Service 連線到適用於 MySQL 伺服器的 Azure 資料庫</span><span class="sxs-lookup"><span data-stu-id="c4759-103">Connect an existing Azure App Service to Azure Database for MySQL server</span></span>
<span data-ttu-id="c4759-104">本文件說明如何將現有的 Azure App Service 連線到適用於 MySQL 伺服器的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c4759-104">This document explains how to connect an existing Azure App Service to your Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c4759-105">開始之前</span><span class="sxs-lookup"><span data-stu-id="c4759-105">Before you begin</span></span>
<span data-ttu-id="c4759-106">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="c4759-106">Log in to the [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="c4759-107">建立適用於 MySQL 伺服器的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c4759-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="c4759-108">如需詳細資訊，請參閱[如何從入口網站建立適用於 MySQL 伺服器的 Azure 資料庫](quickstart-create-mysql-server-database-using-azure-portal.md)或[如何使用 CLI 建立適用於 MySQL 伺服器的 Azure 資料庫](quickstart-create-mysql-server-database-using-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="c4759-108">For details, refer to [How to create Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How to create Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="c4759-109">目前有兩種解決方案可讓您從 Azure App Service 存取適用於 MySQL 的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c4759-109">Currently there are two solutions to enable access from an Azure App Service to an Azure Database for MySQL.</span></span> <span data-ttu-id="c4759-110">這兩種解決方案都需要設定伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="c4759-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-to-allow-all-ips"></a><span data-ttu-id="c4759-111">解決方案 1 - 建立防火牆規則以允許所有 IP</span><span class="sxs-lookup"><span data-stu-id="c4759-111">Solution 1 - Create a firewall rule to allow all IPs</span></span>
<span data-ttu-id="c4759-112">適用於 MySQL 的 Azure 資料庫提供存取安全性，使用防火牆來保護您的資料。</span><span class="sxs-lookup"><span data-stu-id="c4759-112">Azure Database for MySQL provides access security using a firewall to protect your data.</span></span> <span data-ttu-id="c4759-113">Azure App Service 連線到適用於 MySQL 伺服器的 Azure 資料庫時，請注意 App Service 的輸出 IP 本質上是動態的。</span><span class="sxs-lookup"><span data-stu-id="c4759-113">When connecting from an Azure App Service to Azure Database for MySQL server, keep in mind that the outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="c4759-114">為了確保 Azure App Service 的可用性，建議使用此解決方案，以允許所有 IP。</span><span class="sxs-lookup"><span data-stu-id="c4759-114">To ensure the availability of your Azure App Service, we recommend using this solution to allow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="c4759-115">Microsoft 正努力提供長期解決方案，以避免允許所有 Azure 服務 IP 都能連線到適用於 MySQL 的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="c4759-115">Microsoft is working for a long-term solution to avoid allowing all IPs for Azure services to connect to Azure Database for MySQL.</span></span>

1. <span data-ttu-id="c4759-116">在 [MySQL 伺服器] 刀鋒視窗的 [設定] 標題下，按一下 [連線安全性]，開啟「適用於 MySQL 的 Azure 資料庫」的 [連線安全性] 刀鋒視窗。</span><span class="sxs-lookup"><span data-stu-id="c4759-116">On the MySQL server blade, under Settings heading, click **Connection Security** to open the Connection Security blade for the Azure Database for MySQL.</span></span>

   ![Azure 入口網站 - 按一下 [連線安全性]](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="c4759-118">輸入 [規則名稱]、[起始 IP] 和 [結束 IP]。</span><span class="sxs-lookup"><span data-stu-id="c4759-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="c4759-119">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="c4759-119">Then click **Save**.</span></span>
   - <span data-ttu-id="c4759-120">規則名稱：允許所有 IP</span><span class="sxs-lookup"><span data-stu-id="c4759-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="c4759-121">起始 IP：0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="c4759-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="c4759-122">結束 IP：255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="c4759-122">End IP: 255.255.255.255</span></span>

   ![Azure 入口網站 - 新增所有 IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-to-explicitly-allow-outbound-ips"></a><span data-ttu-id="c4759-124">解決方案 2 - 建立防火牆規則以明確允許輸出 IP</span><span class="sxs-lookup"><span data-stu-id="c4759-124">Solution 2 - Create a firewall rule to explicitly allow outbound IPs</span></span>
<span data-ttu-id="c4759-125">您可以明確新增 Azure App Service 的所有輸出 IP。</span><span class="sxs-lookup"><span data-stu-id="c4759-125">You can explicitly add all the outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="c4759-126">在 App Service 的 [屬性] 刀鋒視窗上，檢視您的 [輸出 IP 位址]。</span><span class="sxs-lookup"><span data-stu-id="c4759-126">On the App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Azure 入口網站 - 檢視輸出 IP](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="c4759-128">在 MySQL 的 [連線安全性] 刀鋒視窗上，逐一新增輸出 IP。</span><span class="sxs-lookup"><span data-stu-id="c4759-128">On the MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Azure 入口網站 - 新增明確的 IP](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="c4759-130">記得**儲存**您的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="c4759-130">Remember to **Save** your firewall rules.</span></span>

<span data-ttu-id="c4759-131">雖然 Azure App Service 會嘗試將 IP 位址保持固定一段時間，IP 位址有時還是可能會變更。</span><span class="sxs-lookup"><span data-stu-id="c4759-131">Though the Azure App service attempts to keep IP addresses constant over time, there are cases where the IP addresses may change.</span></span> <span data-ttu-id="c4759-132">例如，發生應用程式回收或調整規模作業時，或在 Azure 地區資料中心內新增機器以增加容量時。</span><span class="sxs-lookup"><span data-stu-id="c4759-132">For example, when the app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers to increase the capacity.</span></span> <span data-ttu-id="c4759-133">當 IP 位址變更時，應用程式可能會在無法再連線到 MySQL 伺服器時發生停機。</span><span class="sxs-lookup"><span data-stu-id="c4759-133">When the IP addresses change, the app could experience downtime in the event it can no longer connect to the MySQL server.</span></span> <span data-ttu-id="c4759-134">選擇上述其中一種解決方案時，請考慮這個可能性。</span><span class="sxs-lookup"><span data-stu-id="c4759-134">Consider this potential when choosing one of the preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="c4759-135">SSL 設定</span><span class="sxs-lookup"><span data-stu-id="c4759-135">SSL configuration</span></span>
<span data-ttu-id="c4759-136">適用於 MySQL 的 Azure 資料庫預設會啟用 SSL。</span><span class="sxs-lookup"><span data-stu-id="c4759-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="c4759-137">如果您的應用程式未使用 SSL 連線到資料庫，則必須在 MySQL 伺服器上停用 SSL。</span><span class="sxs-lookup"><span data-stu-id="c4759-137">If your application is not using SSL to connect to the database, then you need to disable SSL on MySQL server.</span></span> <span data-ttu-id="c4759-138">如需如何設定 SSL 的詳細資訊，請參閱[使用 SSL 與適用於 MySQL 的 Azure 資料庫](howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="c4759-138">For details on how to configure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4759-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="c4759-139">Next steps</span></span>
<span data-ttu-id="c4759-140">如需連接字串的詳細資訊，請參閱[連接字串](howto-connection-string.md)。</span><span class="sxs-lookup"><span data-stu-id="c4759-140">For more information about connection strings, refer to [Connection Strings](howto-connection-string.md).</span></span>
