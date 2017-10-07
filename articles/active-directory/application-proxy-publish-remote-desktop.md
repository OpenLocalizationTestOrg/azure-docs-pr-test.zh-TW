---
title: "使用 Azure AD 應用程式 Proxy 的遠端桌面 aaaPublish |Microsoft 文件"
description: "涵蓋有關 Azure AD 應用程式 Proxy 連接器 hello 基本概念。"
services: active-directory
documentationcenter: 
author: kgremban
manager: femila
editor: harshja
ms.assetid: 
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/11/2017
ms.author: kgremban
ms.custom: it-pro
ms.reviewer: harshja
ms.openlocfilehash: 1174161d0b5ef1157c334970f00ef4f0702a9545
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="publish-remote-desktop-with-azure-ad-application-proxy"></a>使用 Azure AD 應用程式 Proxy 發佈遠端桌面

本文件涵蓋如何 toodeploy 應用程式 proxy 的遠端桌面服務 (RDS)，讓遠端使用者仍能提高生產力。

hello 想要針對這個發行項的對象：
- 目前 Azure AD Application Proxy 客戶希望 toooffer 多個應用程式 tootheir 使用者藉由發行內部應用程式，透過遠端桌面服務。
- 目前遠端桌面服務的客戶想使用 Azure AD Application Proxy 部署 tooreduce hello 受攻擊面。 此案例提供一組有限的雙步驟驗證和條件式存取控制 tooRDS。

## <a name="how-application-proxy-fits-in-hello-standard-rds-deployment"></a>應用程式 Proxy 如何納入 hello 標準 RDS 部署

標準 RDS 部署包含 Windows Server 上執行的各種遠端桌面角色服務。 查看 hello[遠端桌面服務架構](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture)，有多個部署選項。 hello 最明顯差異 hello [RDS 部署與 Azure AD Application Proxy](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/desktop-hosting-logical-architecture) （hello 下列圖表所示） 和 hello 其他部署選項是該 hello 應用程式 Proxy 案例已永久的輸出從執行 hello 連接器服務的 hello 伺服器連接。 其他部署會透過負載平衡器保留開啟的輸入連線。

![Hello RDS VM 和 hello 公用網際網路之間的應用程式 Proxy 位於](./media/application-proxy-publish-remote-desktop/rds-with-app-proxy.png)

在 RDS 部署中，hello RD Web 角色和 hello RD 閘道角色網際網路對向在機器上執行。 這些端點會公開下列原因 hello:
- RD Web 提供 hello 使用者的公用端點 toosign 中，並檢視 hello 各種內部部署應用程式和桌面他們可以存取。 在選取的資源，RDP 連線會使用 hello OS 上的 hello 原生應用程式所建立的。
- RD 閘道進入 hello 圖片，一旦使用者啟動 hello RDP 連接。 hello RD 閘道處理 hello 網際網路透過傳入的 hello 加密 RDP 流量，並將它轉譯的 toohello hello 使用者的內部部署伺服器連線到。 在此案例中，RD 閘道收到 hello 流量 hello 來自 hello Azure AD Application Proxy。

>[!TIP]
>如果您尚未部署之前，RDS，或想要的詳細資訊，在您開始前，了解如何太[順暢地部署與 Azure 資源管理員和 Azure Marketplace 的 RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure)。

## <a name="requirements"></a>需求

- 同時 hello RD Web 和 RD 閘道必須位於端點 hello 相同電腦，以及常見的根目錄。 RD Web 和 RD 閘道將做為單一的應用程式發行，因此您可以擁有單一登入體驗 hello 兩個應用程式之間。

