---
title: "aaaIssuer 名稱和簽發者金鑰，在 BizTalk 服務 |Microsoft 文件"
description: "深入了解如何 tooretrieve 的簽發者名稱和簽發者金鑰的服務匯流排 」 或 「 存取控制 (ACS) 在 BizTalk 服務中。 MABS，WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 067fe356-d1aa-420f-b2f2-1a418686470a
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: cc84c2820724ae3e7fc7c40ddbcd83a169add911
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="biztalk-services-issuer-name-and-issuer-key"></a>BizTalk 服務：簽發者名稱和簽發者金鑰

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]

Hello 服務匯流排簽發者名稱和簽發者金鑰和 hello 存取控制簽發者名稱和簽發者金鑰，則會使用 azure BizTalk 服務。 具體而言：

| 工作 | 什麼簽發者名稱和簽發者金鑰 |
| --- | --- |
| 從 Visual Studio 部署應用程式 |存取控制簽發者名稱和簽發者金鑰 |
| 設定 hello Azure BizTalk 服務入口網站 |存取控制簽發者名稱和簽發者金鑰 |
| 建立 LOB 轉送以 hello Visual Studio 中的 BizTalk 配接器服務 |服務匯流排簽發者名稱和簽發者金鑰 |

本主題列出 hello 步驟 tooretrieve hello 簽發者名稱和簽發者金鑰。 

## <a name="access-control-issuer-name-and-issuer-key"></a>存取控制簽發者名稱和簽發者金鑰
hello 存取控制簽發者名稱和簽發者金鑰會使用 hello 下列：

* 在 Visual Studio 中建立 Azure BizTalk 服務應用程式： toosuccessfully 部署在 Visual Studio tooAzure BizTalk 服務應用程式，您輸入 hello 存取控制簽發者名稱和簽發者金鑰。 
* hello Azure BizTalk 服務入口網站： 當您建立 BizTalk 服務，再開啟 hello BizTalk 服務入口網站，您的存取控制簽發者名稱和簽發者金鑰就會自動為您的部署與註冊 hello 相同的存取控制值。

### <a name="get-hello-access-control-issuer-name-and-issuer-key"></a>取得 hello 存取控制簽發者名稱和簽發者金鑰

toouse ACS 驗證和 get hello 簽發者名稱和簽發者金鑰值，hello 整體步驟包括：

1. 安裝 hello [Azure Powershell cmdlet](https://azure.microsoft.com/documentation/articles/powershell-install-configure/)。
2. 新增您的 Azure 帳戶：`Add-AzureAccount`
3. 傳回您的訂用帳戶名稱：`get-azuresubscription`
4. 選取您的訂用帳戶：`select-azuresubscription <name of your subscription>` 
5. 建立新的命名空間：`new-azuresbnamespace <name for hello service bus> "Location" -CreateACSNamespace $true -NamespaceType Messaging`

    範例：`new-azuresbnamespace biztalksbnamespace "South Central US" -CreateACSNamespace $true -NamespaceType Messaging`
      
5. （這可能要花費幾分鐘的時間） 建立 hello 新 ACS 命名空間時，會列出 hello 連接字串 hello 簽發者名稱和簽發者金鑰值： 

    ```
    Name                  : biztalksbnamespace
    Region                : South Central US
    DefaultKey            : abcdefghijklmnopqrstuvwxyz
    Status                : Active
    CreatedAt             : 10/18/2016 9:36:30 PM
    AcsManagementEndpoint : https://biztalksbnamespace-sb.accesscontrol.windows.net/
    ServiceBusEndpoint    : https://biztalksbnamespace.servicebus.windows.net/
    ConnectionString      : Endpoint=sb://biztalksbnamespace.servicebus.windows.net/;SharedSecretIssuer=owner;SharedSecretValue=abcdefghijklmnopqrstuvwxyz
    NamespaceType         : Messaging
    ```

toosummarize:  
簽發者名稱 = SharedSecretIssuer  
簽發者金鑰 = SharedSecretKey

有更詳細的 hello [New-azuresbnamespace](https://msdn.microsoft.com/library/dn495165.aspx) cmdlet。 

## <a name="service-bus-issuer-name-and-issuer-key"></a>服務匯流排簽發者名稱和簽發者金鑰
BizTalk 配接器服務會使用服務匯流排簽發者名稱和簽發者金鑰。 在 Visual Studio 中 BizTalk 服務專案中，您可以使用 hello BizTalk 配接器服務 tooconnect tooan 在內部部署的特定業務 (LOB) 系統。 tooconnect，您建立 hello LOB 轉送，並輸入您的 LOB 系統詳細資料。 如此一來，您也輸入 hello 服務匯流排簽發者名稱和簽發者金鑰。

### <a name="tooretrieve-hello-service-bus-issuer-name-and-issuer-key"></a>tooretrieve hello 服務匯流排簽發者名稱和簽發者金鑰
1. 登入 toohello [Azure 傳統入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。
2. 在 hello 左側瀏覽窗格中，選取**Service Bus**。
3. 選取您的命名空間。 在 hello 工作列上，選取 **連接資訊**。 這會顯示 hello**預設簽發者**（簽發者名稱） 和**預設金鑰**（簽發者金鑰）。 您可以複製這些值。  

toosummarize:  
簽發者名稱 = 預設簽發者  
簽發者金鑰 = 預設金鑰

## <a name="next"></a>下一步
其他 Azure BizTalk 服務主題：

* [安裝 hello Azure BizTalk 服務 SDK](http://go.microsoft.com/fwlink/p/?LinkID=241589)<br/>
* [教學課程：Azure BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=236944)<br/>
* [開始使用我要如何 hello Azure BizTalk 服務 SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [Azure BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=303664)<br/>

## <a name="see-also"></a>另請參閱
* [如何： 使用 ACS 管理服務 tooConfigure 服務身分識別](http://go.microsoft.com/fwlink/p/?LinkID=303942)<br/>
* [BizTalk 服務：開發人員、基本、標準和高級版本圖表](http://go.microsoft.com/fwlink/p/?LinkID=302279)<br/>
* [BizTalk 服務：使用 Azure 傳統入口網站進行佈建](http://go.microsoft.com/fwlink/p/?LinkID=302280)<br/>
* [BizTalk 服務：佈建狀態圖](http://go.microsoft.com/fwlink/p/?LinkID=329870)<br/>
* [BizTalk 服務：儀表板、監視和調整索引標籤](http://go.microsoft.com/fwlink/p/?LinkID=302281)<br/>
* [BizTalk 服務：備份與還原](http://go.microsoft.com/fwlink/p/?LinkID=329873)<br/>
* [BizTalk 服務：節流](http://go.microsoft.com/fwlink/p/?LinkID=302282)<br/>

