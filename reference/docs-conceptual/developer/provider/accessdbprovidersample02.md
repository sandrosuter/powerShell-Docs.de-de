---
title: AccessDBProviderSample02 | Microsoft-Dokumentation
ms.date: 09/13/2016
ms.openlocfilehash: e9a0444d17bec230633e1dd1709455f6ba83dd5c
ms.sourcegitcommit: 0907b8c6322d2c7c61b17f8168d53452c8964b41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87786899"
---
# <a name="accessdbprovidersample02"></a>AccessDBProviderSample02

In diesem Beispiel wird gezeigt, wie die Methoden [System. Management. Automation. Provider. drivecmdletprovider. newdrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) und [System. Management. Automation. Provider. drivecmdletprovider. removedrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) überschrieben werden, um Aufrufe der `New-PSDrive` -und- `Remove-PSDrive` Cmdlets zu unterstützen. Die Anbieter Klasse in diesem Beispiel wird von der [System. Management. Automation. Provider. drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) -Klasse abgeleitet.

## <a name="demonstrates"></a>Zeigt

> [!IMPORTANT]
> Ihre Anbieter Klasse wird wahrscheinlich von einer der folgenden Klassen abgeleitet und kann möglicherweise andere Anbieter Schnittstellen implementieren:
>
> - [System. Management. Automation. Provider. itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider) -Klasse. Siehe [AccessDBProviderSample03](./accessdbprovidersample03.md).
> - [System. Management. Automation. Provider. containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider) -Klasse. Siehe [AccessDBProviderSample04](./accessdbprovidersample04.md).
> - [System. Management. Automation. Provider. navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider) -Klasse. Siehe [AccessDBProviderSample05](./accessdbprovidersample05.md).
>
> Weitere Informationen zum Auswählen der Anbieter Klasse, von der basierend auf den Anbieter Features abgeleitet werden soll, finden [Sie unter Entwerfen des Windows PowerShell-Anbieters](./provider-types.md).

Dieses Beispiel zeigt Folgendes:

- Deklarieren des `CmdletProvider` Attributs.

- Definieren einer Anbieter Klasse, die von der [System. Management. Automation. Provider. drivecmdletprovider](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider) -Klasse Laufwerks gesteuert wird.

- Überschreiben der [System. Management. Automation. Provider. drivecmdletprovider. newdrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) -Methode, um das Erstellen neuer Laufwerke zu unterstützen. (Dieses Beispiel zeigt nicht, wie dem Cmdlet dynamische Parameter hinzugefügt werden `New-PSDrive` .)

- Überschreiben der [System. Management. Automation. Provider. drivecmdletprovider. removedrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) -Methode, um das Entfernen vorhandener Laufwerke zu unterstützen.

## <a name="example"></a>Beispiel

In diesem Beispiel wird gezeigt, wie die Methoden [System. Management. Automation. Provider. drivecmdletprovider. newdrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.NewDrive) und [System. Management. Automation. Provider. drivecmdletprovider. removedrive *](/dotnet/api/System.Management.Automation.Provider.DriveCmdletProvider.RemoveDrive) überschrieben werden. Bei diesem Beispiel Anbieter werden bei der Erstellung eines Laufwerks die Verbindungsinformationen in einem- `AccessDBPsDriveInfo` Objekt gespeichert.

:::code language="csharp" source="~/../powershell-sdk-samples/SDK-2.0/csharp/AccessDBProviderSample02/AccessDBProviderSample02.cs" range="11-154":::

## <a name="see-also"></a>Weitere Informationen

[System. Management. Automation. Provider. itemcmdletprovider](/dotnet/api/System.Management.Automation.Provider.ItemCmdletProvider)

[System. Management. Automation. Provider. containercmdletprovider](/dotnet/api/System.Management.Automation.Provider.ContainerCmdletProvider)

[System. Management. Automation. Provider. navigationcmdletprovider](/dotnet/api/System.Management.Automation.Provider.NavigationCmdletProvider)

[Entwerfen eines Windows PowerShell-Anbieters](./provider-types.md)
