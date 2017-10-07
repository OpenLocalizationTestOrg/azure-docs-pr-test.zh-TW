---
title: "在 VM 上的大量 aaaCompute 的 Java 應用程式 |Microsoft 文件"
description: "了解如何 toocreate 執行需要大量計算的 Java 應用程式的 Azure 虛擬機器可以受到其他 Java 應用程式。"
services: virtual-machines-windows
documentationcenter: java
author: rmcmurray
manager: erikre
editor: 
tags: azure-service-management,azure-resource-manager
ms.assetid: ae6f2737-94c7-4569-9913-d871450c2827
ms.service: virtual-machines-windows
ms.workload: infrastructure-services
ms.tgt_pltfrm: vm-windows
ms.devlang: Java
ms.topic: article
ms.date: 04/25/2017
ms.author: robmcm
ms.openlocfilehash: 02a198802a8d78bd444cd5a9197a78cb94f48e3b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-compute-intensive-task-in-java-on-a-virtual-machine"></a>在 Java 中 toorun 大量計算工作虛擬機器上如何
> [!IMPORTANT] 
> Azure 建立和處理資源的部署模型有二種： [資源管理員和傳統](../../../resource-manager-deployment-model.md)。 本文件涵蓋使用 hello 傳統部署模型。 Microsoft 建議最新的部署使用 hello 資源管理員的模型。

有了 Azure，您可以使用虛擬機器 toohandle 需要大量計算的工作。 例如，虛擬機器可以處理工作，並傳遞結果 tooclient 電腦或行動應用程式。 請閱讀這篇文章之後，您必須了解如何 toocreate 執行需要大量計算的 Java 應用程式的虛擬機器可以受到其他 Java 應用程式。

本教學課程假設您知道如何 toocreate Java 主控台應用程式，可以匯入程式庫 tooyour Java 應用程式，而且可以產生 Java 封存檔 (JAR)。 並假設您對 Microsoft Azure 一無所知。

您將了解：

* 如何 toocreate 虛擬機器與 Java Development Kit (JDK) 已安裝。
* 如何 tooremotely 登 tooyour 虛擬機器中。
* 如何 toocreate 服務匯流排命名空間。
* 如何 toocreate Java 應用程式執行需要大量計算的工作。
* 如何監視 Java 應用程式 toocreate hello hello 需要大量計算工作的進度。
* 如何 toorun hello Java 應用程式。
* 如何 toostop hello Java 應用程式。

本教學課程會使用 hello 業務員拜訪客戶順序問題的 hello 需要大量計算的工作。 hello 的範例如下的 hello Java 應用程式正在執行 hello 運算密集的工作。

![Traveling Salesman Problem solver][solver_output]

hello 的範例如下的 Java 應用程式監視 hello 需要大量計算工作 hello。

![Traveling Salesman Problem client][client_output]

[!INCLUDE [create-account-and-vms-note](../../../../includes/create-account-and-vms-note.md)]

## <a name="toocreate-a-virtual-machine"></a>toocreate 虛擬機器
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 依序按一下 [新增]、[計算]、[虛擬機器] 及 [從組件庫]。
3. 在 hello**虛擬機器映像選取**對話方塊中，選取**JDK 7 的 Windows Server 2012**。
   請注意， **JDK 6 Windows Server 2012**是可用的如果您有尚無法準備 toorun JDK 7 的舊版應用程式。
4. 按一下 [下一步] 。
5. 在 hello**虛擬機器組態**對話方塊：
   1. 指定 hello 虛擬機器的名稱。
   2. 指定 hello 大小 toouse hello 虛擬機器。
   3. 輸入 hello 系統管理員的名稱在 hello**使用者名**欄位。 請記住這個接下來，您將輸入的名稱和 hello 密碼，您會在您從遠端登入 toohello 虛擬機器時使用它們。
   4. 輸入密碼，hello**新密碼**欄位，並重新進入 hello**確認**欄位。 這是 hello 系統管理員帳戶密碼。
   5. 按一下 [下一步] 。
