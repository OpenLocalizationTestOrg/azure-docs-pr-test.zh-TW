---
title: "適用於 MySQL 的 Azure 資料庫的 SSL 連線能力 | Microsoft Docs"
description: "用以設定適用於 MySQL 之 Azure 資料庫及相關聯應用程式以適當使用 SSL 連接的資訊"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 4b03b3a2dbfad92cc0cfa84777b38ddff90452cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="4b56a-103">適用於 MySQL 的 Azure 資料庫中的 SSL 連線能力</span><span class="sxs-lookup"><span data-stu-id="4b56a-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="4b56a-104">適用於 MySQL 的 Azure 資料庫支援使用安全通訊端層 (SSL)，將資料庫伺服器連接至用戶端應用程式。</span><span class="sxs-lookup"><span data-stu-id="4b56a-104">Azure Database for MySQL supports connecting your database server to client applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="4b56a-105">在您的資料庫伺服器和用戶端應用程式之間強制執行 SSL 連接，有助於藉由將伺服器與您應用程式之間的資料流加密，來提供保護以抵禦「中間人」攻擊。</span><span class="sxs-lookup"><span data-stu-id="4b56a-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in the middle" attacks by encrypting the data stream between the server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="4b56a-106">預設設定</span><span class="sxs-lookup"><span data-stu-id="4b56a-106">Default settings</span></span>
<span data-ttu-id="4b56a-107">根據預設，資料庫服務應該會設定為在連接至 MySQL時需要 SSL 連接。</span><span class="sxs-lookup"><span data-stu-id="4b56a-107">By default, the database service should be configured to require SSL connections when connecting to MySQL.</span></span>  <span data-ttu-id="4b56a-108">我們建議盡可能避免停用 SSL 選項。</span><span class="sxs-lookup"><span data-stu-id="4b56a-108">It is recommended avoid disabling the SSL option whenever possible.</span></span> 

<span data-ttu-id="4b56a-109">透過 Azure 入口網站和 CLI 佈建新的適用於 MySQL 的 Azure 資料庫伺服器時，預設會強制執行 SSL 連接。</span><span class="sxs-lookup"><span data-stu-id="4b56a-109">When provisioning a new Azure Database for MySQL server through the Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="4b56a-110">同樣地，您在 Azure 入口網站的伺服器下方 [連接字串] 設定中預先定義的連接字串，會包含通用語言使用 SSL 連接到您資料庫伺服器所需的必要參數。</span><span class="sxs-lookup"><span data-stu-id="4b56a-110">Likewise, connection strings that are pre-defined in the "Connection Strings" settings under your server in the Azure portal include the required parameters for common languages to connect to your database server using SSL.</span></span> <span data-ttu-id="4b56a-111">SSL 參數會根據連接器而有所不同，例如，"ssl=true" 或 "sslmode=require" 或 "sslmode=required" 及其他變化。</span><span class="sxs-lookup"><span data-stu-id="4b56a-111">The SSL parameter varies based on the connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="4b56a-112">若要了解如何在開發應用程式時啟用或停用 SSL 連接，請參閱[如何設定 SSL](howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="4b56a-112">To learn how to enable or disable SSL connection when developing application, please refer to [How to configure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4b56a-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4b56a-113">Next steps</span></span>
[<span data-ttu-id="4b56a-114">適用於 MySQL 的 Azure 資料庫的連線庫</span><span class="sxs-lookup"><span data-stu-id="4b56a-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
