---
title: "Azure 資訊安全中心中的 Just-In-Time 虛擬機器存取 | Microsoft Docs"
description: "本文件將逐步引導您認識 Azure 資訊安全中心的 Just-In-Time VM 存取可如何協助您控制 Azure 虛擬機器的存取。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 10/04/2017
ms.author: terrylan
ms.openlocfilehash: c715afe55a3aedd5c4f826bc34c3c56e167d2f82
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/11/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time-preview"></a>使用 Just-In-Time 管理虛擬機器存取 (預覽)

Just-In-Time 虛擬機器 (VM) 存取可用於鎖定 Azure VM 的輸入流量、降低暴露於攻擊的風險，同時能夠視需要輕鬆存取連線至 VM。

> [!NOTE]
> Just-in-Time 為預覽功能，由資訊安全中心的標準層提供。  若要深入了解資訊安全中心的定價層，請參閱[價格](security-center-pricing.md)。
>
>

## <a name="attack-scenario"></a>攻擊案例

暴力密碼破解攻擊通常會以管理連接埠為目標，作為取得 VM 存取權的手段。 如果成功，攻擊者便可以控制 VM，並在您的環境中建立據點。

若要降低暴露於暴力密碼破解攻擊，其中一個方法是限制的連接埠開啟時間。 管理連接埠不需要隨時保持開啟。 只有在連線至 VM 時 (例如進行執行管理或維修工作)，才需要將管理連接埠開啟。 啟用 Just-In-Time 時，資訊安全中心會使用[網路安全性群組](../virtual-network/virtual-networks-nsg.md) (NSG) 規則，以限制對管理連接埠的存取，讓攻擊者無法將這些連接埠作為攻擊目標。

![Just-In-Time 案例][1]

## <a name="how-does-just-in-time-access-work"></a>Just-In-Time 存取如何運作？

啟用 Just-In-Time 時，資訊安全中心會建立 NSG 規則，藉此鎖定進入 Azure VM 的流量。 系統會鎖定選取的 VM 連接埠的輸入流量。 Just-In-Time 解決方案會控制這些連接埠。

當使用者要求存取 VM 時，資訊安全中心會檢查該使用者是否擁有可提供 VM 寫入存取權限的[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md) 權限。 如果其擁有寫入權限、要求會通過核准，且資訊安全中心會將網路安全性群組 (NSG) 自動設定為在指定時間內允許輸入流量進入管理連接埠。 時間到期之後，資訊安全中心會將 NSG 還原為其先前的狀態。

> [!NOTE]
> 資訊安全中心 Just-In-Time VM 存取目前僅支援透過 Azure Resource Manager 部署的 VM。 若要深入了解傳統部署和資源管理員部署的模型，請參閱 [Azure Resource Manager 與傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)。
>
>

## <a name="using-just-in-time-access"></a>使用 Just-In-Time 存取

[資訊安全中心] 下方的 [Just-In-Time VM 存取] 圖格會顯示過去一週內設定 Just-In-Time 存取的 VM 數目和核准的存取要求數目。

![[Just-In-Time VM 存取] 圖格][2]

選取 [Just-In-Time VM 存取] 圖格，[Just-In-Time VM 存取] 隨即開啟。

![[Just-In-Time VM 存取] 圖格][10]

[Just-In-Time VM 存取] 會提供 VM 狀態的相關資訊：

