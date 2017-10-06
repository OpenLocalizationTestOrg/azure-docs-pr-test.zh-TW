---
title: "web 應用程式使用範本-Azure Cosmos DB aaaDeploy |Microsoft 文件"
description: "了解如何 toodeploy Azure Cosmos DB 帳戶、 Azure App Service Web 應用程式和範例 web 應用程式使用 Azure Resource Manager 範本。"
services: cosmos-db, app-service\web
author: mimig1
manager: jhubbard
editor: monicar
documentationcenter: 
ms.assetid: 087d8786-1155-42c7-924b-0eaba5a8b3e0
ms.service: cosmos-db
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 12/08/2016
ms.author: mimig
ms.openlocfilehash: b2bdde9279aad570606d7bf06dfc710f564b4d0c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-cosmos-db-and-azure-app-service-web-apps-using-an-azure-resource-manager-template"></a>使用 Azure Resource Manager 範本部署 Azure Cosmos DB 和 Azure App Service Web Apps
本教學課程示範如何 toouse Azure Resource Manager 範本 toodeploy 和整合[Microsoft Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/)、 [Azure App Service](http://go.microsoft.com/fwlink/?LinkId=529714) web 應用程式和範例 web 應用程式。

使用 Azure 資源管理員範本，您可以輕鬆地自動化 hello 部署和設定您的 Azure 資源。  本教學課程示範如何 toodeploy web 應用程式並自動設定 Azure Cosmos DB 帳戶連線資訊。

完成本教學課程之後, 您將無法 tooanswer hello 下列問題：  

* 如何使用 Azure Resource Manager 範本 toodeploy 和整合 Azure Cosmos DB 帳戶和 Azure App Service 中的 web 應用程式？
* 如何使用 Azure Resource Manager 範本 toodeploy 和整合 Azure Cosmos DB 帳戶、 App Service Web 應用程式中的 web app 和 Webdeploy 應用程式？

<a id="Prerequisites"></a>

## <a name="prerequisites"></a>必要條件
> [!TIP]
> 雖然本教學課程不會假設使用 Azure Resource Manager 範本或 JSON 的使用經驗，如果您想 toomodify hello 參考範本或部署選項，然後將需要的每個區域的知識。
> 
> 

之前遵循 hello 指示在本教學課程，請確定您擁有 hello 下列：

* Azure 訂用帳戶。 Azure 是訂閱型平台。  如需取得訂用帳戶的詳細資訊，請參閱[購買選項](https://azure.microsoft.com/pricing/purchase-options/)、[成員優惠](https://azure.microsoft.com/pricing/member-offers/)或[免費使用](https://azure.microsoft.com/pricing/free-trial/)。

## <a id="CreateDB"></a>步驟 1： 下載 hello 範本檔案
讓我們開始下載 hello 範本檔案，我們將在本教學課程中使用。

1. 下載 hello[建立 Azure Cosmos DB 帳戶，Web 應用程式，並部署示範應用程式範例](https://portalcontent.blob.core.windows.net/samples/DocDBWebsiteTodo.json)範本 tooa 本機資料夾 (例如 C:\Azure Cosmos DBTemplates)。 這個範本將會部署 Azure Cosmos DB 帳戶、App Service Web 應用程式和 Web 應用程式。  它也會自動將設定 hello web 應用程式 tooconnect toohello Azure Cosmos DB 帳戶。
2. 下載 hello[建立 Azure Cosmos DB 帳戶和 Web 應用程式範例](https://portalcontent.blob.core.windows.net/samples/DocDBWebSite.json)範本 tooa 本機資料夾 (例如 C:\Azure Cosmos DBTemplates)。 此範本將部署 Azure Cosmos DB 帳戶，App Service web 應用程式，並將修改 hello 站台的應用程式設定 tooeasily 介面 Azure Cosmos DB 連接資訊，但不包含 web 應用程式。  

<a id="Build"></a>

## <a name="step-2-deploy-hello-azure-cosmos-db-account-app-service-web-app-and-demo-application-sample"></a>步驟 2： 部署的 hello Azure Cosmos DB 帳戶，App Service web 應用程式和示範應用程式範例
現在讓我們來部署第一個範本。

> [!TIP]
> hello 範本不會驗證 hello web 應用程式名稱並輸入下方的 Azure Cosmos DB 帳戶名稱是） 有效且 b） 可用。  強烈建議您確認的 hello hello 可用性命名您計劃 toosupply 先前 toosubmitting hello 部署。
> 
> 

1. 登入 toohello [Azure 入口網站](https://portal.azure.com)、 按一下 [新增]，並搜尋 「 範本部署 」。
    ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment1.png)
2. 選取 hello 範本部署項目，然後按一下**建立** ![hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment2.png)
3. 按一下**編輯範本**，貼上 hello 內容 hello DocDBWebsiteTodo.json 範本檔案，然後按一下**儲存**。
   ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment3.png)
4. 按一下**編輯參數**，提供值的每一個 hello 強制參數，然後按一下**確定**。  hello 參數如下所示：
   
   1. 網站名稱： 指定 hello App Service web 應用程式名稱，而且您將使用 tooaccess hello web 應用程式使用的 tooconstruct hello URL (例如： 如果您指定"mydemodocdbwebapp"，則 hello URL 將會存取 hello web 應用程式mydemodocdbwebapp.azurewebsites.net)。
   2. HOSTINGPLANNAME： 指定應用程式服務裝載計劃 toocreate hello 名稱。
   3. 位置： 指定 hello toocreate hello Azure Cosmos DB 和 web 應用程式資源中的 Azure 位置。
   4. DATABASEACCOUNTNAME： 指定 hello Azure Cosmos DB 帳戶 toocreate hello 名稱。   
      
      ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment4.png)
5. 選擇現有的資源群組或提供名稱 toomake 新的資源群組，並選擇 hello 資源群組的位置。

    ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment5.png)
6. 按一下**檢查 法律條款**，**購買**，然後按一下**建立**toobegin hello 部署。  選取**Pin toodashboard**因此 hello 產生部署是輕鬆地看到您的 Azure 入口網站首頁上。
   ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment6.png)
