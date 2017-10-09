---
title: "您需要的 Azure RemoteApp aaaWhat 種集合嗎？ | Microsoft Docs"
description: "深入了解 hello 種集合類型與 Azure RemoteApp 一起使用。"
services: remoteapp
documentationcenter: 
author: msmbaldwin
manager: mbaldwin
ms.assetid: c13ec78d-07e9-4646-8194-cf3efafc1760
ms.service: remoteapp
ms.workload: compute
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/26/2017
ms.author: mbaldwin
ms.openlocfilehash: f00b5fe41af597cf75e26300bf7842c3a8ff94fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="what-kind-of-collection-do-you-need-for-azure-remoteapp"></a>Azure RemoteApp 需要何種集合？
> [!IMPORTANT]
> Azure RemoteApp 即將於 2017 年 8 月 31 日停止服務。 讀取 hello[公告](https://go.microsoft.com/fwlink/?linkid=821148)如需詳細資訊。
> 
> 

Azure RemoteApp 可讓您在任何裝置上與使用者共用應用程式和資源。 要執行此作業建立集合 toohold hello 應用程式及資源，並接著與使用者共用這些集合。 有兩個不同的集合選項，各有不同的網路和驗證選項 - 哪一種最適合您？

讓我們逐步 hello 不同考量和選項，您需要 toomake tooget hello 最超出您的 Azure RemoteApp 集合。 

## <a name="quick-differences-between-hello-collection-types"></a>快速 hello 集合型別之間的差異
|  | 雲端 | 混合式 |
| --- | --- | --- |
| 使用現有的 VNET |是 |是 |
| 需要連線到 AD 的帳戶 (DirSync) |否 |是 |
| 需要加入網域 |否 |是 |
| 需要網域控制站可存取 tooVNET |否 |是 |

## <a name="cloud-collections"></a>雲端集合
* 快速 toocreate-hello 集合的快速佈建，這表示您的應用程式取得 toousers 速度較快。
* 提供您自己的應用程式或共用我們的應用程式。 您可以使用自訂映像 （內建的 Azure VM） 或其中一個 hello 映像包含您訂用帳戶。
* 您不需要 tooconfigure 連接您的集合與您在內部部署的網域之間。
* 但是，您可以選擇性地使用您自己的 Azure VNET tooprovide 存取至內部部署環境到資源，例如 SQL Server （使用資料庫驗證） 的資料共用或 toouse 非 Windows 驗證。

那麼，要怎麼建立？

* 僅限雲端使用嗎？ 建立以 hello**快速建立**hello 入口網站中的選項。
* 雲端 + VNET？ 建立使用 hello**使用 VNET 建立**選項，但不是選擇 toojoin 網域。

## <a name="hybrid-collections"></a>混合式集合
* 提供的完整存取 tooon 內部部署網路 + Azure VNET。
* 包含應用程式和資料的網域加入存取權限。 遠端應用程式可以向您內部部署的 Active Directory 驗證 - 接著便能存取您網域中的資源。
* 以現有的 System Center 解決方案和 Windows 群組原則啟用進階監視和管理功能 (透過在 Windows Server 2012 R2 上建置的自訂映像)
* 支援[ExpressRoute](https://azure.microsoft.com/services/expressroute/) tooconnect Azure VNET tooyour 區域 VNET。

建立使用 hello**使用 VNET 建立**選項，然後選擇 toojoin 網域。

## <a name="authentication-options"></a>驗證選項
Azure RemoteApp 支援 Microsoft 帳戶和 Azure Active Directory 帳戶，但並非所有集合都支援所有方法。 

| 帳戶類型 |  | 雲端 | 雲端 + VNET | 混合式 |
| --- | --- | --- | --- | --- |
| Microsoft 帳戶 | |是 |是 |否 |
| Azure Active Directory (Azure AD) | | | | |
| 僅限 Azure AD 使用 |是 |是 |否 | |
| 具有密碼同步的 AD Connect |是 |是 |是 | |
| 不具密碼同步的 AD Connect |是 |是 |否 | |
| 具 AD FS 的 AD Connect |是 |是 |是 | |
| Azure 支援的第三方識別提供者 (例如 Ping) |是 |是 |是 | |
| Multi-Factor Authentication | |是 |是 |是 |

### <a name="cloud-and-cloud--vnet"></a>雲端和雲端 + VNET
與雲端集合中，您可以使用 Microsoft 帳戶、 Azure AD 帳戶或 hello 兩者的混合。 使用最適合您的使用者的 hello 帳戶。

使用 Microsoft 帳戶沒有任何明確要求。 

如果您想 toouse Azure AD 帳戶，您需要確定您的 Azure AD 租用戶符合其中一個訂用帳戶相關聯的 hello toomake。 當您建立 Azure RemoteApp 訂閱後時，所使用的 hello Azure AD 租用戶已自動與您訂用帳戶相關聯。 任何 Azure AD 使用者，您授與權限 tooneeds toobe 該相同的租用戶。 如有需要您可以[變更 hello Azure AD 租用戶](remoteapp-changetenant.md)與您訂用帳戶相關聯。

### <a name="hybrid-or-cloud--azure-ad--ad"></a>混合式 (或雲端 + Azure AD + AD)
使用 Azure AD + 內部部署 Active Directory 是混合式集合的必要條件。 您需要 toouse AD Connect toointegrate hello 兩個目錄。 但當您設定 AD Connect toohow 需要某些選擇。 

AD Connect 有兩種案例 - 使用密碼同步化或使用 AD 同盟。 簽出 hello [AD Connect 資訊](../active-directory/active-directory-aadconnect.md)toofigure 其中出最適合您。

您也可以使用 Azure AD + AD 搭配雲端集合。 請確定您遵循相同的設定步驟的 hello。

簽出[Azure AD + 的 Azure RemoteApp 的 Active Directory 需求](remoteapp-ad.md)hello 步驟需要的 tooconfigure Azure AD 和 Active Directory。

## <a name="go-create-your-collection"></a>立即建立您的集合！
好了，我認為我們已經知道它現在，因此只有一個項目左邊的 toodo-建立您的第一個 Azure RemoteApp 集合。

[建立雲端集合](remoteapp-create-cloud-deployment.md)或[建立混合式集合](remoteapp-create-hybrid-deployment.md) -立即建立。

