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
ms.openlocfilehash: 150c4f53c5ab6a6425b6af7d286d4c1518b006f8
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="azure-database-for-postgresql-server-firewall-rules"></a><span data-ttu-id="987b3-103">適用於 PostgreSQL 的 Azure 資料庫伺服器防火牆規則</span><span class="sxs-lookup"><span data-stu-id="987b3-103">Azure Database for PostgreSQL Server firewall rules</span></span>
<span data-ttu-id="987b3-104">防火牆會防止對您資料庫伺服器的所有存取，直到您指定哪些電腦擁有權限。</span><span class="sxs-lookup"><span data-stu-id="987b3-104">Firewalls prevent all access to your database server until you specify which computers have permission.</span></span> <span data-ttu-id="987b3-105">此防火牆會根據每一個要求的來源 IP 位址來授與伺服器存取權。</span><span class="sxs-lookup"><span data-stu-id="987b3-105">The firewall grants access to the server based on the originating IP address of each request.</span></span>
<span data-ttu-id="987b3-106">若要設定您的防火牆，您可以建立防火牆規則，指定可接受的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="987b3-106">To configure your firewall, you create firewall rules that specify ranges of acceptable IP addresses.</span></span> <span data-ttu-id="987b3-107">您可以在伺服器層級建立防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="987b3-107">You can create firewall rules at the server level.</span></span>

<span data-ttu-id="987b3-108">**防火牆規則：**這些規則可讓用戶端完整存取適用於 PostgreSQL 的 Azure 資料庫伺服器，也就是相同邏輯伺服器內的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="987b3-108">**Firewall rules:** These rules enable clients to access your entire Azure Database for PostgreSQL Server, that is, all the databases within the same logical server.</span></span> <span data-ttu-id="987b3-109">使用 Azure 入口網站或使用 Azure CLI 命令，即可設定伺服器層級的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="987b3-109">Server-level firewall rules can be configured by using the Azure portal or using Azure CLI commands.</span></span> <span data-ttu-id="987b3-110">若要建立伺服器層級的防火牆規則，您必須是訂用帳戶擁有者或訂用帳戶參與者。</span><span class="sxs-lookup"><span data-stu-id="987b3-110">To create server-level firewall rules, you must be the subscription owner or a subscription contributor.</span></span>

## <a name="firewall-overview"></a><span data-ttu-id="987b3-111">防火牆概觀</span><span class="sxs-lookup"><span data-stu-id="987b3-111">Firewall overview</span></span>
<span data-ttu-id="987b3-112">根據預設，防火牆會封鎖對適用於 PostgreSQL 之 Azure 資料庫伺服器的所有資料庫存取。</span><span class="sxs-lookup"><span data-stu-id="987b3-112">All database access to your Azure Database for PostgreSQL server is blocked by the firewall by default.</span></span> <span data-ttu-id="987b3-113">若要從其他電腦開始使用您的伺服器，請指定一或多個伺服器層級的防火牆規則，以便啟用對伺服器的存取。</span><span class="sxs-lookup"><span data-stu-id="987b3-113">To begin using your server from another computer, you need to specify one or more server-level firewall rules to enable access to your server.</span></span> <span data-ttu-id="987b3-114">使用防火牆規則，來指定允許從網際網路存取的 IP 位址範圍。</span><span class="sxs-lookup"><span data-stu-id="987b3-114">Use the firewall rules to specify which IP address ranges from the Internet to allow.</span></span> <span data-ttu-id="987b3-115">存取 Azure 入口網站本身，並不會受到防火牆規則所影響。</span><span class="sxs-lookup"><span data-stu-id="987b3-115">Access to the Azure portal website itself is not impacted by the firewall rules.</span></span>
<span data-ttu-id="987b3-116">來自網際網路和 Azure 的連接嘗試必須先通過防火牆，才能到達您的 PostgreSQL 資料庫，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="987b3-116">Connection attempts from the Internet and Azure must first pass through the firewall before they can reach your PostgreSQL Database, as shown in the following diagram:</span></span>

