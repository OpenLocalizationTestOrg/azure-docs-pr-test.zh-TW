---
title: "在 Operations Management Suite 安全性和稽核解決方案內監視資源 | Microsoft Docs"
description: "本文件可協助您使用 OMS 安全性和稽核的功能來監視您的資源及識別安全性問題。"
services: operations-management-suite
documentationcenter: na
author: YuriDio
manager: swadhwa
editor: 
ms.assetid: d6752120-821f-4aa7-a049-25bf5a653b95
ms.service: operations-management-suite
ms.custom: oms-security
ms.topic: article
ms.devlang: na
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/30/2017
ms.author: yurid
ms.openlocfilehash: 2f73266b65a4eda6c8751a2d56bc3f11bf4e6a57
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="monitoring-resources-in-operations-management-suite-security-and-audit-solution"></a><span data-ttu-id="f5b62-103">在 Operations Management Suite 安全性和稽核內監視資源</span><span class="sxs-lookup"><span data-stu-id="f5b62-103">Monitoring resources in Operations Management Suite Security and Audit Solution</span></span>
<span data-ttu-id="f5b62-104">本文件可協助您使用 OMS 安全性和稽核的功能來監視您的資源及識別安全性問題。</span><span class="sxs-lookup"><span data-stu-id="f5b62-104">This document helps you use OMS Security and Audit capabilities to monitor your resources and identify security issues.</span></span>

## <a name="what-is-oms"></a><span data-ttu-id="f5b62-105">何謂 OMS？</span><span class="sxs-lookup"><span data-stu-id="f5b62-105">What is OMS?</span></span>
<span data-ttu-id="f5b62-106">Microsoft Operations Management Suite (OMS) 是 Microsoft 的雲端型 IT 管理解決方案，可協助您管理並保護內部部署和雲端基礎結構。</span><span class="sxs-lookup"><span data-stu-id="f5b62-106">Microsoft Operations Management Suite (OMS) is Microsoft's cloud based IT management solution that helps you manage and protect your on-premises and cloud infrastructure.</span></span> <span data-ttu-id="f5b62-107">如需 OMS 的詳細資訊，請閱讀 [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx)一文。</span><span class="sxs-lookup"><span data-stu-id="f5b62-107">For more information about OMS, read the article [Operations Management Suite](https://technet.microsoft.com/library/mt484091.aspx).</span></span>

## <a name="monitoring-resources"></a><span data-ttu-id="f5b62-108">監視資源</span><span class="sxs-lookup"><span data-stu-id="f5b62-108">Monitoring resources</span></span>
<span data-ttu-id="f5b62-109">在盡可能的情況下，您會想要從一開始就防止發生安全性事件。</span><span class="sxs-lookup"><span data-stu-id="f5b62-109">Whenever is possible, you will want to prevent security incidents from happening in the first place.</span></span> <span data-ttu-id="f5b62-110">然而，要防止所有安全性事件是不可能的。</span><span class="sxs-lookup"><span data-stu-id="f5b62-110">However, it is impossible to prevent all security incidents.</span></span> <span data-ttu-id="f5b62-111">當安全性事件發生時，您將需要確保其所帶來的影響為最低。</span><span class="sxs-lookup"><span data-stu-id="f5b62-111">When a security incident does happen, you will need to ensure that its impact is minimized.</span></span>  <span data-ttu-id="f5b62-112">有三項極為重要的建議，可用來將安全性事件的發生次數及影響降至最低︰</span><span class="sxs-lookup"><span data-stu-id="f5b62-112">There are three critical recommendations that can be used to minimize the number and the impact of security incidents:</span></span>

* <span data-ttu-id="f5b62-113">定期評估您環境內的弱點。</span><span class="sxs-lookup"><span data-stu-id="f5b62-113">Routinely assess vulnerabilities in your environment.</span></span>
* <span data-ttu-id="f5b62-114">定期檢查所有電腦系統和網路裝置，確保它們皆已安裝最新的修補程式。</span><span class="sxs-lookup"><span data-stu-id="f5b62-114">Routinely check all computer systems and network devices to ensure that they have all of the latest patches installed.</span></span>
* <span data-ttu-id="f5b62-115">定期檢查所有記錄檔和記錄機制，包括作業系統事件記錄檔、應用程式特定記錄檔,以及入侵偵測系統記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f5b62-115">Routinely check all logs and logging mechanisms, including operating system event logs, application specific logs and intrusion detection system logs.</span></span>

