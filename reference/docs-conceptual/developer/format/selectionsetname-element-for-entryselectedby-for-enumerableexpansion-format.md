---
title: Selectionsetname-Element für entryselectedby für enumerableexpansion (Format) | Microsoft-Dokumentation
ms.date: 09/13/2016
ms.openlocfilehash: 8745ef9e6f326c3e8a5dbf185a595bbe93e92414
ms.sourcegitcommit: 0907b8c6322d2c7c61b17f8168d53452c8964b41
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/05/2020
ms.locfileid: "87785318"
---
# <a name="selectionsetname-element-for-entryselectedby-for-enumerableexpansion-format"></a>Element „SelectionSetName“ für EntrySelectedBy für EnumerableExpansion (Format)

Gibt den Satz von .NET-Typen an, die durch diese Definition erweitert werden.

Configuration-Element (Format) DefaultSettings-Element (Format) enumerableerweiterungen-Element (Format) enumerableweiterung-Element (Format) entryselectedby-Element für enumerableexpansion (Format) selectionsetname-Element für entryselectedby für enumerableexpansion (Format)

## <a name="syntax"></a>Syntax

```xml
<SelectionSetName>NameofSelectionSet</SelectionSetName>

```

## <a name="attributes-and-elements"></a>Attribute und Elemente

In den folgenden Abschnitten werden Attribute, untergeordnete Elemente und das übergeordnete Element des- `SelectionSetName` Elements beschrieben.

### <a name="attributes"></a>Attribute

Keine

### <a name="child-elements"></a>Untergeordnete Elemente

Keine

### <a name="parent-elements"></a>Übergeordnete Elemente

|Element|BESCHREIBUNG|
|-------------|-----------------|
|[Element „EntrySelectedBy“ für EnumerableExpansion (Format)](./entryselectedby-element-for-enumerableexpansion-format.md)|Definiert die .net-Auflistungs Objekte, die durch diese Definition erweitert werden.|

## <a name="text-value"></a>Textwert

Geben Sie den Namen des Auswahl Satzes an.

## <a name="remarks"></a>Bemerkungen

Jede Definition muss einen oder mehrere Typnamen, einen Auswahl Satz oder eine Auswahlbedingung angeben.

Auswahl Sätze werden in der Regel verwendet, wenn Sie eine Gruppe von Objekten definieren möchten, die in mehreren Ansichten verwendet werden. Beispielsweise können Sie eine Tabellenansicht und eine Listenansicht für denselben Satz von Objekten erstellen. Weitere Informationen zum Definieren von Auswahl Sätzen finden Sie unter [Definieren von Objekt Sätzen für eine Sicht](./defining-selection-sets.md).

## <a name="see-also"></a>Weitere Informationen

[Definieren von Auswahlgruppen](./defining-selection-sets.md)

[Element „EntrySelectedBy“ für EnumerableExpansion (Format)](./entryselectedby-element-for-enumerableexpansion-format.md)

[Schreiben einer PowerShell-Formatierungsdatei](./writing-a-powershell-formatting-file.md)