7. Hello 部署完成時，就會開啟 hello 資源群組 刀鋒視窗。
   ![Hello 資源群組 刀鋒視窗的螢幕擷取畫面](./media/create-website/TemplateDeployment7.png)  
8. toouse hello 應用程式，直接瀏覽 toohello web 應用程式 URL （hello 上述範例中，在 hello URL 會是 http://mydemodocdbwebapp.azurewebsites.net）。  您會看到下列 web 應用程式的 hello:
   
   ![範例待辦事項應用程式](./media/create-website/image2.png)
9. 請繼續並 hello web 應用程式中建立數個工作，然後傳回 toohello 資源群組 刀鋒視窗中 hello Azure 入口網站。 按一下 hello 資源 清單中的 hello Azure Cosmos DB 帳戶資源，然後按一下**查詢總管**。
    ![螢幕擷取畫面的 hello 透鏡與 hello 反白顯示的 web 應用程式的摘要](./media/create-website/TemplateDeployment8.png)  
10. 執行 hello 預設查詢，「 選取 * 從 c"，並檢查 hello 結果。  請注意該 hello 查詢已擷取您在步驟 7 上述建立 hello todo 項目的 hello JSON 表示法。  感覺可用 tooexperiment 查詢;例如，請嘗試重新執行 SELECT * FROM c WHERE c.isComplete = true tooreturn 已標示為完成的所有 todo 項目。
    
    ![Hello 查詢總管和結果的刀鋒視窗顯示 hello 查詢結果的螢幕擷取畫面](./media/create-website/image5.png)
11. 感覺可用 tooexplore hello Azure Cosmos DB 入口網站體驗，或修改 hello 範例待辦事項應用程式。  當您準備好時，讓我們來部署另一個範本。

<a id="Build"></a> 

## <a name="step-3-deploy-hello-document-account-and-web-app-sample"></a>步驟 3： 部署 hello 文件的帳戶和 web 應用程式範例
現在讓我們來部署第二個範本。  此範本是很有用的 tooshow 如何您可以將 Azure Cosmos DB 連接資訊，例如帳戶端點和服務主要金鑰插入 web 應用程式做為應用程式設定或自訂連接字串。 例如，您可能有您的 web 應用程式，您會想 toodeploy Azure Cosmos DB 帳戶，且有 hello 連接資訊在部署期間自動填入。

> [!TIP]
> hello 範本不會驗證 hello web 應用程式名稱並輸入下方的 Azure Cosmos DB 帳戶名稱是） 有效且 b） 可用。  強烈建議您確認的 hello hello 可用性命名您計劃 toosupply 先前 toosubmitting hello 部署。
> 
> 

