---
title: "在 Azure 中的工作負載 IaaS aaaSecurity 最佳作法 |Microsoft 文件"
description: " hello 移轉的工作負載 tooAzure IaaS 帶來的商機 tooreevaluate 設計 "
services: security
documentationcenter: na
author: barclayn
manager: MBaldwin
editor: TomSh
ms.assetid: 02c5b7d2-a77f-4e7f-9a1e-40247c57e7e2
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/29/2017
ms.author: barclayn
ms.openlocfilehash: 9cee1ca6effe9561e51dc8b945e7388ffea169b6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="security-best-practices-for-iaas-workloads-in-azure"></a>Azure 中 IaaS 工作負載的安全性最佳作法

當您啟動思考移動工作負載 tooAzure 基礎結構即服務 (IaaS) 時，您可能實現的一些考量是很熟悉。 您可能已經體驗虛擬環境保護。 當您移動 tooAzure IaaS 時，您可以套用您在保護虛擬環境的專業知識，並使用一組新的選項 toohelp 安全資產。

讓我們開始所說，我們不應預期 toobring 內部部署資源為一對一 tooAzure。 hello 新的挑戰和 hello 新選項將有機會 tooreevaluate 現有 deigns、 工具，並處理。

您負責安全性為基礎的雲端服務的 hello 型別。 hello 圖將摘要列出 Microsoft 和您的責任 hello 之間取得的平衡：


![責任範圍](./media/azure-security-iaas/sec-cloudstack-new.png)


我們將討論一些可協助您符合組織的安全性需求的 Azure 中可用的 hello 選項。 請記住，不同類型的工作負載會有不同的安全性需求。 任何其中一個最佳作法均無法獨自保護您的系統。 像任何其他項目安全性，您會有 toochoose hello 適當選項，並查看如何 hello 解決方案可以彼此互補的填滿間距。

## <a name="use-privileged-access-workstations"></a>使用特殊權限存取工作站

組織通常落眾 toocyberattacks 因為系統管理員執行動作時使用較高權限的帳戶。 這通常不是惡意行為，而是因為現有的組態和程序允許這麼做。 大部分的這些使用者了解從概念觀點來看這些動作的 hello 風險，但仍然選擇 toodo 它們。

執行一些作業，例如檢查電子郵件和瀏覽網際網路 hello 看起來不夠無害。 但是它們可能會公開提升權限的帳戶 toocompromise 由惡意使用者可以使用瀏覽活動、 特製的電子郵件或其他技術 toogain 存取 tooyour 企業動作項目。 我們強烈建議您將使用的安全管理工作站 hello 執行所有的 Azure 系統管理工作，以降低暴露 tooaccidental 洩露。

特殊權限存取工作站 (PAW) 提供敏感性工作的專用作業系統，此系統可免於遭受網際網路攻擊和威脅載體攻擊。 區隔這些機密工作並從帳戶 hello 每日使用工作站和裝置提供強式保護網路釣魚攻擊，應用程式和作業系統安全性弱點、 各種模擬攻擊和認證遭竊攻擊，例如按鍵記錄、 傳遞的雜湊，與傳遞票證。

hello PAW 方法是 hello 完善的擴充功能和建議做法 toouse 不同於標準使用者帳戶的個別指派系統管理帳戶。 PAW 會為這些敏感性帳戶提供可靠的工作站。

如需詳細資訊和實作指引，請參閱[特殊權限存取工作站](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/privileged-access-workstations)。

## <a name="use-multi-factor-authentication"></a>使用 Multi-Factor Authentication

在過去的 hello，網路周邊會是使用的 toocontrol 存取 toocorporate 資料。 在雲端優先 （contract-first）、 行動裝置前的世界中，身分識別是 hello 控制平面： toocontrol 存取 tooIaaS 服務從任何裝置使用。 您也使用它 tooget 可見性和深入了解使用您的資料位置和方式。 保護 hello Azure 使用者的數位身分識別就是保護您的訂用帳戶，從身分識別盜用和其他 cybercrimes 的 hello 基石。

