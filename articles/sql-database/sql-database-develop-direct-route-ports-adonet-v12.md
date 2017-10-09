---
title: "超過 SQL database 1433 aaaPorts |Microsoft 文件"
description: "從 ADO.NET tooAzure SQL Database 的用戶端連接有時會略過 hello proxy，並與 hello 資料庫直接互動。 1433 以外的連接埠變得重要。"
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
ms.openlocfilehash: a35ff2d827ae3fa29b3ea855dbb7ed78583c82eb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="ports-beyond-1433-for-adonet-45"></a><span data-ttu-id="97329-104">ADO.NET 4.5 超過 1433 以外的連接埠</span><span class="sxs-lookup"><span data-stu-id="97329-104">Ports beyond 1433 for ADO.NET 4.5</span></span>
<span data-ttu-id="97329-105">本主題描述使用 ADO.NET 4.5 或更新版本的用戶端 hello Azure SQL Database 連接行為。</span><span class="sxs-lookup"><span data-stu-id="97329-105">This topic describes hello Azure SQL Database connection behavior for clients that use ADO.NET 4.5 or a later version.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="97329-106">如需連線架構的資訊，請參閱 [Azure SQL Database 連線架構](sql-database-connectivity-architecture.md)。</span><span class="sxs-lookup"><span data-stu-id="97329-106">For information about connectivity architecture, see [Azure SQL Database connectivity architecture](sql-database-connectivity-architecture.md).</span></span>
>

## <a name="outside-vs-inside"></a><span data-ttu-id="97329-107">比較內部與外部</span><span class="sxs-lookup"><span data-stu-id="97329-107">Outside vs inside</span></span>
<span data-ttu-id="97329-108">針對連接 tooAzure SQL 資料庫，我們必須先詢問是否要執行用戶端程式*外*或*內*hello Azure 雲端界限。</span><span class="sxs-lookup"><span data-stu-id="97329-108">For connections tooAzure SQL Database, we must first ask whether your client program runs *outside* or *inside* hello Azure cloud boundary.</span></span> <span data-ttu-id="97329-109">hello 各節將討論兩個常見的案例。</span><span class="sxs-lookup"><span data-stu-id="97329-109">hello subsections discuss two common scenarios.</span></span>

#### <a name="outside-client-runs-on-your-desktop-computer"></a><span data-ttu-id="97329-110">*外部：* 在桌上型電腦上執行的用戶端</span><span class="sxs-lookup"><span data-stu-id="97329-110">*Outside:* Client runs on your desktop computer</span></span>
<span data-ttu-id="97329-111">通訊埠 1433年是必須在裝載 SQL 資料庫用戶端應用程式的桌上型電腦上開啟 hello 唯一連接埠。</span><span class="sxs-lookup"><span data-stu-id="97329-111">Port 1433 is hello only port that must be open on your desktop computer that hosts your SQL Database client application.</span></span>

#### <a name="inside-client-runs-on-azure"></a><span data-ttu-id="97329-112">*內部：* 在 Azure 上執行的用戶端</span><span class="sxs-lookup"><span data-stu-id="97329-112">*Inside:* Client runs on Azure</span></span>
<span data-ttu-id="97329-113">當您的用戶端執行 hello Azure 雲端界限內時，它會使用我們可以呼叫*直接路由*toointeract 與 hello SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="97329-113">When your client runs inside hello Azure cloud boundary, it uses what we can call a *direct route* toointeract with hello SQL Database server.</span></span> <span data-ttu-id="97329-114">建立連接之後，進一步 hello 用戶端與資料庫之間的互動會涉及任何中介軟體 proxy。</span><span class="sxs-lookup"><span data-stu-id="97329-114">After a connection is established, further interactions between hello client and database involve no middleware proxy.</span></span>

<span data-ttu-id="97329-115">hello 順序如下所示：</span><span class="sxs-lookup"><span data-stu-id="97329-115">hello sequence is as follows:</span></span>

1. <span data-ttu-id="97329-116">ADO.NET 4.5 （含） 以後啟始 hello Azure 的雲端，簡短的互動，並收到以動態方式識別連接埠號碼。</span><span class="sxs-lookup"><span data-stu-id="97329-116">ADO.NET 4.5 (or later) initiates a brief interaction with hello Azure cloud, and receives a dynamically identified port number.</span></span>
   
   * <span data-ttu-id="97329-117">hello 以動態方式識別連接埠號碼正在 11000 11999 或 14000 14999 hello 範圍中。</span><span class="sxs-lookup"><span data-stu-id="97329-117">hello dynamically identified port number is in hello range of 11000-11999 or 14000-14999.</span></span>
2. <span data-ttu-id="97329-118">ADO.NET 然後 toohello SQL Database 伺服器直接與連線沒有中介軟體之間。</span><span class="sxs-lookup"><span data-stu-id="97329-118">ADO.NET then connects toohello SQL Database server directly, with no middleware in between.</span></span>
3. <span data-ttu-id="97329-119">查詢會傳送直接 toohello 資料庫，並傳回結果直接 toohello 用戶端。</span><span class="sxs-lookup"><span data-stu-id="97329-119">Queries are sent directly toohello database, and results are returned directly toohello client.</span></span>

