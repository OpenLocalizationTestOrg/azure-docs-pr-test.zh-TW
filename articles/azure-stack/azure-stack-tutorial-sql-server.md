---
title: "aaaMake SQL 資料庫可用 tooyour Azure 堆疊使用者 |Microsoft 文件"
description: "教學課程 tooinstall hello SQL Server 資源提供者，並建立提供項目，讓 Azure 堆疊使用者可以建立 SQL 資料庫。"
services: azure-stack
documentationcenter: 
author: ErikjeMS
manager: 
editor: 
ms.assetid: 
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 7/03/2017
ms.author: erikje
ms.custom: mvc
ms.openlocfilehash: 778513ba982981895afe2d57b3b5dda71ead8886
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="make-sql-databases-available-tooyour-azure-stack-users"></a>將 SQL 資料庫可用 tooyour Azure 堆疊使用者

身為 Azure Stack 雲端系統管理員，您可以建立供應項目以讓您的使用者 (租用戶) 建立 SQL 資料庫，以搭配其雲端原生應用程式、網站與工作負載使用。 藉由提供這些自訂、 隨、 以雲端為基礎的資料庫 tooyour 使用者，您可以將它們儲存時間和資源。 tooset 最，您將會：

> [!div class="checklist"]
> * 部署 hello SQL Server 資源提供者
> * 建立優惠
> * 測試 hello 優惠

## <a name="deploy-hello-sql-server-resource-provider"></a>部署 hello SQL Server 資源提供者

hello 部署程序中有詳細說明在 hello [Azure 堆疊發行項上的使用 SQL 資料庫](azure-stack-sql-resource-provider-deploy.md)，包含下列主要步驟 hello:

1.  [部署 hello SQL 資源提供者]( azure-stack-sql-resource-provider-deploy.md#deploy-the-resource-provider)。
2.  [確認 hello 部署]( azure-stack-sql-resource-provider-deploy.md#verify-the-deployment-using-the-azure-stack-portal)。
3.  [藉由連接 tooa 主控 SQL server 提供的容量]( azure-stack-sql-resource-provider-deploy.md#provide-capacity-by-connecting-to-a-hosting-sql-server)。

## <a name="create-an-offer"></a>建立優惠

1.  [設定配額](azure-stack-setting-quotas.md)並將它命名為 *SQLServerQuota*。 選取**Microsoft.SQLAdapter** hello**命名空間**欄位。
2.  [建立方案](azure-stack-create-plan.md)。 命名*TestSQLServerPlan*，選取 hello **Microsoft.SQLAdapter**服務，以及**SQLServerQuota**配額。

    > [!NOTE]
    > toolet 使用者建立其他應用程式，可能需要其他服務 hello 計劃中。 例如，Azure 函式需要該 hello 計劃包含 hello **Microsoft.Storage**服務，而 Wordpress **Microsoft.MySQLAdapter**。
    > 
    >

3.  [建立優惠](azure-stack-create-offer.md)，其命名**TestSQLServerOffer**和選取 hello **TestSQLServerPlan**計劃。

## <a name="test-hello-offer"></a>測試 hello 優惠

既然您已部署的 hello SQL Server 資源提供者，以及建立提供項目時，您可以登入的使用者身分，訂閱 toohello 供應項目，並建立資料庫。

### <a name="subscribe-toohello-offer"></a>訂閱 toohello 供應項目
1. 登入 toohello 堆疊 Azure 入口網站 (https://portal.local.azurestack.external) 做為租用戶。
2. 按一下 [取得訂用帳戶]，然後在 [顯示名稱] 下輸入 **TestSQLServerSubscription**。
3. 按一下 [選取服務] > [TestSQLServerOffer] > [建立]。
4. 按一下 [更多服務] > [訂用帳戶] > [TestSQLServerSubscription] > [資源提供者]。
5. 按一下**註冊**下一步 toohello **Microsoft.SQLAdapter**提供者。

### <a name="create-a-sql-database"></a>建立 SQL 資料庫

1. 按一下 [+] > [資料 + 儲存體] > [SQL Database]。
2. 保持 hello 或預設值 hello 欄位，您可以使用這些範例：
    - **資料庫名稱**：SQLdb
    - **大小上限 (MB)**：100
    - **訂用帳戶**：TestSQLOffer
    - **資源群組**：SQL-RG
3. 按一下**登入設定**hello 資料庫中，輸入認證，然後按**確定**。
4. 按一下**SKU** > 選取 hello 建立 hello SQL 主控伺服器的 SQL SKU >**確定**。
5. 按一下 [建立] 。

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 部署 hello SQL Server 資源提供者
> * 建立優惠
> * 測試 hello 優惠

如何前進 toohello 下一個教學課程 toolearn 至：

> [!div class="nextstepaction"]
> [讓 web、 行動裝置、 應用程式開發介面應用程式可用 tooyour 使用者]( azure-stack-tutorial-app-service.md)

