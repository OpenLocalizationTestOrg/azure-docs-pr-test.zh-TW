---
title: "在 Azure 邏輯應用程式的內部部署 aaaAccess 資料來源 |Microsoft 文件"
description: "設定 hello 在內部部署資料閘道，讓您可以從邏輯應用程式存取內部部署資料來源"
keywords: "存取資料, 內部部署, 資料傳輸, 加密, 資料來源"
services: logic-apps
author: jeffhollan
manager: anneta
editor: 
documentationcenter: 
ms.assetid: 6cb4449d-e6b8-4c35-9862-15110ae73e6a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 07/13/2017
ms.author: LADocs; dimazaid; estfan
ms.openlocfilehash: 1d3deaac5a095316ce78e224dab0c08559bc2ff2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="access-data-sources-on-premises-from-logic-apps-with-hello-on-premises-data-gateway"></a>在從邏輯應用程式使用 hello 在內部部署資料閘道的內部部署存取資料來源

在您的 logic apps，從內部部署 tooaccess 資料來源設定邏輯應用程式可以使用支援的連接器的內部部署資料閘道。 hello gateway 是做為提供快速的資料傳輸和加密您的 logic apps 在內部部署資料來源之間的橋樑。 hello 閘道轉送上 hello Azure Service Bus 透過加密通道在內部部署來源的資料。 所有流量都來自為 hello 閘道代理程式的安全輸出流量。 深入了解[hello 資料閘道的運作方式](logic-apps-gateway-install.md#gateway-cloud-service)。 

hello 閘道支援連線 toothese 資料來源，在內部部署：

*   BizTalk Server 2016
*   DB2  
*   檔案系統
*   Informix
*   MQ
*   MySQL
*   Oracle 資料庫
*   PostgreSQL
*   SAP 應用程式伺服器 
*   SAP 訊息伺服器
*   SharePoint
*   SQL Server
*   Teradata

這些步驟顯示如何 tooset hello 註冊內部部署資料閘道 toowork 隨應用程式邏輯。 如需所支援連接器的詳細資訊，請參閱 [Azure Logic Apps 的連接器](../connectors/apis-list.md)。 

如需如何 toouse hello 閘道與其他服務資訊，請參閱下列文章：

*   [Microsoft Power BI 內部部署資料閘道](https://powerbi.microsoft.com/documentation/powerbi-gateway-onprem/)
*   [Azure Analysis Services 內部部署資料閘道](../analysis-services/analysis-services-gateway.md)
*   [Microsoft Flow 內部部署資料閘道](https://flow.microsoft.com/documentation/gateway-manage/)
*   [Microsoft PowerApps 內部部署資料閘道](https://powerapps.microsoft.com/tutorials/gateway-management/)

## <a name="requirements"></a>需求

* 您必須已經[hello 資料閘道安裝在本機電腦上](logic-apps-gateway-install.md)。

* 當您登入 toohello Azure 入口網站時，您可以 toouse hello 相同的工作或學校帳戶，使用了太[安裝 hello 在內部部署資料閘道](logic-apps-gateway-install.md#requirements)。 Hello Azure 入口網站中建立的閘道安裝閘道資源時，您登入的帳戶也必須具有 Azure 訂用帳戶 toouse。

* 您的閘道安裝不能已由 Azure 閘道資源加以宣告。 您可以將閘道安裝 tooonly 一個 Azure 閘道資源產生關聯。 當您建立 hello 閘道資源以便 hello 安裝不適用於其他資源時，就會發生宣告。

## <a name="set-up-hello-data-gateway-connection"></a>Hello 資料閘道連接設定

### <a name="1-install-hello-on-premises-data-gateway"></a>1.安裝 hello 在內部部署資料閘道

如果您還沒有這麼做，請遵循 hello[步驟 tooinstall hello 在內部部署資料閘道](logic-apps-gateway-install.md)。 在繼續 hello 之前的其他步驟，請確定您在本機電腦上安裝 hello 資料閘道。

<a name="create-gateway-resource"></a>
### <a name="2-create-an-azure-resource-for-hello-on-premises-data-gateway"></a>2.建立 hello 在內部部署資料閘道的 Azure 資源

您在本機電腦上安裝 hello 閘道之後，您必須建立您的 data gateway 為 Azure 中的資源。 此步驟也會讓閘道資源與 Azure 訂用帳戶產生關聯。

1. 登入 toohello [Azure 入口網站](https://portal.azure.com "Azure 入口網站")。 請確定 toouse hello 相同的 Azure 工作或學校電子郵件地址使用 tooinstall hello 閘道。

2. 在 Azure 中的 hello 左功能表中選擇**新增** > **企業整合** > **在內部部署資料閘道**如下所示：

   ![尋找 [內部部署資料閘道]](./media/logic-apps-gateway-connection/find-on-premises-data-gateway.png)

3. 在 hello**建立連接閘道**刀鋒視窗中，提供這些詳細資料 toocreate 您的資料閘道資源：

    * **名稱**：輸入閘道資源的名稱。 

    * **訂用帳戶**： 選取 hello Azure 訂用帳戶 tooassociate 與閘道資源。 
    此訂用帳戶應為 hello 邏輯應用程式相同訂用帳戶。
   
      hello 預設訂用帳戶根據 hello 用 toosign 中的 Azure 帳戶。

    * **資源群組**：建立資源群組或選取現有資源群組來部署閘道資源。 
    資源群組可協助您集合管理相關的 Azure 資產。

    * **位置**: Azure 限制此位置 toohello hello 閘道器雲端服務時所選取的相同區域[閘道安裝](logic-apps-gateway-install.md)。 

      > [!NOTE]
      > 請確定 hello 閘道資源位置符合 hello 閘道雲端服務的位置。 否則，閘道安裝可能不會出現在您 tooselect hello 安裝閘道的清單中 hello 下一個步驟中。
      > 
      > 閘道資源和邏輯應用程式可使用不同的區域。

    * **安裝名稱**： 如果尚未選取閘道安裝，請選取您先前安裝的 hello 閘道。 

    tooadd hello 閘道資源 tooyour Azure 儀表板中，選擇**Pin toodashboard**。 
    完成之後，請選擇 [建立]。

    例如：

    ![提供詳細資料 toocreate 您的內部部署資料閘道](./media/logic-apps-gateway-connection/createblade.png)

    您的 data gateway，任何時候 hello 主要 Azure 左窗格中，從 toofind 或檢視表太移**更服務** > **企業整合** > **在內部部署資料閘道**。

    ![移太 「 多個服務 」，「 企業整合 」，「 內部部署資料閘道 」](./media/logic-apps-gateway-connection/find-on-premises-data-gateway-enterprise-integration.png)

<a name="connect-logic-app-gateway"></a>
### <a name="3-connect-your-logic-app-toohello-on-premises-data-gateway"></a>3.連接邏輯應用程式 toohello 在內部部署資料閘道

現在您已建立您的資料閘道資源，並與該資源相關聯 Azure 訂用帳戶，建立邏輯應用程式與 hello 資料閘道之間的連線。

> [!NOTE]
> 閘道連線您的位置必須存在於 hello 相同區域，做為應用程式邏輯，但您可以使用存在的資料閘道位於不同的區域。

1. 在 hello Azure 入口網站，建立或開啟邏輯應用程式邏輯應用程式的設計工具中。

2. 新增支援內部部署連線的連接器 (例如 SQL Server)。

3. 遵循 hello 順序如下所示，選取**連接透過內部部署資料閘道**，提供唯一的連接名稱和 hello 必要的資訊，然後選取您想 toouse hello 資料閘道資源。 完成之後，請選擇 [建立]。

   > [!TIP]
   > 唯一的連線名稱可在之後協助您輕鬆識別該連線，尤其是當您建立了多個連線時。 如果適用的話，也包含 hello 合格的網域使用者名稱。 

   ![建立邏輯應用程式與資料閘道之間的連線](./media/logic-apps-gateway-connection/blankconnection.png)

恭喜，您的閘道連線已準備好您的邏輯應用程式 toouse 進行。

## <a name="edit-your-gateway-connection-settings"></a>編輯閘道連線設定

邏輯應用程式建立的閘道連接之後，您可能想 toolater 更新 hello 設定為該特定的連接。

1. toofind hello 閘道連線：

   * Hello 邏輯應用程式 刀鋒視窗，在**開發工具**，選取**API 連線**。 
   
     hello **API 連線** 窗格會顯示邏輯應用程式，包括閘道連線相關聯的所有應用程式開發介面連線。

     ![移 tooyour 邏輯應用程式中，選取 [API 連線]](./media/logic-apps-gateway-connection/logic-app-find-api-connections.png)

   * 或從 hello 主要 Azure 左窗格中，移過**更服務** > **Web 和行動服務** > **API 連線**對於所有應用程式開發介面的連線，包括閘道連線，與您 Azure 訂用帳戶相關聯。 

   * 或在 hello 主要 Azure 左窗格中，移過**所有資源**對於所有應用程式開發介面的連線，包括您 Azure 訂用帳戶相關聯的閘道連線。

2. 選取您想要 tooview 或編輯，並選擇 hello 閘道連接**編輯 API 連線**。

   > [!TIP]
   > 如果您的更新才會生效，請嘗試[停止並重新啟動 hello 閘道 Windows 服務](./logic-apps-gateway-install.md#restart-gateway)。

<a name="change-delete-gateway-resource"></a>
## <a name="switch-or-delete-your-on-premises-data-gateway-resource"></a>切換或刪除內部部署資料閘道資源

toocreate 不同閘道資源時，將您的閘道與不同的資源，建立關聯或移除 hello 閘道資源，您可以刪除 hello 閘道資源，而不會影響 hello 閘道安裝。 

1. 從 hello 主要 Azure 左窗格中，移過**所有資源**。 
2. 尋找並選取資料閘道資源。
3. 選擇**在內部部署資料閘道**，hello 資源在工具列上，選擇 **刪除**。

<a name="faq"></a>
## <a name="frequently-asked-questions"></a>常見問題集

[!INCLUDE [existing-gateway-location-changed](../../includes/logic-apps-existing-gateway-location-changed.md)]

## <a name="next-steps"></a>後續步驟

* [保護邏輯應用程式](./logic-apps-securing-a-logic-app.md)
* [Logic Apps 範例和常見案例](./logic-apps-examples-and-scenarios.md)
