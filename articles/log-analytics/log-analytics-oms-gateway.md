---
title: "使用 aaaConnect 電腦 tooOMS hello OMS 閘道 |Microsoft 文件"
description: "您的 OMS 管理的裝置和 Operations Manager 監視的電腦與 hello OMS 閘道 toosend 資料 toohello OMS 服務時連線沒有網際網路存取。"
services: log-analytics
documentationcenter: 
author: MGoedtel
manager: carmonm
editor: 
ms.assetid: ae9a1623-d2ba-41d3-bd97-36e65d3ca119
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/20/2017
ms.author: magoedte
ms.openlocfilehash: 0cfa8f2fb66016e494f22c780e328be472b5fdee
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="connect-computers-without-internet-access-toooms-using-hello-oms-gateway"></a>電腦沒有網際網路存取 tooOMS 使用 hello OMS 閘道連線

本文件說明如何您 OMS 管理和監視的 System Center Operations Manager 的電腦可以傳送資料 toohello OMS 服務時並沒有網際網路存取。 hello OMS 閘道，這是支援 HTTP 通道 HTTP 正向 proxy 使用 hello HTTP 連接命令，可以收集資料並將它代表它們傳送 toohello OMS 服務。  

hello OMS 閘道支援：

* Azure 自動化混合式 Runbook 背景工作  
* 以 hello Microsoft Monitoring Agent 的 Windows 電腦直接連線 tooan OMS 工作區
* 以 hello OMS Agent for Linux 的 Linux 電腦直接連線 tooan OMS 工作區  
* System Center Operations Manager 2012 SP1 (含 UR7)、Operations Manager 2012 R2 (含 UR3) 或與 OMS 整合的 Operations Manager 2016 管理群組。  

如果您的 IT 安全性原則不允許電腦上點的銷售點 (POS) 裝置或伺服器支援 IT 服務，例如您網路 tooconnect toohello 網際網路，但需要 tooconnect 它們 tooOMS toomanage 和監視它們，也可以設定toocommunicate 直接與 hello OMS 閘道 tooreceive 組態和其代表的轉送資料。  如果這些電腦設定為 hello OMS 代理程式 toodirectly 連接 tooan OMS 工作區中，所有的電腦與 hello OMS 閘道會改為進行通訊。  hello 閘道將資料從傳送嗨代理程式 tooOMS 直接，並不會分析任何在傳輸過程中的 hello 資料。

與 OMS 整合的 Operations Manager 管理群組時，可以是設定的 tooconnect toohello OMS 閘道 tooreceive 組態資訊 hello 管理伺服器，並傳送收集的資料，根據您已啟用的 hello 解決方案。  Operations Manager 代理程式會傳送一些資料，例如 Operations Manager 警示、 組態評估、 執行個體空間和容量資料 toohello 管理伺服器。 其他的大量資料，例如 IIS 記錄檔、 效能及安全性事件會直接傳送 toohello OMS 閘道。  如果您有一或多個 Operations Manager 閘道伺服器部署在周邊網路或其他隔離的網路 toomonitor 不受信任的系統，它無法與 OMS 閘道進行通訊。  Operations Manager 閘道伺服器可以只有報告 tooa 管理伺服器。  Hello proxy 組態資訊以 hello OMS 閘道設定的 toocommunicate Operations Manager 管理群組時，會自動發佈的 tooevery 代理程式管理之電腦的記錄分析設定的 toocollect 資料即使hello 設定為空白。    

tooprovide 高可用性的直接連接或是 Operations 管理群組，將其與 OMS 通訊透過 hello 閘道中您可以使用網路負載平衡 tooredirect 流量並分散 hello 跨越多台閘道伺服器。  如果一個閘道伺服器當機時，hello 流量就會是重新導向的 tooanother 可用的節點。  

建議您執行 hello OMS 閘道軟體 toomonitor hello OMS 閘道的 hello 電腦上安裝 hello OMS 代理程式，並分析事件或效能資料。 此外，hello 代理程式可協助 hello OMS 閘道會識別它需要與 toocommunicate hello 服務結束點。

