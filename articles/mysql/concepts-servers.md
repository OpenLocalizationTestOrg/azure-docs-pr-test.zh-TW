---
title: "適用於 MySQL 的 Azure 資料庫中的伺服器概念 | Microsoft Docs"
description: "本主題提供使用適用於 MySQL 之 Azure 資料庫伺服器的考量和指導方針。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: a2556206ac53829fcd6ab92ffe292859349790d7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="server-concepts-in-azure-database-for-mysql"></a><span data-ttu-id="0560d-103">適用於 MySQL 的 Azure 資料庫中的伺服器概念</span><span class="sxs-lookup"><span data-stu-id="0560d-103">Server concepts in Azure Database for MySQL</span></span>
<span data-ttu-id="0560d-104">本主題提供使用適用於 MySQL 之 Azure 資料庫伺服器的考量和指導方針。</span><span class="sxs-lookup"><span data-stu-id="0560d-104">This topic provides considerations and guidelines for working with Azure Database for MySQL servers.</span></span>

## <a name="what-is-an-azure-database-for-mysql-server"></a><span data-ttu-id="0560d-105">什麼是適用於 MySQL 的 Azure 資料庫伺服器？</span><span class="sxs-lookup"><span data-stu-id="0560d-105">What is an Azure Database for MySQL server?</span></span>

<span data-ttu-id="0560d-106">適用於 MySQL 的 Azure 資料庫伺服器是多個資料庫的中央管理點。</span><span class="sxs-lookup"><span data-stu-id="0560d-106">An Azure Database for MySQL server is a central administrative point for multiple databases.</span></span> <span data-ttu-id="0560d-107">這與您可能已在內部部署領域中熟悉的 MySQL 伺服器建構相同。</span><span class="sxs-lookup"><span data-stu-id="0560d-107">It is the same MySQL server construct that you may be familiar with in the on-premises world.</span></span> <span data-ttu-id="0560d-108">具體來說，適用於 MySQL 的 Azure 資料庫服務會受到管理、提供效能保證、公開伺服器層級的存取和功能。</span><span class="sxs-lookup"><span data-stu-id="0560d-108">Specifically, the Azure Database for MySQL service is managed, provides performance guarantees, exposes access and features at server-level.</span></span>

<span data-ttu-id="0560d-109">適用於 MySQL 的 Azure 資料庫伺服器：</span><span class="sxs-lookup"><span data-stu-id="0560d-109">An Azure Database for MySQL server:</span></span>

- <span data-ttu-id="0560d-110">建立於 Azure 訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="0560d-110">Is created within an Azure subscription.</span></span>
- <span data-ttu-id="0560d-111">是資料庫的父資源。</span><span class="sxs-lookup"><span data-stu-id="0560d-111">Is the parent resource for databases.</span></span>
- <span data-ttu-id="0560d-112">可為資料庫提供命名空間。</span><span class="sxs-lookup"><span data-stu-id="0560d-112">Provides a namespace for databases.</span></span>
- <span data-ttu-id="0560d-113">是具有強式存留期語意 (刪除伺服器) 的容器，而且會刪除自主資料庫。</span><span class="sxs-lookup"><span data-stu-id="0560d-113">Is a container with strong lifetime semantics - delete a server and it deletes the contained databases.</span></span>
- <span data-ttu-id="0560d-114">在一個區域中共置資源。</span><span class="sxs-lookup"><span data-stu-id="0560d-114">Collocates resources in a region.</span></span>
- <span data-ttu-id="0560d-115">提供用來存取伺服器和資料庫的連接端點。</span><span class="sxs-lookup"><span data-stu-id="0560d-115">Provides a connection endpoint for server and database access.</span></span>
- <span data-ttu-id="0560d-116">提供適用於其資料庫的管理原則範圍︰登入、防火牆、使用者、角色、設定等等。</span><span class="sxs-lookup"><span data-stu-id="0560d-116">Provides the scope for management policies that apply to its databases: login, firewall, users, roles, configurations, etc.</span></span>
- <span data-ttu-id="0560d-117">可在多個版本中使用。</span><span class="sxs-lookup"><span data-stu-id="0560d-117">Is available in multiple versions.</span></span> <span data-ttu-id="0560d-118">如需詳細資訊，請參閱[支援適用於 MySQL 之 Azure 資料庫的資料庫版本](./concepts-supported-versions.md)。</span><span class="sxs-lookup"><span data-stu-id="0560d-118">For more information, see [Supported Azure Database for MySQL database versions](./concepts-supported-versions.md).</span></span>

