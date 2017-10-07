---
title: "現有 Azure App Service tooAzure aaaConnect MySQL 資料庫 |Microsoft 文件"
description: "指示如何 tooproperly 連接現有的 Azure App Service tooAzure 資料庫的 MySQL"
services: mysql
author: v-chenyh
ms.author: v-chenyh
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/23/2017
ms.openlocfilehash: 6d5b16f316e186d665370adcd8b7c7bb38c8d51a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-an-existing-azure-app-service-tooazure-database-for-mysql-server"></a><span data-ttu-id="53603-103">連接 [MySQL 伺服器的現有 Azure App Service tooAzure 資料庫</span><span class="sxs-lookup"><span data-stu-id="53603-103">Connect an existing Azure App Service tooAzure Database for MySQL server</span></span>
<span data-ttu-id="53603-104">本文件說明如何 tooconnect 現有的 Azure App Service tooyour Azure 資料庫的 MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="53603-104">This document explains how tooconnect an existing Azure App Service tooyour Azure Database for MySQL server.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="53603-105">開始之前</span><span class="sxs-lookup"><span data-stu-id="53603-105">Before you begin</span></span>
<span data-ttu-id="53603-106">登入 toohello [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="53603-106">Log in toohello [Azure portal](https://portal.azure.com).</span></span> <span data-ttu-id="53603-107">建立適用於 MySQL 伺服器的 Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="53603-107">Create an Azure Database for MySQL server.</span></span> <span data-ttu-id="53603-108">如需詳細資訊，請參閱太[如何從入口網站的 MySQL 伺服器資料庫的 toocreate Azure](quickstart-create-mysql-server-database-using-azure-portal.md)或[如何 toocreate Azure 資料庫的 MySQL 伺服器使用 CLI](quickstart-create-mysql-server-database-using-azure-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="53603-108">For details, refer too[How toocreate Azure Database for MySQL server from Portal](quickstart-create-mysql-server-database-using-azure-portal.md) or [How toocreate Azure Database for MySQL server using CLI](quickstart-create-mysql-server-database-using-azure-cli.md).</span></span>

<span data-ttu-id="53603-109">目前有兩個方案 tooenable Azure App Service tooan Azure 資料庫存取的權限 MySQL。</span><span class="sxs-lookup"><span data-stu-id="53603-109">Currently there are two solutions tooenable access from an Azure App Service tooan Azure Database for MySQL.</span></span> <span data-ttu-id="53603-110">這兩種解決方案都需要設定伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="53603-110">Both solutions involve setting up server-level firewall rules.</span></span>

## <a name="solution-1---create-a-firewall-rule-tooallow-all-ips"></a><span data-ttu-id="53603-111">解決方案 1-建立防火牆規則 tooallow 所有 Ip</span><span class="sxs-lookup"><span data-stu-id="53603-111">Solution 1 - Create a firewall rule tooallow all IPs</span></span>
<span data-ttu-id="53603-112">Azure 的 MySQL 資料庫提供使用防火牆 tooprotect 您資料的存取安全性。</span><span class="sxs-lookup"><span data-stu-id="53603-112">Azure Database for MySQL provides access security using a firewall tooprotect your data.</span></span> <span data-ttu-id="53603-113">時從 MySQL 伺服器的 Azure App Service tooAzure 資料庫連接記住該 hello 輸出應用程式服務的 Ip 是動態的本質。</span><span class="sxs-lookup"><span data-stu-id="53603-113">When connecting from an Azure App Service tooAzure Database for MySQL server, keep in mind that hello outbound IPs of App Service are dynamic in nature.</span></span> 

<span data-ttu-id="53603-114">tooensure hello 可用性，您的 Azure 應用程式服務，我們建議使用此方案 tooallow 所有 Ip。</span><span class="sxs-lookup"><span data-stu-id="53603-114">tooensure hello availability of your Azure App Service, we recommend using this solution tooallow ALL IPs.</span></span>

> [!NOTE]
> <span data-ttu-id="53603-115">Microsoft 正在為長期的方案 tooavoid MySQL 允許 Azure 服務 tooconnect tooAzure 資料庫的所有 Ip。</span><span class="sxs-lookup"><span data-stu-id="53603-115">Microsoft is working for a long-term solution tooavoid allowing all IPs for Azure services tooconnect tooAzure Database for MySQL.</span></span>

1. <span data-ttu-id="53603-116">Hello MySQL 伺服器] 刀鋒視窗，設定下標題之下，按一下**連線安全性**tooopen hello 連線安全性刀鋒視窗中的 hello Azure MySQL 資料庫。</span><span class="sxs-lookup"><span data-stu-id="53603-116">On hello MySQL server blade, under Settings heading, click **Connection Security** tooopen hello Connection Security blade for hello Azure Database for MySQL.</span></span>

   ![Azure 入口網站 - 按一下 [連線安全性]](./media/howto-manage-firewall-using-portal/1-connection-security.png)

2. <span data-ttu-id="53603-118">輸入 [規則名稱]、[起始 IP] 和 [結束 IP]。</span><span class="sxs-lookup"><span data-stu-id="53603-118">Enter **RULE NAME**, **START IP**, and **END IP**.</span></span> <span data-ttu-id="53603-119">然後按一下 [儲存] 。</span><span class="sxs-lookup"><span data-stu-id="53603-119">Then click **Save**.</span></span>
   - <span data-ttu-id="53603-120">規則名稱：允許所有 IP</span><span class="sxs-lookup"><span data-stu-id="53603-120">Rule name: Allow-All-IPs</span></span>
   - <span data-ttu-id="53603-121">起始 IP：0.0.0.0</span><span class="sxs-lookup"><span data-stu-id="53603-121">Start IP: 0.0.0.0</span></span>
   - <span data-ttu-id="53603-122">結束 IP：255.255.255.255</span><span class="sxs-lookup"><span data-stu-id="53603-122">End IP: 255.255.255.255</span></span>

   ![Azure 入口網站 - 新增所有 IP](./media/howto-connect-webapp/1_2-add-all-ips.png)

## <a name="solution-2---create-a-firewall-rule-tooexplicitly-allow-outbound-ips"></a><span data-ttu-id="53603-124">解決方案 2-建立防火牆規則 tooexplicitly 允許輸出 Ip</span><span class="sxs-lookup"><span data-stu-id="53603-124">Solution 2 - Create a firewall rule tooexplicitly allow outbound IPs</span></span>
<span data-ttu-id="53603-125">您可以明確加入所有 hello 輸出 Ip，您的 Azure 應用程式服務。</span><span class="sxs-lookup"><span data-stu-id="53603-125">You can explicitly add all hello outbound IPs of your Azure App Service.</span></span>

1. <span data-ttu-id="53603-126">在 [hello 應用程式服務的屬性刀鋒視窗中，檢視您**輸出的 IP 位址**。</span><span class="sxs-lookup"><span data-stu-id="53603-126">On hello App Service Properties blade, view your **OUTBOUND IP ADDRESS**.</span></span>

   ![Azure 入口網站 - 檢視輸出 IP](./media/howto-connect-webapp/2_1-outbound-ip-address.png)

2. <span data-ttu-id="53603-128">在 hello MySQL 連線安全性刀鋒視窗中，新增一個輸出的 Ip。</span><span class="sxs-lookup"><span data-stu-id="53603-128">On hello MySQL Connection security blade, add outbound IPs one by one.</span></span>

   ![Azure 入口網站 - 新增明確的 IP](./media/howto-connect-webapp/2_2-add-explicit-ips.png)

3. <span data-ttu-id="53603-130">請記住太**儲存**您的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="53603-130">Remember too**Save** your firewall rules.</span></span>

<span data-ttu-id="53603-131">雖然 hello Azure 應用程式服務會嘗試 tookeep IP 位址常數經過一段時間，有可能會在其中變更 hello IP 位址的情況。</span><span class="sxs-lookup"><span data-stu-id="53603-131">Though hello Azure App service attempts tookeep IP addresses constant over time, there are cases where hello IP addresses may change.</span></span> <span data-ttu-id="53603-132">比方說，當 hello 應用程式回收或調整規模作業，就會發生，或在 Azure 的區域資料中加入新機器時中心 tooincrease hello 容量。</span><span class="sxs-lookup"><span data-stu-id="53603-132">For example, when hello app recycles or a scale operation occurs, or when new machines are added in Azure regional data centers tooincrease hello capacity.</span></span> <span data-ttu-id="53603-133">當 hello IP 位址變更時，hello 應用程式可能會停止運作，無法再連接 hello 事件中的 toohello MySQL 伺服器。</span><span class="sxs-lookup"><span data-stu-id="53603-133">When hello IP addresses change, hello app could experience downtime in hello event it can no longer connect toohello MySQL server.</span></span> <span data-ttu-id="53603-134">選擇 hello 前面解決方案的其中一個時，請考慮此可能性。</span><span class="sxs-lookup"><span data-stu-id="53603-134">Consider this potential when choosing one of hello preceding solutions.</span></span>

## <a name="ssl-configuration"></a><span data-ttu-id="53603-135">SSL 設定</span><span class="sxs-lookup"><span data-stu-id="53603-135">SSL configuration</span></span>
<span data-ttu-id="53603-136">適用於 MySQL 的 Azure 資料庫預設會啟用 SSL。</span><span class="sxs-lookup"><span data-stu-id="53603-136">Azure Database for MySQL has SSL Enabled by default.</span></span> <span data-ttu-id="53603-137">如果您的應用程式不使用 SSL tooconnect toohello 資料庫，您需要 toodisable SSL MySQL 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="53603-137">If your application is not using SSL tooconnect toohello database, then you need toodisable SSL on MySQL server.</span></span> <span data-ttu-id="53603-138">如需詳細資訊，如何 tooconfigure SSL，請參閱[使用 SSL 與 Azure 資料庫的 MySQL](howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="53603-138">For details on how tooconfigure SSL, See [Using SSL with Azure Database for MySQL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="53603-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="53603-139">Next steps</span></span>
<span data-ttu-id="53603-140">如需有關連接字串的詳細資訊，請參閱太[連接字串](howto-connection-string.md)。</span><span class="sxs-lookup"><span data-stu-id="53603-140">For more information about connection strings, refer too[Connection Strings](howto-connection-string.md).</span></span>
