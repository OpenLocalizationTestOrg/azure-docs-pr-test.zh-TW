---
title: "為 Stretch Database 啟用透明資料加密- Azure | Microsoft Docs"
description: "為 Azure 上的 SQL Server Stretch Database 啟用透明資料加密 (TDE)"
services: sql-server-stretch-database
documentationcenter: 
author: douglaslMS
manager: barbkess
editor: 
ms.assetid: a44ed8f5-b416-4c41-9b1e-b7271f10bdc3
ms.service: sql-server-stretch-database
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/14/2016
ms.author: douglasl
ms.openlocfilehash: ceb355d2ba872ed5d3886c6dc82ca75b1854db0a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="aed6b-103">為 Azure 上的 Stretch Database 啟用透明資料加密 (TDE)</span><span class="sxs-lookup"><span data-stu-id="aed6b-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aed6b-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="aed6b-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="aed6b-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="aed6b-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="aed6b-106">透明資料加密 (TDE) 可在不需變更應用程式的情況下，對靜止的資料庫、相關聯的備份和交易記錄檔執行即時加密和解密，協助防止惡意活動的威脅。</span><span class="sxs-lookup"><span data-stu-id="aed6b-106">Transparent Data Encryption (TDE) helps protect against the threat of malicious activity by performing real-time encryption and decryption of the database, associated backups, and transaction log files at rest without requiring changes to the application.</span></span>

<span data-ttu-id="aed6b-107">TDE 會使用稱為資料庫加密金鑰的對稱金鑰來加密整個資料庫的儲存體。</span><span class="sxs-lookup"><span data-stu-id="aed6b-107">TDE encrypts the storage of an entire database by using a symmetric key called the database encryption key.</span></span> <span data-ttu-id="aed6b-108">資料庫加密金鑰是由內建伺服器憑證保護。</span><span class="sxs-lookup"><span data-stu-id="aed6b-108">The database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="aed6b-109">內建伺服器憑證對每個 Azure 伺服器都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="aed6b-109">The built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="aed6b-110">Microsoft 至少每 90 天會自動替換這些憑證。</span><span class="sxs-lookup"><span data-stu-id="aed6b-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="aed6b-111">如需 TDE 的一般描述，請參閱 [透明資料加密 (TDE)]。</span><span class="sxs-lookup"><span data-stu-id="aed6b-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="aed6b-112">啟用加密</span><span class="sxs-lookup"><span data-stu-id="aed6b-112">Enabling Encryption</span></span>
<span data-ttu-id="aed6b-113">若要為 Azure 資料庫 (儲存從已啟用 Stretch 之 SQL Server 料庫移轉的資料) 啟用 TDE，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="aed6b-113">To enable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="aed6b-114">在 [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="aed6b-114">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="aed6b-115">在資料庫刀鋒視窗中，按一下 [設定]  按鈕</span><span class="sxs-lookup"><span data-stu-id="aed6b-115">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="aed6b-116">選取 [透明資料加密]  選項 ![][1]</span><span class="sxs-lookup"><span data-stu-id="aed6b-116">Select the **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="aed6b-117">選取 **[開啟]** 設定，然後選取 **[儲存]**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="aed6b-117">Select the **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="aed6b-118">停用加密</span><span class="sxs-lookup"><span data-stu-id="aed6b-118">Disabling Encryption</span></span>
<span data-ttu-id="aed6b-119">若要為 Azure 資料庫 (儲存從已啟用 Stretch 之 SQL Server 料庫移轉的資料) 停用 TDE，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="aed6b-119">To disable TDE for an Azure database that's storing the data migrated from a Stretch-enabled SQL Server database, do the following things:</span></span>

1. <span data-ttu-id="aed6b-120">在 [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="aed6b-120">Open the database in the [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="aed6b-121">在資料庫刀鋒視窗中，按一下 [設定]  按鈕</span><span class="sxs-lookup"><span data-stu-id="aed6b-121">In the database blade, click the **Settings** button</span></span>
3. <span data-ttu-id="aed6b-122">選取 [透明資料加密]  選項</span><span class="sxs-lookup"><span data-stu-id="aed6b-122">Select the **Transparent data encryption** option</span></span>
4. <span data-ttu-id="aed6b-123">選取 [關閉] 設定，然後選取 [儲存]</span><span class="sxs-lookup"><span data-stu-id="aed6b-123">Select the **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
<span data-ttu-id="aed6b-124">[透明資料加密 (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span><span class="sxs-lookup"><span data-stu-id="aed6b-124">[Transparent Data Encryption (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx</span></span>


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
