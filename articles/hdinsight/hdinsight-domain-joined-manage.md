---
title: "管理已加入網域的 HDInsight 叢集 - Azure | Microsoft Docs"
description: "了解如何管理已加入網域的 HDInsight 叢集"
services: hdinsight
documentationcenter: 
author: saurinsh
manager: jhubbard
editor: cgronlun
tags: 
ms.assetid: 6ebc4d2f-2f6a-4e1e-ab6d-af4db6b4c87c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/25/2016
ms.author: saurinsh
ms.openlocfilehash: 9b56ce6cc5bdd3b8d48d047751e978cad08598e1
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/11/2017
---
# <a name="manage-domain-joined-hdinsight-clusters-preview"></a><span data-ttu-id="4eb96-103">管理已加入網域的 HDInsight 叢集 (預覽)</span><span class="sxs-lookup"><span data-stu-id="4eb96-103">Manage Domain-joined HDInsight clusters (Preview)</span></span>
<span data-ttu-id="4eb96-104">認識已加入網域的 HDInsight 叢集中的使用者和角色，了解如何管理已加入網域的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="4eb96-104">Learn the users and the roles in Domain-joined HDInsight, and how to manage domain-joined HDInsight clusters.</span></span>

## <a name="users-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="4eb96-105">已加入網域的 HDInsight 叢集的使用者</span><span class="sxs-lookup"><span data-stu-id="4eb96-105">Users of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="4eb96-106">未加入網域的 HDInsight 叢集有兩個使用者帳戶，是在叢集建立期間建立的︰</span><span class="sxs-lookup"><span data-stu-id="4eb96-106">An HDInsight cluster that is not domain-joined has two user accounts that are created during the cluster creation:</span></span>

* <span data-ttu-id="4eb96-107">**Ambari 系統管理員**：此帳戶亦稱為「Hadoop 使用者」或「HTTP 使用者」。</span><span class="sxs-lookup"><span data-stu-id="4eb96-107">**Ambari admin**: This account is also known as *Hadoop user* or *HTTP user*.</span></span> <span data-ttu-id="4eb96-108">此帳戶可以用來登入 Ambari，網址是 https://&lt;clustername>.azurehdinsight.net。</span><span class="sxs-lookup"><span data-stu-id="4eb96-108">This account can be used to log on to Ambari at https://&lt;clustername>.azurehdinsight.net.</span></span> <span data-ttu-id="4eb96-109">它也可以用來在 Ambari 檢視上執行查詢、透過外部工具 (即 PowerShell、Templeton、Visual Studio)執行作業、以及使用 Hive ODBC 驅動程式和 BI 工具 (即 Excel、PowerBI、或 Tableau) 進行驗證。</span><span class="sxs-lookup"><span data-stu-id="4eb96-109">It can also be used to run queries on Ambari views, execute jobs via external tools (i.e. PowerShell, Templeton, Visual Studio), and authenticate with the Hive ODBC driver and BI tools (i.e. Excel, PowerBI, or Tableau).</span></span>
* <span data-ttu-id="4eb96-110">**SSH 使用者**︰此帳戶可以搭配 SSH 使用，執行 sudo 命令。</span><span class="sxs-lookup"><span data-stu-id="4eb96-110">**SSH user**:  This account can be used with SSH, and execute sudo commands.</span></span> <span data-ttu-id="4eb96-111">它具有 Linux VM 上的根權限。</span><span class="sxs-lookup"><span data-stu-id="4eb96-111">It has root privileges to the Linux VMs.</span></span>

<span data-ttu-id="4eb96-112">除了 Ambari 系統管理員和 SSH 使用者之外，已加入網域的 HDInsight 叢集有三個新的使用者。</span><span class="sxs-lookup"><span data-stu-id="4eb96-112">A domain-joined HDInsight cluster has three new users in addition to Ambari Admin and SSH user.</span></span>

