---
title: "aaaAzure 資料庫的 MySQL 伺服器防火牆規則 |Microsoft 文件"
description: "描述適用於 MySQL 的 Azure 資料庫伺服器防火牆規則。"
services: mysql
author: v-chenyh
ms.author: v-chenyh
manager: jhubbard
editor: jasonwhowell
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 1f85310385da947b6c492aa6aa21c1b885c2a97d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-database-for-mysql-server-firewall-rules"></a><span data-ttu-id="b126f-103">適用於 MySQL 的 Azure 資料庫伺服器防火牆規則</span><span class="sxs-lookup"><span data-stu-id="b126f-103">Azure Database for MySQL server firewall rules</span></span>
<span data-ttu-id="b126f-104">防火牆會阻止所有存取 tooyour 資料庫伺服器，直到您指定哪些電腦有權限。</span><span class="sxs-lookup"><span data-stu-id="b126f-104">Firewalls prevent all access tooyour database server until you specify which computers have permission.</span></span> <span data-ttu-id="b126f-105">hello 防火牆會授與存取 toohello 伺服器 hello 來自每個要求的 IP 位址為基礎。</span><span class="sxs-lookup"><span data-stu-id="b126f-105">hello firewall grants access toohello server based on hello originating IP address of each request.</span></span>

<span data-ttu-id="b126f-106">tooconfigure 防火牆，您會建立指定的可接受的 IP 位址範圍的防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="b126f-106">tooconfigure your firewall, you create firewall rules that specify ranges of acceptable IP addresses.</span></span> <span data-ttu-id="b126f-107">您可以在 hello 伺服器層級建立防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="b126f-107">You can create firewall rules at hello server level.</span></span>

<span data-ttu-id="b126f-108">**防火牆規則：**這些規則可讓用戶端 tooaccess 整個 Azure 資料庫的 MySQL server，也就是所有都 hello 資料庫都 hello 相同邏輯伺服器。</span><span class="sxs-lookup"><span data-stu-id="b126f-108">**Firewall rules:** These rules enable clients tooaccess your entire Azure Database for MySQL server, that is, all hello databases within hello same logical server.</span></span> <span data-ttu-id="b126f-109">藉由使用 hello Azure 入口網站，或使用 Azure CLI 命令，可以設定伺服器層級防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="b126f-109">Server-level firewall rules can be configured by using hello Azure portal or using Azure CLI commands.</span></span> <span data-ttu-id="b126f-110">toocreate 伺服器層級防火牆規則，您必須是 hello 訂用帳戶擁有者或訂閱參與者。</span><span class="sxs-lookup"><span data-stu-id="b126f-110">toocreate server-level firewall rules, you must be hello subscription owner or a subscription contributor.</span></span>

## <a name="firewall-overview"></a><span data-ttu-id="b126f-111">防火牆概觀</span><span class="sxs-lookup"><span data-stu-id="b126f-111">Firewall overview</span></span>
<span data-ttu-id="b126f-112">Hello 防火牆封鎖 MySQL 伺服器的所有資料庫存取 tooyour Azure 資料庫的預設值。</span><span class="sxs-lookup"><span data-stu-id="b126f-112">All database access tooyour Azure Database for MySQL server is blocked by hello firewall by default.</span></span> <span data-ttu-id="b126f-113">toobegin 使用您的伺服器從另一部電腦，您需要 toospecify 其中一個或多伺服器層級防火牆規則 tooenable 存取 tooyour 伺服器。</span><span class="sxs-lookup"><span data-stu-id="b126f-113">toobegin using your server from another computer, you need toospecify one or more server-level firewall rules tooenable access tooyour server.</span></span> <span data-ttu-id="b126f-114">使用的 IP 位址範圍是從 hello 網際網路 tooallow hello 防火牆規則 toospecify。</span><span class="sxs-lookup"><span data-stu-id="b126f-114">Use hello firewall rules toospecify which IP address ranges from hello Internet tooallow.</span></span> <span data-ttu-id="b126f-115">存取 toohello Azure 入口網站本身不會受到 hello 防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="b126f-115">Access toohello Azure portal website itself is not impacted by hello firewall rules.</span></span>

<span data-ttu-id="b126f-116">從連線嘗試 hello 網際網路和 Azure 必須先通過 hello 防火牆才能到達您的 Azure 資料庫的 MySQL 資料庫，如下列圖表中的 hello 中所示：</span><span class="sxs-lookup"><span data-stu-id="b126f-116">Connection attempts from hello Internet and Azure must first pass through hello firewall before they can reach your Azure Database for MySQL database, as shown in hello following diagram:</span></span>

![範例流程的 hello 防火牆的運作方式](./media/concepts-firewall-rules/1-firewall-concept.png)

## <a name="connecting-from-hello-internet"></a><span data-ttu-id="b126f-118">從 hello 網際網路連線</span><span class="sxs-lookup"><span data-stu-id="b126f-118">Connecting from hello Internet</span></span>
<span data-ttu-id="b126f-119">伺服器層級防火牆規則套用 tooall 資料庫上的 MySQL 伺服器 hello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b126f-119">Server-level firewall rules apply tooall databases on hello Azure Database for MySQL server.</span></span>

<span data-ttu-id="b126f-120">如果 hello 要求 hello IP 位址是其中一個 hello hello 伺服器層級防火牆規則中指定的範圍內，會授與 hello 連線。</span><span class="sxs-lookup"><span data-stu-id="b126f-120">If hello IP address of hello request is within one of hello ranges specified in hello server-level firewall rules, hello connection is granted.</span></span>

