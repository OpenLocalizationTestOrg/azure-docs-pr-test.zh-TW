---
title: "高可用性的 Azure MFA Server aaaConfigure |Microsoft 文件"
description: "在設定中部署多個 Azure Multi-Factor Authentication Server 執行個體以提供高可用性。"
services: multi-factor-authentication
keywords: Azure MFA,
documentationcenter: 
author: MicrosoftGuyJFlo
manager: femila
ms.assetid: 
ms.service: multi-factor-authentication
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/23/2017
ms.author: joflore
ms.reviewer: alexwe
ms.custom: it-pro
ms.openlocfilehash: 8c6b1921c734c7a7273e443b3591fbbb15cd5e6c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="configure-azure-multi-factor-authentication-server-for-high-availability"></a>針對高可用性設定 Azure Multi-Factor Authentication Server

您需要 toodeploy tooachieve 高可用性與 Azure 伺服器 MFA 部署多部 MFA 伺服器。 本節提供資訊的載入平衡設計 tooachieve 上您在您的 Azure MFS 伺服器部署的高可用性目標。

## <a name="mfa-server-overview"></a>MFA Server 概觀

hello Azure MFA Server 服務架構是由數個元件組成 hello 下列圖表所示：

 ![MFA Server 架構](./media/mfa-server-high-availability/mfa-ha-architecture.png)

MFA 伺服器是 Windows 伺服器已安裝的 hello Azure Multi-factor Authentication Server 軟體。 在 Azure toofunction hello MFA 服務必須先啟用 hello MFA Server 執行個體。 您可以在內部部署安裝多部 MFA Server。

是第一部已安裝的 MFA 伺服器 hello hello 主要的 MFA 伺服器啟動時由預設的 hello Azure MFA 服務。 hello 主要 MFA server 具有可寫入的 hello PhoneFactor.pfdata 資料庫複本。 MFA Server 執行個體的後續安裝稱為從屬。 hello MFA 從屬有 hello PhoneFactor.pfdata 資料庫的複寫唯讀複本。 MFA Server 使用遠端程序呼叫 (RPC) 複寫資訊。 所有的 MFA 伺服器共同必須加入網域或獨立 tooreplicate 資訊。

MFA 主要和備用 MFA 伺服器通訊以 hello MFA 服務需要雙因素驗證時。 比方說，當使用者嘗試 toogain 存取 tooan 應用程式需要雙因素驗證，hello 會先驗證使用者身分識別提供者，例如 Active Directory (AD)。

在使用 AD 成功驗證後 hello MFA Server 會以 hello MFA 服務進行通訊。 hello MFA Server 等候來自 hello MFA 服務 tooallow 通知，或拒絕 hello 使用者存取 toohello 應用程式。

如果 hello MFA 主要伺服器離線，仍可處理驗證，但無法處理要求變更 toohello MFA 資料庫的作業。 (範例包括： hello 加入的使用者、 自助 PIN 變更，以及變更使用者資訊)

## <a name="deployment"></a>部署

請考慮下列重點負載平衡 Azure MFA Server 以及其相關的元件 hello。

* **使用 RADIUS 標準 tooachieve 高可用性**。 如果您使用 Azure MFA Server 作為 RADIUS 伺服器，您可能會將一部 MFA Server 設定為主要 RADIUS 驗證目標，並將其他 Azure MFA Server 設定為次要驗證目標。 不過，此方法 tooachieve 高可用性可能不實用，因為您必須等候逾時期間 toooccur hello 主要驗證目標上之前，您可以針對 hello 次要驗證進行驗證失敗的驗證目標。 它是更有效率 tooload 平衡 hello 之間的 RADIUS 流量 hello RADIUS 用戶端與 hello RADIUS 伺服器 （在此情況下，做為 RADIUS 伺服器 hello Azure MFA 伺服器），讓您可以使用單一的 URL 可以指向設定 hello RADIUS 用戶端。
* **需要 toomanually 升級 MFA 從屬**。 如果 hello 主要 Azure MFA 伺服器離線，hello 次要 Azure MFA 伺服器會繼續 tooprocess MFA 要求。 不過，主要的 MFA 伺服器可用之前，系統管理員無法將使用者加入或修改 MFA 設定，而且使用者可以進行使用 hello 使用者入口網站的變更。 永遠升級 MFA 從屬 toohello 主機角色是手動程序。
* **元件的可分性**。 Azure MFA Server 是由數個可安裝於的元件組成的 hello hello 相同的 Windows 伺服器執行個體或不同的執行個體上。 這些元件包括 hello 使用者入口網站、 行動裝置應用程式 Web 服務，與 hello ADFS 配接器 （代理程式）。 此 separability 使它可能 toouse hello Web 應用程式 Proxy toopublish hello 使用者入口網站和行動裝置應用程式的網頁伺服器從 hello 周邊網路。 這種組態中加入 toohello 整體安全性的設計，hello 下列圖表所示。 hello MFA 使用者入口網站和行動裝置應用程式 Web 伺服器也可能在 HA 負載平衡設定中部署。

   ![具有周邊網路的 MFA Server](./media/mfa-server-high-availability/mfasecurity.png)

