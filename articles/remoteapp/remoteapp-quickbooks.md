---
title: "在 Azure RemoteApp QuickBooks aaaDeploy |Microsoft 文件"
description: "深入了解如何 tooshare QuickBooks 與 Azure RemoteApp。"
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
ms.openlocfilehash: c21b1ac311449be2281f9ce157828260e856f55d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-you-deploy-quickbooks-in-azure-remoteapp"></a>您如何在 Azure RemoteApp 中部署 QuickBooks？
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

使用下列資訊 tooshare QuickBooks 成 Azure RemoteApp 中的應用程式的 hello。

您可以在混合式或雲端集合中使用 Azure RemoteApp 來共用 QuickBooks 2015 Enterprise。 hello 公司檔案必須位於執行 QuickBooks 資料庫伺服器與 hello Azure RemoteApp 伺服器位於不同的 VM。 永遠不會儲存在您的 Azure RemoteApp 映像上的 hello 公司檔案-如果您這麼做預期資料遺失。 只有 QuickBooks Enterprise 支援在外部共用 QuickBooks 可透過標準 Windows 網路存取的資料庫伺服器上裝載 hello QuickBooks 檔案。   

> [!IMPORTANT]
> hello QuickBooks 裝載 hello 公司檔案的資料庫伺服器必須位於不同的 VM 內 hello 相同 VNET 與 hello Azure RemoteApp 集合。  
> 
> 

## <a name="steps-toodeploy-quickbooks"></a>步驟 toodeploy QuickBooks
1. 建立 Azure VM 和安裝 QuickBooks 等 QuickBooks 資料庫伺服器，並放在 Azure VM 上的 hello 公司檔案。  請確定 tooproperly 設定防火牆規則。
2. 在上安裝 QuickBooks[自訂映像](remoteapp-imageoptions.md)並建立[Azure RemoteApp 集合](remoteapp-collections.md)，雲端或混合式 hello 內完全相同的 VNET，其中 VM 所裝載的 hello hello 與 QuickBooks 資料庫伺服器位於公司檔案。 
3. [發行](remoteapp-publish.md)QuickBooks 應用程式 toousers
4. 啟動 hello Azure RemoteApp 裝載 QuickBooks 用戶端，使用標準 Windows 網路 toohello VM 主控 hello QuickBooks 資料庫伺服器瀏覽並開啟 hello 公司檔案。 

## <a name="documentation-references"></a>文件參考
* QuickBooks [支援的組態](http://enterprisesuite.intuit.com/products/enterprise-solutions/technical/#top)
* QuickBooks [部署選項](http://enterprisesuite.intuit.com/everythingenterprise/launchpad/new-user/)

您也可以查看 Ignite 簡報，[基礎的 Microsoft Azure RemoteApp 管理和管理](https://channel9.msdn.com/Events/Ignite/2015/BRK3868)-向前快轉 too1:02:45 tooget toohello QuickBooks 組件。

## <a name="deployment-architecture"></a>部署架構
![QuickBooks + Azure RemoteApp 部署](./media/remoteapp-quickbooks/ra-quickbooks.png)

