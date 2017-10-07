---
title: "aaaTroubleshoot StorSimple 部署問題 |Microsoft 文件"
description: "描述如何 toodiagnose 並修正您先部署 StorSimple 時所發生的錯誤。"
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: f8352eaa-193c-42d1-8818-0b8e02d8485d
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 9a31a3cfb3be577500b226c2bc8172dd8664bad9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-storsimple-device-deployment-issues"></a>StorSimple 裝置部署問題的疑難排解
## <a name="overview"></a>概觀
本文提供對於 Microsoft Azure StorSimple 部署很有幫助的疑難排解指引。 它描述常見的問題、 可能原因和建議的步驟 toohelp 解決當您設定 StorSimple 時可能遇到的問題。 這項資訊適用於 tooboth hello StorSimple 內部部署實體裝置和 hello StorSimple 虛擬裝置。

> [!NOTE]
> 裝置組態相關問題，您可能會面臨可能是當您部署的 hello hello 裝置第一次，或就可能會導致稍後 hello 裝置可以運作。 本文著重於第一次部署問題的疑難排解。 tootroubleshoot 操作的裝置，跳過[疑難排解作業裝置問題](storsimple-troubleshoot-operational-device.md)。
> 
> 

本文也描述適用於疑難排解 StorSimple 部署的 hello 工具，並提供逐步疑難排解範例。

## <a name="first-time-deployment-issues"></a>第一次部署問題
如果遇到問題時部署您的裝置 hello 第一次，請考慮下列 hello:

