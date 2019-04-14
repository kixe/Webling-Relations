Modul WeblingRelations
=======================

#### Webling ProcessWire API Schnittstelle


## Installation

Bei der Installation des Moduls muß die entsprechende Webling **Subdomain** und ein **API Key** mit entsprechenden Berechtigungen eingerichtet werden.

+++

## Konfiguration

### Relation

**Relation** beschreibt eine Beziehung zwischen einem Webling **Objekttyp** und einem ProcessWire **Template**. z.B. Objektyp 'member' und Template 'user'

#### Bedingungen
+ Pro **Objekttyp**, bzw. **Template** kann jeweils **nur eine Relation** erstellt werden.
+ Es können nur Templates verwendet werden denen das ProcessWire Feld **webling_ID** zugeordnet wurde. Das Feld wird bei der Installation durch das Modul automatisch erzeugt. Es ist zunächst nur für Nutzer mit der Rolle _**superuser**_ sicht- und editierbar. In den Feldeinstellungen können weitere Rollen zugewiesen werden. 

### Link

**Link** beschreibt eine Beziehung innerhalb einer Relation zwischen einem Webling **Property** (Feld) und einem ProcessWire **Feld**. Für die Art der Beziehung gibt es **4 Typen**

+ **show**  
Der Inhalt wird aus Webling eingelesen und in der aktuellen ProcessWire Session gespeichert. Das entsprechende ProcessWire Feld bleibt leer oder wird beim nächsten Speichern geleert. Eine Aktualisierung aus Webling erfolgt nach dem Start einer neuer ProcessWire Session, oder, wenn ein Wert in einem Feld vom Typ pull oder push verändert wurde und die Seite gespeichert wurde.

+ **hash**  
Der Inhalt wird aus Webling eingelesen und in der aktuellen ProcessWire Session gespeichert. Das entsprechende ProcessWire Feld wird mit einem Hashwert des Originalwertes befüllt. Dies ermöglicht den Webling Wert mit dem ProcessWire Wert zu vergleichen. Bei Inkosistenz wird ein entsprechender Hinweis ausgegeben. Eine Aktualisierung erfolgt wie beim Typ _**show**_. Der tatsächliche Wert wird nicht in der ProcessWire Datenbank gespeichert. Es ist nicht möglich aus den Daten in der ProcessWire Datenbank den tatsächlichen Wert zu ermitteln.

+ **pull**  
Inhalte werden bei jedem Speichern synchronisiert. Die Webling Datenbank ist führend. Beim Öffnen der ProcessWire Page-Edit Seite erscheint der Webling Wert.
Im Falle von Inkosistenz wird ein Hinweis ausgegeben, dass der Wert aktualisiert wurde.

+ **push**  
Inhalte werden bei jedem Speichern synchronisiert. Die ProcessWire Datenbank ist führend. Beim Öffnen der ProcessWire Page-Edit Seite wird der ProcessWire Wert geladen.
Im Falle von Inkosistenz wird eine Warnung ausgegeben.

Zusätzlich besteht die Möglichkeit die ProcessWire Page ID mit einem Webling Datenfeld zu verknüpfen. Hier ist nur der Typ **push** zu gelassen. Der Wert ist auf der ProcessWire Seite unveränderbar. Eine Aktualisierung des Wertes auf der Webling Seite findet jeweils nur dann statt, wenn von der ProcessWire Seite ein anderer **push** Wert erfolgreich aktualisiert wird.

#### Bedingungen
+ Pro **Property** bzw. **Feld** kann jeweils **nur ein Link** erstellt werden.
+ ProcessWire Felder müssen **access_control** aktiviert haben. Ohne diese Einstellung werden Daten zwar eingelesen und synchronisiert, es werden jedoch keine Zusatzinformationen oder Warnungen ausgegeben.
+ Bei der Einrichtung muß auf Kompatibilität der Datentypen geachtet werden. z.B. kann für das Feld Email nicht der Linktyp hash gewählt werden, das Format des Hashwertes für verschiedene Felder (z.B:email) bzw. Datentypen (z.B:date) nicht zulässig ist.

+++

## Funktionsweise

Die Schnittstelle synchronisiert im Hintergrund Daten zwischen ProcessWire und Webling.
Die Synchronisation wird jeweils durch das Laden des Editierbereichs oder das Speichern einer ProcessWire Seite ausgelöst. Zur Identifizierung muß auf der ProcessWire Seite die eindeutige **Webling-Objekt-ID** im Feld **webling_ID** vorhanden sein.

<small>_Version: 1.0.0 Datum: 2019-04-13_

