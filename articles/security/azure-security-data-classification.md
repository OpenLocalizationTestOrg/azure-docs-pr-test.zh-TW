---
title: "分類適用於 Azure aaaData |Microsoft 文件"
description: "這篇文章提供簡介 toohello 資料分類的基本概念，並反白顯示它的值，特別是在雲端運算和使用 Microsoft Azure 的 hello 內容"
services: security
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: TomSh
ROBOTS: NOINDEX
redirect_url: https://aka.ms/data-classification-cloud
ms.assetid: 91d4afed-b80f-4a26-b526-b52b9c858cfb
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/18/2017
ms.author: yurid
ms.openlocfilehash: 726da2482beab3bf7b0ac33510f2b523d5074df8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="data-classification-for-azure"></a>Azure 的資料分類
這篇文章提供簡介 toohello 資料分類的基本概念，並反白顯示它的值，特別是在雲端運算和使用 Microsoft Azure 的 hello 內容。 

## <a name="data-classification-fundamentals"></a>資料分類的基本概念
組織若想成功進行資料分類，便需要廣泛認識自身的需求，並徹底了解資料資產的所在位置。  

資料有三種基本存在狀態︰ 

* 待用 
* 處理中 
* 傳輸中 

資料分類，所有三種狀態需要唯一的技術解決方案，但是 hello 套用的資料分類原則應該是 hello 相同每個。 歸類為機密的資料需要 toostay 機密在其餘部分，在程序，然後在傳輸過程中時。 

資料也可分為結構化或非結構化形式。 Hello 的一般分類程序化資料庫中找到的資料，並試算表會較不複雜且耗時 toomanage 以外的非結構化資料，例如文件、 程式碼中，與電子郵件。 

> [!TIP]
> 如需有關 Azure 功能與資料加密最佳作法的詳細資訊，請閱讀 [Azure 資料加密的最佳作法](azure-security-data-encryption-best-practices.md)
> 
> 

一般來說，組織的非結構化資料會多過結構化資料。 不論資料是結構化或非結構化，請務必您 toomanage 資料敏感度。 正確實作時，資料分類可協助確保資產受管理的資料資產視為公用或免費 toodistribute 比大於監督敏感或機密資料。 

### <a name="controlling-access-toodata"></a>控制存取 toodata
驗證和授權常被混淆，兩者角色也常被誤解。 在現實，都非常不同，hello 遵循圖所示。  

![資料存取和控制](./media/azure-security-data-classification/azure-security-data-classification-fig1.png)

### <a name="authentication"></a>驗證
驗證通常包括至少兩個部分： 使用者名稱或使用者識別碼 tooidentify 的使用者以及語彙基元，例如 tooconfirm hello username 認證的密碼無效。 hello 程序不會提供 hello 已驗證的使用者存取 tooany 項目或服務。它會驗證該 hello 使用者是屬實。   

> [!TIP]
> [Azure Active Directory](../active-directory/active-directory-whatis.md)提供雲端式身分識別服務，允許您 tooauthenticate 和授權使用者。 
> 
> 

### <a name="authorization"></a>Authorization
授權是 hello 程序會提供已驗證的使用者 hello 能力 tooaccess 應用程式、 資料集、 資料檔或其他物件。 指派已驗證的使用者 hello 權限 toouse、 修改或刪除他們可以存取的項目需要注意 toodata 分類。 

成功授權需要實作機制 toovalidate 個別使用者的 「 需要 tooaccess 檔案和資訊為基礎的角色、 安全性原則和風險原則考量。 例如，從特定的業務 (LOB) 應用程式的資料可能不需要存取的所有員工，toobe 和員工一小部分可能需要存取 toohuman 資源 (HR) 檔案。 但如組織 toocontrol 誰可以存取資料，以及時機與方法，以驗證使用者的有效的系統必須先準備就緒。 

