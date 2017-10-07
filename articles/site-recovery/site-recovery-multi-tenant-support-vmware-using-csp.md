---
title: "VMware VM 複寫 tooAzure （CSP 程式） 的 aaaMulti 租用戶支援 |Microsoft 文件"
description: "描述如何 toodeploy Azure Site Recovery 中的多租用戶環境 tooorchestrate 複寫、 容錯移轉和復原的內部部署 VMware 虛擬機器 (Vm) tooAzure hello CSP 程式透過使用 hello Azure 入口網站"
services: site-recovery
documentationcenter: 
author: mayanknayar
manager: rochakm
editor: 
ms.assetid: 
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/23/2017
ms.author: manayar
ms.openlocfilehash: 9be555c9a438f66e6d3dfcdc9f507a84763846d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="multi-tenant-support-in-azure-site-recovery-for-replicating-vmware-virtual-machines-tooazure-through-csp"></a>複寫透過 CSP 的 VMware 虛擬機器 tooAzure Azure Site Recovery 中的多租用戶支援

Azure Site Recovery 支援租用戶訂用帳戶的多租用戶環境。 它也支援多租用戶的租用戶訂用帳戶所建立及管理透過 hello Microsoft 雲端方案提供者 (CSP) 計劃。 這篇文章會說明實作和管理多租用戶 VMware-Azure 案例的 hello 指引。 其中也涵蓋透過 CSP 建立及管理租用戶訂用帳戶。

本指南大量繪製 hello 複寫 VMware 虛擬機器 tooAzure 現有文件。 如需詳細資訊，請參閱[與 Site Recovery 的複寫 VMware 虛擬機器 tooAzure](site-recovery-vmware-to-azure.md)。

## <a name="multi-tenant-environments"></a>多租用戶環境
多租用戶模型主要有三種：

* **共用裝載服務提供者 (HSP)**: hello 合作夥伴擁有 hello 實體基礎結構，並使用共用的資源 （vCenter、 資料中心、 實體儲存體，等等） toohost 上的多個租用戶 Vm hello 相同的基礎結構。 hello 夥伴可以提供災害復原管理受管理的服務，或 hello 租用戶可以擁有災害復原做為自助服務方案。

* **專用主控的服務提供者**: hello 夥伴已擁有 hello 實體基礎結構，但使用專用的資源 （多部 Vcenter、 實體 datastores，等等） toohost 另外的基礎結構上的每個租用戶 Vm。 hello 夥伴可以提供災害復原管理受管理的服務，或 hello 租用戶可以擁有它做為自助服務方案。

* **管理服務提供者 (MSP)**: hello 客戶擁有裝載 hello Vm 的 hello 實體基礎結構和 hello 夥伴提供嚴重損壞修復啟用和管理。

## <a name="shared-hosting-multi-tenant-guidance"></a>共用主機多租用戶指南
本章節涵蓋詳細的 hello 共用裝載案例。 hello 其他兩個案例是子集 hello 共用裝載案例中，並使用 hello 相同的原則。 hello 差異描述結尾 hello hello 共用裝載的指引。

hello 基本需求的多租用戶案例就是 tooisolate hello 各種租用戶。 一個租用戶不應該能 tooobserve 另一個租用戶裝載。 這個需求在自助管理環境中，比在合作夥伴管理的環境中來得重要，甚至有重大影響。 本指南假設租用戶隔離是必要條件。

hello 架構是以 hello 下列圖表所示：

![含一個 vCenter 的共用 HSP](./media/site-recovery-multi-tenant-support-vmware-using-csp/shared-hosting-scenario.png)  
**含一個 vCenter 的共用主機案例**

Hello 上述圖表所示，每個客戶都有個別的管理伺服器。 此設定限制租用戶存取 tootenant 特定 Vm，並可讓租用戶隔離。 VMware 虛擬機器複寫案例使用 hello 組態伺服器 toomanage 帳戶 toodiscover Vm，並安裝代理程式。 我們會遵循 hello 多租用戶環境中，限制他們透過 vCenter VM 探索 hello 加入相同的原則的存取控制。

