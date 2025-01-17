![gematik GmbH](docs/img/Gematik_Logo_Flag.png)

# Gematik Referenzvalidator

<details>
  <summary>Inhaltsverzeichnis</summary>
  <ol>
    <li>
      <a href="#über-das-projekt">Über das Projekt</a>
       <ul>
        <li><a href="#releasenotes">Release Notes</a></li>
      </ul>     
    </li>
    <li>
      <a href="#funktionsumfang">Funktionsumfang</a>
      <ul>
        <li><a href="#e-rezept-modul">E-Rezept-Modul</a></li>
      </ul>
    </li>
    <li>
      <a href="#erste-schritte">Erste Schritte</a>
      <ul>
        <li><a href="#voraussetzungen">Voraussetzungen</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#verwendung">Verwendung</a></li>
    <li><a href="#lizenz">Lizenz</a></li>
    <li><a href="#kontakt">Kontakt</a></li>
  </ol>
</details>

## Über das Projekt


Der Referenzvalidator ermöglicht eine erweiterte Validierung von FHIR-Ressourcen, die in den Anwendungen der Telematikinfrastruktur (TI) verwendet werden. Der Referenzvalidator liefert autoritative Antworten zur Validität von übertragenen Datensätzen und ist somit eine Referenz für eventuell sonst im Rahmen einer TI-Anwendung eingesetzte FHIR-Validatoren. 

Siehe [Use Cases, Anforderungen, Architektur, Entwicklungsprozess](docs/concept/concept.md) für weitere Informationen.

### Release Notes

Siehe [Release Notes](ReleaseNotes.md)

## Funktionsumfang

