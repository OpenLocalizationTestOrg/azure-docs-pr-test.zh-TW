---
title: "與 Azure Active Directory 稽核記錄檔的記錄檔整合 aaaAzure |Microsoft 文件"
description: "了解 tooinstall hello Azure 記錄檔整合服務，並整合來自 Azure 稽核記錄檔記錄檔"
services: security
documentationcenter: na
author: Barclayn
manager: MBaldwin
editor: TomShinder
ms.assetid: 
ms.service: security
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ums.workload: na
ms.date: 08/08/2017
ms.author: barclayn
ms.custom: azlog
ms.openlocfilehash: 3ee8fa3b8b5e9bd33202e57ed5327cd8d3127f00
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="33f6d-103">整合 Azure Active Directory 稽核記錄</span><span class="sxs-lookup"><span data-stu-id="33f6d-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="33f6d-104">Azure Active Directory (Azure AD) 稽核事件可協助您識別 Azure Active Directory 中發生的特殊權限動作。</span><span class="sxs-lookup"><span data-stu-id="33f6d-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="33f6d-105">您可以查看您可以藉由檢視追蹤的事件 hello 類型[Azure Active Directory 稽核報告事件](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md)。</span><span class="sxs-lookup"><span data-stu-id="33f6d-105">You can see hello types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="33f6d-106">您嘗試在本文中的 hello 步驟之前，您必須檢閱 hello[開始](security-azure-log-integration-get-started.md)發行項，並完成 hello 步驟。</span><span class="sxs-lookup"><span data-stu-id="33f6d-106">Before you attempt hello steps in this article, you must review hello [Get started](security-azure-log-integration-get-started.md) article and complete hello steps there.</span></span>

## <a name="steps-toointegrate-azure-active-directory-audit-logs"></a><span data-ttu-id="33f6d-107">步驟 toointegrate Azure Active directory 稽核記錄檔</span><span class="sxs-lookup"><span data-stu-id="33f6d-107">Steps toointegrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="33f6d-108">開啟 hello 命令提示字元並執行此命令：</span><span class="sxs-lookup"><span data-stu-id="33f6d-108">Open hello command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="33f6d-109">請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="33f6d-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="33f6d-110">此命令會提示您登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="33f6d-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="33f6d-111">hello 命令接著會建立 Azure Active Directory 服務主體在 hello Azure AD 租用戶主機 hello Azure 訂用帳戶中的 hello 登入的使用者是系統管理員、 共同管理員或擁有者。</span><span class="sxs-lookup"><span data-stu-id="33f6d-111">hello command then creates an Azure Active Directory service principal in hello Azure AD tenants that host hello Azure subscriptions in which hello logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="33f6d-112">如果 hello 登入的使用者是只 hello Azure AD 租用戶中的 guest 使用者，hello 命令會失敗。</span><span class="sxs-lookup"><span data-stu-id="33f6d-112">hello command will fail if hello logged-in user is only a guest user in hello Azure AD tenant.</span></span> <span data-ttu-id="33f6d-113">驗證 tooAzure 是透過 Azure AD。</span><span class="sxs-lookup"><span data-stu-id="33f6d-113">Authentication tooAzure is done through Azure AD.</span></span> <span data-ttu-id="33f6d-114">建立 Azure 記錄檔整合的服務主體建立 hello 根據存取 tooread 指定 Azure 訂用帳戶的 Azure AD 身分識別。</span><span class="sxs-lookup"><span data-stu-id="33f6d-114">Creating a service principal for Azure Log Integration creates hello Azure AD identity that is given access tooread from Azure subscriptions.</span></span>

