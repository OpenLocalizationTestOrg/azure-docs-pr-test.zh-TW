---
title: "SQL Database 1433 以外的連接埠 | Microsoft Docs"
description: "從 ADO.NET 至 Azure SQL Database 的用戶端連線有時會略過 Proxy 並直接與資料庫互動。 1433 以外的連接埠變得重要。"
services: sql-database
documentationcenter: 
author: MightyPen
manager: jhubbard
editor: 
ms.assetid: 3f17106a-92fd-4aa4-b6a9-1daa29421f64
ms.service: sql-database
ms.custom: develop apps
ms.workload: drivers
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/17/2016
ms.author: sstein
ms.openlocfilehash: d47ee8c794d1e231507dae6bb4aa88bf19ce6418
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="d72dd-104">ADO.NET 4.5 超過 1433 以外的連接埠</span><span class="sxs-lookup"><span data-stu-id="d72dd-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="d72dd-105">本主題針對使用 ADO.NET 4.5 或更新版本的用戶端，說明 Azure SQL Database 的連接行為。</span><span class="sxs-lookup"><span data-stu-id="d72dd-105">This topic describes the Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="d72dd-106">如需連線架構的資訊，請參閱 [Azure SQL Database 連線架構](sql-database-connectivity-architecture.md)。</span><span class="sxs-lookup"><span data-stu-id="d72dd-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="d72dd-107">比較內部與外部</span><span class="sxs-lookup"><span data-stu-id="d72dd-107">Outside vs inside</span></span>
<span data-ttu-id="d72dd-108">對於連到 Azure SQL Database 的連線，必須先了解您的用戶端程式是在 Azure 雲端界限「外部」或「內部」執行。</span><span class="sxs-lookup"><span data-stu-id="d72dd-108">For connections to Azure SQL Database, we must first ask whether your client program runs *outside* or *inside* the Azure cloud boundary.</span></span> <span data-ttu-id="d72dd-109">這些小節將討論兩種常見案例。</span><span class="sxs-lookup"><span data-stu-id="d72dd-109">The subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="d72dd-110">*外部：* 在桌上型電腦上執行的用戶端</span><span class="sxs-lookup"><span data-stu-id="d72dd-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="d72dd-111">連接埠 1433 是裝載您的 SQL Database 用戶端應用程式的桌上型電腦上唯一必須開啟的連接埠。</span><span class="sxs-lookup"><span data-stu-id="d72dd-111">Port 1433 is the only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="d72dd-112">*內部：* 在 Azure 上執行的用戶端</span><span class="sxs-lookup"><span data-stu-id="d72dd-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="d72dd-113">當您的用戶端是在 Azure 雲端界限內部執行時，它會使用我們可以稱為 *直接路由* 的路由與 SQL Database 伺服器互動。</span><span class="sxs-lookup"><span data-stu-id="d72dd-113">When your client runs inside the Azure cloud boundary, it uses what we can call a *direct route* to interact with the SQL Database server.</span></span> <span data-ttu-id="d72dd-114">建立連線之後，用戶端和資料庫之間的進一步互動未牽涉到任何中介軟體 proxy。</span><span class="sxs-lookup"><span data-stu-id="d72dd-114">After a connection is established, further interactions between the client and database involve no middleware proxy.</span></span>

<span data-ttu-id="d72dd-115">順序如下：</span><span class="sxs-lookup"><span data-stu-id="d72dd-115">The sequence is as follows:</span></span>

1. <span data-ttu-id="d72dd-116">ADO.NET 4.5 (或更新版本) 會起始與 Azure 雲端的簡短互動，並且接收動態已識別的連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="d72dd-116">ADO.NET 4.5 (or later) initiates a brief interaction with the Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="d72dd-117">動態識別的連接埠號碼範圍為 11000-11999 或 14000-14999。</span><span class="sxs-lookup"><span data-stu-id="d72dd-117">The dynamically identified port number is in the range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="d72dd-118">然後 ADO.NET 會直接連線到 SQL Database 伺服器，中間沒有中介軟體。</span><span class="sxs-lookup"><span data-stu-id="d72dd-118">ADO.NET then connects to the SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="d72dd-119">查詢會直接傳送到資料庫，結果會直接傳回至用戶端。</span><span class="sxs-lookup"><span data-stu-id="d72dd-119">Queries are sent directly to the database, and results are returned directly to the client.</span></span>

