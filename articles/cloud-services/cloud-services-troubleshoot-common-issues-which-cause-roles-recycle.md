---
title: "雲端服務角色回收的原因的 aaaCommon |Microsoft 文件"
description: "突然回收的雲端服務角色可能會造成顯著的停機時間。 以下是一些常見的問題會造成角色 toobe 回收，這能協助您降低停機時間。"
services: cloud-services
documentationcenter: 
author: simonxjx
manager: felixwu
editor: 
tags: top-support-issue
ms.assetid: 533930d1-8035-4402-b16a-cf887b2c4f85
ms.service: cloud-services
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: tbd
ms.date: 7/26/2017
ms.author: v-six
ms.openlocfilehash: 8fa152b33d2b22a8a02f834d4bc38519b4272f7b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="common-issues-that-cause-roles-toorecycle"></a>常見的問題，導致角色 toorecycle
本文將討論一些 hello 的部署問題的常見原因，並提供疑難排解秘訣 toohelp 解決這些問題。 Hello 角色執行個體失敗 toostart，或 hello 初始化、 忙碌和停止狀態之間循環時，應用程式有問題的指示。

[!INCLUDE [support-disclaimer](../../includes/support-disclaimer.md)]

## <a name="missing-runtime-dependencies"></a>遺失執行階段相依性
如果您的應用程式中的角色不屬於 hello 任何組件所依賴.NET Framework 或 hello Azure 受管理程式庫，您必須明確 hello 應用程式封裝中包含該組件。 請記住，其他 Microsoft 架構依預設並未在 Azure 上提供。 如果您的角色依賴這類架構，您必須先將這些組件 toohello 應用程式封裝。

您建置並封裝您的應用程式之前，請確認下列 hello:

* 如果使用 Visual studio，請確定 hello**複製到本機**屬性設定太**True**每個參考的組件的專案不是 hello Azure SDK 的一部分或 hello.NET Framework。
* 請確定 hello web.config 檔案並未參考任何未使用的組件以 hello compilation 項目。
* hello**建置動作**每個.cshtml 檔案設定太**內容**。 這可確保 hello 檔案會正確出現在 hello 封裝，並讓其他的參照的檔案 tooappear hello 封裝中。

## <a name="assembly-targets-wrong-platform"></a>組件以錯誤的平台作為目標
Azure 是 64 位元環境。 因此，針對 32 位元目標編譯的 .NET 組件無法在 Azure 上運作。

## <a name="role-throws-unhandled-exceptions-while-initializing-or-stopping"></a>角色在初始化或停止時會擲回未處理的例外狀況
Hello hello 方法所擲回任何例外狀況[RoleEntryPoint]類別，其中包含 hello [OnStart]， [OnStop]，和[執行]方法，都是未處理例外狀況。 如果未處理的例外狀況發生在其中一種方法，就會回收 hello 角色。 如果 hello 角色重複回收，它可能會擲回未處理例外狀況，它會嘗試 toostart 每次。

## <a name="role-returns-from-run-method"></a>角色因 Run 方法而回收
hello[執行]方法是預定的 toorun 無限期。 如果您的程式碼會覆寫 hello[執行]方法，它應該睡眠無限期。 如果 hello[執行]方法傳回時，hello 角色回收。

## <a name="incorrect-diagnosticsconnectionstring-setting"></a>不正確的 DiagnosticsConnectionString 設定
如果應用程式使用 Azure 診斷，您的服務組態檔必須指定 hello`DiagnosticsConnectionString`組態設定。 這項設定應該指定在 Azure 中的 HTTPS 連線 tooyour 儲存體帳戶。

tooensure，您`DiagnosticsConnectionString`設定是否正確，然後再部署您的應用程式封裝 tooAzure、 hello 下列驗證：  

* hello`DiagnosticsConnectionString`在 Azure 中設定點 tooa 有效的儲存體帳戶。  
  根據預設，此設定點 toohello 模擬儲存體帳戶，讓您部署應用程式套件之前，您必須明確變更這個設定。 如果您不要變更此設定，hello 角色執行個體會嘗試 toostart hello 診斷監視器時，會擲回例外狀況。 這將造成 hello 角色執行個體 toorecycle 無限期。
* hello 連接字串中指定 hello 下列[格式](../storage/common/storage-configure-connection-string.md)。 （hello 通訊協定必須指定為 HTTPS）。取代*MyAccountName* hello 儲存體帳戶名稱和*MyAccountKey*與您的存取金鑰：    

        DefaultEndpointsProtocol=https;AccountName=MyAccountName;AccountKey=MyAccountKey

  如果您正在使用 Azure Tools for Microsoft Visual Studio 開發您的應用程式，您可以使用 hello 屬性頁 tooset 此值。

## <a name="exported-certificate-does-not-include-private-key"></a>匯出的憑證未包含私密金鑰
toorun web 角色在 SSL 下，您必須確保匯出的管理憑證包含 hello 的私密金鑰。 如果您使用 hello *Windows 憑證管理員*tooexport hello 憑證，可確定 tooselect**是**hello**匯出 hello 私密金鑰**選項。 hello 憑證必須匯出 hello PFX 格式是 hello 目前支援的唯一格式。

## <a name="next-steps"></a>後續步驟
檢視更多雲端服務的 [疑難排解文章](https://azure.microsoft.com/documentation/articles/?tag=top-support-issue&product=cloud-services) 。

在以下位置檢視多個角色回收案例： [Kevin Williamson 的部落格系列](http://blogs.msdn.com/b/kwill/archive/2013/08/09/windows-azure-paas-compute-diagnostics-data.aspx)。

[RoleEntryPoint]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.aspx
[OnStart]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstart.aspx
[OnStop]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.onstop.aspx
[執行]: https://msdn.microsoft.com/library/microsoft.windowsazure.serviceruntime.roleentrypoint.run.aspx
