---
title: "aaaUse Azure 資訊安全中心建議 tooenhance 安全性 |Microsoft 文件"
description: " 了解 toouse 安全性原則和建議 Azure 資訊安全中心 toohelp 降低安全性攻擊。 "
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
ms.date: 05/08/2017
ms.author: terrylan
ms.openlocfilehash: bd314350a5abfceea3e171f2e1b55afe4549c1b1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="use-azure-security-center-recommendations-tooenhance-security"></a>使用 Azure 資訊安全中心建議 tooenhance 安全性
您可以設定安全性原則，然後實作 hello Azure 資訊安全中心所提供的建議，以減少 hello 機會的重大的安全性事件。 本文章將示範如何 toouse 安全性原則和建議的資訊安全中心 toohelp 降低安全性攻擊。

> [!NOTE]
> 這篇文章是根據 hello 角色和概念，hello 資訊安全中心[規劃及作業指南](security-center-planning-and-operations-guide.md)。 它是個不錯的主意 tooreview hello 規劃指南，然後再繼續。
>
>

## <a name="managing-security-recommendations"></a>管理安全性建議
安全性原則定義 hello 組 hello 指定訂用帳戶或資源群組中資源的建議使用的控制項。 資訊安全中心，您可以定義原則根據 tooyour 公司的安全性需求。 詳細資訊，請參閱 toolearn[設定安全性原則資訊安全中心](security-center-policies.md)。

資源群組的安全性原則被繼承自 hello 訂用帳戶層級。

![安全性原則繼承][1]

如果您需要特定的資源群組中的自訂原則，您可以停用 hello 資源群組中的繼承。 toodisable，hello 安全性原則 刀鋒視窗上設定繼承 tooUnique 和自訂的資訊安全中心會顯示建議的 hello 控制項。

比方說，如果您有不需要 hello SQL Database 的透明資料加密 (TDE) 原則的工作負載時，關閉 hello hello 訂用帳戶層級的原則，並只有在需要 SQL TDE 的地方 hello 資源群組中啟用它。

> [!NOTE]
> 如果沒有訂用帳戶層級的原則與資源群組層級原則之間的衝突，會優先 hello 資源群組層級原則。
>
>

資訊安全中心會分析您的 Azure 資源 hello 安全性狀態。 當資訊安全中心識別潛在的安全性漏洞時，它會建立 hello 安全性原則中設定的 hello 控制項為基礎的建議。 hello 建議會引導您完成設定所需的 hello 安全性控制項的 hello 程序。

資訊安全中心目前的原則建議著重於系統更新、作業系統設定、子網路和虛擬機器 (VM) 上的網路安全性群組、SQL Database 稽核、SQL Database TDE 和 Web 應用程式防火牆。 Hello 最新的資訊安全中心建議涵蓋範圍，請參閱[管理資訊安全中心的安全性建議](security-center-recommendations.md)。

