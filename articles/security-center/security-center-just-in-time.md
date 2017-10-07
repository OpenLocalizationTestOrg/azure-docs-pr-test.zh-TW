---
title: "aaaJust 時間虛擬機器中的存取 Azure 資訊安全中心 |Microsoft 文件"
description: "本文件逐步解說如何在 Azure 資訊安全中心可以協助您控制 VM 存取存取 tooyour Azure 虛擬機器。"
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
ms.date: 08/08/2017
ms.author: terrylan
ms.openlocfilehash: e6b58dd2c686cb227392b294e85914df5a546016
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="manage-virtual-machine-access-using-just-in-time"></a>使用 Just-In-Time 管理虛擬機器存取

時間虛擬機器 (VM) 中只可以存取使用的 toolock 輸入的流量 tooyour Azure Vm，降低暴露 tooattacks 同時提供讓您輕鬆存取 tooconnect tooVMs 需要時關閉。

> [!NOTE]
> 在時間 」 功能中的 hello 已預覽並可使用 hello 標準層的資訊安全中心。  請參閱[定價](security-center-pricing.md)toolearn 詳細的資訊安全中心的定價層。
>
>

## <a name="attack-scenario"></a>攻擊案例

暴力攻擊的常見目標管理連接埠為表示 toogain 存取 tooa VM。 如果成功的話，攻擊者可以使用控制 hello VM，並建立據點至您的環境。

其中一種方式 tooreduce 曝光 tooa 暴力攻擊是時間的 toolimit hello 數量的連接埠已開啟。 管理連接埠隨時都能執行需要 toobe 開啟。 他們只需要 toobe 開啟時您所連接的 toohello VM，例如 tooperform 管理或維護工作。 在啟用時，會使用資訊安全中心[網路安全性群組](../virtual-network/virtual-networks-nsg.md)(NSG) 規則，限制存取 toomanagement 連接埠，因此無法由攻擊者為目標。

![Just-In-Time 案例][1]

## <a name="how-does-just-in-time-access-work"></a>Just-In-Time 存取如何運作？

在啟用時，資訊安全中心鎖定輸入的流量 tooyour Azure Vm 建立 NSG 規則。 您選取 hello 連接埠上 hello VM toowhich 輸入的流量會鎖定。 這些連接埠是由在時間方案中的 hello 控制。

當使用者要求存取 tooa VM 時，資訊安全中心會檢查該 hello 使用者擁有[角色型存取控制 (RBAC)](../active-directory/role-based-access-control-configure.md) hello Azure 資源提供寫入存取權的權限。 如果他們擁有寫入權限、 hello 會核准要求並且資訊安全中心會自動設定的網路安全性群組 (Nsg) tooallow hello 傳入流量 toohello 管理連接埠 hello 您指定的時間量。 Hello 時間到期之後，資訊安全中心還原 hello Nsg tootheir 先前的狀態。

> [!NOTE]
> 資訊安全中心 Just-In-Time VM 存取目前僅支援透過 Azure Resource Manager 部署的 VM。 傳統的 hello 與資源管理員部署模型的詳細資訊請參閱的 toolearn [Azure Resource Manager vs 傳統部署](../azure-resource-manager/resource-manager-deployment-model.md)。
>
>

## <a name="using-just-in-time-access"></a>使用 Just-In-Time 存取

hello**階段 VM 存取中的恰好**磚 hello**資訊安全中心**刀鋒視窗中顯示的 Vm 設定為在時間的存取權與 hello 核准的存取提出的要求數目 hello 在過去一週中的 hello 數目。

選取 hello**階段 VM 存取中的恰好**磚與 hello**恰好在時間 VM 存取**刀鋒視窗隨即開啟。

![[Just-In-Time VM 存取] 圖格][2]

hello**階段 VM 存取中的恰好**刀鋒視窗中提供您 Vm hello 狀態的相關資訊：