* <span data-ttu-id="4eb96-113">**Ranger 系統管理員**︰此帳戶是本機的 Apache Ranger 系統管理員帳戶。</span><span class="sxs-lookup"><span data-stu-id="4eb96-113">**Ranger admin**:  This account is the local Apache Ranger admin account.</span></span> <span data-ttu-id="4eb96-114">不是 Active Directory 網域使用者。</span><span class="sxs-lookup"><span data-stu-id="4eb96-114">It is not an active directory domain user.</span></span> <span data-ttu-id="4eb96-115">此帳戶可以用來設定原則、將其他使用者設為系統管理員、或委派系統管理工作 (讓某些使用者可以管理原則)。</span><span class="sxs-lookup"><span data-stu-id="4eb96-115">This account can be used to setup policies and make other users admins or delegated admins (so that those users can manage policies).</span></span> <span data-ttu-id="4eb96-116">預設的使用者名稱是 admin，密碼則是與 Ambari 系統管理員的密碼相同。</span><span class="sxs-lookup"><span data-stu-id="4eb96-116">By default, the username is *admin* and the password is the same as the Ambari admin password.</span></span> <span data-ttu-id="4eb96-117">可以在 Ranger 的 [設定] 頁面中更新密碼。</span><span class="sxs-lookup"><span data-stu-id="4eb96-117">The password can be updated from the Settings page in Ranger.</span></span>
* <span data-ttu-id="4eb96-118">**叢集系統管理員網域使用者**︰此帳戶是被指定為 Hadoop 叢集系統管理員 (包括 Ambari 和 Ranger) 的 Active Directory 網域使用者。</span><span class="sxs-lookup"><span data-stu-id="4eb96-118">**Cluster admin domain user**: This account is an active directory domain user designated as the Hadoop cluster admin including Ambari and Ranger.</span></span> <span data-ttu-id="4eb96-119">您必須在叢集建立期間提供此使用者的認證。</span><span class="sxs-lookup"><span data-stu-id="4eb96-119">You must provide this user’s credentials during cluster creation.</span></span> <span data-ttu-id="4eb96-120">此使用者有下列權限：</span><span class="sxs-lookup"><span data-stu-id="4eb96-120">This user has the following privileges:</span></span>

  * <span data-ttu-id="4eb96-121">在叢集建立期間，將機器加入網域，並將它們放入您指定的 OU 中。</span><span class="sxs-lookup"><span data-stu-id="4eb96-121">Join machines to the domain and place them within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="4eb96-122">在叢集建立期間，於您指定的 OU 中建立服務主體。</span><span class="sxs-lookup"><span data-stu-id="4eb96-122">Create service principals within the OU that you specify during cluster creation.</span></span>
  * <span data-ttu-id="4eb96-123">建立反向 DNS 項目。</span><span class="sxs-lookup"><span data-stu-id="4eb96-123">Create reverse DNS entries.</span></span>

    <span data-ttu-id="4eb96-124">請注意，其他的 AD 使用者也有這些權限。</span><span class="sxs-lookup"><span data-stu-id="4eb96-124">Note the other AD users also have these privileges.</span></span>

    <span data-ttu-id="4eb96-125">叢集內有些端點 (例如，Templeton) 不受 Ranger 管理，因此不安全。</span><span class="sxs-lookup"><span data-stu-id="4eb96-125">There are some end points within the cluster (for example, Templeton) which are not managed by Ranger, and hence are not secure.</span></span> <span data-ttu-id="4eb96-126">這些端點會針對所有使用者鎖定，只有叢集系統管理員網域使用者除外。</span><span class="sxs-lookup"><span data-stu-id="4eb96-126">These end points are locked down for all users except the cluster admin domain user.</span></span>
* <span data-ttu-id="4eb96-127">**一般**︰在叢集建立期間，您可以提供多個 Active Directory 群組。</span><span class="sxs-lookup"><span data-stu-id="4eb96-127">**Regular**: During cluster creation, you can provide multiple active directory groups.</span></span> <span data-ttu-id="4eb96-128">這些群組中的使用者都將同步至 Ranger 和 Ambari。</span><span class="sxs-lookup"><span data-stu-id="4eb96-128">The users in these groups will be synced to Ranger and Ambari.</span></span> <span data-ttu-id="4eb96-129">這些使用者是網域使用者，只有存取 Ranger 管理之端點 (例如Hiveserver2) 的權限。</span><span class="sxs-lookup"><span data-stu-id="4eb96-129">These users are domain users and will have access to only Ranger-managed endpoints (for example, Hiveserver2).</span></span> <span data-ttu-id="4eb96-130">所有 RBAC 原則和稽核皆不適用於這些使用者。</span><span class="sxs-lookup"><span data-stu-id="4eb96-130">All the RBAC policies and auditing will be applicable to these users.</span></span>