## <a name="scenario"></a>案例
這個案例顯示如何 toouse 資訊安全中心 toohelp 減少 hello 機會重大的安全性事件的監視資訊安全中心建議及採取動作。 hello 案例使用 hello 虛構公司 Contoso，而角色中呈現 hello 資訊安全中心[規劃及作業指南](security-center-planning-and-operations-guide.md#security-roles-and-access-controls)。 hello 角色代表個人和小組可能會使用資訊安全中心 tooperform 不同安全性相關的工作。 hello 角色如下：

![案例角色][2]

Contoso 最近移轉其內部部署資源 tooAzure 部分。 Contoso 想 tooimplement 和維護減少其資源 hello 雲端中的弱點可能會 tooa 安全性攻擊的保護。

## <a name="recommended-solution"></a>建議的解決方案
方案是 toouse 資訊安全中心 tooprevent 和偵測安全性弱點。 Contoso 有存取 tooSecurity 中心透過其 Azure 訂用帳戶。 hello[免費層](security-center-pricing.md)的資訊安全中心會自動啟用上所有的 Azure 訂用帳戶，且其訂用帳戶中所有 Vm 上啟用資料收集。

任職於 Contoso IT 安全部門的 David 使用資訊安全中心設定**安全性原則**。 資訊安全中心會分析 hello Contoso 的 Azure 資源安全性狀態。 當資訊安全中心識別潛在的安全性漏洞時，它會建立**建議**hello 安全性原則中設定的 hello 控制項為基礎。

雲端工作負載擁有者 Jeff 負責根據 Contoso 的安全性原則，實作和維護防護措施。 Jeff 可以監視由資訊安全中心 tooapply 保護 hello 建議。 hello 建議引導 Jeff 完成 hello 程序設定所需的 hello 安全性控制項。

中的 Jeff tooimplement 順序和維護保護，避免安全性弱點，他必須：

- 監視資訊安全中心提供的安全性建議
- 評估安全性建議，並決定是否應該套用或解除
- 套用安全性建議

讓我們遵循 Jeff 的步驟 toosee 他使用方式的資訊安全中心建議 tooguide 他透過設定控制項 tooeliminate 安全性弱點的 hello 程序。

## <a name="how-tooimplement-this-solution"></a>如何 tooimplement 此解決方案
Jeff 登入太[Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)和開啟 hello 資訊安全中心主控台。 監視活動其每日的一部分，他會檢查 toosee 是否有安全性建議執行下列步驟的 hello:

1. Jeff 選取 hello**建議**磚 tooopen hello**建議**刀鋒視窗。
   ![選取 hello 建議磚][3]
2. Jeff 檢閱 hello 建議事項的清單。 他會看到資訊安全中心提供建議的優先順序，從最高優先權 toolowest 優先權 hello 清單。 他決定 tooaddress hello 清單上的優先建議。 他選取**安裝 Endpoint Protection**上 hello**建議**刀鋒視窗。
3. hello**安裝 Endpoint Protection**刀鋒視窗會開啟不啟用的反惡意程式碼的情況下顯示的 Vm 清單。 Jeff 檢閱 hello 的 Vm 清單中，選取所有的 Vm，然後選取**3 個 Vm 上安裝**。
   ![安裝端點保護][4]
4. hello**選取 Endpoint Protection**刀鋒視窗中開啟提供 Jeff 與兩個反惡意程式碼解決方案。 Jeff 選取 hello **Microsoft 反惡意程式碼**方案。
5. 會顯示 hello 反惡意程式碼解決方案的其他資訊。 Jeff 選取 [建立]。
   ![Microsoft antimalware][5]
6. Jeff 在 hello 輸入 hello 所需的組態設定**安裝**刀鋒視窗，然後選取**確定**。

[Microsoft 反惡意程式碼](../security/azure-security-antimalware.md)現在 hello 上的作用中選取 Vm。

Jeff 會繼續透過 hello 高優先順序和優先順序建議 toomove 決策實作。 Jeff 參考 hello[管理安全性建議](security-center-recommendations.md)toounderstand hello 建議，和每一項功能如果他適用於文件。

Jeff 學習， [Microsoft Security Response Center (MSRC)](../security/azure-security-response-center.md)執行選取的安全性監視的 hello Azure 網路和基礎結構，並從第三方接收威脅情報和濫用抱怨。 如果 Jeff Contoso 的 Azure 訂用帳戶提供安全性連絡人詳細資料，Microsoft 連絡人 Contoso 如果 hello MSRC 會探索該 Contoso 的客戶資料已存取非法或未經授權的合作對象。 讓我們依照 Jeff 他適用於 hello**提供安全性連絡人詳細資料**建議 （嚴重性的建議中 hello 上述建議清單中）。

1. Jeff 選取**提供安全性連絡人詳細資料**上 hello**建議**刀鋒視窗中，這會開啟 hello**提供安全性連絡人詳細資料**刀鋒視窗。
2. Jeff 在 選取 hello Azure 訂用帳戶 tooprovide 連絡資訊。 第二個 [提供安全性連絡人詳細資料]  刀鋒視窗隨即開啟。
   ![安全性連絡人詳細資料][6]
3. 在 hello 第二個**提供安全性連絡人詳細資料**刀鋒視窗中，Jeff 輸入：

  - （沒有他可以輸入的電子郵件地址限制 toohello 數目） 的逗號分隔的 hello 安全性連絡人的電子郵件地址
  - 一個安全性連絡人電話號碼

4. Jeff 也會開啟 hello 選項**傳送給我以電子郵件警示的相關**tooreceive 有關高嚴重性警示的電子郵件。
5. Jeff 選取**確定**tooapply hello 安全性連絡資訊 tooContoso 訂用帳戶。

最後，Jeff 檢閱 hello 低優先順序建議**修復作業系統的弱點可能會**並決定不適用這項建議。 他想 toodismiss hello 建議。 Jeff 選取 hello 三個點顯示 toohello 權限，然後選取**解除**。
   ![解除建議][7]

## <a name="conclusion"></a>結論
監控資訊安全中心的建議可能有助於在發生攻擊之前消除安全性弱點。 您可以使用資訊安全中心的安全性原則來實作和維護防護措施，以防止安全性事件。

<!--Image references-->
[1]: ./media/security-center-using-recommendations/security-center-policy-inheritance.png
[2]: ./media/security-center-using-recommendations/scenario-roles.png
[3]: ./media/security-center-using-recommendations/select-recommendations-tile.png
[4]: ./media/security-center-using-recommendations/install-endpoint-protection.png
[5]:./media/security-center-using-recommendations/microsoft-antimalware.png
[6]: ./media/security-center-using-recommendations/provide-security-contact-details.png
[7]: ./media/security-center-using-recommendations/dismiss-recommendation.png