1. 在 hello [Azure 入口網站](https://portal.azure.com)、 按一下 [新增]，並搜尋 「 範本部署 」。
    ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment1.png)
2. 選取 hello 範本部署項目，然後按一下**建立** ![hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment2.png)
3. 按一下**編輯範本**，貼上 hello 內容 hello DocDBWebSite.json 範本檔案，然後按一下**儲存**。
   ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment3.png)
4. 按一下**編輯參數**，提供值的每一個 hello 強制參數，然後按一下**確定**。  hello 參數如下所示：
   
   1. 網站名稱： 指定 hello App Service web 應用程式名稱，而且您將使用 tooaccess hello web 應用程式使用的 tooconstruct hello URL (例如： 如果您指定"mydemodocdbwebapp"，則 hello URL 將會存取 hello web 應用程式mydemodocdbwebapp.azurewebsites.net)。
   2. HOSTINGPLANNAME： 指定應用程式服務裝載計劃 toocreate hello 名稱。
   3. 位置： 指定 hello toocreate hello Azure Cosmos DB 和 web 應用程式資源中的 Azure 位置。
   4. DATABASEACCOUNTNAME： 指定 hello Azure Cosmos DB 帳戶 toocreate hello 名稱。   
      
      ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment4.png)
5. 選擇現有的資源群組或提供名稱 toomake 新的資源群組，並選擇 hello 資源群組的位置。

    ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment5.png)
6. 按一下**檢查 法律條款**，**購買**，然後按一下**建立**toobegin hello 部署。  選取**Pin toodashboard**因此 hello 產生部署是輕鬆地看到您的 Azure 入口網站首頁上。
   ![Hello 範本部署 UI 的螢幕擷取畫面](./media/create-website/TemplateDeployment6.png)
7. Hello 部署完成時，就會開啟 hello 資源群組 刀鋒視窗。
   ![Hello 資源群組 刀鋒視窗的螢幕擷取畫面](./media/create-website/TemplateDeployment7.png)  
8. 按一下 hello hello 資源 清單中的 Web 應用程式資源，然後按一下**應用程式設定** ![hello 資源群組的螢幕擷取畫面](./media/create-website/TemplateDeployment9.png)  
9. 請注意如何在 hello Azure Cosmos DB 端點和每個 hello Azure Cosmos 資料庫主要金鑰的應用程式設定。

    ![應用程式設定的螢幕擷取畫面](./media/create-website/TemplateDeployment10.png)  
10. 感覺可用 toocontinue 瀏覽 hello Azure 入口網站，或遵循其中一種我們 Azure Cosmos DB[範例](http://go.microsoft.com/fwlink/?LinkID=402386)toocreate Azure Cosmos DB 應用程式。

<a name="NextSteps"></a>

## <a name="next-steps"></a>後續步驟
恭喜！ 您已使用 Azure Resource Manager 範本部署了 Azure Cosmos DB、App Service Web 應用程式及範例 Web 應用程式。

* 按一下 深入了解 Azure Cosmos DB toolearn[這裡](http://azure.com/docdb)。
* 進一步了解 Azure App Service Web 應用程式，toolearn 按一下[這裡](http://go.microsoft.com/fwlink/?LinkId=325362)。
* 按一下 進一步了解 Azure 資源管理員範本 toolearn[這裡](https://msdn.microsoft.com/library/azure/dn790549.aspx)。

## <a name="whats-changed"></a>變更的項目
* 從網站 tooApp 服務變更如指南 toohello: [Azure 應用程式服務和其對影響現有的 Azure 服務](http://go.microsoft.com/fwlink/?LinkId=529714)
* Hello 舊入口網站 toohello 新入口網站的變更如指南 toohello:[巡覽參考 hello Azure 傳統入口網站](http://go.microsoft.com/fwlink/?LinkId=529715)

> [!NOTE]
> 如果您想 tooget 之前註冊 Azure 帳戶與 Azure 應用程式服務啟動時，請移至太[再試一次應用程式服務](http://go.microsoft.com/fwlink/?LinkId=523751)，可以立即存留較短的入門的 web 應用程式中建立應用程式服務。 不需要信用卡；沒有承諾。
> 
> 

