---
title: Erstellen eines Windows PowerShell-Laufwerk Anbieters | Microsoft-Dokumentation
ms.date: 09/13/2016
helpviewer_keywords:
- drive providers [PowerShell Programmer's Guide]
- providers [PowerShell Programmer's Guide], drive provider
- drives [PowerShell Programmer's Guide]
ms.openlocfilehash: 2a2178714ed548986fe1a1a4de8828e8e0a938cb
ms.sourcegitcommit: 0907b8c6322d2c7c61b17f8168d53452c8964b41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87787188"
---
# <a name="creating-a-windows-powershell-drive-provider"></a>Erstellen eines Windows PowerShell-Laufwerkanbieters

In diesem Thema wird beschrieben, wie Sie einen Windows PowerShell-Laufwerks Anbieter erstellen, der die Möglichkeit bietet, über ein Windows PowerShell-Laufwerk auf einen Datenspeicher zuzugreifen. Diese Art von Anbieter wird auch als Windows PowerShell-Laufwerks Anbieter bezeichnet. Die vom Anbieter verwendeten Windows PowerShell-Laufwerke bieten die Möglichkeit, eine Verbindung mit dem Datenspeicher herzustellen.

Der hier beschriebene Windows PowerShell-Laufwerks Anbieter ermöglicht den Zugriff auf eine Microsoft Access-Datenbank.
Für diesen Anbieter stellt das Windows PowerShell-Laufwerk die Datenbank dar (es ist möglich, einem Laufwerks Anbieter eine beliebige Anzahl von Laufwerken hinzuzufügen), die Container der obersten Ebene des Laufwerks repräsentieren die Tabellen in der Datenbank, und die Elemente der Container repräsentieren die Zeilen in den Tabellen.

## <a name="defining-the-windows-powershell-provider-class"></a>Definieren der Windows PowerShell-Anbieter Klasse

Der Laufwerk Anbieter muss eine .NET-Klasse definieren, die von der [System. Management. Automation. Provider. drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) -Basisklasse abgeleitet wird. Hier ist die Klassendefinition für diesen Laufwerks Anbieter:

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs" range="29-30":::

Beachten Sie, dass das [System. Management. Automation. Provider. cmdletproviderattribute](/dotnet/api/System.Management.Automation.Provider.CmdletProviderAttribute) -Attribut in diesem Beispiel einen benutzerfreundlichen Namen für den Anbieter und die Windows PowerShell-spezifischen Funktionen angibt, die der Anbieter während der Befehls Verarbeitung für die Windows PowerShell-Laufzeit verfügbar macht.
Die möglichen Werte für die Anbieter Funktionen werden von der [System. Management. Automation. Provider. providerfunktionalitäten](/dotnet/api/System.Management.Automation.Provider.ProviderCapabilities) -Enumeration definiert. Dieser Laufwerk Anbieter unterstützt diese Funktionen nicht.

## <a name="defining-base-functionality"></a>Definieren der Basisfunktionalität

Wie in [Entwerfen des Windows PowerShell-Anbieters](./designing-your-windows-powershell-provider.md)beschrieben, wird die [System. Management. Automation. Provider. drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) -Klasse von der [System. Management. Automation. Provider. cmdletprovider](/dotnet/api/System.Management.Automation.Provider.CmdletProvider) -Basisklasse abgeleitet, die die zum Initialisieren und Aufheben der Initialisierung des Anbieters erforderlichen Methoden definiert. Informationen zum Implementieren von Funktionen zum Hinzufügen von Sitzungs spezifischen Initialisierungs Informationen und zum Freigeben von Ressourcen, die vom Anbieter verwendet werden, finden Sie unter [Erstellen eines einfachen Windows PowerShell-Anbieters](./creating-a-basic-windows-powershell-provider.md).
Die meisten Anbieter (einschließlich des hier beschriebenen Anbieters) können jedoch die Standard Implementierung dieser Funktionalität verwenden, die von Windows PowerShell bereitgestellt wird.

## <a name="creating-drive-state-information"></a>Erstellen von Laufwerks Zustandsinformationen

Alle Windows PowerShell-Anbieter gelten als zustandslos. Dies bedeutet, dass Ihr Laufwerks Anbieter alle Zustandsinformationen erstellen muss, die von der Windows PowerShell-Laufzeit benötigt werden, wenn der Anbieter aufgerufen wird.

Bei diesem Laufwerk Anbieter enthalten Zustandsinformationen die Verbindung mit der Datenbank, die als Teil der Laufwerk Informationen beibehalten wird. Der folgende Code zeigt, wie diese Informationen im [System.Management.Automation.PSDriveinfo](/dotnet/api/System.Management.Automation.PSDriveInfo) -Objekt gespeichert werden, das das Laufwerk beschreibt:

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs" range="130-151":::

## <a name="creating-a-drive"></a>Erstellen eines Laufwerks

Damit die Windows PowerShell-Laufzeit ein Laufwerk erstellen kann, muss der Laufwerk Anbieter die [System. Management. Automation. Provider. drivecmdletprovider. newdrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) -Methode implementieren. Der folgende Code zeigt die Implementierung der [System. Management. Automation. Provider. drivecmdletprovider. newdrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) -Methode für diesen Laufwerk Anbieter:

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs" range="42-84":::

Die außer Kraft setzung dieser Methode sollte folgende Aktionen ausführen:

- Überprüfen Sie, ob die [System.Management.Automation.PSDriveingefo. Der root *](/dotnet/api/System.Management.Automation.PSDriveInfo.Root) -Member ist vorhanden, und es kann eine Verbindung mit dem Datenspeicher hergestellt werden.
- Erstellen Sie ein Laufwerk, und füllen Sie das Verbindungs Mitglied auf, um das `New-PSDrive` Cmdlet zu unterstützen.
- Überprüfen Sie das [System.Management.Automation.PSDriveinfo](/dotnet/api/System.Management.Automation.PSDriveInfo) -Objekt für das vorgeschlagene Laufwerk.
- Ändern Sie das [System.Management.Automation.PSDriveinfo](/dotnet/api/System.Management.Automation.PSDriveInfo) -Objekt, das das Laufwerk mit den erforderlichen Leistungs-oder Zuverlässigkeits Informationen beschreibt, oder stellen Sie zusätzliche Daten für Aufrufer mit dem Laufwerk bereit.
- Behandeln Sie Fehler mithilfe der [System. Management. Automation. Provider. cmdletprovider. Write-error](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.WriteError) -Methode, und geben Sie dann zurück `null` .

  Diese Methode gibt entweder die Laufwerk Informationen zurück, die an die-Methode oder eine anbieterspezifische Version der Methode übermittelt wurden.

## <a name="attaching-dynamic-parameters-to-newdrive"></a>Dynamische Parameter werden an newdrive angefügt.

Das `New-PSDrive` Cmdlet, das von Ihrem Laufwerk Anbieter unterstützt wird, erfordert möglicherweise zusätzliche Parameter. Um diese dynamischen Parameter an das Cmdlet anzufügen, implementiert der Anbieter die [System. Management. Automation. Provider. drivecmdletprovider. newdrivedynamicparameters *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDriveDynamicParameters) -Methode. Diese Methode gibt ein Objekt zurück, das über Eigenschaften und Felder mit Attribut Attributen verfügt, die einer Cmdlet-Klasse oder einem [System. Management. Automation. runtimedefinedparameterdictionary](/dotnet/api/System.Management.Automation.RuntimeDefinedParameterDictionary) -Objekt ähneln.

Dieser Laufwerk Anbieter setzt diese Methode nicht außer Kraft. Der folgende Code zeigt jedoch die Standard Implementierung dieser Methode:

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testprovidernewdrivedynamicparameters](Msh_samplestestcmdlets#testprovidernewdrivedynamicparameters)]  -->

## <a name="removing-a-drive"></a>Entfernen eines Laufwerks

Der Laufwerks Anbieter muss die [System. Management. Automation. Provider. drivecmdletprovider. removedrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) -Methode implementieren, um die Datenbankverbindung zu schließen. Diese Methode schließt die Verbindung mit dem Laufwerk, nachdem alle anbieterspezifischen Informationen bereinigt wurden.

Der folgende Code zeigt die Implementierung der [System. Management. Automation. Provider. drivecmdletprovider. removedrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) -Methode für diesen Laufwerk Anbieter:

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs" range="91-116":::

Wenn das Laufwerk entfernt werden kann, sollte die-Methode die an die Methode übergebenen Informationen über den-Parameter zurückgeben `drive` . Wenn das Laufwerk nicht entfernt werden kann, sollte die Methode eine Ausnahme schreiben und dann zurückgeben `null` . Wenn der Anbieter diese Methode nicht außer Kraft setzt, gibt die Standard Implementierung dieser Methode nur die als Eingabe übergebenen Laufwerks Informationen zurück.

## <a name="initializing-default-drives"></a>Standard Laufwerke werden initialisiert.

Der Laufwerks Anbieter implementiert die [System.Management.Automation.Provider.Drivecmdletprovider.Initializedefaultdrives *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.InitializeDefaultDrives) -Methode zum Einbinden von Laufwerken. Beispielsweise kann der Active Directory Anbieter ein Laufwerk für den Standard namens Kontext einbinden, wenn der Computer einer Domäne hinzugefügt wird.

Diese Methode gibt eine Auflistung von Laufwerk Informationen zu den initialisierten Laufwerken oder eine leere Auflistung zurück. Der Aufruf dieser Methode erfolgt, nachdem die Windows PowerShell-Runtime die [System. Management. Automation. Provider. cmdletprovider. Start *](/dotnet/api/System.Management.Automation.Provider.CmdletProvider.Start) -Methode aufgerufen hat, um den Anbieter zu initialisieren.

Dieser Laufwerk Anbieter überschreibt nicht die [System.Management.Automation.Provider.Drivecmdletprovider.Initializedefaultdrives *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.InitializeDefaultDrives) -Methode. Der folgende Code zeigt jedoch die Standard Implementierung, die eine leere Laufwerks Auflistung zurückgibt:

<!-- TODO!!!: review snippet reference  [!CODE [Msh_samplestestcmdlets#testproviderinitializedefaultdrives](Msh_samplestestcmdlets#testproviderinitializedefaultdrives)]  -->

#### <a name="things-to-remember-about-implementing-initializedefaultdrives"></a>Dinge, die Sie beim Implementieren von initializedefaultdrives beachten sollten

Alle Laufwerks Anbieter sollten ein Stamm Laufwerk einbinden, um dem Benutzer die Auffindbarkeit zu erleichtern. Das Stamm Laufwerk kann Speicherorte auflisten, die als Stämme für andere eingebundene Laufwerke fungieren. Beispielsweise kann der Active Directory Anbieter ein Laufwerk erstellen, das die Namenskontexte auflistet, die in den `namingContext` Attributen der DSE-Stamm Umgebung (DSE) gefunden werden. Dadurch können Benutzer Einstellungspunkte für andere Laufwerke ermitteln.

## <a name="code-sample"></a>Codebeispiel

Einen umfassenden Beispielcode finden Sie unter [AccessDbProviderSample02-Codebeispiel](./accessdbprovidersample02-code-sample.md).

## <a name="testing-the-windows-powershell-drive-provider"></a>Testen des Windows PowerShell-Laufwerks Anbieters

Wenn Ihr Windows PowerShell-Anbieter bei Windows PowerShell registriert wurde, können Sie ihn testen, indem Sie die unterstützten Cmdlets in der Befehlszeile ausführen, einschließlich aller Cmdlets, die durch Ableitung verfügbar gemacht wurden. Testen Sie den Beispiel Laufwerk Anbieter.

1. Führen Sie das- `Get-PSProvider` Cmdlet aus, um die Liste der Anbieter abzurufen und sicherzustellen, dass der accessdb-Laufwerks Anbieter vorhanden ist:

   **PS->`Get-PSProvider`**

   Die folgende Ausgabe wird angezeigt:

   ```Output
   Name                 Capabilities                  Drives
   ----                 ------------                  ------
   AccessDB             None                          {}
   Alias                ShouldProcess                 {Alias}
   Environment          ShouldProcess                 {Env}
   FileSystem           Filter, ShouldProcess         {C, Z}
   Function             ShouldProcess                 {function}
   Registry             ShouldProcess                 {HKLM, HKCU}
   ```

2. Stellen Sie sicher, dass ein Datenbankserver Name (DSN) für die Datenbank vorhanden ist, indem Sie auf den **Datenquellen** Teil der **Verwaltungs Tools** für das Betriebssystem zugreifen. Doppelklicken Sie in der Tabelle **Benutzer-DSN** auf **MS Access Database** , und fügen Sie den Laufwerks Pfad hinzu `C:\ps\northwind.mdb` .

3. Erstellen Sie ein neues Laufwerk mithilfe des Beispiel-Laufwerk Anbieters:

   ```powershell
   new-psdrive -name mydb -root c:\ps\northwind.mdb -psprovider AccessDb`
   ```

   Die folgende Ausgabe wird angezeigt:

   ```Output
   Name     Provider     Root                   CurrentLocation
   ----     --------     ----                   ---------------
   mydb     AccessDB     c:\ps\northwind.mdb
   ```

4. Überprüfen Sie die Verbindung. Da die Verbindung als Mitglied des Laufwerks definiert ist, können Sie Sie mithilfe des Cmdlets Get-pddrive überprüfen.

   > [!NOTE]
   > Der Benutzer kann noch nicht als Laufwerk mit dem Anbieter interagieren, da der Anbieter für diese Interaktion Container Funktionen benötigt. Weitere Informationen finden Sie unter [Erstellen eines Windows PowerShell-Container Anbieters](./creating-a-windows-powershell-container-provider.md).

   **PS-> (Get-PSDrive mydb). Connection**

   Die folgende Ausgabe wird angezeigt:

   ```Output
   ConnectionString  : Driver={Microsoft Access Driver (*.mdb)};DBQ=c:\ps\northwind.mdb
   ConnectionTimeout : 15
   Database          : c:\ps\northwind
   DataSource        : ACCESS
   ServerVersion     : 04.00.0000
   Driver            : odbcjt32.dll
   State             : Open
   Site              :
   Container         :
   ```

5. Entfernen Sie das Laufwerk, und beenden Sie die Shell:

   ```powershell
   PS> remove-psdrive mydb
   PS> exit
   ```

## <a name="see-also"></a>Weitere Informationen

[Erstellen von Windows PowerShell-Anbietern](./how-to-create-a-windows-powershell-provider.md)

[Entwerfen Ihres Windows PowerShell-Anbieters](./designing-your-windows-powershell-provider.md)

[Erstellen eines Windows PowerShell-Standardanbieters](./creating-a-basic-windows-powershell-provider.md)
