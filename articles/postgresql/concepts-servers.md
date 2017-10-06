---
title: "Azure PostgreSQL 資料庫中的 aaaServer 概念 |Microsoft 文件"
description: "本主題提供使用適用於 PostgreSQL 之 Azure 資料庫伺服器的考量和指導方針。"
services: postgresql
author: SaloniSonpal
ms.author: salonis
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 07/06/2017
ms.openlocfilehash: 9cc7816992f2ddedd76fdf906075a723b97720a4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-servers"></a><span data-ttu-id="7528e-103">適用於 PostgreSQL 的 Azure 資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="7528e-103">Azure Database for PostgreSQL Servers</span></span>
<span data-ttu-id="7528e-104">本主題提供使用適用於 PostgreSQL 之 Azure 資料庫伺服器的考量和指導方針。</span><span class="sxs-lookup"><span data-stu-id="7528e-104">This topic provides considerations and guidelines for working with Azure Database for PostgreSQL servers.</span></span>

## <a name="what-is-an-azure-database-for-postgresql-server"></a><span data-ttu-id="7528e-105">什麼是適用於 PostgreSQL 的 Azure 資料庫伺服器？</span><span class="sxs-lookup"><span data-stu-id="7528e-105">What is an Azure Database for PostgreSQL server?</span></span>
<span data-ttu-id="7528e-106">適用於 PostgreSQL 的 Azure 資料庫伺服器是多個資料庫的中央管理點。</span><span class="sxs-lookup"><span data-stu-id="7528e-106">An Azure Database for PostgreSQL server is a central administrative point for multiple databases.</span></span> <span data-ttu-id="7528e-107">它是 hello 相同 PostgreSQL server 建構函式，您可能要熟悉 hello 在內部部署的世界中。</span><span class="sxs-lookup"><span data-stu-id="7528e-107">It is hello same PostgreSQL server construct that you may be familiar with in hello on-premises world.</span></span> <span data-ttu-id="7528e-108">具體來說，hello PostgreSQL 服務管理、 提供效能保證，公開存取與伺服器層級的功能。</span><span class="sxs-lookup"><span data-stu-id="7528e-108">Specifically, hello PostgreSQL service is managed, provides performance guarantees, exposes access and features at server-level.</span></span>

<span data-ttu-id="7528e-109">適用於 PostgreSQL 的 Azure 資料庫伺服器：</span><span class="sxs-lookup"><span data-stu-id="7528e-109">An Azure Database for PostgreSQL server:</span></span>