hello 資料隔離需求需要所有的機密的基礎結構資訊 （例如存取認證） 保持 tootenants 保密。 基於這個理由，我們建議 hello 管理伺服器的所有元件都保有 hello 夥伴的 hello 專有控制權。 hello 管理伺服器元件包括：
* 組態伺服器 (CS)
* 處理序伺服器 (PS)
* 主要目標伺服器 (MT) 

向外延展 PS 也是在 hello 夥伴的控制之下。

### <a name="every-cs-in-hello-multi-tenant-scenario-uses-two-accounts"></a>每個 CS hello 多租用戶案例中的會使用兩個帳戶

- **vCenter 存取帳戶**： 使用這個帳戶 toodiscover 租用戶 Vm。 它有 vCenter 指派 tooit （如 hello 下一節中所述） 的存取權限。 toohelp 避免意外存取流失，請建議夥伴 hello 組態工具中輸入這些認證本身。

- **虛擬機器存取帳戶**： 透過自動推入 hello 租用戶 Vm 上使用此帳戶 tooinstall hello 行動代理程式。 它通常是租用戶可能會提供 tooa 夥伴或，或者，hello 夥伴可能直接管理的網域帳戶。 如果租用戶不希望 tooshare hello 詳細資料與 hello 夥伴直接，他或她可以允許透過有限時 tooenter hello 認證會存取 toohello CS，或與 hello 夥伴協助行動手動安裝代理程式。

### <a name="requirements-for-a-vcenter-access-account"></a>vCenter 存取帳戶的需求

Hello 前面一節所述，您必須設定 hello CS 有特殊角色指派 tooit 的帳戶。 hello 角色指派必須套用 toohello vCenter 存取帳戶的每個 vCenter 物件並不會傳播 toohello 子物件。 此組態可確保租用戶隔離，因為存取傳播可能會導致意外存取 tooother 物件。

![hello 傳播 tooChild 物件選項](./media/site-recovery-multi-tenant-support-vmware-using-csp/assign-permissions-without-propagation.png)

hello 的替代方式是 tooassign hello 使用者帳戶和 hello datacenter 物件的角色，並將它們傳播 toohello 子物件。 然後為 hello 帳戶*沒有存取*應該是無法存取 tooa 特定租用戶，每個物件 （例如其他租用戶 Vm) 的角色。 這項設定很麻煩，並因為每個新的子物件也會自動授與存取權繼承自 hello 父公開意外存取控制項。 因此，我們建議您先使用 hello 第一種方法。

hello vCenter 帳戶存取權的程序如下所示：

1. 建立新的角色，藉由複製預先定義的 hello*唯讀*角色，然後將它提供一個方便的名稱 （例如 Azure_Site_Recovery，如本範例所示)。

2. 指派下列權限 toothis 角色 hello:

    * **資料存放區**：配置空間、瀏覽資料存放區、底層檔案作業、移除檔案、更新虛擬機器檔案

    * **網路**：網路指派

    * **資源**： 指派 VM tooresource 集區，移轉電源已關閉 VM、 電源已開啟 VM 的移轉

    * **工作**：建立工作、更新工作

    * **虛擬機器**： 
        * 組態 > 全部
        * 互動 > 回答問題、裝置連線、設定 CD 媒體、設定磁碟片媒體、電源關閉、電源開啟、VMware 工具安裝
        * 清查 > 從現有建立、建立新的、註冊、取消註冊
        * 佈建 > 允許虛擬機器下載、允許虛擬機器檔案上傳
        * 快照集管理 > 移除快照集

    ![hello 編輯角色 對話方塊](./media/site-recovery-multi-tenant-support-vmware-using-csp/edit-role-permissions.png)

3. 指派存取層級 toohello vCenter 帳戶 （用於 hello 租用戶 CS） 的各種不同的物件，如下所示：