## <a name="roles-of-domain-joined-hdinsight-clusters"></a><span data-ttu-id="4eb96-131">已加入網域的 HDInsight 叢集的角色</span><span class="sxs-lookup"><span data-stu-id="4eb96-131">Roles of Domain-joined HDInsight clusters</span></span>
<span data-ttu-id="4eb96-132">已加入網域的 HDInsight 有下列角色︰</span><span class="sxs-lookup"><span data-stu-id="4eb96-132">Domain-joined HDInsight have the following roles:</span></span>

* <span data-ttu-id="4eb96-133">叢集系統管理員</span><span class="sxs-lookup"><span data-stu-id="4eb96-133">Cluster Administrator</span></span>
* <span data-ttu-id="4eb96-134">叢集操作員</span><span class="sxs-lookup"><span data-stu-id="4eb96-134">Cluster Operator</span></span>
* <span data-ttu-id="4eb96-135">服務管理員</span><span class="sxs-lookup"><span data-stu-id="4eb96-135">Service Administrator</span></span>
* <span data-ttu-id="4eb96-136">服務操作員</span><span class="sxs-lookup"><span data-stu-id="4eb96-136">Service Operator</span></span>
* <span data-ttu-id="4eb96-137">叢集使用者</span><span class="sxs-lookup"><span data-stu-id="4eb96-137">Cluster User</span></span>

<span data-ttu-id="4eb96-138">**若要查看這些角色的權限**</span><span class="sxs-lookup"><span data-stu-id="4eb96-138">**To see the permissions of these roles**</span></span>

