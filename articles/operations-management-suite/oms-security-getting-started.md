---
title: "aaaGetting 開始使用 Operations Management Suite 安全性和稽核解決方案 |Microsoft 文件"
description: "此文件將協助您 tooget 入門 Operations Management Suite 安全性和稽核解決方案功能 toomonitor 混合式雲端。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: mbaldwin
editor: 
ms.assetid: 754796ef-a43e-468a-86c9-04a2eda55b5b
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: get-started-article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2017
ms.author: yurid
ms.openlocfilehash: 5cb3e5dbb3e60f9702a34c9413ddc1bf2b14b411
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="getting-started-with-operations-management-suite-security-and-audit-solution"></a>開始使用 Operations Management Suite 安全性和稽核解決方案
本文帶領您認識每個選項，協助您快速開始使用 Operations Management Suite (OMS) 安全性和稽核解決方案功能。

## <a name="what-is-oms"></a>何謂 OMS？
Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。 關於 OMS 的詳細資訊，請參閱 hello 文章[Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)。

## <a name="oms-security-and-audit-dashboard"></a>OMS 安全性和稽核儀表板
hello OMS 安全性和稽核 」 解決方案可讓您完整檢視組織的 IT 安全性狀況，針對值得您注意的問題使用內建的搜尋查詢。 hello**安全性和稽核**儀表板是所有項目 hello 主畫面相關 toosecurity 在 OMS 中的。 會提供在電腦的 hello 安全性狀態的高層級深入。 它也包含 hello 能力 tooview hello 過去 24 小時、 7 天的所有事件或任何其他自訂的時間範圍。 tooaccess hello**安全性和稽核**儀表板，請遵循下列步驟：

1. 在 hello **Microsoft Operations Management Suite**主要儀表板按一下**設定**hello 方的磚。
2. 在 hello**設定**刀鋒視窗底下**解決方案**按一下**安全性和稽核**選項。
3. hello**安全性和稽核**儀表板會顯示：
   
    ![OMS 安全性和稽核儀表板](./media/oms-security-getting-started/oms-getting-started-fig1-ga.png)