- <span data-ttu-id="7528e-110">建立於 Azure 訂用帳戶內。</span><span class="sxs-lookup"><span data-stu-id="7528e-110">Is created within an Azure subscription.</span></span>
- <span data-ttu-id="7528e-111">是 hello 父資源的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7528e-111">Is hello parent resource for databases.</span></span>
- <span data-ttu-id="7528e-112">可為資料庫提供命名空間。</span><span class="sxs-lookup"><span data-stu-id="7528e-112">Provides a namespace for databases.</span></span>
- <span data-ttu-id="7528e-113">是一個容器具有強式存留期語意-刪除伺服器，並在刪除 hello 自主資料庫。</span><span class="sxs-lookup"><span data-stu-id="7528e-113">Is a container with strong lifetime semantics - delete a server and it deletes hello contained databases.</span></span>
- <span data-ttu-id="7528e-114">在一個區域中共置資源。</span><span class="sxs-lookup"><span data-stu-id="7528e-114">Collocates resources in a region.</span></span>
- <span data-ttu-id="7528e-115">提供用來存取伺服器和資料庫的連接端點 (.postgresql.database.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="7528e-115">Provides a connection endpoint for server and database access (.postgresql.database.azure.com).</span></span>
- <span data-ttu-id="7528e-116">提供適用於 tooits 資料庫的管理原則的 hello 範圍： 登入、 防火牆、 使用者、 角色、 設定等。</span><span class="sxs-lookup"><span data-stu-id="7528e-116">Provides hello scope for management policies that apply tooits databases: login, firewall, users, roles, configurations, etc.</span></span>
- <span data-ttu-id="7528e-117">可在多個版本中使用。</span><span class="sxs-lookup"><span data-stu-id="7528e-117">Is available in multiple versions.</span></span> <span data-ttu-id="7528e-118">如需詳細資訊，請參閱[支援的 PostgreSQL 資料庫版本](concepts-supported-versions.md)。</span><span class="sxs-lookup"><span data-stu-id="7528e-118">For more information, see [Supported PostgreSQL database versions](concepts-supported-versions.md).</span></span>
- <span data-ttu-id="7528e-119">可由使用者加以擴充。</span><span class="sxs-lookup"><span data-stu-id="7528e-119">Is extensible by users.</span></span> <span data-ttu-id="7528e-120">如需詳細資訊，請參閱 [PostgreSQL 擴充功能](concepts-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="7528e-120">For more information, see [PostgreSQL extensions](concepts-extensions.md).</span></span>

<span data-ttu-id="7528e-121">在適用於 PostgreSQL 的 Azure 資料庫內，您可以建立一個或多個資料庫。</span><span class="sxs-lookup"><span data-stu-id="7528e-121">Within an Azure Database for PostgreSQL server, you can create one or multiple databases.</span></span> <span data-ttu-id="7528e-122">您可以選擇單一資料庫，每個伺服器 tooutilize toocreate 所有 hello 資源，或建立多個資料庫 tooshare hello 資源。</span><span class="sxs-lookup"><span data-stu-id="7528e-122">You can opt toocreate a single database per server tooutilize all hello resources, or create multiple databases tooshare hello resources.</span></span> <span data-ttu-id="7528e-123">hello 定價是結構化的每個伺服器，根據 hello 組態的定價層，計算單位，儲存體 (GB)。</span><span class="sxs-lookup"><span data-stu-id="7528e-123">hello pricing is structured per-server, based on hello configuration of pricing tier, compute units, storage (GB).</span></span> <span data-ttu-id="7528e-124">如需詳細資訊，請參閱[定價層](./concepts-service-tiers.md)。</span><span class="sxs-lookup"><span data-stu-id="7528e-124">For more details, see [Pricing tiers](./concepts-service-tiers.md).</span></span>

## <a name="how-do-i-connect-and-authenticate-tooan-azure-database-for-postgresql-server"></a><span data-ttu-id="7528e-125">如何連接和驗證 tooan Azure Database PostgreSQL 伺服器嗎？</span><span class="sxs-lookup"><span data-stu-id="7528e-125">How do I connect and authenticate tooan Azure Database for PostgreSQL server?</span></span>
<span data-ttu-id="7528e-126">hello 下列項目有助於確保安全存取 tooyour 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7528e-126">hello following elements help ensure safe access tooyour database.</span></span>

|||
| :-- | :-- |
| <span data-ttu-id="7528e-127">**驗證和授權**</span><span class="sxs-lookup"><span data-stu-id="7528e-127">**Authentication and authorization**</span></span> | <span data-ttu-id="7528e-128">適用於 PostgreSQL 的 Azure 資料庫伺服器支援原生的 PostgreSQL 驗證。</span><span class="sxs-lookup"><span data-stu-id="7528e-128">Azure Database for PostgreSQL server supports native PostgreSQL authentication.</span></span> <span data-ttu-id="7528e-129">您可以連接和驗證 tooserver 與 hello 伺服器系統管理員登入。</span><span class="sxs-lookup"><span data-stu-id="7528e-129">You can connect and authenticate tooserver with hello server's admin login.</span></span> |
| <span data-ttu-id="7528e-130">**通訊協定**</span><span class="sxs-lookup"><span data-stu-id="7528e-130">**Protocol**</span></span> | <span data-ttu-id="7528e-131">hello 服務支援 PostgreSQL 所使用的訊息架構通訊協定。</span><span class="sxs-lookup"><span data-stu-id="7528e-131">hello service supports a message-based protocol used by PostgreSQL.</span></span> |
| <span data-ttu-id="7528e-132">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="7528e-132">**TCP/IP**</span></span> | <span data-ttu-id="7528e-133">透過 TCP/IP，並透過 Unix 網域通訊端支援 hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="7528e-133">hello protocol is supported over TCP/IP, and over Unix-domain sockets.</span></span> |
| <span data-ttu-id="7528e-134">**防火牆**</span><span class="sxs-lookup"><span data-stu-id="7528e-134">**Firewall**</span></span> | <span data-ttu-id="7528e-135">toohelp 保護您的資料、 防火牆規則可防止所有存取 tooyour 資料庫伺服器，或 tooits 資料庫，您必須先指定哪些電腦有權限。</span><span class="sxs-lookup"><span data-stu-id="7528e-135">toohelp protect your data, a firewall rule prevents all access tooyour database server, or tooits databases, until you specify which computers have permission.</span></span> <span data-ttu-id="7528e-136">請參閱[適用於 PostgreSQL 的 Azure 資料庫伺服器防火牆規則](concepts-firewall-rules.md)。</span><span class="sxs-lookup"><span data-stu-id="7528e-136">See [Azure Database for PostgreSQL Server firewall rules](concepts-firewall-rules.md).</span></span> |
|||

## <a name="how-do-i-manage-a-server"></a><span data-ttu-id="7528e-137">如何管理伺服器？</span><span class="sxs-lookup"><span data-stu-id="7528e-137">How do I manage a server?</span></span>
<span data-ttu-id="7528e-138">您可以針對使用 PostgreSQL 伺服器 hello Azure 入口網站或 hello 管理 Azure Database [Azure CLI](/cli/azure/postgres)。</span><span class="sxs-lookup"><span data-stu-id="7528e-138">You can manage Azure Database for PostgreSQL servers by using hello Azure portal or hello [Azure CLI](/cli/azure/postgres).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7528e-139">後續步驟</span><span class="sxs-lookup"><span data-stu-id="7528e-139">Next steps</span></span>
- <span data-ttu-id="7528e-140">如需 hello 服務的概觀，請參閱[Azure Database PostgreSQL 概觀。](overview.md)</span><span class="sxs-lookup"><span data-stu-id="7528e-140">For an overview of hello service, see [Azure Database for PostgreSQL Overview](overview.md)</span></span>
- <span data-ttu-id="7528e-141">如需以您**服務層**為依據之特定資源配額和限制的相關資訊，請參閱[服務層](concepts-service-tiers.md)</span><span class="sxs-lookup"><span data-stu-id="7528e-141">For information about specific resource quotas and limitations based on your **service tier**, see [Service tiers](concepts-service-tiers.md)</span></span>
- <span data-ttu-id="7528e-142">如需連接 toohello 服務的資訊，請參閱[PostgreSQL 的 Azure 資料庫的連接程式庫](concepts-connection-libraries.md)。</span><span class="sxs-lookup"><span data-stu-id="7528e-142">For information on connecting toohello service, see [Connection libraries for Azure Database for PostgreSQL](concepts-connection-libraries.md).</span></span>