<span data-ttu-id="f5b62-116">OMS 安全性和稽核方案可讓 IT 人員主動監視所有資源，此舉有助於將安全性事件的影響降至最低。</span><span class="sxs-lookup"><span data-stu-id="f5b62-116">OMS Security and Audit solution enables IT to actively monitor all resources, which can help minimize the impact of security incidents.</span></span> <span data-ttu-id="f5b62-117">OMS 安全性和稽核俱備可用來監視資源的安全性網域。</span><span class="sxs-lookup"><span data-stu-id="f5b62-117">OMS Security and Audit has security domains that can be used for monitoring resources.</span></span> <span data-ttu-id="f5b62-118">安全性網域提供了特定選項的快速存取方式，接下來的部份將會涵蓋關於安全性監視下列網域的詳細說明︰</span><span class="sxs-lookup"><span data-stu-id="f5b62-118">The security domains provides quick access to a options, for security monitoring the following domains will be covered in more details:</span></span>

* <span data-ttu-id="f5b62-119">惡意程式碼評估</span><span class="sxs-lookup"><span data-stu-id="f5b62-119">Malware assessment</span></span>
* <span data-ttu-id="f5b62-120">更新評估</span><span class="sxs-lookup"><span data-stu-id="f5b62-120">Update assessment</span></span>
* <span data-ttu-id="f5b62-121">身分識別與存取</span><span class="sxs-lookup"><span data-stu-id="f5b62-121">Identity and Access</span></span>

