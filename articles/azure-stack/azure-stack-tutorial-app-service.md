---
title: "aaaMake web、 mobile 及 API 應用程式可用 tooyour Azure 堆疊使用者 |Microsoft 文件"
description: "教學課程 tooinstall hello 應用程式服務資源提供者，並建立提供項目，讓您的 Azure 堆疊使用者 hello 能力 toocreate web、 行動裝置版和 API 應用程式。"
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
ms.openlocfilehash: 62b86cf6288b8f629bc92dade003c712fe523187
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="make-web-mobile-and-api-apps-available-tooyour-azure-stack-users"></a>讓 web、 行動裝置、 應用程式開發介面應用程式可用 tooyour Azure 堆疊使用者

身為 Azure Stack 雲端系統管理員，您可以建立供應項目，以讓您的使用者 (租用戶) 建立 Azure Functions 與 Web、行動裝置與 API 應用程式。 藉由提供存取 toothese tooyour 隨、 以雲端為基礎的應用程式的使用者，您可以將它們儲存時間和資源。 tooset 最，您將會：

> [!div class="checklist"]
> * 部署 hello 應用程式服務資源提供者
> * 建立優惠
> * 測試 hello 優惠

## <a name="deploy-hello-app-service-resource-provider"></a>部署 hello 應用程式服務資源提供者

1. [準備 hello Azure 堆疊開發套件主機](azure-stack-app-service-before-you-get-started.md)。 這包括部署 hello SQL Server 資源提供者，才能建立某些應用程式。
2. [下載 hello installer 和協助程式指令碼](azure-stack-app-service-deploy.md#download-the-required-components)。
3. [執行 hello helper 指令碼所需的 toocreate 憑證](azure-stack-app-service-deploy.md#create-certificates-required-by-app-service-on-azure-stack)。
4. [安裝應用程式服務資源提供者 hello](azure-stack-app-service-deploy.md#use-the-installer-to-download-and-install-app-service-on-azure-stack) (花費幾小時 tooinstall，在所有 hello 背景工作角色 tooappear)。
5. [驗證 hello 安裝](azure-stack-app-service-deploy.md#validate-the-app-service-on-azure-stack-installation)。

## <a name="create-an-offer"></a>建立優惠

例如，您可以建立供應項目，以讓使用者 建立 DNN Web 內容管理系統。 它需要 hello SQL Server 服務已經啟用安裝 hello SQL Server 資源提供者。

1.  [設定配額](azure-stack-setting-quotas.md)並將它命名為 *AppServiceQuota*。 選取**Microsoft.Web** hello**命名空間**欄位。
2.  [建立方案](azure-stack-create-plan.md)。 命名*TestAppServicePlan*，選取 hello hello **Microsoft.SQL**服務，以及**AppService 配額**配額。

    > [!NOTE]
    > toolet 使用者建立其他應用程式，可能需要其他服務 hello 計劃中。 例如，Azure 函式需要該 hello 計劃包含 hello **Microsoft.Storage**服務，而 Wordpress **Microsoft.MySQL**。
    > 
    >

3.  [建立優惠](azure-stack-create-offer.md)，其命名**TestAppServiceOffer**和選取 hello **TestAppServicePlan**計劃。

## <a name="test-hello-offer"></a>測試 hello 優惠

現在您已部署的 hello 應用程式服務資源提供者，以及建立提供項目時，您可以登入的使用者身分，訂閱 toohello 供應項目，並建立應用程式。 針對此範例，我們將建立 DNN 平台內容管理系統。 您必須先建立 SQL 資料庫，然後 hello DNN web 應用程式。

### <a name="subscribe-toohello-offer"></a>訂閱 toohello 供應項目
1. 登入 toohello 堆疊 Azure 入口網站 (https://portal.local.azurestack.external) 做為租用戶。
2. 按一下 [取得訂用帳戶] > 在 [顯示名稱] 下輸入 **TestAppServiceSubscription** > [選取服務] > [TestAppServiceOffer] > [建立]。

### <a name="create-a-sql-database"></a>建立 SQL 資料庫

1. 按一下 [+] > [資料 + 儲存體] > [SQL Database]。
2. 保留 hello hello 欄位的預設值以外，如下所示：
    - **資料庫名稱**：DNNdb
    - **大小上限 (MB)**：100
    - **訂用帳戶**：TestAppServiceOffer
    - **資源群組**：DNN-RG
3. 按一下**登入設定**hello 資料庫中，輸入認證，然後按**確定**。 稍後您將在這些步驟中用到這些認證。
4. 按一下**SKU** > 選取 hello 建立 hello SQL 主控伺服器的 SQL SKU >**確定**。
5. 按一下 [建立] 。

### <a name="create-a-dnn-app"></a>建立 DNN 應用程式    

1. 按一下 [+] > [查看全部] > [DNN 平台預覽] > [建立]。
2. 在 [應用程式名稱] 下輸入 *DNNapp*，然後在 [訂用帳戶] 下選取 [TestAppServiceOffer]。
3. 按一下 [設定必要設定] > [新建] > 輸入 [App Service 方案] 名稱。
4. 按一下 [定價層] > [F1 免費] > [選取] > [確定]。
5. 按一下**資料庫**並輸入您稍早建立的 hello 資訊 hello SQL database。
6. 按一下 [建立] 。

在本教學課程中，您已了解如何：

> [!div class="checklist"]
> * 部署 hello 應用程式服務資源提供者
> * 建立優惠
> * 測試 hello 優惠

如何前進 toohello 下一個教學課程 toolearn 至：

> [!div class="nextstepaction"]
> [部署應用程式 tooAzure 和 Azure 堆疊](azure-stack-solution-pipeline.md)
