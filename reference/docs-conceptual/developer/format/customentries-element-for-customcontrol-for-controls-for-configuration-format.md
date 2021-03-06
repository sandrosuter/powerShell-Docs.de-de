---
title: Customentries-Element für CustomControl für Steuerelemente für die Konfiguration (Format) | Microsoft-Dokumentation
ms.date: 09/13/2016
ms.openlocfilehash: b1f494cf1a254d71362830ba9eb0f4905a2a484d
ms.sourcegitcommit: 0907b8c6322d2c7c61b17f8168d53452c8964b41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87785981"
---
# <a name="customentries-element-for-customcontrol-for-controls-for-configuration-format"></a>Element „CustomEntries“ für CustomControl für Controls für Configuration (Format)

Stellt die Definitionen eines allgemeinen Steuer Elements bereit. Dieses Element wird verwendet, wenn ein gemeinsames Steuerelement definiert wird, das von allen Sichten in der Formatierungs Datei verwendet werden kann.

Konfigurationselement (Format) steuert Element des Konfigurations Elements (Format) Steuerelement für Steuerelemente für Konfiguration (Format) CustomControl-Element für Steuerelement für Configuration (Format) customentries-Element für CustomControl for Configuration (Format)

## <a name="syntax"></a>Syntax

```xml
<CustomEntries>
  <CustomEntry>...</CustomEntry>
</CustomEntries>

```

## <a name="attributes-and-elements"></a>Attribute und Elemente

In den folgenden Abschnitten werden Attribute, untergeordnete Elemente und das übergeordnete Element des- `CustomEntries` Elements beschrieben. Sie müssen mindestens ein untergeordnetes Element angeben.

### <a name="attributes"></a>Attribute

Keine

### <a name="child-elements"></a>Untergeordnete Elemente

|Element|Beschreibung|
|-------------|-----------------|
|[Element „CustomEntry“ für CustomControl für Controls für Configuration (Format)](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)|Stellt eine Definition des allgemeinen Steuer Elements bereit.|

### <a name="parent-elements"></a>Übergeordnete Elemente

|Element|Beschreibung|
|-------------|-----------------|
|[CustomControl-Element für das Steuer Element für die Konfiguration (Format)](./customcontrol-element-for-control-for-controls-for-configuration-format.md)|Definiert ein gängiges Steuerelement.|

## <a name="remarks"></a>Bemerkungen

In den meisten Fällen verfügt ein Steuerelement nur über eine Definition, die in einem einzelnen `CustomEntry` Element definiert ist. Es ist jedoch möglich, mehrere Definitionen zu verwenden, wenn Sie das gleiche Steuerelement verwenden möchten, um unterschiedliche .NET-Objekte anzuzeigen. In diesen Fällen können Sie ein- `CustomEntry` Element für jedes Objekt oder jede Gruppe von Objekten definieren.

## <a name="see-also"></a>Weitere Informationen

[CustomControl-Element für das Steuer Element für die Konfiguration (Format)](./customcontrol-element-for-control-for-controls-for-configuration-format.md)

[Element „CustomEntry“ für CustomControl für Controls für Configuration (Format)](./customentry-element-for-customcontrol-for-controls-for-configuration-format.md)

[Schreiben einer PowerShell-Formatierungsdatei](./writing-a-powershell-formatting-file.md)