1. <span data-ttu-id="4eb96-139">開啟 Ambari 管理 UI。</span><span class="sxs-lookup"><span data-stu-id="4eb96-139">Open the Ambari Management UI.</span></span>  <span data-ttu-id="4eb96-140">請參閱[開啟 Ambari 管理 UI](#open-the-ambari-management-ui)。</span><span class="sxs-lookup"><span data-stu-id="4eb96-140">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="4eb96-141">按一下左側功能表中的 [角色]。</span><span class="sxs-lookup"><span data-stu-id="4eb96-141">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="4eb96-142">按一下藍色問號可查看權限︰</span><span class="sxs-lookup"><span data-stu-id="4eb96-142">Click the blue question mark to see the permissions:</span></span>

    ![已加入網域的 HDInsight 角色權限](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-roles-permissions.png)

## <a name="open-the-ambari-management-ui"></a><span data-ttu-id="4eb96-144">開啟 Ambari 管理 UI</span><span class="sxs-lookup"><span data-stu-id="4eb96-144">Open the Ambari Management UI</span></span>
1. <span data-ttu-id="4eb96-145">登入 [Azure 入口網站](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="4eb96-145">Sign on to the [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="4eb96-146">在刀鋒視窗中開啟您的 HDInsight 叢集。</span><span class="sxs-lookup"><span data-stu-id="4eb96-146">Open your HDInsight cluster in a blade.</span></span> <span data-ttu-id="4eb96-147">請參閱[列出和顯示叢集](hdinsight-administer-use-management-portal.md#list-and-show-clusters)。</span><span class="sxs-lookup"><span data-stu-id="4eb96-147">See [List and show clusters](hdinsight-administer-use-management-portal.md#list-and-show-clusters).</span></span>
3. <span data-ttu-id="4eb96-148">按一下頂端功能表中的 [儀表板]  開啟 Ambari。</span><span class="sxs-lookup"><span data-stu-id="4eb96-148">Click **Dashboard** from the top menu to open Ambari.</span></span>
4. <span data-ttu-id="4eb96-149">使用叢集系統管理員網域使用者的名稱和密碼登入 Ambari：</span><span class="sxs-lookup"><span data-stu-id="4eb96-149">Log on to Ambari using the cluster administrator domain user name and password.</span></span>
5. <span data-ttu-id="4eb96-150">按一下右上角的 [管理] 下拉式功能表，然後按一下 [管理 Ambari]。</span><span class="sxs-lookup"><span data-stu-id="4eb96-150">Click the **Admin** dropdown menu from the upper right corner, and then click **Manage Ambari**.</span></span>

    ![已加入網域的 HDInsight 管理 Ambari](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-manage-ambari.png)

    <span data-ttu-id="4eb96-152">UI 看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="4eb96-152">The UI looks like:</span></span>

    ![已加入網域的 HDInsight 的 Ambari 管理 UI](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui.png)

## <a name="list-the-domain-users-synchronized-from-your-active-directory"></a><span data-ttu-id="4eb96-154">列出從您的 Active Directory 同步處理的網域使用者</span><span class="sxs-lookup"><span data-stu-id="4eb96-154">List the domain users synchronized from your Active Directory</span></span>
1. <span data-ttu-id="4eb96-155">開啟 Ambari 管理 UI。</span><span class="sxs-lookup"><span data-stu-id="4eb96-155">Open the Ambari Management UI.</span></span>  <span data-ttu-id="4eb96-156">請參閱[開啟 Ambari 管理 UI](#open-the-ambari-management-ui)。</span><span class="sxs-lookup"><span data-stu-id="4eb96-156">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="4eb96-157">按一下左側功能表中的 [使用者] 。</span><span class="sxs-lookup"><span data-stu-id="4eb96-157">From the left menu, click **Users**.</span></span> <span data-ttu-id="4eb96-158">您應該會看到從您的 Active Directory 同步至 HDInsight 叢集的所有使用者。</span><span class="sxs-lookup"><span data-stu-id="4eb96-158">You shall see all the users synced from your Active Directory to the HDInsight cluster.</span></span>

    ![已加入網域的 HDInsight 的 Ambari 管理 UI 列出使用者](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-users.png)

## <a name="list-the-domain-groups-synchronized-from-your-active-directory"></a><span data-ttu-id="4eb96-160">列出從您的 Active Directory 同步處理的網域群組</span><span class="sxs-lookup"><span data-stu-id="4eb96-160">List the domain groups synchronized from your Active Directory</span></span>
1. <span data-ttu-id="4eb96-161">開啟 Ambari 管理 UI。</span><span class="sxs-lookup"><span data-stu-id="4eb96-161">Open the Ambari Management UI.</span></span>  <span data-ttu-id="4eb96-162">請參閱[開啟 Ambari 管理 UI](#open-the-ambari-management-ui)。</span><span class="sxs-lookup"><span data-stu-id="4eb96-162">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="4eb96-163">按一下左側功能表中的 [群組]。</span><span class="sxs-lookup"><span data-stu-id="4eb96-163">From the left menu, click **Groups**.</span></span> <span data-ttu-id="4eb96-164">您應該會看到從您的 Active Directory 同步至 HDInsight 叢集的所有群組。</span><span class="sxs-lookup"><span data-stu-id="4eb96-164">You shall see all the groups synced from your Active Directory to the HDInsight cluster.</span></span>

    ![已加入網域的 HDInsight 的 Ambari 管理 UI 列出群組](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-groups.png)

## <a name="configure-hive-views-permissions"></a><span data-ttu-id="4eb96-166">設定 Hive 檢視權限</span><span class="sxs-lookup"><span data-stu-id="4eb96-166">Configure Hive Views permissions</span></span>
1. <span data-ttu-id="4eb96-167">開啟 Ambari 管理 UI。</span><span class="sxs-lookup"><span data-stu-id="4eb96-167">Open the Ambari Management UI.</span></span>  <span data-ttu-id="4eb96-168">請參閱[開啟 Ambari 管理 UI](#open-the-ambari-management-ui)。</span><span class="sxs-lookup"><span data-stu-id="4eb96-168">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="4eb96-169">按一下左側功能表中的 [檢視]。</span><span class="sxs-lookup"><span data-stu-id="4eb96-169">From the left menu, click **Views**.</span></span>
3. <span data-ttu-id="4eb96-170">按一下 [HIVE] 以顯示詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4eb96-170">Click **HIVE** to show the details.</span></span>

    ![已加入網域的 HDInsight 的 Ambari 管理 UI Hive 檢視](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views.png)
4. <span data-ttu-id="4eb96-172">按一下 [Hive 檢視] 連結以設定 Hive 檢視。</span><span class="sxs-lookup"><span data-stu-id="4eb96-172">Click the **Hive View** link to configure Hive Views.</span></span>
5. <span data-ttu-id="4eb96-173">向下捲動至 [權限]。</span><span class="sxs-lookup"><span data-stu-id="4eb96-173">Scroll down to the **Permissions** section.</span></span>

    ![已加入網域的 HDInsight 的 Ambari 管理 UI Hive 檢視設定權限](./media/hdinsight-domain-joined-manage/hdinsight-domain-joined-ambari-management-ui-hive-views-permissions.png)
6. <span data-ttu-id="4eb96-175">按一下 [新增使用者] 或 [新增群組]，然後指定可以使用 Hive 檢視的使用者或群組。</span><span class="sxs-lookup"><span data-stu-id="4eb96-175">Click **Add User** or **Add Group**, and then specify the users or groups that can use Hive Views.</span></span>

## <a name="configure-users-for-the-roles"></a><span data-ttu-id="4eb96-176">設定角色的使用者</span><span class="sxs-lookup"><span data-stu-id="4eb96-176">Configure users for the roles</span></span>
 <span data-ttu-id="4eb96-177">若要查看角色及其權限的清單，請參閱[已加入網域的 HDInsight 叢集的角色](#roles-of-domain---joined-hdinsight-clusters)。</span><span class="sxs-lookup"><span data-stu-id="4eb96-177">To see a list of roles and their permissions, see [Roles of Domain-joined HDInsight clusters](#roles-of-domain---joined-hdinsight-clusters).</span></span>

1. <span data-ttu-id="4eb96-178">開啟 Ambari 管理 UI。</span><span class="sxs-lookup"><span data-stu-id="4eb96-178">Open the Ambari Management UI.</span></span>  <span data-ttu-id="4eb96-179">請參閱[開啟 Ambari 管理 UI](#open-the-ambari-management-ui)。</span><span class="sxs-lookup"><span data-stu-id="4eb96-179">See [Open the Ambari Management UI](#open-the-ambari-management-ui).</span></span>
2. <span data-ttu-id="4eb96-180">按一下左側功能表中的 [角色]。</span><span class="sxs-lookup"><span data-stu-id="4eb96-180">From the left menu, click **Roles**.</span></span>
3. <span data-ttu-id="4eb96-181">按一下 [新增使用者] 或 [新增群組] 以將使用者或群組指定至不同角色。</span><span class="sxs-lookup"><span data-stu-id="4eb96-181">Click **Add User** or **Add Group** to assign users and groups to different roles.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4eb96-182">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4eb96-182">Next steps</span></span>
* <span data-ttu-id="4eb96-183">如需設定已加入網域的 HDInsight 叢集，請參閱[設定已加入網域的 HDInsight 叢集](hdinsight-domain-joined-configure.md)。</span><span class="sxs-lookup"><span data-stu-id="4eb96-183">For configuring a Domain-joined HDInsight cluster, see [Configure Domain-joined HDInsight clusters](hdinsight-domain-joined-configure.md).</span></span>
* <span data-ttu-id="4eb96-184">如需設定 Hive 原則和執行 Hive 查詢，請參閱[針對已加入網域的 HDInisight 叢集設定 Hive 原則](hdinsight-domain-joined-run-hive.md)。</span><span class="sxs-lookup"><span data-stu-id="4eb96-184">For configuring Hive policies and run Hive queries, see [Configure Hive policies for Domain-joined HDInsight clusters](hdinsight-domain-joined-run-hive.md).</span></span>
* <span data-ttu-id="4eb96-185">若要在已加入網域的 HDInsight 叢集上使用 SSH 執行 Hive 查詢，請參閱[搭配 HDInsight 使用 SSH](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined)。</span><span class="sxs-lookup"><span data-stu-id="4eb96-185">For running Hive queries using SSH on Domain-joined HDInsight clusters, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md#domainjoined).</span></span>