- **設定**-已設定的 toosupport 只在時間 VM 存取的 Vm。 顯示 hello 資料 hello 過去一週，而且包含的每個 VM hello 數目核准的要求、 上次存取日期和時間和最後一位使用者。
- [建議] - 可支援但未設定 Just-In-Time VM 存取的 VM。 建議您啟用這些 VM 的 Just-In-Time VM 存取控制。 請參閱[啟用 Just-In-Time VM 存取](#enable-just-in-time-vm-access)。
- **不推薦**-可能會導致 VM toobe 建議的原因如下：
  - 遺漏 NSG-hello 時間解決方案中只需要就地 NSG toobe。
  - 傳統 VM - 資訊安全中心 Just-In-Time VM 存取目前僅支援透過 Azure Resource Manager 部署的 VM。 在時間方案中的 hello 不支援傳統的部署。
  - 其他-VM 如果是在此類別在解決方案已關閉 hello 訂用帳戶或 hello 資源群組、 hello 安全性原則中的 hello 或該 VM 的 hello 遺漏公用 IP，因此未就地擁有 NSG。

## <a name="configuring-a-just-in-time-access-policy"></a>設定 Just-In-Time 存取原則

tooselect hello 想 tooenable Vm:

1. 在 hello**階段 VM 存取中的恰好**刀鋒視窗中，選取 hello**建議** 索引標籤。

  ![啟用 Just-In-Time 存取][3]

2. 在下**Vm**，選取您想 tooenable hello Vm。 這會使核取記號下一步 tooa VM。
3. 選取 [在 VM 上啟用 JIT]。
4. 選取 [ **儲存**]。

### <a name="default-ports"></a>預設連接埠

您可以看到的資訊安全中心建議啟用 just-in-time hello 預設連接埠。

1. 在 hello**階段 VM 存取中的恰好**刀鋒視窗中，選取 hello**建議** 索引標籤。

  ![顯示預設連接埠][6]

2. 在 [VM] 下方，選取 VM。 這會使核取記號下一步 toohello VM，並開啟 hello **JIT VM 存取組態**刀鋒視窗。 此刀鋒視窗會顯示 hello 預設連接埠。

### <a name="add-ports"></a>新增連接埠

從 hello **JIT VM 存取組態**刀鋒視窗中，您可以同時新增並設定新的連接埠，您想要只在時間方案 tooenable hello。

1. 在 hello **JIT VM 存取組態**刀鋒視窗中，選取**新增**。 這會開啟 hello**新增連接埠組態**刀鋒視窗。

  ![連接埠組態][7]

2. 在**新增連接埠組態**刀鋒視窗中，識別 hello 允許通訊埠，通訊協定類型的來源 Ip 和最大要求的時間。

  允許的來源 Ip 是 hello IP 範圍 tooget 允許的存取已核准的要求。

  最大要求時間是特定的連接埠，可以開啟 hello 大的時間間隔。

3. 選取 [確定] 。

## <a name="requesting-access-tooa-vm"></a>要求存取 tooa VM

toorequest 存取 tooa VM:

1. 在 hello**恰好在時間 VM 存取**刀鋒視窗中，選取 hello**設定** 索引標籤。
2. 在下**Vm**，選取您想要 tooenable 存取 hello Vm。 這會使核取記號下一步 tooa VM。
3. 選取 [要求存取]。 這會開啟 hello**要求存取**刀鋒視窗。

  ![要求存取 tooa VM][4]

4. 在 hello**要求存取**刀鋒視窗中，您設定 hello 來源 IP hello 連接埠，以及每個 VM hello 連接埠 tooopen 開啟 tooand hello 時段的 hello 通訊埠已開啟的。 您可以要求存取只有 toohello 連接埠 hello 只在時間原則中所設定。 每個連接埠有衍生自 hello 只在時間原則的最大允許的時間。
5. 選取 [開啟連接埠]。

## <a name="editing-a-just-in-time-access-policy"></a>編輯 Just-In-Time 存取原則

您可以變更 VM 的現有時間原則中，只將新增並設定新的連接埠 tooopen 該 vm，或變更任何其他參數相關的 tooan 已受保護的通訊埠。

在順序 tooedit 現有的 VM，時間原則在 hello**設定**索引標籤可用：

1. 在下**Vm**，選取 VM tooadd 連接埠 tooby hello 三個點 hello 資料列中按一下該 vm。 這會開啟功能表。
2. 選取**編輯**hello 功能表中。 這會開啟 hello **JIT VM 存取組態**刀鋒視窗。

  ![編輯原則][8]

3. 在 hello **JIT VM 存取組態**刀鋒視窗中，您可以在其連接埠，按一下編輯 hello 已受保護的通訊埠現有的設定，或者您可以選取**新增**。 這會開啟 hello**新增連接埠組態**刀鋒視窗。

  ![新增連接埠][7]

4. 在**新增連接埠組態**刀鋒視窗中識別 hello 連接埠、 通訊協定類型，允許的來源 Ip 時，以及最大要求時間。
5. 選取 [確定] 。
6. 選取 [ **儲存**]。

## <a name="auditing-just-in-time-access-activity"></a>稽核 Just-In-Time 存取活動

您可以使用記錄搜尋來深入了解 VM 活動。 tooview 記錄檔：

1. 在 hello**恰好在時間 VM 存取**刀鋒視窗中，選取 hello**設定** 索引標籤。
2. 在下**Vm**，選取 關於 VM tooview 資訊 hello 三個點 hello 資料列中按一下該 vm。 這會開啟功能表。
3. 選取**活動記錄檔**hello 功能表中。 這會開啟 hello**活動記錄檔**刀鋒視窗。

![選取活動記錄][9]

hello**活動記錄檔**刀鋒視窗中提供的時間、 日期和訂用帳戶以及該 vm 的先前作業篩選的檢視。

![檢視活動記錄][5]

您可以藉由選取下載 hello 記錄資訊**按一下這裡 toodownload hello 的所有項目做為 CSV**。

修改 hello 篩選，然後選取**套用**toocreate 搜尋和記錄檔。

## <a name="using-just-in-time-vm-access-via-powershell"></a>透過 PowerShell 使用 Just-In-Time VM 存取

在訂單 toouse hello 只在透過 PowerShell 時間方案，請確定您擁有 hello[最新](/powershell/azure/install-azurerm-ps)Azure PowerShell 版本。
一旦您這樣做，您需要 tooinstall hello[最新](https://www.powershellgallery.com/packages/Azure-Security-Center/0.0.12)hello PowerShell 資源庫從 Azure 資訊安全中心。

### <a name="configuring-a-just-in-time-policy-for-a-vm"></a>為 VM 設定 Just-In-Time 原則

tooconfigure 只在特定 VM 上的時間原則，您需要 toorun 此命令在您的 PowerShell 工作階段中： 組 ASCJITAccessPolicy。
請遵循詳細的 hello cmdlet 文件 toolearn。

### <a name="requesting-access-tooa-vm"></a>要求存取 tooa VM

只在時間方案 hello tooaccess 受到將特定 VM，您需要 toorun 此命令中您的 PowerShell 工作階段： ASCJITAccess 叫用。
請遵循詳細的 hello cmdlet 文件 toolearn。

## <a name="next-steps"></a>後續步驟
在本文中，您學到如何在 VM 存取在資訊安全中心可協助您控制存取 tooyour Azure 虛擬機器。

toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

- [設定安全性原則](security-center-policies.md)— 了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
- [管理安全性建議](security-center-recommendations.md) — 了解建議如何協助保護您的 Azure 資源。
- [安全性健全狀況監視](security-center-monitoring.md)— 了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
- [管理及回應 toosecurity 警示](security-center-managing-and-responding-alerts.md)— 了解如何 toomanage 和回應 toosecurity 警示。
- [監視協力廠商解決方案](security-center-partner-solutions.md)— 了解如何 toomonitor hello 的協力廠商解決方案的健全狀況狀態。
- [資訊安全中心常見問題集](security-center-faq.md)— 尋找使用 hello 服務相關的常見問題集。
- [Azure 安全性部落格](https://blogs.msdn.microsoft.com/azuresecurity/) — 尋找有關 Azure 安全性與相容性的部落格文章。


<!--Image references-->
[1]: ./media/security-center-just-in-time/just-in-time-scenario.png
[2]: ./media/security-center-just-in-time/just-in-time.png
[3]: ./media/security-center-just-in-time/enable-just-in-time-access.png
[4]: ./media/security-center-just-in-time/request-access-to-a-vm.png
[5]: ./media/security-center-just-in-time/activity-log.png
[6]: ./media/security-center-just-in-time/default-ports.png
[7]: ./media/security-center-just-in-time/add-a-port.png
[8]: ./media/security-center-just-in-time/edit-policy.png
[9]: ./media/security-center-just-in-time/select-activity-log.png