* **透過 SMS 也稱為單向簡訊的單次密碼 (OTP) 需要 hello 使用自黏工作階段，如果流量負載平衡**。 單向 SMS 是包含 OTP 的文字訊息功能會讓 hello MFA Server toosend hello 使用者的驗證選項。 hello 使用者輸入 hello OTP 在提示字元視窗 toocomplete hello MFA 挑戰。 如果您載入平衡 Azure MFA Server，hello 處理 hello 初始驗證要求的相同伺服器必須是 hello 伺服器 hello OTP 訊息接收 hello 使用者資訊。如果另一個的 MFA 伺服器收到 hello OTP 回覆，hello 驗證要求將會失敗。 如需詳細資訊，請參閱[SMS 加入 tooAzure MFA Server 上的一個時間密碼](https://blogs.technet.microsoft.com/enterprisemobility/2015/03/02/one-time-password-over-sms-added-to-azure-mfa-server)。
* **負載平衡的 hello 使用者入口網站和行動裝置應用程式 Web 服務的部署需要自黏工作階段**。 如果您是負載平衡 hello MFA 使用者入口網站和 hello Mobile App Web Service，每個工作階段需要 toostay hello 上的相同的伺服器。

## <a name="high-availability-deployment"></a>高可用性部署

hello 下列圖表顯示 Azure MFA 和其元件，以及參考的 ADFS 的完整 HA 負載平衡 」 的實作。

 ![Azure MFA Server HA 實作](./media/mfa-server-high-availability/mfa-ha-deployment.png)

請注意下列項目 hello 跟著編號區域的 hello 上述圖表中的 hello。

1. hello 兩個 Azure MFA 伺服器 （MFA1 和 MFA2） 負載平衡 (mfaapp.contoso.com)，而設定的 toouse 靜態連接埠 (4443) tooreplicate hello PhoneFactor.pfdata 資料庫。 hello Web 服務 SDK 是每一部安裝 hello MFA Server tooenable 通訊與 hello ADFS 伺服器的 TCP 連接埠 443。 hello MFA 伺服器部署在無狀態負載平衡的組態。 不過，如果您想 toouse OTP SMS 透過，您必須使用可設定狀態的負載平衡。
   ![Azure MFA Server - 應用程式伺服器 HA](./media/mfa-server-high-availability/mfaapp.png)

   > [!NOTE]
   > 因為 RPC 使用動態通訊埠，所以不建議 tooopen toohello 各種可能使用 RPC 動態連接埠上的防火牆。 如果您有防火牆**之間**MFA 應用程式伺服器，您應該 hello MFA Server toocommunicate hello 複寫流量從屬與主要伺服器之間，並開啟連接埠的靜態連接埠上設定防火牆。 您可以藉由建立 DWORD 登錄值，在強制 hello 靜態連接埠```HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Positive Networks\PhoneFactor```呼叫```Pfsvc_ncan_ip_tcp_port```和設定 hello 值 tooan 可用的靜態連接埠。 Hello 從屬 MFA Server toohello 主一律起始連線，hello 靜態連接埠時，才需要 hello 在主機上，但因為您可以在任何時間升級從屬 toobe hello master，您應該在所有的 MFA 伺服器上設定 hello 靜態連接埠。

2. hello 兩個使用者入口網站 MFA/行動裝置應用程式伺服器 （MAS1-向上 MFA-和 MFA-向上-MAS2） 進行負載平衡中**可設定狀態**組態 (mfa.contoso.com)。 前文提過黏性工作階段是負載平衡 hello MFA 使用者入口網站和行動應用程式服務的需求。
   ![Azure MFA Server - 使用者入口網站和行動裝置應用程式服務 HA](./media/mfa-server-high-availability/mfaportal.png)
3. 負載平衡，而在 hello 周邊網路中發行 toohello 網際網路透過負載平衡 ADFS proxy hello ADFS 伺服器陣列。 每個 ADFS 伺服器使用 hello ADFS 代理程式 toocommunicate 以 hello Azure MFA 伺服器透過 TCP 連接埠 443 使用單一負載平衡 URL (mfaapp.contoso.com)。

## <a name="next-steps"></a>後續步驟

* [安裝和設定 Azure MFA Server](multi-factor-authentication-get-started-server.md)
