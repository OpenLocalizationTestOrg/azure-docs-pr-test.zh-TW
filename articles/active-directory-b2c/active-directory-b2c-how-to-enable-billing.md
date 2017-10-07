---
title: "aaaHow tooLink Azure 訂用帳戶 tooAzure AD B2C |Microsoft 文件"
description: "逐步指南 tooenable 計費的 Azure AD B2C 租用戶到 Azure 訂用帳戶。"
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 12/05/2016
ms.author: joroja
ms.openlocfilehash: 07b2ed5f7f5f543c9cbb8e9a35107462448e9440
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="linking-an-azure-subscription-tooan-azure-b2c-tenant-toopay-for-usage-charges"></a>連結使用費用 Azure 訂用帳戶 tooan Azure B2C 租用戶 toopay

進行中的使用費用，適用於 Azure Active Directory B2C （或 Azure AD B2C） 會使用票據的 tooan Azure 訂用帳戶。 必須為 hello 租用戶系統管理員 tooexplicitly 連結 hello Azure AD B2C 租用戶 tooan 之後建立 hello B2C 租用戶本身的 Azure 訂用帳戶。  此連結達成方式是建立 Azure AD"B2C 租用戶 「 hello 目標 Azure 訂用帳戶中的資源。 許多 B2C 租用戶可以是連結的 tooa 單一 Azure 訂用帳戶以及其他 Azure 資源 (例如，Vm，資料存放區，LogicApps)


> [!IMPORTANT]
> hello 使用量計費和 B2C 位於 hello 遵循頁面上的定價的最新資訊： [Azure AD B2C 定價](
https://azure.microsoft.com/pricing/details/active-directory-b2c/)

## <a name="step-1---create-an-azure-ad-b2c-tenant"></a>步驟 1 - 建立 Azure AD B2C 租用戶
必須先完成 B2C 租用戶建立。 如果您已經建立目標 B2C 租用戶，請略過此步驟。 [開始使用 Azure AD B2C](active-directory-b2c-get-started.md)

## <a name="step-2---open-azure-portal-in-hello-azure-ad-tenant-that-shows-your-azure-subscription"></a>步驟 2-hello 顯示您的 Azure 訂用帳戶的 Azure AD 租用戶中開啟 Azure 入口網站
瀏覽 toohello [Azure 入口網站](https://portal.azure.com)。 切換 toohello 顯示 hello 希望 toouse 的 Azure 訂用帳戶的 Azure AD 租用戶。 此 Azure AD 租用戶與不同 hello B2C 租用戶。 在 hello Azure 入口網站，按一下 hello 上 hello 右上方的 hello 儀表板 tooselect hello Azure AD 租用戶的帳戶名稱。 Azure 訂用帳戶是必要的 tooproceed。 [取得 Azure 訂用帳戶](https://account.windowsazure.com/signup?showCatalog=True)

![切換 tooyour Azure AD 租用戶](./media/active-directory-b2c-how-to-enable-billing/SelectAzureADTenant.png)

## <a name="step-3---create-a-b2c-tenant-resource-in-azure-marketplace"></a>步驟 3 - 在 Azure Marketplace 中建立 B2C 租用戶資源
開啟 Marketplace 按一下 hello Marketplace 圖示，或選取 hello 綠色"+"hello 左上角的 hello 儀表板。  搜尋並選取 Azure Active Directory B2C。 選取 [建立]。

![選取 Marketplace](./media/active-directory-b2c-how-to-enable-billing/marketplace.png)

![搜尋 AD B2C](./media/active-directory-b2c-how-to-enable-billing/searchb2c.png)

hello Azure AD B2C 資源建立對話方塊涵蓋 hello 下列參數：

1. Azure AD B2C 租用戶 – 從 hello 下拉式清單中選取 Azure AD B2C 租用戶。  只會顯示合格的 Azure AD B2C 租用戶。  合格 B2C 租用戶符合這些條件： 您是 hello hello B2C 租用戶的全域系統管理員和 hello B2C 租用戶不是目前相關聯的 tooan Azure 訂用帳戶

2. Azure AD B2C 資源名稱-是 hello 的 B2C 租用戶的預先選取的 toomatch hello 網域名稱

3. 訂用帳戶 - 您身為系統管理員或共同管理員的作用中 Azure 訂用帳戶。  多個 Azure AD B2C 租用戶加入 tooone Azure 訂用帳戶

4. 資源群組和資源群組位置 - 此構件可協助您安排多個 Azure 資源。  這個選項對於 B2C 租用戶位置、效能或計費狀態沒有任何影響

5. 釘選最簡單的存取 tooyour B2C 租用戶，帳單資訊和 hello B2C 租用戶設定 toodashboard![建立 B2C 資源](./media/active-directory-b2c-how-to-enable-billing/createresourceb2c.png)

## <a name="step-4---manage-your-b2c-tenant-resources-optional"></a>步驟 4 - 管理 B2C 租用戶資源 (選擇性)
當部署完成之後，新的 「 B2C 租用戶 「 資源 hello 目標資源群組中所建立，以及相關 Azure 訂用帳戶。  您應該會看到您其他的 Azure 資源旁邊新增「B2C 租用戶」類型的新資源。

![建立 B2C 資源](./media/active-directory-b2c-how-to-enable-billing/b2cresourcedashboard.png)

藉由按一下 hello B2C 租用戶資源，您就能夠
- 按一下訂用帳戶名稱 tooreview 帳單資訊。 請參閱「計費和使用量」。
- 按一下 [Azure AD B2C 設定 tooopen 直接 tooyour B2C 租用戶設定] 刀鋒視窗中新的瀏覽器索引標籤
- 提交支援要求
- 移動您 B2C 租用戶資源 tooanother Azure 訂用帳戶或 tooanother 資源群組。  這個選項會變更哪一個 Azure 訂用帳戶會收到使用費用。

![B2C 資源設定](./media/active-directory-b2c-how-to-enable-billing/b2cresourcesettings.png)

## <a name="known-issues"></a>已知問題
- B2C 租用戶刪除。 建立 B2C 租用戶時，如果刪除，並重新建立與 hello 相同的網域名稱，請也刪除並重新建立以 hello hello 「 連結 」 資源相同的網域名稱。  您會發現這在 hello 訂用帳戶的租用戶透過 hello Azure 入口網站中 「 連結 」 [資源] 下所有資源。
- 在區域資源位置自我強加的限制。  在罕見的情況下，使用者可能針對建立 Azure 資源建立了區域限制。  這項限制可能會導致 hello 建立 hello 連結 Azure 訂用帳戶和 B2C 租用戶之間。 toomitigate，請放寬這項限制。

## <a name="next-steps"></a>後續步驟
針對每個 B2C 租用戶完成這些步驟後，您的 Azure 訂用帳戶就會根據 Azure 直接或企業合約詳細資料計費。
- 檢閱您選取的 Azure 訂用帳戶內的使用量和計費
- 檢閱詳細的每一天使用量報告使用 hello[使用量報告 API](active-directory-b2c-reference-usage-reporting-api.md)
