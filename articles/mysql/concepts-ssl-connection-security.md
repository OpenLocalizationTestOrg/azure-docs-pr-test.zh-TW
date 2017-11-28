---
title: "Azure 資料庫的 MySQL aaaSSL 連線 |Microsoft 文件"
description: "設定 MySQL 和相關聯的應用程式 tooproperly 的 Azure 資料庫的資訊，請使用 SSL 連線"
services: mysql
author: JasonMAnderson
ms.author: janders
editor: jasonwhowell
manager: jhubbard
ms.service: mysql-database
ms.topic: article
ms.date: 05/10/2017
ms.openlocfilehash: 6fca7c88fc0f1fd6058d68fcff90fd409abd97a7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ssl-connectivity-in-azure-database-for-mysql"></a><span data-ttu-id="5a496-103">適用於 MySQL 的 Azure 資料庫中的 SSL 連線能力</span><span class="sxs-lookup"><span data-stu-id="5a496-103">SSL connectivity in Azure Database for MySQL</span></span>
<span data-ttu-id="5a496-104">Azure 的 MySQL 資料庫支援連接資料庫伺服器 tooclient 應用程式使用安全通訊端層 (SSL)。</span><span class="sxs-lookup"><span data-stu-id="5a496-104">Azure Database for MySQL supports connecting your database server tooclient applications using Secure Sockets Layer (SSL).</span></span> <span data-ttu-id="5a496-105">強制執行您的資料庫伺服器和用戶端應用程式之間的 SSL 連線有助於保護 「 攔截 hello 中間 」 攻擊加密 hello hello 伺服器與您的應用程式之間的資料流。</span><span class="sxs-lookup"><span data-stu-id="5a496-105">Enforcing SSL connections between your database server and your client applications helps protect against "man in hello middle" attacks by encrypting hello data stream between hello server and your application.</span></span>

## <a name="default-settings"></a><span data-ttu-id="5a496-106">預設設定</span><span class="sxs-lookup"><span data-stu-id="5a496-106">Default settings</span></span>
<span data-ttu-id="5a496-107">根據預設，連接 tooMySQL 時 hello 資料庫服務時，應該是設定的 toorequire SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="5a496-107">By default, hello database service should be configured toorequire SSL connections when connecting tooMySQL.</span></span>  <span data-ttu-id="5a496-108">我們建議您避免停用盡可能 hello SSL 選項。</span><span class="sxs-lookup"><span data-stu-id="5a496-108">It is recommended avoid disabling hello SSL option whenever possible.</span></span> 

<span data-ttu-id="5a496-109">佈建時 MySQL 伺服器 hello Azure 入口網站透過新的 Azure 資料庫和 CLI，預設會啟用強制的 SSL 連線。</span><span class="sxs-lookup"><span data-stu-id="5a496-109">When provisioning a new Azure Database for MySQL server through hello Azure portal and CLI, enforcement of SSL connections is enabled by default.</span></span> 

<span data-ttu-id="5a496-110">同樣地，hello hello Azure 入口網站中的伺服器 下的 「 連接字串 」 設定中預先定義的連接字串包含通用語言 tooconnect tooyour 的資料庫伺服器使用 SSL 的 hello 必要參數。</span><span class="sxs-lookup"><span data-stu-id="5a496-110">Likewise, connection strings that are pre-defined in hello "Connection Strings" settings under your server in hello Azure portal include hello required parameters for common languages tooconnect tooyour database server using SSL.</span></span> <span data-ttu-id="5a496-111">hello SSL 參數而異 hello 連接器，例如"ssl = true"或"sslmode = 需要"或"sslmode = 必要 」 和其他變化。</span><span class="sxs-lookup"><span data-stu-id="5a496-111">hello SSL parameter varies based on hello connector, for example "ssl=true" or "sslmode=require" or "sslmode=required" and other variations.</span></span>

<span data-ttu-id="5a496-112">如何 tooenable 或停用 SSL 連線開發應用程式時，請參閱太 toolearn[如何 tooconfigure SSL](howto-configure-ssl.md)。</span><span class="sxs-lookup"><span data-stu-id="5a496-112">toolearn how tooenable or disable SSL connection when developing application, please refer too[How tooconfigure SSL](howto-configure-ssl.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a496-113">後續步驟</span><span class="sxs-lookup"><span data-stu-id="5a496-113">Next steps</span></span>
[<span data-ttu-id="5a496-114">適用於 MySQL 的 Azure 資料庫的連線庫</span><span class="sxs-lookup"><span data-stu-id="5a496-114">Connection libraries for Azure Database for MySQL</span></span>](concepts-connection-libraries.md)