每個代理程式必須有網路連線 tooits 閘道，代理程式可以自動從 hello 閘道傳輸資料 tooand。 不建議在網域控制站上安裝的 hello 閘道。

hello 下列圖表顯示使用 hello 閘道伺服器的直接代理程式 tooOMS 的資料流程。  代理程式必須具有相同的 hello 其 proxy 設定比對連接埠 hello OMS 閘道是設定的 toocommunicate tooOMS 與。  

![代理程式直接與 OMS 通訊的圖表](./media/log-analytics-oms-gateway/oms-omsgateway-agentdirectconnect.png)

hello 下列圖表顯示來自 Operations Manager 管理群組 tooOMS 資料流程。   

![Operations Manager 與 OMS 通訊的圖表](./media/log-analytics-oms-gateway/oms-omsgateway-opsmgrconnect.png)

## <a name="prerequisites"></a>必要條件

當指定的電腦 toorun hello OMS 閘道，這部電腦必須有下列 hello:

* Windows 10、Windows 8.1、Windows 7
* Windows Server 2016、Windows Server 2012 R2、Windows Server 2012、Windows Server 2008 R2 及 Windows Server 2008
* .Net Framework 4.5
* 至少為 4 核心處理器和 8 GB 記憶體

### <a name="language-availability"></a>提供的語言

hello OMS 閘道有下列語言的 hello:

- 中文 (簡體)
- 中文 (繁體)
- 捷克文
- 荷蘭文
- English
- 法文
- 德文
- 匈牙利文
- 義大利文
- 日文
- 韓文
- 波蘭文
- 葡萄牙文 (巴西)
- 葡萄牙文 (葡萄牙)
- 俄文
- 西班牙文 (國際)

## <a name="download-hello-oms-gateway"></a>下載 hello OMS 閘道

有三種方式 tooget hello 最新版本的 hello OMS 閘道安裝程式檔案。