>| Object | 角色 | 備註 |
>| --- | --- | --- |
>| vCenter | 唯讀 | 只有 tooallow vCenter 需要存取來管理不同的物件。 如果 hello 帳戶永遠不會將 toobe 提供 tooa 租用戶，或用於 hello vCenter 上的任何管理作業，您可以移除此權限。 |
>| 資料中心 | Azure_Site_Recovery |  |
>| 主機和主機叢集 | Azure_Site_Recovery | 重新可確保存取在 hello 物件層級，以便只可存取主機有租用戶 Vm 容錯移轉之前和之後容錯回復。 |
>| 資料存放區和資料存放區叢集 | Azure_Site_Recovery | 同上。 |
>| 網路 | Azure_Site_Recovery |  |
>| 管理伺服器 | Azure_Site_Recovery | 如果任何 hello CS 機器之外，包括存取 tooall 元件 （CS、 PS 和 MT）。 |
>| 租用戶 VM | Azure_Site_Recovery | 可確保任何新的租用戶的特定租用戶 Vm 也會取得此存取權，或將不會透過 hello Azure 入口網站可探索。 |

hello vCenter 帳戶存取現在已完成。 此步驟中，可滿足 hello 最小權限需求 toocomplete 容錯回復作業。 也可以搭配現有的原則使用這些存取權限。 只需修改您現有的權限集 tooinclude 角色的權限詳細先前在步驟 2。

toorestrict 嚴重損壞修復作業，直到 hello 容錯移轉狀態 (也就是沒有容錯回復功能)，請遵循上述程序，並發生例外狀況的 hello： 而不要將指派 hello *Azure_Site_Recovery*角色toohello vCenter 存取帳戶，只指派*唯讀*角色 toothat 帳戶。 這個權限集合會允許虛擬機器複寫和容錯移轉，而不允許容錯回復。 Hello 前面程序中的其他所有項目會維持原狀。 tooensure 隔離租用戶，並限制 VM 探索，仍在 hello 物件層級的唯一和未傳播 toochild 物件指派每個權限。

## <a name="other-multi-tenant-environments"></a>其他多租用戶環境

前一節所述方式 hello tooset 共用裝載解決方案多租用戶環境。 hello 其他兩個主要解決方案也是專用主控和受管理的服務。 hello 下列各節將說明這些解決方案的 hello 架構。

### <a name="dedicated-hosting-solution"></a>專用主機解決方案

Hello 下列圖表所示，專用的主控方案中的 hello 架構差異是只有該租用戶的每個租用戶的基礎結構的設定。 由於租用戶隔離到個別的 Vcenter，hello 主機服務提供者必須仍遵循所提供的共用裝載的 hello CSP 步驟，但不需要 tooworry 租用戶隔離的相關資訊。 CSP 安裝程式會保持不變。

![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/dedicated-hosting-scenario.png)  
**含多個 vCenters 的專用主機案例**

### <a name="managed-service-solution"></a>受管理的服務解決方案

中所顯示的 hello 與下列圖表中，受管理的服務方案中的 hello 架構差異是每個租用戶的基礎結構也是實體上與其他租用戶的基礎結構分開。 此案例中通常是指 hello 租用戶擁有 hello 基礎結構和想方案提供者 toomanage 災害復原。 同樣地，由於不同的基礎結構透過實際隔離的租用戶，hello 夥伴需要針對共用裝載所提供的 toofollow hello CSP 步驟，但不需要 tooworry 租用戶隔離的相關資訊。 CSP 佈建保持不變。

![architecture-shared-hsp](./media/site-recovery-multi-tenant-support-vmware-using-csp/managed-service-scenario.png)  
**含多個 vCenters 的受管理的服務案例**