<span data-ttu-id="0560d-119">在適用於 MySQL Server 的 Azure 資料庫內，您可以建立一個或多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="0560d-119">Within an Azure Database for MySQL server, you can create one or multiple databases.</span></span> <span data-ttu-id="0560d-120">您可以選擇在每個伺服器建立單一資料庫以利用所有資源，或建立多個資料庫來共用資源。</span><span class="sxs-lookup"><span data-stu-id="0560d-120">You can opt to create a single database per server to utilize all the resources, or create multiple databases to share the resources.</span></span> <span data-ttu-id="0560d-121">定價是根據伺服器，以定價層設定、計算單位、儲存體 (GB) 作為基礎進行結構化。</span><span class="sxs-lookup"><span data-stu-id="0560d-121">The pricing is structured per-server, based on the configuration of pricing tier, compute units, storage (GB).</span></span> <span data-ttu-id="0560d-122">如需詳細資訊，請參閱[定價層](./concepts-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="0560d-122">For more information, see [Pricing tiers](./concepts-service-tiers.md).</span></span>

## <a name="how-do-i-connect-and-authenticate-to-an-azure-database-for-mysql-server"></a><span data-ttu-id="0560d-123">如何連接及驗證適用於 MySQL 的 Azure 資料庫伺服器？</span><span class="sxs-lookup"><span data-stu-id="0560d-123">How do I connect and authenticate to an Azure Database for MySQL server?</span></span>

<span data-ttu-id="0560d-124">下列項目有助於確保對資料庫的安全存取。</span><span class="sxs-lookup"><span data-stu-id="0560d-124">The following elements help ensure safe access to your database.</span></span>

|||
| :-- | :-- |
| <span data-ttu-id="0560d-125">**驗證和授權**</span><span class="sxs-lookup"><span data-stu-id="0560d-125">**Authentication and authorization**</span></span> | <span data-ttu-id="0560d-126">適用於 MySQL 的 Azure 資料庫伺服器支援原生的 MySQL 驗證。</span><span class="sxs-lookup"><span data-stu-id="0560d-126">Azure Database for MySQL server supports native MySQL authentication.</span></span> <span data-ttu-id="0560d-127">您可以利用伺服器的系統管理員登入來連接和驗證伺服器。</span><span class="sxs-lookup"><span data-stu-id="0560d-127">You can connect and authenticate to server with the server's admin login.</span></span> |
| <span data-ttu-id="0560d-128">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="0560d-128">**Protocol**</span></span> | <span data-ttu-id="0560d-129">此服務支援 MySQL 所使用的訊息架構通訊協定。</span><span class="sxs-lookup"><span data-stu-id="0560d-129">The service supports a message-based protocol used by MySQL.</span></span> |
| <span data-ttu-id="0560d-130">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="0560d-130">**TCP/IP**</span></span> | <span data-ttu-id="0560d-131">TCP/IP 和 Unix 網域通訊端上支援此通訊協定。</span><span class="sxs-lookup"><span data-stu-id="0560d-131">The protocol is supported over TCP/IP, and over Unix-domain sockets.</span></span> |
| <span data-ttu-id="0560d-132">**防火牆**</span><span class="sxs-lookup"><span data-stu-id="0560d-132">**Firewall**</span></span> | <span data-ttu-id="0560d-133">為了協助保護您的資料，防火牆規則會防止對您的資料庫伺服器或其資料庫的所有存取，直到您指定哪些電腦擁有權限為止。</span><span class="sxs-lookup"><span data-stu-id="0560d-133">To help protect your data, a firewall rule prevents all access to your database server, or to its databases, until you specify which computers have permission.</span></span> <span data-ttu-id="0560d-134">請參閱[適用於 MySQL 的 Azure 資料庫伺服器防火牆規則](./concepts-firewall-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="0560d-134">See [Azure Database for MySQL Server firewall rules](./concepts-firewall-rules.md).</span></span> |
| <span data-ttu-id="0560d-135">**SSL**</span><span class="sxs-lookup"><span data-stu-id="0560d-135">**SSL**</span></span> | <span data-ttu-id="0560d-136">此服務支援在您的應用程式和資料庫伺服器之間強制執行 SSL 連接。</span><span class="sxs-lookup"><span data-stu-id="0560d-136">The service supports enforcing SSL connections between your applications and your database server.</span></span>  <span data-ttu-id="0560d-137">請參閱[在您的應用程式中設定 SSL 連線能力，以安全地連線至適用於 MySQL 的 Azure 資料庫](./howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="0560d-137">See [Configure SSL connectivity in your application to securely connect to Azure Database for MySQL](./howto-configure-ssl.md).</span></span> |
|||

## <a name="how-do-i-manage-a-server"></a><span data-ttu-id="0560d-138">如何管理伺服器？</span><span class="sxs-lookup"><span data-stu-id="0560d-138">How do I manage a server?</span></span>
<span data-ttu-id="0560d-139">您可以使用 Azure 入口網站或 Azure CLI，來管理適用於 MySQL 的 Azure 資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="0560d-139">You can manage Azure Database for MySQL servers by using the Azure portal or the Azure CLI.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0560d-140">後續步驟</span><span class="sxs-lookup"><span data-stu-id="0560d-140">Next steps</span></span>
- <span data-ttu-id="0560d-141">如需服務的概觀，請參閱[適用於 MySQL 的 Azure 資料庫概觀](./overview.md)</span><span class="sxs-lookup"><span data-stu-id="0560d-141">For an overview of the service, see [Azure Database for MySQL Overview](./overview.md)</span></span>
- <span data-ttu-id="0560d-142">如需以您**服務層**為依據之特定資源配額和限制的相關資訊，請參閱[服務層](./concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="0560d-142">For information about specific resource quotas and limitations based on your **service tier**, see [Service tiers](./concepts-service-tiers.md)</span></span>
- <span data-ttu-id="0560d-143">如需連接到服務的相關資訊，請參閱[適用於 MySQL 的 Azure 資料庫的連線庫](./concepts-connection-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="0560d-143">For information about connecting to the service, see [Connection libraries for Azure Database for MySQL](./concepts-connection-libraries.md).</span></span>