> [!TIP]
> 在 Microsoft Azure 中，請確定 tooleverage 所有存取控制 (RBAC) toogrant 只有 hello 少量的存取權的使用者需要 tooperform 他們的工作。 讀取[使用角色指派 toomanage 存取 tooyour Azure Active Directory 資源](../active-directory/role-based-access-control-configure.md)如需詳細資訊。 
> 
> 

### <a name="roles-and-responsibilities-in-cloud-computing"></a>雲端運算中的角色和責任
雖然雲端提供者可以協助您管理風險、 客戶需要 tooensure 該資料分類管理和強制執行已正確地實作 tooprovide hello 資料管理服務的適當層級。  

責任而異的資料分類為基礎的雲端服務模型已經就定位，hello 遵循圖所示。 hello 三種主要雲端服務模型是基礎結構即服務 (IaaS)、 平台即服務 (PaaS) 」 和 「 軟體即服務 (SaaS)。 資料分類機制的實作也會跟著改變根據 hello 依賴和期望的 hello 雲端提供者。 

![角色](./media/azure-security-data-classification/azure-security-data-classification-fig2.png)

雖然您必須負責將您的資料分類，但雲端提供者應該要寫入有關如何在將安全及維護 hello 隱私權 hello 客戶資料儲存在其雲端內的承諾。  

* **IaaS 提供者**需求只限於 hello 虛擬環境的 tooensuring 可以容納資料分類功能，與客戶相容性需求。 IaaS 提供者在資料分類中具有較小的角色，因為它們只需要 tooensure 客戶資料位址法規遵循需求。 不過，提供者仍然必須確定其虛擬環境位址資料分類需求中加入 toosecuring 其資料中心。
* **PaaS 提供者**責任可能混用，因為 hello 平台無法使用中的分層的方式 tooprovide 安全性分類工具。 PaaS 提供者可能會負責驗證及可能有些授權規則，而且必須提供安全性和資料分類功能 tootheir 應用程式層。 更像是 IaaS 提供者，PaaS 的提供者會需要與任何相關的資料分類需求 tooensure 符合他們的平台。
* **SaaS 提供者**經常被視為鏈結的一部分授權，並將需要 tooensure hello hello SaaS 應用程式中儲存的資料，可以控制分類類型。 SaaS 應用程式可以使用 LOB 應用程式，及的本質是需要 tooprovide hello 表示 tooauthenticate 和授權所使用且儲存的資料。 

## <a name="classification-process"></a>分類程序
了解 hello 的許多組織必須提供資料分類，而且想 tooimplement 它面對的基本的挑戰是： 其中 toobegin 嗎？

