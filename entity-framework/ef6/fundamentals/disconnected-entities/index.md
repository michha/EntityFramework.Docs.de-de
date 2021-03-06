---
title: 'Arbeiten mit getrennten Entitäten: EF6'
author: divega
ms.date: 2016-10-23
ms.assetid: 12138003-a373-4817-b1b7-724130202f5f
ms.openlocfilehash: b496a9cba48946974844725c5df5e7df7351cf23
ms.sourcegitcommit: dadee5905ada9ecdbae28363a682950383ce3e10
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/27/2018
ms.locfileid: "42998225"
---
# <a name="working-with-disconnected-entities"></a>Arbeiten mit getrennten Entitäten
In einer Anwendung, die auf Entity Framework basiert, ist eine Kontextklasse für das Erfassen von Änderungen zuständig, die an nachverfolgten Entitäten vorgenommen werden. Durch Aufruf der SaveChanges-Methode werden vom Kontext nachverfolgte Änderungen in der Datenbank gespeichert. Bei der Arbeit mit n-schichtigen Anwendungen werden Entitätsobjekte normalerweise modifiziert, wenn keine Verbindung zum Kontext besteht. Sie müssen dann entscheiden, wie Änderungen nachverfolgt und an den Kontext zurückgemeldet werden. In diesem Artikel wird beschrieben, welche Möglichkeiten Sie haben, wenn Sie Entity Framework mit getrennten Entitäten verwenden.   

## <a name="web-service-frameworks"></a>Webdienstframeworks

Webdiensttechnologien unterstützen normalerweise Muster, mit denen Sie Änderungen an einzelnen getrennten Objekten übernehmen können. Mit der ASP.NET-Web-API können Sie z.B. Controlleraktionen (wie etwa Aufrufe an EF zum Übernehmen von Änderungen an Objekten in einer Datenbank) codieren. Mit den Tools der Web-API in Visual Studio können Sie leicht einen Web-API-Controller über das Entity Framework 6-Modell entwerfen. Weitere Informationen finden Sie unter [Using Web API 2 with Entity Framework 6 (Verwenden der Web-API mit Entity Framework 6)](https://docs.microsoft.com/en-us/aspnet/web-api/overview/data/using-web-api-with-entity-framework/).   

Es gab schon immer mehrere andere Webdiensttechnologien, die eine Integration in Entity Framework ermöglicht haben, wie z.B. [WCF Data Services](https://docs.microsoft.com/dotnet/framework/data/wcf/create-a-data-service-using-an-adonet-ef-data-wcf) und [RIA Services](https://docs.microsoft.com/en-us/previous-versions/dotnet/wcf-ria/ee707344(v=vs.91)).

## <a name="low-level-ef-apis"></a>EF-APIs auf niedriger Ebene

Wenn Sie keine bereits vorhandene n-schichtige Lösung verwenden möchten oder wenn Sie Controlleraktionen in einem Web-API-Dienst anpassen möchten, stellt Entity Framework auch APIs bereit, mit denen Sie Änderungen übernehmen können, die an einer getrennten Schicht vorgenommen wurden. Weitere Informationen finden Sie im Artikel zum [Hinzufügen, Anhängen und zu Entitätszuständen](~/ef6/saving/change-tracking/entity-state.md).  

## <a name="self-tracking-entities"></a>Entitäten mit Selbstnachverfolgung  

Das Nachverfolgen von Änderungen an beliebigen Entitätsdiagrammen, die vom EF-Kontext getrennt sind, ist ein schwierig zu lösendes Problem. Eine Möglichkeit zur Lösung ist die Codegenerierungsvorlage für Entitäten mit Selbstnachverfolgung. Diese Vorlage generiert Entitätsklassen, die Logik zum Nachverfolgen von an getrennten Schichten vorgenommenen Änderungen als Zustände in den Entitäten selbst enthält. Außerdem werden mehrere Erweiterungsmethoden generiert, die diese Änderungen auf einen Kontext anwenden.

Diese Vorlage kann nur mit Modellen verwendet werden, die mit dem EF-Designer erstellt wurden, und nicht mit Code First-Modellen. Weitere Informationen finden Sie unter [Self-Tracking Entities (Entitäten mit Selbstnachverfolgung)](self-tracking-entities/index.md).  

> [!IMPORTANT]
> Es wird nicht mehr empfohlen, die Vorlage für Entitäten mit Selbstnachverfolgung zu verwenden. Die Vorlage ist nur für die Unterstützung vorhandener Anwendungen weiterhin verfügbar. Wenn für Ihre Anwendung die Arbeit mit getrennten Diagrammen von Entitäten erforderlich ist, sollten Sie daher Alternativen erwägen, wie z.B. [nachverfolgbare Entitäten](http://trackableentities.github.io/). Diese Technologie ähnelt den Entitäten mit Selbstnachverfolgung und wird von der Community aktiver entwickelt. Alternativ dazu können Sie auch benutzerdefinierten Code mithilfe von APIs auf niedriger Ebene zur Änderungsnachverfolgung schreiben.