* 如果您正在疑難排解實體裝置，請確定 hello 硬體確定已安裝並設定中所述[安裝 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)或[安裝 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md).
* 檢查部署的先決條件。 請確定您擁有 hello 中所述的所有 hello 資訊[部署組態檢查清單](storsimple-deployment-walkthrough.md#deployment-configuration-checklist)。
* 如果所述 hello 問題，請檢閱 hello StorSimple 版本資訊 toosee。 hello 版本資訊包含已知的安裝問題的因應措施。 

裝置在部署期間，最常見的 hello 發出表面發生該使用者執行 hello 安裝精靈時，和當他們註冊 hello 裝置透過 Windows PowerShell for StorSimple。 （您使用 Windows PowerShell for StorSimple tooregister 及設定您的 StorSimple 裝置。 如需裝置註冊的詳細資訊，請參閱 [步驟 3：透過 Windows PowerShell for StorSimple 設定和註冊裝置](storsimple-deployment-walkthrough.md#step-3-configure-and-register-the-device-through-windows-powershell-for-storsimple))。

hello 下列各節可協助您解決您在第一次設定 hello 的 hello StorSimple 裝置時遇到的問題。

## <a name="first-time-setup-wizard-process"></a>第一次執行安裝精靈程序
hello 步驟摘要說明 hello 安裝精靈程序。 如需詳細的安裝資訊，請參閱 [部署內部部署 StorSimple 裝置](storsimple-deployment-walkthrough.md)。

1. 執行 hello [Invoke-hcssetupwizard](https://technet.microsoft.com/library/dn688135.aspx) cmdlet toostart hello 安裝精靈將引導您完成 hello 剩餘步驟。 
2. 設定網路 hello: hello 安裝精靈可讓您設定 StorSimple 裝置上的 hello DATA 0 網路介面的網路設定。 這些設定包括下列 hello:
   * 虛擬 IP (VIP)、 子網路遮罩和閘道 – hello [Set-hcsnetinterface](https://technet.microsoft.com/library/dn688161.aspx) hello 背景中執行此指令程式。 它會在您的 StorSimple 裝置上設定 hello IP 位址、 子網路遮罩和閘道 hello DATA 0 網路介面。
   * 主要 DNS 伺服器 – hello [Set-hcsdnsclientserveraddress](https://technet.microsoft.com/library/dn688172.aspx) hello 背景中執行此指令程式。 它會設定您的 StorSimple 解決方案的 hello DNS 設定。
   * NTP 伺服器 – hello [Set-hcsntpclientserveraddress](https://technet.microsoft.com/library/dn688138.aspx) hello 背景中執行此指令程式。 它會設定您的 StorSimple 解決方案的 hello NTP 伺服器設定。
   * 選擇性 web proxy – hello [Set-hcswebproxy](https://technet.microsoft.com/library/dn688154.aspx) hello 背景中執行此指令程式。 它會設定並可讓您於 StorSimple 解決方案的 hello web proxy 設定。
3. 設定 hello 密碼： hello 下一個步驟是 tooset 裝置系統管理員和 StorSimple Snapshot Manager 密碼。 如果您正在更新 1，然後您將不會需要的 tooset hello StorSimple Snapshot Manager 密碼。
   
   * tooyour 裝置上的使用的 toolog hello 裝置系統管理員密碼。 hello 預設裝置密碼**Password1**。
   * 當您設定裝置 toouse StorSimple Snapshot Manager 時，才需要 hello StorSimple Snapshot Manager 密碼。 您需要 toofirst 組 hello 密碼在 hello 安裝精靈，然後您可以設定，並將它從 hello StorSimple Manager 服務的變更。 此密碼可驗證的裝置 hello 與 StorSimple Snapshot Manager。
     
     > [!IMPORTANT]
     > 密碼會註冊之前, 收集，但只在您成功註冊裝置 hello 之後套用。 如果沒有失敗 tooapply 密碼，您將會提示的 toosupply hello 密碼再次 hello 必要的密碼 （符合 hello 複雜性需求） 會收集之前。
     > 
     > 
4. 註冊的裝置 hello: hello 最後一個步驟是 tooregister hello 裝置 hello StorSimple Manager 服務在 Microsoft Azure 中執行。 hello 註冊會要求您太[取得 hello 服務註冊金鑰](storsimple-manage-service.md#get-the-service-registration-key)從 hello Azure 傳統入口網站，並在 hello 安裝精靈中提供。 Tooyou hello 裝置註冊成功之後，提供服務資料加密金鑰。 請務必的 tookeep 此加密金鑰在安全的位置，因為它會在需要 tooregister 與 hello 服務所有後續的裝置。

## <a name="common-errors-during-device-deployment"></a>裝置部署期間的常見錯誤
hello 下列資料表清單 hello 一般錯誤，您可能會遇到當您：

* 設定所需的 hello 網路設定。
* 設定 hello 選擇性的 web proxy 設定。
* 設定 hello 裝置系統管理員和 StorSimple Snapshot Manager 密碼。 
* 註冊裝置 hello。 

## <a name="errors-during-hello-required-network-settings"></a>Hello 期間發生的錯誤所需的網路設定
| 否。 | 錯誤訊息 | 可能的原因 | 建議的動作 |
| --- | --- | --- | --- |
| 1 |叫用 HcsSetupWizard： 這個命令只能 hello 作用中控制器上執行。 |組態 hello 被動控制站上執行。 |從 hello 作用中控制器執行此命令。 如需詳細資訊，請參閱 [識別裝置上的主動控制器](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device)。 |
| 2 |Invoke-HcsSetupWizard：裝置尚未就緒。 |有一些 hello DATA 0 上的網路連線問題。 |請檢查 hello DATA 0 上的實體網路連線。 |
| 3 |叫用 HcsSetupWizard： 沒有 IP 位址衝突的 hello 網路上的另一個系統 (來自 HRESULT 的例外狀況： 0x80070263)。 |提供給 DATA 0 的 hello IP 已經由另一個系統使用中。 |提供未使用的新 IP。 |
| 4 |Invoke-HcsSetupWizard：某個叢集資源失敗了 (例外狀況發生於 HRESULT：0x800713AE)。 |重複的 VIP。 提供的 hello IP 已在使用中。 |提供未使用的新 IP。 |
| 5 |Invoke-HcsSetupWizard: 無效的 IPv4 位址。 |提供的 hello IP 位址格式不正確。 |請檢查 hello 格式，並再次提供您的 IP 位址。 如需詳細資訊，請參閱 [Ipv4 定址][1]。 |
| 6 |Invoke-HcsSetupWizard：無效的 IPv6 位址。 |提供的 hello IP 位址格式不正確。 |請檢查 hello 格式，並再次提供您的 IP 位址。 如需詳細資訊，請參閱 [Ipv6 定址][2]。 |
| 7 |叫用 HcsSetupWizard： 有多個端點可用 hello 端點對應程式。 (例外狀況發生於 HRESULT：0x800706D9) |hello 叢集 」 功能無法運作。 |[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md) 以進行後續步驟。 |

## <a name="errors-during-hello-optional-web-proxy-settings"></a>Hello 選擇性的 web proxy 設定期間發生的錯誤
| 否。 | 錯誤訊息 | 可能的原因 | 建議的動作 |
| --- | --- | --- | --- |
| 1 |Invoke-HcsSetupWizard：無效的參數 (例外狀況發生於 HRESULT：0x80070057) |其中一個 hello 參數提供給 hello proxy 設定不正確。 |未提供 hello URI hello 正確格式。 使用下列格式的 hello: http://*<IP address or FQDN of hello web proxy server>*:*<TCP port number>* |
| 2 |Invoke-HcsSetupWizard：RPC 伺服器無法使用 (例外狀況發生於 HRESULT：0x800706ba) |hello 根本原因是 hello 下列其中一種：<ol><li>hello 叢集未啟動。</li><li>hello 被動控制器無法與 hello 主動控制器，並從被動控制站執行 hello 命令。</li></ol> |根據 hello 根本原因：<ol><li>[請連絡 Microsoft 支援](storsimple-contact-microsoft-support.md)toomake 確定該 hello 叢集已啟動。</li><li>從 hello 作用中控制器執行 hello 命令。 如果您想從被動控制站 hello toorun hello 命令時，您將需要 tooensure 該 hello 被動控制站可以與 hello active 控制器通訊。 您必須太[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)如果此連接已中斷。</li></ol> |
| 3 |Invoke-HcsSetupWizard：RPC 呼叫失敗 (例外狀況發生於 HRESULT：0x800706be) |叢集已關閉。 |[請連絡 Microsoft 支援](storsimple-contact-microsoft-support.md)toomake 確定該 hello 叢集已啟動。 |
| 4 |Invoke-HcsSetupWizard：找不到叢集資源 (例外狀況發生於 HRESULT：0x8007138f) |找不到 hello 叢集資源。 這個情形 hello 安裝不正確。 |您可能需要 tooreset hello 裝置 toohello 原廠預設值。 [請連絡 Microsoft 支援](storsimple-contact-microsoft-support.md)toocreate 叢集資源。 |
| 5 |Invoke-HcsSetupWizard：叢集資源不在線上 (例外狀況發生於 HRESULT：0x8007138c) |叢集資源不在線上。 |[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md) 以進行後續步驟。 |

## <a name="errors-related-toodevice-administrator-and-storsimple-snapshot-manager-passwords"></a>錯誤相關的 toodevice 系統管理員和 StorSimple Snapshot Manager 密碼
hello 預設裝置系統管理員密碼是**Password1**。 此密碼過期之後 hello 第一個登入。因此，您將需要 toouse hello 安裝程式精靈 toochange 它。 當您第一次註冊 hello 的 hello 裝置時，您必須提供新的裝置系統管理員密碼。 

如果您使用 hello Windows 伺服器主機 toomanage hello 裝置上執行的 hello StorSimple Snapshot Manager 軟體，然後您必須也提供 StorSimple Snapshot Manager 密碼在第一次登錄期間。 

請確定您的密碼符合下列需求的 hello:

* 裝置系統管理員密碼長度應介於 8 到 15 個字元。
* StorSimple Snapshot Manager 密碼長度應該是 14 或 15 個字元。
* 密碼必須包含 3 個 hello 下列 4 個字元類型： 小寫字母、 大寫字母、 數字和特殊。 
* 您的密碼無法 hello 與 hello 最後 24 個密碼相同。

此外，請注意，密碼每年，過期，而且您已成功登錄 hello 裝置之後，才可以變更。 如果 hello 註冊因為任何原因失敗，將不會變更 hello 密碼。 如需有關裝置系統管理員和 StorSimple Snapshot Manager 密碼的詳細資訊，請移太[使用 hello StorSimple Manager 服務 toochange StorSimple 密碼](storsimple-change-passwords.md)。

您可能會遇到一或多個 hello hello 裝置系統管理員和 StorSimple Snapshot Manager 密碼時，下列錯誤。

| 否。 | 錯誤訊息 | 建議的動作 |
| --- | --- | --- |
| 1 |hello 密碼超過 hello 最大長度。 |使用符合這些需求的密碼︰<ul><li>您的裝置系統管理員密碼長度必須介於 8 到 15 個字元。</li><li>StorSimple Snapshot Manager 密碼長度必須是 14 或 15 個字元。</li></ul> |
| 2 |hello 密碼不符合所需的 hello 長度。 |使用符合這些需求的密碼︰<ul><li>您的裝置系統管理員密碼長度必須介於 8 到 15 個字元。</li><li>StorSimple Snapshot Manager 密碼長度必須是 14 或 15 個字元。</lu></ul> |
| 3 |hello 密碼必須包含小寫字元。 |密碼必須包含 3 個 hello 下列 4 個字元類型： 小寫字母、 大寫字母、 數字和特殊。 請確定您的密碼符合這些需求。 |
| 4 |hello 密碼必須包含數字字元。 |密碼必須包含 3 個 hello 下列 4 個字元類型： 小寫字母、 大寫字母、 數字和特殊。 請確定您的密碼符合這些需求。 |
| 5 |hello 密碼必須包含特殊字元。 |密碼必須包含 3 個 hello 下列 4 個字元類型： 小寫字母、 大寫字母、 數字和特殊。 請確定您的密碼符合這些需求。 |
| 6 |hello 密碼必須包含 3 個 hello 下列 4 個字元類型： 大寫字母、 小寫、 數字和特殊。 |您的密碼不包含所需的 hello 類型的字元。 請確定您的密碼符合這些需求。 |
| 7 |參數與確認不相符。 |請確定您的密碼符合所有需求，且您已正確輸入它。 |
| 8 |您的密碼不符 hello 預設值。 |hello 預設密碼為*Password1*。 您需要 toochange 這個密碼登入之後 hello 第一次。 |
| 9 |您輸入的 hello 密碼與 hello 裝置密碼不符。 請重新輸入 hello 密碼。 |檢查 hello 密碼並再次輸入。 |

Hello 裝置已經註冊，但是只有在成功註冊之後會套用之前，會收集密碼。 hello 密碼復原工作流程需要 hello 裝置 toobe 註冊。 

> [!IMPORTANT]
> 一般情況下，如果嘗試 tooapply 密碼失敗，則 hello 軟體重複嘗試 toocollect hello 密碼，直到成功為止。 在罕見情況下，無法套用 hello 密碼。 在此情況下，您可以註冊的裝置 hello 並繼續進行，不過 hello 密碼將不會變更。 因為 toowhich 密碼並未變更，您會收到指示 — hello 裝置系統管理員密碼或 hello StorSimple Snapshot Manager 密碼。 如果發生這種情況，建議您變更這兩個密碼。
> 
> 

您可以重設 hello hello StorSimple Manager 服務透過 Azure 傳統入口網站中的 hello 密碼。 如需詳細資訊，請移至： 

* [變更 hello 裝置系統管理員密碼](storsimple-change-passwords.md#change-the-device-administrator-password)。
* [變更 hello StorSimple Snapshot Manager 密碼](storsimple-change-passwords.md#change-the-storsimple-snapshot-manager-password)。

## <a name="errors-during-device-registration"></a>裝置註冊期間發生錯誤
您使用執行 Microsoft Azure tooregister hello 裝置中的 hello StorSimple Manager 服務。 您可能會遇到一或多個下列問題的裝置註冊期間的 hello。

| 否。 | 錯誤訊息 | 可能的原因 | 建議的動作 |
| --- | --- | --- | --- |
| 1 |錯誤 350027： 無法以 hello StorSimple Manager tooregister hello 裝置。 | |等候幾分鐘的時間，然後再次嘗試 hello 操作。 如果 hello 問題持續發生，[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。 |
| 2 |錯誤 350013： 註冊 hello 裝置發生錯誤。 這可能是由於 tooincorrect 服務註冊金鑰。 | |請再次使用 hello 正確的服務註冊金鑰註冊 hello 裝置。 如需詳細資訊，請參閱[Get hello 服務註冊金鑰。](storsimple-manage-service.md#get-the-service-registration-key) |
| 3 |錯誤 350063： 傳遞了驗證 tooStorSimple Manager 服務，但註冊失敗。 請重試 hello 一段時間後的作業。 |此錯誤表示向 ACS 驗證已通過，但 hello 暫存器呼叫 toohello 服務失敗。 這可能是零星網路問題的結果。 |如果 hello 問題持續發生，請[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。 |
| 4 |錯誤 350049： 無法在註冊期間連線 hello 服務。 |Hello 呼叫進行 toohello 服務時，收到 web 例外狀況。 在某些情況下，這可能會修正 hello 作業稍後重試一次。 |請檢查您的 IP 位址和 DNS 名稱，然後再重試 hello 作業。 如果 hello 問題持續發生，[連絡 Microsoft 支援服務。](storsimple-contact-microsoft-support.md) |
| 5 |錯誤 350031: hello 裝置已登錄。 | |不需採取任何動作。 |
| 6 |錯誤 350016：裝置註冊失敗。 | |請確定 hello 註冊金鑰正確無誤。 |
| 7 |叫用 HcsSetupWizard： 發生錯誤時，發生註冊您的裝置。這可能是由於 tooincorrect IP 位址或 DNS 名稱。 請檢查您的網路設定，然後再試一次。 如果 hello 問題持續發生，[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)。 (錯誤 350050) |請確定您的裝置可以 ping 網路外部的 hello。 如果您沒有連線 toooutside 網路，hello 註冊可能失敗，發生下列錯誤。 這個錯誤可能是的一或多個 hello 下列組合：<ul><li>不正確的 IP</li><li>不正確的子網路</li><li>不正確的閘道</li><li>不正確的 DNS 設定</li></ul> |請參閱 hello 步驟 hello[逐步疑難排解範例](#step-by-step-storsimple-troubleshooting-example)。 |
| 8 |叫用 HcsSetupWizard: hello 目前的作業失敗，因為 tooan 內部服務錯誤 [0x1FBE2]。 請稍後重試 hello 作業。 如果 hello 問題持續發生，請連絡 Microsoft 支援服務。 |這是從服務或代理程式針對所有使用者看不見的錯誤所擲回的一般錯誤。 hello 最常見的原因可能是 hello ACS 驗證失敗。 Hello 失敗的原因可能是 hello NTP 伺服器組態問題，並在 hello 裝置上的時間未正確設定。 |更正 hello 時間 （如果有問題），然後再重試 hello 註冊作業。 如果您使用 hello 組 HcsSystem 時區命令 tooadjust hello 時區，改成大寫 hello 時區 （例如 「 太平洋標準時間 」） 中的每個字。  如果問題持續發生，請 [連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md) 以進行後續步驟。 |
| 9 |警告： 無法啟動 hello 裝置。 您的設定裝置系統管理員和 StorSimple Snapshot Manager 密碼尚未變更。 |如果 hello 註冊失敗，hello 裝置系統管理員和 StorSimple Snapshot Manager 密碼不會變更。 | |

## <a name="tools-for-troubleshooting-storsimple-deployments"></a>適用於疑難排解 StorSimple 部署的工具
StorSimple 包括數個工具，您可以使用 tootroubleshoot 您於 StorSimple 解決方案。 其中包含：

* 支援封裝和裝置記錄 
* 專為疑難排解而設計的 Cmdlet 

## <a name="support-packages-and-device-logs-available-for-troubleshooting"></a>可用來疑難排解的支援封裝和裝置記錄
支援封裝包含所有 hello 相關記錄，可以協助 hello Microsoft 支援服務團隊疑難排解裝置問題。 您可以使用 Windows PowerShell for StorSimple toogenerate 您可以在與支援人員共用加密的支援封裝。

### <a name="tooview-hello-logs-or-hello-contents-of-hello-support-package"></a>tooview hello 記錄檔或 hello hello 支援封裝的內容
1. 中所述，使用 Windows PowerShell for StorSimple toogenerate 支援封裝[建立及管理支援封裝](storsimple-create-manage-support-package.md)。
2. 下載 hello[解密指令碼](https://gallery.technet.microsoft.com/scriptcenter/Script-to-decrypt-a-a8d1ed65)儲存在用戶端電腦本機。
3. 使用此[逐步程序](storsimple-create-manage-support-package.md#edit-a-support-package)tooopen 和解密 hello 支援封裝。
4. hello 解密支援封裝記錄檔為 etw/etvx 格式。 您可以在 Windows 事件檢視器中執行下列步驟 tooview hello 這些檔案：
   
   1. 執行 hello **eventvwr**命令在您的 Windows 用戶端上。 這會啟動 hello 事件檢視器。
   2. 在 hello**動作** 窗格中，按一下 **開啟已儲存的記錄**和點 toohello etvx/etw 格式 （hello 支援封裝） 中的記錄檔。 您現在可以檢視 hello 檔案。 開啟 hello 檔案之後，您可以以滑鼠右鍵按一下，並將 hello 檔案儲存為文字。
      
      > [!IMPORTANT]
      > 您也可以使用 hello **Get-winevent** cmdlet tooopen Windows PowerShell 中的這些檔案。 如需詳細資訊，請參閱[Get-winevent](https://technet.microsoft.com/library/hh849682.aspx) hello Windows PowerShell cmdlet 參考文件中。
      > 
      > 
5. 當 hello 記錄檔開啟事件檢視器中時，尋找下列包含問題相關的 toohello 裝置設定的記錄檔的 hello:
   
   * hcs_pfconfig/Operational Log
   * hcs_pfconfig/Config
6. Hello 記錄檔中搜尋的字串 hello 安裝精靈所呼叫的相關的 toohello cmdlet。 如需這些 Cmdlet 的清單，請參閱 [第一次安裝精靈程序](#first-time-setup-wizard-process) 。 
7. 如果您不能 toofigure 出 hello hello 問題原因，您可以[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)接下來的步驟。 中的步驟使用 hello[建立支援要求](storsimple-contact-microsoft-support.md#create-a-support-request)連絡 Microsoft 支援服務尋求協助。

## <a name="cmdlets-available-for-troubleshooting"></a>可用於疑難排解的 Cmdlet
使用下列 Windows PowerShell cmdlet toodetect 連線錯誤 hello。

* `Get-NetAdapter`： 使用此 cmdlet toodetect hello 健全狀況的網路介面卡。 
* `Test-Connection`： 使用這個指令程式 toocheck hello 網路連線內部和外部 hello。
* `Test-HcsmConnection`： 使用這個指令程式 toocheck hello 連線能力的成功註冊的裝置。

如果您在您的 StorSimple 裝置上執行 Update 1，hello 下列診斷 cmdlet 也會提供。

* `Sync-HcsTime`： 使用這個指令程式 toodisplay 裝置時間和強制與 hello NTP 伺服器同步時間處理。
* `Enable-HcsPing`和`Disable-HcsPing`： 您的 StorSimple 裝置上使用這些 cmdlet tooallow hello 主機 tooping hello 網路介面。 根據預設，hello StorSimple 網路介面未回應 tooping 要求。
* `Trace-HcsRoute`：此 Cmdlet 可做為路由追蹤工具。 它會傳送 hello 方式 tooa 最終目的地的封包 tooeach 路由器經過一段時間，，然後再計算根據 hello 封包從每個躍點傳回的結果。 因為`Trace-HcsRoute`顯示 hello 程度封包遺失，在任何給定的路由器或連結，您可以找出哪些路由器或連結可能會造成網路問題。 
* `Get-HcsRoutingTable`： 使用這個指令程式 toodisplay hello 本機 IP 路由表。

## <a name="troubleshoot-with-hello-get-netadapter-cmdlet"></a>疑難排解 hello Get-netadapter cmdlet
當您設定第一次裝置部署的網路介面時，hello 硬體狀態不是用於 hello StorSimple Manager 服務 UI 因為 hello 裝置不使用 hello 服務尚未註冊。 此外，hello 硬體狀態 頁面可能不一定會正確地反映 hello 狀態 hello 裝置，特別是當影響服務同步處理的問題。 在這些情況下，您可以使用 hello `Get-NetAdapter` cmdlet toodetermine hello 健全狀況和您的網路介面狀態。

### <a name="toosee-a-list-of-all-hello-network-adapters-on-your-device"></a>toosee 一份您的裝置上的所有 hello 網路介面卡
1. 啟動 Windows PowerShell for StorSimple，然後鍵入 `Get-NetAdapter`。 
2. 使用的 hello hello 輸出`Get-NetAdapter`指令程式，並遵循的指導方針 toounderstand hello hello 網路介面的狀態。
   
   * 如果 hello 介面狀況良好且已啟用，hello **ifIndex**狀態會顯示為**向上**。
   * 如果 hello 介面狀況良好，但尚未實際連線 （透過網路纜線），hello **ifIndex**會顯示為**已停用**。
   * 如果 hello 介面狀況良好但未啟用，hello **ifIndex**狀態會顯示為**NotPresent**。
   * 如果 hello 介面不存在，它不會出現在這份清單。 hello StorSimple Manager 服務 UI 仍將顯示此介面處於失敗狀態。

如需有關如何 toouse 這個指令程式，跳過[GetNetAdapter](https://technet.microsoft.com/library/jj130867.aspx) hello Windows PowerShell cmdlet 參考中。 

hello 下列各節說明來自 hello 輸出範例`Get-NetAdapter`cmdlet。 

 在這些範例中，控制器 0 已 hello 被動控制站，而且已設定，如下所示：

* DATA 0、 DATA 1、 DATA 2 和 DATA 3 網路介面存在於 hello 裝置。
* DATA 4 和 DATA 5 網路介面卡沒有出現。因此，它們並未列在 hello 輸出中。
* DATA 0 已啟用。

控制器 1 的 hello 主動控制器，而且已設定，如下所示：

* DATA 0、 DATA 1、 DATA 2、 3、 DATA 4 和 DATA 5 網路介面存在於 hello 裝置。
* DATA 0 已啟用。

**範例輸出 - 控制站 0**

hello 以下是從控制器 0 （hello 被動控制站） 的 hello 輸出。 未連接 DATA 1、DATA 2 及 DATA 3。 DATA 4 和 DATA 5 未列出，因為它們不會出現在 hello 裝置上。 

     Controller0>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter #2     17       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter        14       NotPresent
     Ethernet 2           HCS VNIC                                    13       Up
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up


**範例輸出 - 控制站 1**

hello 以下是從控制器 1 （hello 作用中控制器） 的 hello 輸出。 只有 hello 的 DATA 0 網路介面 hello 裝置上的設定和使用。

     Controller1>Get-NetAdapter
     Name                 InterfaceDescription                        ifIndex  Status
     ------               --------------------                        -------  ----------
     DATA3                Mellanox ConnectX-3 Ethernet Adapter        18       NotPresent
     DATA2                Mellanox ConnectX-3 Ethernet Adapter #2     19       NotPresent
     DATA1                Intel(R) 82574L Gigabit Network Co...#2     16       NotPresent
     DATA0                Intel(R) 82574L Gigabit Network Conn...     15       Up
     Ethernet 2           HCS VNIC                                    13       Up
     DATA5                Intel(R) Gigabit ET Dual Port Server...     14       NotPresent
     DATA4                Intel(R) Gigabit ET Dual Port Serv...#2     17       NotPresent


## <a name="troubleshoot-with-hello-test-connection-cmdlet"></a>疑難排解 hello Test-connection cmdlet
您可以使用 hello `Test-Connection` cmdlet toodetermine StorSimple 裝置是否可連接 toohello 網路外部。 如果所有 hello 網路參數，包括 hello DNS 都已正確設定 hello 安裝精靈 中，您可以使用 hello `Test-Connection` cmdlet tooping hello 網路，例如 outlook.com 之外的已知位址。 

如果 ping 已停用，您應該啟用這個指令程式 ping tootroubleshoot 連線問題。

請參閱 hello hello 中的下列輸出範例`Test-Connection`cmdlet。 

> [!NOTE]
> 在 hello 第一個範例中，使用不正確的 DNS 設定 hello 裝置。 在 hello 第二個範例中，hello DNS 是正確的。
> 
> 

**範例輸出 - 不正確的 DNS**

在下列範例的 hello，沒有表示 DNS 未解析該 hello hello IPV4 和 IPV6 位址的輸出。 這表示沒有任何外部網路的連線能力 toohello，正確的 DNS 需要 toobe 提供。 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com
     HCSNODE0      outlook.com

**範例輸出 - 正確的 DNS**

在下列範例的 hello，hello DNS 傳回 hello 指出 DNS 已正確設定該 hello 的 IPV4 位址。 這可確認沒有網路外部連線能力 toohello。 

     Source        Destination     IPV4Address      IPV6Address
     ------        -----------     -----------      -----------
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194
     HCSNODE0      outlook.com     132.245.92.194

## <a name="troubleshoot-with-hello-test-hcsmconnection-cmdlet"></a>疑難排解 hello Test-hcsmconnection cmdlet
使用 hello`Test-HcsmConnection`指令程式的裝置已連接 tooand 向 StorSimple Manager 服務。 這個指令程式可協助您確認 hello 已註冊的裝置與 hello 對應 StorSimple Manager 服務之間的連線。 您可以在 Windows PowerShell for StorSimple 上執行這個命令。 

### <a name="toorun-hello-test-hcsmconnection-cmdlet"></a>toorun hello Test-hcsmconnection cmdlet
1. 請確定該 hello 裝置已註冊。
2. 檢查 hello 裝置狀態。 如果 hello 裝置停用時，處於維護模式，或離線，您可能會看到下列錯誤 hello: 
   
   * ErrorCode.CiSDeviceDecommissioned – 這表示該 hello 裝置停用。
   * ErrorCode.DeviceNotReady – 這表示該 hello 裝置處於維護模式。
   * ErrorCode.DeviceNotReady – 這表示該 hello 裝置不在線上。
3. 請確認該 hello StorSimple Manager 服務正在執行 (使用 hello [Get-clusterresource](https://technet.microsoft.com/library/ee461004.aspx) cmdlet)。 如果 hello 服務未在執行中，您可能會看到下列錯誤 hello:
   
   * ErrorCode.CiSApplianceAgentNotOnline
   * ErrorCode.CisPowershellScriptHcsError - 這表示在執行 Get-ClusterResource 時發生例外狀況。
4. 請檢查 hello 存取控制服務 (ACS) 權杖。 如果它擲回 web 例外狀況，可能是 hello 閘道問題、 遺漏 proxy 驗證、 不正確的 DNS，或發生驗證錯誤的結果。 您可能會看到下列錯誤 hello:
   
   * ErrorCode.CiSApplianceGateway – 這表示 HttpStatusCode.BadGateway 例外狀況： hello 名稱解析程式服務無法解析 hello 主機名稱。 
   * ErrorCode.CiSApplianceProxy – 這表示 HttpStatusCode.ProxyAuthenticationRequired 例外狀況 （HTTP 狀態碼 407）： hello 用戶端無法向 hello proxy 伺服器。 
   * ErrorCode.CiSApplianceDNSError – 這表示 WebExceptionStatus.NameResolutionFailure 例外狀況： hello 名稱解析程式服務無法解析 hello 主機名稱。
   * ErrorCode.CiSApplianceACSError – 這表示 hello 服務傳回驗證錯誤，但沒有連線。
     
     如果服務未擲回 Web 例外狀況，請檢查導致 ErrorCode.CiSApplianceFailure 產生的錯誤。 這表示該 hello 應用裝置失敗。
5. 檢查 hello 雲端服務連線。 如果 hello 服務擲回 web 例外狀況，您可能會看到下列錯誤 hello:
   
   * ErrorCode.CiSApplianceGateway – 這表示 HttpStatusCode.BadGateway 例外狀況： 中繼 proxy 伺服器收到不正確的要求，從另一個 proxy 或從 hello 原始伺服器。
   * ErrorCode.CiSApplianceProxy – 這表示 HttpStatusCode.ProxyAuthenticationRequired 例外狀況 （HTTP 狀態碼 407）： hello 用戶端無法向 hello proxy 伺服器。 
   * ErrorCode.CiSApplianceDNSError – 這表示 WebExceptionStatus.NameResolutionFailure 例外狀況： hello 名稱解析程式服務無法解析 hello 主機名稱。
   * ErrorCode.CiSApplianceACSError – 這表示 hello 服務傳回驗證錯誤，但沒有連線。
     
     如果服務未擲回 Web 例外狀況，請檢查導致 ErrorCode.CiSApplianceSaasServiceError 發生的錯誤。 這表示 hello StorSimple Manager 服務發生問題。
6. 檢查 Azure 服務匯流排連線。 ErrorCode.CiSApplianceServiceBusError 表示該 hello 裝置無法連線 toohello Service Bus。

hello 記錄檔 CiSCommandletLog0Curr.errlog 和 cisagentsvc0curr.errlog 將詳細資訊，例如例外狀況詳細資料。 

如需有關如何 toouse hello cmdlet 的詳細資訊，請移至太[Test-hcsmconnection](https://technet.microsoft.com/library/dn715782.aspx) hello Windows PowerShell 中的參考文件。

> [!IMPORTANT]
> 您可以執行這個指令程式使用中的 hello 和 hello 被動控制器。 
> 
> 

請參閱 hello hello 中的下列輸出範例`Test-HcsmConnection`cmdlet。 

**範例輸出 – 執行 StorSimple 版本的已成功註冊裝置 (2014 年 7 月)**

hello 第一個範例是從已成功向 StorSimple Manager 服務的 hello 和沒有連線問題的裝置。 

     Controller1>Test-HcsmConnection -verbose
     Checking device state  ... Success.
     Device registered successfully
     Checking device authentication.  ... This operation will take few minutes toocomplete....
     Checking device authentication.  ... Success.
     Checking connectivity from device tooStorSimple Manager service.  ... This operation will take few minutes toocomplete....
     Checking connectivity from device tooStorSimple Manager service.  ... Success.
     Checking connectivity from StorSimple Manager service tooStorSimple device. .... Success.
     Controller1>

**範例輸出 – 執行 StorSimple Update 1 的已成功註冊裝置**

如果您在您的 StorSimple 裝置上執行 Update 1，您就不需要 toorun 它與 hello verbose 參數。

      Controller1>Test-HcsmConnection

      Checking device registration state  ... Success
      Device registered successfully

      Checking primary NTP server [time.windows.com] ... Success

      Checking web proxy  ... NOT SET

      Checking primary IPv4 DNS server [10.222.118.154] ... Success
      Checking primary IPv6 DNS server  ... NOT SET
      Checking secondary IPv4 DNS server [10.222.120.24] ... Success
      Checking secondary IPv6 DNS server  ... NOT SET

      Checking device online  ... Success

      Checking device authentication  ... This will take a few minutes.
      Checking device authentication  ... Success

      Checking connectivity from device tooservice  ... This will take a few minutes.

      Checking connectivity from device tooservice  ... Success

      Checking connectivity from service toodevice  ... Success

      Checking connectivity tooMicrosoft Update servers  ... Success
      Controller1>

**範例輸出 – 執行 StorSimple 版本的離線裝置 (2014 年 7 月)**

這個範例會從裝置中的狀態為**離線**hello Azure 傳統入口網站中。

     Checking device state: Success 
     Device is registered successfully 
     Checking connectivity from device tooSaaS.. Failure

hello 裝置無法連線使用 hello 目前的 web proxy 組態。 這可能是 hello web proxy 組態的問題或網路連線問題。 在此情況下，您應該確定 Web Proxy 設定正確無誤，而且您的 Web Proxy 伺服器在線上且可連線。 

## <a name="troubleshoot-with-hello-sync-hcstime-cmdlet"></a>疑難排解 hello 同步 HcsTime cmdlet
使用這個指令程式 toodisplay hello 裝置時間。 如果 hello 裝置時間與 hello NTP 伺服器的位移，然後您可以使用這個指令程式 tooforce-hello 時間與 NTP 伺服器同步。 如果 hello 裝置與 NTP 伺服器之間的 hello 位移為 5 分鐘以上，您會看到一個警告。 如果 hello 位移超過 15 分鐘，然後 hello 裝置會離線。 您仍然可以使用這個指令程式 tooforce 時間同步。不過，如果 hello 位移超過 15 小時，然後將不會無法 tooforce 同步 hello 時間，並會顯示錯誤訊息。

**範例輸出 – 已使用 Sync-HcsTime 執行的強制同步時間作業**

     Controller0>Sync-HcsTime
     hello current device time is 4/24/2015 4:05:40 PM UTC.

     Time difference between NTP server and appliance is 00.0824069 seconds. Do you want tooresync time with NTP server?
     [Y] Yes [N] No (Default is "Y"): Y
     Controller0>

## <a name="troubleshoot-with-hello-enable-hcsping-and-disable-hcsping-cmdlets"></a>使用 hello 啟用 HcsPing 和停用 HcsPing cmdlet 進行疑難排解
使用這些 cmdlet tooensure，hello 在裝置上的網路介面回應 tooICMP ping 要求。 根據預設 hello StorSimple 網路介面未回應 tooping 要求。 如果您的裝置在線上且可使用這個指令程式是最簡單方式 tooknow hello。  

**範例輸出 – 啟用 HcsPing 和停用 HcsPing**

     Controller0>
     Controller0>Enable-HcsPing
     Successfully enabled ping.
     Controller0>
     Controller0>
     Controller0>Disable-HcsPing
     Successfully disabled ping.
     Controller0>

## <a name="troubleshoot-with-hello-trace-hcsroute-cmdlet"></a>疑難排解 hello 追蹤 HcsRoute cmdlet
此 Cmdlet 可做為路由追蹤工具。 它會傳送 hello 方式 tooa 最終目的地的封包 tooeach 路由器經過一段時間，，然後再計算根據 hello 封包從每個躍點傳回的結果。 因為 hello cmdlet 會顯示在任何給定的路由器或連結的封包遺失的 hello 程度，您可以找出哪些路由器或連結可能會造成網路問題。

**範例輸出顯示方式 tootrace hello 與追蹤 HcsRoute 封包的路由**

     Controller0>Trace-HcsRoute -Target 10.126.174.25

     Tracing route toocontoso.com [10.126.174.25]
     over a maximum of 30 hops:
       0  HCSNode0 [10.126.173.90]
       1  contoso.com [10.126.174.25]

     Computing statistics for 25 seconds...
                 Source tooHere   This Node/Link
     Hop  RTT    Lost/Sent = Pct  Lost/Sent = Pct  Address
       0                                           HCSNode0 [10.126.173.90]
                                     0/ 100 =  0%   |
       1    0ms     0/ 100 =  0%     0/ 100 =  0%  contoso.com
      [10.126.174.25]

     Trace complete.

## <a name="troubleshoot-with-hello-get-hcsroutingtable-cmdlet"></a>疑難排解 hello Get HcsRoutingTable cmdlet
StorSimple 裝置的使用這個指令程式 tooview hello 路由表。 路由表是一組規則，可以協助您判斷經由網際網路通訊協定 (IP) 傳輸的資料封包會將被導向的位置。 

hello 路由表顯示 hello 介面和 hello 路由 hello 資料 toohello 指定閘道的網路。 同時也提供 hello 路由公制是 hello 決策者的 hello 採取路徑 tooreach 特定目的地。 hello 低 hello 路由公制，hello 高 hello 的喜好設定。 

例如，如果您有 2 的網路介面 DATA 2 和 DATA 3，已連線 toohello 網際網路。 如果 hello 路由度量資料 2 和 DATA 3 會分別為 15 和 261、 DATA 2 與 hello 較低的路由公制是會以 hello 慣用的介面使用 tooreach hello 網際網路。

如果您在您的 StorSimple 裝置上執行 Update 1，您的 DATA 0 網路介面具有 hello hello 雲端流量的最高喜好設定。 這表示，即使有其他具備雲端功能的介面，hello 雲端流量就會路由傳送到 DATA 0。 

如果您要執行 hello`Get-HcsRoutingTable`但未指定任何參數 （做為 hello 下列範例所示)，hello cmdlet 的 cmdlet 會輸出 IPv4 和 IPv6 路由表。 或者，您可以指定`Get-HcsRoutingTable -IPv4`或`Get-HcsRoutingTable -IPv6`tooget 相關的路由表。

      Controller0>
      Controller0>Get-HcsRoutingTable
      ===========================================================================
      Interface List
       14...00 50 cc 79 63 40 ......Intel(R) 82574L Gigabit Network Connection
       12...02 9a 0a 5b 98 1f ......Microsoft Failover Cluster Virtual Adapter
       13...28 18 78 bc 4b 85 ......HCS VNIC
        1...........................Software Loopback Interface 1
       21...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #2
       22...00 00 00 00 00 00 00 e0 Microsoft ISATAP Adapter #3
      ===========================================================================

      IPv4 Route Table
      ===========================================================================
      Active Routes:
      Network Destination        Netmask          Gateway       Interface  Metric
                0.0.0.0          0.0.0.0  192.168.111.100  192.168.111.101     15
              127.0.0.0        255.0.0.0         On-link         127.0.0.1    306
              127.0.0.1  255.255.255.255         On-link         127.0.0.1    306
        127.255.255.255  255.255.255.255         On-link         127.0.0.1    306
            169.254.0.0      255.255.0.0         On-link     169.254.1.235    261
          169.254.1.235  255.255.255.255         On-link     169.254.1.235    261
        169.254.255.255  255.255.255.255         On-link     169.254.1.235    261
          192.168.111.0    255.255.255.0         On-link   192.168.111.101    266
        192.168.111.101  255.255.255.255         On-link   192.168.111.101    266
        192.168.111.255  255.255.255.255         On-link   192.168.111.101    266
              224.0.0.0        240.0.0.0         On-link         127.0.0.1    306
              224.0.0.0        240.0.0.0         On-link     169.254.1.235    261
              224.0.0.0        240.0.0.0         On-link   192.168.111.101    266
        255.255.255.255  255.255.255.255         On-link         127.0.0.1    306
        255.255.255.255  255.255.255.255         On-link     169.254.1.235    261
        255.255.255.255  255.255.255.255         On-link   192.168.111.101    266
      ===========================================================================
      Persistent Routes:
        Network Address          Netmask  Gateway Address  Metric
                0.0.0.0          0.0.0.0  192.168.111.100       5
      ===========================================================================

      IPv6 Route Table
      ===========================================================================
      Active Routes:
       If Metric Network Destination      Gateway
        1    306 ::1/128                  On-link
       13    276 fd99:4c5b:5525:d80b::/64 On-link
       13    276 fd99:4c5b:5525:d80b::1/128
                                          On-link
       13    276 fd99:4c5b:5525:d80b::3/128
                                          On-link
       13    276 fe80::/64                On-link
       12    261 fe80::/64                On-link
       13    276 fe80::17a:4eba:7c80:727f/128
                                          On-link
       12    261 fe80::fc97:1a53:e81a:3454/128
                                          On-link
        1    306 ff00::/8                 On-link
       13    276 ff00::/8                 On-link
       12    261 ff00::/8                 On-link
       14    266 ff00::/8                 On-link
      ===========================================================================
      Persistent Routes:
        None

      Controller0>

## <a name="step-by-step-storsimple-troubleshooting-example"></a>StorSimple 逐步疑難排解範例
hello 下列範例顯示逐步疑難排解的 StorSimple 部署。 在 hello 範例案例中，裝置註冊失敗，錯誤訊息，指出 hello 網路設定或 hello DNS 名稱不正確。

hello 傳回的錯誤訊息如下：

     Invoke-HcsSetupWizard: An error has occurred while registering hello device. This could be due tooincorrect IP address or DNS name. Please check your network settings and try again. If hello problems persist, contact Microsoft Support.
     +CategoryInfo: Not specified
     +FullyQualifiedErrorID: CiSClientCommunicationErros, Microsoft.HCS.Management.PowerShell.Cmdlets.InvokeHcsSetupWizardCommand

hello 錯誤可能被因 hello 下列任何一項：

* 不正確的硬體安裝
* 故障的網路介面
* 不正確的 IP 位址、子網路遮罩、閘道、主要 DNS 伺服器或 Web Proxy
* 不正確的註冊金鑰
* 不正確的防火牆設定

### <a name="toolocate-and-fix-hello-device-registration-problem"></a>toolocate 並修正 hello 裝置註冊問題
1. 請檢查您的裝置設定： 在 hello 主動控制站上執行`Invoke-HcsSetupWizard`。
   
   > [!NOTE]
   > hello 作用中控制器上必須執行 hello 安裝精靈。 您所連接的 toohello 主動控制器，看看 hello hello 序列主控台中顯示的橫幅 tooverify。 hello 橫幅指出您是否已連線的 toocontroller 0 或控制器 1，以及 hello 控制器是主動或被動。 如需詳細資訊，請移至太[識別您的裝置上的主動控制站](storsimple-controller-replacement.md#identify-the-active-controller-on-your-device)。
   > 
   > 
2. 請確定該 hello 裝置的纜線連接正確： 檢查 hello 網路纜線 hello 裝置背上。 hello 纜線是特定 toohello 裝置模型。 如需詳細資訊，請移至太[安裝 StorSimple 8100 裝置](storsimple-8100-hardware-installation.md)或[安裝 StorSimple 8600 裝置](storsimple-8600-hardware-installation.md)。
   
   > [!NOTE]
   > 如果您使用的 10 GbE 網路連接埠，您必須提供 QSFP 對 SFP 介面卡和 SFP 纜線 toouse hello。 如需詳細資訊，請參閱 hello[的纜線、 交換器以及收發器建議 hello 10 GbE 連接埠清單](storsimple-supported-hardware-for-10-gbe-network-interfaces.md)。
   > 
   > 
3. 請確認 hello hello 網路介面的健全狀況：
   
   * 使用 DATA 0 hello Get-netadapter cmdlet toodetect hello 健全狀況的 hello 網路介面卡。 
   * 如果 hello 連結沒有運作，hello **ifindex**狀態會指出該 hello 介面已關閉。 然後您必須在 hello 連接埠 toohello 應用裝置和 toohello 交換器 toocheck hello 網路連線。 您也需要 toorule 出損壞的纜線。 
   * 如果您懷疑該 hello DATA 0 連接埠 hello 作用中控制器上的失敗時，您可以確認此連接 toohello DATA 0 連接埠控制器 1 上。 tooconfirm，hello 網路纜線中斷從控制器 0 的 hello 裝置背面的 hello、 連線 hello 纜線 toocontroller 1，並接著執行一次 hello Get-netadapter cmdlet。 
     如果 hello DATA 0 連接埠控制站上的失敗，[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)接下來的步驟。 在您的系統上，您可能需要 tooreplace hello 控制站。
4. 請確認 hello 連線 toohello 交換器：
   
   * 請確定控制器 0 及控制器 1 中將主要機箱上的 DATA 0 網路介面位於 hello 相同子網路。 
   * 請檢查 hello 集線器或路由器。 一般而言，您應該連接這兩個控制器 toohello 相同的集線器或路由器。 
   * 請確定您用於 hello 連線 hello 參數，其 DATA 0 hello 中這兩個控制站相同的 vLAN。
5. 排除任何使用者錯誤：
   
   * 再次執行 hello 安裝精靈 (執行**Invoke-hcssetupwizard**)，然後輸入 hello 再次值 toomake 確定沒有任何錯誤。 
   * 確認 hello 註冊金鑰。 hello 相同的註冊金鑰可以是多個裝置 tooa StorSimple Manager 服務使用的 tooconnect。 使用中的 hello 程序[Get hello 服務註冊金鑰](storsimple-manage-service.md#get-the-service-registration-key)您使用的 tooensure hello 正確的註冊金鑰。
     
     > [!IMPORTANT]
     > 如果您有多個服務執行時，您將需要 tooensure 該 hello 註冊金鑰 hello 適當的服務是使用的 tooregister hello 裝置。 如果您擁有 hello 錯誤 StorSimple Manager 服務註冊裝置，您將需要太[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)接下來的步驟。 您可能必須 tooperform hello 裝置 （這可能會導致資料遺失） 的原廠重設 toothen 連接 toohello 能用於服務。
     > 
     > 
6. 使用您擁有網路外部連線能力 toohello hello Test-connection cmdlet tooverify。 如需詳細資訊，請移至太[hello Test-connection cmdlet 與疑難排解](#troubleshoot-with-the-test-connection-cmdlet)。
7. 檢查防火牆干擾。 如果您已確認該 hello 虛擬 IP (VIP)、 子網路、 閘道和 DNS 設定都正確，您仍看見連線問題，然後很可能您的防火牆封鎖裝置和網路外部的 hello 之間的通訊。 您需要 tooensure 連接埠 80 和 443，位於您的 StorSimple 裝置供連出通訊。 如需詳細資訊，請參閱 [StorSimple 裝置的網路需求](storsimple-system-requirements.md#networking-requirements-for-your-storsimple-device)。
8. 查看 hello 記錄檔。 跳過[支援封裝和裝置記錄檔來疑難排解](#support-packages-and-device-logs-available-for-troubleshooting)。
9. 如果 hello 上述步驟無法解決 hello 問題[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)以取得協助。

## <a name="next-steps"></a>後續步驟
[深入了解如何操作的裝置 tootroubleshoot](storsimple-troubleshoot-operational-device.md)。

<!--Link references-->

[1]: https://technet.microsoft.com/library/dd379547(v=ws.10).aspx
[2]: https://technet.microsoft.com/library/dd392266(v=ws.10).aspx 
