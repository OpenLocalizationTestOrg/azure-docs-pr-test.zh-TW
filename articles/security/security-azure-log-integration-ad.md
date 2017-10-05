---
title: "使用 Azure Active Directory 稽核記錄進行 Azure 記錄整合 | Microsoft Docs"
description: "了解如何安裝 Azure 記錄整合服務，整合 Azure 的稽核記錄檔"
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
ms.openlocfilehash: 8a1295cc86057ed72940e774d0bd423d61142e31
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/29/2017
---
# <a name="integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="12712-103">整合 Azure Active Directory 稽核記錄</span><span class="sxs-lookup"><span data-stu-id="12712-103">Integrate Azure Active Directory audit logs</span></span>

<span data-ttu-id="12712-104">Azure Active Directory (Azure AD) 稽核事件可協助您識別 Azure Active Directory 中發生的特殊權限動作。</span><span class="sxs-lookup"><span data-stu-id="12712-104">Azure Active Directory (Azure AD) audit events help you identify privileged actions that occurred in Azure Active Directory.</span></span> <span data-ttu-id="12712-105">您可以藉由檢視 [Azure Active Directory 稽核報告事件](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md)看到您可以追蹤的事件類型。</span><span class="sxs-lookup"><span data-stu-id="12712-105">You can see the types of events that you can track by reviewing [Azure Active Directory audit report events](/active-directory/active-directory-reporting-audit-events#list-of-audit-report-events.md).</span></span>

> [!NOTE]
> <span data-ttu-id="12712-106">在嘗試執行本文中的步驟之前，您必須先檢閱[開始使用](security-azure-log-integration-get-started.md)一文並完成此處的步驟。</span><span class="sxs-lookup"><span data-stu-id="12712-106">Before you attempt the steps in this article, you must review the [Get started](security-azure-log-integration-get-started.md) article and complete the steps there.</span></span>

## <a name="steps-to-integrate-azure-active-directory-audit-logs"></a><span data-ttu-id="12712-107">整合 Azure Active Directory 稽核記錄的步驟</span><span class="sxs-lookup"><span data-stu-id="12712-107">Steps to integrate Azure Active directory audit logs</span></span>

1. <span data-ttu-id="12712-108">開啟命令提示字元並執行此命令：</span><span class="sxs-lookup"><span data-stu-id="12712-108">Open the command prompt and run this command:</span></span>

   ``cd c:\Program Files\Microsoft Azure Log Integration``

2. <span data-ttu-id="12712-109">請執行這個命令：</span><span class="sxs-lookup"><span data-stu-id="12712-109">Run this command:</span></span> 
 
   ``azlog createazureid``

   <span data-ttu-id="12712-110">此命令會提示您登入 Azure。</span><span class="sxs-lookup"><span data-stu-id="12712-110">This command prompts you for your Azure login.</span></span> <span data-ttu-id="12712-111">此命令接著會建立託管 Azure 訂用帳戶 (其中登入的使用者是系統管理員、共同管理員或擁有者) 的 Azure AD 租用戶中的 Azure Active Directory 服務主體。</span><span class="sxs-lookup"><span data-stu-id="12712-111">The command then creates an Azure Active Directory service principal in the Azure AD tenants that host the Azure subscriptions in which the logged-in user is an administrator, a co-administrator, or an owner.</span></span> <span data-ttu-id="12712-112">若登入的使用者只是 Azure AD 租用戶中的來賓使用者，則此命令將會失敗。</span><span class="sxs-lookup"><span data-stu-id="12712-112">The command will fail if the logged-in user is only a guest user in the Azure AD tenant.</span></span> <span data-ttu-id="12712-113">對 Azure 的驗證會透過 Azure AD 來進行。</span><span class="sxs-lookup"><span data-stu-id="12712-113">Authentication to Azure is done through Azure AD.</span></span> <span data-ttu-id="12712-114">建立 Azure 記錄整合的服務主體會建立 Azure AD 身分識別，以獲得 Azure 訂用帳戶的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="12712-114">Creating a service principal for Azure Log Integration creates the Azure AD identity that is given access to read from Azure subscriptions.</span></span>

3. <span data-ttu-id="12712-115">執行下列命令以提供您的租用戶識別碼。</span><span class="sxs-lookup"><span data-stu-id="12712-115">Run the following command to provide your tenant ID.</span></span> <span data-ttu-id="12712-116">您必須是租用戶系統管理員角色的成員才能執行命令。</span><span class="sxs-lookup"><span data-stu-id="12712-116">You need to be member of the tenant admin role to run the command.</span></span>

   ``Azlog.exe authorizedirectoryreader tenantId``

   <span data-ttu-id="12712-117">範例：</span><span class="sxs-lookup"><span data-stu-id="12712-117">Example:</span></span>

   ``AZLOG.exe authorizedirectoryreader ba2c0000-d24b-4f4e-92b1-48c4469999``

4. <span data-ttu-id="12712-118">檢查下列資料夾以確認其中是否建立了 Azure Active Directory 稽核記錄 JSON 檔案：</span><span class="sxs-lookup"><span data-stu-id="12712-118">Check the following folders to confirm that the Azure Active Directory audit log JSON files are created in them:</span></span>

   * <span data-ttu-id="12712-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span><span class="sxs-lookup"><span data-stu-id="12712-119">**C:\Users\azlog\AzureActiveDirectoryJson**</span></span>
   * <span data-ttu-id="12712-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span><span class="sxs-lookup"><span data-stu-id="12712-120">**C:\Users\azlog\AzureActiveDirectoryJsonLD**</span></span>

<span data-ttu-id="12712-121">下列影片會示範本文所述的步驟：</span><span class="sxs-lookup"><span data-stu-id="12712-121">The following video demonstrates the steps covered in this article:</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure-Security-Videos/Azure-Log-Integration-Videos-Azure-AD-Integration/player]


