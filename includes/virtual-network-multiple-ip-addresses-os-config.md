## <a name="os-config"></a>新增 IP 位址 tooa VM 作業系統

連線並建立具有多個私人 IP 位址的登入 tooa VM。 您必須手動加入所有 hello 私人 IP 位址 （包括 hello 主要複本），就像加入 toohello VM。 完成下列步驟適用於您的 VM 作業系統的 hello:

### <a name="windows"></a>Windows

1. 從命令提示字元輸入 *ipconfig /all*。  您只會看見 hello*主要*私人 IP 位址 （透過 DHCP)。
2. 型別*ncpa.cpl*在 hello 命令提示字元 tooopen hello**網路連線**視窗。
3. 開啟 hello hello 適當的配接器屬性：**區域連線**。
4. 按兩下 [網際網路通訊協定第 4 版 (IPv4)]。
5. 選取**下列的 IP 位址使用 hello**並輸入下列值的 hello:

    * **IP 位址**： 輸入 hello*主要*私人 IP 位址
    * **子網路遮罩**︰根據您的子網路設定。 例如，如果 hello 子網路是 / 24 子網路則 hello 子網路遮罩為 255.255.255.0。
    * **預設閘道**: hello hello 子網路中的第一個 IP 位址。 如果您的子網路是 10.0.0.0/24，hello 閘道 IP 位址為 10.0.0.1。
    * 按一下**下列的 DNS 伺服器位址使用 hello**並輸入下列值的 hello:
        * **慣用 DNS 伺服器**︰如果您不是使用自己的 DNS 伺服器，請輸入 168.63.129.16。  如果您使用您自己的 DNS 伺服器，輸入您的伺服器 hello IP 位址。
    * 按一下 hello**進階**按鈕，然後加入其他 IP 位址。 新增的每個 hello 次要私用 IP 位址列入的 hello hello 主要 IP 位址的指定相同的子網路的步驟 8 toohello NIC。
        >[!WARNING] 
        >如果未正確地依照 hello 上述步驟，您可能會失去連線 tooyour VM。 請確定輸入的步驟 5 的 hello 資訊正確無誤後再繼續。

    * 按一下**[確定]** tooclose 出 hello TCP/IP 設定，然後**確定**再次 tooclose hello 介面卡的設定。 您的 RDP 連接已重建。

6. 從命令提示字元輸入 *ipconfig /all*。 此時會顯示您加入的所有 IP 位址，而 DHCP 是關閉的。


### <a name="validation-windows"></a>驗證 (Windows)

tooensure 都能 tooconnect toohello 上面步驟從透過公用 IP 相關聯，一旦您加入它使用正確的 hello 次要 IP 設定的網際網路，請使用下列命令的 hello:

```bash
ping -S 10.0.0.5 hotmail.com
```
>[!NOTE]
>對於次要 IP 設定，您只可以 ping toohello 網際網路如果 hello 組態都有與其相關聯的公用 IP 位址。 主要的 IP 組態的公用 IP 位址不需要的 tooping toohello 網際網路。

### <a name="linux-ubuntu"></a>Linux (Ubuntu)

1. 開啟終端機視窗。
2. 請確定您是 hello 根使用者。 如果您不是，輸入下列命令的 hello:

    ```bash
    sudo -i
    ```

3. 更新 hello hello （假設 'eth0'） 的網路介面的組態檔。

    * 保留 hello 現有明細項目 dhcp。 在先前 hello 主要 IP 位址依然會設定。
    * 加入額外的靜態 IP 位址組態，以 hello 下列命令：

        ```bash
        cd /etc/network/interfaces.d/
        ls
        ```

    您應該會看到一個 .cfg 檔案。
4. 開啟 hello 檔案。 您應該會看到下列行 hello hello 檔結尾的 hello:

    ```bash
    auto eth0
    iface eth0 inet dhcp
    ```

5. 加入下列行之後存在此檔案中的 hello 行 hello:

    ```bash
    iface eth0 inet static
    address <your private IP address here>
    netmask <your subnet mask>
    ```

6. 使用下列命令的 hello 儲存 hello 檔案：

    ```bash
    :wq
    ```

7. 重設 hello 網路介面，以 hello 下列命令：

    ```bash
    sudo ifdown eth0 && sudo ifup eth0
    ```

    > [!IMPORTANT]
    > 請執行 ifdown 和 ifup 中相同列如果使用遠端連線的 hello。
    >

8. 請確認 hello IP 位址加入 toohello 網路介面以 hello 下列命令：

    ```bash
    ip addr list eth0
    ```

    您應該會看到 hello IP 位址您加入 hello 清單的一部分。

### <a name="linux-redhat-centos-and-others"></a>Linux (Redhat、CentOS 以及其他)

1. 開啟終端機視窗。
2. 請確定您是 hello 根使用者。 如果您不是，輸入下列命令的 hello:

    ```bash
    sudo -i
    ```

3. 輸入您的密碼，並且依照提示的指示。 一旦 hello 根使用者，請瀏覽 toohello 網路指令碼 資料夾，以 hello 下列命令：

    ```bash
    cd /etc/sysconfig/network-scripts
    ```

4. 清單 hello 相關 ifcfg 檔案使用下列命令的 hello:

    ```bash
    ls ifcfg-*
    ```

    您應該會看到*ifcfg eth0*做為其中一個 hello 檔案。

5. tooadd IP 位址，為其建立組態檔，如下所示。 請注意，必須針對每個 IP 組態建立一個檔案。

    ```bash
    touch ifcfg-eth0:0
    ```

6. 開啟 hello *ifcfg-eth0:0*檔案以 hello 下列命令：

    ```bash
    vi ifcfg-eth0:0
    ```

7. 加入內容 toohello 檔案*eth0:0*在此情況下，使用下列命令的 hello。 確定 tooupdate 資訊可根據您的 IP 位址。

    ```bash
    DEVICE=eth0:0
    BOOTPROTO=static
    ONBOOT=yes
    IPADDR=192.168.101.101
    NETMASK=255.255.255.0
    ```

8. 儲存 hello 檔案以 hello 下列命令：

    ```bash
    :wq
    ```

9. 重新啟動 hello 網路服務，並確定 hello 變更都能藉由執行下列命令的 hello 成功：

    ```bash
    /etc/init.d/network restart
    ifconfig
    ```

    您應該會看見 hello IP 位址加入，您*eth0:0*，傳回的 hello 清單中。

### <a name="validation-linux"></a>驗證 (Linux)

從次要 IP 設定 hello 公用 IP 透過網際網路相關它都能夠 tooconnect toohello tooensure，請使用下列命令的 hello:

```bash
ping -I 10.0.0.5 hotmail.com
```
>[!NOTE]
>對於次要 IP 設定，您只可以 ping toohello 網際網路如果 hello 組態都有與其相關聯的公用 IP 位址。 主要的 IP 組態的公用 IP 位址不需要的 tooping toohello 網際網路。

適用於 Linux Vm，嘗試從次要 NIC toovalidate 輸出連線時，您可能需要 tooadd 適當的路由。 有許多方式 toodo 這。 請參閱您的 Linux 散發套件相關文件。 hello 下列這是一個方法 tooaccomplish:

```bash
echo 150 custom >> /etc/iproute2/rt_tables 

ip rule add from 10.0.0.5 lookup custom
ip route add default via 10.0.0.1 dev eth2 table custom

```
- 為確定 tooreplace:
    - **10.0.0.5**具有 hello 私人 IP 位址具有公用 IP 位址相關聯的 tooit
    - **10.0.0.1** tooyour 預設閘道
    - **eth2**您次要 NIC toohello 名稱