## <a name="csp-program-overview"></a>CSP 計畫概觀
hello [CSP 程式](https://partner.microsoft.com/en-US/cloud-solution-provider)培養好一起提供所有的 Microsoft 雲端服務，包括 Office 365、 Enterprise Mobility Suite 和 Microsoft Azure 的協力廠商的劇本。 CSP，與我們的合作夥伴與客戶擁有 hello 端對端關係，並成為 hello 主要關聯性的連絡點。 夥伴可以部署客戶的 Azure 訂用帳戶，並將合併訂閱 hello 自己提供加值的自訂項目。

使用 Azure Site Recovery，夥伴可以管理客戶直接透過 CSP hello 完整的災害復原解決方案。 或者，使用 CSP tooset Site Recovery 環境，讓自助服務的方式管理其自己的災害復原需求的客戶。 在這兩種情況下，夥伴都是站台復原與客戶之間的 hello 連絡人。 協力廠商服務 hello 客戶關聯性，並開立其帳單客戶站台復原使用。

## <a name="create-and-manage-tenant-accounts"></a>建立及管理租用戶帳戶

### <a name="step-0-prerequisite-check"></a>步驟 0：必要條件檢查

hello VM 必要條件是 hello hello 中所述相同[Azure Site Recovery 文件](site-recovery-vmware-to-azure.md)。 在加法 toothose prerequisites 中，您應該有 hello 先前所述的存取控制管理租用戶透過 CSP 繼續。 每個租用戶，建立個別的管理伺服器進行通訊與 hello 租用戶 Vm 和夥伴的 vCenter。 只有 hello 夥伴具有存取權限 toothis 伺服器。

### <a name="step-1-create-a-tenant-account"></a>步驟 1︰建立租用戶帳戶

1. 透過[Microsoft 合作夥伴中心](https://partnercenter.microsoft.com/)，登入 tooyour CSP 帳戶。 
 
2. 在 hello**儀表板**功能表上，選取**客戶**。

    ![hello Microsoft 夥伴中心客戶連結](./media/site-recovery-multi-tenant-support-vmware-using-csp/csp-dashboard-display.png)

3. 在開啟的 hello 頁面上，按一下 [hello**新增客戶**] 按鈕。

    ![hello Add Customer 按鈕](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-new-customer.png)

4. 在 hello**新客戶**頁面上，填寫 hello hello 租用戶帳戶的資訊詳細資料，然後按一下**下一步： 訂用帳戶**。

    ![hello 帳戶資訊 頁面](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-add-filled.png)

5. 在 hello 訂用帳戶選取 頁面上，選取 hello **Microsoft Azure**核取方塊。 您可以立即或在其他任何時候新增其他訂用帳戶。

    ![hello Microsoft Azure 訂用帳戶 核取方塊](./media/site-recovery-multi-tenant-support-vmware-using-csp/azure-subscription-selection.png)

6. 在 hello**檢閱**頁面上，確認 hello 租用戶詳細資料，然後按**送出**。

    ![hello 檢閱 頁面](./media/site-recovery-multi-tenant-support-vmware-using-csp/customer-summary-page.png)  

    在您建立 hello 租用戶帳戶後，確認網頁隨即出現，顯示 hello 詳細資料的 hello 預設帳戶及 hello 該訂用帳戶的密碼。 

7. 儲存 hello 的詳細資訊，並變更 hello 密碼稍後視需要透過 hello Azure 入口網站登入頁面。  
 
    您可以共用這項資訊與 hello 租用戶，或您可以建立並共用不同的帳戶。

### <a name="step-2-access-hello-tenant-account"></a>步驟 2： 存取 hello 租用戶的帳戶

中所述，您可以透過 hello Microsoft 夥伴中心儀表板，存取 hello 租用戶的訂用帳戶 」 步驟 1： 建立租用戶帳戶。 」 

1. 移 toohello**客戶**頁面，然後再按一下 hello hello 租用戶的帳戶名稱。

2. 在 hello**訂閱**頁面的 hello 租用戶的帳戶，您可以監視 hello 現有帳戶訂用帳戶，並視需要新增多個訂閱。 toomanage hello 租用戶的嚴重損壞修復作業，選取**（Azure 入口網站） 的所有資源**。

    ![hello 的所有資源的連結](./media/site-recovery-multi-tenant-support-vmware-using-csp/all-resources-select.png)  
    
    按一下**所有資源**授與存取 toohello 租用戶的 Azure 訂用帳戶。 您可以在 hello hello Azure Active Directory 連結，即可驗證存取的 hello Azure 入口網站右上方。

    ![[Azure Active Directory] 連結](./media/site-recovery-multi-tenant-support-vmware-using-csp/aad-admin-display.png)

您現在可以執行 hello 租用戶透過 hello Azure 入口網站的所有站台復原作業，並管理 hello 嚴重損壞修復作業。 tooaccess hello 租用戶訂用帳戶透過 CSP 受管理的嚴重損壞修復，後續 hello 前述程序。

### <a name="step-3-deploy-resources-toohello-tenant-subscription"></a>步驟 3： 部署資源 toohello 租用戶訂用帳戶
1. Hello Azure 入口網站，在建立資源群組，並將每個 hello 一般程序的復原服務保存庫。 
 
2. 下載 hello 保存庫註冊金鑰。

3. 使用 hello 保存庫註冊金鑰註冊 hello CS hello 租用戶。

4. 輸入 hello 認證 hello 兩個存取帳戶： vCenter 存取帳戶 」 且 VM 存取帳戶。

    ![管理員設定伺服器帳戶](./media/site-recovery-multi-tenant-support-vmware-using-csp/config-server-account-display.png)

### <a name="step-4-register-site-recovery-infrastructure-toohello-recovery-services-vault"></a>步驟 4： 註冊 Site Recovery 基礎結構 toohello 復原服務保存庫
1. 在 hello hello 您稍早建立的保存庫上的 Azure 入口網站中註冊 hello vCenter server toohello CS 您登錄中的 「 步驟 3： 部署資源 toohello 租用戶訂用帳戶。 」 針對此用途使用 hello vCenter 存取帳戶。
2. 完成站台復原的 hello 「 準備基礎結構 」 程序，每個 hello 一般程序。
3. hello Vm 現在已經準備就緒 toobe 複寫。 確認只有 hello 租用戶的 Vm 會顯示在 hello**選取虛擬機器**刀鋒視窗底下 hello**複寫**選項。

    ![Hello 選取虛擬機器刀鋒視窗上的租用戶 Vm 清單](./media/site-recovery-multi-tenant-support-vmware-using-csp/tenant-vm-display.png)

### <a name="step-5-assign-tenant-access-toohello-subscription"></a>步驟 5： 指派租用戶存取 toohello 訂用帳戶

自助災害復原，提供 toohello 租用戶 hello 帳戶詳細資料，如所述的 hello 步驟 6 中 「 步驟 1： 建立租用戶帳戶 」 一節。 Hello 夥伴設定 hello 嚴重損壞修復基礎結構之後，請執行此動作。 Hello 災害復原類型是否受管理或自助服務，合作夥伴必須透過 hello CSP 入口網站存取租用戶訂用帳戶。 這些設定 hello 夥伴擁有保存庫，並註冊基礎結構 toohello 租用戶訂用帳戶。

協力廠商也可以新增新使用者 toohello 租用戶訂用帳戶透過 hello CSP 入口網站執行 hello 下列：

1. 移 toohello 租用戶的 CSP 訂用帳戶] 頁面上，然後再選取 [hello**使用者與授權**選項。

    ![hello 租用戶的 CSP 訂用帳戶頁面](./media/site-recovery-multi-tenant-support-vmware-using-csp/users-and-licences.png)

    您現在可以建立新的使用者輸入 hello 相關詳細資料，然後選取 權限，或上傳的 CSV 檔案中的使用者的 hello 清單。

2. 您已建立新的使用者之後，請回到 toohello Azure 入口網站，然後在 hello**訂用帳戶**刀鋒視窗中，選取 hello 相關訂用帳戶。

3. 在開啟的 hello 刀鋒視窗，選取**存取控制 (IAM)**，然後按一下**新增**tooadd hello 相關的存取層級的使用者。      
    透過 hello CSP 入口網站所建立的 hello 使用者會自動顯示 hello] 刀鋒視窗，按一下 [存取層級之後，隨即開啟。

    ![新增使用者](./media/site-recovery-multi-tenant-support-vmware-using-csp/add-user-subscription.png)

    大部分的管理作業，如 hello*參與者*角色已足夠。 除了變更存取層級 (必須具有「擁有者」存取層級) 之外，具有此存取層級的使用者可以在訂用帳戶上執行任何作業。 您也可以微調 hello 所需的存取層級。