- [已設定] - 已設定為支援 Just-In-Time VM 存取的 VM。 其會提供過去一週的資料，包含每個 VM 核准的要求數量、上次存取的日期和時間、以及最後一位使用者。
- [建議] - 可支援但未設定 Just-In-Time VM 存取的 VM。 建議您啟用這些 VM 的 Just-In-Time VM 存取控制。 請參閱[設定 Just-In-Time 存取原則](#configuring-a-just-in-time-access-policy)。
- [不建議] - 可能會導致不建議 VM 進行設定的原因如下：
  - 缺少 NSG - Just-In-Time 解決方案需要 NSG。
  - 傳統 VM - 資訊安全中心 Just-In-Time VM 存取目前僅支援透過 Azure Resource Manager 部署的 VM。 Just-In-Time 解決方案不支援傳統部署。
  - 其他 - 如果訂用帳戶或資源群組的安全性原則已關閉 Just-In-Time 解決方案，或 VM 缺少公用 IP 且未設定 NSG，則該 VM 也屬於此類別。

## <a name="configuring-a-just-in-time-access-policy"></a>設定 Just-In-Time 存取原則

若要選取您想要啟用的 VM：

1. 在 [Just-In-Time VM 存取] 下方，選取 [建議] 索引標籤。

  ![啟用 Just-In-Time 存取][3]

2. 在 [虛擬機器] 下方，選取您想要啟用的 VM。 這會讓 VM 旁邊顯示核取記號。
3. 選取 [在 VM 上啟用 JIT]。
4. 選取 [ **儲存**]。

### <a name="default-ports"></a>預設連接埠

您可以看到資訊安全中心建議啟用 Just-In-Time 的預設連接埠。

1. 在 [Just-In-Time VM 存取] 下方，選取 [建議] 索引標籤。

  ![顯示預設連接埠][6]

2. 在 [VM] 下方，選取 VM。 這會讓 VM 旁邊顯示核取記號，並開啟 [JIT VM 存取設定]。 此刀鋒視窗會顯示預設連接埠。

### <a name="add-ports"></a>新增連接埠

在 [JIT VM 存取設定] 下方，您也可以新增和設定要啟用 Just-In-Time 解決方案的新連接埠。

1. 在 [JIT VM 存取設定] 下方，選取 [新增]。 這會開啟 [新增連接埠組態]。

  ![連接埠組態][7]

2. 在 [新增連接埠組態] 下方，可識別連接埠、通訊協定類型、允許的來源 IP 和要求時間上限。

  允許的來源 IP 是經核准的要求中允許取得存取權的 IP 範圍。

  要求時間上限是開啟特定連接埠的時間範圍上限。

3. 選取 [確定] 。

## <a name="requesting-access-to-a-vm"></a>要求存取 VM

若要要求存取 VM：

1. 在 [Just-In-Time VM 存取] 下方，選取 [已設定] 索引標籤。
2. 在 [VM] 下方，選取您想要啟用存取的 VM。 這會讓 VM 旁邊顯示核取記號。
3. 選取 [要求存取]。 這會開啟 [要求存取]。

  ![要求存取 VM][4]

4. 在 [要求存取] 下方，可設定要針對每個 VM 開啟的連接埠，以及對連接埠開放的來源 IP，還有開啟連接埠的時間範圍。 您可以要求只存取 Just-In-Time 原則中設定的連接埠。 每個連接埠都具有衍生自 Just-In-Time 原則的許可時間上限。
5. 選取 [開啟連接埠]。

## <a name="editing-a-just-in-time-access-policy"></a>編輯 Just-In-Time 存取原則

可以藉由新增和設定一個對 VM 開放的新連接埠，或是變更與受保護的連接埠相關的其他任何參數，來變更該 VM 現有的 Just-In-Time 原則。

若要編輯 VM 現有的 Just-In-Time 原則，請使用 [已設定] 索引標籤：

1. 在 [VM] 下方，按一下 VM 列中的三點圖示，選取要新增連接埠的 VM。 這會開啟功能表。
2. 在功能表中，選取 [編輯]。 這會開啟 [JIT VM 存取設定]。

  ![編輯原則][8]

3. 在 [JIT VM 存取設定] 下方，您可以按一下已經受到保護的連接埠來編輯該連接埠的現有設定，也可以選取 [新增]。 這會開啟 [新增連接埠組態]。

  ![新增連接埠][7]

4. 在 [新增連接埠組態] 下方，識別連接埠、通訊協定類型、允許的來源 IP 和要求時間上限。
5. 選取 [確定] 。
6. 選取 [ **儲存**]。

## <a name="auditing-just-in-time-access-activity"></a>稽核 Just-In-Time 存取活動

您可以使用記錄搜尋來深入了解 VM 活動。 若要檢視記錄：

1. 在 [Just-In-Time VM 存取] 下方，選取 [已設定] 索引標籤。
2. 在 [VM] 下方，按一下 VM 列中的三點圖示，選取要檢視相關資訊的 VM。 這會開啟功能表。
3. 在功能表中，選取 [活動記錄]。 這會開啟 [活動記錄]。

  ![選取活動記錄][9]

  [活動記錄] 可提供篩選過的檢視，列出該 VM 先前的作業，以及時間、日期和訂用帳戶。

  ![檢視活動記錄][5]

選取 [按一下這裡，將所有項目下載為 CSV 格式] 即可下載記錄資訊。

修改篩選條件，並選取 [套用] 以建立搜尋和記錄。

## <a name="using-just-in-time-vm-access-via-powershell"></a>透過 PowerShell 使用 Just-In-Time VM 存取

若要透過 PowerShell 使用 Just-In-Time 解決方案，請確定您擁有 Azure PowerShell 的[最新](/powershell/azure/install-azurerm-ps)版本。
若確定有最新版本，則需要從 PowerShell 資源庫安裝[最新](https://aka.ms/asc-psgallery)的 Azure 資訊安全中心。

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a>為 VM 設定 Just-In-Time 原則

若要在特定 VM 上設定 Just-In-Time 原則，您需要在 PowerShell 工作階段中執行下列命令：Set-ASCJITAccessPolicy。
如需詳細資訊，請參閱 Cmdlet 文件。

### <a name="requesting-access-to-a-vm"></a>要求存取 VM

若要存取受 Just-In-Time 原則保護的特定 VM，您需要在 PowerShell 工作階段中執行下列命令：Invoke-ASCJITAccess。
如需詳細資訊，請參閱 Cmdlet 文件。

## <a name="next-steps"></a>後續步驟
您已透過本文了解到資訊安全中心中的 Just-In-Time VM 存取可如何協助您控制 Azure 虛擬機器的存取。

如要深入了解資訊安全中心，請參閱下列主題：

- [設定安全性原則](security-center-policies.md) — 了解如何為您的 Azure 訂用帳戶及資源群組設定安全性原則。
- [管理安全性建議](security-center-recommendations.md) — 了解建議如何協助保護您的 Azure 資源。
- [安全性健康情況監視](security-center-monitoring.md) — 了解如何監視 Azure 資源的健康清況。
- [管理與回應安全性警示](security-center-managing-and-responding-alerts.md) — 了解如何管理與回應安全性警示。
- [監視合作夥伴解決方案](security-center-partner-solutions.md) — 了解如何監視合作夥伴解決方案的健全狀態。
- [資訊安全中心常見問題集](security-center-faq.md) — 尋找有關使用服務的常見問題。
- [Azure 安全性部落格](https://blogs.msdn.microsoft.com/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[10]: ./media/security-center-just-in-time/just-in-time-access.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
