---
title: "aaaAzure 操作安全性檢查清單 |Microsoft 文件"
description: "本文提供一組 Azure 作業安全性的檢查清單。"
services: security
documentationcenter: na
author: unifycloud
manager: swadhwa
editor: tomsh
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/27/2017
ms.author: tomsh
ms.openlocfilehash: 03abe41ec828e929024ee59acd45b06410e9fbf5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-operational-security-checklist"></a>Azure 作業安全性檢查清單
在 Azure 上部署應用程式很快速、輕鬆且符合成本效益。 之前部署雲端應用程式中實際的有用 toohave 檢查清單 tooassist 評估您的應用程式針對清單您 tooconsider 重要和建議的營運安全性動作。

## <a name="introduction"></a>簡介

Azure 提供一套的基礎結構服務，您可以使用 toodeploy 應用程式。 Azure 操作的安全性是指 toohello 服務、 控制項和功能可用 toousers 保護其資料、 應用程式，以及其他 Microsoft Azure 中的資產。

-   tooget hello 最大益處 hello 雲端平台，我們建議您利用 Azure 服務，並遵循 hello 檢查清單。
-   投入時間和資源評估 hello 操作整備狀態的應用程式啟動前的組織擁有的滿意度比沒有更高的速率。 當執行這項工作，檢查清單可以是應用程式會評估一致的方式和而加以進行歷程一兩機制 tooensure。
-   操作評估 hello 層級將 hello 組織的雲端成熟度層級和 hello 應用程式的開發階段、 可用性需求和有所不同資料敏感度需求。

## <a name="checklist"></a>檢查清單

Toohelp 企業將透過各種作業的安全性考量，在部署 Azure 上的複雜的企業應用程式視為是這份檢查清單。 它也可以使用的 toohelp 安全雲端移轉和操作策略打造您的組織。