> [!NOTE]
> <span data-ttu-id="12712-122">如需有關將 JSON 檔案中的資訊帶入到安全性資訊和事件管理 (SIEM) 系統的特定指示，請連絡您的 SIEM 廠商。</span><span class="sxs-lookup"><span data-stu-id="12712-122">For specific instructions on bringing the information in the JSON files into your security information and event management (SIEM) system, contact your SIEM vendor.</span></span>

<span data-ttu-id="12712-123">可透過 [Azure 記錄檔整合 MSDN 論壇](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration)取得社群協助。</span><span class="sxs-lookup"><span data-stu-id="12712-123">Community assistance is available through the [Azure Log Integration MSDN Forum](https://social.msdn.microsoft.com/Forums/office/home?forum=AzureLogIntegration).</span></span> <span data-ttu-id="12712-124">此論壇可透過分享問題、解答、秘訣和技巧，讓 Azure 記錄整合社群的成員彼此支援。</span><span class="sxs-lookup"><span data-stu-id="12712-124">This forum enables people in the Azure Log Integration community to support each other with questions, answers, tips, and tricks.</span></span> <span data-ttu-id="12712-125">此外，Azure 記錄整合小組會監看這個論壇，並且會盡全力提供協助。</span><span class="sxs-lookup"><span data-stu-id="12712-125">In addition, the Azure Log Integration team monitors this forum and helps whenever it can.</span></span>

<span data-ttu-id="12712-126">您也可以建立[支援要求](../azure-supportability/how-to-create-azure-support-request.md)。</span><span class="sxs-lookup"><span data-stu-id="12712-126">You can also open a [support request](../azure-supportability/how-to-create-azure-support-request.md).</span></span> <span data-ttu-id="12712-127">選取 [記錄整合] 作為您要求支援的服務。</span><span class="sxs-lookup"><span data-stu-id="12712-127">Select **Log Integration** as the service for which you are requesting support.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12712-128">後續步驟</span><span class="sxs-lookup"><span data-stu-id="12712-128">Next steps</span></span>
<span data-ttu-id="12712-129">若要深入了解 Azure 記錄整合，請參閱：</span><span class="sxs-lookup"><span data-stu-id="12712-129">To learn more about Azure Log Integration, see:</span></span>

* <span data-ttu-id="12712-130">[Azure 記錄的 Microsoft Azure 記錄整合](https://www.microsoft.com/download/details.aspx?id=53324)：此下載中心頁面會提供關於 Azure 記錄整合的詳細資料、系統需求和安裝指示。</span><span class="sxs-lookup"><span data-stu-id="12712-130">[Microsoft Azure Log Integration for Azure logs](https://www.microsoft.com/download/details.aspx?id=53324): This Download Center page gives details, system requirements, and installation instructions for Azure Log Integration.</span></span>
* <span data-ttu-id="12712-131">[Azure 記錄整合簡介](security-azure-log-integration-overview.md)：本文會為您介紹 Azure 記錄整合、其主要功能以及運作方式。</span><span class="sxs-lookup"><span data-stu-id="12712-131">[Introduction to Azure Log Integration](security-azure-log-integration-overview.md): This article introduces you to Azure Log Integration, its key capabilities, and how it works.</span></span>
* <span data-ttu-id="12712-132">[合作夥伴設定步驟](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/)：此部落格文章說明如何設定 Azure 記錄整合，以搭配使用合作夥伴解決方案 Splunk、HP ArcSight 和 IBM QRadar。</span><span class="sxs-lookup"><span data-stu-id="12712-132">[Partner configuration steps](https://blogs.msdn.microsoft.com/azuresecurity/2016/08/23/azure-log-siem-configuration-steps/): This blog post shows you how to configure Azure Log Integration to work with partner solutions Splunk, HP ArcSight, and IBM QRadar.</span></span>
* <span data-ttu-id="12712-133">[Azure 記錄整合常見問題集](security-azure-log-integration-faq.md)：本文提供 Azure 記錄整合的相關問題解答。</span><span class="sxs-lookup"><span data-stu-id="12712-133">[Azure Log Integration FAQ](security-azure-log-integration-faq.md): This article answers questions about Azure Log Integration.</span></span>
* <span data-ttu-id="12712-134">[以 Azure 記錄整合來整合資訊安全中心警示](../security-center/security-center-integrating-alerts-with-log-integration.md)：本文會說明如何將資訊安全中心警示以及 Azure 診斷和 Azure 稽核記錄檔所收集的虛擬機器安全性事件，與您的 Log Analytics 或 SIEM 方案進行同步處理。</span><span class="sxs-lookup"><span data-stu-id="12712-134">[Integrating Security Center alerts with Azure Log Integration](../security-center/security-center-integrating-alerts-with-log-integration.md): This article shows you how to sync Security Center alerts, along with virtual machine security events collected by Azure Diagnostics and Azure audit logs, with your log analytics or SIEM solution.</span></span>
* <span data-ttu-id="12712-135">[Azure 診斷和 Azure 稽核記錄的新功能](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/)：此部落格文章為您介紹 Azure 稽核記錄和其他功能，協助您深入了解您的 Azure 資源的作業。</span><span class="sxs-lookup"><span data-stu-id="12712-135">[New features for Azure Diagnostics and Azure audit logs](https://azure.microsoft.com/blog/new-features-for-azure-diagnostics-and-azure-audit-logs/): This blog post introduces you to Azure audit logs and other features that help you gain insights into the operations of your Azure resources.</span></span>