> [!NOTE]
> <span data-ttu-id="f5b62-122">如需所有這些選項的概觀，請參閱 [開始使用 Operations Management Suite 安全性和稽核解決方案](oms-security-getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="f5b62-122">for an overview of all these options, read [Getting started with Operations Management Suite Security and Audit Solution](oms-security-getting-started.md).</span></span>
> 
> 

### <a name="monitoring-system-protection"></a><span data-ttu-id="f5b62-123">監視系統保護</span><span class="sxs-lookup"><span data-stu-id="f5b62-123">Monitoring system protection</span></span>
<span data-ttu-id="f5b62-124">在深度防禦方法中，對於您資產的整體安全性狀態而言，每個保護層都是極為重要。</span><span class="sxs-lookup"><span data-stu-id="f5b62-124">In a defense in depth approach, every layer of protection is important for the overall security state of your asset.</span></span> <span data-ttu-id="f5b62-125">偵測到威脅及保護效力不足的電腦，會在「安全網域」下的「惡意程式碼評估圖格」內出現。</span><span class="sxs-lookup"><span data-stu-id="f5b62-125">Computers with detected threats and computers with insufficient protection are shown in the Malware Assessment tile under Security Domains.</span></span> <span data-ttu-id="f5b62-126">透過使用「惡意程式碼評估」上的資訊，您可以識別計劃以將保護措施套用在需要的伺服器上。</span><span class="sxs-lookup"><span data-stu-id="f5b62-126">By using the information on the Malware Assessment, you can identify a plan to apply protection to the servers that need it.</span></span> <span data-ttu-id="f5b62-127">若要存取此選項，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f5b62-127">To access this option follow the steps below:</span></span>

1. <span data-ttu-id="f5b62-128">在 [Microsoft Operations Management Suite] 主儀表板內按一下 [安全性和稽核] 圖格。</span><span class="sxs-lookup"><span data-stu-id="f5b62-128">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
   
    ![安全性和稽核](./media/oms-security-responding-alerts/oms-security-responding-alerts-fig1.png)
2. <span data-ttu-id="f5b62-130">在 [安全性和稽核] 儀表板內，按一下 [安全性網域] 下的 [惡意程式碼評估]。</span><span class="sxs-lookup"><span data-stu-id="f5b62-130">In the **Security and Audit** dashboard, click **Antimalware Assessment** under **Security Domains**.</span></span> <span data-ttu-id="f5b62-131">如下所示，[反惡意程式碼評估] 儀表板會出現：</span><span class="sxs-lookup"><span data-stu-id="f5b62-131">The **Antimalware Assessment** dashboard appears as shown below:</span></span>

![惡意程式碼評估](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig2-ga.png)

<span data-ttu-id="f5b62-133">您可以使用 [惡意程式碼評估]  儀表板來識別下列安全性問題：</span><span class="sxs-lookup"><span data-stu-id="f5b62-133">You can use the **Malware Assessment** dashboard to identify the following security issues:</span></span>

* <span data-ttu-id="f5b62-134">[作用中威脅]︰電腦曾受到入侵，而且系統內有作用中威脅。</span><span class="sxs-lookup"><span data-stu-id="f5b62-134">**Active threats**: computers that were compromised and have active threats in the system.</span></span>
* <span data-ttu-id="f5b62-135">[已矯正的威脅]︰電腦曾受到入侵，但已矯正了這些威脅。</span><span class="sxs-lookup"><span data-stu-id="f5b62-135">**Remediated threats**: computers that were compromised but the threats were remediated.</span></span>
* <span data-ttu-id="f5b62-136">[簽章已過期]︰電腦已啟用惡意程式碼保護，但是簽章已過期。</span><span class="sxs-lookup"><span data-stu-id="f5b62-136">**Signature out of date**: computers that have malware protection enabled but the signature is out of date.</span></span>
* <span data-ttu-id="f5b62-137">[沒有即時保護]：電腦並無安裝反惡意程式碼產品。</span><span class="sxs-lookup"><span data-stu-id="f5b62-137">**No real time protection**: computers that don’t have antimalware installed.</span></span>

### <a name="monitoring-updates"></a><span data-ttu-id="f5b62-138">監控更新</span><span class="sxs-lookup"><span data-stu-id="f5b62-138">Monitoring updates</span></span>
<span data-ttu-id="f5b62-139">套用最新的安全性更新是確保安全性的最佳作法，而且應將其納入您的更新管理策略之中。</span><span class="sxs-lookup"><span data-stu-id="f5b62-139">Applying the most recent security updates is a security best practice and it should be incorporated in your update management strategy.</span></span> <span data-ttu-id="f5b62-140">Microsoft Monitoring Agent 服務 (HealthService.exe) 會讀取來自受監視電腦的更新資訊，接著會傳送此更新過的資訊至雲端上的 OMS 服務以進行處理。</span><span class="sxs-lookup"><span data-stu-id="f5b62-140">Microsoft Monitoring Agent service (HealthService.exe) reads update information from monitored computers and then sends this updated information to the OMS service in the cloud for processing.</span></span> <span data-ttu-id="f5b62-141">Microsoft Monitoring Agent 服務會設定為自動服務，而其應一律在目標電腦中執行。</span><span class="sxs-lookup"><span data-stu-id="f5b62-141">The Microsoft Monitoring Agent service is configured as an automatic service and it should be always running in the target computer.</span></span>

![監控更新](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig3.png)

<span data-ttu-id="f5b62-143">會將邏輯套用至更新資料，且雲端服務會記錄資料。</span><span class="sxs-lookup"><span data-stu-id="f5b62-143">Logic is applied to the update data and the cloud service records the data.</span></span> <span data-ttu-id="f5b62-144">如果找到遺失的更新，它們會顯示在 [ **更新** ] 儀表板。</span><span class="sxs-lookup"><span data-stu-id="f5b62-144">If missing updates are found, they are shown on the **Updates** dashboard.</span></span> <span data-ttu-id="f5b62-145">您可以使用 [ **更新** ] 儀表板處理遺失的更新及開發計劃，將它們套用至所需要的伺服器。</span><span class="sxs-lookup"><span data-stu-id="f5b62-145">You can use the **Updates** dashboard to work with missing updates and develop a plan to apply them to the servers that need them.</span></span> <span data-ttu-id="f5b62-146">請遵循下列步驟來存取 [更新]  儀表板：</span><span class="sxs-lookup"><span data-stu-id="f5b62-146">Follow the steps below to access the **Updates** dashboard:</span></span>

1. <span data-ttu-id="f5b62-147">在 [Microsoft Operations Management Suite] 主儀表板內按一下 [安全性和稽核] 圖格。</span><span class="sxs-lookup"><span data-stu-id="f5b62-147">In the **Microsoft Operations Management Suite** main dashboard click **Security and Audit** tile.</span></span>
2. <span data-ttu-id="f5b62-148">在 [安全性和稽核] 儀表板內，按一下 [安全性網域] 下的 [更新評估]。</span><span class="sxs-lookup"><span data-stu-id="f5b62-148">In the **Security and Audit** dashboard, click **Update Assessment** under **Security Domains**.</span></span> <span data-ttu-id="f5b62-149">如下所示，[更新儀表板] 會出現：</span><span class="sxs-lookup"><span data-stu-id="f5b62-149">The Update dashboard appears as shown below:</span></span>

![更新評估](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig4.png)

<span data-ttu-id="f5b62-151">在此儀表板中，您可以執行更新評估來了解您電腦目前的狀態，接著解決最為嚴重的威脅。</span><span class="sxs-lookup"><span data-stu-id="f5b62-151">In this dashboard you can perform an update assessment to understand the current state of your computers and address the most critical threats.</span></span> <span data-ttu-id="f5b62-152">透過使用 [重大或安全性更新]  圖格的方式，IT 系統管理員將能存取遺失的更新詳細資訊，如下所示︰</span><span class="sxs-lookup"><span data-stu-id="f5b62-152">By using the **Critical or Security Updates** tile, IT administrators will be able to access detailed information about the updates that are missing as shown below:</span></span>

![搜尋結果](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig5.png)

<span data-ttu-id="f5b62-154">此報告包含可用來識別此系統容易遭受何種類型威脅攻擊的重要資訊，其中包括與安全性更新相關的 Microsoft 知識庫文章，以及有更多關於弱點詳細資料的 Microsoft 資訊安全公告。</span><span class="sxs-lookup"><span data-stu-id="f5b62-154">This report include critical information that can be used to identify the type of threat this system is vulnerable to, which includes the Microsoft KB articles associated with the security update and the MS Bulletin that has more details about the vulnerability.</span></span>

### <a name="monitoring-identity-and-access"></a><span data-ttu-id="f5b62-155">監視身分識別與存取</span><span class="sxs-lookup"><span data-stu-id="f5b62-155">Monitoring identity and access</span></span>
<span data-ttu-id="f5b62-156">由於使用者有隨處工作、使用不同裝置，以及存取大量雲端及內部部署應用程式的需求，因此務必確保他們的認證能受到保護。</span><span class="sxs-lookup"><span data-stu-id="f5b62-156">With users working from anywhere, using different devices and accessing a vast amount of cloud and on-premises apps, it is imperative that their credentials are protected.</span></span> <span data-ttu-id="f5b62-157">認證竊取攻擊是指攻擊者一開始先取得一般使用者的認證，進而在網路內存取系統。</span><span class="sxs-lookup"><span data-stu-id="f5b62-157">Credential theft attacks are those in which an attacker initially gains access to a regular user’s credentials to access a system within the network.</span></span> <span data-ttu-id="f5b62-158">許多情況下，此初始攻擊僅是取得存取網路權限的一種方式，而終極目標是探索有使用權限的帳戶。</span><span class="sxs-lookup"><span data-stu-id="f5b62-158">Many times, this initial attack is only a way to get access to the network, the ultimate goal is to discover privilege accounts.</span></span> 

<span data-ttu-id="f5b62-159">攻擊者將會在網路內停留，並隨意地使用合適的工具針對工作階段內的其他已登入帳戶來擷取認證。</span><span class="sxs-lookup"><span data-stu-id="f5b62-159">Attackers will stay in the network, using freely available tooling to extract credentials from the sessions of other logged-on accounts.</span></span> <span data-ttu-id="f5b62-160">根據系統組態而定，這些認證可擷取為雜湊、票證或甚至是純文字密碼的格式。</span><span class="sxs-lookup"><span data-stu-id="f5b62-160">Depending on the system configuration, these credentials can be extracted in the form of hashes, tickets, or even plaintext passwords.</span></span>  

> [!NOTE]
> <span data-ttu-id="f5b62-161">直接與網際網路連接的機器，將會看到許多的失敗登入嘗試，都是試著使用各種類型的常用使用者名稱 (例如：系統管理員) 來登入。</span><span class="sxs-lookup"><span data-stu-id="f5b62-161">machines that are directly exposed to the Internet will see many failed attempts that try to login using all kind of well-known usernames (e.g. Administrator).</span></span> <span data-ttu-id="f5b62-162">若是並未使用常用的使用者名稱，而且所使用的密碼強度夠強，在大部分情況下沒有問題。</span><span class="sxs-lookup"><span data-stu-id="f5b62-162">In most cases it is OK if the well-known usernames are not used and if the password is strong enough.</span></span>
> 
> 

<span data-ttu-id="f5b62-163">其實要在這些入侵者危害俱有權限的帳戶之前，就已先行識別是有可能的。</span><span class="sxs-lookup"><span data-stu-id="f5b62-163">It is possible to identify these intruders before they compromise a privilege account.</span></span> <span data-ttu-id="f5b62-164">您可以利用 **OMS 安全性和稽核解決方案** 來監視身分識別與存取。</span><span class="sxs-lookup"><span data-stu-id="f5b62-164">You can leverage **OMS Security and Audit Solution** to monitor identity and access.</span></span> <span data-ttu-id="f5b62-165">請遵循下列步驟來存取 [身分識別與存取]  儀表板：</span><span class="sxs-lookup"><span data-stu-id="f5b62-165">Follow the steps below to access the **Identity and Access** dashboard:</span></span>

1. <span data-ttu-id="f5b62-166">在 [Microsoft Operations Management Suite]  主儀表板內按一下 [安全性和稽核] 圖格。</span><span class="sxs-lookup"><span data-stu-id="f5b62-166">In the **Microsoft Operations Management Suite** main dashboard click Security and Audit tile.</span></span>
2. <span data-ttu-id="f5b62-167">在 [安全性和稽核] 儀表板內，按一下 [安全性網域] 下的 [身分識別與存取]。</span><span class="sxs-lookup"><span data-stu-id="f5b62-167">In the **Security and Audit** dashboard, click **Identity and Access** under **Security Domains**.</span></span> <span data-ttu-id="f5b62-168">如下所示，[身分識別與存取] 儀表板會出現：</span><span class="sxs-lookup"><span data-stu-id="f5b62-168">The **Identity and Access** dashboard appears as shown below:</span></span>

![身分識別與存取](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig6-ga.png)

<span data-ttu-id="f5b62-170">作為定期監視策略的一部分，您必須包含身分識別監視。</span><span class="sxs-lookup"><span data-stu-id="f5b62-170">As part of your regular monitoring strategy, you must include identity monitoring.</span></span> <span data-ttu-id="f5b62-171">IT 系統管理員應查看是否有特定的有效使用者名稱，出現多次登入嘗試的情況。</span><span class="sxs-lookup"><span data-stu-id="f5b62-171">IT Admin should look if there is a specific valid username that has many attempts.</span></span> <span data-ttu-id="f5b62-172">這可能代表攻擊者已取得實際的使用者名稱，接著嘗試進行暴力密碼破解，或是使用透過已過期硬式編碼密碼的自動工具進行破解。</span><span class="sxs-lookup"><span data-stu-id="f5b62-172">This might indicate either attacker that acquired the real username and try to brute force or an automatic tool that uses hard-coded password that expired.</span></span>

<span data-ttu-id="f5b62-173">此儀表板可讓 IT 人員迅速地判斷和身分識別與存取公司資源相關的潛在威脅。</span><span class="sxs-lookup"><span data-stu-id="f5b62-173">This dashboard enable IT to quickly identify potential threats related to identity and access to company’s resources.</span></span> <span data-ttu-id="f5b62-174">而在識別潛在趨勢上，其亦特別重要，例如：在 [登入經過時間] 圖格上，您可以看到過往期間曾進行過的失敗登入嘗試次數。</span><span class="sxs-lookup"><span data-stu-id="f5b62-174">It is particular important to also identify potential trends, for example in the Logons Over Time tile, you can see over period of time how many times a failed logon attempt was performed.</span></span> <span data-ttu-id="f5b62-175">在此案例中， **FileServer** 電腦已接收到 35 次登入嘗試。</span><span class="sxs-lookup"><span data-stu-id="f5b62-175">In this case the computer **FileServer** received 35 logon attempts.</span></span> <span data-ttu-id="f5b62-176">只要按一下該項目，您就可以瞭解更多關於此電腦的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f5b62-176">You can explore more details about this computer by clicking on it.</span></span> 

![其他詳細資訊](./media/oms-security-monitoring-resources/oms-security-monitoring-resources-fig7-new.png)

<span data-ttu-id="f5b62-178">為此電腦而產生的報告，提供了與此模式相關的有用詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="f5b62-178">The report generated for this computer brings valuable details about this pattern.</span></span> <span data-ttu-id="f5b62-179">請注意，**ACCOUNT** 資料行提供您用於嘗試存取系統的使用者帳戶，而 **TIMEGENERATED** 資料行提供您已進行嘗試的時間間隔，至於 **LOGONTYPENAME** 資料行則提供您進行此嘗試的所在位置。</span><span class="sxs-lookup"><span data-stu-id="f5b62-179">Noticed that the **ACCOUNT** column gives you the user account that was used to try to access the system, the **TIMEGENERATED** column gives you the time interval in which the attempt was done and the **LOGONTYPENAME** column gives you the location where this attempt was done.</span></span> <span data-ttu-id="f5b62-180">如果這些嘗試是在本機內透過程式所進行，則 **PROCESS** 資料行會顯示處理程序的名稱。</span><span class="sxs-lookup"><span data-stu-id="f5b62-180">If these attempts were performed locally in the system by a program, the **PROCESS** column would be showing the process’s name.</span></span> <span data-ttu-id="f5b62-181">在透過程式所進行的登入嘗試案例中，您已取得可用的處理程序名稱，現在您可以在目標系統內進行更進一步的調查。</span><span class="sxs-lookup"><span data-stu-id="f5b62-181">In scenarios where the logon attempt is coming from a program, you already have the process name available and now you can perform further investigation in the target system.</span></span>

## <a name="see-also"></a><span data-ttu-id="f5b62-182">另請參閱</span><span class="sxs-lookup"><span data-stu-id="f5b62-182">See also</span></span>
<span data-ttu-id="f5b62-183">在本文件中，您已了解如何使用「OMS 安全性和稽核」解決方案來監視您的資源。</span><span class="sxs-lookup"><span data-stu-id="f5b62-183">In this document, you learned how to use OMS Security and Audit solution to monitor your resources.</span></span> <span data-ttu-id="f5b62-184">若要深入了解 OMS 安全性，請參閱下列文章：</span><span class="sxs-lookup"><span data-stu-id="f5b62-184">To learn more about OMS Security, see the following articles:</span></span>

* [<span data-ttu-id="f5b62-185">Operations Management Suite (OMS) 概觀</span><span class="sxs-lookup"><span data-stu-id="f5b62-185">Operations Management Suite (OMS) overview</span></span>](operations-management-suite-overview.md)
* [<span data-ttu-id="f5b62-186">開始使用 Operations Management Suite 安全性和稽核解決方案</span><span class="sxs-lookup"><span data-stu-id="f5b62-186">Getting started with Operations Management Suite Security and Audit Solution</span></span>](oms-security-getting-started.md)
* [<span data-ttu-id="f5b62-187">在 Operations Management Suite 安全性和稽核內監視及回應安全性警示</span><span class="sxs-lookup"><span data-stu-id="f5b62-187">Monitoring and Responding to Security Alerts in Operations Management Suite Security and Audit Solution</span></span>](oms-security-responding-alerts.md)