<span data-ttu-id="b126f-121">如果 hello 要求 hello IP 位址不在任何 hello 資料庫層級中指定 hello 範圍或伺服器層級防火牆規則，hello 連接要求會失敗。</span><span class="sxs-lookup"><span data-stu-id="b126f-121">If hello IP address of hello request is not within hello ranges specified in any of hello database-level or server-level firewall rules, hello connection request fails.</span></span>

## <a name="programmatically-managing-firewall-rules"></a><span data-ttu-id="b126f-122">以程式設計方式管理防火牆規則</span><span class="sxs-lookup"><span data-stu-id="b126f-122">Programmatically managing firewall rules</span></span>
<span data-ttu-id="b126f-123">除了以程式設計方式使用 Azure CLI toohello Azure 入口網站中，防火牆規則可以是所管理。</span><span class="sxs-lookup"><span data-stu-id="b126f-123">In addition toohello Azure portal, firewall rules can be managed programmatically using Azure CLI.</span></span> <span data-ttu-id="b126f-124">另請參閱[使用 Azure CLI 建立和管理適用於 MySQL 的 Azure 資料庫防火牆規則](./howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b126f-124">See also [Create and manage Azure Database for MySQL firewall rules using Azure CLI](./howto-manage-firewall-using-cli.md)</span></span>

## <a name="troubleshooting-hello-database-firewall"></a><span data-ttu-id="b126f-125">疑難排解 hello database 防火牆</span><span class="sxs-lookup"><span data-stu-id="b126f-125">Troubleshooting hello database firewall</span></span>
<span data-ttu-id="b126f-126">請考慮 hello 時存取 toohello Microsoft Azure 資料庫的 MySQL server 服務未如預期般運作，下列點：</span><span class="sxs-lookup"><span data-stu-id="b126f-126">Consider hello following points when access toohello Microsoft Azure Database for MySQL server service does not behave as you expect:</span></span>

* <span data-ttu-id="b126f-127">**變更 toohello 允許清單有尚未生效：**可能會如往常般的五分鐘延遲變更 MySQL 伺服器的防火牆組態 tootake 效果 toohello Azure 資料庫。</span><span class="sxs-lookup"><span data-stu-id="b126f-127">**Changes toohello allow list have not taken effect yet:** There may be as much as a five-minute delay for changes toohello Azure Database for MySQL Server firewall configuration tootake effect.</span></span>

* <span data-ttu-id="b126f-128">**hello 登入未獲授權，或使用不正確的密碼：**登入沒有權限 hello Azure 資料庫上使用的 MySQL 伺服器或 hello 密碼不正確，如果 hello 連接 toohello Azure 資料庫的 MySQL 伺服器遭拒。</span><span class="sxs-lookup"><span data-stu-id="b126f-128">**hello login is not authorized or an incorrect password was used:** If a login does not have permissions on hello Azure Database for MySQL server or hello password used is incorrect, hello connection toohello Azure Database for MySQL server is denied.</span></span> <span data-ttu-id="b126f-129">建立防火牆設定只提供連接 tooyour 伺服器; 機會 tooattempt 用戶端每個用戶端必須提供 hello 必要的安全性認證。</span><span class="sxs-lookup"><span data-stu-id="b126f-129">Creating a firewall setting only provides clients with an opportunity tooattempt connecting tooyour server; each client must provide hello necessary security credentials.</span></span>

* <span data-ttu-id="b126f-130">**動態 IP 位址：**如果您有使用動態 IP 位址的網際網路連線，並且在經由 hello 防火牆時遇到，您可以嘗試下列解決方案 hello 的其中一個：</span><span class="sxs-lookup"><span data-stu-id="b126f-130">**Dynamic IP address:** If you have an Internet connection with dynamic IP addressing and you are having trouble getting through hello firewall, you could try one of hello following solutions:</span></span>

* <span data-ttu-id="b126f-131">要求網際網路服務提供者 (ISP) hello IP 位址範圍指派 tooyour 用戶端電腦的 MySQL server，該存取 hello Azure 資料庫，然後將 hello IP 位址範圍新增為防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="b126f-131">Ask your Internet Service Provider (ISP) for hello IP address range assigned tooyour client computers that access hello Azure Database for MySQL server, and then add hello IP address range as a firewall rule.</span></span>

* <span data-ttu-id="b126f-132">取得靜態 IP 位址改為您的用戶端電腦，然後將 hello IP 位址新增為防火牆規則。</span><span class="sxs-lookup"><span data-stu-id="b126f-132">Get static IP addressing instead for your client computers, and then add hello IP addresses as firewall rules.</span></span>

## <a name="next-steps"></a><span data-ttu-id="b126f-133">後續步驟</span><span class="sxs-lookup"><span data-stu-id="b126f-133">Next steps</span></span>

<span data-ttu-id="b126f-134">[建立和管理 MySQL 防火牆規則使用 hello Azure 入口網站的 Azure 資料庫](./howto-manage-firewall-using-portal.md)
[建立及管理 Azure 資料庫使用 Azure CLI MySQL 防火牆規則](./howto-manage-firewall-using-cli.md)</span><span class="sxs-lookup"><span data-stu-id="b126f-134">[Create and manage Azure Database for MySQL firewall rules using hello Azure portal](./howto-manage-firewall-using-portal.md)
[Create and manage Azure Database for MySQL firewall rules using Azure CLI](./howto-manage-firewall-using-cli.md)</span></span>
