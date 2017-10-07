---
title: "適用於 PostgreSQL 的 Azure 資料庫伺服器防火牆規則 | Microsoft Docs"
description: "描述適用於 PostgreSQL 的 Azure 資料庫伺服器防火牆規則。"
services: postgresql
author: jasonwhowell
ms.author: jasonh
manager: jhubbard
editor: jasonwhowell
ms.service: postgresql
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1d46a4434c483c3612a9a7b4cdef718d6dc3e765
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a><span data-ttu-id="ca80f-103">適用於 PostgreSQL 的 Azure 資料庫伺服器防火牆規則</span><span class="sxs-lookup"><span data-stu-id="ca80f-103">Azure Database for PostgreSQL Server firewall rules</span></span>
<span data-ttu-id="ca80f-104">防火牆會阻止所有存取 tooyour 資料庫伺服器，直到您指定哪些電腦有權限。</span><span class="sxs-lookup"><span data-stu-id="ca80f-104">Firewalls prevent all access tooyour database server until you specify which computers have permission.</span></span> <span data-ttu-id="ca80f-105">hello 防火牆會授與存取 toohello 伺服器 hello 來自每個要求的 IP 位址為基礎。</span><span class="sxs-lookup"><span data-stu-id="ca80f-105">hello firewall grants access toohello server based on hello originating IP address of each request.</span></span>
<span data-ttu-id="ca80f-106">tooconfigure 防火牆，您會建立指定的可接受的 IP 位址範圍的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="ca80f-106">tooconfigure your firewall, you create firewall rules that specify ranges of acceptable IP addresses.</span></span> <span data-ttu-id="ca80f-107">您可以在 hello 伺服器層級建立防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="ca80f-107">You can create firewall rules at hello server level.</span></span>

<span data-ttu-id="ca80f-108">**防火牆規則：**這些規則可讓用戶端 tooaccess 整個 Azure 資料庫 PostgreSQL 伺服器，也就是所有都 hello 資料庫都 hello 相同邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca80f-108">**Firewall rules:** These rules enable clients tooaccess your entire Azure Database for PostgreSQL Server, that is, all hello databases within hello same logical server.</span></span> <span data-ttu-id="ca80f-109">藉由使用 hello Azure 入口網站，或使用 Azure CLI 命令，可以設定伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="ca80f-109">Server-level firewall rules can be configured by using hello Azure portal or using Azure CLI commands.</span></span> <span data-ttu-id="ca80f-110">toocreate 伺服器層級防火牆規則，您必須是 hello 訂用帳戶擁有者或訂閱參與者。</span><span class="sxs-lookup"><span data-stu-id="ca80f-110">toocreate server-level firewall rules, you must be hello subscription owner or a subscription contributor.</span></span>

## <a name="firewall-overview"></a><span data-ttu-id="ca80f-111">防火牆概觀</span><span class="sxs-lookup"><span data-stu-id="ca80f-111">Firewall overview</span></span>
<span data-ttu-id="ca80f-112">Hello 防火牆封鎖 PostgreSQL 伺服器的所有資料庫存取 tooyour Azure 資料庫的預設值。</span><span class="sxs-lookup"><span data-stu-id="ca80f-112">All database access tooyour Azure Database for PostgreSQL server is blocked by hello firewall by default.</span></span> <span data-ttu-id="ca80f-113">toobegin 使用您的伺服器從另一部電腦，您需要 toospecify 其中一個或多伺服器層級防火牆規則 tooenable 存取 tooyour 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ca80f-113">toobegin using your server from another computer, you need toospecify one or more server-level firewall rules tooenable access tooyour server.</span></span> <span data-ttu-id="ca80f-114">使用的 IP 位址範圍是從 hello 網際網路 tooallow hello 防火牆規則 toospecify。</span><span class="sxs-lookup"><span data-stu-id="ca80f-114">Use hello firewall rules toospecify which IP address ranges from hello Internet tooallow.</span></span> <span data-ttu-id="ca80f-115">存取 toohello Azure 入口網站本身不會受到 hello 防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="ca80f-115">Access toohello Azure portal website itself is not impacted by hello firewall rules.</span></span>
<span data-ttu-id="ca80f-116">從連線嘗試 hello 網際網路和 Azure 必須先通過 hello 防火牆才能到達您的 PostgreSQL 資料庫 hello 下列圖表所示：</span><span class="sxs-lookup"><span data-stu-id="ca80f-116">Connection attempts from hello Internet and Azure must first pass through hello firewall before they can reach your PostgreSQL Database, as shown in hello following diagram:</span></span>

