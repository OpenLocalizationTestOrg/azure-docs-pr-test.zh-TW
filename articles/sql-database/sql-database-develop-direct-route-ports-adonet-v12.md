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
# <a name="ports-beyond-1433-for-adonet-45"></a>ADO.NET 4.5 超過 1433 以外的連接埠
本主題針對使用 ADO.NET 4.5 或更新版本的用戶端，說明 Azure SQL Database 的連接行為。 

> [!IMPORTANT]
> 如需連線架構的資訊，請參閱 [Azure SQL Database 連線架構](sql-database-connectivity-architecture.md)。
>

## <a name="outside-vs-inside"></a>比較內部與外部
對於連到 Azure SQL Database 的連線，必須先了解您的用戶端程式是在 Azure 雲端界限「外部」或「內部」執行。 這些小節將討論兩種常見案例。

#### <a name="outside-client-runs-on-your-desktop-computer"></a>*外部：* 在桌上型電腦上執行的用戶端
連接埠 1433 是裝載您的 SQL Database 用戶端應用程式的桌上型電腦上唯一必須開啟的連接埠。

#### <a name="inside-client-runs-on-azure"></a>*內部：* 在 Azure 上執行的用戶端
當您的用戶端是在 Azure 雲端界限內部執行時，它會使用我們可以稱為 *直接路由* 的路由與 SQL Database 伺服器互動。 建立連線之後，用戶端和資料庫之間的進一步互動未牽涉到任何中介軟體 proxy。

順序如下：

1. ADO.NET 4.5 (或更新版本) 會起始與 Azure 雲端的簡短互動，並且接收動態已識別的連接埠號碼。
   
   * 動態識別的連接埠號碼範圍為 11000-11999 或 14000-14999。
2. 然後 ADO.NET 會直接連線到 SQL Database 伺服器，中間沒有中介軟體。
3. 查詢會直接傳送到資料庫，結果會直接傳回至用戶端。

請確定已保留 Azure 用戶端電腦上的 11000-11999 及 14000-14999 連接埠範圍，以供 ADO.NET 4.5 用戶端與 SQL Database 進行互動使用。

* 特別是範圍中的連接埠必須沒有其他任何輸出封鎖器。
* 在您的 Azure VM 上， **具有進階安全性的 Windows 防火牆** 會控制此連接埠設定。
  
  * 您可以使用[防火牆的使用者介面](http://msdn.microsoft.com/library/cc646023.aspx)來新增規則，其中您可使用如 **11000-11999** 的語法指定 **TCP** 通訊協定和連接埠範圍。

## <a name="version-clarifications"></a>版本說明
本章節將釐清參考產品版本的 Moniker。 它也會列出產品之間的一些版本配對。

#### <a name="adonet"></a>ADO.NET
* ADO.NET 4.0 支援 TDS 7.3 通訊協定，但不支援 7.4。
* ADO.NET 4.5 和更新版本支援 TDS 7.4 通訊協定。

## <a name="related-links"></a>相關連結
* ADO.NET 4.6 於 2015 年 7 月 20 日發行。 您可以在 [這裡](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx)查看 .NET 小組的部落格公告。
* ADO.NET 4.5 於 2012 年 8 月 15 日發行。 您可以在 [這裡](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx)查看 .NET 小組的部落格公告。
  
  * 您可以在 [這裡](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx)查看有關 ADO.NET 4.5.1 的部落格文章。
* [TDS 通訊協定版本清單](http://www.freetds.org/userguide/tdshistory.htm)
* [SQL Database 開發概觀](sql-database-develop-overview.md)
* [Azure SQL Database 防火牆](sql-database-firewall-configure.md)
* [如何：在 SQL Database 上進行防火牆設定](sql-database-configure-firewall-settings.md)

