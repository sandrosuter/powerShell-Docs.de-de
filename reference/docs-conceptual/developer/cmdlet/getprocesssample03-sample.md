---
title: GetProcessSample03-Beispiel | Microsoft-Dokumentation
ms.date: 09/13/2016
ms.openlocfilehash: 09df93792ab611e167279bc35755d8d6c28e7cf3
ms.sourcegitcommit: 0907b8c6322d2c7c61b17f8168d53452c8964b41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87784213"
---
# <a name="getprocesssample03-sample"></a>GetProcessSample03-Beispiel

In diesem Beispiel wird gezeigt, wie ein Cmdlet implementiert wird, das die Prozesse auf dem lokalen Computer abruft. Sie stellt einen `Name` Parameter bereit, der ein Objekt aus der Pipeline oder einen Wert aus einer Eigenschaft eines Objekts akzeptieren kann, dessen Eigenschaftsname mit dem Parameternamen identisch ist. Dieses Cmdlet ist eine vereinfachte Version des `Get-Process` Cmdlets, das von Windows PowerShell 2,0 bereitgestellt wird.

## <a name="how-to-build-the-sample-using-visual-studio"></a>So erstellen Sie das Beispiel mithilfe von Visual Studio.

1. Navigieren Sie mit installiertem Windows PowerShell 2,0 SDK zum Ordner GetProcessSample03. Der Standard Speicherort ist "c:\Programme (x86) \Microsoft SDKs\Windows\v7.0\samples\sysmgmt\windowspowershell\csharp\getprocesssample03.".

2. Doppelklicken Sie auf das Symbol für die Projektmappendatei (. sln). Dadurch wird das Beispiel Projekt in Visual Studio geöffnet.

3. Wählen Sie im Menü **Erstellen** die Option **Projektmappe erstellen** aus.

    Die Bibliothek für das Beispiel wird im Standardordner \bin oder \bin\Debug erstellt.

### <a name="how-to-run-the-sample"></a>Ausführen des Beispiels

1. Erstellen Sie den folgenden Modul Ordner:

    `[user]/documents/windowspowershell/modules/GetProcessSample03`

2. Kopieren Sie die Beispielassembly in den Modul Ordner.

3. Starten Sie Windows PowerShell.

4. Führen Sie den folgenden Befehl aus, um die Assembly in Windows PowerShell zu laden:

    `Import-module getprossessample03`

5. Führen Sie den folgenden Befehl aus, um das Cmdlet auszuführen:

    `get-proc`

## <a name="requirements"></a>Requirements (Anforderungen)

Dieses Beispiel erfordert Windows PowerShell 2,0.

## <a name="demonstrates"></a>Zeigt

In diesem Beispiel wird Folgendes veranschaulicht:

- Deklarieren einer Cmdlet-Klasse mithilfe des Cmdlet-Attributs.

- Deklarieren eines Cmdlet-Parameters mithilfe des Parameter-Attributs.

- Angeben der Position des Parameters.

- Angeben, dass der Parameter Eingaben aus der Pipeline annimmt. Die Eingabe kann aus einem Objekt oder einem Wert aus einer Eigenschaft eines Objekts entnommen werden, dessen Eigenschaftsname mit dem Parameternamen identisch ist.

- Deklarieren eines Validierungs Attributs für die Parameter Eingabe.

## <a name="example"></a>Beispiel

Dieses Beispiel zeigt eine Implementierung des Get-proc-Cmdlets, das einen `Name` Parameter enthält, der Eingaben aus der Pipeline akzeptiert.

```csharp
namespace Microsoft.Samples.PowerShell.Commands
{
  using System;
  using System.Diagnostics;
  using System.Management.Automation;           // Windows PowerShell namespace
  #region GetProcCommand

  /// <summary>
  /// This class implements the get-proc cmdlet.
  /// </summary>
  [Cmdlet(VerbsCommon.Get, "Proc")]
  public class GetProcCommand : Cmdlet
  {
    #region Parameters

    /// <summary>
    /// The names of the processes retrieved by the cmdlet.
    /// </summary>
    private string[] processNames;

    /// <summary>
    /// Gets or sets the names of the
    /// process that the cmdlet will retrieve.
    /// </summary>
    [Parameter(
               Position = 0,
               ValueFromPipeline = true,
               ValueFromPipelineByPropertyName = true)]
    [ValidateNotNullOrEmpty]
    public string[] Name
    {
      get { return this.processNames; }
      set { this.processNames = value; }
    }

    #endregion Parameters

    #region Cmdlet Overrides

    /// <summary>
    /// The ProcessRecord method calls the Process.GetProcesses
    /// method to retrieve the processes specified by the Name
    /// parameter. Then, the WriteObject method writes the
    /// associated processes to the pipeline.
    /// </summary>
    protected override void ProcessRecord()
    {
      // If no process names are passed to the cmdlet, get all
      // processes.
      if (this.processNames == null)
      {
        WriteObject(Process.GetProcesses(), true);
      }
      else
      {
        // If process names are passed to the cmdlet, get and write
        // the associated processes.
        foreach (string name in this.processNames)
        {
          WriteObject(Process.GetProcessesByName(name), true);
        }
      } // End if (processNames ...)
    } // End ProcessRecord.

    #endregion Overrides
  } // End GetProcCommand.
  #endregion GetProcCommand
}
```

## <a name="see-also"></a>Weitere Informationen

[Schreiben eines Windows PowerShell-Cmdlets](./writing-a-windows-powershell-cmdlet.md)
