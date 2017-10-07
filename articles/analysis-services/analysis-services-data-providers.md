---
title: "連接 tooAzure Analysis Services 所需的 aaaClient 程式庫 |Microsoft 文件"
description: "描述所需的用戶端應用程式和工具 tooconnect Azure Analysis Services 的用戶端程式庫"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 74ba5c05ba76c6587c5aed38f200a1ba469aa4f3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="client-libraries-for-connecting-tooazure-analysis-services"></a>連接 tooAzure Analysis Services 的用戶端程式庫

用戶端程式庫所需的用戶端應用程式和工具 tooconnect tooAnalysis 服務伺服器。 

Analysis Services 會利用三個用戶端程式庫。 ADOMD.NET 和「Analysis Services 管理物件」(AMO) 是受管理的用戶端程式庫。 hello Analysis Services OLE DB 提供者 (MSOLAP DLL) 是原生用戶端程式庫。 一般來說，這三個可安裝在 hello 相同的時間。 Azure Analysis Services 需要 hello 最新版本。 

Microsoft 用戶端應用程式 (例如 Power BI Desktop 和 Excel) 會安裝這所有三個用戶端程式庫。 不過，根據 hello 版本或更新的頻率，用戶端程式庫可能無法 hello Azure Analysis Services 所需的最新版本。 hello 一樣 toocustom 應用程式或其他介面，例如 AsCmd，TOM，ADOMD.NET。 這些應用程式需要以手動方式安裝 hello 程式庫。 hello 進行手動安裝的用戶端程式庫隨附的 SQL Server 功能套件散發的封裝。 不過，這些用戶端程式庫會繫結的 toohello SQL Server 版本，可能無法 hello 最新版本。  

用戶端連線的用戶端程式庫會與不同的資料提供者需要 tooconnect 從 Azure Analysis Services 伺服器 tooa 資料來源。 toolearn 進一步了解資料來源連接，請參閱[資料來源連接](analysis-services-datasource.md)。

## <a name="download-hello-latest-client-libraries"></a>下載最新用戶端程式庫 hello  
使用下列用戶端程式庫，如果您是在生產環境中，而且需要完整發行和支援版本的 hello。

[MSOLAP (amd64)](https://go.microsoft.com/fwlink/?linkid=829576)</br>
[MSOLAP (x86)](https://go.microsoft.com/fwlink/?linkid=829575)</br>
[AMO](https://go.microsoft.com/fwlink/?linkid=829578)</br>
[ADOMD](https://go.microsoft.com/fwlink/?linkid=829577)</br>

## <a name="next-steps"></a>後續步驟
[使用 Excel 進行連接](analysis-services-connect-excel.md)    
[與 Power BI 連線](analysis-services-connect-pbi.md)