![防火牆運作方式的範例流程](media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-the-internet"></a><span data-ttu-id="987b3-118">從網際網路連線</span><span class="sxs-lookup"><span data-stu-id="987b3-118">Connecting from the Internet</span></span>
<span data-ttu-id="987b3-119">伺服器層級的防火牆規則可套用至適用於 PostgreSQL 之 Azure 資料庫伺服器上的所有資料庫。</span><span class="sxs-lookup"><span data-stu-id="987b3-119">Server-level firewall rules apply to all databases on the Azure Database for PostgreSQL server.</span></span> <span data-ttu-id="987b3-120">如果要求的 IP 位址在伺服器層級防火牆規則中指定的其中一個範圍內，就會允許連線。</span><span class="sxs-lookup"><span data-stu-id="987b3-120">If the IP address of the request is within one of the ranges specified in the server-level firewall rules, the connection is granted.</span></span>
<span data-ttu-id="987b3-121">如果要求的 IP 位址不在任何資料庫層級或伺服器層級防火牆規則中指定的範圍內，連線要求會失敗。</span><span class="sxs-lookup"><span data-stu-id="987b3-121">If the IP address of the request is not within the ranges specified in any of the database-level or server-level firewall rules, the connection request fails.</span></span>
<span data-ttu-id="987b3-122">例如，如果您的應用程式透過適用於 PostgreSQL 的 JDBC 驅動程式來連接，若您在防火牆封鎖連接期間嘗試進行連接，則可能會遇到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="987b3-122">For example, if your application connects with JDBC driver for PostgreSQL, you may encounter this error attempting to connect when the firewall is blocking the connection.</span></span>
> <span data-ttu-id="987b3-123">java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: no pg\_hba.conf entry for host "123.45.67.890", user "adminuser", database "postgresql", SSL</span><span class="sxs-lookup"><span data-stu-id="987b3-123">java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: no pg\_hba.conf entry for host "123.45.67.890", user "adminuser", database "postgresql", SSL</span></span>

## <a name="programmatically-managing-firewall-rules"></a><span data-ttu-id="987b3-124">以程式設計方式管理防火牆規則</span><span class="sxs-lookup"><span data-stu-id="987b3-124">Programmatically managing firewall rules</span></span>
<span data-ttu-id="987b3-125">除了 Azure 入口網站之外，防火牆規則還可以程式設計方式使用 Azure CLI 來管理。</span><span class="sxs-lookup"><span data-stu-id="987b3-125">In addition to the Azure portal, firewall rules can be managed programmatically using Azure CLI.</span></span>
<span data-ttu-id="987b3-126">另請參閱[使用 Azure CLI 建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則](howto-manage-firewall-using-cli.md)。</span><span class="sxs-lookup"><span data-stu-id="987b3-126">See also [Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI](howto-manage-firewall-using-cli.md)</span></span>

## <a name="troubleshooting-the-database-firewall"></a><span data-ttu-id="987b3-127">針對資料庫防火牆問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="987b3-127">Troubleshooting the database firewall</span></span>
<span data-ttu-id="987b3-128">對於適用於 PostgreSQL 的 Microsoft Azure 資料庫伺服器服務的存取未如預期般運作時，請考慮下列幾點：</span><span class="sxs-lookup"><span data-stu-id="987b3-128">Consider the following points when access to the Microsoft Azure Database for PostgreSQL Server service does not behave as you expect:</span></span>

* <span data-ttu-id="987b3-129">**對允許清單的變更尚未生效：**對適用於 PostgreSQL 之 Azure 資料庫伺服器防火牆組態的變更最多可能會延遲 5 分鐘才能生效。</span><span class="sxs-lookup"><span data-stu-id="987b3-129">**Changes to the allow list have not taken effect yet:** There may be as much as a five-minute delay for changes to the Azure Database for PostgreSQL Server firewall configuration to take effect.</span></span>

* <span data-ttu-id="987b3-130">**登入未獲授權或使用不正確的密碼：**如果適用於 PostgreSQL 的 Azure 資料庫伺服器上的登入沒有權限，或使用的密碼不正確，與適用於 PostgreSQL 的 Azure 資料庫伺服器連接就會遭到拒絕。</span><span class="sxs-lookup"><span data-stu-id="987b3-130">**The login is not authorized or an incorrect password was used:** If a login does not have permissions on the Azure Database for PostgreSQL server or the password used is incorrect, the connection to the Azure Database for PostgreSQL server is denied.</span></span> <span data-ttu-id="987b3-131">建立防火牆設定只會讓用戶端有機會嘗試連線至您的伺服器；每個用戶端必須提供必要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="987b3-131">Creating a firewall setting only provides clients with an opportunity to attempt connecting to your server; each client must provide the necessary security credentials.</span></span>

<span data-ttu-id="987b3-132">例如，使用 JDBC 用戶端，可能會出現下列錯誤。</span><span class="sxs-lookup"><span data-stu-id="987b3-132">For example, using a JDBC client, the following error may appear.</span></span>
> <span data-ttu-id="987b3-133">java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: password authentication failed for user "yourusername"</span><span class="sxs-lookup"><span data-stu-id="987b3-133">java.util.concurrent.ExecutionException: java.lang.RuntimeException: org.postgresql.util.PSQLException: FATAL: password authentication failed for user "yourusername"</span></span>

* <span data-ttu-id="987b3-134">**動態 IP 位址：** 如果您有使用動態 IP 位址的網際網路連線，並且在通過防火牆時遇到問題，您可以嘗試下列其中一個解決方案：</span><span class="sxs-lookup"><span data-stu-id="987b3-134">**Dynamic IP address:** If you have an Internet connection with dynamic IP addressing and you are having trouble getting through the firewall, you could try one of the following solutions:</span></span>

* <span data-ttu-id="987b3-135">要求您的網際網路服務提供者 (ISP) 將可存取適用於 PostgreSQL 的 Azure 資料庫伺服器之 IP 位址範圍指派給您的用戶端電腦，然後將 IP 位址範圍新增為防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="987b3-135">Ask your Internet Service Provider (ISP) for the IP address range assigned to your client computers that access the Azure Database for PostgreSQL Server, and then add the IP address range as a firewall rule.</span></span>

* <span data-ttu-id="987b3-136">改為針對您的用戶端電腦取得靜態 IP 位址，然後將 IP 位址新增為防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="987b3-136">Get static IP addressing instead for your client computers, and then add the IP addresses as firewall rules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="987b3-137">後續步驟</span><span class="sxs-lookup"><span data-stu-id="987b3-137">Next steps</span></span>
<span data-ttu-id="987b3-138">如需有關建立伺服器層級和資料庫層級防火牆規則的文章，請參閱：</span><span class="sxs-lookup"><span data-stu-id="987b3-138">For articles on creating server-level and database-level firewall rules, see:</span></span>
* [<span data-ttu-id="987b3-139">使用 Azure 入口網站建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則</span><span class="sxs-lookup"><span data-stu-id="987b3-139">Create and manage Azure Database for PostgreSQL firewall rules using the Azure portal</span></span>](howto-manage-firewall-using-portal.md)
* [<span data-ttu-id="987b3-140">使用 Azure CLI 建立和管理適用於 PostgreSQL 的 Azure 資料庫防火牆規則</span><span class="sxs-lookup"><span data-stu-id="987b3-140">Create and manage Azure Database for PostgreSQL firewall rules using Azure CLI</span></span>](howto-manage-firewall-using-cli.md)