|檢查清單類別| 說明|
| ------------ | -------- |
| [<br>安全性角色和存取控制](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide)|<ul><li>使用[角色型存取控制 (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure) tooprovide 特定使用者在特定範圍內使用 tooassign 權限 toousers、 群組和應用程式。</li></ul> |
| [<br>資料收集和儲存](https://docs.microsoft.com/azure/storage/storage-security-guide)|<ul><li>使用您的儲存體帳戶使用的管理平面安全性 toosecure[角色型存取控制 (RBAC)](https://docs.microsoft.com/azure/active-directory/role-based-access-control-configure)。</li><li>平面安全性 tooSecuring 存取 tooyour 資料使用資料[共用存取簽章 (SAS)](https://docs.microsoft.com/azure/storage/storage-dotnet-shared-access-signature-part-1)和預存存取原則。</li><li>使用傳輸層級加密 – 使用 HTTPS 和 hello 所使用的加密[（伺服器訊息區塊通訊協定） 的 SMB 3.0](https://msdn.microsoft.com/library/windows/desktop/aa365233.aspx)如[Azure 檔案共用](https://docs.microsoft.com/azure/storage/storage-dotnet-how-to-use-files)。</li><li>使用[用戶端加密](https://docs.microsoft.com/azure/storage/storage-client-side-encryption)toosecure 資料將傳送 toostorage 帳戶，當您需要唯一的加密金鑰的控制權。 </li><li>使用[儲存體服務加密 (SSE)](https://docs.microsoft.com/azure/storage/storage-service-encryption) tooautomatically 加密資料中的 Azure 儲存體，和[Azure 磁碟加密](https://docs.microsoft.com/azure/security/azure-security-disk-encryption)tooencrypt hello OS 和資料磁碟的虛擬機器磁碟檔案。</li><li>使用 Azure[儲存體分析](https://docs.microsoft.com/rest/api/storageservices/storage-analytics)toomonitor 授權類型; 例如使用 Blob 儲存體，您可以看到使用者使用共用存取簽章或 hello 儲存體帳戶金鑰。</li><li>使用[跨原始資源共用 (CORS)](https://docs.microsoft.com/rest/api/storageservices/cross-origin-resource-sharing--cors--support-for-the-azure-storage-services) tooaccess 來自不同網域的儲存體資源。</li></ul> |
|[<br>安全性原則和建議](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide)|<ul><li>使用[Azure 資訊安全中心](https://docs.microsoft.com/azure/security-center/security-center-install-endpoint-protection)toodeploy 端點解決方案。</li><li>新增[web 應用程式防火牆 (WAF)](https://docs.microsoft.com/azure/application-gateway/application-gateway-web-application-firewall-overview) toosecure web 應用程式。</li><li>  使用[下一個層代防火牆 (NGFW)](https://docs.microsoft.com/azure/security-center/security-center-add-next-generation-firewall)從 Microsoft 夥伴 tooincrease 安全性保護。 </li><li>套用安全性 Azure 訂用帳戶; 連絡人詳細資料這個 hello [Microsoft Security Response Centre (MSRC)](https://technet.microsoft.com/security/dn528958.aspx)如果它發現的不合法或未獲授權的合作對象已存取您的客戶資料，請連絡您。</li></ul> |
| [<br>身分識別與存取管理](https://docs.microsoft.com/azure/security/azure-security-identity-management-best-practices)|<ul><li>[使用 Azure AD 同步處理內部部署目錄與雲端目錄](https://docs.microsoft.com/azure/active-directory/connect/active-directory-aadconnect)。</li><li>使用[單一登入](https://azure.microsoft.com/resources/videos/overview-of-single-sign-on/)tooenable 使用者 tooaccess 其 SaaS 應用程式根據 Azure ad 組織帳戶。</li><li>使用 hello[密碼重設註冊活動](https://docs.microsoft.com/azure/active-directory/active-directory-passwords-get-insights)報表 toomonitor hello 使用者註冊。</li><li>對使用者啟用 [Multi-Factor Authentication (MFA)](https://docs.microsoft.com/azure/multi-factor-authentication/multi-factor-authentication)。</li><li>應用程式的開發人員 toouse 安全的身分識別功能類似[Microsoft 安全性開發週期 (SDL)](https://www.microsoft.com/download/details.aspx?id=12379)。</li><li>主動監視可疑的活動，方法是使用 Azure AD Premium 異常報告和 [Azure AD Identity Protection 功能](https://docs.microsoft.com/azure/active-directory/active-directory-identityprotection)。</li></ul> |
|[<br>持續安全性監視](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide)|<ul><li>使用惡意程式碼評定解決方案[記錄分析](https://docs.microsoft.com/azure/log-analytics/log-analytics-overview)tooreport hello 基礎結構中的反惡意程式碼保護狀態。</li><li>使用[更新評估](https://docs.microsoft.com/azure/operations-management-suite/oms-solution-update-management)toodetermine hello 整體曝光 toopotential 安全性問題，以及是否或重要性這些更新適用於您的環境。</li><li>hello[身分識別和存取](https://docs.microsoft.com/azure/operations-management-suite/oms-security-monitoring-resources)提供您的使用者概觀 </li><ul><li>使用者身分識別狀態、</li><li>失敗的嘗試 toolog 的數目</li><li>  hello 期間每次嘗試後，已鎖定的帳戶所使用的使用者帳戶</li> <li>密碼已變更或重設的帳戶 </li><li>目前已登入的帳戶數目。</li></ul></ul> |
| [<br>Azure 資訊安全中心的偵測功能](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)|<ul><li>使用[偵測功能](https://docs.microsoft.com/azure/security-center/security-center-detection-capabilities)、 tooidentify 目標 Microsoft Azure 資源的作用中威脅。</li><li>使用[整合威脅情報](https://blogs.msdn.microsoft.com/azuresecurity/2016/12/19/get-threat-intelligence-reports-with-azure-security-center/)這看起來的已知的不良執行者利用全域威脅 Microsoft 產品和服務，從智慧 hello [Microsoft 數位犯罪單元 (DCU)](https://www.microsoft.com/stories/cyber.aspx)，hello[Microsoft Security Response Center (MSRC)](https://docs.microsoft.com/azure/security/azure-security-response-center)，和外部的摘要。</li><li>使用[行為分析](https://blogs.technet.microsoft.com/enterprisemobility/2016/06/30/ata-behavior-analysis-monitoring/)套用已知的模式 toodiscover 惡意行為。 </li><li>使用[異常偵測](https://msdn.microsoft.com/library/azure/dn913096.aspx)使用統計分析 toobuild 歷程記錄的基準。</li></ul> |
| [<br>開發人員作業 (DevOps)](https://docs.microsoft.com/azure/architecture/checklist/dev-ops)|<ul><li>[基礎結構程式碼 (IaC)](https://azure.microsoft.com/documentation/articles/resource-group-authoring-templates/)是可啟用 hello 自動化和驗證的建立和清除作業，以提供安全且穩定裝載平台的應用程式的網路和虛擬機器 toohelp 作法。</li><li>[連續整合及部署](https://www.visualstudio.com/docs/build/overview)磁碟機 hello 進行中的合併和程式碼，而導致 toofinding 缺失早期測試。 </li><li>[Release Management](https://msdn.microsoft.com/library/vs/alm/release/overview) 可透過您管線的每個階段管理自動化的部署。</li><li>執行中應用程式的[應用程式效能監視](https://azure.microsoft.com/documentation/articles/app-insights-start-monitoring-app-health-usage/)包括應用程式健康情況的生產環境以及客戶的使用方式，能協助組織產生假設並快速驗證或反駁策略。</li><li>使用[負載測試和自動調整規模](https://www.visualstudio.com/docs/test/performance-testing/getting-started/getting-started-with-performance-testing)我們可以在我們的應用程式 tooimprove 部署品質和 toomake 確定我們的應用程式永遠是最新的或使用 toocater toohello 商務需求找出效能問題。</li></ul> |


## <a name="conclusion"></a>結論
許多組織已成功在 Azure 上部署和操作其雲端應用程式。 hello 檢查清單提供會反白顯示數個是不可或缺的檢查清單，並幫助您成功部署和挫折免費作業 tooincrease hello 可能性。 強烈建議您在 Azure 上進行現有和新的應用程式部署時，使用這些作業和策略考量。

## <a name="next-steps"></a>後續步驟
在本文件中，您所導入了的 tooOMS 安全性和稽核 」 解決方案。 toolearn 進一步了解 OMS 安全性，請參閱下列文章 hello:

- [Operations Management Suite (OMS) 概觀](https://docs.microsoft.com/en-us/azure/operations-management-suite/operations-management-suite-overview)。
- [設計與作業安全性](https://www.microsoft.com/trustcenter/security/designopsecurity)。
- [Azure 資訊安全中心規劃和操作](https://docs.microsoft.com/azure/security-center/security-center-planning-and-operations-guide)。
