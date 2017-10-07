---
title: "在 Azure 入口網站 hello aaaCreate Azure BizTalk 服務 |Microsoft 文件"
description: "深入了解如何 tooprovision 或 hello Azure 入口網站; 中建立 Azure BizTalk 服務MABS WABS"
services: biztalk-services
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 3ad18876-a649-40d6-9aa0-1509c1d62c43
ms.service: biztalk-services
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: hero-article
ms.date: 11/07/2016
ms.author: mandia
ms.openlocfilehash: 6781cadada8ac9c84e1fe045d2b0f995811f75b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="create-biztalk-services-using-hello-azure-portal"></a>建立 BizTalk 服務使用 hello Azure 入口網站

> [!INCLUDE [BizTalk Services is being retired, and replaced with Azure Logic Apps](../../includes/biztalk-services-retirement.md)]


> [!TIP]
> toosign toohello Azure 入口網站中的，您需要 Azure 帳戶和 Azure 訂用帳戶。 如果沒有帳戶，您可在幾分鐘內建立免費試用帳戶。 查看 [Azure 免費試用](http://go.microsoft.com/fwlink/p/?LinkID=239738)。


## <a name="CreateService"></a>建立 BizTalk 服務
依據 hello 您選擇的版本，可能提供不是所有的 BizTalk 服務設定。

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。
2. 在 hello 下方瀏覽窗格中，選取**新增**:  
   ![選取 hello 新按鈕][NEWButton]
3. 選取 [應用程式服務]  >  [BIZTALK 服務]  >  [自訂建立]：  
   ![選取 BizTalk 服務] 與選取 [自訂建立]][NewBizTalkService]
4. 輸入 hello BizTalk 服務設定：
   
    <table border="1">
    <tr>
    <td><strong>BizTalk 服務名稱</strong></td>
    <td>您可以輸入任何名稱，但請使用特定的名稱。 部分範例包括：<br/><br/>
    <em>mycompany</em>.biztalk.windows.net<br/>
    <em>mycompanymyapplication</em>.biztalk.windows.net<br/>
    <em>myapplication</em>.biztalk.windows.net<br/><br/>「。 」 會自動新增的 toohello 您所輸入的名稱。 這會建立您的 BizTalk 服務，例如使用的 tooaccess URL <strong>https://<em>myapplication</em>。</strong>。
    </td>
    </tr>
    <tr>
    <td><strong>版本</strong></td>
    <td>如果您是在 hello 測試/開發階段中，選擇 <strong>開發人員</strong>。 如果您是在 hello 生產階段中，使用 hello <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=302279">BizTalk 服務： 版本圖表</a>toodetermine 如果<strong>Premium</strong>，<strong>標準</strong>，或<strong>Basic</strong>是正確的選擇 hello 的商務案例。
    </td>
    </tr>
    <tr>
    <td><strong>區域</strong></td>
    <td>選取 hello 地理區域 toohost BizTalk 服務。</td>
    </tr>
    <tr>
    <td><strong>網域 URL</strong></td>
    <td><strong>選用</strong>。 根據預設，hello 網域 URL 是<em>y</em>。。 您也可輸入自訂網域。 比方說，如果您的網域為 <em>contoso</em>，則可以輸入： <br/><br/>
    <em>MyCompany</em>.contoso.com<br/>
    <em>MyCompanyMyApplication</em>.contoso.com<br/>
    <em>MyApplication</em>.contoso.com<br/>
    <em>YourBizTalkServiceName</em>.contoso.com<br/>
    </td>
    </tr>
    </table>
選取 hello 下一步 箭號。
5. 輸入 hello 儲存體和資料庫設定：  <table border="1">
    <tr>
    <td><strong>監視/封存儲存體帳戶</strong></td>
    <td>選取現有的儲存體帳戶或建立新的儲存體帳戶。 <br/><br/>如果您建立新的儲存體帳戶，請輸入 hello<strong>儲存體帳戶名稱</strong>。</td>
    </tr>
    <tr>
    <td><strong>追蹤資料庫</strong></td>
    <td>如果您使用現有的 Azure SQL Database，其他 BizTalk 服務將無法使用它。 您需要輸入時建立的 Azure SQL Database 伺服器 hello 登入名稱和密碼。<br/><br/><strong>提示</strong>建立 hello 追蹤資料庫和監視/封存儲存體帳戶中的 hello 相同的區域為 hello BizTalk 服務。</td>
    </tr>
    </table>
選取 hello 下一步 箭號。
6. 輸入 hello 資料庫設定：  <table border="1">
    <tr>
    <td><strong>名稱</strong></td>
    <td>時，才能使用<strong>建立新的 SQL Database 執行個體</strong>hello 上一個畫面中選取。
    <br/><br/>
