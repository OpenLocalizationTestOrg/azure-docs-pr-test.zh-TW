---
title: "aaaAdd Azure 資訊安全中心中的 web 應用程式防火牆 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議 * * 加入 web 應用程式防火牆 * * 和 * * 完成應用程式保護 * *。"
services: security-center
documentationcenter: na
author: TerryLanfear
manager: MBaldwin
editor: 
ms.assetid: 8f56139a-4466-48ac-90fb-86d002cf8242
ms.service: security-center
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/09/2017
ms.author: terrylan
ms.openlocfilehash: bff0aa2a5c6e0dde23396f93de52abe295053581
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-web-application-firewall-in-azure-security-center"></a>在 Azure 資訊安全中心新增 Web 應用程式防火牆
Azure 資訊安全中心可能會建議您新增的 web 應用程式的防火牆 (WAF) 從 Microsoft 夥伴 toosecure web 應用程式。 本文件將逐步引導您透過如何的範例 tooapply 這項建議。

系統會針對任何具有相關聯網路安全性群組 (包含開放輸入 Web 連接埠 (80,443)) 的公開 IP (執行個體層級 IP 或負載平衡 IP)，顯示 WAF 建議。

資訊安全中心建議您佈建 WAF toohelp 防禦目標 web 應用程式的 App Service 環境和虛擬機器上的攻擊。 App Service 環境 (ASE) 是Azure App Service 的 [Premium](https://azure.microsoft.com/pricing/details/app-service/) 服務方案選項，可提供完全隔離和專用的環境，以便安全地執行 Azure App Service 應用程式。 toolearn 深入了解 ASE，請參閱 hello[應用程式服務環境的文件](../app-service/app-service-app-service-environments-readme.md)。

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。  本文件不是一份逐步解說指南。
>
>

## <a name="implement-hello-recommendation"></a>實作 hello 建議
1. 在 hello**建議**刀鋒視窗中，選取**保護 web 應用程式使用 web 應用程式防火牆**。
   ![保護 Web 應用程式][1]
2. 在 hello**保護您的 web 應用程式使用 web 應用程式防火牆**刀鋒視窗中，選取 web 應用程式。 hello**加入 Web 應用程式防火牆**刀鋒視窗隨即開啟。
   ![新增 Web 應用程式防火牆][2]
3. 您可以選擇 toouse 現有 web 應用程式防火牆如果有的話，或您可以建立一個新。 此範例中沒有任何可用的現有 WAF，因此我們會建立一個 WAF。
4. toocreate WAF，從 hello 整合協力電腦清單中選取方案。 在此範例中，我們會選取 [Barracuda Web 應用程式防火牆]。
5. hello **Barracuda Web 應用程式防火牆**刀鋒視窗會開啟提供您 hello 夥伴方案的相關資訊。 選取**建立**hello 資訊刀鋒視窗中。

   ![防火牆資訊刀鋒視窗][3]

6. hello**新的 Web 應用程式防火牆**刀鋒視窗隨即開啟，您可以在其中執行**VM 組態**步驟並提供**WAF 資訊**。 選取 [VM 組態]。
7. 在 hello **VM 組態**刀鋒視窗中，輸入 hello 虛擬機器執行的必要的 toospin hello WAF 的資訊。
   ![VM configuration][4]
8. 傳回 toohello**新的 Web 應用程式防火牆**刀鋒視窗，然後選取**WAF 資訊**。 在 hello **WAF 資訊**刀鋒視窗中，設定 hello WAF 本身。 步驟 7 可讓您在哪個 hello WAF 執行和步驟 8 可讓您 tooprovision hello WAF 本身 tooconfigure hello 虛擬機器。

## <a name="finalize-application-protection"></a>完成應用程式保護
1. 傳回 toohello**建議**刀鋒視窗。 建立 hello WAF，呼叫後產生新的項目**完成應用程式保護**。 此項目可讓您知道您需要 toocomplete hello 程序實際上裝設 hello WAF hello Azure 虛擬網路內，讓它可以保護 hello 應用程式。

   ![完成應用程式保護][5]

2. 選取 [完成應用程式保護] 。 此時會開啟新的分頁。 您可以看到是需要 toohave 其流量重新路由到 web 應用程式。
3. 選取 hello web 應用程式。 刀鋒視窗隨即開啟，可讓您的正在完成 hello web 應用程式防火牆安裝的步驟。 完成 hello 步驟，然後選取 **限制流量**。 資訊安全中心未 hello 配線接您。

   ![限制流量][6]

> [!NOTE]
> 您可以藉由新增這些應用程式 tooyour 現有 WAF 部署保護的資訊安全中心中的多個 web 應用程式。
>
>

現在完全整合，從該 WAF hello 記錄檔。 資訊安全中心可以啟動自動收集和分析 hello 記錄檔，如此它就會出現重要的安全性警示 tooyou。

## <a name="next-steps"></a>後續步驟
這份文件範例說明了如何 tooimplement 會 hello 資訊安全中心建議 「 新增 web 應用程式 」。 toolearn 進一步了解設定 web 應用程式防火牆，請參閱 hello 下列資訊：

* [設定 App Service 環境的 Web 應用程式防火牆 (WAF)](../app-service-web/app-service-app-service-environment-web-application-firewall.md)

toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [管理 Azure 資訊安全中心的安全性建議](security-center-recommendations.md) -- 了解建議如何協助保護您的 Azure 資源。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) -- 尋找有關 Azure 安全性與相容性的部落格文章。

<!--Image references-->
[1]: ./media/security-center-add-web-application-firewall/secure-web-application.png
[2]:./media/security-center-add-web-application-firewall/add-a-waf.png
[3]: ./media/security-center-add-web-application-firewall/info-blade.png
[4]: ./media/security-center-add-web-application-firewall/select-vm-config.png
[5]: ./media/security-center-add-web-application-firewall/finalize-waf.png
[6]: ./media/security-center-add-web-application-firewall/restrict-traffic.png