其中一個 hello 最有幫助，您可以採取的步驟 toosecure 帳戶是 tooenable 雙因素驗證。 雙因素驗證是一種驗證加法 tooa 密碼中使用的項目。 有助於降低 hello 風險管理 tooget 的人存取的其他人的密碼。

[Azure Multi-factor Authentication](../multi-factor-authentication/multi-factor-authentication.md)協助保護存取 toodata 和應用程式同時滿足簡單登入程序的使用者需求。 它可以透過一些簡單的驗證選項 (例如電話、文字訊息，或行動應用程式驗證) 來提供強大的驗證功能。 使用者選擇其偏好的 hello 方法。

最簡單方式 toouse hello Multi-factor Authentication 是 hello Microsoft Authenticator 行動應用程式可以在執行 Windows、 iOS 和 Android 的行動裝置上使用。 Hello 最新版本的 Windows 10 和 hello 整合內部部署 Active directory 與 Azure Active Directory (Azure AD)、 [Windows Hello 企業](../active-directory/active-directory-azureadjoin-passport-deployment.md)可用來無縫式單一登入 tooAzure 資源。 在此情況下，hello Windows 10 裝置作為 hello 第二個因素驗證。

管理您的 Azure 訂用帳戶的帳戶以及可以登入 toovirtual 機器的帳戶，使用多因素驗證可讓您更高一層的安全性比使用的密碼。 其他形式的雙因素驗證或許也有用，但如果這些形式還沒有在生產環境中，其部署可能會很複雜。

hello 下列螢幕擷取畫面顯示部份 hello Azure Multi-factor authentication 可用的選項：

![Multi-Factor Authentication 選項](./media/azure-security-iaas/mfa-options.png)

## <a name="limit-and-constrain-administrative-access"></a>限制系統管理存取權

