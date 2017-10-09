---
title: "已部署的 StorSimple 裝置 aaaTroubleshoot |Microsoft 文件"
description: "描述如何 toodiagnose 並修正目前已部署且可運作的 StorSimple 裝置發生的錯誤。"
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: ea5d89ae-e379-423f-b68b-53785941d9d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 05/16/2016
ms.author: v-sharos
ms.openlocfilehash: b48433055e05e3fb27575b88dca9f6b23c649ca2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="troubleshoot-an-operational-storsimple-device"></a>可運作的 StorSimple 裝置疑難排解
## <a name="overview"></a>概觀
本文提供實用的疑難排解指導方針，可用來解決在部署 StorSimple 裝置且可運作之後您可能遇到的問題。 它描述常見的問題、 可能原因和解決執行 Microsoft Azure StorSimple 時可能遇到的問題的建議的步驟 toohelp。 這項資訊適用於 tooboth hello StorSimple 內部部署實體裝置和 hello StorSimple 虛擬裝置。

在 hello 本文，您可以找到的 Microsoft Azure StorSimple 作業期間可能會遇到的錯誤碼清單結尾，步驟以及您可以採取 tooresolve hello 錯誤。 

## <a name="setup-wizard-process-for-operational-devices"></a>適用於可運作裝置的安裝精靈程序
您使用 hello 安裝精靈 ([Invoke-hcssetupwizard][1]) toocheck hello 裝置設定，並採取修正動作，如有必要。

當您在之前設定並正常運作的裝置上執行 hello 安裝精靈時，hello 程序流程會不同。 您可以變更下列項目只有 hello:

* IP 位址、子網路遮罩及閘道器
* 主要 DNS 伺服器
* 主要 NTP 伺服器
* 選用的 Web Proxy 設定

hello 安裝精靈不會執行 hello 作業相關的 toopassword 集合與裝置註冊。

## <a name="errors-that-occur-during-subsequent-runs-of-hello-setup-wizard"></a>Hello 安裝精靈的後續執行期間發生的錯誤
hello 下表描述作業的裝置上執行 hello 安裝精靈時，可能會遇到的 hello 錯誤，可能會造成 hello 錯誤和建議的動作 tooresolve 它們。 

| 否。 | 錯誤訊息或情況 | 可能的原因 | 建議的動作 |
|:--- |:--- |:--- |:--- |
| 1 |錯誤 350032：此裝置已經停用。 |如果您已停用裝置上執行 hello 安裝精靈，您會看到這個錯誤。 |[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md) 以進行後續步驟。 已停用的裝置無法處於執行狀態。 Hello 裝置可以再次啟用前，可能需要原廠重設。 |
| 2 |Invoke-HcsSetupWizard：ERROR_INVALID_FUNCTION (發生例外狀況於 HRESULT：0x80070001) |hello DNS 伺服器更新失敗。 DNS 設定為全域設定，而且會套用於所有 hello 啟用網路介面。 |啟用 hello 介面並重新套用 hello DNS 設定。 這可能會中斷其他啟用的介面的 hello 網路，因為這些設定是全域設定。 |
| 3 |hello 裝置出現 toobe 線上 hello StorSimple Manager 服務入口網站中的，但是當您嘗試 toocomplete hello 最小安裝，並儲存 hello 組態，hello 作業失敗。 |初始安裝期間，hello web proxy 未設定，即使已備妥實際的 proxy 伺服器。 |使用 hello [Test-hcsmconnection cmdlet] [ 2] toolocate hello 錯誤。 [請連絡 Microsoft 支援](storsimple-contact-microsoft-support.md)是否無法 toocorrect hello 問題。 |
| 4 |叫用 HcsSetupWizard： 值不在預期的 hello 範圍內。 |這個錯誤是因為不正確的子網路遮罩而引發。 可能的原因： <ul><li> hello 子網路遮罩已遺漏或空白。</li><li>hello Ipv6 首碼格式不正確。</li><li>hello 介面具備雲端功能，但 hello 閘道已遺失或不正確。</li></ul>請注意，DATA 0 自動具備雲端功能是否透過 hello 安裝精靈進行設定。 |toodetermine hello 問題，請使用子網路 0.0.0.0 或 256.256.256.256，，，然後查看 hello 輸出。 視需要的 hello 子網路遮罩、 閘道和 Ipv6 首碼輸入正確的值。 |

## <a name="error-codes"></a>錯誤碼
錯誤以數字順序列出。

| 錯誤號碼 | 錯誤文字或描述 | 建議的使用者動作 |
|:--- |:--- |:--- |
| 10502 |存取儲存體帳戶時發生錯誤。 |請等候幾分鐘，然後再次嘗試。 如果 hello 錯誤持續發生，請連絡 Microsoft 支援取得後續步驟。 |
| 40017 |hello 備份作業失敗，因為 hello 裝置上找不到 hello 備份原則中指定的磁碟區。 |重試 hello 備份作業，如果 hello 錯誤持續發生，請連絡 Microsoft 支援服務。 後續步驟。 |
| 40018 |hello 備份作業失敗，因為無 hello hello 備份原則中指定的磁碟區上找不到 hello 裝置。 |重試 hello 備份作業，如果 hello 錯誤持續發生，請連絡 Microsoft 支援服務。 後續步驟。 |
| 390061 |hello 系統是忙碌或無法使用。 |請等候幾分鐘，然後再次嘗試。 如果 hello 錯誤持續發生，請連絡 Microsoft 支援取得後續步驟。 |
| 390143 |發生錯誤碼為 390143 的錯誤。 (未知的錯誤。) |如果 hello 錯誤持續發生，請連絡 Microsoft 支援以取得後續步驟。 |

## <a name="next-steps"></a>後續步驟
如果您無法 tooresolve hello 問題，[連絡 Microsoft 支援服務](storsimple-contact-microsoft-support.md)以取得協助。 

[1]: https://technet.microsoft.com/en-us/%5Clibrary/Dn688135(v=WPS.630).aspx
[2]: https://technet.microsoft.com/en-us/%5Clibrary/Dn715782(v=WPS.630).aspx