- Validierung von FHIR-Ressourcen anhand der referenzierten [Profile](#unterstützte-profile-und-versionen)
- Der Prüfumfang entspricht dem Umfang des [HL7 Java Validators](https://www.hl7.org/fhir/validation.html):
  - Struktur: Alle Elemente einer Instanz MÜSSEN in dem referenzierten Profil definiert sein
  - Kardinalität: Die Min/Max-Angaben aller Eigenschaften sind berücksichtigt
  - Wertebereiche: Die Wertebereiche von Eigenschaften werden berücksichtigt (einschließlich aufgelistete Codes)
  - Coding/CodeableConcept bindings: Die Code-Angaben in einer Instanz entsprechen der Definition des Kodierungssystems aus dem Profil
  - Constraints/Invariants: Die für die Eigenschaften im Profil definierten Regeln sind eingehalten

Dabei gilt folgendes:
- Instanzen mit unbekannten Profilen führen zum invaliden Ergebnis
- Instanzen mit unbekannten Extensions führen zum invaliden Ergebnis

### E-Rezept-Modul

Abweichend vom allgemeinen Prüfumfang verhält sich das E-Rezept-Modul wie folgt:
- Codes aus den CodeSystemen `http://fhir.de/CodeSystem/ifa/pzn` und `http://fhir.de/CodeSystem/ask` werden nicht validiert
- Fehler, die bei Validierung von `http://fhir.abda.de/eRezeptAbgabedaten/StructureDefinition/DAV-PR-ERP-AbgabedatenBundle|1.0.3` im Zusammenhang mit falschen Angaben bei `http://fhir.abda.de/Identifier/DAV-Herstellerschluessel` stehen, werden ignoriert und führen zum **validen** Ergebnis

#### Unterstützte Profile und Versionen
* https://fhir.kbv.de/StructureDefinition/KBV_PR_ERP_Bundle
    * 1.0.1
    * 1.0.2
* https://gematik.de/fhir/StructureDefinition/ErxMedicationDispense
    * 1.0.3
    * 1.0.3-1 (Instanzen ohne Versionsangaben werden gegen die Version 1.0.3-1 validiert)
    * 1.1.1
* https://gematik.de/fhir/StructureDefinition/ErxReceipt
    * 1.0.3
    * 1.0.3-1 (Instanzen ohne Versionsangaben werden gegen die Version 1.0.3-1 validiert)
    * 1.1.1
* http://fhir.abda.de/eRezeptAbgabedaten/StructureDefinition/DAV-PR-ERP-AbgabedatenBundle
    * 1.0.3
    * 1.1.0
    * 1.2
* https://fhir.gkvsv.de/StructureDefinition/GKVSV_PR_TA7_Sammelrechnung_Bundle
    * 1.0.4
    * 1.0.5
    * 1.0.6
    * 1.1.0
    * 1.2
  
#### Eingebundene Packages (R4) 
* de.basisprofil.r4-0.9.13.tgz
* kbv.basis-1.1.3.tgz
* kbv.ita.for-1.0.3.tgz
* kbv.ita.erp-1.0.1.tgz
* kbv.ita.erp-1.0.2.tgz
* de.gematik.erezept-workflow.r4-1.0.3-1.tgz
* de.gematik.erezept-workflow.r4-1.1.1.tgz
* de.abda.erezeptabgabedatenbasis-1.1.0.tgz
* de.abda.erezeptabgabedatenbasis-1.1.3.tgz
* de.abda.erezeptabgabedatenbasis-1.2.0.tgz
* de.abda.erezeptabgabedaten-1.0.3.tgz
* de.abda.erezeptabgabedaten-1.1.2.tgz
* de.abda.erezeptabgabedaten-1.2.0.tgz
* de.gkvsv.erezeptabrechnungsdaten-1.0.4.tgz
* de.gkvsv.erezeptabrechnungsdaten-1.0.5.tgz
* de.gkvsv.erezeptabrechnungsdaten-1.0.6.tgz
* de.gkvsv.erezeptabrechnungsdaten-1.1.0.tgz
* de.gkvsv.erezeptabrechnungsdaten-1.2.0.tgz

[Validierungsrelevante Codesysteme und Valuesets der KBV:](https://update.kbv.de/ita-update/DigitaleMuster/ERP/KBV_FHIR_eRP_V1.0.2_zur_Validierung.zip)
* dav.kbv.sfhir.cs.vs-1.0.2-json.tgz
* dav.kbv.sfhir.cs.vs-1.0.3-json.tgz (Anpassung DARREICHUNGSFORM v1.09 ab 01.04.2022)

#### Anpassungen der Packages:
- delete examples in Packages
- de.gematik.erezept-workflow.r4-1.0.3-1.tgz
  - Delete ProFile StructureDefinition-ChargeItem-erxChargeItem.json (keine Relevanz - future use)
- kbv.ita.erp-1.0.1.tgz
  - Change Profile KBV_PR_ERP_Prescription.json (MedicationRequest.insurance = "type":[{"code":"Reference","targetProfile":["https://fhir.kbv.de/StructureDefinition/KBV_PR_FOR_Coverage|1.0.3"]}])
- de.abda.erezeptabgabedatenbasis-1.1.0.tgz -> siehe [ChangeLog.md des ABDA Referenzvalidators](https://github.com/DAV-ABDA/eRezept-Referenzvalidator/blob/main/CHANGELOG.md) - Version 0.9.6

## Erste Schritte

### Voraussetzungen

Der Referenzvalidator wird als Java-Bibliothek und als Konsolenanwendung verteilt. Für die Verwendung ist JDK 11 erforderlich (z.B. [AdoptOpenJDK](https://adoptopenjdk.net/)).  

### Installation

#### Konsolenanwendung

Für die Verwendung der Konsolenanwendung soll lediglich das Release-Paket entpackt werden. 

#### Java-Bibliothek

Die Installation als Java-Bibliothek kann zur Zeit nur manuell erfolgen, indem die referencevalidatror-lib.jar dem Classpath einer Anwendung hinzugefügt wird. Veröffentlichung in Maven Central und Einbindung als Maven-Dependency sind in Planung.

## Verwendung

### Konsolenanwendung

Der Referenzvalidator erfordert als Eingabe einen Modulnamen und einen gültigen Pfad zur Datei, die eine FHIR-Ressource enthält:

    java -jar referencevalidator-cli.jar -m erp -i c:\temp\example.xml

### Java-Bibliothek

Folgende Beispiele veranschaulichen die Verwendung vom Referenzvalidator in einer Java-Anwendung.

Validierung einer FHIR-Ressource aus einer Datei:

    ValidationModule erpModule = ValidationModuleFactory.createValidationModule(SupportedValidationModule.ERP);
    Path path = Paths.get("c:/temp/KBV_PR_ERP_Bundle.xml");
    ValidationResult result = erpModule.validateFile(path);
    System.out.println(result.isValid());
    System.out.println(result.getFilteredValidationMessages());

Validierung einer FHIR-Ressource als String:

    ValidationModule erpModule = ValidationModuleFactory.createValidationModule(SupportedValidationModule.ERP);
    String fhirRessource = "<Bundle xmlns=\"http://hl7.org/fhir\">\n"
        + "    <id value=\"fb16b9fb-eca9-4a64-b257-083ac87c9c9c\"/>\n"
        + "    <meta>\n"
        + "        <profile value=\"https://fhir.kbv.de/StructureDefinition/KBV_PR_ERP_Bundle|1.0.1\"/>\n"
        + "        \n"
        + "    </meta>\n"
        + "</Bundle>";
    ValidationResult result = erpModule.validateString(fhirRessource);
    System.out.println(result.isValid());
    System.out.println(result.getFilteredValidationMessages());

## Lizenz

Siehe [Apache License, Version 2.0](LICENSE)

Teile des Projekts basieren auf dem [ABDA E-Rezept-Referenzvalidator (Copyright 2022 Deutscher Apothekerverband (DAV))](https://github.com/DAV-ABDA/eRezept-Referenzvalidator/), der unter [Apache License, Version 2.0](https://www.apache.org/licenses/LICENSE-2.0) steht. Modifizierte Quellcodedateien sind im Quellcode als solche gekennzeichnet.  

## Kontakt

Fragen, Anregungen, Bug Reports und Feature requests sind willkommen und können gerne über die [GitHub Issues](https://github.com/gematik/app-referencevalidator/issues) oder über [referenzvalidator&commat;gematik.de](mailto:referenzvalidator&commat;gematik.de) eingereicht werden.