1. 從 hello 下載[Microsoft Download Center](https://www.microsoft.com/download/details.aspx?id=54443)。

2. 從 hello OMS 入口網站下載。  您登入 tooyour OMS 工作區之後，瀏覽過**設定** > **連線來源** > **Windows 伺服器**按一下**下載 OMS 閘道**。

3. 從 hello 下載[Azure 入口網站](https://portal.azure.com)。  在登入後︰  

   1. 瀏覽 hello 服務清單，然後選取**記錄分析**。  
   2. 選取工作區。
   3. 在 [工作區] 刀鋒視窗的 [一般] 下方，按一下 [快速入門]。
   4. 在下**選擇資料來源 tooconnect toohello 工作區**，按一下 **電腦**。
   5. 在 hello**直接代理程式**刀鋒視窗中，按一下 **下載 OMS 閘道**。<br><br> ![下載 OMS 閘道](./media/log-analytics-oms-gateway/download-gateway.png)


## <a name="install-hello-oms-gateway"></a>安裝 hello OMS 閘道

tooinstall 閘道，請執行下列步驟的 hello。  如果您已安裝舊版，先前稱為*記錄分析轉寄站*，它將會升級 toothis 版本。  

1. Hello 目的地資料夾中，按兩下**OMS Gateway.msi**。
2. 在 hello ** 褖畫惎**頁面上，按一下**下一步**。<br><br> ![閘道設定精靈](./media/log-analytics-oms-gateway/gateway-wizard01.png)<br>
3. 在 [hello**授權合約**頁面上，選取**我接受授權合約 hello 中的 hello 條款**tooagree toohello 使用者授權合約，然後按一下**下一步]**。
4. 在 hello**通訊埠和 proxy 位址**頁面：
   1. 型別 hello TCP 連接埠號碼 toobe 用於 hello 閘道。 安裝程式會使用此連接埠號碼在 Windows 防火牆上設定輸入規則。  hello 預設值為 8080。
      hello 的 hello 通訊埠編號的有效範圍是 1-65535 之間。 如果 hello 輸入不在此範圍內，則會出現錯誤訊息。
   2. （選擇性） 如果 hello hello 閘道所在的伺服器安裝需要 toocommunicate 透過 proxy，請輸入必須 hello 閘道 tooconnect hello proxy 位址。 例如： `http://myorgname.corp.contoso.com:80`。  如果空白，hello 閘道會直接嘗試 tooconnect toohello 網際網路。  如果您的 Proxy 伺服器需要驗證，請輸入使用者名稱與密碼。<br><br> ![閘道精靈 Proxy 組態](./media/log-analytics-oms-gateway/gateway-wizard02.png)<br>   
   3. 按一下 [下一步] 。
5. 如果您沒有啟用 Microsoft Update，hello Microsoft Update 頁面隨即出現，您可以選擇 tooenable 它。 選擇想要的選項，然後按一下下一步。 否則，請繼續 toohello 下一個步驟。
6. 在 [hello**目的地資料夾**] 頁面上，保留 hello 預設資料夾 C:\Program Files\OMS 閘道或型別 hello 位置您想 tooinstall 閘道，然後按一下**下一步**。
7. 在 hello**準備 tooinstall**頁面上，按一下**安裝**。 使用者帳戶控制可能會出現提出要求的權限 tooinstall。 如果有顯示，請按一下 [是]。
8. 安裝完成後，請按一下 [完成]。 您可以確認 hello 服務是否執行 hello services.msc 嵌入式管理單元開啟，並確認**OMS 閘道**會出現在 hello 服務清單，以及其狀態是**執行**。<br><br> ![服務 – OMS 閘道](./media/log-analytics-oms-gateway/gateway-service.png)  

## <a name="configure-network-load-balancing"></a>設定網路負載平衡
您可以設定使用的網路負載平衡 (NLB) 使用 Microsoft 網路負載平衡 (NLB) 或以硬體為依據負載平衡器的高可用性的 hello 閘道。  hello 負載平衡器管理流量重新導向 hello 要求其節點之間的連線從 hello OMS 代理程式或 Operations Manager 管理伺服器。 如果一個閘道伺服器當機時，hello 流量取得重新導向的 tooother 節點。

toolearn 如何 toodesign 和部署 Windows Server 2016 網路負載平衡叢集，請參閱[網路負載平衡](https://technet.microsoft.com/windows-server-docs/networking/technologies/network-load-balancing)。  hello 下列步驟說明如何 tooconfigure Microsoft 網路負載平衡叢集。  

1.  登入 hello Windows 伺服器 hello NLB 叢集的系統管理帳戶的成員。  
2.  在 [伺服器管理員] 中開啟網路負載平衡管理員，然後依序按一下 [工具] 和 [網路負載平衡管理員]。
3. tooconnect hello Microsoft Monitoring Agent 安裝，OMS 閘道伺服器 hello 叢集 IP 位址，以滑鼠右鍵按一下，然後按一下**新增主機 tooCluster**。<br><br> ![網路負載平衡管理員-新增主機 tooCluster](./media/log-analytics-oms-gateway/nlb02.png)<br>
4. 輸入您想 tooconnect hello 閘道伺服器 hello IP 位址。<br><br> ![網路負載平衡管理員-新增主機 tooCluster： 連接](./media/log-analytics-oms-gateway/nlb03.png)

## <a name="configure-oms-agent-and-operations-manager-management-group"></a>設定 OMS 代理程式和 Operations Manager 管理群組
hello 下一節包含有關如何 tooconfigure 直接連線 OMS 的代理程式、 Operations Manager 管理群組或 Azure 自動化 Hybrid Runbook Worker hello OMS 閘道 toocommunicate 與 OMS 的步驟。  

請參閱 toounderstand 需求與步驟上 tooinstall hello 直接連接 tooOMS，Windows 電腦上的 OMS 代理程式的方式[連接的 Windows 電腦 tooOMS](log-analytics-windows-agents.md)或 Linux 電腦，請參閱[Linux 電腦連接tooOMS](log-analytics-linux-agents.md)。

### <a name="configuring-hello-oms-agent-and-operations-manager-toouse-hello-oms-gateway-as-a-proxy-server"></a>為 proxy 伺服器設定 hello OMS 代理程式和 Operations Manager toouse hello OMS 閘道

### <a name="configure-standalone-oms-agent"></a>設定獨立的 OMS 代理程式
請參閱[以 hello Microsoft Monitoring Agent 設定 proxy 和防火牆設定](log-analytics-proxy-firewall.md)設定代理程式 toouse 在此情況下是 hello 閘道的 proxy 伺服器的資訊。  如果您已部署在網路負載平衡器後方的多重閘道伺服器，hello OMS 代理程式 proxy 組態是 hello 虛擬 IP 位址的 hello NLB:<br><br> ![Microsoft Monitoring Agent 內容 – Proxy 設定](./media/log-analytics-oms-gateway/nlb04.png)

### <a name="configure-operations-manager---all-agents-use-hello-same-proxy-server"></a>設定 Operations Manager-hello，所有代理程式使用相同的 proxy 伺服器
設定 Operations Manager tooadd hello 閘道伺服器。  hello Operations Manager 的 proxy 設定，則會自動套用 tooall 代理程式回報 tooOperations 管理員 中，即使 hello 設定為空白。

toouse hello 閘道 toosupport Operations Manager，您必須：

* Microsoft Monitoring Agent (代理程式版本 – **8.0.10900.0**和更新版本) hello 閘道伺服器上安裝及設定您要與其 toocommunicate hello OMS 工作區。
* hello 閘道必須具有網際網路連線，或必須連接的 tooa proxy 伺服器會執行。

> [!NOTE]
> 如果您不指定 hello 閘道的值、 空白值會推入 tooall 代理程式。


1. 開啟 hello Operations Manager 主控台，並在**Operations Management Suite**，按一下 **連接**，然後按一下**設定 Proxy 伺服器**。<br><br> ![Operations Manager – 設定 Proxy 伺服器](./media/log-analytics-oms-gateway/scom01.png)<br>
2. 選取**使用 proxy 伺服器 tooaccess hello Operations Management Suite** ，然後輸入 hello hello OMS 閘道伺服器的 IP 位址或 hello NLB 虛擬 IP 位址。 請確定您以 hello 開頭`http://`前置詞。<br><br> ![Operations Manager – Proxy 伺服器位址](./media/log-analytics-oms-gateway/scom02.png)<br>
3. 按一下 [完成] 。 Operations Manager 伺服器是連線的 tooyour OMS 工作區。

### <a name="configure-operations-manager---specific-agents-use-proxy-server"></a>設定 Operations Manager - 特定代理程式使用 Proxy 伺服器
對於大型或複雜的環境，您可能只想特定伺服器 （或群組） toouse hello OMS 閘道伺服器。  針對這些伺服器，您無法更新 hello Operations Manager 代理程式直接做為這個值會覆寫 hello hello 管理群組的全域值。  而是您需要 toooverride hello 規則用於 toopush 這些值。

> [!NOTE]
> 這個相同的設定技巧，可以將您的環境中使用 tooallow hello 使用多個 OMS 閘道伺服器。  例如，您可能需要特定的 OMS 閘道伺服器 toobe，指定每個區域為基礎。

1. 開啟 hello Operations Manager 主控台並選取 hello**製作**工作區。  
2. 在 hello 撰寫 工作區中，選取 **規則**按一下 hello**範圍**hello Operations Manager 工具列上的按鈕。 如果此按鈕無法使用，請檢查 toomake 確定您已選取的物件而不是資料夾，hello 監視中 窗格中。 hello**管理組件物件決定領域**對話方塊會顯示一般的目標的類別、 群組或物件的清單。
3. 型別**健全狀況服務**在 hello**尋找**欄位，然後選取從 hello 清單。  按一下 [確定] 。  
4. 搜尋 hello 規則**Advisor 的 Proxy 設定規則**在 hello Operations 主控台工具列中，按一下 **會覆寫**然後點太**覆寫 hello Rule\For 類別的特定物件： 健全狀況服務**和從 hello 清單中選取特定的物件。  或者，您可以在其中建立此自訂群組中包含 hello 健全狀況服務物件的 hello 伺服器想 tooapply 此覆寫 tooand，然後套用 hello 覆寫 toothat 群組。
5. 在 hello**覆寫內容**對話方塊方塊中，按一下 tooplace hello 核取記號**覆寫**資料行下一步 toohello **WebProxyAddress**參數。  在 hello**覆寫值**欄位中，輸入您以 hello 開頭的 hello URL hello OMS 閘道伺服器確保`http://`前置詞。
   >[!NOTE]
   > 因為它已自動管理使用覆寫 hello Microsoft System Center Advisor 安全參照覆寫管理組件以 hello Microsoft System Center Advisor 監控伺服器群組中包含不需要 tooenable hello 規則。
   >
6. 請選取管理組件從 hello**選取目的地管理組件**清單，或按一下 建立新的未密封的管理組件**新增**。
7. 當您變更完成時，按一下 [確定]。

### <a name="configure-for-automation-hybrid-workers"></a>設定自動 Hybrid Worker
如果您將自動化 Hybrid Runbook Worker 在您的環境時，hello 下列步驟提供手動、 暫時的因應措施 tooconfigure hello 閘道 toosupport 它們。

在 hello 下列步驟，您會需要 tooknow hello hello 自動化帳戶所在的 Azure 區域。 toolocate hello 位置：

1. 登入 toohello [Azure 入口網站](https://portal.azure.com/)。
2. 選取 hello Azure 自動化服務。
3. 選取 hello 適當的 Azure 自動化帳戶。
4. 在 [位置] 底下檢視其區域。<br><br> ![Azure 入口網站 – 自動化帳戶位置](./media/log-analytics-oms-gateway/location.png)  

使用下列資料表 tooidentify hello URL，針對每個位置的 hello:

**作業執行階段資料服務 URL**

| **位置** | **URL** |
| --- | --- |
| 美國中北部 |ncus-jobruntimedata-prod-su1.azure-automation.net |
| 西歐 |we-jobruntimedata-prod-su1.azure-automation.net |
| 美國中南部 |scus-jobruntimedata-prod-su1.azure-automation.net |
| 美國東部 2 |eus2-jobruntimedata-prod-su1.azure-automation.net |
| 加拿大中部 |cc-jobruntimedata-prod-su1.azure-automation.net |
| 北歐 |ne-jobruntimedata-prod-su1.azure-automation.net |
| 東南亞 |sea-jobruntimedata-prod-su1.azure-automation.net |
| 印度中部 |cid-jobruntimedata-prod-su1.azure-automation.net |
| 日本 |jpe-jobruntimedata-prod-su1.azure-automation.net |
| 澳大利亞 |ase-jobruntimedata-prod-su1.azure-automation.net |

**代理程式服務 URL**

| **位置** | **URL** |
| --- | --- |
| 美國中北部 |ncus-agentservice-prod-1.azure-automation.net |
| 西歐 |we-agentservice-prod-1.azure-automation.net |
| 美國中南部 |scus-agentservice-prod-1.azure-automation.net |
| 美國東部 2 |eus2-agentservice-prod-1.azure-automation.net |
| 加拿大中部 |cc-agentservice-prod-1.azure-automation.net |
| 北歐 |ne-agentservice-prod-1.azure-automation.net |
| 東南亞 |sea-agentservice-prod-1.azure-automation.net |
| 印度中部 |cid-agentservice-prod-1.azure-automation.net |
| 日本 |jpe-agentservice-prod-1.azure-automation.net |
| 澳大利亞 |ase-agentservice-prod-1.azure-automation.net |

如果您的電腦註冊為混合式 Runbook 背景工作會自動進行修補使用 hello 更新管理解決方案，請遵循下列步驟：

1. Hello OMS 閘道上加入 hello 工作執行階段資料服務 Url toohello 允許主控件清單。 例如：`Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
2. 使用下列 PowerShell cmdlet 的 hello，重新啟動 hello OMS 閘道服務：`Restart-Service OMSGatewayService`

如果您的電腦是初始 tooAzure 自動化使用 hello 混合式 Runbook 背景工作註冊 cmdlet，請遵循下列步驟：

1. Hello OMS 閘道上加入 hello 代理程式服務註冊 URL toohello 允許主控件清單。 例如：`Add-OMSGatewayAllowedHost ncus-agentservice-prod-1.azure-automation.net`
2. Hello OMS 閘道上加入 hello 工作執行階段資料服務 Url toohello 允許主控件清單。 例如：`Add-OMSGatewayAllowedHost we-jobruntimedata-prod-su1.azure-automation.net`
3. 重新啟動 hello OMS 閘道服務。
    `Restart-Service OMSGatewayService`

## <a name="useful-powershell-cmdlets"></a>PowerShell Cmdlet
Cmdlet 可協助您完成工作所需的 tooupdate hello OMS 閘道的組態設定。 在您使用它們之前，請務必先：

1. 安裝 hello OMS 閘道 (MSI)。
2. 開啟 PowerShell 主控台視窗。
3. tooimport hello 模組中，輸入下列命令：`Import-Module OMSGateway`
4. 如果未發生錯誤 hello 上一個步驟中，hello 模組已成功匯入和 hello cmdlet 可用。 輸入 `Get-Module OMSGateway`
5. 您可以使用 hello cmdlet 進行變更之後，請重新啟動 hello 閘道服務。

如果您在步驟 3 中收到錯誤，hello 模組未匯入。 PowerShell 無法 toofind hello 模組時，可能會發生 hello 錯誤。 您可以在 hello 閘道的安裝路徑中找到它： *C:\Program Files\Microsoft OMS Gateway\PowerShell*。

| **Cmdlet** | **參數** | **說明** | **範例** |
| --- | --- | --- | --- |  
| `Get-OMSGatewayConfig` |Key |取得 hello hello 服務組態 |`Get-OMSGatewayConfig` |  
| `Set-OMSGatewayConfig` |索引鍵 (必要) <br> 值 |變更 hello hello 服務組態 |`Set-OMSGatewayConfig -Name ListenPort -Value 8080` |  
| `Get-OMSGatewayRelayProxy` | |取得 hello proxy 位址的轉送 （上游） |`Get-OMSGatewayRelayProxy` |  
| `Set-OMSGatewayRelayProxy` |位址<br> 使用者名稱<br> 密碼 |Hello 位址 （和認證） 的轉送 （上游） proxy 設定 |1.設定回覆 Proxy 和認證：<br> `Set-OMSGatewayRelayProxy`<br>`-Address http://www.myproxy.com:8080`<br>`-Username user1 -Password 123` <br><br> 2.設定不需要驗證的回覆 Proxy：`Set-OMSGatewayRelayProxy`<br> `-Address http://www.myproxy.com:8080` <br><br> 3.清除 hello 轉送的 proxy 設定：<br> `Set-OMSGatewayRelayProxy` <br> `-Address ""` |  
| `Get-OMSGatewayAllowedHost` | |取得 hello 目前允許主應用程式 （僅限 hello 本機設定允許的主機，不包括允許的主機會自動下載） |`Get-OMSGatewayAllowedHost` |
| `Add-OMSGatewayAllowedHost` |主機 (必要) |新增允許清單的 hello 主機 toohello |`Add-OMSGatewayAllowedHost -Host www.test.com` |  
| `Remove-OMSGatewayAllowedHost` |主機 (必要) |Hello 主機移除 hello 允許清單 |`Remove-OMSGatewayAllowedHost`<br> `-Host www.test.com` |  
| `Add-OMSGatewayAllowedClientCertificate` |主體 (必要) |新增 hello 用戶端憑證主旨 toohello 允許清單 |`Add-OMSGatewayAllowed`<br>`ClientCertificate` <br> `-Subject mycert` |  
| `Remove-OMSGatewayAllowedClientCertificate` |主體 (必要) |移除 hello 允許清單中的 hello 用戶端憑證的主體 |`Remove-OMSGatewayAllowed` <br> `ClientCertificate` <br> `-Subject mycert` |  
| `Get-OMSGatewayAllowedClientCertificate` | |取得 hello 目前允許用戶端憑證主體 （只有在本機 hello 設定允許的主體，不包括自動下載允許的主旨） |`Get-`<br>`OMSGatewayAllowed`<br>`ClientCertificate` |  

## <a name="troubleshooting"></a>疑難排解
toocollect hello 閘道所記錄的事件，您需要 tooalso hello 安裝 OMS 代理程式。<br><br> ![事件檢視器 – OMS 閘道記錄](./media/log-analytics-oms-gateway/event-viewer.png)

**OMS 閘道事件識別碼與描述**

hello 下表顯示 hello 事件識別碼和 OMS 閘道記錄檔事件的描述。

| **識別碼** | **描述** |
| --- | --- |
| 400 |沒有特定識別碼的任何應用程式錯誤 |
| 401 |錯誤組態。 例如：listenPort = "text"，而不是整數 |
| 402 |剖析 TLS 交握訊息時發生例外狀況 |
| 403 |網路錯誤。 例如： 無法連接 tootarget 伺服器 |
| 100 |一般資訊 |
| 101 |服務已經啟動 |
| 102 |服務已經停止 |
| 103 |已從用戶端接收到 HTTP CONNECT 命令 |
| 104 |不是 HTTP CONNECT 命令 |
| 105 |目的地伺服器不在允許清單或 hello 目的地連接埠不是安全的連接埠 (443) <br> <br> 請確認閘道伺服器上的該 hello MMA 代理程式，然後 hello 代理程式通訊以 hello 閘道已連接的 toohello 相同的記錄分析工作區。 |
| 105 |ERROR TcpConnection – 無效的用戶端憑證: CN=Gateway <br><br> 請確定： <br>    <br> &#149; 您是使用版本號碼為 1.0.395.0 或更新版本的閘道。 <br> &#149;hello MMA 閘道伺服器上的代理程式和 hello 代理程式通訊以 hello 閘道是連接的 toohello 相同的記錄分析工作區。 |
| 106 |任何 hello TLS 工作階段是可疑和已拒絕的原因 |
| 107 |hello TLS 工作階段已經過驗證 |

**效能計數器 toocollect**

hello 下表顯示 hello 適用於 hello OMS 閘道的效能計數器。 您可以新增使用效能監視器的 hello 計數器。

| **名稱** | **描述** |
| --- | --- |
| OMS 閘道/使用中用戶端連線 |使用中用戶端網路 (TCP) 連線數目 |
| OMS 閘道/錯誤計數 |錯誤數目 |
| OMS 閘道/已連線用戶端 |已連線用戶端數目 |
| OMS 閘道/拒絕計數 |拒絕由於 tooany TLS 驗證錯誤的數目 |

![OMS 閘道效能計數器](./media/log-analytics-oms-gateway/counters.png)

## <a name="get-assistance"></a>取得協助
登入的 toohello Azure 入口網站時，您可以建立與 hello OMS 閘道或其他 Azure 服務或服務功能的協助的要求。
toorequest 協助，請按一下 hello 右上角的 hello 入口網站中的 hello 問號符號，然後按一下**新增支援要求**。 接著，完成 hello 新支援要求表單。

![新增支援要求](./media/log-analytics-oms-gateway/support.png)

您也可以將留在 hello OMS 或記錄分析相關的意見反應[Microsoft Azure 意見反應論壇](https://feedback.azure.com/forums/267889)。

## <a name="next-steps"></a>後續步驟
* [將資料來源加入](log-analytics-data-sources.md)toocollect 資料 hello 連接您的 OMS 工作區的來源，並將它儲存在 hello OMS 儲存機制。
