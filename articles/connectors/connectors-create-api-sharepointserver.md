---
title: "aaaUse hello 邏輯應用程式中的 SharePoint 伺服器連接器 |Microsoft 文件"
description: "開始使用邏輯應用程式中的 hello hello SharePoint 伺服器連接器"
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 0238a060-d592-4719-b7a2-26064c437a1a
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/18/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 3b814f42611e4971ff5c94ae3b021829217911dc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-sharepoint-connector"></a>開始使用 hello SharePoint 連接器
hello SharePoint 連接器提供清單方式的 toowork SharePoint 上。

從建立邏輯應用程式開始，請參閱[建立邏輯應用程式](../logic-apps/logic-apps-create-a-logic-app.md)。

## <a name="create-a-connection-toosharepoint"></a>建立連接 tooSharePoint
toouse hello SharePoint 連接器，請先建立**連接**然後提供這些屬性中的 hello 詳細資料： 

| 屬性 | 必要 | 說明 |
| --- | --- | --- |
| 權杖 |是 |提供 SharePoint 的認證 |

tooconnect 太**SharePoint**，輸入您的身分識別 （使用者名稱和密碼、 智慧卡認證等） tooSharePoint。 一旦您已驗證，您可以繼續 toouse hello SharePoint 連接器應用程式邏輯中。 

在 hello 設計工具中的應用程式邏輯，請依照這些步驟 toosign SharePoint toocreate hello 連線到**連接**邏輯應用程式中使用：

1. 輸入 SharePoint hello [搜尋] 方塊中，並等候 hello 搜尋 tooreturn hello 名稱中在與 SharePoint 的所有項目：   
   ![設定 SharePoint][1]  
2. 選取 [SharePoint - 當檔案建立時]   
3. 選取**登入 tooSharePoint**:   
   ![設定 SharePoint][2]    
4. 提供與 SharePoint 中 tooauthenticate 您 SharePoint 認證 toosign   
   ![設定 SharePoint][3]     
5. Hello 驗證完成後，您應該重新導向的 tooyour 邏輯應用程式 toocomplete 它藉由設定 SharePoint 的**會建立一個檔案**對話方塊。          
   ![設定 SharePoint][4]  
6. 然後，您可以加入其他觸發程序，您需要 toocomplete 邏輯應用程式的動作。   
7. 儲存您的工作，藉由選取**儲存**hello 上方的功能表列上。  

## <a name="connector-specific-details"></a>連接器特定的詳細資料

檢視任何觸發程序和動作中 hello swagger 定義，另請參閱 hello 的任何限制[連接器詳細資料](/connectors/sharepoint/)。

## <a name="more-connectors"></a>其他連接器
返回 toohello [Api 清單](apis-list.md)。

[1]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig1.png  
[2]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig2.png 
[3]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig3.png
[4]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig4.png
[5]: ../../includes/media/connectors-create-api-sharepointonline/connectionconfig5.png
