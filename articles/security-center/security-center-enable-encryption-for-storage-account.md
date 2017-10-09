---
title: "在 Azure 資訊安全中心的儲存體帳戶的 aaaEnable 加密 |Microsoft 文件"
description: "本文件說明如何 tooimplement hello Azure 資訊安全中心建議 * * 啟用加密的 Azure 儲存體帳戶 * *。"
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
ms.date: 12/20/2016
ms.author: terrylan
ms.openlocfilehash: c5cbafbf3a8be86f213dcf1c0c0ddcc0222b3d95
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="enable-encryption-for-azure-storage-account-in-azure-security-center"></a>在 Azure 資訊安全中心啟用 Azure 儲存體帳戶的加密
Azure 資訊安全中心可能建議您對待用資料啟用 Azure 儲存體服務加密。

儲存體服務加密 (SSE) 中的運作方式 hello 資料寫入 tooAzure 儲存時加密和解密 hello 之前擷取的資料。  SSE 目前僅適用於 hello Azure Blob 服務可用於區塊 blob，分頁 blob，並附加 blob。  詳細資訊，請參閱 toolearn[待用資料的儲存體服務加密](../storage/common/storage-service-encryption.md)。


> [!Note]
> 啟用加密之後，只有新的資料會加密。 儲存體帳戶中任何現有的 blob 保持未加密。 tooencrypt 現有的 blob，請參閱 hello[儲存體服務加密常見問題集](../storage/common/storage-service-encryption.md#frequently-asked-questions-about-storage-service-encryption-for-data-at-rest)。
>
>

只有 Resource Manager 儲存體帳戶才支援儲存體服務加密。 目前不支援傳統儲存體帳戶。 傳統的 toounderstand hello 和資源管理員部署模型，請參閱[Azure 部署模型](../azure-classic-rm.md)。

> [!NOTE]
> 本文件介紹 hello 服務使用的範例部署。  本文件不是一份逐步解說指南。
>
>

## <a name="implement-hello-recommendation"></a>實作 hello 建議
1. 在 hello**建議**刀鋒視窗中，選取**啟用 Azure 儲存體帳戶的加密**。
   ![啟用儲存體帳戶的加密][1]
2. hello**啟用儲存體加密**刀鋒視窗隨即開啟。 此刀鋒視窗會列出 hello Azure 儲存體帳戶已停用儲存體加密。 在此範例中，我們選取 [storageacct1]。
   ![啟用儲存體加密][2]
3. hello**加密**刀鋒伺服器**storageacct1**隨即開啟。 選取 [啟用] 。
   ![加密刀鋒視窗][3]
4. 選取 [ **儲存**]。

您現在已啟用 **storageacct1** 的儲存體加密。


## <a name="see-also"></a>另請參閱
這份文件範例說明了如何 tooimplement 會 hello 資訊安全中心建議 「 啟用加密的 Azure 儲存體帳戶。 」 toolearn 進一步了解 Azure 儲存體服務加密，請參閱 hello 下列資訊：

* [待用資料的 Azure 儲存體服務加密](../storage/common/storage-service-encryption.md)

toolearn 有關資訊安全中心的詳細資訊，請參閱 hello 下列資訊：

* [在 Azure 資訊安全中心中設定安全性原則](security-center-policies.md)-了解如何 tooconfigure 您的 Azure 訂用帳戶和資源群組的安全性原則。
* [在 Azure 資訊安全中心中的安全性健全狀況監視](security-center-monitoring.md)-了解如何 toomonitor hello 您的 Azure 資源的健全狀況。
* [在 Azure 資訊安全中心警示管理，而且有回應 toosecurity](security-center-managing-and-responding-alerts.md) -了解如何 toomanage 和回應 toosecurity 警示。
* [在 Azure 資訊安全中心管理安全性建議](security-center-recommendations.md) - 了解建議如何協助您保護您的 Azure 資源。
* [Azure 資訊安全中心常見問題集](security-center-faq.md)-尋找使用 hello 服務相關的常見問題集。
* [Azure 安全性部落格](http://blogs.msdn.com/b/azuresecurity/) - 尋找有關 Azure 安全性與合規性的部落格文章。

<!--Image references-->
[1]: ./media/security-center-enable-encryption-for-storage-account/enable-encryption-for-storage-account.png
[2]: ./media/security-center-enable-encryption-for-storage-account/enable-storage-encryption.png
[3]: ./media/security-center-enable-encryption-for-storage-account/encryption-blade.png