輸入 BizTalk 服務所使用的 SQL 資料庫名稱 toobe。</td>
    </tr>
    <tr>
    <td><strong>伺服器</strong></td>
    <td>時，才能使用<strong>建立新的 SQL Database 執行個體</strong>hello 上一個畫面中選取。
    <br/><br/>
選取現有的 SQL Database 伺服器，或是建立全新的 SQL Database 伺服器。</td>
    </tr>
    <tr>
    <td><strong>伺服器登入名稱</strong></td>
    <td>輸入 hello 登入使用者名稱。</td>
    </tr>
    <tr>
    <td><strong>伺服器登入密碼</strong></td>
    <td>輸入 hello 登入密碼。</td>
    </tr>
    <tr>
    <td><strong>區域</strong></td>
    <td>可在選取 [建立新的 SQL 資料庫執行個體]<strong></strong> 時使用。 選取 hello 地理區域 toohost SQL 資料庫。</td>
    </tr>
    </table>

選取 hello 核取記號 toocomplete hello 精靈。 hello 進度圖示會出現：  
![進度圖示即會顯示][ProgressComplete]

完成時，hello Azure BizTalk 服務已建立且可供應用程式。 hello 預設設定，已足夠。 如果您想 toochange hello 預設設定，請選取**BIZTALK 服務**在 hello 左側瀏覽窗格，然後選取 BizTalk 服務。 其他設定會顯示在 hello[儀表板、 監視器和小數位數的索引標籤](biztalk-dashboard-monitor-scale-tabs.md)hello 頂端。

根據 hello 的 hello BizTalk 服務的狀態，有一些無法完成的作業。 如需這些作業的清單，請移至太[BizTalk Services 狀態圖表](biztalk-service-state-chart.md)。

