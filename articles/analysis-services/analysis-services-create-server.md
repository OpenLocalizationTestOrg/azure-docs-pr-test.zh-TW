---
title: "在 Azure 中的 Analysis Services 伺服器 aaaCreate |Microsoft 文件"
description: "了解 toocreate Analysis Services 伺服器在 Azure 中的執行個體。"
services: analysis-services
documentationcenter: 
author: minewiskan
manager: erikre
editor: 
tags: 
ms.assetid: 7f560216-8a9a-4d06-852e-48cf24deab19
ms.service: analysis-services
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: na
ms.date: 08/15/2017
ms.author: owend
ms.openlocfilehash: 3668f659039f79f3dd71498d1066e8682bf33228
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-azure-analysis-services-server-in-azure-portal"></a>在 Azure 入口網站中建立 Azure Analysis Services 伺服器
本文將逐步引導您在 Azure 訂用帳戶中建立 Analysis Services 伺服器資源。

## <a name="before-you-begin"></a>開始之前
toocomplete 本快速入門中，您需要：

* **Azure 訂用帳戶**： 瀏覽[Azure 免費試用](https://azure.microsoft.com/offers/ms-azr-0044p/)toocreate 帳戶。
* **Azure Active Directory**：您的訂用帳戶必須與 Azure Active Directory 租用戶相關聯。 此外，您必須使用 Azure Active Directory 中的帳戶登入 tooAzure toobe。 不支援 Microsoft 帳戶。 詳細資訊，請參閱 toolearn[驗證和使用者權限](analysis-services-manage-users.md)。
* **資源群組**：使用現有資源群組，或[建立新的群組](../azure-resource-manager/resource-group-overview.md)。

> [!NOTE]
> 建立伺服器可能會導致新的可計費服務。 詳細資訊，請參閱 toolearn [Analysis Services 定價](https://azure.microsoft.com/pricing/details/analysis-services/)。
> 
> 

## <a name="toocreate-a-server-in-azure-portal"></a>toocreate Azure 入口網站中的伺服器
1. 登入 toohello [Azure 入口網站](https://portal.azure.com)。  
2. 按一下 [+ 新增] > [資料 + 分析] > [Analysis Services]。
3. 在 hello **Analysis Services**刀鋒視窗中，填寫必要的 hello 欄位，然後按**建立**。
   
    ![建立伺服器](./media/analysis-services-create-server/aas-create-server-blade.png)
   
   * **伺服器名稱**： 輸入所使用的唯一名稱 tooreference hello 伺服器。
   * **訂用帳戶**： 選取此伺服器帳單以 hello 訂用帳戶。
   * **資源群組**： 這些容器會設計的 toohelp 管理 Azure 資源的集合。 詳細資訊，請參閱 toolearn[資源群組](../azure-resource-manager/resource-group-overview.md)。
   * **位置**： 此 Azure 資料中心位置主機 hello 伺服器。 請選擇最靠近最大使用者群體的位置。
   * **定價層**：選取定價層。 支援表格式模型向上 too400 GB。 詳細資訊，請參閱 toolearn [Azure Analysis Services 定價](https://azure.microsoft.com/pricing/details/analysis-services/)。
4. 按一下 [建立] 。

建立程序通常不到一分鐘即可完成；往往在數秒內。 如果您選取**新增 tooPortal**，瀏覽 tooyour 入口 toosee 新的伺服器。 或者，您也可以瀏覽過**更多服務** > **Analysis Services** toosee 是否準備您的伺服器。

 ![儀表板](./media/analysis-services-create-server/aas-create-server-dashboard.png)


## <a name="next-steps"></a>後續步驟
一旦您已建立您的伺服器，您可以[部署模型](analysis-services-deploy.md)tooit 使用 SSDT 或 SSMS。

如果您部署 tooyour 伺服器模型連接 tooon 內部部署資料來源，您需要 tooinstall[在內部部署資料閘道](analysis-services-gateway.md)您網路中的電腦上。