![範例流程的 hello 防火牆的運作方式](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a><span data-ttu-id="ca80f-118">從 hello 網際網路連線</span><span class="sxs-lookup"><span data-stu-id="ca80f-118">Connecting from hello Internet</span></span>
<span data-ttu-id="ca80f-119">伺服器層級防火牆規則 PostgreSQL 伺服器 hello Azure 資料庫上套用 tooall 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ca80f-119">Server-level firewall rules apply tooall databases on hello Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="ca80f-120">如果 hello 要求 hello IP 位址是其中一個 hello hello 伺服器層級防火牆規則中指定的範圍內，會授與 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="ca80f-120">If hello IP address of hello request is within one of hello ranges specified in hello server-level firewall rules, hello connection is granted.</span></span>
<span data-ttu-id="ca80f-121">如果 hello 要求 hello IP 位址不在任何 hello 資料庫層級中指定 hello 範圍或伺服器層級防火牆規則，hello 連接要求會失敗。</span><span class="sxs-lookup"><span data-stu-id="ca80f-121">If hello IP address of hello request is not within hello ranges specified in any of hello database-level or server-level firewall rules, hello connection request fails.</span></span>
<span data-ttu-id="ca80f-122">例如，如果您的應用程式會針對 PostgreSQL 連接 JDBC 驅動程式，您可能會遇到 hello 防火牆封鎖 hello 連接時，嘗試 tooconnect 這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="ca80f-122">For example, if your application connects with JDBC driver for PostgreSQL, you may encounter this error attempting tooconnect when hello firewall is blocking hello connection.</span></span>
> <span data-ttu-id="ca80f-123">java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: no pg\_hba.conf entry for host "123.45.67.890", user "adminuser", database "postgresql", SSL</span><span class="sxs-lookup"><span data-stu-id="ca80f-123">java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: no pg\_hba.conf entry for host "123.45.67.890", user "adminuser", database "postgresql", SSL</span></span>

## <a name="programmatically-managing-firewall-rules"></a><span data-ttu-id="ca80f-124">以程式設計方式管理防火牆規則</span><span class="sxs-lookup"><span data-stu-id="ca80f-124">Programmatically managing firewall rules</span></span>
<span data-ttu-id="ca80f-125">除了以程式設計方式使用 Azure CLI toohello Azure 入口網站中，防火牆規則可以是所管理。</span><span class="sxs-lookup"><span data-stu-id="ca80f-125">In addition toohello Azure portal, firewall rules can be managed programmatically using Azure CLI.</span></span>
<span data-ttu-id="ca80f-126">另請參閱[使用 Azure CLI 建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則](howto-manage-firewall-using-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="ca80f-126">See also [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>

## <a name="troubleshooting-hello-database-firewall"></a><span data-ttu-id="ca80f-127">疑難排解 hello database 防火牆</span><span class="sxs-lookup"><span data-stu-id="ca80f-127">Troubleshooting hello database firewall</span></span>
<span data-ttu-id="ca80f-128">請考慮 hello PostgreSQL 伺服器服務的存取 toohello Microsoft Azure 資料庫未如預期運作時，下列點：</span><span class="sxs-lookup"><span data-stu-id="ca80f-128">Consider hello following points when access toohello Microsoft Azure Database for PostgreSQL Server service does not behave as you expect:</span></span>

* <span data-ttu-id="ca80f-129">**變更 toohello 允許清單有尚未生效：**可能會如往常般的五分鐘延遲變更 PostgreSQL 伺服器防火牆設定 tootake 效果 toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="ca80f-129">**Changes toohello allow list have not taken effect yet:** There may be as much as a five-minute delay for changes toohello Azure Database for PostgreSQL Server firewall configuration tootake effect.</span></span>

* <span data-ttu-id="ca80f-130">**hello 登入未獲授權，或使用不正確的密碼：**登入沒有權限 hello Azure 資料庫上使用 PostgreSQL 伺服器或 hello 密碼不正確，如果 hello Azure 資料庫的連接 toohello PostgreSQL server被拒絕。</span><span class="sxs-lookup"><span data-stu-id="ca80f-130">**hello login is not authorized or an incorrect password was used:** If a login does not have permissions on hello Azure Database for PostgreSQL server or hello password used is incorrect, hello connection toohello Azure Database for PostgreSQL server is denied.</span></span> <span data-ttu-id="ca80f-131">建立防火牆設定只提供連接 tooyour 伺服器; 機會 tooattempt 用戶端每個用戶端必須提供 hello 必要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="ca80f-131">Creating a firewall setting only provides clients with an opportunity tooattempt connecting tooyour server; each client must provide hello necessary security credentials.</span></span>

<span data-ttu-id="ca80f-132">例如，使用 JDBC 用戶端，hello 下列錯誤可能會出現。</span><span class="sxs-lookup"><span data-stu-id="ca80f-132">For example, using a JDBC client, hello following error may appear.</span></span>
> <span data-ttu-id="ca80f-133">java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: password authentication failed for user "yourusername"</span><span class="sxs-lookup"><span data-stu-id="ca80f-133">java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: password authentication failed for user "yourusername"</span></span>

* <span data-ttu-id="ca80f-134">**動態 IP 位址：**如果您有使用動態 IP 位址的網際網路連線，並且在經由 hello 防火牆時遇到，您可以嘗試下列解決方案 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="ca80f-134">**Dynamic IP address:** If you have an Internet connection with dynamic IP addressing and you are having trouble getting through hello firewall, you could try one of hello following solutions:</span></span>

* <span data-ttu-id="ca80f-135">要求網際網路服務提供者 (ISP) hello IP 位址範圍指派 tooyour 用戶端電腦的存取 hello Azure Database PostgreSQL 伺服器，然後將 hello IP 位址範圍新增為防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="ca80f-135">Ask your Internet Service Provider (ISP) for hello IP address range assigned tooyour client computers that access hello Azure Database for PostgreSQL Server, and then add hello IP address range as a firewall rule.</span></span>

* <span data-ttu-id="ca80f-136">取得靜態 IP 位址改為您的用戶端電腦，然後將 hello IP 位址新增為防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="ca80f-136">Get static IP addressing instead for your client computers, and then add hello IP addresses as firewall rules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ca80f-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="ca80f-137">Next steps</span></span>
<span data-ttu-id="ca80f-138">如需有關建立伺服器層級和資料庫層級防火牆規則的文章，請參閱：</span><span class="sxs-lookup"><span data-stu-id="ca80f-138">For articles on creating server-level and database-level firewall rules, see:</span></span>
* [<span data-ttu-id="ca80f-139">建立和管理 Azure 資料庫使用 hello Azure 入口網站的 PostgreSQL 防火牆規則</span><span class="sxs-lookup"><span data-stu-id="ca80f-139">Create and manage Azure Database for PostgreSQL firewall rules using hello Azure portal</span></span>](howto-manage-firewall-using-portal.md)
* [<span data-ttu-id="ca80f-140">使用 Azure CLI 建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則</span><span class="sxs-lookup"><span data-stu-id="ca80f-140">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>](howto-manage-firewall-using-cli.md)