<span data-ttu-id="d72dd-120">請確定已保留 Azure 用戶端電腦上的 11000-11999 及 14000-14999 連接埠範圍，以供 ADO.NET 4.5 用戶端與 SQL Database 進行互動使用。</span><span class="sxs-lookup"><span data-stu-id="d72dd-120">Ensure that the port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="d72dd-121">特別是範圍中的連接埠必須沒有其他任何輸出封鎖器。</span><span class="sxs-lookup"><span data-stu-id="d72dd-121">In particular, ports in the range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="d72dd-122">在您的 Azure VM 上， **具有進階安全性的 Windows 防火牆** 會控制此連接埠設定。</span><span class="sxs-lookup"><span data-stu-id="d72dd-122">On your Azure VM, the **Windows Firewall with Advanced Security** controls the port settings.</span></span>
  
  * <span data-ttu-id="d72dd-123">您可以使用[防火牆的使用者介面](http://msdn.microsoft.com/library/cc646023.aspx)來新增規則，其中您可使用如 **11000-11999** 的語法指定 **TCP** 通訊協定和連接埠範圍。</span><span class="sxs-lookup"><span data-stu-id="d72dd-123">You can use the [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) to add a rule for which you specify the **TCP** protocol along with a port range with the syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="d72dd-124">版本說明</span><span class="sxs-lookup"><span data-stu-id="d72dd-124">Version clarifications</span></span>
<span data-ttu-id="d72dd-125">本章節將釐清參考產品版本的 Moniker。</span><span class="sxs-lookup"><span data-stu-id="d72dd-125">This section clarifies the monikers that refer to product versions.</span></span> <span data-ttu-id="d72dd-126">它也會列出產品之間的一些版本配對。</span><span class="sxs-lookup"><span data-stu-id="d72dd-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="d72dd-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="d72dd-127">ADO.NET</span></span>
* <span data-ttu-id="d72dd-128">ADO.NET 4.0 支援 TDS 7.3 通訊協定，但不支援 7.4。</span><span class="sxs-lookup"><span data-stu-id="d72dd-128">ADO.NET 4.0 supports the TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="d72dd-129">ADO.NET 4.5 和更新版本支援 TDS 7.4 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="d72dd-129">ADO.NET 4.5 and later supports the TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="d72dd-130">相關連結</span><span class="sxs-lookup"><span data-stu-id="d72dd-130">Related links</span></span>
* <span data-ttu-id="d72dd-131">ADO.NET 4.6 於 2015 年 7 月 20 日發行。</span><span class="sxs-lookup"><span data-stu-id="d72dd-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="d72dd-132">您可以在 [這裡](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx)查看 .NET 小組的部落格公告。</span><span class="sxs-lookup"><span data-stu-id="d72dd-132">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="d72dd-133">ADO.NET 4.5 於 2012 年 8 月 15 日發行。</span><span class="sxs-lookup"><span data-stu-id="d72dd-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="d72dd-134">您可以在 [這裡](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx)查看 .NET 小組的部落格公告。</span><span class="sxs-lookup"><span data-stu-id="d72dd-134">A blog announcement from the .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="d72dd-135">您可以在 [這裡](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx)查看有關 ADO.NET 4.5.1 的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="d72dd-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="d72dd-136">TDS 通訊協定版本清單</span><span class="sxs-lookup"><span data-stu-id="d72dd-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="d72dd-137">SQL Database 開發概觀</span><span class="sxs-lookup"><span data-stu-id="d72dd-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="d72dd-138">Azure SQL Database 防火牆</span><span class="sxs-lookup"><span data-stu-id="d72dd-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="d72dd-139">如何：在 SQL Database 上進行防火牆設定</span><span class="sxs-lookup"><span data-stu-id="d72dd-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

