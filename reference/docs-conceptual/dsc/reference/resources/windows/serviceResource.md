---
ms.date: 09/20/2019
keywords: DSC,PowerShell,Konfiguration,Setup,Einrichtung
title: DSC-Ressource „Service“
ms.openlocfilehash: acd0710fb4b131876e3edece15b07cff8e9a8a9e
ms.sourcegitcommit: 173556307d45d88de31086ce776770547eece64c
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 05/19/2020
ms.locfileid: "83557004"
---
# <a name="dsc-service-resource"></a>DSC-Ressource „Service“

> Gilt für: Windows PowerShell 4.0, Windows PowerShell 5.x

Die Ressource **Service** in Windows PowerShell DSC bietet einen Mechanismus zum Verwalten von Diensten auf dem Zielknoten.

## <a name="syntax"></a>Syntax

```Syntax
Service [string] #ResourceName
{
    Name = [string]
    [ BuiltInAccount = [string] { LocalService | LocalSystem | NetworkService }  ]
    [ Credential = [PSCredential] ]
    [ StartupType = [string] { Automatic | Disabled | Manual }  ]
    [ State = [string] { Running | Stopped }  ]
    [ Description = [string] ]
    [ DisplayName = [string] ]
    [ Path = [string] ]
    [ DependsOn = [string[]] ]
    [ Ensure = [string] { Absent | Present } ]
    [ PsDscRunAsCredential = [PSCredential] ]
}
```

## <a name="properties"></a>Eigenschaften

|Eigenschaft |BESCHREIBUNG |
|---|---|
|Name |Gibt den Namen des Diensts an. Beachten Sie, dass sich dieser mitunter vom Anzeigenamen unterscheidet. Mit dem Cmdlet `Get-Service` können Sie eine Liste der Dienste und ihren aktuellen Status abrufen. |
|BuiltInAccount |Gibt das zu verwendende Anmeldekonto für den Dienst an. Die für diese Eigenschaft zulässigen Werte sind: **LocalService**, **LocalSystem** und **NetworkService**. |
|Anmeldeinformationen |Gibt die Anmeldeinformationen für das Konto an, unter dem der Dienst ausgeführt wird. Diese Eigenschaft und die **BuiltinAccount**-Eigenschaft können nicht zusammen verwendet werden. |
|StartupType |Gibt den Starttyp für den Dienst an. Die für diese Eigenschaft zulässigen Werte sind: **Automatic**, **Disabled** und **Manual**. |
|State |Gibt den Status an, den Sie für den Dienst sicherstellen möchten. Die Werte sind: **Running** oder **Stopped**. |
|BESCHREIBUNG |Gibt die Beschreibung des Zieldiensts an. |
|DisplayName |Gibt den Anzeigenamen des Zieldiensts an. |
|`Path` |Gibt den Pfad zur Binärdatei eines neuen Diensts an. |

## <a name="common-properties"></a>Allgemeine Eigenschaften

|Eigenschaft |BESCHREIBUNG |
|---|---|
|DependsOn |Gibt an, dass die Konfiguration einer anderen Ressource ausgeführt werden muss, bevor diese Ressource konfiguriert wird. Wenn beispielsweise die ID des Skriptblocks mit der Ressourcenkonfiguration, den Sie zuerst ausführen möchten, „ResourceName“ und dessen Typ „ResourceType“ ist, lautet die Syntax für das Verwenden dieser Eigenschaft `DependsOn = "[ResourceType]ResourceName"`. |
|Ensure |Gibt an, ob der Zieldienst auf dem System vorhanden ist. Legen Sie diese Eigenschaft auf **Absent** fest, um sicherzustellen, dass der Zieldienst nicht vorhanden ist. Das Festlegen auf **Present** stellt sicher, dass der Zieldienst vorhanden ist. Der Standardwert ist **Present**. |
|PsDscRunAsCredential |Legt die Anmeldeinformationen für die Ausführung der gesamten Ressource fest. |

> [!NOTE]
> Die allgemeine Eigenschaft **PsDscRunAsCredential** wurde in WMF 5.0 hinzugefügt, um das Ausführen einer beliebigen DSC-Ressource in Verbindung mit anderen Anmeldeinformationen zu ermöglichen. Weitere Informationen finden Sie unter [Use Credentials with DSC Resources](../../../configurations/runasuser.md) (Verwenden von Anmeldeinformationen mit DSC-Ressourcen).

## <a name="example"></a>Beispiel

```powershell
configuration ServiceTest
{
    Import-DscResource -ModuleName PSDesiredStateConfiguration
    Node localhost
    {

        Service ServiceExample
        {
            Name        = "TermService"
            StartupType = "Manual"
            State       = "Running"
        }
    }
}
```