<span data-ttu-id="97329-120">請確定該 hello 連接埠範圍 11000 11999 和 Azure 用戶端電腦上的 14000 14999 保留供 SQL Database 的 ADO.NET 4.5 用戶端互動。</span><span class="sxs-lookup"><span data-stu-id="97329-120">Ensure that hello port ranges of 11000-11999 and 14000-14999 on your Azure client machine are left available for ADO.NET 4.5 client interactions with SQL Database.</span></span>

* <span data-ttu-id="97329-121">特別是，hello 範圍中的連接埠必須是可用的任何其他輸出封鎖器。</span><span class="sxs-lookup"><span data-stu-id="97329-121">In particular, ports in hello range must be free of any other outbound blockers.</span></span>
* <span data-ttu-id="97329-122">在您的 Azure VM 上 hello**具有進階安全性的 Windows 防火牆**控制項 hello 通訊埠設定。</span><span class="sxs-lookup"><span data-stu-id="97329-122">On your Azure VM, hello **Windows Firewall with Advanced Security** controls hello port settings.</span></span>
  
  * <span data-ttu-id="97329-123">您可以使用 hello[防火牆的使用者介面](http://msdn.microsoft.com/library/cc646023.aspx)的規則，用以指定 hello tooadd **TCP**通訊協定及連接埠範圍與 hello 語法喜歡**11000 11999**。</span><span class="sxs-lookup"><span data-stu-id="97329-123">You can use hello [firewall's user interface](http://msdn.microsoft.com/library/cc646023.aspx) tooadd a rule for which you specify hello **TCP** protocol along with a port range with hello syntax like **11000-11999**.</span></span>

## <a name="version-clarifications"></a><span data-ttu-id="97329-124">版本說明</span><span class="sxs-lookup"><span data-stu-id="97329-124">Version clarifications</span></span>
<span data-ttu-id="97329-125">本節將釐清 tooproduct 版本，請參閱的 hello moniker。</span><span class="sxs-lookup"><span data-stu-id="97329-125">This section clarifies hello monikers that refer tooproduct versions.</span></span> <span data-ttu-id="97329-126">它也會列出產品之間的一些版本配對。</span><span class="sxs-lookup"><span data-stu-id="97329-126">It also lists some pairings of versions between products.</span></span>

#### <a name="adonet"></a><span data-ttu-id="97329-127">ADO.NET</span><span class="sxs-lookup"><span data-stu-id="97329-127">ADO.NET</span></span>
* <span data-ttu-id="97329-128">ADO.NET 4.0 支援 hello TDS 7.3 通訊協定，但不是 7.4。</span><span class="sxs-lookup"><span data-stu-id="97329-128">ADO.NET 4.0 supports hello TDS 7.3 protocol, but not 7.4.</span></span>
* <span data-ttu-id="97329-129">ADO.NET 4.5 及更新版本支援 TDS 7.4 hello 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="97329-129">ADO.NET 4.5 and later supports hello TDS 7.4 protocol.</span></span>

## <a name="related-links"></a><span data-ttu-id="97329-130">相關連結</span><span class="sxs-lookup"><span data-stu-id="97329-130">Related links</span></span>
* <span data-ttu-id="97329-131">ADO.NET 4.6 於 2015 年 7 月 20 日發行。</span><span class="sxs-lookup"><span data-stu-id="97329-131">ADO.NET 4.6 was released on July 20, 2015.</span></span> <span data-ttu-id="97329-132">Hello.NET 小組的部落格通知可[這裡](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx)。</span><span class="sxs-lookup"><span data-stu-id="97329-132">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx).</span></span>
* <span data-ttu-id="97329-133">ADO.NET 4.5 於 2012 年 8 月 15 日發行。</span><span class="sxs-lookup"><span data-stu-id="97329-133">ADO.NET 4.5 was released on August 15, 2012.</span></span> <span data-ttu-id="97329-134">Hello.NET 小組的部落格通知可[這裡](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx)。</span><span class="sxs-lookup"><span data-stu-id="97329-134">A blog announcement from hello .NET team is available [here](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx).</span></span>
  
  * <span data-ttu-id="97329-135">您可以在 [這裡](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx)查看有關 ADO.NET 4.5.1 的部落格文章。</span><span class="sxs-lookup"><span data-stu-id="97329-135">A blog post about ADO.NET 4.5.1 is available [here](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx).</span></span>
* [<span data-ttu-id="97329-136">TDS 通訊協定版本清單</span><span class="sxs-lookup"><span data-stu-id="97329-136">TDS protocol version list</span></span>](http://www.freetds.org/userguide/tdshistory.htm)
* [<span data-ttu-id="97329-137">SQL Database 開發概觀</span><span class="sxs-lookup"><span data-stu-id="97329-137">SQL Database Development Overview</span></span>](sql-database-develop-overview.md)
* [<span data-ttu-id="97329-138">Azure SQL Database 防火牆</span><span class="sxs-lookup"><span data-stu-id="97329-138">Azure SQL Database firewall</span></span>](sql-database-firewall-configure.md)
* [<span data-ttu-id="97329-139">如何：在 SQL Database 上進行防火牆設定</span><span class="sxs-lookup"><span data-stu-id="97329-139">How to: Configure firewall settings on SQL Database</span></span>](sql-database-configure-firewall-settings.md)

