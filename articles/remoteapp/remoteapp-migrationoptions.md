---
title: "移轉超出 Azure RemoteApp aaaOptions |Microsoft 文件"
description: "深入了解 Azure RemoteApp 超出移轉 hello 選項。"
services: remoteapp
documentationcenter: 
author: ericorman
manager: mbaldwin
ms.assetid: c4e0e5bc-5c13-4487-b1b6-ebf2a5edc1f0
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: 75324597881520d0c75939983b728ae9bbd7f436
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="options-for-migrating-out-of-azure-remoteapp"></a>移出 Azure RemoteApp 的選項
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。


如果您已停止使用 Azure RemoteApp，因為 hello[淘汰公告](https://go.microsoft.com/fwlink/?linkid=821148)或因為您已完成評估版，您需要 toomigrate 移出 Azure RemoteApp tooanother 應用程式服務。 移轉有兩種不同的方法︰自我管理 (通常稱為基礎結構即服務 [IaaS]) 部署，或完全受管理 (通常稱為平台即服務或軟體即服務 [PaaS/SaaS]) 供應項目。 

自助服務的 IaaS 是由您管理、操作及擁有的自己動手部署，可直接部署在虛擬機器 (VM) 或實體系統上。 在其他 hello 結束，完全受管理的 PaaS/SaaS 供應項目多個要 Azure RemoteApp-夥伴提供服務之上的層級處理操作在遠端處理解決方案以及服務時，hello 客戶執行一些映像和應用程式管理。

[移轉選項上檢視 hello Azure RemoteApp 網路研討會](https://social.msdn.microsoft.com/Forums/azure/40557aaa-3e9f-403c-b221-ad3eac10dc56/migration-option-webinar-recordings?forum=AzureRemoteApp)，或閱讀並了解詳細資訊 （包括 hello 不同裝載選項的範例）。

## <a name="self-managed-iaas-solutions"></a>自我管理的 (IaaS) 解決方案
### <a name="rds-on-iaas"></a>**IaaS 上的 RDS**
您可以使用 RemoteApp 或內部部署桌上型電腦或在託管環境 (如 Azure Vm 上) 中，部署以工作階段為基礎的原生遠端桌面服務 (在 Windows Server 中) 部署。 IaaS 部署上的 RDS 最適合於已經熟悉 RDS 部署且具備其現有技術專業知識的客戶。 

> [!NOTE]
> 您需要大量授權的軟體保證 (SA) 的 RDS 用戶端存取授權 toouse 此部署選項。

在 Azure VM 上部署 RDS 比以往您使用部署和修補範本時還要容易 (請讀取[概觀](https://blogs.technet.microsoft.com/enterprisemobility/2015/07/13/azure-resource-manager-template-for-rds-deployment/)，然後 [加以取得](https://aka.ms/rdautomation))。 您可以取得 hello 相同彈性調整能力與 Azure RemoteApp 中的 Azure 傳統部署模型資源 （不是 Azure 資源模型資源） 使用 hello[自動調整指令碼](https://gallery.technet.microsoft.com/scriptcenter/Automatic-Scaling-of-9b4f5e76)，不過，當有多個自訂與設定。 當您部署 Azure Vm 上的 RDS 時，透過提供支援[Azure 支援](https://azure.microsoft.com/support/plans/)，hello 相同的技術支援工程師支援您的 Azure RemoteApp。 您可以取得成本連絡來根據現有的使用量估算[Azure 支援](https://azure.microsoft.com/support/plans/)，您可以自行執行計算或使用 toobe 立即釋放成本計算機。  此外，N 系列 Vm （目前在私人預覽中） 您可以新增 vGPU-太多有關加入 vGPU 支援，以及有關如何聽到[駕馭 RDS 改善 Windows Server 2016 中的](https://myignite.microsoft.com/videos/2794)我們 Ignite 工作階段中。   

我們有逐步部署指南[Windows Server 2012 R2](http://aka.ms/rdsonazure)和[Windows Server 2016](http://aka.ms/rdsonazure2016) tooassist 與您的部署。 簽出 hello[遠端桌面部落格](https://blogs.technet.microsoft.com/enterprisemobility/?product=windows-server-remote-desktop-services)如 hello 最新消息。

### <a name="citrix-on-iaas"></a>**IaaS 上的 Citrix**
以工作階段為基礎之 XenApp 或 XenDesktop 的原生 Citrix 部署，可以部署於內部部署或託管環境中 (例如在 Azure VM 上)。 

簽出 hello 逐步部署指南 》，[在 Azure 上的 Citrix XA 7.6](http://www.citrixandmicrosoft.com/Documents/Citrix-Azure Deployment Guide-v.1.0.docx)，如需詳細資訊。 深入了解 [Azure 上的 Citrix](http://www.citrixandmicrosoft.com/Solutions/AzureCloud.aspx)，包括價格計算機。 您也可以尋找[Citrix 連絡人](http://citrix.com/English/contact/index.asp)toodiscuss 您使用的選項。

## <a name="fully-managed-paassaas-offerings"></a>完全受管理的 (PaaS/SaaS) 供應項目

### <a name="citrix-xenapp-essentials-released-april-2017"></a>Citrix XenApp Essentials (2017 年 4 月發行)
現在可在 hello [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Citrix.XenAppEssentials)、 Citrix XenApp Essentials 為新應用程式虛擬化服務 hello，結合 hello 電源和彈性的 hello 與 hello 簡單，不夠，Citrix 雲端平台和輕鬆使用 Microsoft Azure RemoteApp 願景。 

現有 Azure RemoteApp 客戶可以 [註冊免費試用](https://www.citrix.com/products/citrix-cloud/form/xenapp-essentials-msft-trial/)。  注意：只有 Citrix 使用者服務費免費，仍須收取 Azure 計算和儲存體費用

深入了解：
- [從 Azure RemoteApp tooCitrix XenApp Essentials 移轉](remoteapp-migrate-citrix.md)
- [Citrix 和 Microsoft](https://www.citrix.com/global-partners/microsoft/remote-app.html) \(英文\)
- [Citrix XenApp Essentials 簡報](https://www.youtube.com/watch?v=91Z7CCfQ-9k) \(英文\)。  

### <a name="citrix-cloud-xenapp-service-and-xendesktop-service"></a>Citrix Cloud XenApp 服務和 XenDesktop 服務 

[Citrix 雲端 XenApp 服務和 XenDesktop 服務](https://www.citrix.com/products/citrix-cloud/services.html)是 hello hello 傳遞的同時應用程式和桌面，以及進階的管理和監視功能的最佳解決方案。 

#### <a name="conexlink-platform-name-mycloudit"></a>Conexlink (平台名稱︰MyCloudIT)
[MyCloudIT](https://mycloudit.com)是和 IT 公司 toosimplify，一個自動化平台最佳化及調整 hello 移轉遠端桌面、 遠端的應用程式和基礎結構中的傳送 hello Microsoft Azure 雲端。 

hello MyCloudIT 平台降低 95%，成本 30%的 Azure 部署時間，並將其用戶端的整個 IT 基礎結構移至 hello 雲端中的幾個按鍵。 夥伴可以立即管理客戶從一個通用的儀表板，hello 世界各地的服務使用者前所未有，成長而不會增加額外負荷或廣泛 Azure 訓練的營收。  

> 主要地點︰美國德州達拉斯
> 
> 營運區域︰全球
> 
> 合作夥伴狀態︰[金級](https://partnercenter.microsoft.com/pcv/solution-providers/conexlink_4298787366/843036_1?k=Conexlink)
> 
> Microsoft Cloud 服務提供者：是
> 
> 提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者
> 
> Azure RemoteApp 移轉解決方案︰是，[深入了解](https://mycloudit.com/remote-app-microsoft/)
> 
> Brian Garoutte, VP of Business Development
> 
> 電話：972-218-0741
>   
> 電子郵件：[brian.garoutte@conexlink.com](mailto:brian.garoutte@conexlink.com)

### <a name="frame"></a>Frame

IT 組織中企業和政府、 受管理的服務提供者和前置的軟體廠商選擇框架 toocreate 及管理其安全的軟體定義的工作區 hello 雲端中。 從小型 toolarge 組織畫面格，讓非常容易 toolet 使用者從任何裝置存取的任何瀏覽器上的 Windows 應用程式。 hello 框架平台包括的所有項目從 hello 雲端包括 hello Azure 基礎結構和 RDS 授權系統管理需求 toodeploy 應用程式 （攜帶您自己的 Azure 帳戶和授權是選擇性的）。 

深入了解 [Azure 上的 Frame](https://www.fra.me/ara)。 

> 主要位置︰美國加州的聖馬刁
>
> 營運區域︰全球
>
> Microsoft 合作夥伴：是
> 
> 電話：1-480-269-4668

### <a name="awingu"></a>Awingu
Awingu 提供執行傳統應用程式的簡易線上工作區解決方案、SaaS 和 html5 瀏覽器的文件。 這麼一來，即可在任何類型的裝置上安全地使用任何應用程式， 而 SaaS 服務也可使用多種單一登入選項。 此外，多樣化 (雲端) 檔案系統可深入整合至您的工作區。 下一步 toofull 行動力，Awingu 的豐富線上工作區，將會獲得最佳的安全性與細微的控制 （例如下載/上傳）、 多重要素驗證 (例如 Azure MFA)、 工作階段錄製和多個稽核的完整使用量。 現成的 Awingu 可讓您分享文件和應用程式工作階段，以達到最佳化和安全的工作作業。
Awingu 的解決方案是多租用戶、多 AD 和開放式 API。 小型和大型企業、雲端服務提供者和 [Isv](http://www.isv2saas.com) 使用此解決方案。 這些客戶特別喜歡 hello 容易使用，方便安裝與低 TCO。

Awingu All-in-one 合一是[hello Azure Marketplace 中可用](https://azuremarketplace.microsoft.com/marketplace/apps/awingu.awingu-arm)與 2 內建的並行使用者。 其他授權可透過 [廣大的經銷商和轉售商](http://www.awingu.com/reseller) 取得。

深入了解[Awingu 上的做為替代 tooAzure RemoteApp](http://alternative-for-azure-remoteapp.awingu.com/)。


> 主要地點︰比利時
> 
> 作業區域：EMEA、北美洲和巴西
> 
> 提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者 
> 
> 全域：
> 
> Arnaud Marlière，CMO
> 
> 電子郵件：[arnaud@awingu.com](mailto:arnaud@awingu.com)
> 
> 電話：+1 646 583 3025
> 
> **比利時總部**：
> 
> Ottergemsesteenweg-Zuid 808 B44
> 
> 9000 Gent
> 
> 電子郵件：[info@awingu.com](mailto:info@awingu.com) 
> 
> 電話：+32 9 296 40 11
> 
> 美國：
> 
> 第 7 floor、 1177 Ave 的 hello 美洲，
> 
> New York, NY 10036
> 
> 電子郵件：[info.us@awingu.com](mailto:info.us@awingu.com)

### <a name="microsoft-hosted-service-provider"></a>Microsoft 託管服務提供者
主控夥伴通常會提供完整的管理裝載的 Windows 桌面和應用程式服務，其中可能包含管理 hello Azure 資源、 作業系統、 應用程式，使用 hello 夥伴的技術服務人員的授權合約與 Microsoft 和正在服務提供者授權合約 tooallow 充任訂戶存取授權 (SAL) 以及其他軟體提供者。 hello 下列資訊提供詳細資料和部分特製化協助客戶使用他們的 Azure RemoteApp 移轉中的 hello 主控者的連絡資訊。 簽出[hello 目前裝載的服務提供者的清單](http://aka.ms/rdsonazurecertified)，已完成 hello RDS 學習路徑和評估 IaaS 上。  

### <a name="citrix-service-provider-program"></a>Citrix 服務提供者方案
hello Citrix 服務提供者程式輕鬆虛擬雲端運算 tooSMBs 中，提供他們希望方便且隨用隨付模型中的 hello 服務的服務提供者 toodeliver hello 簡易性。 Citrix 服務提供者增加其 Microsoft SPLA 企業和展開其 RDS 平台投資與任何裝置、 隨處存取、 hello 範圍最廣泛的應用程式支援、 豐富的體驗，提高的安全性和增強的延展性。 接著，Citrix 服務提供者可吸引更多訂閱者、提高客戶滿意度並降低其營運成本。 [深入了解](http://www.citrix.com/products/service-providers.html)或[尋找合作夥伴](https://www.citrix.com/buy/partnerlocator.html)。

#### <a name="acuutech"></a>Acuutech
[Acuutech](http://www.acuutech.com)專門用來提供託管桌面的解決方案，提供完整的桌面和 ISV 應用程式 Microsoft 技術 tooa 全域用戶端上建置基底他們自己的資料中心與 Azure 的體驗。

> 主要地點︰英國倫敦、新加坡、休士頓、德州
> 
> 營運區域︰全球
> 
> 合作夥伴狀態︰金級
> 
> Microsoft Cloud 服務提供者：是
> 
> 提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者
> 
> Azure RemoteApp 移轉解決方案︰是，[深入了解](http://www.acuutech.com/ara-migration/)
> 
> **英國**：
>   
> 5/6 York House, Langston Road,
>   
> Loughton, Essex IG10 3TQ
>   
> 電話：+44 (0) 20 8502 2155
> 
> **新加坡**：
>   
> 100 Cecil Street, #09-02, 
>   
> hello 地球，新加坡 069532
> 
> 電話：+65 6709 4933
>   
> **北美洲**：
>   
> 3601 S. Sandman St.
>   
> Suite 200, Houston, TX 77098
>   
> 電話：+1 713 691 0800

#### <a name="aspex"></a>ASPEX
[ASPEX](http://www.aspex.be/en)專門用來轉換 toohello 雲端和 ISV Isv ' 尋找 toooptimize 其目前的雲端設定。 ASPEX 會提供廣泛的受管理服務、開發和諮詢服務。  

> 主要地點︰比利時安特衛普
> 
> 營運區域︰西歐
> 
> 合作夥伴狀態︰[銀級](https://partnercenter.microsoft.com/pcv/solution-providers/aspex_9397f5dd-ebdd-405b-b926-19a5bda61f7a/cfe00bac-ea36-4591-a60b-ec001c4c3dff)
> 
> Microsoft Cloud 服務提供者：是
> 
> 提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者
> 
> Azure RemoteApp 移轉解決方案︰是，[深入了解](https://www.aspex.be/en/azure-remote-apps)
> 
> 電話︰+3232202198
> 
> 電子郵件︰[info@aspex.be](mailto:info@aspex.be)
> 
> Web：[http://cloud.aspex.be/contact-ara-0](http://cloud.aspex.be/contact-ara-0)

#### <a name="caasecom"></a>Caase.com
[Caase.com](http://www.caase.com/)可協助企業、 本機政府、 非政府主體以及與 hello Microsoft 雲端中的工作更聰明的方式向其旅程醫療保健機構。 無論身在何處或使用何種裝置，您都能在安全的環境下發揮生產力，而不需要支付昂貴的 IT 成本。 Caase.com 是真正專精於 Microsoft Office 365、Azure、Enterprise Mobility + Security 及 Windows 的專家。 透過我們的諮詢、移轉服務、採用計畫、訓練、管理和支援，Caase.com 能夠為客戶的員工、合作夥伴和供應商建立最佳化且安全的共同作業平台。
Caase.com 是 hello mastermind hello Azure 遠端工作區 （行動場所中） 和 hello 數位工作場所 （社交內部網路）。 這兩種解決方案 – 完成與採用 – 是 hello foundation 可確保這些解決方案的 hello 使用者在其路由 toohello Microsoft 雲端具有 hello 最愉快、 成功且有效的經驗。
荷蘭文翻譯和支援影片的位址為：http://caase.com/over-ons/

> 營運區域：以荷蘭為基礎，觸角擴及全球
> 
> 合作夥伴狀態︰[金級](https://partnercenter.microsoft.com/pcv/solution-providers/caasecom_4295593260/51159_3)
> 
> Microsoft Cloud 服務提供者：是
> 
> 提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者
> 
> Azure RemoteApp 移轉解決方案︰是。[深入了解](http://caase.com/diensten/microsoft-azure/) \(英文\)。
> 
> 
> 荷蘭：
> 
> Rigtersbleek-Zandvoort 10 (De Spinnerij)
> 
> 7521 BE, Enschede
> 
> 電話：+31 (0) 88 4320 000


#### <a name="nerdio"></a>Nerdio
[Azure Nerdio](http://getnerdio.com/nfa/)是傳遞 hello Microsoft 雲端為非常簡單的佈建、 管理和最佳化的 IT 環境中完成的 IT 自動化平台。 只需要幾小時，您就能建立虛擬桌面、遠端應用程式和伺服器。 管理 hello 環境中按三下或更少與 Nerdio 系統管理入口網站。 使用智慧型的自動調整並儲存在 Azure IaaS 資源 40 too60%。

> 主要位置：伊利諾伊州芝加哥，營運區域：全球，合作夥伴狀態：[金級](https://partnercenter.microsoft.com/en-us/pcv/solution-providers/adar-inc_341c9afa-f12c-46f5-8f7b-3f9ef59a66a5/3a7ae479-3ac2-42f6-84e2-d456dc7424e1)，Microsoft Cloud 服務提供者：是
> 
> 提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者
> 
> Azure RemoteApp 移轉解決方案：是
> 
> 
> 8001 Lincoln Ave
> 
> Suite 212
> 
> Skokie, IL 60077
> 
> USA
> 
> (844) 4NERDIO 分機6
> 
> [sayhello@getnerdio.com](mailto:sayhello@getnerdio.com)

#### <a name="saasplaza"></a>**SaaSplaza**
[SaaSplaza](http://www.saasplaza.com/) 提供完整的 Microsoft Dynamics 組合 (NAV、AX、GP、SL、CRM) 私人和公用雲端 (Azure)。

> 主要位置︰荷蘭
> 
> 營運區域︰全球
> 
> 合作夥伴狀態︰[金級](https://partnercenter.microsoft.com/pcv/solution-providers/saasplaza_4295495801/791011_2?k=saasplaza)
> 
> Microsoft Cloud 服務提供者：是
> 
> 提供以工作階段為基礎的 RemoteApp 和桌面解決方案︰是，兩者
> 
> **歐洲、中東與非洲**：
> 
> Prins Mauritslaan 29-35
> 
> 71 LP Badhoevedorp
> 
> hello 荷蘭
> 
> 電話：+31 20 547 8060 
> 
>  **美洲**：
> 
> 171 Saxony Road, Suite 105
> 
> Encinitas, CA 92024
> 
> San Diego
> 
> 美國
> 
> 電話：+1 858 385 8900 
> 
> **亞太地區**：
> 
> 105 Cecil Street
>    
> \#11-08 版 hello 八邊形
> 
> Singapore 069534
> 
> 新加坡
>   
> 電話 - 新加坡：+65 6222 6591
> 
> 電話 - 澳大利亞：+61 2 8310 5568 
>    
> 電話 - 紐西蘭：+64 4 488 0321
> 
## <a name="need-more-help"></a>需要其他協助？
仍然需要協助進行選擇，或有進一步的問題？ 使用下列方法 tooget 說明 hello 的其中一個。 

1. 請透過下列電子郵件地址連絡我們：[arainfo@microsoft.com](mailto:arainfo@microsoft.com)。
2. 連絡 [Azure 支援](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)。 從開啟 [Azure 支援案例](https://portal.azure.com/?#blade/Microsoft_Azure_Support/HelpAndSupportBlade)著手。
3. 致電給我們。 [尋找當地的銷售代表電話](https://azure.microsoft.com/overview/sales-number/)。

