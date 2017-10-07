---
title: "aaaAzure 服務網狀架構安全性檢查清單 |Microsoft 文件"
description: "本文提供一組 Azure 網狀架構安全性的檢查清單。"
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
ms.date: 08/04/2017
ms.author: tomsh
ms.openlocfilehash: 10ffaea9e7e4de6d758b0a57a79e269c87bfd14d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="azure-service-fabric-security-checklist"></a>Azure Service Fabric 安全性檢查清單
本文提供便於使用的檢查清單，以協助您保護 Azure Service Fabric 環境。

## <a name="introduction"></a>簡介
Azure Service Fabric 是分散式的系統平台，可讓您輕鬆 toopackage、 部署及管理可擴充且可靠的 microservices。 服務網狀架構也會討論 hello 在開發和管理雲端應用程式的重大挑戰。 開發人員與管理員能夠避免複雜的基礎結構問題，專注於實作關鍵且嚴格要求之可調整、可信賴且可管理的工作負載。

## <a name="checklist"></a>檢查清單
使用下列檢查清單 toohelp 您先確定您尚未被忽略任何重要問題管理和設定安全的 Azure Service Fabric 解決方案中的 hello。


|檢查清單類別| 說明 |
| ------------ | -------- |
|[角色型存取控制 (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles) | <ul><li>存取控制可讓 hello 叢集系統管理員 toolimit 存取 toocertain 叢集作業會針對不同使用者群組，讓 hello 叢集更安全。</li><li>系統管理員具有完整存取 toomanagement 功能 （包括讀取/寫入功能）。 </li><li>   使用者，根據預設，具有讀取權限 toomanagement 功能 （例如，查詢功能） 和 hello 能力 tooresolve 應用程式和服務。</li></ul>|
|[X.509 憑證和 Service Fabric](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>執行生產環境工作負載之叢集中所使用的[憑證](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/working-with-certificates)應該是使用已正確設定的 Windows Server 憑證服務來建立，或是從已核准的[憑證授權單位 (CA)](https://en.wikipedia.org/wiki/Certificate_authority) 取得。</li><li>絕對不要在生產環境中使用以 [MakeCert.exe](https://msdn.microsoft.com/library/windows/desktop/aa386968.aspx) 這類工具建立的[暫時或測試憑證](https://docs.microsoft.com/en-us/dotnet/framework/wcf/feature-details/how-to-create-temporary-certificates-for-use-during-development)。 </li><li>您可以使用[自我簽署憑證](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security)，但應該只用於測試叢集，不應該在生產環境中使用。</li></ul>|
|[叢集安全性](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security) | <ul><li>hello 叢集安全性案例包括節點對節點安全性、 用戶端對節點安全性[角色型存取控制 (RBAC)](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-security-roles)。</li></ul>|
|[叢集驗證](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>驗證叢集同盟的[節點對節點通訊](https://github.com/MicrosoftDocs/azure-docs/blob/master/articles/service-fabric/service-fabric-cluster-security.md)。 </li></ul>|
|[伺服器驗證](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm) | <ul><li>驗證 hello[叢集管理端點](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-portal)tooa 管理用戶端。</li></ul>|
|[應用程式安全性](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-creation-via-arm)| <ul><li>將應用程式組態值加密和解密。</li><li> 在複寫期間將資料跨節點加密。</li></ul>|
|[叢集憑證](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security) | <ul><li>此憑證是在叢集上的 hello 節點之間需要的 toosecure hello 通訊。</li><li>  Hello hello 指紋 > 一節中的 hello 主要憑證指紋和設定的 hello 次要 hello ThumbprintSecondary 變數中。</li></ul>|
|[ServerCertificate](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-windows-cluster-x509-security)| <ul><li>當它嘗試 tooconnect toothis 叢集時，此憑證會呈現 toohello 用戶端。 您可以使用兩個不同的伺服器憑證 (主要和次要) 進行更新。</li></ul>|
|ClientCertificateThumbprints| <ul><li>這是一組您想 tooinstall hello 驗證用戶端上的憑證。 </li></ul>|
|ClientCertificateCommonNames| <ul><li>設定 hello 的一般名稱的第一個用戶端憑證 hello hello CertificateCommonName。 hello CertificateIssuerThumbprint 是 hello hello 簽發者，此憑證的指紋。 </li></ul>|
|ReverseProxyCertificate| <ul><li>這是選擇性的憑證，可以指定是否要讓 toosecure 您[反向 Proxy](https://docs.microsoft.com/en-in/azure/service-fabric/service-fabric-reverseproxy)。 </li></ul>|
|金鑰保存庫| <ul><li>用於在 Azure 中的 Service Fabric 叢集 toomanage 憑證。  </li></ul>|


## <a name="next-steps"></a>後續步驟
- [Service Fabric 叢集升級程序與您的期望](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-cluster-upgrade)
- [在 Visual Studio 中管理 Service Fabric 應用程式](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-manage-application-in-visual-studio)。
- [Service Fabric 健康狀態模型簡介](https://docs.microsoft.com/en-us/azure/service-fabric/service-fabric-health-introduction)。