如果您要存取此儀表板 hello 第一次，您不需要 OMS 監視的裝置 hello 磚將不會填入取自 hello 代理程式的資料。 一旦您安裝 hello 代理程式時，可能需要一些時間 toopopulate，因此您看到一開始可能會遺失某些資料因為它們仍在上傳 toohello 雲端。  在此情況下，它是一般 toosee 某些磚沒有具體的資訊。 讀取[連接的 Windows 電腦直接 tooOMS](https://technet.microsoft.com/library/mt484108.aspx)如需有關如何 tooinstall OMS 代理程式在 Windows 系統和[連線 Linux 電腦 tooOMS](https://technet.microsoft.com/library/mt622052.aspx)如需有關如何 tooperform 這項工作在 Linux 系統中。

> [!NOTE]
> hello 代理程式會收集 hello 資訊根據 hello 目前事件已啟用，例如電腦名稱、 IP 位址和使用者名稱。 但不會收集任何文件/檔案、資料庫名稱或私人資料。   
> 
> 

解決方案是邏輯、視覺效果和資料擷取規則的集合，可解決客戶所面臨的重要挑戰。 「安全性和稽核」是其他人可以個別新增的一種解決方案。 閱讀文章 hello[新增解決方案](https://technet.microsoft.com/library/mt674635.aspx)如需有關如何 tooadd 新方案。

hello OMS 安全性和稽核儀表板分為四個主要類別：

* **安全性網域**： 在此區域中，您將無法能 toofurther 探索安全性記錄一段時間，存取惡意程式碼評估、 更新評估、 網路安全性、 身分識別和存取資訊、 電腦與安全性事件並能快速地存取 tooAzure 資訊安全中心儀表板。
* **值得注意的問題**： 此選項可讓您 tooquickly 識別作用中問題的 hello 數目和 hello 這些問題的嚴重性。
* **偵測 （預覽）**： 可讓您透過視覺化安全性警示，因為它們對您的資源進行的 tooidentify 攻擊的模式。
* **威脅情報**： 可讓您所視覺化的具有惡意連出 IP 流量、 hello 惡意之威脅類型和顯示來自這些 Ip 其中的對應伺服器 hello 總數的 tooidentify 攻擊的模式。 
* **常見安全性查詢**： 這個選項提供您一份 hello 最常見安全性查詢，您可以使用 toomonitor 您的環境。 當您按一下其中一個這些查詢中時，它會開啟 hello**搜尋**hello 結果該查詢的刀鋒視窗。

> [!NOTE]
> 如需 OMS 如何保留您的資料安全的詳細資訊，請閱讀「OMS 如何保護您的資料」。
> 
> 

## <a name="security-domains"></a>安全性網域
監視資源時，重要 toobe 無法 tooquickly 存取 hello 目前狀態的環境。 不過也很重要的 toobe 無法 tootrack 後發生的事件，hello 過去可能導致 tooa 進一步了解這為什麼在特定時間點您環境中的時間。 

> [!NOTE]
> 資料保留根據 toohello OMS 定價方案。 如需詳細資訊，請造訪 hello [Microsoft Operations Management Suite](https://www.microsoft.com/server-cloud/operations-management-suite/pricing.aspx)定價頁面。
> 
> 

事件的回應和鑑識調查情況直接將從中獲益 hello 結果會提供在 hello**經過一段時間的安全性記錄**磚。

![一段時間的安全性記錄](./media/oms-security-getting-started/oms-getting-started-fig2.JPG)

當您按一下這個磚時，hello**搜尋**隨即會開啟刀鋒視窗，顯示查詢結果**安全性事件**(類型 = SecurityEvents) 與資料是根據 hello 過去七天，如下所示：

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![一段時間的安全性記錄](./media/oms-security-getting-started/oms-getting-started-fig3.JPG)

hello 搜尋結果會分割成兩個窗格： hello 的左的窗格可讓您找不到，hello 電腦中的這些事件找不到，帳戶所探索到這些電腦中的 hello 數目和 hello 類型的安全性事件的 hello 數目的細目活動。 hello 右窗格會提供您 hello 總結果和 hello 電腦的名稱和事件的活動與 hello 安全性事件的時間檢視。 您也可以按一下**顯示更多**tooview 更詳細說明有關此事件，例如 hello 事件資料、 hello 事件識別碼和 hello 事件來源。

> [!NOTE]
> 如需 OMS 搜尋查詢的詳細資訊，請參閱 [OMS 搜尋參考](https://technet.microsoft.com/library/mt450427.aspx)。
> 
> 

### <a name="antimalware-assessment"></a>反惡意程式碼評估
此選項會啟用您 tooquickly 識別電腦和保護不足和都遭到惡意軟體的電腦。 惡意程式碼評估狀態 hello 監視伺服器上偵測到的威脅閱讀，並再 hello 資料會傳送 toohello OMS 服務進行處理的 hello 雲端中。 偵測到威脅及保護效力不足的伺服器會顯示 hello 惡意程式碼評定儀表板中，也就是可存取在 hello 按一下後**反惡意程式碼評定**磚。 

![惡意程式碼評估](./media/oms-security-getting-started/oms-getting-started-fig4-ga.png)

就像任何其他動態磚提供 OMS 儀表板中，當您按一下它，hello**搜尋**hello 查詢結果將會開啟刀鋒視窗。 針對這個選項，如果您按一下 hello**未回報**選項在**保護狀態**，您必須 hello 查詢結果會顯示包含 hello 電腦的名稱和其陣序規範，與此單一項目如下所示：

![搜尋結果](./media/oms-security-getting-started/oms-getting-started-fig5.png)

> [!NOTE]
> *順位*是提供 tooreflect hello 狀態的 hello 保護等級 （on、 off、 更新，等等） 以及發現的威脅。 讓，成為數字的協助 toomake 彙總。
> 
> 

如果您按一下 hello 電腦名稱中，您必須 hello hello 保護狀態，此電腦的時間檢視。 這是非常有用的案例，您需要 toounderstand 如果 hello 反惡意程式碼曾安裝，以及在某個時間點已移除。   

### <a name="update-assessment"></a>更新評估
此選項可讓您 tooquickly 判斷 hello 整體曝光 toopotential 安全性問題，以及是否或重要性這些更新適用於您的環境。 OMS 安全性和稽核解決方案只提供這些更新的 hello 視覺效果、 hello 實際資料是來自[更新管理解決方案](oms-solution-update-management.md)，這是在不同的模組，在 OMS 中。 這裡 hello 更新的範例：

![系統更新](./media/oms-security-getting-started/oms-getting-started-fig6-new.png)

> [!NOTE]
> 如需更新管理解決方案的詳細資訊，請參閱[在 OMS 中更新管理解決方案](oms-solution-update-management.md)。
> 
> 

### <a name="identity-and-access"></a>身分識別與存取
識別應與 hello 控制您的企業，保護您的身分識別的平面應為您的優先考量。 雖然在 hello 過去發生周圍組織的周邊和這些周邊是其中一個 hello 主要防禦界限，screen 鍵移動 toohello 雲端的更多應用程式詳細資料與 hello 身分識別會變得 hello 新周邊。 

> [!NOTE]
> 目前 hello 資料只會根據在 hello 未來 Office365 登入的安全性事件登入資料 （事件識別碼 4624），Azure AD 資料也會包含在內。
> 
> 

監視您的身分識別活動您會無法 tootake 預防措施事件之前或反應動作 toostop 攻擊。 hello**身分識別和存取**儀表板會提供您的身分識別狀態，包括 hello 期間每次嘗試後，帳戶已鎖定，所使用的 hello 使用者帳戶上的失敗的嘗試 toolog 數目的概觀具有帳戶變更或重設密碼和目前的登入的帳戶數目。 

當您按一下在 hello**身分識別和存取**您會看到 hello 下列儀表板的磚：

![身分識別與存取](./media/oms-security-getting-started/oms-getting-started-fig7-ga.png)

此儀表板中可用的 hello 資訊可以立即協助 tooidentify 潛在可疑的活動。 例如，有 338 嘗試 toolog 上做為**管理員**和 100%的這些嘗試失敗。 這可能是由暴力密碼破解攻擊這個帳戶所造成。 如果您按一下此帳戶將會取得詳細的資訊可協助您 toodetermine hello 目標資源的潛在攻擊：

![搜尋結果](./media/oms-security-getting-started/oms-getting-started-fig8.JPG)

hello 詳細資料報表提供關於這個事件中，重要的資訊包括： hello 目標電腦、 hello 類型 （在此案例的網路登入） 的登入]、 [hello 活動 （在此案例事件 4625） 以及每次嘗試的完整時間軸。 

### <a name="computers"></a>電腦
這張牌可以是使用的 tooaccess 主動具有安全性事件的所有電腦。 當您按一下此磚中您會看到每一部電腦上的 hello 與安全性事件和事件的 hello 數目的電腦清單：

![電腦](./media/oms-security-getting-started/oms-getting-started-fig9.JPG)

您可以在每一部電腦上，即可繼續調查程式，並檢閱已加上旗標的 hello 安全性事件。

### <a name="threat-intelligence"></a>威脅情報

藉由使用 hello 威脅情報選項可以在 OMS 安全性和稽核，IT 系統管理員可以識別針對 hello 環境的安全性威脅，例如，必須識別特定的電腦是否殭屍網路的一部分。 當攻擊者非法地安裝惡意軟體偷偷地連接此電腦 toohello 命令和控制項時，電腦可能會變成殭屍網路中的節點。 它也可以識別來自地下通訊通道 (例如暗網) 的潛在威脅。 深入了解威脅情報閱讀[Operations Management Suite 安全性和稽核解決方案中的監視和回應 toosecurity 警示](oms-security-responding-alerts.md)發行項。

在某些情況下，您可能會發現已從一部受監視的電腦存取潛在惡意 IP：

![威脅情報對應](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig6.png)

此警示和其他人在 hello 相同類別目錄，利用透過 OMS 安全性會產生[Microsoft 威脅情報](https://youtu.be/O4WtxgUrDc8)。 hello 威脅情報資料是 Microsoft 所收集，以及主要威脅情報提供者購買。 這項資料會經常更新，並調整 toofast 移動的威脅。 Tooits 本質，因為它應與結合其他來源的安全性資訊時[調查](https://blogs.technet.microsoft.com/msoms/2016/12/08/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/)安全性警示。 

### <a name="baseline-assessment"></a>基準評估

Microsoft 與全球產業和政府組織共同定義可代表高度安全伺服器部署的 Windows 組態。 此組態是一組登錄機碼、稽核原則設定和安全性原則設定，以及 Microsoft 對於這些設定的建議值。 這組規則也稱為安全性基準。 如需此選項的詳細資訊，請參閱 [Operations Management Suite 安全性和稽核解決方案中的基準評估](oms-security-baseline.md)。

### <a name="azure-security-center"></a>Azure 資訊安全中心
此磚基本上是快顯 tooaccess Azure 資訊安全中心儀表板。 如需此解決方案的詳細資訊，請閱讀 [開始使用 Azure 資訊安全中心](../security-center/security-center-get-started.md) 。

## <a name="notable-issues"></a>值得注意的問題
此群組的選項 hello 主要目的是 tooprovide 您尚未在環境中，分類，以進行重大、 警告及資訊中的 hello 問題的快速檢視。 hello 作用中的問題類型的磚是視覺效果的這些問題，但它並不允許的 tooexplore 更多詳細資料，您必須具有 hello 名稱多少物件有此項動作 （計數） 的 hello 問題 （名稱），此磚的 toouse hello 下半部，重要性是 （嚴重性）。

![值得注意的問題](./media/oms-security-getting-started/oms-getting-started-fig10.JPG)

您可以看到這些問題已已經涵蓋 hello 的不同領域中**安全性網域**群組，這可加強 hello 意圖，此檢視： 以視覺化方式檢視您的環境，從單一位置中的 hello 最重要問題。

## <a name="detections-preview"></a>偵測 (預覽)
hello 這個選項的主要目的是 tooallow IT tooquickly 識別潛在威脅 tootheir 環境中的透過和 hello 的這項威脅的嚴重性。

![威脅情報](./media/oms-security-getting-started/oms-getting-started-fig12.png)

此選項也可用在[事件回應調查](https://blogs.msdn.microsoft.com/azuresecurity/2016/11/30/investigating-suspicious-activity-in-a-hybrid-cloud-with-oms-security/)tooperform hello 評估，並取得更多有關 hello 攻擊。

> [!NOTE]
> 如需有關如何 toouse 事件回應 OMS 觀看這段影片： [tooLeverage 如何 hello Azure 資訊安全中心 & Microsoft Operations Management Suite 事件回應](https://channel9.msdn.com/Blogs/Taste-of-Premier/ToP1703)。
> 
> 

## <a name="threat-intelligence"></a>威脅情報
hello 新威脅智慧一節的 hello 安全性和稽核 」 解決方案會視覺化 hello 可能的攻擊模式幾種： hello 的具有惡意連出 IP 流量的伺服器總數、 hello 惡意之威脅類型及顯示在哪裡對應這些 Ip來自。 您可以互動 hello 對應，然後按一下 hello Ip 如需詳細資訊。

黃色圖釘 hello 地圖上的指出惡意 Ip 的連入流量。 是很常見的伺服器公開 toohello 網際網路 toosee 連入惡意流量，但我們建議您檢閱這些嘗試 toomake 確定沒有任何已順利完成。 這些指標是以 IIS 記錄、WireData 和 Windows 防火牆記錄為基礎。  

![威脅情報](./media/oms-security-getting-started/oms-getting-started-fig11-ga.png)

## <a name="common-security-queries"></a>常見安全性查詢
可用的常見安全性查詢 hello 清單可以用於您 toorapidly 存取資源的資訊，並根據您的環境需求加以自訂。 這些常用查詢如下︰

* 所有安全性活動
* Hello 電腦"computer01.contoso.com"（取代為您自己的電腦名稱） 的安全性活動
* Hello 電腦"computer01.contoso.com"帳戶"Administrator"（以您自己的電腦和帳戶名稱取代） 的安全性活動
* 依電腦的登入活動
* 在任何電腦上終止 Microsoft 反惡意程式碼的帳戶
* Hello Microsoft 反惡意程式碼處理序已終止的電腦
* 已執行 "hash.exe" 的電腦 (以不同的處理序名稱取代)
* 已執行的所有處理序名稱
* 依帳戶的登入活動
* 從遠端登入帳戶 hello 電腦"computer01.contoso.com"（以您自己的電腦名稱取代）

## <a name="see-also"></a>另請參閱
在本文件中，您所導入了的 tooOMS 安全性和稽核 」 解決方案。 toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:

* [Operations Management Suite (OMS) 概觀](operations-management-suite-overview.md)
* [監視及回應 tooSecurity 警示在 Operations Management Suite 安全性和稽核解決方案](oms-security-responding-alerts.md)
* [在 Operations Management Suite 安全性和稽核解決方案內監視資源](oms-security-monitoring-resources.md)

