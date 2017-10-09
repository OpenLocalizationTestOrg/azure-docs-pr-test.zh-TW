---
title: "aaaAzure 資訊安全中心快速入門指南 |Microsoft 文件"
description: "這篇文章可協助您快速開始使用 Azure 資訊安全中心帶領您完成 hello 安全性監視和原則管理元件，並將您連結 toonext 步驟。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 61e95a87-39c5-48f5-aee6-6f90ddcd336e
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: terrylan
ms.openlocfilehash: 23b2444ba1ba30d0a1bd1a1afbc4fd0abfd0827c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-security-center-quick-start-guide"></a>Azure 資訊安全中心快速入門指南
這篇文章可協助您快速地開始使用 Azure 資訊安全中心透過帶領您完成 hello 安全性監視和原則管理元件的資訊安全中心。

> [!NOTE]
> 從開始早期年 6 月 2017年，資訊安全中心將會使用 hello Microsoft Monitoring Agent toocollect 及儲存資料。 請參閱[Azure 安全性 Center 平台移轉](security-center-platform-migration.md)toolearn 更多。 本文章中的 hello 資訊表示資訊安全中心功能之後轉換 toohello Microsoft Monitoring Agent。
>
>

## <a name="prerequisites"></a>必要條件
tooget 啟動與資訊安全中心，您必須擁有 Azure 的訂用帳戶 tooMicrosoft。 如果您沒有訂用帳戶，可以註冊[免費帳戶](https://azure.microsoft.com/pricing/free-trial/)。

hello 免費層的資訊安全中心與您的訂用帳戶會自動啟用，並提供您的 Azure 資源 hello 安全性狀態的可視性。 它提供基本的安全性原則管理、安全性建議並整合 Azure 合作夥伴的安全性產品和服務。

您可以存取的資訊安全中心從 hello [Azure 入口網站](https://azure.microsoft.com/features/azure-portal/)。 toolearn 深入了解 hello Azure 入口網站，請參閱 hello[入口網站的文件](https://azure.microsoft.com/documentation/services/azure-portal/)。

## <a name="permissions"></a>權限
資訊安全中心，因此您只看到相關的資訊 tooan 指派資源所屬的 hello 訂用帳戶或資源群組的擁有者、 參與者或讀取器 hello 角色時的 Azure 資源。 請參閱[Azure 資訊安全中心中的權限](security-center-permissions.md)toolearn 深入了解角色與資訊安全中心所允許的動作。

## <a name="data-collection"></a>資料收集
資訊安全中心會收集從虛擬機器 (Vm) tooassess 其資訊安全狀態、 提供安全性建議事項，並警示您 toothreats。 當您第一次存取資訊安全中心時，訂用帳戶中的所有 VM 都會啟用資料收集。 對所有現有的資訊安全中心會佈建 hello Microsoft Monitoring Agent 支援的 Azure Vm 和建立任何新的。 請參閱[啟用資料收集](security-center-enable-data-collection.md)toolearn 更多關於資料收集的運作方式。

建議您啟用資料收集。 如果您使用 hello 免費層的資訊安全中心，您可以關閉資料收集 hello 安全性原則中停用的 Vm 所傳來的資料收集。 需要訂閱 hello 標準層的資訊安全中心上的資料收集。 請參閱[資訊安全中心定價](security-center-pricing.md)toolearn 深入了解 hello 免費及標準定價層。

hello 下列步驟說明 tooaccess 並用 hello 資訊安全中心的元件。 在這些步驟中，我們會示範如何關閉資料收集，如果您選擇出 tooopt tooturn。

> [!NOTE]
> 本文介紹 hello 服務使用的範例部署。 此文章不是逐步指南。
>
>

## <a name="access-security-center"></a>存取資訊安全中心
在 hello 入口網站，請遵循這些步驟 tooaccess 資訊安全中心：

1. 在 hello **Microsoft Azure**功能表上，選取**資訊安全中心**。

   ![Azure 功能表][1]
2. 如果您要存取的資訊安全中心 hello 第一次，hello ** 褖畫惎**刀鋒視窗隨即開啟。 選取**啟動資訊安全中心**tooopen hello**資訊安全中心**刀鋒視窗，然後 tooenable 資料收集。
   ![歡迎使用畫面][10]
3. 啟動資訊安全中心的 hello  褖畫惎] 刀鋒視窗，或從 hello Microsoft Azure 功能表選取 [資訊安全中心之後，hello**資訊安全中心**刀鋒視窗隨即開啟。 針對輕鬆存取 toohello**資訊安全中心**刀鋒視窗中 hello 未來，選取 hello **Pin 刀鋒視窗 toodashboard**選項 （右上方）。
   ![Pin 刀鋒視窗 toodashboard 選項][2]

## <a name="use-security-center"></a>使用資訊安全中心
您可以設定 Azure 訂用帳戶和資源群組的安全性原則。 一同設定您訂用帳戶的安全性原則：

1. 在 hello**資訊安全中心**刀鋒視窗中，選取 hello**原則**磚。
2. 在 hello**安全性原則-定義每個訂閱的原則**刀鋒視窗中，選取的訂用帳戶。
3. 在 hello**安全性原則**刀鋒視窗中，**資料收集**是啟用的 tooautomatically 收集記錄檔。 hello 監視功能延伸模組的 hello 訂用帳戶中的所有目前和新 Vm 上佈建。 (在 hello 免費層上的資訊安全中心，您可以退出資料收集設定**資料收集**太**關閉**。 設定**資料收集**太**關閉**防止資訊安全中心提供安全性警示和建議。)
4. 在 hello**安全性原則**刀鋒視窗中，選取**防止原則**。 這會開啟 hello**防止原則**刀鋒視窗。
5. 在 hello**防止原則**刀鋒視窗中，開啟 hello 建議的 toosee 做為您的安全性原則的一部分。 範例：

   * 設定**系統更新**太**上**掃描所有遺漏的 OS 更新支援的 Vm。
   * 設定**作業系統弱點**太**上**掃描所有支援的 Vm tooidentify 可能會使任何 OS 設定 hello VM 更容易遭受 tooattack。

### <a name="view-recommendations"></a>檢視建議
1. 傳回 toohello**資訊安全中心**刀鋒視窗，然後選取 hello**建議**磚。 資訊安全中心定期分析您的 Azure 資源 hello 安全性狀態。 當資訊安全中心識別潛在的安全性漏洞時，它會顯示建議的 hello**建議**刀鋒視窗。
   ![Azure 資訊安全中心的建議][5]
2. 選取在 hello 建議**建議**刀鋒視窗 tooview 詳細的資訊和/或 tootake 動作 tooresolve hello 發出。

### <a name="view-hello-security-state-of-your-resources"></a>檢視您資源的 hello 安全性狀態
1. 傳回 toohello**資訊安全中心**刀鋒視窗。 hello**防止**hello 儀表板 區段包含 hello 安全性狀態的指標，這對於資料和應用程式網路的 Vm。
2. 選取**計算**tooview 的詳細資訊。 hello**計算**刀鋒視窗會開啟顯示三個索引標籤：

  - **概觀** - 包含監視和 VM 的建議。
  - **虛擬機器** - 列出所有 VM 及其目前的安全性狀態。
  - **雲端服務** - 列出資訊安全中心監視的 Web 和背景工作角色清單。

    ![Azure 資訊安全中心中的 hello 資源健全狀況圖格][6]

3. 在 hello**概觀**索引標籤上，選取下方的建議**虛擬機器建議**tooview 詳細資訊和/或採取動作 tooconfigure 必要的控制項。
4. 在 hello**虛擬機器**索引標籤上，選取 VM tooview 其他詳細資料。

### <a name="view-security-alerts"></a>檢視安全性警示
1. 傳回 toohello**資訊安全中心**刀鋒視窗，然後選取 hello**安全性警示**磚。 hello**安全性警示**刀鋒視窗會開啟並顯示警示的清單。 hello 資訊安全中心分析您的安全性記錄檔和網路活動會產生這些警示。 包含來自整合式合作夥伴解決方案的警示。
   ![Azure 資訊安全中心的安全性警示][7]

   > [!NOTE]
   > 安全性警示才可使用的資訊安全中心 hello 標準層啟用。 使用 60 天免費試用版的 hello Standard 價格區間。 請參閱[後續步驟](#next-steps)如需如何 tooget hello 標準層。
   >
   >
2. 選取警示 tooview 其他資訊。 在此範例中，請選取 [探索到修改過的系統二進位檔]。 這會開啟刀鋒視窗，提供有關 hello 警示的其他詳細資料。
   ![Azure 資訊安全中心的安全性警示詳細資料][8]

### <a name="view-hello-health-of-your-partner-solutions"></a>檢視 hello 健康情況的協力廠商解決方案
1. 傳回 toohello**資訊安全中心**刀鋒視窗。 hello**合作夥伴解決方案**磚可讓您監視您一眼 hello 與您 Azure 訂用帳戶整合協力廠商方案的健全狀況狀態。
2. 選取 hello**合作夥伴解決方案**磚。 刀鋒視窗會開啟，並顯示的協力廠商解決方案清單連接 tooSecurity 中心。
   ![][9]
3. 選取合作夥伴解決方案。 在此範例中，我們選取 hello **QualysVa1**方案。  刀鋒視窗會開啟並顯示 hello 夥伴方案和 hello 方案 hello 狀態相關聯的資源。 選取**方案主控台**tooopen hello 夥伴管理體驗此解決方案。

## <a name="next-steps"></a>後續步驟
這篇文章會引進 toohello 安全性監視和原則管理元件的資訊安全中心。 既然您已熟悉的資訊安全中心，請嘗試下列步驟的 hello:

* 為您的 Azure 訂用帳戶設定安全性原則。 詳細資訊，請參閱 toolearn [Azure 資訊安全中心中設定安全性原則](security-center-policies.md)。
* 您可以使用 hello 建議的資訊安全中心 toohelp 保護您的 Azure 資源。 詳細資訊，請參閱 toolearn[管理 Azure 資訊安全中心中的安全性建議](security-center-recommendations.md)。
* 檢閱並管理目前的安全性警示。 詳細資訊，請參閱 toolearn[中 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md)。
- [Azure 資訊安全中心資料安全性](security-center-data-security.md) - 了解資訊安全中心如何管理及保護其中的資料。
* 深入了解 hello[進階威脅偵測功能](security-center-detection-capabilities.md)隨附的 hello[標準層](security-center-pricing.md)的資訊安全中心。 hello 標準層是免費提供 hello 前 60 天。
* 如果您有關於使用資訊安全中心的問題，請參閱 hello [Azure 安全性中心常見問題集](security-center-faq.md)。

<!--Image references-->
[1]: ./media/security-center-get-started/azure-menu.png
[2]: ./media/security-center-get-started/security-center-pin.png
[3]: ./media/security-center-get-started/security-policy.png
[4]: ./media/security-center-get-started/prevention-policy.png
[5]: ./media/security-center-get-started/recommendations.png
[6]: ./media/security-center-get-started/resources-health.png
[7]: ./media/security-center-get-started/security-alert.png
[8]: ./media/security-center-get-started/security-alert-detail.png
[9]: ./media/security-center-get-started/partner-solutions.png
[10]: ./media/security-center-get-started/welcome.png
