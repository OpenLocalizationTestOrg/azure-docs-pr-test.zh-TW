---
title: "aaaCreate 工作流程，從 範本-Azure 邏輯應用程式 |Microsoft 文件"
description: "快速入門-利用 Azure 邏輯應用程式範本 tooconnect 應用程式，快速建立工作流程和整合資料。"
author: kevinlam1
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 3656acfb-eefd-4e75-b5d2-73da56c424c9
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: LADocs; klam
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 0127523662a12076772b52968f1e2f9cbad72a1b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-a-workflow-using-a-pre-built-template-or-pattern-tooget-started-quickly"></a>設定使用預先建立的範本或模式 tooget 快速入門工作流程

## <a name="what-are-logic-app-templates"></a>何謂邏輯應用程式範本
邏輯應用程式範本是預先建立的邏輯應用程式，您可以使用 tooquickly 開始建立您自己的工作流程。 

這些範本是很好的方式 toodiscover 各種可以使用邏輯應用程式建立的模式。 您可以使用這些範本做為修改它們 toofit 您的案例。

## <a name="overview-of-available-templates"></a>可用範本概觀
有許多可用的範本目前已發行的 hello 邏輯應用程式平台。 以下列出一些範例類別以及 hello 的連接器，使用的型別。

### <a name="enterprise-cloud-templates"></a>企業雲端範本
此範本會整合 Dynamics CRM、Salesforce、Box、Azure Blob 及其他連接器，以滿足您的企業雲端需求。 部分可使用這些範本來進行的範例包含組織您的潛在客戶和備份企業檔案資料。

### <a name="enterprise-integration-pack-templates"></a>企業整合套件範本
VETER 的組態 （驗證、 擷取、 轉換、 充實、 路由傳送） 管線，接收的 X12 EDI 透過 AS2 文件，並將其轉換 tooXML，以及做為 X12 和 AS2 訊息處理。

### <a name="protocol-pattern-templates"></a>通訊協定模式範本
這些範本由包含通訊協定模式的邏輯應用程式所組成，例如透過 HTTP 的要求回應以及跨 FTP 和 SFTP 的整合。 使用這些現存模式，或將它們做為基礎來建立更複雜的通訊協定模式。  

### <a name="personal-productivity-templates"></a>個人生產力範本
模式 toohelp 改善個人的產能包含範本設定每日提醒，重要的工作項目變成待辦事項清單，以及向 tooa 單一使用者核准步驟的冗長工作自動化。

### <a name="consumer-cloud-templates"></a>取用者雲端範本
與社交媒體服務 (如 Twitter、Slack 和電子郵件) 整合的簡單範本，最終能夠強化社交媒體行銷計劃。 其中也包含多雲複製之類的範本，其可透過節省花在傳統重複性工作的時間來協助提高生產力。 

## <a name="how-toocreate-a-logic-app-using-a-template"></a>如何 toocreate 邏輯應用程式使用的範本
使用邏輯應用程式範本時，啟動 tooget 進入 hello 邏輯應用程式的設計工具。 如果您正在輸入 hello 設計工具開啟現有的邏輯應用程式，hello 邏輯應用程式會自動載入設計工具檢視中。 不過，如果您要建立新的邏輯應用程式，您會看到下列囉 」 畫面。  
 ![](../../includes/media/app-service-logic-templates/template7.png)  

在這個畫面上，您可以選擇 toostart 空白邏輯應用程式或預先建立的範本。 如果您選取其中一個 hello 範本，您會提供其他資訊。 在此範例中，我們使用 hello *Dropbox 中建立新的檔案時，將它複製 tooOneDrive*範本。  
 ![](../../includes/media/app-service-logic-templates/template2.png)  

如果您選擇 toouse hello 範本，只要選取 hello*使用此範本* 按鈕。 系統會詢問 toosign tooyour 根據哪一個連接器 hello 範本使用的帳戶中。 或者，如果您先前已建立使用這些連接器的連線，您可以選取 [繼續]，如下所示。  
 ![](../../includes/media/app-service-logic-templates/template3.png)  

建立 hello 連接，並選取後*繼續*，hello 邏輯應用程式在設計工具的檢視中開啟。  
 ![](../../includes/media/app-service-logic-templates/template4.png)  

Hello 上述範例中，在許多範本，使用的 hello 案例一些 hello 必要的屬性欄位可能填滿 hello 連接器; 內不過，部分可能仍需要值，才能 tooproperly 部署 hello 邏輯應用程式。 如果您嘗試 toodeploy 而不需輸入一些 hello 遺漏的欄位，並出現錯誤訊息就會通知您。

如果您想 tooreturn toohello 範本檢視器，選取 hello*範本*hello 上方導覽列中的按鈕。 藉由切換後 toohello 範本檢視器，您會遺失任何未儲存的進度。 至範本檢視器的先前 tooswitching，您會看到警告訊息，通知您。  
 ![](../../includes/media/app-service-logic-templates/template5.png)  

## <a name="how-toodeploy-a-logic-app-created-from-a-template"></a>如何 toodeploy 邏輯應用程式範本所建立的
一旦您已載入您的範本，並進行任何所需的變更，選取儲存按鈕的 hello hello 左上角。 這可儲存並發佈邏輯應用程式。  
 ![](../../includes/media/app-service-logic-templates/template6.png)  

如果您會喜歡上如何 tooadd 多步驟到現有的邏輯應用程式範本的詳細資訊，或在一般情況下進行編輯，閱讀更多在[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