6. 在 hello 下一步**虛擬機器組態**對話方塊：
   1. 如**雲端服務**，使用預設的 hello**建立新的雲端服務**。
   2. hello 值**雲端服務 DNS 名稱**必須是唯一的.cloudapp.net。 必要時請修改此值，使 Azure 指出該值是唯一的。
   3. 指定區域、同質群組或虛擬網路。 為因應本教學課程的目的，請指定如 [美國西部] 的區域。
   4. 針對 [儲存體帳戶]，選取 [使用自動產生的儲存體帳戶]。
   5. 針對 [可用性設定組]，選取 [(無)]。
   6. 按一下 [下一步] 。
7. 在最終的 hello**虛擬機器組態**對話方塊：
   1. 接受 hello 預設端點項目。
   2. 按一下頁面底部的 [新增] 。

## <a name="tooremotely-log-in-tooyour-virtual-machine"></a>tooremotely tooyour 虛擬機器中的記錄檔
1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 按一下 [虛擬機器] 。
3. 按一下您要 toolog 中的 hello 虛擬機器的 hello 名稱。
4. 按一下 [ **連接**]。
5. 回應 toohello 提示做為所需的 tooconnect toohello 虛擬機器。 當提示 hello 管理員名稱和密碼，請使用 hello 值建立 hello 虛擬機器時提供。

請注意該 hello Azure 服務匯流排功能需要隨您 JRE hello Baltimore CyberTrust 根憑證 toobe **cacerts**儲存。 此憑證會自動包含在 hello Java Runtime Environment (JRE) 本教學課程所使用。 如果您沒有此憑證中您 JRE **cacerts**存放區，請參閱[加入 Java CA 憑證存放區的憑證 toohello] [ add_ca_cert]上將它加入資訊 （如檢視資訊 hello 憑證 cacerts 存放區中）。

## <a name="how-toocreate-a-service-bus-namespace"></a>如何 toocreate 服務匯流排命名空間
使用服務匯流排 toobegin 排入佇列，在 Azure 中，您必須先建立服務命名空間。 服務命名空間提供範圍容器，可在應用程式內定址服務匯流排資源。

toocreate 服務命名空間：

