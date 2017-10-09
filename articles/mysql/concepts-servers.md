---
title: "在 Azure 資料庫的 MySQL aaaServer 概念 |Microsoft 文件"
description: "本主題提供使用適用於 MySQL 之 Azure 資料庫伺服器的考量和指導方針。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 4d994cbdbde93ac5af3f4a2a7375b5851bebb1cc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="server-concepts-in-azure-database-for-mysql"></a><span data-ttu-id="976c1-103">適用於 MySQL 的 Azure 資料庫中的伺服器概念</span><span class="sxs-lookup"><span data-stu-id="976c1-103">Server concepts in Azure Database for MySQL</span></span>
<span data-ttu-id="976c1-104">本主題提供使用適用於 MySQL 之 Azure 資料庫伺服器的考量和指導方針。</span><span class="sxs-lookup"><span data-stu-id="976c1-104">This topic provides considerations and guidelines for working with Azure Database for MySQL servers.</span></span>

## <a name="what-is-an-azure-database-for-mysql-server"></a><span data-ttu-id="976c1-105">什麼是適用於 MySQL 的 Azure 資料庫伺服器？</span><span class="sxs-lookup"><span data-stu-id="976c1-105">What is an Azure Database for MySQL server?</span></span>

<span data-ttu-id="976c1-106">適用於 MySQL 的 Azure 資料庫伺服器是多個資料庫的中央管理點。</span><span class="sxs-lookup"><span data-stu-id="976c1-106">An Azure Database for MySQL server is a central administrative point for multiple databases.</span></span> <span data-ttu-id="976c1-107">它是 hello 相同就可以熟悉 hello 在內部部署的世界中的 MySQL server 建構。</span><span class="sxs-lookup"><span data-stu-id="976c1-107">It is hello same MySQL server construct that you may be familiar with in hello on-premises world.</span></span> <span data-ttu-id="976c1-108">具體來說，hello Azure 資料庫的 MySQL 服務管理、 提供效能保證，公開存取與伺服器層級的功能。</span><span class="sxs-lookup"><span data-stu-id="976c1-108">Specifically, hello Azure Database for MySQL service is managed, provides performance guarantees, exposes access and features at server-level.</span></span>

<span data-ttu-id="976c1-109">適用於 MySQL 的 Azure 資料庫伺服器：</span><span class="sxs-lookup"><span data-stu-id="976c1-109">An Azure Database for MySQL server:</span></span>

- <span data-ttu-id="976c1-110">建立於 Azure 訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="976c1-110">Is created within an Azure subscription.</span></span>
- <span data-ttu-id="976c1-111">是 hello 父資源的資料庫。</span><span class="sxs-lookup"><span data-stu-id="976c1-111">Is hello parent resource for databases.</span></span>
- <span data-ttu-id="976c1-112">可為資料庫提供命名空間。</span><span class="sxs-lookup"><span data-stu-id="976c1-112">Provides a namespace for databases.</span></span>
- <span data-ttu-id="976c1-113">是一個容器具有強式存留期語意-刪除伺服器，並在刪除 hello 自主資料庫。</span><span class="sxs-lookup"><span data-stu-id="976c1-113">Is a container with strong lifetime semantics - delete a server and it deletes hello contained databases.</span></span>
- <span data-ttu-id="976c1-114">在一個區域中共置資源。</span><span class="sxs-lookup"><span data-stu-id="976c1-114">Collocates resources in a region.</span></span>
- <span data-ttu-id="976c1-115">提供用來存取伺服器和資料庫的連接端點。</span><span class="sxs-lookup"><span data-stu-id="976c1-115">Provides a connection endpoint for server and database access.</span></span>
- <span data-ttu-id="976c1-116">提供適用於 tooits 資料庫的管理原則的 hello 範圍： 登入、 防火牆、 使用者、 角色、 設定等。</span><span class="sxs-lookup"><span data-stu-id="976c1-116">Provides hello scope for management policies that apply tooits databases: login, firewall, users, roles, configurations, etc.</span></span>
- <span data-ttu-id="976c1-117">可在多個版本中使用。</span><span class="sxs-lookup"><span data-stu-id="976c1-117">Is available in multiple versions.</span></span> <span data-ttu-id="976c1-118">如需詳細資訊，請參閱[支援適用於 MySQL 之 Azure 資料庫的資料庫版本](./concepts-supported-versions.md)。</span><span class="sxs-lookup"><span data-stu-id="976c1-118">For more information, see [Supported Azure Database for MySQL database versions](./concepts-supported-versions.md).</span></span>

