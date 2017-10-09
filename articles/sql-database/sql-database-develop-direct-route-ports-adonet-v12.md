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
# <a name="ports-beyond-1433-for-adonet-45"></a>ADO.NET 4.5 超過 1433 以外的連接埠
本主題描述使用 ADO.NET 4.5 或更新版本的用戶端 hello Azure SQL Database 連接行為。 

> [!IMPORTANT]
> 如需連線架構的資訊，請參閱 [Azure SQL Database 連線架構](sql-database-connectivity-architecture.md)。
>

## <a name="outside-vs-inside"></a>比較內部與外部
針對連接 tooAzure SQL 資料庫，我們必須先詢問是否要執行用戶端程式*外*或*內*hello Azure 雲端界限。 hello 各節將討論兩個常見的案例。

#### <a name="outside-client-runs-on-your-desktop-computer"></a>*外部：* 在桌上型電腦上執行的用戶端
通訊埠 1433年是必須在裝載 SQL 資料庫用戶端應用程式的桌上型電腦上開啟 hello 唯一連接埠。

#### <a name="inside-client-runs-on-azure"></a>*內部：* 在 Azure 上執行的用戶端
當您的用戶端執行 hello Azure 雲端界限內時，它會使用我們可以呼叫*直接路由*toointeract 與 hello SQL Database 伺服器。 建立連接之後，進一步 hello 用戶端與資料庫之間的互動會涉及任何中介軟體 proxy。

hello 順序如下所示：

1. ADO.NET 4.5 （含） 以後啟始 hello Azure 的雲端，簡短的互動，並收到以動態方式識別連接埠號碼。
   
   * hello 以動態方式識別連接埠號碼正在 11000 11999 或 14000 14999 hello 範圍中。
2. ADO.NET 然後 toohello SQL Database 伺服器直接與連線沒有中介軟體之間。
3. 查詢會傳送直接 toohello 資料庫，並傳回結果直接 toohello 用戶端。

請確定該 hello 連接埠範圍 11000 11999 和 Azure 用戶端電腦上的 14000 14999 保留供 SQL Database 的 ADO.NET 4.5 用戶端互動。

* 特別是，hello 範圍中的連接埠必須是可用的任何其他輸出封鎖器。
* 在您的 Azure VM 上 hello**具有進階安全性的 Windows 防火牆**控制項 hello 通訊埠設定。
  
  * 您可以使用 hello[防火牆的使用者介面](http://msdn.microsoft.com/library/cc646023.aspx)的規則，用以指定 hello tooadd **TCP**通訊協定及連接埠範圍與 hello 語法喜歡**11000 11999**。

## <a name="version-clarifications"></a>版本說明
本節將釐清 tooproduct 版本，請參閱的 hello moniker。 它也會列出產品之間的一些版本配對。

#### <a name="adonet"></a>ADO.NET
* ADO.NET 4.0 支援 hello TDS 7.3 通訊協定，但不是 7.4。
* ADO.NET 4.5 及更新版本支援 TDS 7.4 hello 通訊協定。

## <a name="related-links"></a>相關連結
* ADO.NET 4.6 於 2015 年 7 月 20 日發行。 Hello.NET 小組的部落格通知可[這裡](http://blogs.msdn.com/b/dotnet/archive/2015/07/20/announcing-net-framework-4-6.aspx)。
* ADO.NET 4.5 於 2012 年 8 月 15 日發行。 Hello.NET 小組的部落格通知可[這裡](http://blogs.msdn.com/b/dotnet/archive/2012/08/15/announcing-the-release-of-net-framework-4-5-rtm-product-and-source-code.aspx)。
  
  * 您可以在 [這裡](http://blogs.msdn.com/b/dotnet/archive/2013/06/26/announcing-the-net-framework-4-5-1-preview.aspx)查看有關 ADO.NET 4.5.1 的部落格文章。
* [TDS 通訊協定版本清單](http://www.freetds.org/userguide/tdshistory.htm)
* [SQL Database 開發概觀](sql-database-develop-overview.md)
* [Azure SQL Database 防火牆](sql-database-firewall-configure.md)
* [如何：在 SQL Database 上進行防火牆設定](sql-database-configure-firewall-settings.md)