1. 登入 toohello [Azure 傳統入口網站](https://manage.windowsazure.com)。
2. 在 hello 左下方的巡覽窗格中的 hello Azure 傳統入口網站，按一下 **服務匯流排、 存取控制和 Caching**。
3. Hello 左上方窗格中的 hello Azure 傳統入口網站，按一下 hello **Service Bus**  節點，然後按一下hello**新增** 按鈕。  
   ![Service Bus Node screenshot][svc_bus_node]
4. 在 [hello**建立新的服務命名空間**對話方塊方塊中，輸入**命名空間**，toomake 確定是唯一的然後按一下**檢查可用性**] 按鈕。  
   ![Create a New Namespace screenshot][create_namespace]
5. 請先確定 hello 命名空間名稱使用，選擇的國家或地區，您的命名空間應該裝載，然後按一下hello**建立命名空間** 按鈕。  
   
   您所建立的 hello 命名空間即會出現在 hello Azure 傳統入口網站，並會採用目前 tooactivate。 等候 hello 狀態**Active**再繼續進行 hello 下一個步驟。

## <a name="obtain-hello-default-management-credentials-for-hello-namespace"></a>取得 hello hello 命名空間的預設管理認證
在順序 tooperform 管理作業，例如 hello 新命名空間上建立佇列，您需要命名空間 tooobtain hello 管理認證。

1. Hello 左側瀏覽窗格中，按一下 hello **Service Bus**節點以顯示 hello 清單可用的命名空間。
   ![Available Namespaces screenshot][avail_namespaces]
2. 選取您剛才建立的 hello 清單中所示的 hello 命名空間。
   ![命名空間清單螢幕擷取畫面][namespace_list]
3. hello 右**屬性**窗格會列出新的命名空間的 hello 屬性。
   ![Properties Pane screenshot][properties_pane]
4. hello**預設金鑰**隱藏的。 按一下 hello**檢視**按鈕 toodisplay hello 安全性認證。
   ![Default Key screenshot][default_key]
5. 請記下 hello**預設簽發者**和 hello**預設金鑰**當您將使用這項資訊下方 tooperform 作業與命名空間。

## <a name="how-toocreate-a-java-application-that-performs-a-compute-intensive-task"></a>如何 toocreate Java 應用程式執行需要大量計算的工作
1. 在開發電腦上 （但不需要您建立的 toobe hello 虛擬機器），下載 hello [Azure SDK for Java](https://azure.microsoft.com/develop/java/)。
2. 建立在 hello 本節結尾使用 hello 範例程式碼的 Java 主控台應用程式。 在此教學課程中，我們將使用**TSPSolver.java** hello Java 的檔案名稱。 修改 hello**您\_服務\_匯流排\_命名空間**，**您\_服務\_匯流排\_擁有者**，和**您\_服務\_匯流排\_金鑰**預留位置 toouse 服務匯流排**命名空間**，**預設簽發者**和**預設金鑰**分別值。
3. 撰寫程式碼之後, 匯出 hello 應用程式 tooa 可執行 Java 封存檔 (JAR)，封裝 hello 需要和 hello 到程式庫產生 JAR。 在此教學課程中，我們將使用**TSPSolver.jar**做為產生的 hello JAR 名稱。

<p/>

    // TSPSolver.java

    import com.microsoft.windowsazure.services.core.Configuration;
    import com.microsoft.windowsazure.services.core.ServiceException;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import java.io.*;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import java.util.ArrayList;
    import java.util.Date;
    import java.util.List;

    public class TSPSolver {

        //  Value specifying how often tooprovide an update toohello console.
        private static long loopCheck = 100000000;  

        private static long nTimes = 0, nLoops=0;

        private static double[][] distances;
        private static String[] cityNames;
        private static int[] bestOrder;
        private static double minDistance;
        private static ServiceBusContract service;

        private static void buildDistances(String fileLocation, int numCities) throws Exception{
            try{
                BufferedReader file = new BufferedReader(new InputStreamReader(new DataInputStream(new FileInputStream(new File(fileLocation)))));
                double[][] cityLocs = new double[numCities][2];
                for (int i = 0; i<numCities; i++){
                    String[] line = file.readLine().split(", ");
                    cityNames[i] = line[0];
                    cityLocs[i][0] = Double.parseDouble(line[1]);
                    cityLocs[i][1] = Double.parseDouble(line[2]);
                }
                for (int i = 0; i<numCities; i++){
                    for (int j = i; j<numCities; j++){
                        distances[i][j] = Math.hypot(Math.abs(cityLocs[i][0] - cityLocs[j][0]), Math.abs(cityLocs[i][1] - cityLocs[j][1]));
                        distances[j][i] = distances[i][j];
                    }
                }
            } catch (Exception e){
                throw e;
            }
        }

        private static void permutation(List<Integer> startCities, double distSoFar, List<Integer> restCities) throws Exception {

            try
            {
                nTimes++;
                if (nTimes == loopCheck)
                {
                    nLoops++;
                    nTimes = 0;
                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.print("Current time is " + dateFormat.format(date) + ". ");
                    System.out.println(  "Completed " + nLoops + " iterations of size of " + loopCheck + ".");
                }

                if ((restCities.size() == 1) && ((minDistance == -1) || (distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-1)] < minDistance))){
                    startCities.add(restCities.get(0));
                    newBestDistance(startCities, distSoFar + distances[restCities.get(0)][startCities.get(0)] + distances[restCities.get(0)][startCities.get(startCities.size()-2)]);
                    startCities.remove(startCities.size()-1);
                }
                else{
                    for (int i=0; i<restCities.size(); i++){
                        startCities.add(restCities.get(0));
                        restCities.remove(0);
                        permutation(startCities, distSoFar + distances[startCities.get(startCities.size()-1)][startCities.get(startCities.size()-2)],restCities);
                        restCities.add(startCities.get(startCities.size()-1));
                        startCities.remove(startCities.size()-1);
                    }
                }
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        private static void newBestDistance(List<Integer> cities, double distance) throws ServiceException, Exception {
            try
            {
                minDistance = distance;
                String cityList = "Shortest distance is "+minDistance+", with route: ";
                for (int i = 0; i<bestOrder.length; i++){
                    bestOrder[i] = cities.get(i);
                    cityList += cityNames[bestOrder[i]];
                    if (i != bestOrder.length -1)
                        cityList += ", ";
                }
                System.out.println(cityList);
                service.sendQueueMessage("TSPQueue", new BrokeredMessage(cityList));
            }
            catch (ServiceException se)
            {
                throw se;
            }
            catch (Exception e)
            {
                throw e;
            }
        }

        public static void main(String args[]){

            try {

                Configuration config = ServiceBusConfiguration.configureWithWrapAuthentication(
                        "your_service_bus_namespace", "your_service_bus_owner",
                        "your_service_bus_key",
                        ".servicebus.windows.net",
                        "-sb.accesscontrol.windows.net/WRAPv0.9");

                service = ServiceBusService.create(config);

                int numCities = 10;  // Use as hello default, if no value is specified at command line.
                if (args.length != 0)
                {
                    if (args[0].toLowerCase().compareTo("createqueue")==0)
                    {
                        // No processing toooccur other than creating hello queue.
                        QueueInfo queueInfo = new QueueInfo("TSPQueue");

                        service.createQueue(queueInfo);

                        System.out.println("Queue named TSPQueue was created.");

                        System.exit(0);
                    }

                    if (args[0].toLowerCase().compareTo("deletequeue")==0)
                    {
                        // No processing toooccur other than deleting hello queue.
                        service.deleteQueue("TSPQueue");

                        System.out.println("Queue named TSPQueue was deleted.");

                        System.exit(0);
                    }

                    // Neither creating or deleting a queue.
                    // Assume hello value passed in is hello number of cities toosolve.
                    numCities = Integer.valueOf(args[0]);  
                }

                System.out.println("Running for " + numCities + " cities.");

                List<Integer> startCities = new ArrayList<Integer>();
                List<Integer> restCities = new ArrayList<Integer>();
                startCities.add(0);
                for(int i = 1; i<numCities; i++)
                    restCities.add(i);
                distances = new double[numCities][numCities];
                cityNames = new String[numCities];
                buildDistances("c:\\TSP\\cities.txt", numCities);
                minDistance = -1;
                bestOrder = new int[numCities];
                permutation(startCities, 0, restCities);
                System.out.println("Final solution found!");
                service.sendQueueMessage("TSPQueue", new BrokeredMessage("Complete"));
            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }
        }

    }



## <a name="how-toocreate-a-java-application-that-monitors-hello-progress-of-hello-compute-intensive-task"></a>Toocreate 監視 Java 應用程式如何 hello hello 需要大量計算工作的進度
1. 在您的開發電腦上建立 Java 主控台應用程式在 hello 本節結尾使用 hello 範例程式碼。 在此教學課程中，我們將使用**TSPClient.java** hello Java 的檔案名稱。 如先前所示，修改 hello**您\_服務\_匯流排\_命名空間**，**您\_服務\_匯流排\_擁有者**，和**您\_服務\_匯流排\_金鑰**預留位置 toouse 服務匯流排**命名空間**，**預設簽發者**和**預設金鑰**分別值。
2. 匯出 hello 應用程式 tooa 可執行的 JAR 和套件 hello 需要 hello 到程式庫產生的 JAR。 在此教學課程中，我們將使用**TSPClient.jar**做為產生的 hello JAR 名稱。

<p/>

    // TSPClient.java

    import java.util.Date;
    import java.text.DateFormat;
    import java.text.SimpleDateFormat;
    import com.microsoft.windowsazure.services.serviceBus.*;
    import com.microsoft.windowsazure.services.serviceBus.models.*;
    import com.microsoft.windowsazure.services.core.*;

    public class TSPClient
    {

        public static void main(String[] args)
        {
                try
                {

                    DateFormat dateFormat = new SimpleDateFormat("MM/dd/yyyy HH:mm:ss");
                    Date date = new Date();
                    System.out.println("Starting at " + dateFormat.format(date) + ".");

                    String namespace = "your_service_bus_namespace";
                    String issuer = "your_service_bus_owner";
                    String key = "your_service_bus_key";

                    Configuration config;
                    config = ServiceBusConfiguration.configureWithWrapAuthentication(
                            namespace, issuer, key,
                            ".servicebus.windows.net",
                            "-sb.accesscontrol.windows.net/WRAPv0.9");

                    ServiceBusContract service = ServiceBusService.create(config);

                    BrokeredMessage message;

                    int waitMinutes = 3;  // Use as hello default, if no value is specified at command line.
                    if (args.length != 0)
                    {
                        waitMinutes = Integer.valueOf(args[0]);  
                    }

                    String waitString;

                    waitString = (waitMinutes == 1) ? "minute." : waitMinutes + " minutes.";

                    // This queue must have previously been created.
                    service.getQueue("TSPQueue");

                    int numRead;

                    String s = null;

                    while (true)
                    {

                        ReceiveQueueMessageResult resultQM = service.receiveQueueMessage("TSPQueue");
                        message = resultQM.getValue();

                        if (null != message && null != message.getMessageId())
                        {

                            // Display hello queue message.
                            byte[] b = new byte[200];

                            System.out.print("From queue: ");

                            s = null;
                            numRead = message.getBody().read(b);
                            while (-1 != numRead)
                            {
                                s = new String(b);
                                s = s.trim();
                                System.out.print(s);
                                numRead = message.getBody().read(b);
                            }
                            System.out.println();
                            if (s.compareTo("Complete") == 0)
                            {
                                // No more processing toooccur.
                                date = new Date();
                                System.out.println("Finished at " + dateFormat.format(date) + ".");
                                break;
                            }
                        }
                        else
                        {
                            // hello queue is empty.
                            System.out.println("Queue is empty. Sleeping for another " + waitString);
                            Thread.sleep(60000 * waitMinutes);
                        }
                    }

            }
            catch (ServiceException se)
            {
                System.out.println(se.getMessage());
                se.printStackTrace();
                System.exit(-1);
            }
            catch (Exception e)
            {
                System.out.println(e.getMessage());
                e.printStackTrace();
                System.exit(-1);
            }

        }

    }

## <a name="how-toorun-hello-java-applications"></a>如何 toorun hello Java 應用程式
執行 hello 需要大量計算的應用程式，第一個 toocreate hello 佇列，然後 toosolve hello 旅行 Saleseman 問題，即可將新增 hello 目前最佳路由 toohello 服務匯流排佇列。 Hello 時需要大量計算的應用程式會執行 （或之後），執行的 hello 用戶端 toodisplay 結果 hello 服務匯流排佇列。

### <a name="toorun-hello-compute-intensive-application"></a>toorun hello 需要大量計算的應用程式
1. 登入 tooyour 虛擬機器。
2. 建立將執行您應用程式的資料夾。 例如 **c:\TSP**。
3. 複製**TSPSolver.jar**太**c:\TSP**，
4. 建立名為**c:\TSP\cities.txt**以下列內容的 hello。
   
        City_1, 1002.81, -1841.35
        City_2, -953.55, -229.6
        City_3, -1363.11, -1027.72
        City_4, -1884.47, -1616.16
        City_5, 1603.08, -1030.03
        City_6, -1555.58, 218.58
        City_7, 578.8, -12.87
        City_8, 1350.76, 77.79
        City_9, 293.36, -1820.01
        City_10, 1883.14, 1637.28
        City_11, -1271.41, -1670.5
        City_12, 1475.99, 225.35
        City_13, 1250.78, 379.98
        City_14, 1305.77, 569.75
        City_15, 230.77, 231.58
        City_16, -822.63, -544.68
        City_17, -817.54, -81.92
        City_18, 303.99, -1823.43
        City_19, 239.95, 1007.91
        City_20, -1302.92, 150.39
        City_21, -116.11, 1933.01
        City_22, 382.64, 835.09
        City_23, -580.28, 1040.04
        City_24, 205.55, -264.23
        City_25, -238.81, -576.48
        City_26, -1722.9, -909.65
        City_27, 445.22, 1427.28
        City_28, 513.17, 1828.72
        City_29, 1750.68, -1668.1
        City_30, 1705.09, -309.35
        City_31, -167.34, 1003.76
        City_32, -1162.85, -1674.33
        City_33, 1490.32, 821.04
        City_34, 1208.32, 1523.3
        City_35, 18.04, 1857.11
        City_36, 1852.46, 1647.75
        City_37, -167.44, -336.39
        City_38, 115.4, 0.2
        City_39, -66.96, 917.73
        City_40, 915.96, 474.1
        City_41, 140.03, 725.22
        City_42, -1582.68, 1608.88
        City_43, -567.51, 1253.83
        City_44, 1956.36, 830.92
        City_45, -233.38, 909.93
        City_46, -1750.45, 1940.76
        City_47, 405.81, 421.84
        City_48, 363.68, 768.21
        City_49, -120.3, -463.13
        City_50, 588.51, 679.33
5. 在命令提示字元中，變更目錄 tooc:\TSP。
6. 確定 hello JRE bin 資料夾 hello PATH 環境變數中。
7. 執行 hello TSP 規劃求解排列之前，您將需要 toocreate hello 服務匯流排佇列。 執行下列命令 toocreate hello 服務匯流排佇列的 hello。
   
        java -jar TSPSolver.jar createqueue
8. Hello 建立佇列，您可以執行 hello TSP 規劃求解排列。 例如，執行下列命令 toorun hello 規劃求解 8 城市 hello。
   
        java -jar TSPSolver.jar 8
   
   如果您沒有指定數目，它將會針對 10 個城市執行。 Hello 規劃求解找出目前的最短路由，因為它會將其加入 toohello 佇列。

> [!NOTE]
> 較大的 hello hello 數字，您指定，hello 長 hello 規劃求解執行。 例如，針對 14 個城市執行可能需花數分鐘，而針對 15 個城市執行可能需花數小時。 增加 too16 或多個城市，可能會導致執行階段 （最終數週、 月數及年數） 的天數。 這是因為 toohello 快速增加 hello hello 數字的城市增加而增加 hello 規劃求解所評估的排列數目。
> 
> 

### <a name="how-toorun-hello-monitoring-client-application"></a>如何 toorun hello 監視用戶端應用程式
1. 登入 tooyour 機器您要執行 hello 用戶端應用程式。 這不需要 toobe hello 同一部電腦執行 hello **TSPSolver**應用程式中，雖然可能造成。
2. 建立將執行您應用程式的資料夾。 例如 **c:\TSP**。
3. 複製**TSPClient.jar**太**c:\TSP**，
4. 確定 hello JRE bin 資料夾 hello PATH 環境變數中。
5. 在命令提示字元中，變更目錄 tooc:\TSP。
6. 執行下列命令的 hello。
   
        java -jar TSPClient.jar
   
    （選擇性） 指定分鐘 toosleep 之間檢查 hello 佇列，透過命令列引數傳入的 hello 數目。 hello 預設睡眠期間檢查 hello 佇列是 3 分鐘，用如果任何命令列引數不傳遞太**TSPClient**。 如果您想要 hello 休眠間隔 toouse 不同的值，比方說，一分鐘，執行下列命令的 hello。
   
        java -jar TSPClient.jar 1
   
    hello 用戶端將會執行直到它看到 「 完成 」 的佇列訊息。 請注意，是否您未執行 hello 用戶端執行的 hello 規劃求解的多個項目，您可能需要 toorun hello 用戶端多次 toocompletely 空 hello 佇列。 或者，您可以刪除 hello 佇列，然後再重新建立。 toodelete hello 佇列中，執行下列 hello **TSPSolver** (不**TSPClient**) 命令。
   
        java -jar TSPSolver.jar deletequeue
   
    hello 規劃求解會執行直到它完成檢查所有路由。

## <a name="how-toostop-hello-java-applications"></a>如何 toostop hello Java 應用程式
Hello 規劃求解和用戶端應用程式中，您可以按**Ctrl + C** tooexit，如果您想 tooend 先前 toonormal 完成。

[solver_output]:media/java-run-compute-intensive-task/WA_JavaTSPSolver.png
[client_output]:media/java-run-compute-intensive-task/WA_JavaTSPClient.png
[svc_bus_node]:media/java-run-compute-intensive-task/SvcBusQueues_02_SvcBusNode.jpg
[create_namespace]:media/java-run-compute-intensive-task/SvcBusQueues_03_CreateNewSvcNamespace.jpg
[avail_namespaces]:media/java-run-compute-intensive-task/SvcBusQueues_04_SvcBusNode_AvailNamespaces.jpg
[namespace_list]:media/java-run-compute-intensive-task/SvcBusQueues_05_NamespaceList.jpg
[properties_pane]:media/java-run-compute-intensive-task/SvcBusQueues_06_PropertiesPane.jpg
[default_key]:media/java-run-compute-intensive-task/SvcBusQueues_07_DefaultKey.jpg
[add_ca_cert]: ../../../java-add-certificate-ca-store.md