3. <span data-ttu-id="33f6d-115">執行下列命令 tooprovide hello 您的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="33f6d-115">Run hello following command tooprovide your tenant ID.</span></span> <span data-ttu-id="33f6d-116">您需要 hello 租用戶系統管理員角色 toorun hello 命令 toobe 的成員。</span><span class="sxs-lookup"><span data-stu-id="33f6d-116">You need toobe member of hello tenant admin role toorun hello command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="33f6d-117">範例：</span><span class="sxs-lookup"><span data-stu-id="33f6d-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="33f6d-118">請檢查下列 hello Azure Active Directory 的稽核記錄檔 JSON 檔案的資料夾 tooconfirm hello 中加以建立：</span><span class="sxs-lookup"><span data-stu-id="33f6d-118">Check hello following folders tooconfirm that hello Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="33f6d-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="33f6d-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="33f6d-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="33f6d-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="33f6d-121">hello 下列影片示範 hello 涵蓋在本文中的步驟：</span><span class="sxs-lookup"><span data-stu-id="33f6d-121">hello following video demonstrates hello steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="33f6d-122">如需有關將在 hello JSON 檔案中的 hello 資訊送回您的安全性資訊和事件管理 (SIEM) 系統的特定指示，請連絡您的 SIEM 廠商。</span><span class="sxs-lookup"><span data-stu-id="33f6d-122">For specific instructions on bringing hello information in hello JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="33f6d-123">社群協助是透過 hello [Azure 記錄檔整合 MSDN 論壇](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration)。</span><span class="sxs-lookup"><span data-stu-id="33f6d-123">Community assistance is available through hello [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="33f6d-124">此論壇可讓使用者在 hello Azure 記錄檔整合社群 toosupport 彼此與問題、 解答、 秘訣與訣竅。</span><span class="sxs-lookup"><span data-stu-id="33f6d-124">This forum enables people in hello Azure Log Integration community toosupport each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="33f6d-125">此外，hello Azure 記錄檔整合小組監視此論壇，而且只要它可以幫助。</span><span class="sxs-lookup"><span data-stu-id="33f6d-125">In addition, hello Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="33f6d-126">您也可以建立[支援要求](../azure-supportability/how-to-create-azure-support-request.md)。</span><span class="sxs-lookup"><span data-stu-id="33f6d-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="33f6d-127">選取**記錄 Integration**為 hello 服務您要求支援。</span><span class="sxs-lookup"><span data-stu-id="33f6d-127">Select **Log Integration** as hello service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="33f6d-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="33f6d-128">Next steps</span></span>
<span data-ttu-id="33f6d-129">toolearn 進一步了解 Azure 記錄檔整合，請參閱：</span><span class="sxs-lookup"><span data-stu-id="33f6d-129">toolearn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="33f6d-130">[Azure 記錄的 Microsoft Azure 記錄整合](https://www.microsoft.com/download/details.aspx?id=53324)：此下載中心頁面會提供關於 Azure 記錄整合的詳細資料、系統需求和安裝指示。</span><span class="sxs-lookup"><span data-stu-id="33f6d-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="33f6d-131">[簡介 tooAzure 記錄 Integration](security-azure-log-integration-overview.md)： 本文介紹您 tooAzure 記錄整合、 其重要功能，和它的運作方式。</span><span class="sxs-lookup"><span data-stu-id="33f6d-131">[Introduction tooAzure Log Integration](security-azure-log-integration-overview.md): This article introduces you tooAzure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="33f6d-132">[夥伴的設定步驟](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/)： 此部落格文章會示範如何與 tooconfigure Azure 記錄檔整合 toowork 夥伴解決方案 Splunk，HP 討論 ArcSight 和 IBM QRadar。</span><span class="sxs-lookup"><span data-stu-id="33f6d-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how tooconfigure Azure Log Integration toowork with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="33f6d-133">[Azure 記錄整合常見問題集](security-azure-log-integration-faq.md)：本文提供 Azure 記錄整合的相關問題解答。</span><span class="sxs-lookup"><span data-stu-id="33f6d-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="33f6d-134">[資訊安全中心警示整合搭配 Azure 記錄檔整合](../security-center/security-center-integrating-alerts-with-log-integration.md)： 本文章將示範如何 toosync 資訊安全中心發出警示通知，以及虛擬機器的安全性事件收集 Azure 診斷和記錄分析 Azure 稽核記錄檔，或SIEM 解決方案。</span><span class="sxs-lookup"><span data-stu-id="33f6d-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how toosync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="33f6d-135">[新功能的 Azure 診斷及 Azure 稽核記錄檔](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/)： 此部落格文章向您介紹 tooAzure 稽核記錄檔和其他功能，可協助您深入了解您的 Azure 資源的 hello 作業。</span><span class="sxs-lookup"><span data-stu-id="33f6d-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you tooAzure audit logs and other features that help you gain insights into hello operations of your Azure resources.</span></span>