<span data-ttu-id="976c1-119">在適用於 MySQL Server 的 Azure 資料庫內，您可以建立一個或多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="976c1-119">Within an Azure Database for MySQL server, you can create one or multiple databases.</span></span> <span data-ttu-id="976c1-120">您可以選擇單一資料庫，每個伺服器 tooutilize toocreate 所有 hello 資源，或建立多個資料庫 tooshare hello 資源。</span><span class="sxs-lookup"><span data-stu-id="976c1-120">You can opt toocreate a single database per server tooutilize all hello resources, or create multiple databases tooshare hello resources.</span></span> <span data-ttu-id="976c1-121">hello 定價是結構化的每個伺服器，根據 hello 組態的定價層，計算單位，儲存體 (GB)。</span><span class="sxs-lookup"><span data-stu-id="976c1-121">hello pricing is structured per-server, based on hello configuration of pricing tier, compute units, storage (GB).</span></span> <span data-ttu-id="976c1-122">如需詳細資訊，請參閱[定價層](./concepts-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="976c1-122">For more information, see [Pricing tiers](./concepts-service-tiers.md).</span></span>

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-mysql-server"></a><span data-ttu-id="976c1-123">如何連接和驗證 tooan Azure 資料庫的 MySQL 伺服器嗎？</span><span class="sxs-lookup"><span data-stu-id="976c1-123">How do I connect and authenticate tooan Azure Database for MySQL server?</span></span>

<span data-ttu-id="976c1-124">hello 下列項目有助於確保安全存取 tooyour 資料庫。</span><span class="sxs-lookup"><span data-stu-id="976c1-124">hello following elements help ensure safe access tooyour database.</span></span>

|||
| :-- | :-- |
| <span data-ttu-id="976c1-125">**驗證和授權**</span><span class="sxs-lookup"><span data-stu-id="976c1-125">**Authentication and authorization**</span></span> | <span data-ttu-id="976c1-126">適用於 MySQL 的 Azure 資料庫伺服器支援原生的 MySQL 驗證。</span><span class="sxs-lookup"><span data-stu-id="976c1-126">Azure Database for MySQL server supports native MySQL authentication.</span></span> <span data-ttu-id="976c1-127">您可以連接和驗證 tooserver 與 hello 伺服器系統管理員登入。</span><span class="sxs-lookup"><span data-stu-id="976c1-127">You can connect and authenticate tooserver with hello server's admin login.</span></span> |
| <span data-ttu-id="976c1-128">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="976c1-128">**Protocol**</span></span> | <span data-ttu-id="976c1-129">hello 服務支援 MySQL 所使用的訊息架構通訊協定。</span><span class="sxs-lookup"><span data-stu-id="976c1-129">hello service supports a message-based protocol used by MySQL.</span></span> |
| <span data-ttu-id="976c1-130">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="976c1-130">**TCP/IP**</span></span> | <span data-ttu-id="976c1-131">透過 TCP/IP，並透過 Unix 網域通訊端支援 hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="976c1-131">hello protocol is supported over TCP/IP, and over Unix-domain sockets.</span></span> |
| <span data-ttu-id="976c1-132">**防火牆**</span><span class="sxs-lookup"><span data-stu-id="976c1-132">**Firewall**</span></span> | <span data-ttu-id="976c1-133">toohelp 保護您的資料、 防火牆規則可防止所有存取 tooyour 資料庫伺服器，或 tooits 資料庫，您必須先指定哪些電腦有權限。</span><span class="sxs-lookup"><span data-stu-id="976c1-133">toohelp protect your data, a firewall rule prevents all access tooyour database server, or tooits databases, until you specify which computers have permission.</span></span> <span data-ttu-id="976c1-134">請參閱[適用於 MySQL 的 Azure 資料庫伺服器防火牆規則](./concepts-firewall-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="976c1-134">See [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md).</span></span> |
| <span data-ttu-id="976c1-135">**SSL**</span><span class="sxs-lookup"><span data-stu-id="976c1-135">**SSL**</span></span> | <span data-ttu-id="976c1-136">hello 服務支援強制執行您的應用程式和資料庫伺服器之間的 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="976c1-136">hello service supports enforcing SSL connections between your applications and your database server.</span></span>  <span data-ttu-id="976c1-137">請參閱[設定 SSL 連接，您的應用程式 toosecurely 所連接的 MySQL tooAzure 資料庫](./howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="976c1-137">See [Configure SSL connectivity in your application toosecurely connect tooAzure Database for MySQL](./howto-configure-ssl.md).</span></span> |
|||

## <a name="how-do-i-manage-a-server"></a><span data-ttu-id="976c1-138">如何管理伺服器？</span><span class="sxs-lookup"><span data-stu-id="976c1-138">How do I manage a server?</span></span>
<span data-ttu-id="976c1-139">您可以使用 Azure 入口網站 hello Azure 資料庫管理 MySQL 伺服器或 hello Azure CLI。</span><span class="sxs-lookup"><span data-stu-id="976c1-139">You can manage Azure Database for MySQL servers by using hello Azure portal or hello Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="976c1-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="976c1-140">Next steps</span></span>
- <span data-ttu-id="976c1-141">如需 hello 服務的概觀，請參閱[Azure 資料庫的 MySQL 概觀](./overview.md)</span><span class="sxs-lookup"><span data-stu-id="976c1-141">For an overview of hello service, see [Azure Database for MySQL Overview](./overview.md)</span></span>
- <span data-ttu-id="976c1-142">如需以您**服務層**為依據之特定資源配額和限制的相關資訊，請參閱[服務層](./concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="976c1-142">For information about specific resource quotas and limitations based on your **service tier**, see [Service tiers](./concepts-service-tiers.md)</span></span>
- <span data-ttu-id="976c1-143">如需連接 toohello 服務的資訊，請參閱[MySQL 的 Azure 資料庫的連接程式庫](./concepts-connection-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="976c1-143">For information about connecting toohello service, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md).</span></span>
