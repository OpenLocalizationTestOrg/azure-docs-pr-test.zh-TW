---
title: "aaaEnterprise b2b-Azure 邏輯應用程式的整合 |Microsoft 文件"
description: "建立 B2B 工作流程和以 hello 企業版整合套件的 logic apps 支援企業整合案例"
services: logic-apps
documentationcenter: .net,nodejs,java
author: msftman
manager: anneta
editor: cgronlun
ms.assetid: dd517c4d-1701-4247-b83c-183c4d8d8aae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/08/2016
ms.author: LADocs; padmavc
ms.openlocfilehash: 8dc866533110b1d07f51cf446056d2ca5ce869ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="overview-b2b-scenarios-and-communication-with-hello-enterprise-integration-pack"></a>概觀： B2B 案例和 hello 企業版整合套件與通訊

企業對企業 (B2B) 工作流程和無縫通訊與 Azure 邏輯應用程式，您可以啟用與 Microsoft 雲端為基礎的解決方案，hello 企業版整合套件的企業整合案例。 組織能以電子方式來交換訊息，即使他們使用不同的通訊協定與格式。 hello 組件會將不同的格式轉換成組織的系統可解譯並處理的格式。 組織可以透過業界標準通訊協定 (包括 [AS2](../logic-apps/logic-apps-enterprise-integration-as2.md)、[X12](logic-apps-enterprise-integration-x12.md) 與 [EDIFACT](../logic-apps/logic-apps-enterprise-integration-edifact.md)) 來交換訊息。 您也可以使用加密與數位簽章來保護訊息的安全。

如果您熟悉 BizTalk Server 或 Microsoft Azure BizTalk 服務，hello 企業整合功能會是簡單 toouse，因為大部分的概念很相似。 一項主要差異是企業整合會使用整合帳戶 toosimplify hello 儲存和管理成品 B2B 通訊中所用。 

在架構上，hello 企業版整合套件根據 「 整合帳戶 」。 這些帳戶是雲端型容器，其中儲存您的所有構件，例如結構描述、合作夥伴、憑證、對應與合約。 您可以使用這些成品 toodesign、 部署和維護 B2B 應用程式和也 logic apps toobuild B2B 工作流程。 但是，您可以使用這些成品之前，您必須先連結整合帳戶 tooyour 邏輯應用程式。 之後，您的邏輯應用程式就可以存取您整合帳戶的構件。

## <a name="why-should-you-use-enterprise-integration"></a>為什麼應該使用企業整合？

* 透過企業整合，您可以在一個位置 (亦即您的整合帳戶) 儲存您的所有構件。
* 您可以建置 B2B 工作流程，並整合協力廠商軟體做為服務 (SaaS) 應用程式、 內部部署應用程式，與自訂應用程式使用 hello Azure 邏輯應用程式的引擎和其所有的連接器。
* 您可以使用 Azure 函式為您的邏輯應用程式建立自訂程式碼。

## <a name="how-tooget-started-with-enterprise-integration"></a>如何 tooget 入門企業整合？

您可以建立和管理 B2B 應用程式，以透過 hello 邏輯應用程式的設計工具中 hello hello Enterprise Integration Pack **Azure 入口網站**。 您也可以使用 [PowerShell](https://msdn.microsoft.com/library/azure/mt652195.aspx "Logic apps PowerShell 主題") 來管理您的邏輯應用程式。

您可以在 hello Azure 入口網站中建立應用程式之前，您必須採取的 hello 高階步驟如下：

![概觀影像](media/logic-apps-enterprise-integration-overview/overview-0.png)  

## <a name="what-are-some-common-scenarios"></a>有哪些常見的案例？

企業整合支援下列產業標準：

* EDI - 電子資料交換
* EAI - 企業應用程式整合

## <a name="heres-what-you-need-tooget-started"></a>以下是您需要啟動 tooget

* 具有整合帳戶的 Azure 訂用帳戶
* Visual Studio 2015 toocreate 對應與結構描述
* [Visual Studio 2015 2.0 適用的 Microsoft Azure Logic Apps 企業整合工具](https://aka.ms/vsmapsandschemas)  

## <a name="try-it-now"></a>立刻嘗試

[部署完全正常運作的範例 AS2 傳送與接收邏輯應用程式](https://github.com/Azure/azure-quickstart-templates/tree/master/201-logic-app-as2-send-receive)hello B2B 功能使用 Azure 邏輯應用程式。

## <a name="learn-more"></a>詳細資訊
* [合約](../logic-apps/logic-apps-enterprise-integration-agreements.md "了解企業整合合約")
* [商務 tooBusiness (B2B) 案例](../logic-apps/logic-apps-enterprise-integration-b2b.md "深入了解如何與 B2B 功能 toocreate Logic apps")  
* [憑證](logic-apps-enterprise-integration-certificates.md "了解企業整合憑證")
* [一般檔案編碼/解碼](logic-apps-enterprise-integration-flatfile.md "深入了解如何 tooencode 及解碼一般檔案內容")  
* [整合帳戶](../logic-apps/logic-apps-enterprise-integration-accounts.md "了解整合帳戶")
* [對應](../logic-apps/logic-apps-enterprise-integration-maps.md "了解企業整合對應")
* [合作夥伴](logic-apps-enterprise-integration-partners.md "了解企業整合夥伴")
* [結構描述](logic-apps-enterprise-integration-schemas.md "了解企業整合結構描述")
* [XML 訊息驗證](logic-apps-enterprise-integration-xml.md "深入了解如何 toovalidate XML 訊息與邏輯應用程式")
* [XML 轉換](logic-apps-enterprise-integration-transform.md "了解企業整合對應")
* [企業整合連接器](../connectors/apis-list.md "了解企業整合套件連接器")
* [整合帳戶中繼資料](../logic-apps/logic-apps-enterprise-integration-metadata.md "深入了解整合帳戶中繼資料")
* [監視 B2B 訊息](logic-apps-monitor-b2b-message.md "深入了解監視 B2B 訊息")
* [在 OMS 入口網站中追蹤 B2B 訊息](logic-apps-track-b2b-messages-omsportal.md "深入了解在 OMS 入口網站中追蹤 B2B 訊息")

