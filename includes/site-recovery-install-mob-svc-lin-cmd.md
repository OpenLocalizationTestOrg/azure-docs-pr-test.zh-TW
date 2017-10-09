1. 將複製 hello installer tooa 本機資料夾 (例如，tec_rule 位於 /tmp) 您想 tooprotect hello 伺服器上。 在終端機中，執行下列命令的 hello:
  ```
  cd /tmp
  tar -xvzf Microsoft-ASR_UA*release.tar.gz
  ```
2. 執行下列命令的 hello tooinstall 行動服務：

  ```
  sudo ./install -d <Install Location> -r MS -v VmWare -q
  ```
3. 安裝完成之後，hello 行動服務需要 tooget toohello 註冊的組態伺服器。 執行下列命令 tooregister hello 行動服務使用組態伺服器 hello。

  ```
  /usr/local/ASR/Vx/bin/UnifiedAgentConfigurator.sh -i <CSIP> -P /var/passphrase.txt
  ```

#### <a name="mobility-service-installer-command-line"></a>行動服務安裝程式命令列

```
Usage:
./install -d <Install Location> -r <MS|MT> -v VmWare -q
```

|參數|類型|說明|可能的值|
|-|-|-|-|
|-r |強制|指定應該安裝行動服務 (MS) 或主要目標 (MT)|MS </br> MT|
|-d |選用|將要安裝行動服務的位置|/usr/local/ASR|
|-v|強制|指定取得哪些 hello 安裝行動服務的 hello 平台 </br> </br>- **VMware**︰如果您要在「VMware vSphere ESXi 主機」、「Hyper-V 主機」和「實體伺服器」上執行的 VM 上安裝行動服務，請使用此值 </br> - **Azure**︰如果您要在 Azure IaaS VM 上安裝代理程式，請使用此值| VMware </br> Azure|
|-q|選用|指定 toorun 安裝程式以無訊息模式| N/A|


#### <a name="mobility-service-configuration-command-line"></a>行動服務設定命令列

```
Usage:
cd /usr/local/ASR/Vx/bin
UnifiedAgentConfigurator.sh -i <CSIP> -P <PassphraseFilePath>
```

|參數|類型|說明|可能的值|
|-|-|-|-|
|-i |強制|Hello 組態伺服器的 IP|任何有效的 IP 位址|
|-P |強制|Hello 連接複雜密碼的儲存位置的完整檔案路徑 hello 檔案|任何有效的資料夾|