- 您應該已經[部署 RDS](https://technet.microsoft.com/windows-server-docs/compute/remote-desktop-services/rds-in-azure) 並[啟用應用程式 Proxy](active-directory-application-proxy-enable.md)。

- 此案例假設您的使用者移到 Internet Explorer 在 hello RD 網頁進行連接的 Windows 7 或 Windows 10 桌上型電腦上。 如果您需要 toosupport 其他作業系統，請參閱[其他用戶端設定的支援](#support-for-other-client-configurations)。

  >[!NOTE]
  >目前不支援 Windows 10 Creator's Update。

- 在 Internet Explorer 中，啟用 hello RDS ActiveX 附加元件。

## <a name="deploy-hello-joint-rds-and-application-proxy-scenario"></a>部署 hello 聯合 RDS 和應用程式 Proxy 案例

設定好 RDS 和 Azure AD Application Proxy 為您的環境之後，請遵循 hello 步驟 toocombine hello 這兩個方案。 這些步驟逐步解說發行 hello 兩個 web 面對 RDS 端點 （RD Web 和 RD 閘道） 做為應用程式，並再將流量導向您透過應用程式 Proxy 的 RDS toogo 上。

### <a name="publish-hello-rd-host-endpoint"></a>發行 hello RD 主應用程式端點

1. [將新的應用程式 Proxy 應用程式發行](application-proxy-publish-azure-portal.md)以 hello 下列值：
   - 內部 URL: https://\<rdhost\>.com /，其中\<rdhost\>是 hello 常見的根目錄 RD Web 和 RD 閘道的共用。
   - 外部 URL： 這個欄位會自動擴展根據 hello hello 應用程式名稱，但您可以修改它。 您的使用者將會移 toothis URL 存取.rds 時
   - 預先驗證方法︰Azure Active Directory
   - 轉譯 URL 標頭：否
2. 將使用者指派 toohello RD 應用程式發行。 請確定它們都有存取 tooRDS 太。
3. 保留 hello 單一登入方法 hello 應用程式做為**Azure AD 單一登入已停用**。 您的使用者要求 tooauthenticate 一旦 tooAzure AD，另一次 tooRD Web，但沒有單一登入 tooRD 閘道。
4. 跳過**Azure Active Directory** > **應用程式註冊** > *您的應用程式* > **設定**.
5. 選取**屬性**和更新 hello**首頁的 URL**欄位 toopoint tooyour RD Web 端點 (例如 https://\<rdhost\>.com/RDWeb)。

### <a name="direct-rds-traffic-tooapplication-proxy"></a>直接 RDS 流量 tooApplication Proxy

Toohello RDS 部署，以系統管理員身分連接，並變更 hello 部署的 hello RD 閘道伺服器名稱。 這可確保連接經過 hello Azure AD Application Proxy。

1. 連接執行 hello RD 連線代理人角色 toohello RDS 伺服器。
2. 啟動**伺服器管理員**。
3. 選取**遠端桌面服務**hello hello 左側窗格中。
4. 選取 [概觀]。
5. 在 hello 部署概觀 區段中，選取 hello 下拉功能表並選擇**編輯部署屬性**。
6. 在 hello RD 閘道索引標籤上，變更 hello**伺服器名稱**欄位 toohello 您為應用程式 Proxy 中的 hello RD 主機端點的外部 URL。
7. 變更 hello**登入方法**欄位太**密碼驗證**。

  ![在 RDS 上部署內容畫面](./media/application-proxy-publish-remote-desktop/rds-deployment-properties.png)

8. 針對每個集合中，執行下列命令的 hello。 使用您自己的資訊來取代 *\<yourcollectionname\>* 和 *\<proxyfrontendurl\>*。 此命令會啟用 RD Web 和 RD 閘道之間的單一登入，並將效能最佳化︰

   ```
   Set-RDSessionCollectionConfiguration -CollectionName "<yourcollectionname>" -CustomRdpProperty "pre-authentication server address:s:<proxyfrontendurl>`nrequire pre-authentication:i:1"
   ```

   **例如：**
   ```
   Set-RDSessionCollectionConfiguration -CollectionName "QuickSessionCollection" -CustomRdpProperty "pre-authentication server address:s:https://gateway.contoso.msappproxy.net/`nrequire pre-authentication:i:1"
   ```

9. tooverify hello 自訂 RDP 屬性，以及檢視 hello RDP 檔案內容，將會針對此集合中，執行下列命令的 hello RDWeb 從下載的 hello 修改：
    ```
    (get-wmiobject -Namespace root\cimv2\terminalservices -Class Win32_RDCentralPublishedRemoteDesktop).RDPFileContents
    ```

既然您已經設定遠端桌面，Azure AD 應用程式 Proxy 已花費為.rds hello 網際網路對向元件 您可以移除 hello RD Web 和 RD 閘道的機器上的其他公用網際網路對向端點。

## <a name="test-hello-scenario"></a>測試 hello 情節

測試與 Windows 7 或 10 的電腦上的 Internet Explorer 的 hello 案例。

1. 移 toohello 外部 URL 設定，或您的應用程式在 hello [MyApps 面板](https://myapps.microsoft.com)。
2. 系統會詢問 tooauthenticate tooAzure Active Directory。 使用您指派 toohello 應用程式的帳戶。
3. 系統會詢問 tooauthenticate tooRD Web。
4. RDS 驗證成功後，您可以選取 hello 桌面或應用程式，並開始使用。

## <a name="support-for-other-client-configurations"></a>其他用戶端設定的支援

這篇文章所述的 hello 設定是在 Windows 7 或 10、 Internet Explorer 再加上 hello RDS ActiveX 附加元件與使用者。 不過，如果需要，您可以支援其他作業系統或瀏覽器。 hello 差異是在您使用的 hello 驗證方法。

| 驗證方法 | 支援的用戶端設定 |
| --------------------- | ------------------------------ |
| 預先驗證    | 使用 Internet Explorer + RDS ActiveX 附加元件的 Windows 7/10 |
| 通道 | 任何其他作業系統支援 hello Microsoft 遠端桌面應用程式 |

hello 預先驗證流程好處也較多的安全性比 hello 通過資料流程。 使用預先驗證，您可以利用內部部署資源的 Azure AD 驗證功能，例如單一登入、條件式存取和雙步驟驗證。 您也可以確定只有驗證過的流量到達您的網路。

toouse 通過驗證，那里兩個修改 toohello 步驟所述這篇文章：
1. 在[發行 hello RD 主機端點](#publish-the-rd-host-endpoint)步驟 1，以設定 hello 預先驗證方法太**通過**。
2. 在[直接 RDS 流量 tooApplication Proxy](#direct-rds-traffic-to-application-proxy)，完全略過步驟 8。

## <a name="next-steps"></a>後續步驟

[啟用與 Azure AD Application Proxy 的遠端存取 tooSharePoint](application-proxy-enable-remote-access-sharepoint.md)  
[使用 Azure AD 應用程式 Proxy 遠端存取應用程式的安全性考量](application-proxy-security-considerations.md)
