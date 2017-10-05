---
title: "在 Azure RemoteApp 中部署 QuickBooks | Microsoft Docs"
description: "了解如何與 Azure RemoteApp 共用 QuickBooks。"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c5d00753-77c0-4f0d-a5df-9451b46a31d3
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: bbfac45220f6ef36c9951daae0ced1974e8ddabb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>您如何在 Azure RemoteApp 中部署 QuickBooks？
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 如需詳細資訊，請參閱 [公告](https://go.microsoft.com/fwlink/?linkid=821148) 。
> 
> 

使用下列資訊在 Azure RemoteApp 中以應用程式形式共用 QuickBooks。

您可以在混合式或雲端集合中使用 Azure RemoteApp 來共用 QuickBooks 2015 Enterprise。 公司檔案必須位於執行 QuickBooks 資料庫伺服器並且與 Azure RemoteApp 伺服器不同的 VM。 永遠不要將公司檔案儲存在您的 Azure RemoteApp 映像檔中 - 這麼做可能導致資料遺失。 只有 QuickBooks Enterprise 支援在外部共用上裝載 QuickBooks 檔案，該共用上具有可透過標準 Windows 網路存取的 QuickBooks 資料庫伺服器。   

> [!IMPORTANT]
> 裝載公司檔案的 QuickBooks 資料庫伺服器必須位於與 Azure RemoteApp 集合相同的 VNET 內的不同 VM 上。  
> 
> 

## <a name="steps-to-deploy-quickbooks"></a>部署 QuickBooks 的步驟
1. 建立 Azure VM 並安裝 QuickBooks、QuickBooks 資料庫伺服器，然後將公司檔案放在 Azure VM 上。  請務必正確設定防火牆規則。
2. 在[自訂映像檔](remoteapp-imageoptions.md)上安裝 QuickBooks，並且在與裝載 QuickBooks 資料庫伺服器 (公司檔案所在) 之 VM 完全相同的 VNET 內建立 [Azure RemoteApp 集合](remoteapp-collections.md) (無論是在雲端或混合式)。 
3. [發佈](remoteapp-publish.md) QuickBooks 應用程式給使用者
4. 啟動 Azure RemoteApp 裝載的 QuickBooks 用戶端，使用標準 Windows 網路瀏覽至裝載 QuickBooks 資料庫伺服器的 VM，並開啟公司檔案。 

## <a name="documentation-references"></a>文件參考
* QuickBooks [支援的組態](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* QuickBooks [部署選項](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

您也可以看看我的 Ignite 簡報 [Microsoft Azure RemoteApp 管理與系統管理的基礎](https://channel9.msdn.com/Events/Ignite/2015/BRK3868) - 向前快轉到 1:02:45，以跳到 QuickBooks 部分。

## <a name="deployment-architecture"></a>部署架構
![QuickBooks + Azure RemoteApp 部署](./media/remoteapp-quickbooks/ra-quickbooks.png)