保護可以管理您的 Azure 訂用帳戶的 hello 帳戶是極為重要。 這些帳戶其中任一 hello 洩露值變成負值 hello 所有 hello tooensure hello 機密性和完整性，您的資料可能需要其他步驟。 為最近所 hello [Edward Snowden](https://en.wikipedia.org/wiki/Edward_Snowden)遺漏的分類資訊時，內部的攻擊會造成很大的威脅 toohello 任何組織的整體安全性。

下列準則的類似 toothese 來評估系統管理權限的人員：

- 是否正在執行需要系統管理權限的工作？
- Hello 工作的執行頻率為何？
- 是否有特定原因為何 hello 工作無法執行其他系統管理員代表它們？

其他所有已知的替代方法 toogranting hello 權限，以及每個為什麼不接受的文件。

在 just-in-time 管理 hello 使用可以防止 hello 不必要的存在較高權限的帳戶不需要這些權限時期間。 帳戶在有限的時間內具有提高的權限，可讓系統管理員執行其作業。 然後，這些權限會移除結尾 hello 的排班或工作完成。

您可以使用[Privileged Identity Management](../active-directory/active-directory-privileged-identity-management-configure.md) toomanage、 監視器和控制存取您組織中。 它可協助您保持警覺，注意 hello 所採取之動作的個人您組織中。 它也會在 just-in-time 管理 tooAzure AD 帶藉由引進 hello 概念合格的系統管理員。 這些是使用者已與 hello 潛在 toobe 帳戶授與系統管理員權限的人員。 這些類型的使用者可以完成啟動程序，並且在有限的時間內被授與系統管理員權限。


## <a name="use-devtest-labs"></a>使用 DevTest Labs

實驗室和開發環境中使用 Azure 啟用採取離開 hello 延遲，將會介紹硬體採購組織 toogain 靈活度中測試和開發。 不幸的是，熟悉 Azure 或 desire toohelp 缺乏加速其採用與權限指派 可能會導致 hello 管理員 toobe 過度寬鬆。 這項風險，可能會不小心公開 hello 組織 toointernal 攻擊。 有些使用者可能會被授與超出其應該擁有的存取權。

hello [Azure DevTest Labs](../devtest-lab/devtest-lab-overview.md)服務使用[所有存取控制](../active-directory/role-based-access-control-what-is.md)(RBAC)。 藉由使用 RBAC，您可以為授與僅 hello 存取層級所需的使用者 toodo 工作的角色責任隔離您的小組內。 RBAC 隨附預先定義的角色 (擁有者、實驗室使用者和參與者)。 您可以甚至可以使用這些角色 tooassign 權限 tooexternal 協力廠商及共同作業，大幅簡化。

DevTest Labs 使用 RBAC，因為它是額外，可能 toocreate[自訂角色](../devtest-lab/devtest-lab-grant-user-permissions-to-specific-lab-policies.md)。 DevTest Labs 不僅簡化 hello 管理的權限，它可簡化的佈建的環境的 hello 程序。 它還能協助您處理小組在開發與測試環境上所面臨的其他典型挑戰。 它需要一些準備工作，但在 hello 長期來看，它會使項目更容易為您的小組。

Azure DevTest Labs 的功能包括︰

- Hello 選項可用 toousers 的系統管理控制權。 hello 系統管理員可以集中管理允許的 VM 大小、 最大數目的 Vm 和 Vm 啟動和關機。
- 自動建立實驗室環境。
- 成本追蹤。
- 針對暫時性共同工作簡化 VM 的散發。
- 自助服務，可讓使用者 tooprovision 其實驗室使用的範本。
- 管理和限制取用。

![使用 DevTest Labs toocreate 實驗室](./media/azure-security-iaas/devtestlabs.png)

任何額外的成本不是相關聯的 DevTest Labs hello 使用量。 hello 建立實驗室、 原則、 範本和成品是免費的。 您需支付只 hello 實驗室，例如虛擬機器、 儲存體帳戶和虛擬網路中所使用的 Azure 資源。



## <a name="control-and-limit-endpoint-access"></a>控制和限制端點存取

裝載實驗室或在 Azure 中的實際執行系統表示您的系統需要 toobe 上可從 hello 網際網路存取。 根據預設，新的 Windows 虛擬機器已從 hello 網際網路存取的 hello RDP 連接埠，並在 Linux 虛擬機器已開啟的 hello SSH 連接埠。 採取的步驟 toolimit 公開端點是未經授權存取的必要 toominimize hello 風險。

在 Azure 中的技術可協助您限制 hello 存取 toothose 管理端點。 在 Azure 中，您可以使用[網路安全性群組](../virtual-network/virtual-networks-nsg.md) (NSG)。 當您使用 Azure Resource Manager 部署時，Nsg 會限制從所有網路 toojust hello 管理端點 （RDP 或 SSH） 的 hello 存取。 當您想到 NSG 時，您就會想到路由器 ACL。 您可以使用它們 tootightly 控制項 hello Azure 網路的各種區段之間的網路通訊。 這是在周邊網路或其他隔離的網路中的類似 toocreating 網路。 它們不會檢查 hello 流量，但它們執行協助使用網路分割。


在 Azure 中，您可以設定從內部部署網路進行的[網站間 VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)。 站對站 VPN 擴充內部網路 toohello 雲端。 這可提供您另一個有機會 toouse Nsg，因為您也可以修改 hello Nsg toonot 允許從任何地方以外 hello 區域網路的存取。 然後，您可以要求管理由第一個連接 toohello 透過 VPN 的 Azure 網路。

hello 站對站 VPN 選項可能會在您要在其中裝載緊密整合您的內部部署資源，在 Azure 中的實際執行系統的情況下最具吸引力。

或者，您可以使用 hello[點對站台](../vpn-gateway/vpn-gateway-howto-point-to-site-rm-ps.md)選項，您想要讓 toomanage 系統，不需要存取 tooon 內部部署資源。 這些系統在自己的 Azure 虛擬網路中可能是孤立的。 系統管理員可以到 hello Azure VPN 裝載環境的系統管理工作站。

>[!NOTE]
>您可以使用任一 hello Nsg toonot 上的 Acl 允許存取 toomanagement 端點從 hello 網際網路的 VPN 選項 tooreconfigure hello。

另一個值得考慮的選項是[遠端桌面閘道](../multi-factor-authentication/multi-factor-authentication-get-started-server-rdg.md)部署。 您可以使用此部署 toosecurely tooRemote 桌上型電腦伺服器透過 HTTPS 連線，而套用更詳細控制 toothose 連線。

您會有的功能存取 tooinclude:

- 系統管理員選項 toolimit 連線 toorequests 從特定的系統。
- 智慧卡驗證或 Azure Multi-Factor Authentication。
- 控制哪些系統上其他人可以 toovia hello 閘道連接。
- 控制裝置與磁碟重新導向。

## <a name="use-a-key-management-solution"></a>使用金鑰管理解決方案

基本 tooprotecting hello 雲端中的資料安全的金鑰管理。 有了 [Azure 金鑰保存庫](../key-vault/key-vault-whatis.md)，您即可安全地儲存加密金鑰和小型密碼，例如硬體安全性模組 (HSM) 中的密碼。 為了加強保證，您可以在 HSM 中匯入或產生金鑰。

Microsoft 會在進行過 FIPS 140-2 Level 2 驗證的 HSM (硬體和韌體) 中處理您的金鑰。 透過 Azure 記錄來監視及稽核金鑰的使用：將記錄傳送到 Azure 中，或您的安全性資訊及事件管理 (SIEM) 系統，以進行其他分析及威脅偵測。

只要擁有 Azure 訂用帳戶，任何人都可以建立和使用金鑰保存庫。 雖然 Key Vault 有益於開發人員和安全性系統管理員，但組織中負責管理 Azure 服務的系統管理員也可以實作並加以管理。


## <a name="encrypt-virtual-disks-and-disk-storage"></a>將虛擬磁碟和磁碟儲存體加密

[Azure 磁碟加密](https://gallery.technet.microsoft.com/Azure-Disk-Encryption-for-a0018eb0)位址 hello 的資料遭竊或未經授權的存取藉由移動磁碟達成暴露威脅。 hello 磁碟可以附加的 tooanother 系統以略過其他安全性控制項。 磁碟加密使用[BitLocker](https://technet.microsoft.com/library/hh831713) Windows 和 Linux tooencrypt 作業系統和資料磁碟機中的資料採礦的 Crypt 中。 Azure 磁碟加密與金鑰保存庫 toocontrol 整合，並管理 hello 加密金鑰。 其可用於標準 VM 和具有進階儲存體的 VM。

如需詳細資訊，請參閱 [Windows 和 Linux IaaS VM 中的 Azure 磁碟加密](azure-security-disk-encryption.md)。

[Azure 儲存體服務加密](../storage/common/storage-service-encryption.md)可協助保護待用資料。 它會啟用在 hello 儲存體帳戶層級。 它會在資料寫入資料中心時進行加密，而資料會在您存取時自動解密。 它支援下列案例的 hello:

- 區塊 Blob、附加 Blob 和分頁 Blob 的加密
- 加密已封存的 Vhd 和範本從內部回到 tooAzure
- 使用您的 VHD 建立的 IaaS VM 基礎 OS 和資料磁碟的加密

繼續使用 Azure 儲存體加密前，請留意兩項限制︰

- 它不適用於傳統儲存體帳戶。
- 它只會加密在啟用加密功能之後寫入的資料。

## <a name="use-a-centralized-security-management-system"></a>使用集中式安全性管理系統

您的伺服器需要 toobe 監視修補、 設定、 事件和可能會被視為安全性考量的活動。 您可以使用那些顧慮的 tooaddress，[資訊安全中心](https://azure.microsoft.com/services/security-center/)和[Operations Management Suite 安全性與相容性](https://azure.microsoft.com/services/security-center/)。 這兩個選項超越 hello 作業系統中的 hello 組態。 它們也提供的基礎基礎結構，例如網路組態和虛擬應用裝置使用的 hello hello 組態的監視。

## <a name="manage-operating-systems"></a>管理作業系統

在 IaaS 部署中，您都仍然必須負責 hello 管理您部署時，就像任何其他伺服器或工作站，在您的環境中的 hello 系統。 修補、 強化，權限指派，以及任何其他活動相關 toohello 維護您的系統仍然您的責任。 針對與您在內部部署的資源會緊密整合的系統，您可能想 toouse hello 相同的工具和程序正在使用的內部部署的防毒軟體、 反惡意程式碼、 修補和備份等事項。

### <a name="harden-systems"></a>強化系統
在 Azure IaaS 中的所有虛擬機器應該強行都寫入，使它們公開所需 hello 所安裝的應用程式的服務端點。 對於 Windows 虛擬機器，請遵循 Microsoft 發行為基準的 hello 的 hello 建議[Security Compliance Manager](https://technet.microsoft.com/solutionaccelerators/cc835245.aspx)方案。

Security Compliance Manager 是免費的工具。 您可以使用它 tooquickly 設定及使用群組原則和 System Center Configuration Manager 中管理您的桌面、 傳統資料中心，以及私人和公用雲端。

Security Compliance Manager 可提供已準備好部署的原則和經過測試的 Desired Configuration Management 設定套件。 這些基準是以 [Microsoft 安全性指南](https://technet.microsoft.com/en-us/library/cc184906.aspx)的建議和業界最佳作法為基礎。 它們可協助您管理設定飄移 (Configuration Drift)、解決相容性需求及降低安全性威脅。

您可以使用兩種不同方式使用 Security Compliance Manager tooimport hello 目前組態的電腦。 第一種方法，您可以匯入以 Active Directory 為基礎的群組原則。 第二，您可以匯入 「 golden master"hello 設定參照電腦使用 hello [LocalGPO 工具](https://blogs.technet.microsoft.com/secguide/2016/01/21/lgpo-exe-local-group-policy-object-utility-v1-0/)tooback hello 本機群組原則。 您可以匯 hello 本機群組原則到 Security Compliance Manager。

比較標準 tooindustry 的最佳作法、 自訂它們，然後建立新的原則和 Desired Configuration Management 設定組件。 已針對所有支援的作業系統 (包括 Windows 10 年度更新版和 Windows Server 2016) 發佈基準。


### <a name="install-and-manage-antimalware"></a>安裝和管理反惡意程式碼

分別從您的生產環境裝載環境中，您可以使用反惡意程式碼擴充 toohelp 保護您的虛擬機器和雲端服務。 該擴充功能會與 [Azure 資訊安全中心](../security-center/security-center-intro.md)整合。


[Microsoft Antimalware](azure-security-antimalware.md) 包含下列功能：即時防護、排程掃描、惡意程式碼補救、簽章更新、引擎更新、範例報告、排除事件收集和 [PowerShell 支援](https://msdn.microsoft.com/library/dn771715.aspx)。

![Azure Antimalware](./media/azure-security-iaas/azantimalware.png)

### <a name="install-hello-latest-security-updates"></a>安裝最新安全性更新 hello
有些客戶移動 tooAzure hello 第一個工作負載是實驗室和外部對向的系統。 如果您 Azure 託管的虛擬機器裝載應用程式或需要 toobe 存取 toohello 網際網路的服務，是警戒修補。 修補 hello 作業系統之外。 未修補的弱點的第三方應用程式也可能會導致 tooproblems 可以避免如果位於良好的修補程式管理。

### <a name="deploy-and-test-a-backup-solution"></a>部署和測試備份解決方案

就像安全性更新、 備份需要 toobe 處理 hello 您處理其他任何作業的方式相同。 這是屬於實際執行環境擴充 toohello 雲端系統的則為 true。 Test 和 dev 系統必須遵循提供的類似 toowhat 使用者還原功能已經成長習慣，根據他們的經驗與內部部署環境的備份策略。

生產工作負載移 tooAzure 應該整合與現有的備份解決方案時可能。 或者，您可以使用[Azure Backup](../backup/backup-azure-arm-vms.md) toohelp 解決您的備份需求。


## <a name="monitor"></a>監視

[資訊安全中心](../security-center/security-center-intro.md)提供持續進行評估 hello 安全性狀態，您的 Azure 資源的 tooidentify 潛在的安全性漏洞。 建議清單會引導您完成設定所需的控制項的 hello 程序。

範例包括：

- 佈建反惡意程式碼 toohelp 識別並移除惡意軟體。
- 設定網路安全性群組與規則 toocontrol 流量 toovirtual 機器。
- 佈建 web 應用程式防火牆 toohelp 防禦攻擊您的 web 應用程式為目標。
- 部署遺漏的系統更新。
- 定址 OS 組態不符合 hello 建議基準。

hello 下圖顯示一些您可以啟用資訊安全中心的 hello 選項。

![Azure 資訊安全中心原則](./media/azure-security-iaas/security-center-policies.png)

[Operations Management Suite](../operations-management-suite/operations-management-suite-overview.md) 是 Microsoft 雲端型 IT 管理解決方案，可協助您管理及保護內部部署和雲端基礎結構。 因為 Operations Management Suite 是以雲端型服務形式實作，所以您對基礎結構資源進行最小的投資就可以快速部署它。

新功能會自動提供，以節省持續性維護和升級成本。 Operations Management Suite 也會與 System Center Operations Manager 整合。 它有您加強管理您的 Azure 工作負載，包括不同元件 toohelp[安全性與相容性](../operations-management-suite/oms-security-getting-started.md)模組。

您可以使用 Operations Management Suite tooview 資訊中的 hello 安全性與相容性功能資源的相關。 hello 資訊會組織成四個主要類別：

- **安全性網域**︰進一步探索一段時間的安全性記錄。 存取惡意程式碼評估、更新評估、網路安全性、身分識別和存取資訊，以及具有安全性事件的電腦。 利用快速存取 toohello Azure 資訊安全中心儀表板。
- **值得注意的問題**： 快速識別作用中問題的 hello 數目及 hello 這些問題的嚴重性。
- **偵測 (預覽)**︰立即將資源的安全性警示視覺化，進而識別攻擊模式。
- **威脅情報**： 識別攻擊模式所視覺化的具有惡意連出 IP 流量，伺服器 hello 總數 hello 惡意之威脅類型，並顯示來自這些 Ip 其中的對應。
- **常見安全性查詢**： 看到一份 hello 最常見安全性查詢，您可以使用 toomonitor 您的環境。 當您按一下這些查詢的其中一個時，hello**搜尋**刀鋒視窗隨即開啟並顯示 hello 該查詢的結果。

hello 下列螢幕擷取畫面顯示 Operations Management Suite 的資訊可以顯示 hello 資訊的範例。

![Operations Management Suite 安全性基準](./media/azure-security-iaas/oms-security-baseline.png)



## <a name="next-steps"></a>後續步驟


* [Azure 安全性小組部落格](https://blogs.msdn.microsoft.com/azuresecurity/)
* [Microsoft 安全性回應中心](https://technet.microsoft.com/library/dn440717.aspx)
* [Azure 安全性最佳作法與模式](security-best-practices-and-patterns.md)
