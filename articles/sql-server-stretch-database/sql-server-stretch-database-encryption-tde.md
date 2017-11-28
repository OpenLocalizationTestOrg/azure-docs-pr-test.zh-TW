---
title: "透明資料加密，以使用 Stretch Database-Azure aaaEnable |Microsoft 文件"
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
ms.openlocfilehash: 1d6bff455030ac8851b2184c1e8097afd61361d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-transparent-data-encryption-tde-for-stretch-database-on-azure"></a><span data-ttu-id="ab4f6-103">為 Azure 上的 Stretch Database 啟用透明資料加密 (TDE)</span><span class="sxs-lookup"><span data-stu-id="ab4f6-103">Enable Transparent Data Encryption (TDE) for Stretch Database on Azure</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="ab4f6-104">Azure 入口網站</span><span class="sxs-lookup"><span data-stu-id="ab4f6-104">Azure portal</span></span>](sql-server-stretch-database-encryption-tde.md)
> * [<span data-ttu-id="ab4f6-105">TSQL</span><span class="sxs-lookup"><span data-stu-id="ab4f6-105">TSQL</span></span>](sql-server-stretch-database-tde-tsql.md)
>
>

<span data-ttu-id="ab4f6-106">透明資料加密 (TDE) 可協助防範惡意活動的 hello 威脅，藉由執行 hello 資料庫、 相關聯的備份和靜止的交易記錄檔的即時加密與解密，而不需要變更 toohello應用程式。</span><span class="sxs-lookup"><span data-stu-id="ab4f6-106">Transparent Data Encryption (TDE) helps protect against hello threat of malicious activity by performing real-time encryption and decryption of hello database, associated backups, and transaction log files at rest without requiring changes toohello application.</span></span>

<span data-ttu-id="ab4f6-107">TDE 會使用對稱金鑰的呼叫的 hello 資料庫加密金鑰將整個資料庫的 hello 儲存體。</span><span class="sxs-lookup"><span data-stu-id="ab4f6-107">TDE encrypts hello storage of an entire database by using a symmetric key called hello database encryption key.</span></span> <span data-ttu-id="ab4f6-108">hello 資料庫加密金鑰受到由內建的伺服器憑證。</span><span class="sxs-lookup"><span data-stu-id="ab4f6-108">hello database encryption key is protected by a built-in server certificate.</span></span> <span data-ttu-id="ab4f6-109">hello 內建伺服器憑證是唯一的每個 Azure 伺服器。</span><span class="sxs-lookup"><span data-stu-id="ab4f6-109">hello built-in server certificate is unique for each Azure server.</span></span> <span data-ttu-id="ab4f6-110">Microsoft 至少每 90 天會自動替換這些憑證。</span><span class="sxs-lookup"><span data-stu-id="ab4f6-110">Microsoft automatically rotates these certificates at least every 90 days.</span></span> <span data-ttu-id="ab4f6-111">如需 TDE 的一般描述，請參閱 [透明資料加密 (TDE)]。</span><span class="sxs-lookup"><span data-stu-id="ab4f6-111">For a general description of TDE, see [Transparent Data Encryption (TDE)].</span></span>

## <a name="enabling-encryption"></a><span data-ttu-id="ab4f6-112">啟用加密</span><span class="sxs-lookup"><span data-stu-id="ab4f6-112">Enabling Encryption</span></span>
<span data-ttu-id="ab4f6-113">正在儲存從已啟用 Stretch 的 SQL Server 資料庫，移轉資料的 hello Azure 資料庫的 TDE tooenable hello 下列事項：</span><span class="sxs-lookup"><span data-stu-id="ab4f6-113">tooenable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="ab4f6-114">開啟 hello 資料庫在 hello [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ab4f6-114">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="ab4f6-115">在 hello 資料庫刀鋒視窗中，按一下 hello**設定**按鈕</span><span class="sxs-lookup"><span data-stu-id="ab4f6-115">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="ab4f6-116">選取 hello**透明資料加密**選項![][1]</span><span class="sxs-lookup"><span data-stu-id="ab4f6-116">Select hello **Transparent data encryption** option ![][1]</span></span>
4. <span data-ttu-id="ab4f6-117">選取 hello**上**設定，然後再選取**儲存**
   ![][2]</span><span class="sxs-lookup"><span data-stu-id="ab4f6-117">Select hello **On** setting, and then select **Save**
![][2]</span></span>

## <a name="disabling-encryption"></a><span data-ttu-id="ab4f6-118">停用加密</span><span class="sxs-lookup"><span data-stu-id="ab4f6-118">Disabling Encryption</span></span>
<span data-ttu-id="ab4f6-119">正在儲存從已啟用 Stretch 的 SQL Server 資料庫，移轉資料的 hello Azure 資料庫的 TDE toodisable hello 下列事項：</span><span class="sxs-lookup"><span data-stu-id="ab4f6-119">toodisable TDE for an Azure database that's storing hello data migrated from a Stretch-enabled SQL Server database, do hello following things:</span></span>

1. <span data-ttu-id="ab4f6-120">開啟 hello 資料庫在 hello [Azure 入口網站](https://portal.azure.com)</span><span class="sxs-lookup"><span data-stu-id="ab4f6-120">Open hello database in hello [Azure portal](https://portal.azure.com)</span></span>
2. <span data-ttu-id="ab4f6-121">在 hello 資料庫刀鋒視窗中，按一下 hello**設定**按鈕</span><span class="sxs-lookup"><span data-stu-id="ab4f6-121">In hello database blade, click hello **Settings** button</span></span>
3. <span data-ttu-id="ab4f6-122">選取 hello**透明資料加密**選項</span><span class="sxs-lookup"><span data-stu-id="ab4f6-122">Select hello **Transparent data encryption** option</span></span>
4. <span data-ttu-id="ab4f6-123">選取 hello**關閉**設定，然後再選取**儲存**</span><span class="sxs-lookup"><span data-stu-id="ab4f6-123">Select hello **Off** setting, and then select **Save**</span></span>

<!--Anchors-->
[透明資料加密 (TDE)]: https://msdn.microsoft.com/library/bb934049.aspx


<!--Image references-->
[1]: ./media/sql-server-stretch-database-encryption-tde/stretchtde1.png
[2]: ./media/sql-server-stretch-database-encryption-tde/stretchtde2.png


<!--Link references-->