一個有效且簡單的方式 tooimplement 資料分類為 toouse hello 計劃，請勿，核取、 ACT 模型從[MOF](https://technet.microsoft.com/solutionaccelerators/dd320379.aspx)。 hello 下列圖圖表需要的 toosuccessfully 實作資料分類，在此模型中的 hello 工作。  

1. **規劃**。 識別資料資產，資料保管者 toodeploy hello 分類程式，並開發保護設定檔中。 
2. **執行**。 資料分類原則都同意之後，部署 hello 程式，並實作所需的機密資料的強制技術。  
3. **檢查**。 請檢查並驗證有效定址 hello 工具和方法所使用的 tooensure hello 分類原則的報告。 
4. **行動**。 檢閱 hello 狀態的資料存取，並檢閱檔案和資料需要使用重新分類和修訂方法 tooadopt 變更 tooaddress 新風險的修訂。  

![規劃、執行、檢查、行動](./media/azure-security-data-classification/azure-security-data-classification-fig3.png)

### <a name="select-a-terminology-model-that-addresses-your-needs"></a>選取可滿足您需求的術語模型
來分類資料，包括手動程序，以位置為基礎的處理序的分類資料的使用者或系統的位置，特定資料庫的分類，例如應用程式為基礎的處理序和自動化有幾種類型的處理程序使用各種不同的技術，其中有些本文稍後的 hello 「 保護機密資料 」 一節所述的處理程序。  

本文介紹兩種已廣受業界好評與使用的模型為基礎的通用術語模型。 這些術語模型，這兩者會提供三種分類敏感度等級時，會顯示 hello 下表中。  

> [!NOTE]
> 當分類的檔案或資源結合通常會歸類在不同的層級，分類存在 hello 最高層級的資料應該建立 hello 整體的分類。 例如，包含敏感資料和受限制資料的檔案應該歸類為受限制。  
> 
> 

| **敏感性** | **術語模型 1** | **術語模型 2** |
| --- | --- | --- |
| 高 |機密 |受限制 |
| 中 |僅供內部使用 |敏感 |
| 低 |公開 |不受限制 |

#### <a name="confidential-restricted"></a>機密 (受限制)
歸類為機密或受限制的資訊包括可以是重大 tooone 或多個個人或組織如果洩漏或遺失的資料。 這類資訊經常 」 需要 tooknow 」 為基礎提供，而且可能包括： 

* 個人資料，包括個人識別資訊，例如社會安全號碼或身分證號碼、護照號碼、信用卡號碼、駕照號碼、醫療記錄和健保識別碼。  
* 金融記錄，包括金融帳戶號碼，例如支票或投資帳戶號碼。 
* 商務資料，例如屬於獨特或特定智慧財產的文件或資料。  
* 法律資料，包括可能的律師特權資料。 
* 驗證資料，包括私人的密碼編譯金鑰、使用者名稱密碼組，或其他識別數列，例如私人生物特徵金鑰檔。 

歸類為機密的資料通常具有資料處理方面的規章和法規遵循需求。 

#### <a name="for-internal-use-only-sensitive"></a>僅供內部使用 (敏感)
歸類為中度敏感性的資訊，其所包含的檔案和資料如果遺失或毀損，並不會對個人及/或組織造成嚴重影響。 這類資訊可能包含︰ 

* 電子郵件，其中大部分可以刪除或分散式而不會造成危機 （不包括從個人 hello 機密分類中所識別的信箱或電子郵件）。  
* 不包含機密資料的文件和檔案。

一般而言，這個分類包含任何不屬於機密的項目。 這個分類可能包含大部分的商務資料，因為大部分受到管理或者會在日常使用的檔案均可歸類為敏感。 Hello 例外狀況為公開金鑰或機密資料的資料，與商務組織內的所有資料都能夠都分類為機密預設。 

#### <a name="public-unrestricted"></a>公開 (不受限制)
會被分類為公用的資訊包括資料和檔案不是重大 toobusiness 需求或作業。 此分類也可以包含刻意已發行的 toohello 公用供其使用，例如行銷資料或按下宣告的資料。 此外，這個分類可能包含電子郵件服務中所儲存的垃圾郵件訊息之類的資料。 

### <a name="define-data-ownership"></a>定義資料擁有權
它是重要 tooestablish custodial 清除所有的資料資產的擁有權鏈結。 hello 下表識別不同的資料擁有權的角色中的資料分類工作和其各自的權限。  

| **角色** | **建立** | **修改/刪除** | **委派** | **讀取** | **封存/還原** |
| --- | --- | --- | --- | --- | --- |
| 擁有者 |X |X |X |X |X |
| 保管者 | | |X | | |
| 系統管理員 | | | | |X |
| 使用者\* | |X | |X | |

**保管者可能會授與使用者其他權限，例如編輯和刪除* 

> [!NOTE]
> 此資料表並未提供完整的角色和權限清單，而是只提供了具有代表性的範例。 
> 
> 

hello**資料資產擁有者**是原始 hello hello 資料，可以委派擁有權，並指派保管者建立者。 建立檔案時，hello 擁有者應該可以 tooassign 分類，表示它們有責任 toounderstand 必須 toobe 歸類為機密的項目會根據其組織的原則。 除非資料資產擁有者負責擁有或建立機密 (受限制) 的資料類型，否則其所有資料都會自動歸類為僅供內部使用 (敏感)。 通常，hello 擁有者角色會變更之後 hello 資料的分類。 例如，hello 擁有者可能會建立分類資訊的資料庫，並放棄其權限 toohello 資料保管者。  

> [!NOTE]
> 資料資產擁有者通常會使用服務、 裝置和媒體，其中有些是個人和其中有些隸屬 toohello 組織的混合。 清楚的組織原則可協助確保裝置 (例如膝上型電腦和智慧型裝置) 的使用方式符合資料分類指導方針。  
> 
> 

hello**資料資產保管者**指派 hello 資產擁有者 （或其委派） toomanage hello 資產相應 tooagreements hello 資產擁有者或根據適用的原則需求。 理想情況下，可以在自動化系統中實作 hello 保管者角色。 資產保管者可確保必要的存取控制所提供，而且會負責管理和保護資產委派 tootheir 小心。 hello 責任 hello 資產保管者可能包括：  

* 保護 hello 資產根據 hello 資產擁有者的方向，或一 hello 資產擁有者 
* 確保符合分類原則 
* 通知的任何資產擁有者變更 tooagreed-時控制項及/或保護程序之前 toothose 變更生效 
* 報告 toohello 資產擁有者，關於變更 tooor 移除 hello 資產保管者的責任 
* **系統管理員**是指負責確保完整性受到維護的使用者，但他們不是資料資產的擁有者、保管者或使用者。 事實上，許多系統管理員角色會提供資料容器管理服務，而不需要存取 toohello 資料。 hello 系統管理員角色包含的 hello 資料，維護 hello 資產的記錄備份和還原，並選擇、 取得和操作 hello 裝置和儲存體的房屋 hello 資產。 
* hello 資產使用者 」 包括會授與存取 toodata 或檔案的人。 存取指派通常是由 hello 擁有者 toohello 資產保管委派。  

### <a name="implementation"></a>實作
管理考量適用於 tooall 分類方法。 這些考量需要對象、 tooinclude 詳細內容，其中時機及原因資料資產會是使用、 存取、 變更或刪除。 了解如何組織檢視其風險，必須完成所有的資產管理，但可套用簡單的方法，hello 資料分類程序中所定義。 資料分類的其他考量包括 hello 導入新的應用程式和工具，以及管理分類方法實作之後的變更。  

### <a name="reclassification"></a>重新分類
Toobe 完成時的使用者或系統決定該 hello 資料資產的重要性或風險設定檔的變更需要重新歸類或變更的資料資產的 hello 分類狀態。 這項工作是確保 hello 分類狀態持續 toobe 目前的重要且有效。 未以手動方式分類的大部分內容皆可自動分類，或根據資料保管者或資料擁有者的使用方式來加以分類。 

### <a name="manual-data-reclassification"></a>以手動方式重新分類資料
在理想情況下，這項工作會確保可擷取變更 hello 詳細資料，及稽核。 hello 手動重新分類的最可能的原因是基於敏感度，或保留在文件格式，或是原本誤分類需求 tooreview 資料中的記錄。 因為這份文件會考慮資料分類和移動資料 toohello 雲端，手動重新分類工作需要注意，根據案例為基礎，並風險管理檢閱是理想的 tooaddress 分類需求。 一般而言，這類投入時間會考慮 hello 組織的原則必須 toobe 分類的項目、 hello 預設分類的狀態 （所有資料和機密，但沒有機密檔案），和 take 例外狀況的高風險的資料。 

### <a name="automatic-data-reclassification"></a>自動重新分類資料
自動資料重新分類會手動分類為使用相同的一般規則的 hello。 hello 例外狀況是規則會遵循與套用視需要可以確保自動化的解決方案。 資料分類可作為資料分類強制執行原則的一部分來進行，而這項原則的強制執行時機為使用授權技術儲存、使用和傳輸資料時。

* 應用程式型。 使用某些應用程式時，依預設會設定分類等級。 例如，來自客戶關係管理 (CRM) 軟體、HR 和健康記錄管理工具的資料預設是機密資料。 
* 位置型。 資料位置可協助您識別資料敏感性。 例如，HR 或財務部門所儲存的資料是更 toobe 機密的本質。  

### <a name="data-retention-recovery-and-disposal"></a>資料保留、復原和處置
資料復原和處置 (例如資料重新分類) 是管理資料資產時的重要層面。 hello 原則進行資料復原和處置資料保留原則會定義並強制執行 hello 相同的資料重新分類; 的方式這類努力 hello 保管者及系統管理員角色，做為共同作業的工作所執行。  

失敗 toohave 資料保留原則，可能表示資料遺失或故障 toocomply 法令和法律探索需求。 大部分的組織不需要明確定義的資料保留原則通常 toouse 預設 [保留所有項目] 保留原則。 不過在雲端服務案例中，這類保留原則會有額外的風險。 

例如，雲端服務提供者的資料保留原則可視為與 「 hello 訂用帳戶的 hello 持續時間 」 （只要 hello 服務付費的 hello 資料會保留）。 這種付款即保留的協議可能無法應付企業或法規的保留原則。 為機密資料定義原則可確保資料會根據最佳作法來進行儲存和移除。 此外，保存的原則可由了解有關哪些資料應該處置的 tooformalize 和時機。 

資料保留原則應該可滿足所需的 hello 法規和相容性需求，以及公司的合法保留需求。 經過分類的資料可能會引發關於提供者已儲存的資料在保留持續時間和例外方面的問題；未正確分類的資料更可能會有這類問題。 

> [!TIP]
> 深入了解 Azure 資料保留原則，甚至讀取 hello [Microsoft 線上訂用帳戶合約](https://azure.microsoft.com/support/legal/subscription-agreement/)
> 
> 

## <a name="protecting-confidential-data"></a>保護機密資料
資料分類之後，尋找及實作方式 tooprotect 機密資料會成為任何資料保護部署策略中不可或缺的一部分。 保護機密資料時，需要多加注意 toohow 資料儲存和傳輸傳統架構也如同 hello 雲端中。 

本節提供 toohelp 保護已分類為機密的資料可以自動化強制努力一些技術的相關基本資訊。 

下列圖顯示 hello，為這些技術可以部署為在內部部署或雲端式解決方案，或混合式的方式，與它們在內部部署的某些部分 hello 雲端中。 （某些技術，例如加密和權限管理，也擴充 toouser 裝置）。  

![技術](./media/azure-security-data-classification/azure-security-data-classification-fig4.png)

### <a name="rights-management-software"></a>版權管理軟體
想要防止資料外洩，其中一個解決方案便是版權管理軟體。 嘗試 toointerrupt hello 在組織中的結束點的資訊流程的方式，與權限管理軟體運作內的資料儲存技術的深度層級上的。 文件會進行加密，並且會控制誰可以解密文件，所使用的存取控制會定義在驗證控制解決方案中，例如目錄服務。  

> [!TIP]
> 做為 hello 資訊保護方案 tooprotect 資料在不同情況下，您可以使用 Azure Rights Management (Azure RMS)。 如需有關此 Azure 解決方案的詳細資訊，請閱讀[什麼是 Azure Rights Management？](https://docs.microsoft.com/rights-management/understand-explore/what-is-azure-rms)。
> 
> 

某些權限管理軟體的 hello 優點包括： 

* 受保護的敏感資訊。 使用者可以直接使用具有版權管理功能的應用程式保護其資料。 不需要任何額外的步驟，撰寫文件、傳送電子郵件和發佈資料皆可提供一致的資料保護體驗。 
* 保護會跟著 hello 資料。 客戶持續掌控哪些人擁有存取 tootheir 資料，不論在 hello 雲端，現有的 IT 基礎結構，或在 hello 使用者的桌面。 組織可以選擇 tooencrypt 其資料，並限制根據 tootheir 商務需求的存取。 
* 預設資訊保護原則。 系統管理員和使用者可以針對許多常見商務案例使用標準原則，例如「公司機密 - 唯讀」和「不要轉送」。 支援一組豐富的使用權限的例如讀取、 複製、 列印、 編輯、 儲存和轉寄 tooallow 有彈性地定義自訂使用權限。 

> [!TIP]
> 您可以使用待用資料的 [Azure 儲存體服務加密](../storage/storage-service-encryption.md)來保護 Azure 儲存體中的資料。 您也可以使用[Azure 磁碟加密](azure-security-disk-encryption.md)toohelp 保護包含在使用 Azure 虛擬機器的虛擬磁碟上的資料。
> 
> 

### <a name="encryption-gateways"></a>加密閘道
加密閘道運作自己的圖層 tooprovide 加密服務由重設路徑的所有存取 toocloud 為基礎的資料。 請勿將這個方法與虛擬私人網路 (VPN) 搞混。 加密閘道是透明的設計的 tooprovide 圖層 toocloud 為基礎的解決方案。   

表示 toomanage 和保護加密傳輸中的 hello 資料，以及靜態資料分類為機密的資料，可以提供加密閘道。  

加密閘道會放入使用者裝置之間的 hello 資料流程和 tooprovide 加密/解密服務應用程式資料中心。 這些解決方案 (例如 VPN) 主要是內部部署解決方案。 它們是設計的 tooprovide 加密金鑰，有助於降低 hello 風險放置 hello 資料和一個提供者與金鑰管理可控制第三方。 這類方案的設計目的，很像加密，toowork 順暢、 透明地使用者與 hello 服務之間。 

> [!TIP]
> 您可以使用 Azure ExpressRoute tooextend 在內部部署網路到 hello Microsoft 雲端透過專用私人連線。 如需此功能的詳細資訊，請閱讀 [ExpressRoute 技術概觀](../expressroute/expressroute-introduction.md)。 內部部署網路與 Azure 之間的其他跨單位連線選項是[站對站 VPN](../vpn-gateway/vpn-gateway-howto-site-to-site-resource-manager-portal.md)。
> 
> 

### <a name="data-loss-prevention"></a>資料外洩防護
資料遺失 （有時參照的 tooas 資料外洩） 是一項重要的考量，且對許多組織而言最重要 hello 防範惡意和意外的測試人員透過外部的資料遺失。  

資料外洩防護 (DLP) 技術可以協助確保解決方案 (例如電子郵件服務) 不會傳輸已歸類為機密的資料。 組織可以充分利用現有的產品中的 DLP 功能 toohelp 防止資料遺失。 這類功能會使用可以在從頭開始或藉由 hello 軟體提供者所提供的範本輕鬆建立的原則。  

DLP 技術可以執行深入內容分析，透過關鍵字比對、 字典比對，規則運算式的評估，以及其他內容檢查 toodetect 內容違反組織的 DLP 原則。 例如，DLP 可協助防止 hello hello 下列類型的資料遺失： 

* 社會安全號碼和身分證號碼 
* 銀行資訊 
* 信用卡號碼  
* IP 位址 

某些 DLP 技術也會提供 hello 能力 toooverride hello DLP 組態 （例如，如果組織需要 tootransmit 身分證號碼資訊 tooa 薪資處理器）。 此外，您也可能 tooconfigure DLP，如此即使試圖 toosend 機密資訊，應該不會在傳輸之前通知使用者。 

> [!TIP]
> 您可以使用 Office 365 DLP 功能 tooprotect 文件。 如需詳細資訊，請閱讀 [Office 365 compliance controls: Data Loss Prevention (Office 365 法規遵循控制︰資料外洩防護)](https://blogs.office.com/2013/10/28/office-365-compliance-controls-data-loss-prevention/)。
> 
> 

## <a name="see-also"></a>另請參閱
* [Azure 資料加密最佳作法](azure-security-data-encryption-best-practices.md)
* [Azure 身分識別管理和存取控制安全性最佳作法](azure-security-identity-management-best-practices.md)
* [Azure 安全性小組部落格](http://blogs.msdn.com/b/azuresecurity/)
* [Microsoft 安全性回應中心](https://technet.microsoft.com/library/dn440717.aspx)