## <a name="post-provisioning-steps"></a>佈建後續步驟
* [在本機電腦上安裝 hello 憑證](#InstallCert)
* [新增實際執行備妥憑證](#AddCert)
* [取得 hello 存取控制命名空間](#ACS)

#### <a name="InstallCert"></a>在本機電腦上安裝 hello 憑證
自我簽署憑證是 BizTalk 服務佈建的一部分，會在您訂閱 BizTalk 服務時建立並相關聯。 您必須下載此憑證，並將它安裝在您部署 BizTalk 服務應用程式或傳送訊息 tooa BizTalk 服務端點的電腦上。

1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。
2. 選取**BIZTALK 服務**在 hello 左側瀏覽窗格，然後選取您的 BizTalk 服務訂閱。
3. 選取 hello**儀表板** 索引標籤。
4. 選取 [下載 SSL 憑證]：  
   ![修改 SSL 憑證][QuickGlance]
5. 按兩下 hello 憑證，並透過 hello 精靈 tooinstall hello 認證執行。 請確定您已安裝 hello hello 憑證**受信任的根憑證授權單位**儲存。

#### <a name="AddCert"></a>新增實際執行備妥憑證
hello 自我簽署的憑證時建立 BizTalk 服務適用於僅限開發環境中自動建立。 若為生產案例，使用實際執行備妥憑證取代它。

1. 在 hello**儀表板**索引標籤上，選取**更新 SSL 憑證**。
2. 瀏覽 tooyour 私用的 SSL 憑證 (*CertificateName*.pfx)，包括您的 BizTalk 服務名稱，輸入 hello 密碼，然後按一下hello 核取記號。

#### <a name="ACS"></a>取得 hello 存取控制命名空間
1. 登入 toohello [Azure 入口網站](http://go.microsoft.com/fwlink/p/?LinkID=213885)。
2. 選取**BIZTALK 服務**在 hello 左側瀏覽窗格，然後選取 BizTalk 服務。
3. 在 hello 工作列上，選取 **連接資訊**:  
   ![選取 [連線資訊]][ACSConnectInfo]
4. 複製 hello 存取控制值。

從 Visual Studio 部署 BizTalk 服務專案時，您可以輸入此存取控制命名空間。 hello 存取控制命名空間會自動建立 BizTalk 服務。

hello 存取控制項的值可以搭配任何應用程式。 建立 Azure BizTalk 服務時，此存取控制命名空間會控制與 BizTalk 服務部署的 hello 驗證。 如果您想 toochange hello 訂用帳戶或管理 hello 命名空間，請選取**ACTIVE DIRECTORY**在 hello 左側的導覽窗格中，然後選取您的命名空間。 hello 工作列列出您的選項。

按一下**管理**開啟 hello 存取控制管理入口網站。 在 hello 存取控制管理入口網站，hello BizTalk 服務會使用**服務身分識別**:  
![在 hello 存取控制管理入口網站中 ACS 服務身分識別][ACSServiceIdentities]

hello 存取控制服務身分識別是一組認證，讓應用程式或用戶端 tooauthenticate 直接與存取控制，並接收權杖。

> [!IMPORTANT]
> hello BizTalk 服務使用**擁有者**hello 預設服務身分識別和 hello**密碼**值。 如果您使用 hello 對稱金鑰值，而不是 hello 密碼值，hello 下列可能發生錯誤。<br/><br/>*無法以指定的 hello 連接 toohello 存取控制管理服務帳戶認證*
> 
> 

[管理您的 ACS 命名空間](https://msdn.microsoft.com/library/azure/hh674478.aspx) 列出一些指導方針和建議。

## <a name="requirements-explained"></a>說明各項需求
這些需求不會套用 toohello 免費版本。

<table border="1">
<tr bgcolor="FAF9F9">
        <td><strong>您需要什麼</strong></td>
        <td><strong>您為何需要它</strong></td>
</tr>
<tr>
<td>Azure 訂閱</td>
<td>hello 訂用帳戶會決定使用者可以登入 toohello Azure 入口網站。 hello 帳戶持有者會建立在 hello 訂閱<a HREF="https://account.windowsazure.com/Subscriptions">Azure 訂用帳戶</a>。
<br/><br/>
hello Azure 帳戶可以有多個訂用帳戶，可以管理允許的任何人。 例如，您的 Azure 帳戶持有者會建立名為訂用帳戶<em>BizTalkServiceSubscription</em>並可讓您公司內 hello BizTalk 系統管理員 (例如， ContosoBTSAdmins@live.com) 存取 toothis 訂用帳戶。 在此案例中，hello BizTalk 系統管理員登入 toohello Azure 入口網站，並在 hello 訂用帳戶，包括 Azure BizTalk 服務中有完整的系統管理員權限 tooall hello 裝載服務。 hello BizTalk 系統管理員不是 hello Azure 帳戶持有者，並因此不需要存取 tooany 帳單資訊。
<br/><br/>
<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=267577">在 hello Azure 入口網站中管理訂用帳戶和儲存體帳戶</a>提供詳細資訊。
</td>
</tr>
<tr>
<td>Azure SQL Database</td>
<td>儲存 hello 資料表、 檢視和 hello BizTalk 服務，包括 hello 追蹤資料所使用的預存程序。
<br/><br/>
在建立 BizTalk 服務時，您可使用現有的 Azure SQL Server、Azure SQL Database，或自動建立新的伺服器或資料庫。
<br/><br/>
hello SQL Database 的小數位數會自動設定。 一般而言，hello 預設小數位數不足，BizTalk 服務。 變更 hello 標尺將會影響定價。 請參閱 <a HREF="http://go.microsoft.com/fwlink/p/?LinkID=234930">Azure SQL Database 中的帳戶和計費</a>
<br/><br/>
<strong>注意</strong>
<br/>
<ul>
<li> 當您建立新的 Azure SQL Server 和 Database 時，即會自動啟用 Azure 服務。 hello BizTalk 服務需要 Azure 服務啟用。</li>
<li>如果您現有的 Azure SQL Server 上建立新的 Azure SQL Database，hello 的 hello 不會變更伺服器的防火牆規則。 如此一來，便可存取 toohello 伺服器的資料庫不允許其他 Azure 服務。</li>
</ul>
</td>
</tr>
<tr>
<td>Azure 存取控制命名空間</td>
<td>利用 Azure BizTalk 服務進行驗證。 從 Visual Studio 部署 BizTalk 服務專案時，您可以輸入此存取控制命名空間。 當您建立 BizTalk 服務時，會自動建立 hello 存取控制命名空間。</td>
</tr>

<tr>
<td>Azure 儲存體帳戶</td>
<td>提供存取 tootables、 blob 和佇列供您的 BizTalk 服務 toosave hello 下列：

<ul>
<li>記錄檔的監視 hello BizTalk 服務。 監視輸出的 hello 也會顯示在 hello**監視**hello Azure 入口網站中的索引標籤。</li>
<li>建立 X12 或合作夥伴之間的 AS2 協議時，您可以啟用 hello 封存功能 toostore 訊息屬性。 這項資料會儲存在 hello 儲存體帳戶。</li>
</ul>
<br/>
當建立 BizTalk 服務時，您可以使用現有的儲存體帳戶，或自動建立新的儲存體帳戶。
<br/><br/>
hello 預設儲存體設定已足夠的 BizTalk 服務。
<br/><br/>
當建立儲存體帳戶時，會自動建立主要金鑰和次要金鑰。 這些金鑰控制存取 tooyour 儲存體帳戶。 hello BizTalk 服務會自動使用 hello 主索引鍵。
<br/><br/>
請參閱<a HREF="http://go.microsoft.com/fwlink/p/?LinkID=285671">儲存體</a>以取得更多資訊。
</td>
</tr>

<tr>
<td>SSL 專用憑證</td>
<td>
當建立 Azure BizTalk 服務時，也會建立一個 HTTPS URL，其中包括 BizTalk 服務名稱。 此 URL 是自動設定的 toouse 開發階段專用的自我簽署憑證。 若為生產案例，您需要私密的 SSL 憑證。
<br/><br/>
<strong>重要 SSL 憑證資訊</strong>


<ul>
<li>hello 憑證到期日必須是少於 5 年。</li>
<li>所有專用憑證都需要一個密碼。 知道此密碼，而且最佳作法為與系統管理員分享此密碼。</li>
<li>自我簽署憑證是在測試/開發環境中使用。 使用自我簽署的憑證時，匯入 hello 憑證 tooyour 個人憑證存放區和 hello 受信任的根憑證授權單位憑證存放區。</li>
</ul>
<br/>將傳送嗨生產憑證要求 tooyour 憑證授權單位時，會提供下列憑證屬性的 hello:
<br/>

<ul>
<li><strong>增強金鑰使用方法</strong>：Azure BizTalk 服務至少需要伺服器驗證。</li>
<li><strong>一般名稱</strong>： 輸入您的 Azure BizTalk 服務 URL 的 hello 完整的網域名稱 (FQDN)。 請參閱本文中的<a HREF="#CreateService">建立 BizTalk 服務</a>。</li>
</ul>
<br/>
建立 hello BizTalk 服務之後，可以加入新的或不同的憑證。
</td>
</tr>
</table>
<!---Loc Comment: Please, check link [Create a BizTalk Service] since it is not redirecting tooany location.--->



## <a name="hybrid-connections"></a>混合式連線
當您建立 Azure BizTalk 服務時，hello**混合式連線** 索引標籤：

![混合式連線索引標籤][HybridConnectionTab]

混合式連線會使用的 tooconnect Azure 網站或 Azure 行動服務 tooany 內部使用靜態 TCP 連接埠，例如 SQL Server、 MySQL、 HTTP 的 Web Api、 行動服務和大部分的自訂 Web 服務的資源。  混合式連線及 hello BizTalk 配接器服務會有所不同。 hello BizTalk Adapter 服務是使用的 tooconnect Azure BizTalk 服務 tooan 在內部部署企業營運 (LOB) 系統。

 請參閱[混合式連線](integration-hybrid-connection-overview.md)toolearn 更多，包括建立和管理混合式連線。

## <a name="next-steps"></a>後續步驟
現在，建立 BizTalk 服務時，讓自己熟悉如何以不同的 hello [BizTalk 服務： 儀表板、 監視器和調整規模 索引標籤](biztalk-dashboard-monitor-scale-tabs.md)。 您的 BizTalk 服務已準備好可供您的應用程式使用。 建立應用程式，請跳過 toostart[Azure BizTalk 服務](http://go.microsoft.com/fwlink/p/?LinkID=235197)。

## <a name="see-also"></a>另請參閱
* [BizTalk 服務：版本圖表](biztalk-editions-feature-chart.md)<br/>
* [BizTalk 服務：狀態圖表](biztalk-service-state-chart.md)<br/>
* [BizTalk 服務：備份與還原](biztalk-backup-restore.md)<br/>
* [BizTalk 服務：節流](biztalk-throttling-thresholds.md)<br/>
* [BizTalk 服務：簽發者名稱和簽發者金鑰](biztalk-issuer-name-issuer-key.md)<br/>
* [開始使用我要如何 hello Azure BizTalk 服務 SDK](http://go.microsoft.com/fwlink/p/?LinkID=302335)<br/>
* [VNet](integration-hybrid-connection-overview.md)

[NewBizTalkService]: ./media/biztalk-provision-services/WABS_NewBizTalkService.png
[NEWButton]: ./media/biztalk-provision-services/WABS_New.png
[ProgressComplete]: ./media/biztalk-provision-services/WABS_ProgressComplete.png
[ACSConnectInfo]: ./media/biztalk-provision-services/WABS_ACSConnectInformation.png
[QuickGlance]: ./media/biztalk-provision-services/WABS_QuickGlance.png
[ACSServiceIdentities]: ./media/biztalk-provision-services/WABS_ACSServiceIdentities.png
[HybridConnectionTab]: ./media/biztalk-provision-services/WABS_HybridConnectionTab.png
