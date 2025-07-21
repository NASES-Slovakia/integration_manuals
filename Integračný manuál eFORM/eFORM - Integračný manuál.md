# Integračný manuál modulu elektronických formulárov (MEF) / eFORM

# Slovník pojmov

| **Skratka / Pojem**     | **Popis**                                                                                                         |
|-------------------------|------------------------------------------------------------------------------------------------------------------ |
| Autentifikácia          | Proces overenia identity používateľa žiadajúceho o službu alebo zdroj                                             |
| eDesk                   | Modul elektronických komunikačných schránok ÚPVS                                                                  |
| eForm / MEF             | Modul elektronických formulárov ÚPVS                                                                              |
|eID card	                | Autentifikačný nástroj pre elektronickú identitu                                                                  |
|eNotify	                | Notifikačný modul ÚPVS                                                                                            |
|G2G	                    | Modul procesnej integrácie a integrácie údajov – komunikačná časť, v zmysle zákona č. 305/2013 Z. z.  Modul ÚPVS vykonávajúci spracovanie synchrónnych a asynchrónnych požiadaviek vrátane orchestrácií komplexnejších procesov v rámci výkonu verejnej správy                                                                           |
| IAM	                    | Identiy Access Management (modul ÚPVS), komunikačná časť autentifikačného modulu v zmysle zákona č. 305/2013 Z.z. |
| ISVS	                  | Informačný systém verejnej správy                                                                                 |
| OVM	                    | Orgán verejnej moci                                                                                               |
| PO/FO	                  | Právnická osoba/Fyzická osoba                                                                                     |
| RFO	                    | Register fyzických osôb                                                                                           |
| RPO	                    | Register právnických osôb                                                                                         |
| SAML	                  | Security assertion markup language                                                                                |
| SkTalk	                | Štandard pre komunikáciu prostredníctvom ÚPVS                                                                     |
| SOAP	                  | Simple object Access protocol                                                                                     |
| SP	                    | Service provider                                                                                                  |
| SSO	                    | Single sign on                                                                                                    |
| STS	                    | Security token service                                                                                            |
| UIR	                    | Univerzálne integračné rozhranie                                                                                  |
| ÚPVS	                  | Ústredný portál verejnej správy                                                                                   |
| Účinnosť elektronického formulára a Platnosť elektronického formulára | V rámci tohto integračného manuálu sa zatiaľ používajú pojmy v pôvodnom význame podľa Vyhlášky č. 78/2020 Z. z. účinnej do roku 2022. Pojem „platnosť“ je používaný pre dátum začiatku publikácie elektronického formulára v eForm. Pojem "účinnosť“ je používaný pre dátum začiatku a konca účinnosti formulára bol v rámci novely Vyhlášky č. 78/2020 Z. z. v roku 2022 zmenený na „platnosť“.                                                                                                              |
| WSDL	                  | Web services description language                                                                                 |
| XML	                    | Extensible markup language                                                                                        |
| XSD	                    |XML schema definition                                                                                              |

# 1. Úvod

  Modul elektronických formulárov (eForm) zabezpečuje centrálne úložisko elektronických formulárov  v zmysle zákona č. 305/2013 Z.z. (ďalej aj „vzor“). Elektronické formuláre pre elektronické podania a elektronické úradné dokumenty sú platné výlučne v prípade, ak sú sprístupnené v module elektronických formulárov a v podobe, v akej sú v tomto module sprístupnené. 
Nad týmto úložiskom je vytvorené používateľské rozhranie pre verejnosť a pre gestorov elektronických formulárov z jednotlivých inštitúcií.  Pre integráciu voči ISVS poskytuje služby prostredníctvom G2G rozhraní. Tieto služby umožňujú základnú prácu so vzorom, ako je podanie žiadosti na registráciu vzoru elektronického formulára, jeho aktualizácia, či zneplatnenie. Taktiež však umožňujú služby pre vyhľadanie vzoru, alebo množiny vzorov v úložisku, poskytnutie vzoru elektronického formulára, jeho metadát a jednotlivých súvisiacich dokumentov - súčastí formulára. Nad jednotlivými vzormi je ďalej umožnené vytvárať vizualizácie s pomocou priložených súvisiacich dokumentov vzoru na základe jeho dát vo formáte XML. 
Pre ISVS je Dôležitou funkcionalitou aj možnosť získania informácie o zmenách v úložisku vzorov na základe tzv. publish/subscribe systému... Odporúčame preštudovanie aj dokumentov [Integračné Scenáre](https://github.com/NASES-Slovakia/integration_manuals/blob/main/Integra%C4%8Dn%C3%A9%20scen%C3%A1re/03_Integra%C4%8Dn%C3%A9_Scen%C3%A1re_OVM-PO_v1.4.5.docx) a [Integračný manuál modulu G2G](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20G2G)

Na integračný manuál modulu eForm nadväzuje dokumentácia k historickej aplikácií FormDesigner (aktuálne už nespĺňajúcej niektoré požiadavky Vyhlášky č. 78/2020 Z. z. o štandardoch pre IT VS):

•	UPG-9-5-Prirucka_pouzivatela_modulu_Designer-UPVSv_1-r2_0-v1_13_1.docx
<!-- Podľa J. Goffu by sa toto mohlo zmazať, nie je to aktuálna info a dokument už neexistuje ani v updatovanej forme -->
 
dostupná pre integrátorov na PFP (Partner Framework Portal) v sekcií „Dizajner“. V dokumente je detailne popísaný spôsob vytvárania vzorov formulárov prostredníctvom ÚPVS technológie ako aj použitie číselníkov a funkcie predvypĺňania eFormulárov.

Volanie služieb modulu eForm vyžaduje, aby príslušná identita, pod ktorou sa volanie uskutočňuje, mala pridelené oprávnenie **GESTOR** za danú inštitúciu.

Súčasťou tohto integračného manuálu je aj návod pre publikáciu elektronických formulárov obsahujúca aj požadované vlastnosti elektronických formulárov. Subjekty (OVM), ktoré realizujú registráciu eFormulárov prostredníctvom GUI Portálu slovensko.sk rovnako realizujú svoje aktivity v zmysle tohto dokumentu: 

•	[Návod pre orgány verejnej moci na registráciu a správu formulárov v module elektronických formulárov](https://www.slovensko.sk/_img/CMS4/Navody/navod_registracia_eform_ovm.pdf)

# 2. Integrácia na eFORM prostredíctvom UIR/G2G

Nasledujúca kapitola popisuje služby eForm publikované na rozhraní UIR – všetky volania musia obsahovať platný SAML token a všetky správy zabalené v obálke SKTalk v. 3. 

Technický použíivateľ, ktorým sa ISVS autentifikuje v rámci volaní webových služieb eForm, musí mať v module IAM pridelenú rolu **„R_EFORM_GESTOR“**.  

Pri registrácii elektronického formulára do modulu elektronických formulárov bude prebiehať validácia súčastí elektronického formulára pre kontrolu súladu voči povinným štandardom uvedeným vo Vyhláške č. 78/2020 Z. z. o štandardoch pre IT VS.

V prípade nevyhovenia validáciám bude žiadateľovi do elektronickej schránky zaslaná správa  „Validačný report“ s informáciami o jednotlivých chybách. Správa bude obsahovať aj identifikáciu konkrétnej časti formulára, ktorá nevyhovuje spolu s návodom na opravu, resp. odporúčanou uvádzanou hodnotou ak je jednoznačne určiteľná. Chyby budú rozdelené na „WARNING“ a „ERROR“, pričom chyba ERROR má za následok nezaregistrovanie formulára, o čom je žiadateľ informovaný samostatnou správou nezávislou od validačného reportu (ktorá je už dlhodobo popísaná v integračnom manuáli).

Zoznam validácií formulárov a ich konfigurácia sú zverejňované na Ústrednom portáli verejnej správy.
Podrobné informácie sú uvedené aj v [Návode pre orgány verejnej moci na registráciu a správu formulárov v module elektronických formulárov](https://www.slovensko.sk/_img/CMS4/Navody/navod_registracia_eform_ovm.pdf)

## 2.1 Asynchrónne služby modulu eFORM

Modul eForm prostredníctvom rozhrania UIR modulu G2G má uverejnenú sadu služieb. Tieto sú popísané v ďalších kapitolách. Pre volanie týchto služieb sú v module G2G zaregistrované ich CLASSNAME podľa nasledovnej tabuľky: 

| **CLASSNAME**                                                   | **Poznámka**                                                                                                    |
|-----------------------------------------------------------------| --------------------------------------------------------------------------------------------------------------- |
| EFORM_ADD_FORM_TEMPLATE_ASYNC_01	                              | GUI / WS                                                                                                        |
| EFORM_CHANGE_FORM_TEMPLATE_MEDATADATA_ASYNC_01	                | GUI / WS                                                                                                        |
| EFORM_INVALIDATE_FORM_TEMPLATE_ASYNC_01	                        | GUI / WS                                                                                                        |
| EFORM_SUBSCRIPTION_MESSAGE_ASYNC_01	                            | Správa odosielaná na podriadený systém – publish/subsribe.                                                      |
| EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_ASYNC_01	          | GUI / WS                                                                                                        |
| EFORM_ADD_FORM_TEMPLATE_REPLY_ASYNC_01	                        | Odpoveď na EFORM_ADD_FORM_TEMPLATE_ASYNC_01 pri úspešnej registrácii a zistení nedostatkov kategórie „WARNING“. |
| FORM_ADD_FORM_TEMPLATE_REPLY_VALIDATION_REPORT_ASYNC_01	        | Odpoveď na EFORM_ADD_FORM_TEMPLATE_ASYNC_01 pri zistených nedostatkoch vo formulári kategórie „WARNING“.        |
| EFORM_ADD_FORM_TEMPLATE_REPLY_REFUSE_VALIDATION_REPORT_ASYNC_01	| Odpoveď na EFORM_ADD_FORM_TEMPLATE_ASYNC_01 pri zistenej chybe vo formulári kategórie „ERROR“ pri jeho vstupnej validácii a teda odmietnutie registrácie.                                                                                                                                                                        |
| EFORM_CHANGE_FORM_TEMPLATE_METADATA_REPLAY_ASYNC_01	            | Odpoveď na EFORM_CHANGE_FORM_TEMPLATE_MEDATADATA_ASYNC_01                                                       |
| EFORM_INVALIDATE_FORM_TEMPLATE_REPLY_ASYNC_01	                  | Odpoveď na EFORM_INVALIDATE_FORM_TEMPLATE_ASYNC_01                                                              |
| EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_REPLY_ASYNC_01	    | Odpoveď na EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_ASYNC_01                                                |
| EFORM_ADD_ROLE_TO_FORM_TEMPLATE_ASYNC_01	                      | WS                                                                                                              |

Modul eForm prostredníctvom rozhrania UIR modulu G2G má uverejnenú sadu služieb. Tieto sú popísané v ďalších kapitolách. Pre volanie týchto služieb sú v module G2G zaregistrované ich CLASSNAME podľa nasledovnej tabuľky: 

| **CLASSNAME**                                                   | **Poznámka**                                                                                                    |
|-----------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------- |
| EFORM_ADD_FORM_TEMPLATE_ASYNC_01                                |	GUI / WS                                                                                                        |
| EFORM_CHANGE_FORM_TEMPLATE_MEDATADATA_ASYNC_01                  |	GUI / WS                                                                                                        |
| EFORM_INVALIDATE_FORM_TEMPLATE_ASYNC_01                         |	GUI / WS                                                                                                        |
| EFORM_SUBSCRIPTION_MESSAGE_ASYNC_01                             |	Správa odosielaná na podriadený systém – publish/subsribe.                                                      |
| EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_ASYNC_01           |	GUI / WS                                                                                                        |
| EFORM_ADD_FORM_TEMPLATE_REPLY_ASYNC_01	                        | Odpoveď na EFORM_ADD_FORM_TEMPLATE_ASYNC_01 pri úspešnej registrácii a zistení nedostatkov kategórie „WARNING“. |
| FORM_ADD_FORM_TEMPLATE_REPLY_VALIDATION_REPORT_ASYNC_01         |	Odpoveď na EFORM_ADD_FORM_TEMPLATE_ASYNC_01 pri zistených nedostatkoch vo formulári kategórie „WARNING“.        |
| EFORM_ADD_FORM_TEMPLATE_REPLY_REFUSE_VALIDATION_REPORT_ASYNC_01 | Odpoveď na EFORM_ADD_FORM_TEMPLATE_ASYNC_01 pri zistenej chybe vo formulári kategórie „ERROR“ pri jeho vstupnej validácii a teda odmietnutie registrácie.                                                                                                                                                                        |
| EFORM_CHANGE_FORM_TEMPLATE_METADATA_REPLAY_ASYNC_01             |	Odpoveď na EFORM_CHANGE_FORM_TEMPLATE_MEDATADATA_ASYNC_01                                                       |
| EFORM_INVALIDATE_FORM_TEMPLATE_REPLY_ASYNC_01	                  | Odpoveď na EFORM_INVALIDATE_FORM_TEMPLATE_ASYNC_01                                                              |
| EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_REPLY_ASYNC_01     |	Odpoveď na EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_ASYNC_01                                                |
| EFORM_ADD_ROLE_TO_FORM_TEMPLATE_ASYNC_01                        |	WS                                                                                                              |

Modul eForm prostredníctvom modulu G2G má vo verzii 2.0 uverejnenú sadu služieb určenú pre asynchrónne spracovanie. Tieto služby implementujú rozhranie SKTalk vo verzii 3.0. Jedná sa o služby určené na :
-	vloženie žiadosti na nový vzor eFormulára,
-	vloženie žiadosti na zmenu metadata vzoru eFormulára,
-	vloženie žiadosti na zneplatnenie vzoru eFormulára,
-	vloženie žiadosti na zmenu súvisiacich dokumentov vzoru eFormulára,
-	zápis pravidiel pre prístupy k vzorom eFormulárom.

| **Názov metódy**                                        | **Popis**                                                                                                          |
|---------------------------------------------------------|------------------------------------------------------------------------------------------------------------------- |
|EFORM_ADD_FORM_TEMPLATE_ASYNC_01	                        | Uloženie žiadosti na vloženie vzoru eFormulára.                                                                    |
| EFORM_CHANGE_FORM_TEMPLATE_MEDATADATA_ASYNC_01          |	Uloženie žiadosti na zmenu metadata vzoru eFormulára.                                                              |
| EFORM_INVALIDATE_FORM_TEMPLATE_ASYNC_01                 |	Uloženie žiadosti na zneplatnenie vzoru eFormulára.                                                                |
| EFORM_SUBSCRIPTION_MESSAGE_ASYNC_01                     |	Túto classname implementuje podriadený modul, ktorý potrebuje dostávať informácie o zmenách vzorov v module eFLCM. |
| EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_ASYNC_01   |	Uloženie žiadosti na zmenu súvisiacich dokumentov vzoru.                                                           |
| EFORM_ADD_ROLE_TO_FORM_TEMPLATE_ASYNC_01                |	Zápis pravidiel pre prístupy k vzorom eFormulárom - pridanie.                                                      |
| EFORM_REMOVE_ROLE_TO_FORM_TEMPLATE_ASYNC_01             |	Zápis pravidiel pre prístupy k vzorom eFormulárom - odobratie.                                                     |

Modul eForm poskytuje nasledovnú sadu služieb registrovaných na G2G asynchrónnom rozhraní, určených pre manipuláciu so vzorom ktorý je vo formáte balíka podľa aktuálne platnej Vyhlášky č. 78/2020 Z. z. o štandardoch pre IT VS: 

-	vloženie vzoru eFormulára v štandardnom balíku ZIP a XML,
-	zmenu metadát vzoru eFormulára na základe súboru meta.xml.

| **Názov metódy**                                                | **Popis**                                                                                                                                 |
|-----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------ |
| EFORM_CHANGE_NOTIFY_TEMPLATE_METADATA_ASYNC_01                  |	Žiadosť na vloženie zmeny metadát vzoru eFormulára typu notifikačná šablóna. Tj meta.xml.                                                 |
| EFORM_CHANGE_FORM_TEMPLATE_METADATA_ASYNC_02                    | Žiadosť na vloženie zmeny metadát vzoru eFormulára typu eFormulár. Tj meta.xml.                                                           |
| EFORM_ADD_FORM_TEMPLATE_ASYNC_02                                | Žiadosť na vloženie vzoru eformulára v štandardnom formáte ZIP/ XML podľa prílohy č. 1 Vyhlášky č. 78/2020 Z. z. o štandardoch pre IT VS. |
| EFORM_ADD_FORM_TEMPLATE_REPLY_ASYNC_02                          |	Odpoveď na: EFORM_ADD_FORM_TEMPLATE_ASYNC_02 pri úspešnej registrácii pri zistení nedostatkov typu „WARNING“.                             |
| EFORM_ADD_FORM_TEMPLATE_REPLY_VALIDATION_REPORT_ASYNC_02	      | Odpoveď na: EFORM_ADD_FORM_TEMPLATE_ASYNC_0 pri zistených nedostatkoch vo formulári kategórie „WARNING“.                                  |
| EFORM_ADD_FORM_TEMPLATE_REPLY_REFUSE_VALIDATION_REPORT_ASYNC_02 |	Odpoveď na: EFORM_ADD_FORM_TEMPLATE_ASYNC_02 pri zistenej chybe vo formulári kategórie ERROR pri jeho vstupnej validácii a teda odmietnutie registrácie.                                                                                                                                                                                                  |
| EFORM_ADD_NOTIFY_TEMPLATE_ASYNC_01                              |	Žiadosť na vloženie vzoru eFormulára typu notifikačná šablóna v štandardnom formáte ZIP / XML podľa prílohy č. 1 Vyhlášky č. 78/2020 Z. z. o štandardoch pre IT VS.                                                                                                                                                                                        |

XML schémy asynchrónnych služieb modulu eForm sú dostupné v kap. 2.1.13 Asynchrónne volané služby eForm – XSD.

Vzory eFormulárov môžu nadobudnúť jeden z nasledujúcich stavov:

- Na schválenie (Po registrácii vzoru do eFormu, pred schválením resp. v schvaľovacom procese.)
- Schválený (Po schválení Výstupnou Kontrolou (VK).)
- Zamietnutý (Ak VK vzor neschváli.)
- Zrušený (Rôzne situácie, napr. ak sú vložené dve verzie vzoru, obidve sú schvalené, ale účinná bude tá vyššia. t.j. počas nadobudnutia účinnosti sa tá staršia nastaví na zrušenú.)
- Zneplatnený (Po uverejnení novšej verzie ako náhle novšia nadobudne účinnosť tak staršia ju stratí.)
- Publikovaný (Každý vzor, ktorý je publikovaný je dostupný cez GUI eFormu, avšak nie každý z nich je aj účinný. Publikovanie je definované v metadátach vzoru.)
- Účinný (Aktuálne platná verzia vzoru zverejnená a dostupná používateľom úložiska eFormulárov. Táto verzia formulára sa zobrazuje všetkým používateľom a v rámci el. služieb je táto verzia použitá ako vstupná údajová štruktúra pri vypĺňaní podaní/rozhodnutí/notifikácií.)

Modul eForm v rámci rozšírenia poskytuje sadu služieb pre:
-	validáciu vzoru eFormulára,
-	vytvorenie vizualizácií z transformačných súborov vzoru eFormulára.

| **CLASSNAME**                                 | **Poznámka**                                                                                                                                             |
|-----------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| EFORM_TRANSFORM_FORM_TEMPLATE_ASYNC_01        | Služba je určená na vytvorenie vizualizácií z prezentačných schém, ktoré sa nachádzajú v balíku vzoru eFormulára vo formáte plok+xml.                    |
| EFORM_TRANSFORM_FORM_TEMPLATE_ASYNC_02        | Služba je určená na vytvorenie vizualizácií z prezentačných schém, ktoré sa nachádzajú v balíku vzoru eFormulára vo formáte .zip.                        |
| EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_01         | Služba je určená na validáciu vzoru eFormulára v balíku vo formáte plok+xml, pred jeho registráciou.                                                     |
| EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_02         | Služba je určená na validáciu vzoru eFormulára v kontajneri vo formáte .zip, pred jeho registráciou.                                                     |
| EFORM_VALIDATE_FORM_TEMPLATE_REPLY_ASYNC_01   | Odpoveď na: EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_01.                                                                                                       |
| EFORM_VALIDATE_FORM_TEMPLATE_REPLY_ASYNC_02   | Odpoveď na: EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_02.                                                                                                       |
| EFORM_TRANSFORM_FORM_TEMPLATE_REPLY_ASYNC_01  | Odpoveď na: EFORM_TRANSFORM_FORM_TEMPLATE_ASYNC_01.                                                                                                      |
| EFORM_TRANSFORM_FORM_TEMPLATE_REPLY_ASYNC_02  | Odpoveď na: EFORM_TRANSFORM_FORM_TEMPLATE_ASYNC_02.                                                                                                      |

> [!NOTE]
> všetky príklady volaní a odpovedí uvedené v tejto kapitole majú ilustračnú povahu, zároveň platí, že dostupné odpovedajúce správy/ odpovede nemusia mať súvis s príkladovými volaniami.

### 2.1.1 EFORM_ADD_FORM_TEMPLATE_ASYNC_01

Služba umožňuje zaslať žiadosť o registráciu a zverejnenie elektronického formulára v module elektronických formulárov. Služba podporuje iba elektronické formuláre vo formáte pkg.xml, resp. registráciu jednotlivých súčastí elektronického formulára s uvedením ich typu.
V tabuľke je pre metódu uvedený popis vstupných a výstupných elementov. Tieto sa pri volaní služby serializujú a ukladajú v rámci SKTalk/Body časti. Popis schém daných typov je uvedení v ďalších kapitolách.

#### 2.1.1.1	Popis správy (Vstupná):

| **Sk-Talk Class:**                        | EFORM_ADD_FORM_TEMPLATE_ASYNC_01                                                 |
| ------------------------------------------| -------------------------------------------------------------------------------- |
| Popis                                     | Žiadosť o registráciu a zverejnenie elektronického formulára vo formáte pkg.xml  |
| Gestor                                    | NASES                                                                            |
| Typ správy                                | Technická                                                                        |
| Odosielateľ                               | Inštitúcia - OVM                                                                 |
| Adresát                                   | UPVS – eFORM (MIRRI / ÚPVS)                                                      |
| Postup spracovania                        | Príjem a spracovanie žiadosti v module eForm                                     |
| Správa prenášaná v rámci štruktúry        | SKTALK 3.0 / InsertNewFormTemplate_Request                                       |
| Identifikátor elektronického formulára    | http://schemas.gov.sk/eflcm/InsertNewFormTemplate/1.0                            |
| Elektronický podpis objektu v class=FORM  | Nie                                                                              |
| Modul/Rozhranie/Služba                    | eFORM / UIR / ServiceSkTalk3Token.svc                                            |
| Modul sprostredkujúci komunikáciu         | UPVS – G2G                                                                       |
| Nadväzná správa 1 (odpoveď/notifikácia)   | EFORM_ADD_FORM_TEMPLATE_REPLY_ASYNC_01                                           |
|                                           | Alternatívne:                                                                    |
|                                           | - EFORM_ADD_FORM_TEMPLATE_REPLY_VALIDATION_REPORT_ASYNC_01                       |
|                                           | - EFORM_ADD_FORM_TEMPLATE_REPLY_REFUSE_VALIDATION_REPORT_ASYNC_01                |
| Poznámka                                  |                                                                                  |

#### 2.1.1.2  Vstupný technický formulár

- **Classname:** EFORM_ADD_FORM_TEMPLATE_ASYNC_01
- **Input object:** InsertNewFormTemplate_Request

| **Názov**          | **Typ**                              | **Povinnosť**                                    | **Popis**                        |
| ------------------ | ------------------------------------ | ------------------------------------------------ | -------------------------------- |
| Request            | EFLCMRequest                         | Áno                                              | Žiadosť vzoru eFormulára         |
| FormTemplate       | FormTemplate                         | Áno                                              | Vzor EFormulára                  |


Popis štruktúr použitých vo webovej službe:

**Názov štruktúry:** EFLCMRequest

| **Meno**                          | **Typ**                           | **Povinnosť**                     | **Popis**                         |
| --------------------------------- | --------------------------------- | --------------------------------- | --------------------------------- |
| Title                             | String                            | Áno                               | Názov žiadosti                    |
| Description                       | String                            | Áno                               | Popis žiadosti                    |
| Publisher                         | String                            | Áno                               | Inštitúcia ktorá žiadosť podala - subjectID – UPVS URI poskytovateľa v IAM |
| Gestor                            | String                            | Áno                               | Gestor elektronického formulára (v GUI MEF sa obvykle uvádza subjectID – UPVS URI gestora v IAM). |

**Názov štruktúry:** FormTemplate

| **Meno**                          | **Typ**                           | **Povinnosť**                     | **Popis**                         |
| --------------------------------- | --------------------------------- | --------------------------------- | --------------------------------- |
| MetaData                          | FormTemplateMetaData              | Áno                               | Metadata                          |
| RelatedDocuments                  | RelatedDocument[]                 | Áno                               | Súvisiace dokumenty – obsahuje súčastí elektronického formulára (súvisiace dokumenty) definujúce vzor eFormulára v rámci technológie, v ktorej bol vytvorený (ÚPVS alebo iné). |
| Data                              | Byte[]                            |                                   | Nepoužívané – pôvodne používané pre uloženie prázdneho vzoru eFormulára. Poznámka: Parameter platný do verzie eForm 1.5. Kvôli spätnej kompatibilite je zahrnutý v schéme |

**Názov štruktúry:** FormTemplateMetaData

| **Meno**                                  | **Typ**                           | **Povinnosť**                     | **Popis**                         |
| ----------------------------------------- | --------------------------------- | --------------------------------- | --------------------------------- | 
| Identifier                                | String                            | Áno                               | Identifikátor vzoru eFormulára    |
| Title                                     | String                            | Áno                               | Názov vzoru                       |
| Type                                      | FormTemplateType                  | Áno                               | Typ vzoru                         |
| Description                               | String                            | Áno                               | Popis vzoru                       |
| Gestor                                    | String                            | Áno                               | Gestor elektronického formulára (v GUI MEF sa obvykle uvádza subjectID – UPVS URI gestora v IAM) |
| Publisher                                 | String                            | Áno                               | Inštitúcia ktorá žiadosť podala - subjectID – UPVS URI poskytovateľa v IAM) |
| Section                                   | String                            |                                   | Sekcia                            |
| Agenda                                    | String                            |                                   | Agenda                            |
| Source                                    | String                            |                                   | Pôvod vzoru                       |
| Version                                   | EFormVersion                      | Áno                               | Verzia vzoru - Väčšia zmena (schéma) = Major, Menšia zmena (visual, labels) = Minor |
| ValidDateFrom                             | DateTime                          | Áno                               | Začiatok platnosti vzoru          |
| ValidDateTo                               | DateTime                          |                                   | Koniec platnosti vzoru            |
| Keywords                                  | String                            |                                   | Kľúčové slová                     |
| AccessGroup                               | String                            |                                   | Prístupová skupina - toto pole sa aktuálne nevypĺňa (uvedené z historických dôvodov). Pre formuláre, ktoré majú uvedenú skupinu prístupu je táto hodnota pri vyhodnocovaní prístupu k formulárom ignorovaná a teda všetky formuláre sú prístupné. |

**Názov štruktúry:** EFormVersion

| **Meno**                                  | **Typ**                           | **Povinnosť**                     | **Popis**                         | 
| ----------------------------------------- | --------------------------------- | --------------------------------- | --------------------------------- |
| Major                                     | Int                               | Áno                               | Verzia vzoru                      |
|Minor                                      | Int                               | Áno                               | Podverzia vzoru                   |

FormTemplateType: string
- eForm
- teForm
- POSP
- NOTIFY

**Názov štruktúry:** RelatedDocument

| **Meno**                                  | **Typ**                           | **Povinnosť**                     | **Popis**                                           | 
| ----------------------------------------- | --------------------------------- | --------------------------------- | --------------------------------------------------- |
| MetaData                                  | RelatedDocumentMetaData           | Áno                               | Štruktúra popisujúca metadáta súvisiaceho dokumentu |
| Data                                      | Byte[]                            | Áno                               | Base64binary dáta súvisiaceho dokumentu v štruktúre a formáte súvisiaceho dokumentu definovanej jeho typom vytvoreného v použitej formulárovej technológii, napr. eFormDesigner.                                                                                          |

> [!NOTE]
> Modul eForm predstavuje úložisko el. Formulárov pre celý eGovernment a podporuje uloženie rôznych typov formulárov, uložených v zákonom definovanej forme (balík), vytvorených buď technológiou ÚPVS, prípadne inou technológiou, ktorú používa ISVS.

**Názov štruktúry:** RelatedDocument

| **Meno**              | **Typ**                           | **Povinnosť**       | **Popis**                                                              |
| --------------------- | --------------------------------- | ------------------- | ---------------------------------------------------------------------- |
| Type                  | String                            | Áno                 | Typ súvisiaceho dokumentu (typ súčasti formulára)                      |
|                       |                                   |                     | Možné hodnoty:                                                         |
|                       |                                   |                     | CLS_F_XSLT_DEFAULT                                                     |
|                       |                                   |                     | CLS_F_XSLT_TXT_SGN                                                     |
|                       |                                   |                     | CLS_F_XSLT_TXT_EMAIL_BODY                                              |
|                       |                                   |                     | CLS_F_XSLT_TXT_EMAIL_SUBJECT                                           |
|                       |                                   |                     | CLS_F_XSLT_HTML_EMAIL_BODY                                             |
|                       |                                   |                     | CLS_F_XSLT_HTML_EMAIL_SUBJECT                                          |
|                       |                                   |                     | CLS_F_XSLT_TXT_SMS                                                     |
|                       |                                   |                     | CLS_F_HTML_FORM                                                        |
|                       |                                   |                     | CLS_F_XML_NAT                                                          |
|                       |                                   |                     | CLS_F_XSD_NAT                                                          |
|                       |                                   |                     | CLS_F_XSD_EDOC                                                         |
|                       |                                   |                     | CLS_F_XML_EDOC                                                         |
|                       |                                   |                     | CLS_F_XML_DCT                                                          |
|                       |                                   |                     | CLS_F_XSL_FO                                                           |
|                       |                                   |                     | CLS_F_XSLT_RO                                                          |
|                       |                                   |                     | CLS_F_DLL_VAL                                                          |
|                       |                                   |                     | CLS_F_XML_MTD                                                          |
|                       |                                   |                     | CLS_F_XSLT_NAT_EDOC                                                    |
|                       |                                   |                     | CLS_F_XSLT_EDOC_NAT                                                    |
|                       |                                   |                     | CLS_F_XSLT_HTML                                                        |
|                       |                                   |                     | BalikXML                                                               |
|                       |                                   |                     | CLS_F_XML_DEF                                                          |
|                       |                                   |                     | CLS_POSP                                                               |
|                       |                                   |                     | POSP_priloha, (táto hodnota sa už nesmie používať v nových formulároch)|
|                       |                                   |                     | POSP, (táto hodnota sa už nesmie používať v nových formulároch)        |
|                       |                                   |                     | EFORM_STANDARD_ZIP_PACKAGE                                             |
| Identifier            | String                            | Áno                 | Identifikátor vzoru - Názov súboru súvisiaceho dokumentu               |
| Description           | String                            |                     | Popis súvisiaceho dokumentu                                            |
| Language              | String                            | Áno                 | Jazyk súvisiaceho dokumentu                                            |

#### 2.1.1.3	Popis správy (Výstupná):

Na výstupe sa môžu vrátiť tri rôzne Sk-Talk Class:

Odpoveď na žiadosť o registráciu formulára sa vracia len v prípade úspešnej registrácie alebo chyby, ktorá nebola zistená v rámci vstupných validácií. Nevracia sa v prípade zistenej chyby pri validácii (kategórie ERROR), ktorá má za následok nezaregistrovanie formulára.

| **Sk-Talk Class**                         | EFORM_ADD_FORM_TEMPLATE_REPLY_ASYNC_01                                            |
| ------------------------------------------| ----------------------------------------------------------------------------------|
| Popis                                     | Odpoveď na žiadosť o registráciu vzoru                                            |
| Gestor                                    | NASES                                                                             |
| Typ správy                                | Technická                                                                         |
| Odosielateľ                               | UPVS – eFORM (MIRRI / ÚPVS)                                                       |
| Adresát                                   | Inštitúcia - OVM                                                                  |
| Postup spracovania                        | NA                                                                                |
| Správa prenášaná v rámci štruktúry        | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“                              |
| Identifikátor elektronického formulára    | Špecifické štruktúry, ktoré nie sú elektronickým formulárom: http://schemas.gov.sk/eflcm/InsertNewFormTemplate/1.0 alebo http://schemas.gov.sk/eflcm/eFLCMExceptionMessage/1.0                                                                                                       |
| Elektronický podpis objektu v class=FORM  | Nie                                                                               |
| Modul/Rozhranie/Služba                    | eFORM / UIR / ServiceSkTalk3Token.svc                                             |
| Modul sprostredkujúci komunikáciu         | UPVS – G2G                                                                        |
| Nadväzná správa 1 (odpoveď/notifikácia)   | NA                                                                                |
| Poznámka                                  |                                                                                   |

Odpoveď na žiadosť o registráciu vzoru – registrácia formulára pokračuje úspešne ďalej, je zaslaný **výsledok validácie formulára so zistenými upozorneniami pri validácii formulára** („WARNING“ v nastavení validácií), ktoré je žiadúce opraviť ale neblokujú registráciu formulára.

| **Sk-Talk Class**                         | EFORM_ADD_FORM_TEMPLATE_REPLY_VALIDATION_REPORT_ASYNC_01                          |
| ------------------------------------------| ----------------------------------------------------------------------------------|
| Popis                                     | Odpoveď na žiadosť o registráciu vzoru - registrácia formulára pokračuje úspešne ďalej, je zaslaný výsledok validácie formulára. so zistenými upozorneniami pri validácii formulára („WARNING“ v nastavení validácií), ktoré je žiadúce opraviť ale neblokujú registráciu formulára.            |
| Gestor                                    | NASES                                                                             |
| Typ správy                                | Technická                                                                         |
| Predmet správy                            | Validačný report                                                                  |
| Odosielateľ                               | UPVS – eFORM (MIRRI / ÚPVS)                                                       |
| Adresát                                   | Inštitúcia - OVM                                                                  | 
| Postup spracovania                        | Je potrebné opraviť elektronický formulár v ďalšej verzii formulára. Registrácia aktuálneho formulára prebieha ďalej. |
| Správa prenášaná v rámci štruktúry        | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“                              |
| Identifikátor elektronického formulára    | http://schemas.gov.sk/form/MEF.Preprocessor.ValidationReport.sk/1.1               |
| Elektronický podpis objektu v class=FORM  | Nie                                                                               |
| Modul/Rozhranie/Služba                    | eFORM/UIR/ServiceSkTalk3Token.svc                                                 |
| Modul sprostredkujúci komunikáciu         | UPVS - G2G                                                                        |
| Nadväzná správa 1 (odpoveď/notifikácia)   | NA                                                                                |
| Poznámka                                  |                                                                                   |

Odpoveď na žiadosť o registráciu vzoru - **spracovanie registrácie formulára ukončené chybou zistenou pri validácii formulára** („ERROR“ v nastavení validácií)

| **Sk-Talk Class**                         | EFORM_ADD_FORM_TEMPLATE_REPLY_REFUSE_VALIDATION_REPORT_ASYNC_01                   |
| ------------------------------------------| ----------------------------------------------------------------------------------|
| Popis                                     | Odpoveď na žiadosť o registráciu vzoru - spracovanie registrácie formulára ukončené chybou zistenou pri validácii formulára („ERROR“ v nastavení validácií) a formulár **nie je v MEF zaregistrovaný.**                                                                                                |
| Gestor                                    | NASES                                                                             |
| Typ správy                                | Technická                                                                         |
| Predmet správy                            | Validačný report                                                                  |
| Odosielateľ                               | UPVS – eFORM (MIRRI / ÚPVS)                                                       |
| Adresát                                   | Inštitúcia - OVM                                                                  | 
| Postup spracovania                        | Je potrebné opraviť elektronický formulár a registráciu vykonať následne opätovne.|
| Správa prenášaná v rámci štruktúry        | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“                              |
| Identifikátor elektronického formulára    | http://schemas.gov.sk/form/MEF.Preprocessor.ValidationReport.sk/1.1               |
| Elektronický podpis objektu v class=FORM  | Nie                                                                               |
| Modul/Rozhranie/Služba                    | eFORM/UIR/ServiceSkTalk3Token.svc                                                 |
| Modul sprostredkujúci komunikáciu         | UPVS - G2G                                                                        |
| Nadväzná správa 1 (odpoveď/notifikácia)   | NA                                                                                |
| Poznámka                                  |                                                                                   |

#### 2.1.1.4	Výstupný technický formulár - Odpoveď

- **CLASSNAME:** EFORM_ADD_FORM_TEMPLATE_ASYNC_01
- **Output object:** 
                                            
| **Názov**                                             | **Popis**                                                                                     | 
| ----------------------------------------------------- | --------------------------------------------------------------------------------------------- |                                             
| http://schemas.gov.sk/form/G2G.InformationMessage/1.3	| Vid. IM – G2G – trieda INFORMATION                                                            |                                                         
| http://schemas.gov.sk/eflcm/eFLCMExceptionMessage/1.0 | (špecifická štruktúra, ktorá nie je elektronickým formulárom)	Popis viď nižšie.               |                                     
| http://schemas.gov.sk/eflcm/InsertNewFormTemplate/1.0 | (špecifická štruktúra, ktorá nie je elektronickým formulárom)	Popis viď nižšie kap. 2.1.12.2. | 

- **CLASSNAME:** EFORM_ADD_FORM_TEMPLATE_REPLY_REFUSE_VALIDATION_REPORT_ASYNC_01
- **Názov štruktúry:** MEF.Preprocessor.ValidationReport.sk/1.1 - ValidationReportData

| **Meno**                                    | **Typ**               | **Povinnosť**      | **Popis**                      |
| ------------------------------------------- | --------------------  | ------------------ | ------------------------------ | 
| FormName	                                  | string	              | Nie   	           | Názov formulára                |
| FormVersion	                                | string	              | Nie	               | Verzia                         |
| FormPurposeDescription	                    | string	              | Nie	               | Popis                          |
| Language	                                  | string	              | Nie	               | Jazyk                          |
| FormProvider	                              | string	              | Nie	               | Poskytovateľ                   |
| ElectronicServiceCoordinator                | string	              | Nie	               | Zodpovedná osoba               |
| FormId	                                    | string	              | Nie	               | Identifikátor                  |
| FormShortId	                                | string	              | Nie	               | Skrátený Identifikátor         |
| ValidDateFrom	                              | dateTime	            | Nie	               | Platný od                      |
| ValidDateTo	                                | dateTime	            | Nie	               | Platný do                      |
| ApplyDateFrom	                              | dateTime	            | Nie	               | Účinný od                      |
| ApplyDateTo	                                | dateTime 	            | Nie	               | Účinný do                      |
| ValidationDateTime	                        | dateTime	            | Nie	               | Dátum validácie                |
| FileName	                                  | string	              | Nie	               | Názov súboru                   |
| FormSpecificationVersion	                  | string	              | Nie	               | Verzia špecifikácie formulára  |
| ValidationResult	                          | string	              | Nie	               | Výsledok validácie             |
| ErrorCount	                                | integer	              | Nie	               | Počet chýb                     |
| WarningCount	                              | integer	              | Nie	               | Počet výstrah                  |
| RuleOutput	                                | < ValidationOutput >	| Nie	               | -                              |
 
**Názov štruktúry:** MEF.Preprocessor.ValidationReport.sk/1.1 - ValidationOutput

| **Meno**                     | **Typ**                              | **Povinnosť**      | **Popis**                       |
| ---------------------------- | ------------------------------------ | ------------------- | ------------------------------ |
| Severity                     | Enum: < ValidationInformationType >  |  Nie                | - ERROR                        |
|                              |                                      |                     | - WARNING                      |
|                              |                                      |                     | - INFO                         |
|                              |                                      |                     | - INTERNALERROR                |
| ErrorCode                    | String                               | Nie                 | Kód chyby                      |
| ApplyDateFrom                | String                               | Nie                 | Dátum aplikácie                |
| PlaceOfError                 | String                               | Nie                 | Miesto chyby                   |
| OutputText                   | String                               | Nie                 | Výstupný text                  |
| RecomendedText               | String                               | Nie                 | Odporúčaný text                |
| TechnicalMessage             | String                               | Nie                 | Technická správa               |

- [XML schéma MEF.Preprocessor.ValidationReport.sk](https://github.com/NASES-Slovakia/integration_manuals/blob/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_ADD_FORM_TEMPLATE_ASYNC_01/MEF.Preprocessor.ValidationReport.sk__schema.xsd)

**Názov štruktúry:** eFLCMExceptionMessage

| **Meno**                    | **Typ**                   | **Povinnosť**       | **Popis**      |
| --------------------------- | ------------------------- | ------------------- | -------------- |
| ErrorCode                   | String                    | Nie                 | Kód chyby      |
| ErrorDescription            | String                    | Nie                 | Popis chyby    |

- [XML schéma eFLCMExceptionMessage](https://github.com/NASES-Slovakia/integration_manuals/blob/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_ADD_FORM_TEMPLATE_ASYNC_01/eFLCMExceptionMessage__schema.xsd)

#### 2.1.1.5	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6 - Chybové hlášky
<!-- Potom prelinkovať na predmetnú kapitolu -->

**Chybové stavy**
- 06000997
-	06000998
-	06000999
-	06000799
-	06000797
-	06000795
-	06000794

#### 2.1.1.6	Príklady volaní a odpovedí služby – SKTalk 

- [Príklady SKTalk](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_ADD_FORM_TEMPLATE_ASYNC_01)

### 2.1.2	EFORM_CHANGE_FORM_TEMPLATE_MEDATADATA_ASYNC_01

Správa popisuje žiadosť na zmenu metadát existujúceho vzoru eFormulára. V tabuľke je pre metódu uvedený popis vstupných a výstupných elementov. Tieto sa pri volaní služby serializujú a ukladajú v rámci SKTalk/Body časti. Popis schém daných typov je uvedení v ďalších kapitolách.

> [!WARNING]
> Názov elektronického formulára sa nesmie meniť vzhľadom na používanie názvu formulára v podpisoch v historických formátoch XAdES_ZEP. Zmenou názvu by sa takéto podpisy mohli overovať ako neplatné.

#### 2.1.2.1	Popis správy (Vstupná):

| **Sk-Talk Class**				                      | EFORM_CHANGE_FORM_TEMPLATE_METADATA_ASYNC_01                |
| --------------------------------------------- | ----------------------------------------------------------- |
| Popis					                                | Žiadosť o zmenu metadát existujúceho vzoru.                 |
| Gestor			                                  | NASES                                                       |
| Typ správy                                    | Technická                                                   |
| Odosielateľ                                   | Inštitúcia - OVM                                            |
| Adresát                                       | UPVS – eFORM (MIRRI / ÚPVS)                                 |
| Postup spracovania                            | Príjem a spracovanie žiadosti v module eForm.               |
| Správa prenášaná v rámci štruktúry            | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“        |
| Identifikátor elektronického formulára        | http://schemas.gov.sk/eflcm/ChangeFormTemplateMetaData/1.0  |
| Elektronický podpis objektu v class=FORM      | Nie                                                         |
| Modul/Rozhranie/Služba                        | eFORM / UIR / ServiceSkTalk3Token.svc                       |
| Modul sprostredkujúci komunikáciu             | UPVS – G2G                                                  |
| Nadväzná správa 1 (odpoveď/notifikácia)       | EFORM_CHANGE_FORM_TEMPLATE_METADATA_REPLY_ASYNC_01          |
| Poznámka                                      |                                                             |

#### 2.1.2.2	Vstupný technický formulár

- **CLASSNAME:** EFORM_CHANGE_FORM_TEMPLATE_METADATA_ASYNC_01
- **Input Object:** ChangeFormTemplateMetaData_Request

| **Meno**                  | **Typ**                                          | **Povinnosť**    | **Popis**                        |
| ------------------------- | ------------------------------------------------ | ---------------- | -------------------------------- |
| Request                   | EFLCMRequest                                     | Áno              | Žiadosť vzoru eFormulára         |
| MetaData                  | FormTemplateMetaData                             | Áno              | MetaData vzoru eFormulára        |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** EFLCMRequest

| **Meno**                    | **Typ**                   | **Povinnosť**  | **Popis**                                                                                         |
| --------------------------- | ------------------------- | -------------- | ------------------------------------------------------------------------------------------------- |
| Title                       | String                    | Áno            | Názov žiadosti                                                                                    |
| Description                 | String                    | Áno            | Popis žiadosti                                                                                    |
| Publisher                   | String                    | Áno            | Inštitúcia ktorá žiadosť podala - subjectID – UPVS URI poskytovateľa v IAM.                       |
| Gestor                      | String                    | Áno            | Gestor elektronického formulára (v GUI MEF sa obvykle uvádza subjectID – UPVS URI gestora v IAM). |

**Názov štruktúry:** FormTemplateMetaData

| **Meno**                    | **Typ**                   | **Povinnosť**  | **Popis**                                                                              |
| --------------------------- | ------------------------- | -------------- | -------------------------------------------------------------------------------------- |
| Identifier                  | String                    | Áno            | Identifikátor vzoru formulára                                                          |
| Title                       | String                    | Áno            | Názov vzoru                                                                            |
| Type                        | FormTemplateType          | Áno            | Typ vzoru                                                                              |
| Description                 | String                    | Áno            | Popis vzoru                                                                            |
| Gestor                      | String                    | Áno            | Gestor                                                                                 |
| Publisher                   | String                    | Áno            | Inštitúcia                                                                             |
| Section                     | String                    |                | Sekcia                                                                                 |
| Agenda                      | String                    |                | Agenda                                                                                 |
| Source                      | String                    |                | Pôvod vzoru                                                                            |
| Version                     | EFormVersion              |                | Verzia vzoru                                                                           |
| ValidDateFrom               | DateTime                  | Áno            | Začiatok platnosti vzoru                                                               |
| ValidDateTo                 | DateTime                  | Áno            | Koniec platnosti vzoru                                                                 |
| Keywords                    | String                    |                | Kľúčové slová                                                                          |
| AccessGroup                 | String                    |                | Prístupová skupina - toto pole sa aktuálne nevypĺňa (uvedené z historických dôvodov). Pre formuláre, ktoré majú uvedenú skupinu prístupu je táto hodnota pri vyhodnocovaní prístupu k formulárom ignorovaná a teda všetky formuláre sú prístupné.                                                            |

**Názov štruktúry:** EFormVersion

| **Meno**             | **Typ**           | **Povinnosť**  | **Popis**          |
| -------------------- | ----------------- | -------------- | ------------------ |
| Major                | Int               | Áno            | Verzia vzoru       |
| Minor                | Int               | Áno            | Podverzia vzoru    |

FormTemplateType: string
- eForm
- teForm
- POSP
- Notify

#### 2.1.2.3	Popis správy (Výstupná):

| **Sk-Talk Class**				                      | EFORM_CHANGE_FORM_TEMPLATE_METADATA_REPLY_ASYNC_01     |
| --------------------------------------------- | ------------------------------------------------------ |
| Popis					                                | Odpoveď na žiadosť o zmenu metadát existujúceho vzoru. |
| Gestor			                                  | NASES                                                  |
| Typ správy                                    | Technická                                              |
| Odosielateľ                                   | UPVS – eFORM (MIRRI / ÚPVS)                            |
| Adresát                                       | Inštitúcia - OVM                                       |
| Postup spracovania                            | NA                                                     |
| Správa prenášaná v rámci štruktúry            | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“   |
| Identifikátor elektronického formulára        | http://schemas.gov.sk/form/G2G.InformationMessage/1.3  |
| Elektronický podpis objektu v class=FORM      | Nie                                                    |
| Modul/Rozhranie/Služba                        | eFORM / UIR / ServiceSkTalk3Token.svc                  |
| Modul sprostredkujúci komunikáciu             | UPVS – G2G                                             |
| Nadväzná správa 1 (odpoveď/notifikácia)       | NA                                                     |
| Poznámka                                      |                                                        |

#### 2.1.2.4	Výstupný technický formulár - Odpoveď
                                           
| **Názov**                                             | **Popis**       |   
| ----------------------------------------------------- | --------------- |
| http://schemas.gov.sk/form/G2G.InformationMessage/1.3 | Viď. IM G2G     |
| http://schemas.gov.sk/eflcm/eFLCMExceptionMessage/1.0 | Viď. vyššie     |

#### 2.1.2.5	Chybové kódy služby

 nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6 - Chybové hlášky
<!-- Potom prelinkovať na predmetnú kapitolu -->

**Chybové stavy**
-	06000997
-	06000998
-	06000999
-	06000797
-	06000794

#### 2.1.2.6  Príklady volaní a odpovedí služby – SKTalk

- [Príklady SKTalk](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_CHANGE_FORM_TEMPLATE_MEDATADATA_ASYNC_01)

### 2.1.3	EFORM_INVALIDATE_FORM_TEMPLATE_ASYNC_01

Služba umožňuje zaslať žiadosť o zrušenie účinnosti elektronického formulára v module elektronických formulárov. Pojem „účinnosť“ používaný pre dátum začiatku a konca účinnosti formulára bol v rámci novely Vyhlášky č. 78/2020 Z. z. v roku 2022 zmenený na „platnosť“. Pôvodný pojem „platnosť“ používaný pre dátum zverejnenia elektronického formulára v eFORM/MEF bol v rámci rovnakej novely zmenený na „dostupnosť“. V rámci tohto integračného manuálu sa však zatiaľ používajú pojmy v pôvodnom význame podľa pôvodne platnej legislatívy.
V tabuľke je pre metódu uvedený popis vstupných a výstupných elementov. Tieto sa pri volaní služby serializujú a ukladajú v rámci SKTalk/Body časti. Popis schém daných typov je uvedení v ďalších kapitolách.

#### 2.1.3.1	Popis správy (Vstupná):

| **Sk-Talk Class**				                      | EFORM_INVALIDATE_FORM_TEMPLATE_ASYNC_01                   |
| --------------------------------------------- | --------------------------------------------------------- |
| Popis					                                | Žiadosť o zrušenie účinnosti vzoru.                       |
| Gestor			                                  | NASES                                                     |
| Typ správy                                    | Technická                                                 |
| Odosielateľ                                   | Inštitúcia - OVM                                          |
| Adresát                                       | UPVS – eFORM (MIRRI / ÚPVS)                               |
| Postup spracovania                            | Príjem a spracovanie žiadosti v module eForm.             |
| Správa prenášaná v rámci štruktúry            | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“      |
| Identifikátor elektronického formulára        | http://schemas.gov.sk/eflcm/InvalidateFormTemplate/1.0    |
| Elektronický podpis objektu v class=FORM      | Nie                                                       |
| Modul/Rozhranie/Služba                        | eFORM / UIR / ServiceSkTalk3Token.svc                     |
| Modul sprostredkujúci komunikáciu             | UPVS – G2G                                                |
| Nadväzná správa 1 (odpoveď/notifikácia)       | EFORM_INVALIDATE_FORM_TEMPLATE_REPLY_ASYNC_01             |
| Poznámka                                      |                                                           |

#### 2.1.3.2	Vstupný technický formulár

- **Classname:** EFORM_INVALIDATE_FORM_TEMPLATE_ASYNC_01
- **Input object:** InvalidateFormTemplate_Request

| **Názov**                         | **Typ**                                     | **Povinnosť**        | **Popis**                        | 
| --------------------------------- | ------------------------------------------- | -------------------- | -------------------------------- | 
| Request                           | EFLCMRequest                                | Áno                  | Žiadosť vzoru eFormulára         |                 
| FormTemplate                      | FormTemplateID                              | Áno                  | ID Vzoru eFormulára              |

Popis štruktúr použitých vo webovej službe:

**Názov štruktúry:** EFLCMRequest

| **Meno**                          | **Typ**                      | **Povinnosť**        | **Popis**                                                                                         | 
| --------------------------------- | ---------------------------- | -------------------- | ------------------------------------------------------------------------------------------------- |
| Title                             | String                       | Áno                  | Názov žiadosti                                                                                    |
| Description                       | String                       | Áno                  | Popis žiadosti                                                                                    |
| Publisher                         | String                       | Áno                  | Inštitúcia ktorá žiadosť podala - subjectID – UPVS URI poskytovateľa v IAM.                       |
| Gestor                            | String                       | Áno                  | Gestor elektronického formulára (v GUI MEF sa obvykle uvádza subjectID – UPVS URI gestora v IAM). |

**Názov štruktúry:** FormTemplateID

| **Meno**                          | **Typ**                      | **Povinnosť**        | **Popis**                             | 
| --------------------------------- | ---------------------------- | -------------------- | ------------------------------------- |
| Identifier                        | String                       | Áno                  | Identifikátor vzoru                   |
| Version                           | eFormVersion                 |                      | Verzia vzoru                          |

**Názov štruktúry:** eFormVersion

| **Meno**                          | **Typ**                    | **Povinnosť**        | **Popis**                             |
| --------------------------------- | -------------------------- | -------------------- | ------------------------------------- |
| Major                             | Int                        | Áno                  | Verzia vzoru                          |
| Minor                             | Int                        | Áno                  | Podverzia vzoru                       |

#### 2.1.3.3	Popis správy (výstupná):

| **Sk-Talk Class**				                      | EFORM_INVALIDATE_FORM_TEMPLATE_REPLY_ASYNC_01            |
| --------------------------------------------- | -------------------------------------------------------- |
| Popis					                                | Odpoveď na žiadosť o zrušenie účinnosti vzoru.           |
| Gestor			                                  | NASES                                                    |
| Typ správy                                    | Technická                                                |
| Odosielateľ                                   | UPVS – eFORM (MIRRI / ÚPVS)                              |
| Adresát                                       | Inštitúcia - OVM                                         |
| Postup spracovania                            | NA                                                       |
| Správa prenášaná v rámci štruktúry            | SKTALK 3.0 / InvalidateFormTemplate_Response             |
| Identifikátor elektronického formulára        | http://schemas.gov.sk/eflcm/InvalidateFormTemplate/1.0   |
| Elektronický podpis objektu v class=FORM      | Nie                                                      |
| Modul/Rozhranie/Služba                        | eFORM / UIR / ServiceSkTalk3Token.svc                    |
| Modul sprostredkujúci komunikáciu             | UPVS – G2G                                               |
| Nadväzná správa 1 (odpoveď/notifikácia)       | NA                                                       |
| Poznámka                                      |                                                          |

#### 2.1.3.4	Výstupný technický formulár - Odpoveď

| **Názov**                                               | **Popis**         |
| ------------------------------------------------------- | ----------------- |
| http://schemas.gov.sk/form/G2G.InformationMessage/1.3   | Viď IM – G2G      |      
| http://schemas.gov.sk/eflcm/eFLCMExceptionMessage/1.0   | Viď vyššie        |
| http://schemas.gov.sk/eflcm/InvalidateFormTemplate/1.0  | Viď nižšie        |

**Názov štruktúry:** sk/1.1 - InvalidateFormTemplate

| **Meno**               | **Typ**                             | **Povinnosť**        | **Popis**                   | 
| ---------------------- | ----------------------------------- | -------------------- | --------------------------- |
| Identifier             | String                              | Nie                  | Identifikátor               |
| Version                | String                              | Nie                  | Verzia vzoru                |
| Major                  | String                              | Nie                  | Verzia hlavná               |
| Minor                  | String                              | Nie                  | Podverzia vzoru             |

#### 2.1.3.5	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy**
-	06000997
-	06000998
-	06000999
-	06000797
-	06000794

#### 2.1.3.6	Príklad volania služby – SKTalk 

- [Príklad SKTalk Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_INVALIDATE_FORM_TEMPLATE_ASYNC_01)

### 2.1.4	  EFORM_SubscriptionMessageASync_01

Pre synchronizáciu s podriadenými modulmi musí podriadený IS,  ktorý požaduje dostávať informácie o zmenách v úložisku eFLCM implementovať službu umožňujúcu spracovanie správy s CLASSNAME=EFORM_SubscriptionMessageASync_01. 

Obsahom tejto správy sú informácie o zmenách v úložisku. Tieto sú uložené vo vstupnom parametri typu eFLCMSubscriptionMessage. Bližší popis služby uvedený v kapitole 5.

V tabuľke je pre metódu uvedený popis vstupných a výstupných elementov. Tieto sa pri volaní služby serializujú a ukladajú v rámci SKTalk/Body časti. Popis schém daných typov je uvedení v ďalších kapitolách.

#### 2.1.4.1	Popis správy (Výstupná):

| **Sk-Talk Class**				                      | EFORM_SUBSCRIPTION_MESSAGE_ASYNC_01                               |
| --------------------------------------------- | ----------------------------------------------------------------- |
| Popis					                                | Notifikácia o zmenách v module eForm.                             |
| Gestor			                                  | NASES                                                             |
| Typ správy                                    | Technická                                                         |
| Odosielateľ                                   | UPVS – eFORM (MIRRI / ÚPVS)                                       |
| Adresát                                       | Inštitúcia - OVM                                                  |
| Postup spracovania                            | Zaslaná notifikácia do eDesku alebo definované URL – rozhranie.   |
| Správa prenášaná v rámci štruktúry            | SKTALK 3.0 / eFLCMSubscriptionMessage                             |
| Identifikátor elektronického formulára        | eFLCMSubscriptionMessage                                          |
| Elektronický podpis objektu v class=FORM      | Nie                                                               |
| Modul/Rozhranie/Služba                        | eFORM / UIR / ServiceSkTalk3Token.svc                             |
| Modul sprostredkujúci komunikáciu             | UPVS – G2G                                                        |
| Nadväzná správa 1 (odpoveď/notifikácia)       | NA                                                                |
| Poznámka                                      | Predpokladá registráciu Subscribera viď. kap. SubscribeForChanges |

- **Classname:** EFORM_SUBSCRIPTION_MESSAGE_ASYNC_01
- **Input object:** eFLCMSubscriptionMessage

| **Názov**                 | **Typ**                                 | **Povinnosť**        | **Popis**                                                    | 
| ------------------------- | --------------------------------------- | -------------------- | ------------------------------------------------------------ | 
| SubscribedGestor          | String                                  | Áno                  | Identifikátor gestora prihláseného k odberu správ.           |
| SubscribedPublisher       | String                                  | Áno                  | Identifikátor inštitúcie prihlásenej k odberu správ.         |
| FormTemplates             | eFormTemplate[]                         |                      | Pole zmien vo publikovaní/zneplatnení vzorov v module EFLCM. |

**Názov štruktúry:** eFormTemplate

| **Meno**                 | **Typ**                | **Povinnosť**   | **Popis**                                           | 
| ------------------------ | ---------------------- | --------------- | --------------------------------------------------- |
| Publisher                | String                 | Áno             | Identifikátor inštitúcie z IAM ktorá vzor vystavila |
| Gestor                   | String                 | Áno             | Identifikátor gestora z IAM ktorý vzor vystavil     |
| Identifier               | String                 | Áno             | Identifikátor vzoru                                 |
| Version                  | eFormTemplateVersion   | Áno             | Verzia vzoru                                        |
| Status                   | eFormTemplateStatus    | Áno             | Stav vzoru                                          |
| Changed                  | DateTime               | Áno             | Dátum zmeny                                         |
| RelatedDocumentChanged   | Boolean                |                 | Indikátor zmeny súvisiaceho .doc.                   |

**Názov štruktúry:** eFormTemplateVersion

| **Meno**                          | **Typ**                    | **Povinnosť**        | **Popis**                             |
| --------------------------------- | -------------------------- | -------------------- | ------------------------------------- |
| Major                             | Int                        | Áno                  | Verzia vzoru                          |
| Minor                             | Int                        | Áno                  | Podverzia vzoru                       |

FormTemplateStatus: string
- PUBLISHED
- INVALIDATED

#### 2.1.4.2	Príklad notifikačnej správy zasielanej modulom eForm pri metóde Subscribe 

```

<SKTalkMessage xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema">
	<EnvelopeVersion xmlns="http://gov.sk/SKTalkMessage">3.0</EnvelopeVersion>
	<Header xmlns="http://gov.sk/SKTalkMessage">
		<MessageInfo>
			<Class>EFORM_SUBSCRIPTION_MESSAGE_ASYNC_01</Class>
			<MessageID>9e1a90d0-b740-4f21-af73-239a023b7b4b</MessageID>
			<CorrelationID>0110d287-ff00-4f15-9ed2-baebd342f450</CorrelationID>
			<BusinessID/>
			<ChannelInfo>
				<Channel>
					<ChannelInfoURI>http://10.20.3.143/eGO.Filler.WS1/Service.svc</ChannelInfoURI>
				</Channel>
			</ChannelInfo>
			<ChannelInfoReply>
				<Channel>
					<ChannelInfoURI>http://10.20.3.143/eGO.Filler.WS1/Service.svc</ChannelInfoURI>
				</Channel>
			</ChannelInfoReply>
		</MessageInfo>
		<SenderInfo>
			<SecurityMethod>security_method</SecurityMethod>
			<SecurityToken/>
			<Identity/>
		</SenderInfo>
		<RoutingInfo/>
	</Header>
	<Body xmlns="http://gov.sk/SKTalkMessage">
		<eFLCMSubscriptionMessage xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:xsd="http://www.w3.org/2001/XMLSchema" xmlns="http://schemas.gov.sk/eflcm/eFLCMSubscribtionMessage/1.1">
			<SubscribedGestor>FillerTest</SubscribedGestor>
			<SubscribedPublisher>UPVSTest</SubscribedPublisher>
			<FormTemplates>
				<EFormTemplate>
					<Publisher>UPVS</Publisher>
					<Gestor>UPVSP-VYVOJ\vladimir.skopik</Gestor>
					<Identifier>Doc.GeneralAgendaStatus</Identifier>
					<Version>
						<Major>1</Major>
						<Minor>3</Minor>
					</Version>
					<Status>PUBLISHED</Status>
					<Changed>2014-07-21T15:30:26</Changed>
					<RelatedDocumentChanged>false</RelatedDocumentChanged>
					<MetaDataChanged>false</MetaDataChanged>
				</EFormTemplate>
				<EFormTemplate>
					<Publisher>UPVS</Publisher>
					<Gestor>UPVSP-VYVOJ\martin.hric</Gestor>
					<Identifier>Doc.GeneralAgendaStatus</Identifier>
					<Version>
						<Major>1</Major>
						<Minor>2</Minor>
					</Version>
					<Status>INVALIDATED</Status>
					<Changed>2014-07-21T15:18:17</Changed>
					<RelatedDocumentChanged>false</RelatedDocumentChanged>
					<MetaDataChanged>false</MetaDataChanged>
				</EFormTemplate>
				<EFormTemplate>
					<Publisher>UPVS</Publisher>
					<Gestor>UPVSP-VYVOJ\vladimir.skopik</Gestor>
					<Identifier>Doc.GeneralAgendaReport</Identifier>
					<Version>
						<Major>1</Major>
						<Minor>3</Minor>
					</Version>
					<Status>PUBLISHED</Status>
					<Changed>2014-07-21T15:30:26</Changed>
					<RelatedDocumentChanged>false</RelatedDocumentChanged>
					<MetaDataChanged>false</MetaDataChanged>
				</EFormTemplate>
				<EFormTemplate>
					<Publisher>UPVS</Publisher>
					<Gestor>UPVSP-VYVOJ\mlassak</Gestor>
					<Identifier>Doc.GeneralAgendaReport</Identifier>
					<Version>
						<Major>1</Major>
						<Minor>2</Minor>
					</Version>
					<Status>INVALIDATED</Status>
					<Changed>2014-07-21T15:18:26</Changed>
					<RelatedDocumentChanged>false</RelatedDocumentChanged>
					<MetaDataChanged>false</MetaDataChanged>
				</EFormTemplate>
				<EFormTemplate>
					<Publisher>UPVS</Publisher>
					<Gestor>UPVSP-VYVOJ\vladimir.skopik</Gestor>
					<Identifier>Doc.GeneralAgendaFiction</Identifier>
					<Version>
						<Major>1</Major>
						<Minor>3</Minor>
					</Version>
					<Status>PUBLISHED</Status>
					<Changed>2014-07-21T15:30:26</Changed>
					<RelatedDocumentChanged>false</RelatedDocumentChanged>
					<MetaDataChanged>false</MetaDataChanged>
				</EFormTemplate>
				<EFormTemplate>
					<Publisher>UPVS</Publisher>
					<Gestor>UPVSP-VYVOJ\mlassak</Gestor>
					<Identifier>Doc.GeneralAgendaFiction</Identifier>
					<Version>
						<Major>1</Major>
						<Minor>2</Minor>
					</Version>
					<Status>INVALIDATED</Status>
					<Changed>2014-07-21T15:18:33</Changed>
					<RelatedDocumentChanged>false</RelatedDocumentChanged>
					<MetaDataChanged>false</MetaDataChanged>
				</EFormTemplate>
				<EFormTemplate>
					<Publisher>UPVS</Publisher>
					<Gestor>UPVSP-VYVOJ\vladimir.skopik</Gestor>
					<Identifier>Doc.GeneralAgenda</Identifier>
					<Version>
						<Major>1</Major>
						<Minor>3</Minor>
					</Version>
					<Status>PUBLISHED</Status>
					<Changed>2014-07-21T15:15:28</Changed>
					<RelatedDocumentChanged>false</RelatedDocumentChanged>
					<MetaDataChanged>false</MetaDataChanged>
				</EFormTemplate>
				<EFormTemplate>
					<Publisher>UPVS</Publisher>
					<Gestor>UPVSP-VYVOJ\mlassak</Gestor>
					<Identifier>Doc.GeneralAgenda</Identifier>
					<Version>
						<Major>1</Major>
						<Minor>2</Minor>
					</Version>
					<Status>INVALIDATED</Status>
					<Changed>2014-07-21T15:13:07</Changed>
					<RelatedDocumentChanged>false</RelatedDocumentChanged>
					<MetaDataChanged>false</MetaDataChanged>
				</EFormTemplate>
				<EFormTemplate>
					<Publisher>UPVS</Publisher>
					<Gestor>UPVSP-VYVOJ\mlassak</Gestor>
					<Identifier>Doc.GeneralAgenda</Identifier>
					<Version>
						<Major>1</Major>
						<Minor>2</Minor>
					</Version>
					<Status>PUBLISHED</Status>
					<Changed>2014-07-21T15:02:00</Changed>
					<RelatedDocumentChanged>true</RelatedDocumentChanged>
					<MetaDataChanged>false</MetaDataChanged>
				</EFormTemplate>
			</FormTemplates>
		</eFLCMSubscriptionMessage>
	</Body>
</SKTalkMessage>


```

> [!NOTE]
> viac o metóde v kapitole 5

### 2.1.5	  EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_ASYNC_01

V tabuľke je pre metódu uvedený popis vstupných a výstupných elementov. Tieto sa pri volaní služby serializujú a ukladajú v rámci SKTalk/Body časti. Popis schém daných typov je uvedení v ďalších kapitolách.

Metóda slúži pre zmenu súčastí elektronického formulára a podlieha schvaľovaniu v NASES. Táto metóda sa môže používať jedine v súlade s bodom 3.1.1 prílohy č. 1 Vyhlášky č. 78/2020 Z. z. o štandardoch pre IT VS. **Upozorňujeme, že zmena súvisiacich dokumentov by sa nemala robiť, nakoľko zmena súčastí formulára môže spôsobiť rozličné problémy** (napríklad neplatnosť už vytvorených podpisov, neaktuálnosť formulárov v rezortných systémoch, nakoľko informácia o zmene súvisiacich dokumentov nie je zasielaná prostredníctvom publish/subscribe mechanizmu, takže sa o zmene súčastí formuláru rezortné systémy, ktoré môžu mať formulár skopírovaný k sebe, nemajú ako dozvedieť).

#### 2.1.5.1	Popis správy (Vstupná):

| **Sk-Talk Class**				                      | EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_ASYNC_01               |
| --------------------------------------------- | ------------------------------------------------------------------- |
| Popis					                                | Žiadosť o zmenu súvisiacich dokumentov vzoru.                       |
| Gestor			                                  | NASES                                                               |
| Typ správy                                    | Technická                                                           |
| Odosielateľ                                   | UPVS – eFORM (MIRRI / ÚPVS)                                         |
| Adresát                                       | Inštitúcia - OVM                                                    |
| Postup spracovania                            | Príjem a spracovanie žiadosti v module eForm                        |
| Správa prenášaná v rámci štruktúry            | SKTALK 3.0 / ChangeFormTemplateRelatedDocuments_Request             |
| Identifikátor elektronického formulára        | http://schemas.gov.sk/eflcm/ChangeFormTemplateRelatedDocuments/1.0  |
| Elektronický podpis objektu v class=FORM      | Nie                                                                 |
| Modul/Rozhranie/Služba                        | eFORM / UIR / ServiceSkTalk3Token.svc                               |
| Modul sprostredkujúci komunikáciu             | UPVS – G2G                                                          |
| Nadväzná správa 1 (odpoveď/notifikácia)       | EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_REPLY_ASYNC_01         |
| Poznámka                                      |                                                                     |

- **CLASSNAME:** EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_ASYNC_01
- **Input Object:** ChangeFormTemplateRelatedDocuments_Request

| **Názov**                 | **Typ**                                                        | **Povinnosť**        | **Popis**                            | 
| ------------------------- | -------------------------------------------------------------- | -------------------- | ------------------------------------ |
| Request                   | EFLCMRequest                                                   | Áno                  | Žiadosť vzoru eFormulára             |
| FormTemplate              | FormTemplateID                                                 | Áno                  | Identifikátor vzoru eFormulára       |
| RelatedDocuments          | RelatedDocument[]                                              | Áno                  | Súvisiace dokumenty                  |

#### 2.1.5.2	Vstupný technický formulár

**Názov štruktúry:** EFLCMRequest

| **Meno**              | **Typ**            | **Povinnosť**     | **Popis**                                                                                        |
| --------------------- | ------------------ | ----------------- | ------------------------------------------------------------------------------------------------ |
| Title                 | String             | Áno               | Názov žiadosti                                                                                   |
| Description           | String             | Áno               | Popis žiadosti                                                                                   |
| Publisher             | String             | Áno               | Inštitúcia ktorá žiadosť podala - subjectID – UPVS URI poskytovateľa v IAM                       |
| Gestor                | String             | Áno               | Gestor elektronického formulára (v GUI MEF sa obvykle uvádza subjectID – UPVS URI gestora v IAM) |

**Názov štruktúry:** FormTemplateID

| **Meno**              | **Typ**            | **Povinnosť**     | **Popis**              |
| --------------------- | ------------------ | ----------------- | ---------------------- |
| Identifier            | String             | Áno               | Identifikátor vzoru    |
| Version               | eFormVersion       | Áno               | Verzia vzoru           |

**Názov štruktúry:** EFormVersion 

| **Meno**              | **Typ**            | **Povinnosť**     | **Popis**              |
| --------------------- | ------------------ | ----------------- | ---------------------- |
| Major                 | int                | Áno               | Verzia vzoru           |
| Minor                 | int                | Áno               | Podverzia vzoru        |

**Názov štruktúry:** RelatedDocument

| **Meno**              | **Typ**                 | **Povinnosť**     | **Popis**                                                 |
| --------------------- | ----------------------- | ----------------- | --------------------------------------------------------- |
| MetaData              | RelatedDocumentMetaData | Áno               | Štruktúra popisujúca metadáta súvisiaceho dokumentu       |
| Data                  | byte[]                  | Áno               | Base64binary dáta súvisiaceho dokumentu                   |

**Názov štruktúry:** RelatedDocumentMetadata

| **Meno**              | **Typ**                 | **Povinnosť**     | **Popis**                                                                 |
| --------------------- | ----------------------- | ----------------- | ------------------------------------------------------------------------- |
| Type                  | String                  | Áno               | Typ súvisiaceho dokumentu (typ súčasti formulára). Možné hodnoty:         |
|                       |                         |                   | CLS_F_XSLT_DEFAULT                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_SGN                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_BODY                                                 |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_SUBJECT                                              |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_BODY                                                |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_SUBJECT                                             |
|                       |                         |                   | CLS_F_XSLT_TXT_SMS                                                        |
|                       |                         |                   | CLS_F_HTML_FORM                                                           |
|                       |                         |                   | CLS_F_XML_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_DCT                                                             |
|                       |                         |                   | CLS_F_XSL_FO                                                              |
|                       |                         |                   | CLS_F_XSLT_RO                                                             |
|                       |                         |                   | CLS_F_DLL_VAL                                                             |
|                       |                         |                   | CLS_F_XML_MTD                                                             |
|                       |                         |                   | CLS_F_XSLT_NAT_EDOC                                                       |
|                       |                         |                   | CLS_F_XSLT_EDOC_NAT                                                       |
|                       |                         |                   | CLS_F_XSLT_HTML                                                           |
|                       |                         |                   | BalikXML                                                                  |
|                       |                         |                   | CLS_F_XML_DEF                                                             |
|                       |                         |                   | CLS_POSP                                                                  |
|                       |                         |                   | POSP_priloha, (táto hodnota sa už nesmie používať v nových formulároch)   |
|                       |                         |                   | POSP, (táto hodnota sa už nesmie používať v nových formulároch)           |
|                       |                         |                   | EFORM_STANDARD_ZIP_PACKAGE                                                |
| Identifier            | String                  | Áno               | Identifikátor vzoru – názov súboru súvisiaceho dokumentu                  |
| Description           | String                  |                   | Popis súvisiaceho dokumentu                                               |
| Language              | String                  | Áno               | Jazyk súvisiaceho dokumentu                                               |

#### 2.1.5.3	Popis správy (Výstupná):

| **Sk-Talk Class**				                      | EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_REPLY_ASYNC_01           |
| --------------------------------------------- | --------------------------------------------------------------------- |
| Popis					                                | Odpoveď na žiadosť o zmenu súvisiacich dokumentov vzoru.              |
| Gestor			                                  | NASES                                                                 |
| Typ správy                                    | Technická                                                             |
| Odosielateľ                                   | UPVS – eFORM (MIRRI/ÚPVS)                                             |
| Adresát                                       | Inštitúcia - OVM                                                      |
| Postup spracovania                            | NA                                                                    |
| Správa prenášaná v rámci štruktúry            | SKTALK 3.0/ChangeFormTemplateRelatedDocuments_Response                |
| Identifikátor elektronického formulára        | http://schemas.gov.sk/eflcm/ChangeFormTemplateRelatedDocuments/1.0    |
| Elektronický podpis objektu v class=FORM      | Nie                                                                   |
| Modul/Rozhranie/Služba                        | eFORM / UIR / ServiceSkTalk3Token.svc                                 |
| Modul sprostredkujúci komunikáciu             | UPVS – G2G                                                            |
| Nadväzná správa 1 (odpoveď/notifikácia)       | NA                                                                    |
| Poznámka                                      |                                                                       |

#### 2.1.5.4	Výstupný technický formulár - Odpoveď:

| **Názov**                                                          | **Popis**     |
|--------------------------------------------------------------------|---------------|
| http://schemas.gov.sk/form/G2G.InformationMessage/1.3              | Viď IM – G2G  |
| http://schemas.gov.sk/eflcm/eFLCMExceptionMessage/1.0              | Viď vyššie    |
| http://schemas.gov.sk/eflcm/ChangeFormTemplateRelatedDocuments/1.0 | Viď nižšie    |

**Názov štruktúry:** sk/1.1 - ChangeFormTemplateRelatedDocuments

| **Meno**   | **Typ**| **Povinnosť** | **Popis**       |
|------------|--------|---------------|-----------------|
| Identifier | string | Nie           | Identifikátor   |
| Version    | string | Nie           | Verzia vzoru    |
| Major      | string | Nie           | Verzia hlavná   |

#### 2.1.5.5	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000797
-	06000794

#### 2.1.5.6	Príklad volania služby – SKTalk

- [Príklad SKTalk Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_ASYNC_01)

### 2.1.6	  EFORM_ADD_ROLE_TO_FORM_TEMPLATE_ASYNC_01 

eForm poskytuje asynchrónne služby na pridanie/odobratie oprávnení vzoru pre príslušnú skupinu/rolu evidovanú v IAM. V prípade, ak sa na vzor pridá aspoň jedna skupina prostredníctvom tejto služby, je takto upravený vzor prístupný prostredníctvom služieb eFormu len pre overených používateľov disponujúcich danou IAM rolou.
Táto služba sa v novom module elektronických formulárov **nepoužíva**, resp. nastavenie oprávnení sa neuplatňuje. Nastavenie oprávnení mohlo spôsobiť nedostupnosť formulára pre niektoré skupiny používateľov, pričom podľa zákona o eGovernmente musia byť všetky elektronické formuláre verejne dostupné.

#### 2.1.6.1	Popis správy (Vstupná):

| **Sk-Talk Class**                        | EFORM_ADD_ROLE_TO_FORM_TEMPLATE_ASYNC_01               |
|------------------------------------------|--------------------------------------------------------|
| Popis                                    | Žiadosť o pridanie oprávnení vzoru.                    |
| Gestor                                   | NASES                                                  |
| Typ správy                               | Technická                                              |
| Odosielateľ                              | Inštitúcia - OVM                                       |
| Adresát                                  | UPVS – eFORM (MIRRI / ÚPVS)                            |
| Postup spracovania                       | Príjem a spracovanie žiadosti v module eForm           |
| Správa prenášaná v rámci štruktúry       | SKTALK 3.0 / AddRoleToFormTemplate_Request             |
| Identifikátor elektronického formulára   | http://schemas.gov.sk/eflcm/AddRoleToFormTemplate/1.0  |
| Elektronický podpis objektu v class=FORM | Nie                                                    |
| Modul/Rozhranie/Služba                   | eFORM / UIR / ServiceSkTalk3Token.svc                  |
| Modul sprostredkujúci komunikáciu        | UPVS – G2G                                             |
| Nadväzná správa 1 (odpoveď/notifikácia)  | NA                                                     |
| Poznámka                                 | NEPOUŽÍVA SA – uvedená z historických dôvodov          |

#### 2.1.6.2	Vstupný technický formulár

- **CLASSNAME:** EFORM_ADD_ROLE_TO_FORM_TEMPLATE_ASYNC_01
- **Input Object:** AddRoleToFormTemplate_Request

| **Meno**     | **Typ**        | **Povinnosť** | **Popis**                 |
|--------------|----------------|---------------|---------------------------|
| Request      | EFLCMRequest   | Áno           | Žiadosť vzoru eFormulára  |
| FormTemplate | FormTemplateID | Áno           | ID Vzoru eFormulára       |
| RoleName     | string         | Áno           | Názov role                |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** EFLCMRequest 

| **Meno**    | **Typ**| **Povinnosť** | **Popis**                                                                    |
|-------------|--------|---------------|------------------------------------------------------------------------------|
| Title       | String | Áno           | Názov žiadosti                                                               |
| Description | String | Áno           | Popis žiadosti                                                               |
| Publisher   | String | Áno           | Inštitúcia ktorá žiadosť podala - subjectID – UPVS URI poskytovateľa v IAM   |

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

#### 2.1.6.3	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy**
-	06000997
-	06000998
-	06000999
-	06000798
-	06000797
-	06000795

#### 2.1.6.4	Príklad volania služby – SKTalk

- [Príklad SKTalk Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_ADD_ROLE_TO_FORM_TEMPLATE_ASYNC_01)

### 2.1.7	  EFORM_REMOVE_ROLE_TO_FORM_TEMPLATE_ASYNC_01

Služba slúži na pridanie/odobratie oprávnení vzoru pre príslušnú skupinu/rolu evidovanú v IAM. V prípade, ak sa na vzor pridá aspoň jedna skupina, prostredníctvom tejto služby, je takto upravený vzor prístupný prostredníctvom služieb eFormu len pre overených používateľov disponujúcich danou IAM rolou.

#### 2.1.7.1	Popis správy (Vstupná):

| **Sk-Talk Class**                        | EFORM_REMOVE_ROLE_TO_FORM_TEMPLATE_ASYNC_01                 |
|------------------------------------------|-------------------------------------------------------------|
| Popis                                    | Žiadosť o odobratie oprávnení vzoru.                        |
| Gestor                                   | NASES                                                       |
| Typ správy                               | Technická                                                   |
| Odosielateľ                              | Inštitúcia - OVM                                            |
| Adresát                                  | UPVS – eFORM (MIRRI / ÚPVS)                                 |
| Postup spracovania                       | Príjem a spracovanie žiadosti v module eForm                |
| Správa prenášaná v rámci štruktúry       | SKTALK 3.0 / RemoveRoleFromFormTemplate_Request             |
| Identifikátor elektronického formulára   | http://schemas.gov.sk/eflcm/RemoveRoleFromFormTemplate/1.0  |
| Elektronický podpis objektu v class=FORM | Nie                                                         |
| Modul/Rozhranie/Služba                   | eFORM / UIR / ServiceSkTalk3Token.svc                       |
| Modul sprostredkujúci komunikáciu        | UPVS – G2G                                                  |
| Nadväzná správa 1 (odpoveď/notifikácia)  | NA                                                          |
| Poznámka                                 | NEPOUŽÍVA SA – uvedená z historických dôvodov               |

#### 2.1.7.2	Vstupný technický formulár

- **CLASSNAME:** EFORM_REMOVE_ROLE_TO_FORM_TEMPLATE_ASYNC_01
- **Input Object:** RemoveRoleFromFormTemplate_Request

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**                 |
|--------------|----------------|---------------|---------------------------|
| Request      | EFLCMRequest   | Áno           | Žiadosť vzoru eFormulára  |
| FormTemplate | FormTemplateID | Áno           | ID Vzoru eFormulára       |
| RoleName     | string         | Áno           | Názov role                |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** EFLCMRequest 

| **Meno**    | **Typ** | **Povinnosť** | **Popis**                                                                     |
|-------------|---------|---------------|-------------------------------------------------------------------------------|
| Title       | String  | Áno           | Názov žiadosti                                                                |
| Description | String  | Áno           | Popis žiadosti                                                                |
| Publisher   | String  | Áno           | Inštitúcia ktorá žiadosť podala - subjectID – UPVS URI poskytovateľa v IAM).  |

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

#### 2.1.7.3	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000798
-	06000797
-	06000795

#### 2.1.7.4	Príklad volania služby – SKTalk

- [Príklad SKTalk Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_REMOVE_ROLE_TO_FORM_TEMPLATE_ASYNC_01)

### 2.1.8	  EFORM_ADD_FORM_TEMPLATE_ASYNC_02

Služba je určená na registrovanie vzoru eformulára v štandardnom balíku .zip podľa Vyhlášky č. 78/2020 Z.z. o štandardoch pre IT VS. Registrácia prebieha odoslaním SKTalk správy na G2G rozhranie UPVS, pričom v body časti je vložený formulár upvs.eform.EFormRequest vo verzii 1.0 so žiadosťou. Tento je uložený v rámci Message containera. Štruktúra formuláru je popísaná v nasledovnej tabuľke:

#### 2.1.8.1	Popis správy (Vstupná):

| **Sk-Talk Class**                        | **EFORM_ADD_FORM_TEMPLATE_ASYNC_02**                             |
|------------------------------------------|------------------------------------------------------------------|
| Popis                                    | Žiadosť o registráciu vzoru v zmysle výnosu o štandardoch ISVS.  |
| Gestor                                   | NASES                                                            |
| Typ správy                               | Technická                                                        |
| Odosielateľ                              | Inštitúcia - OVM                                                 |
| Adresát                                  | UPVS – eFORM (MIRRI / ÚPVS)                                      |
| Postup spracovania                       | Príjem a spracovanie žiadosti v module eForm                     |
| Správa prenášaná v rámci štruktúry       | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“             |
| Identifikátor elektronického formulára   | http://schemas.gov.sk/form/upvs.eform.EFormRequest/1.0           |
| Elektronický podpis objektu v class=FORM | Nie                                                              |
| Modul/Rozhranie/Služba                   | eFORM / UIR / ServiceSkTalk3Token.svc                            |
| Modul sprostredkujúci komunikáciu        | UPVS – G2G                                                       |
| Nadväzná správa 1 (odpoveď/notifikácia)  | EFORM_ADD_FORM_TEMPLATE_REPLY_VALIDATION_REPORT_ASYNC_02         |
| Poznámka                                 |                                                                  |

#### 2.1.8.2	Vstupný technický formulár

- **CLASSNAME:** EFORM_ADD_FORM_TEMPLATE_ASYNC_02
- **Input Object:** http://schemas.gov.sk/form/upvs.eform.EFormRequest/1.0

| **Názov**   | **Typ** | **Povinnosť** | **Popis**                        |
|-------------|---------|---------------|----------------------------------|
| Title       | String  | Áno           | Názov žiadosti                   |
| Description | String  | Áno           | Popis žiadosti                   |
| Publisher   | String  | Áno           | Inštitúcia ktorá vzor publikuje  |
| Gestor      | String  | Áno           | Gestor za daný vzor              |

Samotný formulár je v rámci message containera ako samostatný objekt typu ATTACHMENT. Formát vloženého balíka sa určuje podľa MIMEType atribútu v message containery pre daný objekt. Kde platí že:
-	hodnota mimetype ak je **application/vnd.gov.sk.e-form+zip** tak vložený objekt je kódovaný base64 ZIP súbor, 
-	pokiaľ by bola hodnota **application/vnd.gov.sk.e-form+xml** tak vložený objekt je balík vo formáte XML, avšak tento formát už vzhľadom na novelu vyhlášky č. 78/2020 Z. z. nie je podporovaný.

#### 2.1.8.3	Popis správy (Výstupná):

Na výstupe sa môžu vrátiť tri rôzne Sk-Talk Class:
Odpoveď na žiadosť o registráciu formulára sa vracia len v prípade úspešnej registrácie alebo chyby, ktorá nebola zistená v rámci vstupných validácií. Nevracia sa v prípade zistenej chyby pri validácii, ktorá má za následok nezaregistrovanie formulára.

| **Sk-Talk Class**                                                    | **EFORM_ADD_FORM_TEMPLATE_REPLY_ASYNC_02**              |
|----------------------------------------------------------------------|---------------------------------------------------------|
| Popis                                                                | Odpoveď na žiadosť o registráciu vzoru .zip balíka.     |
| Gestor                                                               | NASES                                                   |
| Typ správy                                                           | Technická                                               |
| Odosielateľ                                                          | UPVS – eFORM (MIRRI/ÚPVS)                               |
| Adresát                                                              | Inštitúcia - OVM                                        |
| Postup spracovania                                                   | NA                                                      |
| Správa prenášaná v rámci štruktúry                                   | SKTALK 3.0/MessageContainer/ObjectClass = „FORM“        |
| Identifikátor elektronického formulára                               | http://schemas.gov.sk/form/G2G.InformationMessage/1.3   |
| alebo                                                                |                                                         |
| http://schemas.gov.sk/form/G2G.ErrorMessage/1.3                      |                                                         |
| http://schemas.gov.sk/form/MEF.Preprocessor.ValidationReport.sk/1.1  |                                                         |
| Elektronický podpis objektu v class=FORM                             | Nie                                                     |
| Modul/Rozhranie/Služba                                               | eFORM / UIR / ServiceSkTalk3Token.svc                   |
| Modul sprostredkujúci komunikáciu                                    | UPVS – G2G                                              |
| Nadväzná správa 1 (odpoveď/notifikácia)                              | NA                                                      |
| Poznámka                                                             |                                                         |

Odpoveď na žiadosť o registráciu vzoru – registrácia formulára pokračuje úspešne ďalej, je zaslaný výsledok **validácie formulára so zistenými upozorneniami pri validácii formulára** („WARNING“ v nastavení validácií), ktoré je žiadúce opraviť, ale neblokujú registráciu formulára.

| **Sk-Talk Class**                         | **EFORM_ADD_FORM_TEMPLATE_REPLY_VALIDATION_REPORT_ASYNC_02**                                                              |
|-------------------------------------------|---------------------------------------------------------------------------------------------------------------------------|
| Popis                                     | Odpoveď na žiadosť o registráciu vzoru - registrácia formulára pokračuje úspešne ďalej, je zaslaný výsledok validácie formulára so zistenými upozorneniami pri validácii formulára („WARNING“ v nastavení validácií), ktoré je žiadúce opraviť ale neblokujú registráciu formulára.                                                              |
| Gestor                                    | NASES                                                                                                                     |
| Typ správy                                | Technická                                                                                                                 |
| Odosielateľ                               | UPVS – eFORM (MIRRI / ÚPVS)                                                                                               |
| Adresát                                   | Inštitúcia - OVM                                                                                                          |
| Postup spracovania                        | Je potrebné opraviť elektronický formulár v ďalšej verzii formulára. Registrácia aktuálneho formulára prebieha ďalej.     |
| Správa prenášaná v rámci štruktúry        | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“                                                                      |
| Identifikátor elektronického formulára    | http://schemas.gov.sk/form/MEF.Preprocessor.ValidationReport.sk/1.1                                                       |
| Elektronický podpis objektu v class=FORM  | Nie                                                                                                                       |
| Modul/Rozhranie/Služba                    | eFORM / UIR / ServiceSkTalk3Token.svc                                                                                     |
| Modul sprostredkujúci komunikáciu         | UPVS – G2G                                                                                                                |
| Nadväzná správa 1 (odpoveď/notifikácia)   | NA                                                                                                                        |
| Poznámka                                  |                                                                                                                           |

Odpoveď na žiadosť o registráciu vzoru - **spracovanie registrácie formulára ukončené chybou zistenou pri validácii formulára** („ERROR“ v nastavení validácií).

| **Sk-Talk Class**                        | **EFORM_ADD_FORM_TEMPLATE_REPLY_REFUSE_VALIDATION_REPORT_ASYNC_02**                 |
|------------------------------------------|-------------------------------------------------------------------------------------|
| Popis                                    | Odpoveď na žiadosť o registráciu vzoru - spracovanie registrácie formulára ukončené chybou zistenou pri validácii formulára (ERROR v nastavení validácií) a formulár nie je v MEF zaregistrovaný.                                                                                                         |
| Gestor                                   | NASES                                                                               |
| Typ správy                               | Technická                                                                           |
| Predmet správy                           | Validačný report                                                                    |
| Odosielateľ                              | UPVS – eFORM (MIRRI / ÚPVS)                                                         |
| Adresát                                  | Inštitúcia - OVM                                                                    |
| Postup spracovania                       | Je potrebné opraviť elektronický formulár a registráciu vykonať následne opätovne.  |
| Správa prenášaná v rámci štruktúry       | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“                                |
| Identifikátor elektronického formulára   | http://schemas.gov.sk/form/MEF.Preprocessor.ValidationReport.sk/1.1                 |
| Elektronický podpis objektu v class=FORM | Nie                                                                                 |
| Modul/Rozhranie/Služba                   | eFORM / UIR / ServiceSkTalk3Token.svc                                               |
| Modul sprostredkujúci komunikáciu        | UPVS – G2G                                                                          |
| Nadväzná správa 1 (odpoveď/notifikácia)  | NA                                                                                  |
| Poznámka                                 |                                                                                     |

#### 2.1.8.4	Výstupný technický formulár - Odpoveď

- **CLASSNAME:** EFORM_ADD_FORM_TEMPLATE_REPLY_ASYNC_02
- **Output Object:**

| **Názov**                                             | **Popis**     |
|-------------------------------------------------------|---------------|
| http://schemas.gov.sk/form/G2G.InformationMessage/1.3 | Viď IM – G2G  |
| http://schemas.gov.sk/form/G2G.ErrorMessage/1.3       | Viď IM – G2G  |

- **CLASSNAME:** EFORM_ADD_FORM_TEMPLATE_REPLY_VALIDATION_REPORT_ASYNC_02
- **Output object:**

| **Názov**                                                           |
|---------------------------------------------------------------------|
| http://schemas.gov.sk/form/MEF.Preprocessor.ValidationReport.sk/1.1 |

- **CLASSNAME:** EFORM_ADD_FORM_TEMPLATE_REPLY_REFUSE_VALIDATION_REPORT_ASYNC_02
- **Output object:**

| **Názov**                                                           |
|---------------------------------------------------------------------|
| http://schemas.gov.sk/form/MEF.Preprocessor.ValidationReport.sk/1.1 |

#### 2.1.8.5	Chybové kódy služby

**Chybové stavy:**
- 06000997

#### 2.1.8.6	Príklad volania služby – SKTalk

- [Príklad SKTalk Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_ADD_FORM_TEMPLATE_ASYNC_02)

### 2.1.9 	EFORM_ADD_NOTIFY_TEMPLATE_ASYNC_01

Služba je určená na registrovanie vzoru eFormulára typu notifikačná šablóna v štandardnom balíku ZIP alebo XML. Registrácia prebieha odoslaním SKTalk správy na G2G rozhranie UPVS, pričom v body časti je vložený formulár upvs.eform.EFormRequest vo verzii 1.0 so žiadosťou. Tento je uložený v rámci Message containera. Štruktúra formuláru je popísaná v nasledovnej tabuľke nižšie.

#### 2.1.9.1	Popis správy (Vstupná):

| **Sk-Talk Class**                        | **EFORM_ADD_NOTIFY_TEMPLATE_ASYNC_01**                    |
|------------------------------------------|-----------------------------------------------------------|
| Popis                                    | Žiadosť o registráciu notifikačnej šablóny.               |
| Gestor                                   | NASES                                                     |
| Typ správy                               | Technická                                                 |
| Odosielateľ                              | Inštitúcia - OVM                                          |
| Adresát                                  | UPVS – eFORM (MIRRI / ÚPVS)                               |
| Postup spracovania                       | Príjem, validácia a spracovanie žiadosti v module eForm.  |
| Správa prenášaná v rámci štruktúry       | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“      |
| Identifikátor elektronického formulára   | http://schemas.gov.sk/form/upvs.eform.EFormRequest/1.0    |
| Elektronický podpis objektu v class=FORM | Nie                                                       |
| Modul/Rozhranie/Služba                   | eFORM / UIR / ServiceSkTalk3Token.svc                     |
| Modul sprostredkujúci komunikáciu        | UPVS – G2G                                                |
| Nadväzná správa 1 (odpoveď/notifikácia)  | EFORM_ADD_NOTIFY_TEMPLATE_REPLY_ASYNC_01                  |
| Poznámka                                 |                                                           |

#### 2.1.9.2	Vstupný technický formulár

- **CLASSNAME:** EFORM_ADD_NOTIFY_TEMPLATE_ASYNC_01
- **Input Object:** http://schemas.gov.sk/form/upvs.eform.EFormRequest/1.0

| **Title**   | **String** | **Áno** | **Názov žiadosti**               |
|-------------|------------|---------|----------------------------------|
| Description | String     | Áno     | Popis žiadosti                   |
| Publisher   | String     | Áno     | Inštitúcia ktorá vzor publikuje  |
| Gestor      | String     | Áno     | Gestor za daný vzor              |

Samotný formulár je v rámci message containera ako samostatný objekt typu ATTACHMENT.  
Formát vloženého balíka sa určuje podľa MIMEType atribútu v message containeri pre daný objekt. Kde platí že:
-	hodnota mimetype ak je **application/vnd.gov.sk.e-form+zip** tak vložený objekt je kódovaný base64 .zip súbor, 
-	pokiaľ je hodnota **application/vnd.gov.sk.e-form+xml** tak vložený objekt je balík vo formáte XML , pričom pokiaľ je atribút ENCODING nastavený na Base64 tak .xml súbor je encodovaný ako base64 reťazec.

#### 2.1.9.3	Popis správy (Výstupná):

| **Sk-Talk Class**                                      | **EFORM_ADD_NOTIFY_TEMPLATE_REPLY_ASYNC_01**            |
|--------------------------------------------------------|---------------------------------------------------------|
| Popis                                                  | Odpoveď na žiadosť o registráciu notifikačnej šablóny.  |
| Gestor                                                 | NASES                                                   |
| Typ správy                                             | Technická                                               |
| Odosielateľ                                            | UPVS – eFORM (MIRRI / ÚPVS)                             |
| Adresát                                                | Inštitúcia - OVM                                        |
| Postup spracovania                                     | NA                                                      |
| Správa prenášaná v rámci štruktúry                     | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“    |
| Identifikátor elektronického formulára                 | http://schemas.gov.sk/form/G2G.InformationMessage/1.3   |
| http://schemas.gov.sk/eflcm/eFLCMExceptionMessage/1.0  |                                                         |
| Elektronický podpis objektu v class=FORM               | Nie                                                     |
| Modul/Rozhranie/Služba                                 | eFORM / UIR / ServiceSkTalk3Token.svc                   |
| Modul sprostredkujúci komunikáciu                      | UPVS – G2G                                              |
| Nadväzná správa 1 (odpoveď/notifikácia)                | NA                                                      |
| Poznámka                                               |                                                         |

#### 2.1.9.4	Výstupný technický formulár - Odpoveď

- **CLASSNAME:**
- **Output Object:**

| **Názov**                                             | **Popis**      |
|-------------------------------------------------------|----------------|
| http://schemas.gov.sk/form/G2G.InformationMessage/1.3 | Vid. IM – G2G  |
| http://schemas.gov.sk/eflcm/eFLCMExceptionMessage/1.0 | Vid. vyššie    |

#### 2.1.9.5	Chybové kódy služby

**Chybové stavy:**
-	06000997

#### 2.1.9.6	Príklad volania služby – SKTalk

- [Príklad SKTalk Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_ADD_NOTIFY_TEMPLATE_ASYNC_01)

### 2.1.10	EFORM_CHANGE_NOTIFY_TEMPLATE_METADATA_ASYNC_01

Služba je určená na zmenu metadát vzoru eFormulára typu notifikačná **šablóna v štandardnom balíku .zip alebo XML.**  

Notifikačné šablóny slúžia len pre prípad, ak OVM chce vytvárať a zasielať notifikácie cez modul eNotify a na tento účel používať notifikačné šablóny. Táto funkčnosť sa v praxi obvykle nepoužíva a preto je potrebné si dať pozor, aby táto služba nebola omylom používaná namiesto registrácie formulára.

Registrácia prebieha odoslaním SKTalk správy na G2G rozhranie UPVS, pričom v „body“ časti je vložený formulár upvs.eform.EFormRequest vo verzii 1.0 so žiadosťou. Tento je uložený v rámci Message containera. Štruktúra formuláru je popísaná v nasledovnej tabuľke:

#### 2.1.10.1	Popis správy (Vstupná):

| **Sk-Talk Class**                        | **EFORM_CHANGE_NOTIFY_TEMPLATE_METADATA_ASYNC_01**              |
|------------------------------------------|-----------------------------------------------------------------|
| Popis                                    | Žiadosť o zmenu metadát existujúceho vzoru – typu notifikácia.  |
| Gestor                                   | NASES                                                           |
| Typ správy                               | Technická                                                       |
| Odosielateľ                              | Inštitúcia - OVM                                                |
| Adresát                                  | UPVS – eFORM (MIRRI / ÚPVS)                                     |
| Postup spracovania                       | Príjem a spracovanie žiadosti v module eForm.                   |
| Správa prenášaná v rámci štruktúry       | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“            |
| Identifikátor elektronického formulára   | http://schemas.gov.sk/form/upvs.eform.EFormRequest/1.0          |
| Elektronický podpis objektu v class=FORM | Nie                                                             |
| Modul/Rozhranie/Služba                   | eFORM / UIR / ServiceSkTalk3Token.svc                           |
| Modul sprostredkujúci komunikáciu        | UPVS – G2G                                                      |
| Nadväzná správa 1 (odpoveď/notifikácia)  | EFORM_CHANGE_NOTIFY_TEMPLATE_METADATA_REPLY_ASYNC_01            |
| Poznámka                                 |                                                                 |

#### 2.1.10.2	Vstupný technický formulár

- **CLASSNAME:** EFORM_CHANGE_NOTIFY_TEMPLATE_METADATA_ASYNC_01
- **Input Object:** http://schemas.gov.sk/form/upvs.eform.EFormRequest/1.0

| **Názov**   | **Typ** | **Povinnosť** | **Popis**                        |
|-------------|---------|---------------|----------------------------------|
| Title       | String  | Áno           | Názov žiadosti                   |
| Description | String  | Áno           | Popis žiadosti                   |
| Publisher   | String  | Áno           | Inštitúcia ktorá vzor publikuje  |
| Gestor      | String  | Áno           | Gestor za daný vzor              |

Samotné metadáta sú v rámci message containera ako samostatný objekt typu **ATTACHMENT**. Ako metadáta sa vkladá súbor meta.xml. Pri vkladaní tohto súboru, pokiaľ je vkladaný ako base64, je potrebné nastaviť atribút ENCODING v message containery pre objekt na Base64.

#### 2.1.10.3	Popis správy (Výstupná):

| **Sk-Talk Class**                                      | **EFORM_CHANGE_NOTIFY_TEMPLATE_METADATA_REPLY_ASYNC_01**                   |
|--------------------------------------------------------|----------------------------------------------------------------------------|
| Popis                                                  | Odpoveď na žiadosť o zmenu metadát existujúceho vzoru – typu notifikácia.  |
| Gestor                                                 | NASES                                                                      |
| Typ správy                                             | Technická                                                                  |
| Odosielateľ                                            | UPVS – eFORM (MIRRI / ÚPVS)                                                |
| Adresát                                                | Inštitúcia - OVM                                                           |
| Postup spracovania                                     | NA                                                                         |
| Správa prenášaná v rámci štruktúry                     | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“                       |
| Identifikátor elektronického formulára                 | http://schemas.gov.sk/form/G2G.InformationMessage/1.3                      |
|	  										  			 | http://schemas.gov.sk/eflcm/eFLCMExceptionMessage/1.0                      |   
| Elektronický podpis objektu v class=FORM               | Nie                                                                        |
| Modul/Rozhranie/Služba                                 | eFORM / UIR / ServiceSkTalk3Token.svc                                      |
| Modul sprostredkujúci komunikáciu                      | UPVS – G2G                                                                 |
| Nadväzná správa 1 (odpoveď/notifikácia)                | NA                                                                         |
| Poznámka                                               |                                                                            |

#### 2.1.10.4	Výstupný technický formulár - Odpoveď

- **CLASSNAME:**
- **Output Object:**

| **Názov**                                             | **Popis**      |
|-------------------------------------------------------|----------------|
| http://schemas.gov.sk/form/G2G.InformationMessage/1.3 | Vid. IM – G2G  |
| http://schemas.gov.sk/eflcm/eFLCMExceptionMessage/1.0 | Vid. vyššie    |

#### 2.1.10.5	Chybové kódy služby

**Chybové stavy:**
-	06000997

#### 2.1.10.6	Príklad volania služby – SKTalk

- [Príklad SKTalk Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_CHANGE_NOTIFY_TEMPLATE_METADATA_ASYNC_01)

### 2.1.11	EFORM_CHANGE_FORM_TEMPLATE_METADATA_ASYNC_02

Služba je určená na zmenu metadát vzoru eFormulára typu eFormulár v štandardnom balíku .zip alebo XML.  Registrácia prebieha odoslaním SKTalk správy na G2G rozhranie UPVS, pričom v body časti je vložený formulár upvs.eform.EFormRequest vo verzii 1.0 so žiadosťou. Tento je uložený v rámci Message containera. Štruktúra formuláru je popísaná v nasledovnej tabuľke nižšie.

#### 2.1.11.1	Popis správy (Vstupná):

| **Sk-Talk Class**                        | **EFORM_CHANGE_FORM_TEMPLATE_METADATA_ASYNC_02**        |
|------------------------------------------|---------------------------------------------------------|
| Popis                                    | Žiadosť o zmenu metadát existujúceho vzoru - v02.       |
| Gestor                                   | NASES                                                   |
| Typ správy                               | Technická                                               |
| Odosielateľ                              | Inštitúcia - OVM                                        |
| Adresát                                  | UPVS – (MIRRI / ÚPVS)                                   |
| Postup spracovania                       | Príjem a spracovanie žiadosti v module eForm.           |
| Správa prenášaná v rámci štruktúry       | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“    |
| Identifikátor elektronického formulára   | http://schemas.gov.sk/form/upvs.eform.EFormRequest/1.0  |
| Elektronický podpis objektu v class=FORM | Nie                                                     |
| Modul/Rozhranie/Služba                   | eFORM / UIR / ServiceSkTalk3Token.svc                   |
| Modul sprostredkujúci komunikáciu        | UPVS – G2G                                              |
| Nadväzná správa 1 (odpoveď/notifikácia)  | EFORM_CHANGE_FORM_TEMPLATE_METADATA_REPLY_ASYNC_02      |
| Poznámka                                 |                                                         |

#### 2.1.11.2	Vstupný technický formulár

- **CLASSNAME:** EFORM_CHANGE_FORM_TEMPLATE_METADATA_ASYNC_02
- **Input Object:** http://schemas.gov.sk/form/upvs.eform.EFormRequest/1.0

| **Názov**   | **Typ** | **Povinnosť** | **Popis**                        |
|-------------|---------|---------------|----------------------------------|
| Title       | String  | Áno           | Názov žiadosti                   |
| Description | String  | Áno           | Popis žiadosti                   |
| Publisher   | String  | Áno           | Inštitúcia ktorá vzor publikuje  |
| Gestor      | String  | Áno           | Gestor za daný vzor              |

Samotné metadáta sú v rámci message containera ako samostatný objekt typu ATTACHMENT. Ako metadáta sa vkladá súbor meta.xml. Pri vkladaní tohto súboru pokiaľ je vkladaný ako base64 je potrebné nastaviť atribút ENCODING v message containery pre objekt na Base64.

#### 2.1.11.3	Popis správy (Výstupná):

| **Sk-Talk Class**                                                                                                          | **EFORM_CHANGE_FORM_TEMPLATE_METADATA_REPLY_ASYNC_02**  |
|----------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------|
| Popis                                                                                                                      | Odpoveď na žiadosť o zmenu metadát existujúceho vzoru.  |
| Gestor                                                                                                                     | NASES                                                   |
| Typ správy                                                                                                                 | Technická                                               |
| Odosielateľ                                                                                                                | UPVS – (MIRRI / ÚPVS)                                   |
| Adresát                                                                                                                    | Inštitúcia - OVM                                        |
| Postup spracovania                                                                                                         | NA                                                      |
| Správa prenášaná v rámci štruktúry                                                                                         | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“    |
| Identifikátor elektronického formulára                                                                                     | http://schemas.gov.sk/form/G2G.InformationMessage/1.3   |
|                                                                                                                            | alebo špecifická štruktúra, ktorá nie je elektronickým formulárom: http://schemas.gov.sk/eflcm/eFLCMExceptionMessage/1.0                                                                                                                                                     |
| Elektronický podpis objektu v class=FORM                                                                                   | Nie                                                     |
| Modul/Rozhranie/Služba                                                                                                     | eFORM / UIR / ServiceSkTalk3Token.svc                   |
| Modul sprostredkujúci komunikáciu                                                                                          | UPVS – G2G                                              |
| Nadväzná správa 1 (odpoveď/notifikácia)                                                                                    | NA                                                      |
| Poznámka                                                                                                                   |                                                         |

#### 2.1.11.4	Výstupný technický formulár - Odpoveď

- **CLASSNAME:**
- **Output Object:**

| **Názov**                                             | **Popis**     |
|-------------------------------------------------------|---------------|
| http://schemas.gov.sk/form/G2G.InformationMessage/1.3 | Viď IM – G2G  |
| http://schemas.gov.sk/eflcm/eFLCMExceptionMessage/1.0 | Viď vyššie    |

#### 2.1.11.5	Chybové kódy služby

**Chybové stavy:**
-	06000997

#### 2.1.11.6	Príklad volania služby – SKTalk

- [Príklad SKTalk Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_CHANGE_FORM_TEMPLATE_METADATA_ASYNC_02)

### 2.1.12	EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_01

Služba je určená na validáciu vzoru eFormulára v balíku vo formáte pkg+xml, pred jeho registráciou v úložisku vzorov. Validácia prebieha odoslaním SKTalk správy na G2G rozhranie UPVS. Výsledný validačný report je zaslaný do eDesku identity odosielateľa žiadosti. Služba je dostupná aj pre subjekty, ktoré nie sú orgánmi verejnej moci.

Štruktúra žiadosti o validáciu je rovnaká ako pri žiadosti o registráciu nového vzoru podľa EFORM_ADD_FORM_TEMPLATE_ASYNC_01.

#### 2.1.12.1	Popis správy (Vstupná):

| ****                                      | ****                                                                                                                                                   |
|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|                                           |                                                                                                                                                        |
|                                           |                                                                                                                                                        |
| Sk-Talk Class                             | EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_01                                                                                                                  |
| Popis                                     | Správa slúži na zaslanie žiadosti o validáciu elektronického formulára  vo formáte pkg+xml pre účely preverenia validity formulára.                    |
| Gestor                                    | NASES                                                                                                                                                  |
| Typ správy                                | Technická                                                                                                                                              |
| Odosielateľ                               | OVM, PO, FO                                                                                                                                            |
| Adresát                                   | UPVS (MIRRI / ÚPVS) – aktuálne ico://sk/50349287_10005                                                                                                 |
| Postup spracovania                        | Zobrazenie na strane odosielateľa. Spracúva sa na strane UPVS/MEF, ktorý vykoná validáciu                                                              |
| Správa prenášaná v rámci štruktúry        | MessageContainer                                                                                                                                       |
| Identifikátor elektronického formulára    | http://schemas.gov.sk/eflcm/InsertNewFormTemplate/1.0 (špecifická štruktúra, ktorá nie je registrovaná ako elektronický formulár v eFORM/MEF)          |
| Elektronický podpis objektu v class=FORM  | nie                                                                                                                                                    |
| Modul/Rozhranie/Služba                    | eFORM                                                                                                                                                  |
| Modul sprostredkujúci komunikáciu         | NA                                                                                                                                                     |
| Nadväzná správa 1 (odpoveď/notifikácia)   | EFORM_VALIDATE_FORM_TEMPLATE_REPLY_ASYNC_01                                                                                                            |
| Poznámka                                  |                                                                                                                                                        |

#### 2.1.12.2	Vstupný technický formulár

- **CLASSNAME:** EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_01
- **Input Object:** InsertNewFormTemplate_Request

| **Názov**    | **Typ**      | **Povinnosť** | **Popis**                 |
|--------------|--------------|---------------|---------------------------|
| Request      | EFLCMRequest | Áno           | Žiadosť vzoru eFormulára  |
| FormTemplate | FormTemplate | Áno           | Vzor EFormulára           |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** EFLCMRequest

| **Meno**    | **Typ** | **Povinnosť**  | **Popis**                                                                                         |
|-------------|---------|----------------|---------------------------------------------------------------------------------------------------|
| Title       | String  | Áno            | Názov žiadosti                                                                                    |
| Description | String  | Áno            | Popis žiadosti                                                                                    |
| Publisher   | String  | Áno            | Inštitúcia ktorá žiadosť podala - subjectID – UPVS URI poskytovateľa v IAM.                       |
| Gestor      | String  | Áno            | Gestor elektronického formulára (v GUI MEF sa obvykle uvádza subjectID – UPVS URI gestora v IAM). |

**Názov štruktúry:** FormTemplate 

| **Meno**           | **Typ**               | **Povinnosť**  | **Popis**                                                                                         |
|--------------------|-----------------------|----------------|---------------------------------------------------------------------------------------------------|
| MetaData           | FormTemplateMetaData  | Áno            | Metadata                                                                                          |
| RelatedDocuments   | RelatedDocument[]     | Áno            | Súvisiace dokumenty – obsahuje súčastí elektronického formulára (súvisiace dokumenty) definujúce vzor eFormulára v rámci technológie, v ktorej bol vytvorený (ÚPVS alebo iné).                                                                                                                                       |
| Data               | byte[]                |                | Nepoužívané – pôvodne používané pre uloženie prázdneho vzoru eFormulára.Poznámka: Parameter platný do verzie eForm 1.5. Kvôli spätnej kompatibilite je zahrnutý v schéme.                                                              																				     |

**Názov štruktúry:** FormTemplateMetaData

| **Meno**           | **Typ**          | **Povinnosť**  | **Popis**                                                                                              |
|--------------------|------------------|----------------|--------------------------------------------------------------------------------------------------------| 
| Identifier         | String           | Áno            | Identifikátor vzoru eFormulára                                                                         |
| Title              | String           | Áno            | Názov vzoru                                                                                            |
| Type               | FormTemplateType | Áno            | Typ vzoru                                                                                              |
| Description        | String           | Áno            | Popis vzoru                                                                                            |
| Gestor             | String           | Áno            | Gestor elektronického formulára (v GUI MEF sa obvykle uvádza subjectID – UPVS URI gestora v IAM).      |             
| Publisher          | String           | Áno            | Inštitúcia ktorá žiadosť podala - subjectID – UPVS URI poskytovateľa v IAM.                            |
| Section            | String           |                | Sekcia                                                                                                 |
| Agenda             | String           |                | Agenda                                                                                                 |
| Source             | String           |                | Pôvod vzoru                                                                                            |
| Version            | EFormVersion     | Áno            | Verzia vzoru. Väčšia zmena (schéma) = Major, Menšia zmena (visual, labels) = Minor                     |
| ValidDateFrom      | DateTime         | Áno            | Začiatok platnosti vzoru                                                                               |
| ValidDateTo        | DateTime         |                | Koniec platnosti vzoru                                                                                 |
| Keywords           | String           |                | Kľúčové slová                                                                                          |
| AccessGroup        | String           |                | Prístupová skupina - toto pole sa aktuálne nevypĺňa (uvedené z historických dôvodov). Pre formuláre, ktoré majú uvedenú skupinu prístupu je táto hodnota pri vyhodnocovaní prístupu k formulárom ignorovaná a teda všetky formuláre sú prístupné.                                                                          |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

FormTemplateType: string
-	eForm
-	teForm
-	POSP
-	NOTIFY

**Názov štruktúry:** RelatedDocument

| **Meno** | **Typ**                 | **Povinnosť** | **Popis**                                            |
|----------|-------------------------|---------------|------------------------------------------------------|
| MetaData | RelatedDocumentMetaData | Áno           | Štruktúra popisujúca metadata súvisiaceho dokumentu  |
| Data     | byte[]                  | Áno           | Base64binary dáta súvisiaceho dokumentu v štruktúre a formáte súvisiaceho dokumentu definovanej jeho typom vytvoreného v použitej formulárovej technológii, napr. eFormDesigner.																						   |                                                     

> [!NOTE]
> Modul eForm predstavuje úložisko el. Formulárov pre celý eGovernment a podporuje uloženie rôznych typov formulárov, uložených v zákonom definovanej forme (balík), vytvorených buď technológiou ÚPVS prípadne inou technológiou, ktorú používa ISVS.  

**Názov štruktúry:** RelatedDocumentMetadata

| **Meno**              | **Typ**                 | **Povinnosť**     | **Popis**                                                                 |
| --------------------- | ----------------------- | ----------------- | ------------------------------------------------------------------------- |
| Type                  | String                  | Áno               | Typ súvisiaceho dokumentu (typ súčasti formulára). Možné hodnoty:         |
|                       |                         |                   | CLS_F_XSLT_DEFAULT                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_SGN                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_BODY                                                 |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_SUBJECT                                              |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_BODY                                                |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_SUBJECT                                             |
|                       |                         |                   | CLS_F_XSLT_TXT_SMS                                                        |
|                       |                         |                   | CLS_F_HTML_FORM                                                           |
|                       |                         |                   | CLS_F_XML_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_DCT                                                             |
|                       |                         |                   | CLS_F_XSL_FO                                                              |
|                       |                         |                   | CLS_F_XSLT_RO                                                             |
|                       |                         |                   | CLS_F_DLL_VAL                                                             |
|                       |                         |                   | CLS_F_XML_MTD                                                             |
|                       |                         |                   | CLS_F_XSLT_NAT_EDOC                                                       |
|                       |                         |                   | CLS_F_XSLT_EDOC_NAT                                                       |
|                       |                         |                   | CLS_F_XSLT_HTML                                                           |
|                       |                         |                   | BalikXML                                                                  |
|                       |                         |                   | CLS_F_XML_DEF                                                             |
|                       |                         |                   | CLS_POSP                                                                  |
|                       |                         |                   | POSP_priloha, (táto hodnota sa už nesmie používať v nových formulároch)   |
|                       |                         |                   | POSP, (táto hodnota sa už nesmie používať v nových formulároch)           |
|                       |                         |                   | EFORM_STANDARD_ZIP_PACKAGE                                                |
| Identifier            | String                  | Áno               | Identifikátor vzoru – názov súboru súvisiaceho dokumentu                  |
| Description           | String                  |                   | Popis súvisiaceho dokumentu                                               |
| Language              | String                  | Áno               | Jazyk súvisiaceho dokumentu                                               |

Popis a nastavenia validácií elektronických formulárov pre FIX prostredie je zverejňované na adrese http://portal.upvsfixnew.gov.sk/static/eform/validation/MEF_Business_Validation_rules.csv

Jednotlivé číselníky používané pre validáciu sú uvádzané v popise validácií a ich hodnoty sú zverejnené na adrese vyskladatelnej z URL a čísla číselníka: 

https://portal.upvsfixnew.gov.sk/static/eform/validation/P_[poradové číslo].csv

> [!TIP]
> napr. pre číselník P.24.: https://portal.upvsfixnew.gov.sk/static/eform/validation/P_24.csv

#### 2.1.12.3	Popis správy (Výstupná):

| **Sk-Talk Class**                        | **EFORM_VALIDATE_FORM_TEMPLATE_REPLY_ASYNC_01**                            |
|------------------------------------------|----------------------------------------------------------------------------|
| Popis                                    | Odpoveď na žiadosť o validáciu vzoru eFormulára vo formáte pkg+xml.        |
| Gestor                                   | NASES                                                                      |
| Typ správy                               | Technická                                                                  |
| Predmet správy                           | Validačný report                                                           |
| Odosielateľ                              | UPVS – (MIRRI / ÚPVS)                                                      |
| Adresát                                  | –OVM, PO, FO                                                               |
| Postup spracovania                       | Zobrazenie. Na základe reportu je potrebné opraviť elektronický formulár.  |
| Správa prenášaná v rámci štruktúry       | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“                       |
| Identifikátor elektronického formulára   | http://schemas.gov.sk/form/MEF.Preprocessor.ValidationReport.sk/1.1        |
| Elektronický podpis objektu v class=FORM | Nie                                                                        |
| Modul/Rozhranie/Služba                   | eFORM / UIR / ServiceSkTalk3Token.svc                                      |
| Modul sprostredkujúci komunikáciu        | UPVS – G2G                                                                 |
| Nadväzná správa 1 (odpoveď/notifikácia)  | NA                                                                         |
| Poznámka                                 |                                                                            |

#### 2.1.12.4	Výstupný technický formulár - Odpoveď

- **CLASSNAME:**
- **Output Object:** 

| **Názov**                                                           | **Popis**   |
|---------------------------------------------------------------------|-------------|
| http://schemas.gov.sk/form/MEF.Preprocessor.ValidationReport.sk/1.1 | Viď vyššie  |

#### 2.1.12.5	Príklad volania služby – SKTalk 

- [Príklad SKTalk Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_01)

### 2.1.13	EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_02

Služba je určená na validáciu vzoru eFormulára v **balíku vo formáte .zip** (podľa prílohy č. 1 Vyhlášky 78/2020 Z. z. o štandardoch pre IT VS), pred jeho registráciou v úložisku vzorov. Validácia prebieha odoslaním SKTalk správy na G2G rozhranie ÚPVS, pričom v „body“ časti je vložený určený formulár ValidationEFormPkgPackage.sk. Tento je uložený v rámci Message containera. Výsledný validačný report je zaslaný do eDesku identity odosielateľa žiadosti. Táto služba zasiela rovnaký validačný report (technický formulár) ako pri registrácii formulára, len s odlišným Sk-Talk Class a prípadne predmetom správy.

Použitím služby si môže napríklad dodávateľ implementujúci formulár alebo OVM otestovať, či formulár prejde validáciami a v prípade zistených chýb postupne odstraňovať chyby. 

#### 2.1.13.1	Popis správy (Vstupná):

| **Sk-Talk Class**                        | **EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_02**                                                                                                 |
|------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------|
| Popis                                    | Správa slúži na zaslanie žiadosti o validáciu elektronického formulára v balíku vo formáte .zip pre účely preverenia validity formulára.  |
| Gestor                                   | NASES                                                                                                                                     |
| Typ správy                               | Technická                                                                                                                                 |
| Odosielateľ                              | –OVM, PO, FO                                                                                                                              |
| Adresát                                  | UPVS – eFORM (MIRRI / ÚPVS)                                                                                                               |
| Postup spracovania                       | Validácia podľa definovaných pravidiel                                                                                                    |
| Správa prenášaná v rámci štruktúry       | MessageContainer                                                                                                                          |
| Identifikátor elektronického formulára   | http://data.gov.sk/doc/eform/ValidationEFormPkgPackage.sk/1.0                                                                             |
| Elektronický podpis objektu v class=FORM | nie                                                                                                                                       |
| Modul/Rozhranie/Služba                   | eFORM                                                                                                                                     |
| Modul sprostredkujúci komunikáciu        | NA                                                                                                                                        |
| Nadväzná správa 1 (odpoveď/notifikácia)  | EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_02                                                                                                     |
| Poznámka                                 |                                                                                                                                           |

#### 2.1.13.2	Vstupný technický formulár

- **CLASSNAME:** EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_02
- **Input Object:** _ValidationEFormPkgPackage.sk

| **Názov** | **Typ** | **Povinnosť** | **Popis**  |
|-----------|---------|---------------|------------|
| NA        | NA      | NA            | NA         |

#### 2.1.13.3	Popis správy (Výstupná):

| **Sk-Talk Class**                        | **EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_02**                                  |
|------------------------------------------|----------------------------------------------------------------------------|
| Popis                                    | Odpoveď na žiadosť o validáciu vzoru eFormulára v balíku vo formáte .zip.  |
| Gestor                                   | NASES                                                                      |
| Typ správy                               | Technická                                                                  |
| Predmet správy                           | Validačný report                                                           |
| Odosielateľ                              | UPVS – (MIRRI/ÚPVS)                                                        |
| Adresát                                  | –OVM, PO, FO                                                               |
| Postup spracovania                       | NA                                                                         |
| Správa prenášaná v rámci štruktúry       | SKTALK 3.0 / MessageContainer / ObjectClass = „FORM“                       |
| Identifikátor elektronického formulára   | http://schemas.gov.sk/form/MEF.Preprocessor.ValidationReport.sk/1.1        |
| Elektronický podpis objektu v class=FORM | Nie                                                                        |
| Modul/Rozhranie/Služba                   | eFORM / UIR / ServiceSkTalk3Token.svc                                      |
| Modul sprostredkujúci komunikáciu        | UPVS – G2G                                                                 |
| Nadväzná správa 1 (odpoveď/notifikácia)  | NA                                                                         |
| Poznámka                                 |                                                                            |

#### 2.1.13.4	Výstupný technický formulár - Odpoveď

- **CLASSNAME:**
- **Output Object:**

| **Názov**                                                           | **Popis**   |
|---------------------------------------------------------------------|-------------|
| http://schemas.gov.sk/form/MEF.Preprocessor.ValidationReport.sk/1.1 | Viď vyššie  |

#### 2.1.13.5	Príklad volania služby – SKTalk

- [Príklad SKTalk Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_VALIDATE_FORM_TEMPLATE_ASYNC_02)

### 2.1.14	EFORM_TRANSFORM_FORM_TEMPLATE_ASYNC_01

Služba je určená na vytvorenie vizualizácií z prezentačných schém, ktoré sa nachádzajú v balíku vzoru eFormulára vo formáte pkg+xml. Vo formulári sa podľa manifest.xml identifikujú schémy „sign“, „view“, „screen“, „print“ a „help“, pričom do transformácie sa berie prvá nájdená schéma daného typu. Konkrétne z prvej nájdenej prezentačnej schémy pre jednotlivé účely: 
-	pre podpisovanie (sign), 
-	pre zobrazovanie bez možnosti zmeny vyplnených údajov (view), 
-	pre vypĺňanie (screen), 
-	pre tlač (print),
-	pre nápovedy (help).
 
Súbory môžu byť pomenované podľa transformačnej schémy (napr. “tprint.pdf”, “tscreen.html”).  Transformácia sa vykoná po odoslaní SKTalk správy na G2G rozhranie ÚPVS. Výsledné vizualizácie sú následne zaslané do eDesku identity odosielateľa žiadosti.

Žiadosť o vytvorenie vizualizácie obsahuje štruktúru FormTemplate v body SKTalk správy poďla príkladu. 
Do žiadosti je možné voliteľne uviesť prílohu – dátové .xml vyplnené podľa elektronického formulára, ktoré sa použije pri transformácii. V prípade, že nie je uvedené použije sa data.xml z balíka vzoru formulára.

#### 2.1.14.1	Popis vstupnej správy:

| **Sk-Talk Class**                        | **EFORM_TRANSFORM_FORM_TEMPLATE_ASYNC_01**                         |
|------------------------------------------|--------------------------------------------------------------------|
| Popis                                    | Žiadosť o vytvorenie vizualizácie z prezentačných schém.           |
| Gestor                                   | NASES                                                              |
| Typ správy                               | Technická                                                          |
| Odosielateľ                              | OVM, PO, FO                                                        |
| Adresát                                  | – UPVS – (MIRRI / ÚPVS)                                            |
| Postup spracovania                       | Príjem a spracovanie žiadosti v module eForm.                      |
| Správa prenášaná v rámci štruktúry       | SKTALK 3.0/XML Formulár                                            |
| Identifikátor elektronického formulára   | http://data.gov.sk/doc/eform/TransformationEFormPkgPackage.sk/1.0  |
| Elektronický podpis objektu v class=FORM | Nie                                                                |
| Modul/Rozhranie/Služba                   | eFORM/UIR / ServiceSkTalk3Token.svc                                |
| Modul sprostredkujúci komunikáciu        | UPVS – G2G                                                         |
| Nadväzná správa 1 (odpoveď/notifikácia)  | EFORM_TRANSFORM_FORM_TEMPLATE_REPLY_ASYNC_01                       |
| Vrátené jednotlivé vizualizácie.         |                                                                    |
| Poznámka                                 |                                                                    |

#### 2.1.14.2	Vstupný technický formulár

**Názov štruktúry:** FormTemplate

| **Meno**           | **Typ**               | **Povinnosť**  | **Popis**                                                                                         |
|--------------------|-----------------------|----------------|---------------------------------------------------------------------------------------------------|
| MetaData           | FormTemplateMetaData  | Áno            | Metadata                                                                                          |
| RelatedDocuments   | RelatedDocument[]     | Áno            | Súvisiace dokumenty – obsahuje súčastí elektronického formulára (súvisiace dokumenty) definujúce vzor eFormulára v rámci technológie, v ktorej bol vytvorený (ÚPVS alebo iné).                                                                                                                                       |
| Data               | byte[]                |                | Nepoužívané – pôvodne používané pre uloženie prázdneho vzoru eFormulára.Poznámka: Parameter platný do verzie eForm 1.5. Kvôli spätnej kompatibilite je zahrnutý v schéme.        																																		 |

**Názov štruktúry:** FormTemplateMetaData

| **Meno**           | **Typ**          | **Povinnosť**  | **Popis**                                                                                              |
|--------------------|------------------|----------------|--------------------------------------------------------------------------------------------------------| 
| Identifier         | String           | Áno            | Identifikátor vzoru eFormulára                                                                         |
| Title              | String           | Áno            | Názov vzoru                                                                                            |
| Type               | FormTemplateType | Áno            | Typ vzoru                                                                                              |
| Description        | String           | Áno            | Popis vzoru                                                                                            |
| Gestor             | String           | Áno            | Gestor elektronického formulára (v GUI MEF sa obvykle uvádza subjectID – UPVS URI gestora v IAM).      |             
| Publisher          | String           | Áno            | Inštitúcia ktorá žiadosť podala - subjectID – UPVS URI poskytovateľa v IAM.                            |
| Section            | String           |                | Sekcia                                                                                                 |
| Agenda             | String           |                | Agenda                                                                                                 |
| Source             | String           |                | Pôvod vzoru                                                                                            |
| Version            | EFormVersion     | Áno            | Verzia vzoru. Väčšia zmena (schéma) = Major, Menšia zmena (visual, labels) = Minor                     |
| ValidDateFrom      | DateTime         | Áno            | Začiatok platnosti vzoru                                                                               |
| ValidDateTo        | DateTime         |                | Koniec platnosti vzoru                                                                                 |
| Keywords           | String           |                | Kľúčové slová                                                                                          |
| AccessGroup        | String           |                | Prístupová skupina - toto pole sa aktuálne nevypĺňa (uvedené z historických dôvodov). Pre formuláre, ktoré majú uvedenú skupinu prístupu je táto hodnota pri vyhodnocovaní prístupu k formulárom ignorovaná a teda všetky formuláre sú prístupné.                                                                          |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

FormTemplateType: string
-	eForm
-	teForm
-	POSP
-	NOTIFY

**Názov štruktúry:** RelatedDocument

| **Meno** | **Typ**                 | **Povinnosť** | **Popis**                                            |
|----------|-------------------------|---------------|------------------------------------------------------|
| MetaData | RelatedDocumentMetaData | Áno           | Štruktúra popisujúca metadata súvisiaceho dokumentu  |
| Data     | byte[]                  | Áno           | Base64binary dáta súvisiaceho dokumentu v štruktúre a formáte súvisiaceho dokumentu definovanej jeho typom vytvoreného v použitej formulárovej technológii, napr. eFormDesigner.																						   |                                                     

**Názov štruktúry:** RelatedDocumentMetadata

| **Meno**              | **Typ**                 | **Povinnosť**     | **Popis**                                                                 |
| --------------------- | ----------------------- | ----------------- | ------------------------------------------------------------------------- |
| Type                  | String                  | Áno               | Typ súvisiaceho dokumentu (typ súčasti formulára). Možné hodnoty:         |
|                       |                         |                   | CLS_F_XSLT_DEFAULT                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_SGN                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_BODY                                                 |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_SUBJECT                                              |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_BODY                                                |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_SUBJECT                                             |
|                       |                         |                   | CLS_F_XSLT_TXT_SMS                                                        |
|                       |                         |                   | CLS_F_HTML_FORM                                                           |
|                       |                         |                   | CLS_F_XML_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_DCT                                                             |
|                       |                         |                   | CLS_F_XSL_FO                                                              |
|                       |                         |                   | CLS_F_XSLT_RO                                                             |
|                       |                         |                   | CLS_F_DLL_VAL                                                             |
|                       |                         |                   | CLS_F_XML_MTD                                                             |
|                       |                         |                   | CLS_F_XSLT_NAT_EDOC                                                       |
|                       |                         |                   | CLS_F_XSLT_EDOC_NAT                                                       |
|                       |                         |                   | CLS_F_XSLT_HTML                                                           |
|                       |                         |                   | BalikXML                                                                  |
|                       |                         |                   | CLS_F_XML_DEF                                                             |
|                       |                         |                   | CLS_POSP                                                                  |
|                       |                         |                   | POSP_priloha, (táto hodnota sa už nesmie používať v nových formulároch)   |
|                       |                         |                   | POSP, (táto hodnota sa už nesmie používať v nových formulároch)           |
|                       |                         |                   | EFORM_STANDARD_ZIP_PACKAGE                                                |
| Identifier            | String                  | Áno               | Identifikátor vzoru – názov súboru súvisiaceho dokumentu                  |
| Description           | String                  |                   | Popis súvisiaceho dokumentu                                               |
| Language              | String                  | Áno               | Jazyk súvisiaceho dokumentu                                               |

#### 2.1.14.3	Popis správy (Výstupná):

| **Sk-Talk Class**                        | **EFORM_TRANSFORM_FORM_TEMPLATE_REPLY_ASYNC_01**                           |
|------------------------------------------|----------------------------------------------------------------------------|
| Popis                                    | Odpoveď na žiadosť o vytvorenie vizualizácie z prezentačných schém vzoru.  |
| Gestor                                   | NASES                                                                      |
| Typ správy                               | Technická                                                                  |
| Odosielateľ                              | UPVS – eFORM (MIRRI/ÚPVS)                                                  |
| Adresát                                  | –OVM, PO, FO                                                               |
| Postup spracovania                       | NA                                                                         |
| Správa prenášaná v rámci štruktúry       | SKTALK 3.0/MessageContainer/ObjectClass = „ATTACHMENT“                     |
| Identifikátor elektronického formulára   | http://schemas.gov.sk/form/G2G.InformationMessage/1.3                      |
| Elektronický podpis objektu v class=FORM | Nie                                                                        |
| Modul/Rozhranie/Služba                   | eFORM/UIR/ServiceSkTalk3Token.svc                                          |
| Modul sprostredkujúci komunikáciu        | UPVS – G2G                                                                 |
| Nadväzná správa 1 (odpoveď/notifikácia)  | NA                                                                         |
| Poznámka                                 |                                                                            |

#### 2.1.14.4	Výstupný technický formulár - Odpoveď

- **CLASSNAME:** EFORM_TRANSFORM_FORM_TEMPLATE_REPLY_ASYNC_01
- **Output Object:**

| **Názov**    | **Popis**  |
|--------------|------------|
| FormTemplate | NA         |

#### 2.1.14.5	Príklad– SKTalk

- [Príklady SKTalk](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_TRANSFORM_FORM_TEMPLATE_ASYNC_01)

### 2.1.15	EFORM_TRANSFORM_FORM_TEMPLATE_ASYNC_02

Služba je určená na vytvorenie vizualizácií z transformačných súborov, ktoré sa nachádzajú v balíku vzoru eFormulára v štandardnom formáte .zip podľa Vyhlášky č. 78/2020 Z. z. o štandardoch pre IT VS. Konkrétne z prvej nájdenej prezentačnej schémy pre jednotlivé účely: 
-	pre podpisovanie (sign), 
-	pre zobrazovanie bez možnosti zmeny vyplnených údajov (view), 
-	pre vypĺňanie (screen), pre tlač (print)
-	pre nápovedy (help).

Transformácia prebieha odoslaním SKTalk správy na G2G rozhranie ÚPVS. Výsledné vizualizácie sú zaslané do eDesku identity odosielateľa žiadosti.

Žiadosť o vytvorenie vizualizácie obsahuje štruktúru:
„http://data.gov.sk/doc/eform/TransformationEFormPkgPackage.sk/1.0“ umiestnenú v Message containeri v body SKTalk správy podľa príkladu a .zip balík formulára umiestnený v Message containeri ako prílohu. Do prílohy je zároveň možné vložiť aj XML súbor vyplnený podľa elektronického formulára, ktorý bude použitý pri transformácii pre naplnenie údajov do vizualizácie.

#### 2.1.15.1	Popis správy (Vstupná):

| **Sk-Talk Class**                        | **EFORM_TRANSFORM_FORM_TEMPLATE_ASYNC_02**                         |
|------------------------------------------|--------------------------------------------------------------------|
| Popis                                    | Vytvorenie vizualizácie z prezentačných schém                      |
| Gestor                                   | NASES                                                              |
| Typ správy                               | Technická                                                          |
| Odosielateľ                              | OVM, PO, FO                                                        |
| Adresát                                  | ÚPVS – (MIRRI/ÚPVS)                                                |
| Postup spracovania                       | Príjem a spracovanie žiadosti v module eForm.                      |
| Správa prenášaná v rámci štruktúry       | SKTALK 3.0/MessageContainer/ObjectClass = „FORM“                   |
| Identifikátor elektronického formulára   | http://data.gov.sk/doc/eform/TransformationEFormPkgPackage.sk/1.0  |
| Elektronický podpis objektu v class=FORM | Nie                                                                |
| Modul/Rozhranie/Služba                   | eFORM/UIR/ServiceSkTalk3Token.svc                                  |
| Modul sprostredkujúci komunikáciu        | UPVS – G2G                                                         |
| Nadväzná správa 1 (odpoveď/notifikácia)  | EFORM_TRANSFORM_FORM_TEMPLATE_REPLY_ASYNC_02                       |
| Poznámka                                 |                                                                    |

#### 2.1.15.2	Popis správy (Výstupná):

| **Sk-Talk Class**                        | **EFORM_TRANSFORM_FORM_TEMPLATE_REPLY_ASYNC_02**                                  |
|------------------------------------------|-----------------------------------------------------------------------------------|
| Popis                                    | Odpoveď na žiadosť o vytvorenie vizualizácie z prezentačných schém balíka vzoru.  |
| Gestor                                   | NASES                                                                             |
| Typ správy                               | Technická                                                                         |
| Odosielateľ                              | UPVS – eFORM (MIRRI/ÚPVS)                                                         |
| Adresát                                  | –OVM, PO, FO                                                                      |
| Postup spracovania                       | NA                                                                                |
| Správa prenášaná v rámci štruktúry       | SKTALK 3.0 / MessageContainer / ObjectClass = „ATTACHMENT“                        |
| Identifikátor elektronického formulára   | http://schemas.gov.sk/form/G2G.InformationMessage/1.3                             |
| Elektronický podpis objektu v class=FORM | Nie                                                                               |
| Modul/Rozhranie/Služba                   | eFORM / UIR / ServiceSkTalk3Token.svc                                             |
| Modul sprostredkujúci komunikáciu        | UPVS – G2G                                                                        |
| Nadväzná správa 1 (odpoveď/notifikácia)  | NA                                                                                |
| Poznámka                                 |                                                                                   |

#### 2.1.15.3	Výstupný technický formulár - Odpoveď

- **CLASSNAME:**
- **Output Object:**

| **Názov**                                             | **Popis**     |
|-------------------------------------------------------|---------------|
| http://schemas.gov.sk/form/G2G.InformationMessage/1.3 | Viď IM – G2G  |

#### 2.1.15.4	Príklad volania služby – SKTalk

- [Príklady SKTalk Request/Respose](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/EFORM_TRANSFORM_FORM_TEMPLATE_ASYNC_02)

### 2.1.16	Vstupný formulár pre asynchrónne žiadosti 

Pre odosielanie žiadostí na MEF sa používa formulár upvs.eform.EFormRequest, ktorý je uvedený v tomto dokumente a je zaregistrovaný na príslušných prostrediach ÚPVS. V rámci eformulára sú jednotlivé polia povinné. Formulár slúži ako sprievodný list pre samotnú registráciu, tj jeho obsah je zobrazovaný v rámci evidencie žiadostí na vloženie, resp. zmenu eFormulára pre výstupnú kontrolu ÚPVS. Príklad vyplneného eFormulára ako i jeho schéma je uvedená nižšie. Aktuálna verzia daného eFormulára je zároveň aj zaregistrovaná v rámci modulu MEF.

```

<EFormRequest xmlns="http://schemas.gov.sk/form/upvs.eform.EFormRequest/1.0">
	<Title>Názov žiadosti - povinné vyplniť </Title>
	<Description>Popis žiadosti - povinné vyplniť</Description>
	<Publisher>UPVS ID inštitúcie za ktorú sa eformulár registruje resp mení – povinné</Publisher>
	<Gestor>UPVS ID autora poslednej zmeny – povinné </Gestor>
</EFormRequest>


```

- [Podklady](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/Vstupn%C3%BD%20formul%C3%A1r%20pre%20asynchr%C3%B3nne%20%C5%BEiadosti) 

### 2.1.17	Asynchrónne volané služby eForm – XML Schémy

- [XML schémy](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/XML%20Sch%C3%A9my/Vstupn%C3%A9%20sch%C3%A9my)

### 2.1.18	Asynchrónne služby eForm – výstupné XML Schémy

- [Výstupné schémy](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Asynchr%C3%B3nne%20slu%C5%BEby%20-%20Rozhranie%20UIR%20a%20G2G/XML%20Sch%C3%A9my/V%C3%BDstupn%C3%A9%20sch%C3%A9my)

# 3	Integrácia na eFORM cez Externú zbernicu - USR

Detaily k volaniu služieb publikovaných na externej zbernici (G2G - USR) je možné nájsť v IM – G2G v kapitole venovanej Externej Zbernici – USR. 

## 3.1	Externá zbernica – G2G (USR)

Externá zbernica slúži na sprostredkovanie synchrónnej komunikácie zo systémov ISVS do ÚPVS. Poskytuje univerzálne synchrónne rozhranie – USR pre volanie služieb ÚPVS na spoločnej adrese s definíciami komunikačných štruktúr, vďaka čomu umožní rýchle a jednoduché prepojenie modulov navzájom a udržovanie týchto prepojení po prípadných zmenách komunikačných adries a štruktúr.

Externá zbernica poskytuje štandardizované komunikačné rozhranie založené na webových službách SOAP a REST.

 ![Schéma komunikácie](https://github.com/NASES-Slovakia/integration_manuals/blob/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Images/Sch%C3%A9ma%20vz%C3%A1jomnej%20komunik%C3%A1cie%20modulov%20prostredn%C3%ADctvom%20externej%20zbernice.png)

Schéma vzájomnej komunikácie modulov prostredníctvom externej zbernice

Externá zbernica poskytuje informácie o všetkých dostupných službách a ich rozhraniach potrebné na zavolanie služby. Volania služieb prebiehajú prostredníctvom externej zbernice ktorá vykoná validáciu správnosti vstupujúcich parametrov, logovanie volania a presmerovanie komunikácie na volanú službu.

## 3.2	Volanie služieb eFORM cez externú zbernicu

Na externej zbernici je publikovaná sada služieb bežiaca pod systémom eFLCM, ktorá je implementovaná v technológii Microsoft SharePoint. Táto sada služieb je bližšie popísaná v kapitole 3.3. Pri publikovaní služieb na externej zbernici prichádza k zmene vstupných atribútov služby na objekt. Parametre sa nemenia mení sa len formát ich zápisu pri volaní. Spôsob tohto volania je popísaný v integračnej dokumentácii modulu Externá zbernica – USR.

## 3.3	eForm webové služby (WS) publikované na Externej zbernici

Rozhranie integračného komponentu modulu eForm poskytuje eForm webové služby zabezpečujúce sadu základných služieb pre získanie vzoru formulára, jeho metadata a súvisiacich dokumentov. 

Súbor eForm webových služieb slúži na: 

-	získanie metadát vzoru eFormulára,
-	získanie zoznamu súvisiacich dokumentov vzoru eFormulára,
-	získanie súvisiaceho dokumentu vzoru eFormulára,
-	vyhľadanie zoznamu vzorov eformulárov na základe kritérií,
-	získanie prázdneho vzoru eFormulára,
-	získanie vizualizácie elektronického dokumentu vo formáte .pdf,
-	získanie vizualizácie elektronického dokumentu vo formáte .pdf na základe vstupných dát,
-	prihlásenie a odhlásenie sa k odberu informácií o zmenách v úložisku vzorov EFLCM,
-	zmena výberových kritérií a zmena endpointov pre prihlásený odber informácií eFLCM,
-	získanie vizualizácie na základe typu súvisiaceho dokumentu a jazyka. 

Pre podporu výnosu o štandardoch ISVS boli zapracované nové služby pre:
-	poskytnutie vzoru eFormulára vo formáte .zip,
-	poskytnutie vzoru eFormulára vo formáte XML,
-	poskytnutie súboru meta.xml zo vzoru eFormulára,
-	poskytnutie súboru attachments.xml zo vzoru eFormulára,
-	poskytnutie súboru manifest.xml zo vzoru eFormulára,
-	poskytnutie jednotlivých súborov zo vzoru eFormulára.

Použité metódy webových služieb s krátkym popisom: 

| **** | **Názov metódy**                       | **CLASS na IZ**                                         | **Popis** |
|------|----------------------------------------|---------------------------------------------------------|----------------------------------------------------------------------------------------------------|
| 1.   | GetFormTemplateMetaData                | eForm_GetFormTemplateMetaData_SOAP_V_1_0                | Získanie metadát vzoru eFormulára na základe identifikátora vzoru a verzie.                        |
| 2.   | GetRelatedDocumentList                 | eForm_GetRelatedDocumentList_SOAP_V_1_0                 | Získanie zoznamu súvisiacich dokumentov vzoru eFormulára na základe identifikátora vzoru a verzie  |
| 3.   | GetRelatedDocument                     | eForm_GetRelatedDocument_SOAP_V_1_0                     | Získanie súvisiaceho dokumentu vzoru eFormulára na základe identifikátora vzoru, jeho verzie a názvu/identifikátora súvisiaceho dokumentu.        																																			                        |
| 4.   | GetFormTemplateStatus                  | eForm_GetFormTemplateStatus_SOAP_V_1_0                  | Získanie stavu vzoru eFormulára na základe identifikátora vzoru a jeho verzie.                     |   
| 5.   | FindFormTemplates                      | eForm_FindFormTemplates_SOAP_V_1_0                      | Vyhľadanie vzorov eFormulárov na základe kritérií.                                                 |  
| 6.   | GetEDocFromXML                         | eForm_GetEDocFromXML_SOAP_V_1_0                         | Získanie vizualizácie elektronického dokumentu vo formáte PDF na základe vstupných dát.            |  
| 7.   | GetEDoc                                | eForm_GetEDoc_SOAP_V_1_0                                | Získanie vizualizácie elektronického dokumentu vo formáte PDF na základe prázdneho vzoru eFormulára          																																															|
| 8.   | GetEmptyEForm                          | eForm_GetEmptyEForm_SOAP_V_1_0                          | Získanie prázdneho vzoru eFormulára.														       |
| 9.   | SubscribeForChanges                    | eForm_SubscribeForChanges_SOAP_V_1_0                    | Prihlásenie sa k odberu zmien vybranej množiny vzorov na základe výberových kritérií.              |
| 10.  | UnsubscribeForChanges                  | eForm_UnsubscribeForChanges_SOAP_V_1_0                  | Odhlásenie sa od odberu zmien.																	   |  
| 11.  | ChangeSubscriberSearchCriteria         | eForm_ChangeSubscriberSearchCriteria_SOAP_V_1_0         | Zmena výberových kritérií pre aktívny odber zmien.                                                 |
| 12.  | ChangeSubscriberEndpointUrl            | eForm_ChangeSubscriberEndpointUrl_SOAP_V_1_0            | Zmena endpointu pre aktívny odber zmien.          												   |
| 13.  | GetSubscriberSearchCriteria            | eForm_GetSubscriberSearchCriteria_SOAP_V_1_0            | Vráť nastavené výberové kritériá pre aktívny odber zmien          								   |
| 14.  | GetSubscriberEndpointUrl               | eForm_GetSubscriberEndpointUrl_SOAP_V_1_0               | Vráť nastavenú EndpointURL pre aktívny odber zmien.                                                |
| 15.  | GetRelatedDocumentByType               | eForm_GetRelatedDocumentByType_SOAP_V_1_0               | Výstupom metódy je súvisiaci dokument vzoru, získaný na základe jeho typu a jazyka.                |      
| 16.  | TransformRelatedDocument               | eForm_TransformRelatedDocument_SOAP_V_1_0               | Výstupom metódy transformácia súvisiacich dokumentov. Identifikátory týchto sú ako vstupné parametre metódy.          																																																|
| 17.  | TransformRelatedDocumentFromXML        | eForm_TransformRelatedDocumentFromXML_SOAP_V_1_0        | Výstupom metódy je transformácia vstupného XML na základe parametrom identifikovaného súvisiaceho dokumentu. Tento musí označovať vizualizáciu.          																																					     |
| 18.  | TransformRelatedDocumentByType         | eForm_TransformRelatedDocumentByType_SOAP_V_1_0         | Výstupom metódy je transformácia súvisiaceho dokumentu majúceho character vzoru. Tento musí byť identifikovaný s pomocou typu a jazyka.  Transformácia sa vykoná s pomocou vizualizácie, táto je rovnako ako vzor identifikovaná prostredníctvom typu a jazyka.          									   |
| 19.  | TransformRelatedDocumentFromXMLByType  | eForm_TransformRelatedDocumentFromXMLByType_SOAP_V_1_0  | Výstupom metódy je transformácia vstupného XML súboru voči vizualizácii identifikovanej typom a jazykom.          																																															   |
| 20.  | GetFormTemplate                        | eForm_GetFormTemplate_SOAP_V_1_0                        | Výstupom je vzor eFormulára, vrátane metadata vzoru a jeho príloh.          					   |
| 21.  | SetFormTemplateStatus                  | eForm_SetFormTemplateStatus _SOAP_V_1_0                 | Nastavenie stavu vzoru eFormulára na základe jeho identifikátora                                   |
| 22.  | getFilledFormTemplate                  | eForm_GetFilledFormTemplate _SOAP_V_1_0                 | Získanie predvyplneného vzoru eFormulára                                                           |
| 23.  | GetEFormPackage                        | eForm_GetEFormPackage_SOAP_V_1_0                        | Poskytnutie balíku vzoru eFormulára vo formáte XML a ZIP podľa Vyhlášky č. 78/2020 Z. z. o štandardoch pre IT VS          																																														          |
| 24.  | GetEFormTemplateManifestXML            | eForm_GetEFormTemplateManifestXML_SOAP_V_1_0            | Poskytnutie súboru manifest.xml zo vzoru eFormulára                                                |
| 25.  | GetEFormTemplateAttachmentsXML         | eForm_GetEFormTemplateAttachmentsXML_SOAP_V_1_0         | Poskytnutie súboru attachments.xml zo vzoru eFormulára.                                            |
| 26.  | GetEFormTemplateMetaXML                | eForm_GetEFormTemplateMetaXML_SOAP_V_1_0                | Poskytnutie súboru meta.xml zo vzoru eFormulára                                                    |
| 27.  | GetEFormPackageArtefact                | eForm_GetEFormPackageArtefact_SOAP_V_1_0                | Poskytnutie súvisiaceho dokumentu zo vzoru eFormulára.                                             |

> ![NOTE]
> všetky príklady volaní a odpovedí uvedené v tejto kap. majú ilustračnú povahu

### 3.3.1	GetFormTemplateMetaData

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov

- **Názov metódy:** GetFormTemplateMetaData

**Input Object:** GetFormTemplateMetaDataReq

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**  |
|--------------|----------------|---------------|------------|
| FormTemplate | FormTemplateID | Áno           | ID vzoru   |

**Output Object:** Output Object – GetFormTemplateMetaDataRes

| **Názov** | **Typ**              | **Povinnosť** | **Popis**                                      |
|-----------|----------------------|---------------|------------------------------------------------|
| MetaData  | FormTemplateMetaData |               | Štruktúra popisujúca metadáta vzoru eFormulára |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateMetaData

| **Meno**           | **Typ**          | **Povinnosť**  | **Popis**                                                                                              |
|--------------------|------------------|----------------|--------------------------------------------------------------------------------------------------------| 
| Identifier         | String           | Áno            | Identifikátor vzoru eFormulára                                                                         |
| Title              | String           | Áno            | Názov vzoru                                                                                            |
| Type               | FormTemplateType | Áno            | Typ vzoru                                                                                              |
| Description        | String           | Áno            | Popis vzoru                                                                                            |
| Gestor             | String           | Áno            | Gestor elektronického formulára (v GUI MEF sa obvykle uvádza subjectID – UPVS URI gestora v IAM).      |             
| Publisher          | String           | Áno            | Inštitúcia ktorá žiadosť podala - subjectID – UPVS URI poskytovateľa v IAM.                            |
| Section            | String           |                | Sekcia                                                                                                 |
| Agenda             | String           |                | Agenda                                                                                                 |
| Source             | String           |                | Pôvod vzoru                                                                                            |
| Version            | EFormVersion     | Áno            | Verzia vzoru. Väčšia zmena (schéma) = Major, Menšia zmena (visual, labels) = Minor                     |
| ValidDateFrom      | DateTime         | Áno            | Začiatok platnosti vzoru                                                                               |
| ValidDateTo        | DateTime         |                | Koniec platnosti vzoru                                                                                 |
| Keywords           | String           |                | Kľúčové slová                                                                                          |
| AccessGroup        | String           |                | Prístupová skupina - toto pole sa aktuálne nevypĺňa (uvedené z historických dôvodov). Pre formuláre, ktoré majú uvedenú skupinu prístupu je táto hodnota pri vyhodnocovaní prístupu k formulárom ignorovaná a teda všetky formuláre sú prístupné.                                                                          |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

FormTemplateType: string
-	eForm
-	teForm
-	POSP
-	NOTIFY

#### 3.3.1.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000798

#### 3.3.1.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetFormTemplateMetaData)

### 3.3.2	GetRelatedDocumentList

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

 **Názov metódy:** GetRelatedDocumentList

**Input Object:** GetRelatedDocumentListReq

| **Meno**        | **Typ**        | **Povinnosť** | **Popis**                                  |
|-----------------|----------------|---------------|--------------------------------------------|
| FormTemplate    | FormTemplateID | Áno           | ID vzoru                                   |

**Output Object:** GetRelatedDocumentListRes

| **Meno**        | **Typ**         | **Povinnosť** | **Popis**                                                             |
|-----------------|-----------------|---------------|-----------------------------------------------------------------------|
| RelatedDocument | RelatedDocument |               | Štruktúra obsahujúca metadata súvisiaceho dokumentu vzoru eFormulára  |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** RelatedDocumentMetadata

| **Meno**              | **Typ**                 | **Povinnosť**     | **Popis**                                                                 |
| --------------------- | ----------------------- | ----------------- | ------------------------------------------------------------------------- |
| Type                  | String                  | Áno               | Typ súvisiaceho dokumentu (typ súčasti formulára). Možné hodnoty:         |
|                       |                         |                   | CLS_F_XSLT_DEFAULT                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_SGN                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_BODY                                                 |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_SUBJECT                                              |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_BODY                                                |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_SUBJECT                                             |
|                       |                         |                   | CLS_F_XSLT_TXT_SMS                                                        |
|                       |                         |                   | CLS_F_HTML_FORM                                                           |
|                       |                         |                   | CLS_F_XML_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_DCT                                                             |
|                       |                         |                   | CLS_F_XSL_FO                                                              |
|                       |                         |                   | CLS_F_XSLT_RO                                                             |
|                       |                         |                   | CLS_F_DLL_VAL                                                             |
|                       |                         |                   | CLS_F_XML_MTD                                                             |
|                       |                         |                   | CLS_F_XSLT_NAT_EDOC                                                       |
|                       |                         |                   | CLS_F_XSLT_EDOC_NAT                                                       |
|                       |                         |                   | CLS_F_XSLT_HTML                                                           |
|                       |                         |                   | BalikXML                                                                  |
|                       |                         |                   | CLS_F_XML_DEF                                                             |
|                       |                         |                   | CLS_POSP                                                                  |
|                       |                         |                   | POSP_priloha, (táto hodnota sa už nesmie používať v nových formulároch)   |
|                       |                         |                   | POSP, (táto hodnota sa už nesmie používať v nových formulároch)           |
|                       |                         |                   | EFORM_STANDARD_ZIP_PACKAGE                                                |
| Identifier            | String                  | Áno               | Identifikátor vzoru – názov súboru súvisiaceho dokumentu                  |
| Description           | String                  |                   | Popis súvisiaceho dokumentu                                               |
| Language              | String                  | Áno               | Jazyk súvisiaceho dokumentu                                               |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

#### 3.3.2.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000798

#### 3.3.2.2	Príklad volania služby - SOAP

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetRelatedDocumentList)

### 3.3.3	GetRelatedDocument

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov

- **Názov metódy:** GetRelatedDocument

**Input Object:** GetRelatedDocumentReq

| **Meno**        | **Typ**        | **Povinnosť** | **Popis**                                  |
|-----------------|----------------|---------------|--------------------------------------------|
| FormTemplate    | FormTemplateID | Áno           | ID vzoru                                   |
| RelatedDocument | String         | Áno           | Identifikátor/názov súvisiaceho dokumentu  |

**Output Object:** GetRelatedDocumentRes

| **Meno**        | **Typ**         | **Povinnosť** | **Popis**                                                                                |
|-----------------|-----------------|---------------|------------------------------------------------------------------------------------------|
| FormTemplate    | FormTemplateID  |               | ID vzoru                                                                                 |
| RelatedDocument | RelatedDocument |               | Štruktúra obsahujúca metadata súvisiaceho dokumentu a jeho dáta vo formáte base64binary  |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** RelatedDocument

| **Meno** | **Typ**                 | **Povinnosť** | **Popis**                                            |
|----------|-------------------------|---------------|------------------------------------------------------|
| MetaData | RelatedDocumentMetaData | Áno           | Štruktúra popisujúca metadáta súvisiaceho dokumentu  |
| Data     | byte[]                  | Áno           | Base64binary dáta súvisiaceho dokumentu              |

**Názov štruktúry:** RelatedDocumentMetadata

| **Meno**              | **Typ**                 | **Povinnosť**     | **Popis**                                                                 |
| --------------------- | ----------------------- | ----------------- | ------------------------------------------------------------------------- |
| Type                  | String                  | Áno               | Typ súvisiaceho dokumentu (typ súčasti formulára). Možné hodnoty:         |
|                       |                         |                   | CLS_F_XSLT_DEFAULT                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_SGN                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_BODY                                                 |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_SUBJECT                                              |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_BODY                                                |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_SUBJECT                                             |
|                       |                         |                   | CLS_F_XSLT_TXT_SMS                                                        |
|                       |                         |                   | CLS_F_HTML_FORM                                                           |
|                       |                         |                   | CLS_F_XML_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_DCT                                                             |
|                       |                         |                   | CLS_F_XSL_FO                                                              |
|                       |                         |                   | CLS_F_XSLT_RO                                                             |
|                       |                         |                   | CLS_F_DLL_VAL                                                             |
|                       |                         |                   | CLS_F_XML_MTD                                                             |
|                       |                         |                   | CLS_F_XSLT_NAT_EDOC                                                       |
|                       |                         |                   | CLS_F_XSLT_EDOC_NAT                                                       |
|                       |                         |                   | CLS_F_XSLT_HTML                                                           |
|                       |                         |                   | BalikXML                                                                  |
|                       |                         |                   | CLS_F_XML_DEF                                                             |
|                       |                         |                   | CLS_POSP                                                                  |
|                       |                         |                   | POSP_priloha, (táto hodnota sa už nesmie používať v nových formulároch)   |
|                       |                         |                   | POSP, (táto hodnota sa už nesmie používať v nových formulároch)           |
|                       |                         |                   | EFORM_STANDARD_ZIP_PACKAGE                                                |
| Identifier            | String                  | Áno               | Identifikátor vzoru – názov súboru súvisiaceho dokumentu                  |
| Description           | String                  |                   | Popis súvisiaceho dokumentu                                               |
| Language              | String                  | Áno               | Jazyk súvisiaceho dokumentu                                               |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

#### 3.3.3.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000798
-	06000796

#### 3.3.3.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetRelatedDocument)

### 3.3.4	GetFormTemplateStatus

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** GetFormTemplateStatus

**Input Object:** GetFormTemplateStatusReq

| **Meno**     | **Typ**        | **Povinnosť** | **Popis** |
|--------------|----------------|---------------|-----------|
| FormTemplate | FormTemplateID | Áno           | ID vzoru  |

**Output Object:** GetFormTemplateStatusRes

| **Meno**     | **Typ**        | **Povinnosť** | **Popis**                |
|--------------|----------------|---------------|--------------------------|
| FormTemplate | FormTemplateID |               | ID vzoru                 |
| FormStatus   | string         |               | Stav vzoru eFormulára.   |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

#### 3.3.4.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000798

#### 3.3.4.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetFormTemplateStatus)

### 3.3.5	FindFormTemplates

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov

- **Názov metódy:** FindFormTemplates

**Input Object:** FindFormTemplatesReq

| **Meno** | **Typ**        | **Povinnosť** | **Popis**              |
|----------|----------------|---------------|------------------------|
| Criteria | SearchCriteria |               | Vyhľadávacie kritériá  |

**Output Object:** FindFormTemplatesRes

| **Meno**      | **Typ**          | **Povinnosť** | **Popis**                                |
|---------------|------------------|---------------|------------------------------------------|
| FormTemplates | FormTemplateID[] |               | Zoznam ID vyhľadaných vzorov eFormulárov |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** SearchCriteria

| **Meno**     | **Typ**          | **Povinnosť** | **Popis**                                                                    |
|--------------|------------------|---------------|------------------------------------------------------------------------------|
| FormTemplate | FormTemplateID   |               | Identifikácia vzoru                                                          |
| Type         | FormTemplateType |               | Typ vzoru                                                                    |
| Title        | String           |               | Názov vzoru                                                                  |
| Description  | String           |               | Popis vzoru                                                                  |
| Publisher    | String           |               | Inštitúcia ktorá žiadosť podala - subjectID – UPVS URI poskytovateľa v IAM   |
| FreeText     | String           |               | Voľný text, vyhľadáva naprieč atribútmi.                                     |
| Keywords     | String           |               | Text sa vyhľadáva v kľúčových slovách vzoru.                                 |

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

FormTemplateType: string
-	eForm
-	teForm
-	POSP
-	NOTIFY

#### 3.3.5.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000999

#### 3.3.5.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/FindFormTemplates)

### 3.3.6	GetEDoc

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov

- **Názov metódy:** GetEDoc

**Input Object:** GetEDocReq

| **Meno**     | **Typ**        | **Povinnosť** | **Popis** |
|--------------|----------------|---------------|-----------|
| FormTemplate | FormTemplateID | Áno           | ID vzoru  |

**Output Object:** GetEDocRes

| **Meno**     | **Typ**        | **Povinnosť** | **Popis**                                                                                             |
|--------------|----------------|---------------|-------------------------------------------------------------------------------------------------------|
| FormTemplate | FormTemplateID |               | ID vzoru                                                                                              |
| EDoc         | EDocument      |               | Štruktúra obsahuje názov dokumentu a dáta elektronického dokumentu  vizualizovaného vo formáte .pdf.  |

> [!NOTE]
> *Služba do transformácie použije XML a XSLFO dokumenty v jazyku formulára. Ak dokument v jazyku formulára neexistuje, služba hľadá dokument v jazyku „sk“. Ak taký dokument neexistuje, služba v transformácii použije prvý nájdený dokument daného typu.

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

**Názov štruktúry:** EDocument

| **Meno** | **Typ** | **Povinnosť** | **Popis**                                                                                                  |
|----------|---------|---------------|------------------------------------------------------------------------------------------------------------|
| Title    | string  |               | Názov elektronického dokumentu s príponou .pdf.                                                            |
| Data     | byte[]  |               | Dáta elektronického dokumentu vizualizovaného vo formáte .pdf. Kódovanie prenášaných dát je base64Binary.  |

#### 3.3.6.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000999
-	06000798
-	06000796
-	06000787

#### 3.3.6.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetEDoc)

### 3.3.7	GetEDocFromXML

Služba transformuje XML údaje vyplnené podľa elektronického formulára do .pdf pomocou tlačovej prezentačnej schémy.

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov

- **Názov metódy:** GetEDocFromXML

**Input Object:** GetEDocFromXMLReq

| **Meno**     | **Typ**        | **Povinnosť** | **Popis**                                                   |
|--------------|----------------|---------------|-------------------------------------------------------------|
| FormTemplate | FormTemplateID | Áno           | ID vzoru                                                    |
| Data         | byte[]         | Áno           | Base64Binary kódované XML dáta elektronického formulára.    |

**Output Object:** GetEDocFromXMLRes

| **Meno**     | **Typ**        | **Povinnosť** | **Popis**                                                                                            |
|--------------|----------------|---------------|------------------------------------------------------------------------------------------------------|
| FormTemplate | FormTemplateID |               | ID vzoru                                                                                             |
| EDoc         | EDocument      |               | Štruktúra obsahuje názov dokumentu a dáta elektronického dokumentu vizualizovaného vo formáte .pdf.  |

> [!NOTE]
> *Služba do transformácie použije XSLFO v jazyku formulára. Ak dokument v jazyku formulára neexistuje, služba hľadá dokument v jazyku „sk“. Ak taký dokument neexistuje, služba v transformácii použije prvý nájdený dokument daného typu.

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

**Názov štruktúry:** EDocument

| **Meno** | **Typ** | **Povinnosť** | **Popis**                                                                                                  |
|----------|---------|---------------|------------------------------------------------------------------------------------------------------------|
| Title    | string  |               | Názov elektronického dokumentu s príponou .pdf.                                                            |
| Data     | byte[]  |               | Dáta elektronického dokumentu vizualizovaného vo formáte .pdf. Kódovanie prenášaných dát je base64Binary.  |

#### 3.3.7.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000999
-	06000798
-	06000796
-	06000787

#### 3.3.7.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetEDocFromXML)

### 3.3.8	GetEmptyEForm

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** GetEmptyEForm 

**Input Object:** GetEmptyEFormReq

| **Meno**     | **Typ**        | **Povinnosť** | **Popis** |
|--------------|----------------|---------------|-----------|
| FormTemplate | FormTemplateID | Áno           | ID vzoru  |

**Output Object:** Output Object – GetEmptyEFormRes

| **Meno**        | **Typ**         | **Povinnosť** | **Popis**                                                                                           |
|-----------------|-----------------|---------------|-----------------------------------------------------------------------------------------------------|
| FormTemplate    | FormTemplateID  |               | ID vzoru                                                                                            |
| RelatedDocument | RelatedDocument |               | Štruktúra obsahuje metadáta prázdneho vzoru eFormuláru a jeho dáta. Dáta sú kódované base64Binary.  |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

**Názov štruktúry:** RelatedDocument

| **Meno** | **Typ**                 | **Povinnosť** | **Popis**                                            |
|----------|-------------------------|---------------|------------------------------------------------------|
| MetaData | RelatedDocumentMetaData | Áno           | Štruktúra popisujúca metadata súvisiaceho dokumentu  |
| Data     | byte[]                  | Áno           | Base64binary dáta súvisiaceho dokumentu    		    | 

**Názov štruktúry:** RelatedDocumentMetadata

| **Meno**              | **Typ**                 | **Povinnosť**     | **Popis**                                                                 |
| --------------------- | ----------------------- | ----------------- | ------------------------------------------------------------------------- |
| Type                  | String                  | Áno               | Typ súvisiaceho dokumentu (typ súčasti formulára). Možné hodnoty:         |
|                       |                         |                   | CLS_F_XSLT_DEFAULT                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_SGN                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_BODY                                                 |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_SUBJECT                                              |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_BODY                                                |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_SUBJECT                                             |
|                       |                         |                   | CLS_F_XSLT_TXT_SMS                                                        |
|                       |                         |                   | CLS_F_HTML_FORM                                                           |
|                       |                         |                   | CLS_F_XML_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_DCT                                                             |
|                       |                         |                   | CLS_F_XSL_FO                                                              |
|                       |                         |                   | CLS_F_XSLT_RO                                                             |
|                       |                         |                   | CLS_F_DLL_VAL                                                             |
|                       |                         |                   | CLS_F_XML_MTD                                                             |
|                       |                         |                   | CLS_F_XSLT_NAT_EDOC                                                       |
|                       |                         |                   | CLS_F_XSLT_EDOC_NAT                                                       |
|                       |                         |                   | CLS_F_XSLT_HTML                                                           |
|                       |                         |                   | BalikXML                                                                  |
|                       |                         |                   | CLS_F_XML_DEF                                                             |
|                       |                         |                   | CLS_POSP                                                                  |
|                       |                         |                   | POSP_priloha, (táto hodnota sa už nesmie používať v nových formulároch)   |
|                       |                         |                   | POSP, (táto hodnota sa už nesmie používať v nových formulároch)           |
|                       |                         |                   | EFORM_STANDARD_ZIP_PACKAGE                                                |
| Identifier            | String                  | Áno               | Identifikátor vzoru – názov súboru súvisiaceho dokumentu                  |
| Description           | String                  |                   | Popis súvisiaceho dokumentu                                               |
| Language              | String                  | Áno               | Jazyk súvisiaceho dokumentu                                               |

#### 3.3.8.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
•	06000999
•	06000798
•	06000796

#### 3.3.8.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetEmptyEForm)

### 3.3.9	SubscribeForChanges

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** SubscribeForChanges

**Input Object:** SubscribeForChangesReq

| **Meno**            | **Typ**                  | **Povinnosť** | **Popis**                                                                              |
|---------------------|--------------------------|---------------|----------------------------------------------------------------------------------------|
| SubscribedPublisher | String                   | Áno           | Identifikátor inštitúcie, ktorá sa hlási k odberu. Položka je povinná.                 |
| SubscribedGestor    | String                   | Áno           | Identifikátor gestora, ktorý sa hlási k odberu. Položka je povinná.                    |
| EndpointUrl         | String                   | Áno           | Endpoint URL, na ktoré bude odoslaná správa obsahujúca zmeny vo vypublikovaní/zneplatnení vzorov na základe výberových kritérií.                                                            																			            |
| SearchCriteria      | SubscriberSearchCriteria |               | Vyberové kritériá na základe ktorých sa pre danú inštitúciu a gestora odosielajú informácie o zmenách. V prípade nezadania výberových kritérií sa posielajú informácie o každej zmene v úložisku eFLCM.																									   |

**Output Object:** SubscribeForChangesRes

| **Meno**   | **Typ** | **Povinnosť** | **Popis**                                                  |
|------------|---------|---------------|------------------------------------------------------------|
| ResultCode | Int     |               | Kód chyby. V prípade korektného spracovania je hodnota 0.  |
| Message    | String  |               | Popis vzniknutej chyby                                     |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** SubscriberSearchCriteria

| **Meno**     | **Typ**                  | **Povinnosť** | **Popis**                                        |
|--------------|--------------------------|---------------|--------------------------------------------------|
| FormTemplate | FormTemplateId           |               | Identifikátor vzoru                              |
| Type         | SearchFormTemplateType   |               | Typ vzoru eFormulára                             |
| Title        | String                   |               | Názov vzoru eFormulára                           |
| Description  | String                   |               | Popis vzoru eFormulára                           |
| Publisher    | String                   |               | Identifikátor inštitúcie, ktorá vzor publikuje.  |
| Gestor       | String                   |               | Identifikátor gestora, ktorý vzor publikuje.     |
| FreeText     | String                   |               | Voľný text                                       |
| Keywords     | String                   |               | Zadaný text sa vyhľadáva v  kľúčových slovách.   |
| Status       | SearchFormTemplateStatus |               | Stav vzoru eformulára                            |

SearchFormTemplateType: string
-	All
-	eForm
-	teForm
-	POSP
-	NOTIFY

SearchFormTemplateStatus: string
-	All
-	PUBLISHED
-	INVALIDATED

#### 3.3.9.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000999
-	06000792
-	06000791
-	06000790
-	06000789

#### 3.3.9.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/SubscribeForChanges)

### 3.3.10	UnsubscribeForChanges

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov

- **Názov metódy:** UnsubscribeForChanges

**Input Object:** UnsubscribeForChangesReq

| **Meno**            | **Typ** | **Povinnosť** | **Popis**                                                                    |
|---------------------|---------|---------------|------------------------------------------------------------------------------|
| SubscribedPublisher | String  | Áno           | Identifikátor inštitúcie, ktorá je prihlásená k odberu. Položka je povinná.  |
| SubscribedGestor    | String  | Áno           | Identifikátor gestora, ktorý je prihlásený k odberu. Položka je povinná.     |

**Output Object:** UnsubscribeForChangesRes

| **Meno**   | **Typ** | **Povinnosť** | **Popis**                                                  |
|------------|---------|---------------|------------------------------------------------------------|
| ResultCode | int     |               | Kód chyby. V prípade korektného spracovania je hodnota 0.  |
| Message    | String  |               | Popis vzniknutej chyby                                     |

#### 3.3.10.1	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/UnsubscribeForChanges)

### 3.3.11	ChangeSubscriberSearchCriteria

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov

- **Názov metódy:** ChangeSubscriberSearchCriteria

**Input Object:** ChangeSubscriberSearchCriteriaReq

| **Názov**           | **Typ**                  | **Povinnosť** | **Popis**                                                                                      |
|---------------------|--------------------------|---------------|------------------------------------------------------------------------------------------------|
| SubscribedPublisher | String                   | Áno           | Identifikátor inštitúcie, ktorá je prihlásená k odberu. Položka je povinná.                    |
| SubscribedGestor    | String                   | Áno           | Identifikátor gestora, ktorý je prihlásený k odberu. Položka je povinná.                       |
| SearchCriteria      | SubscriberSearchCriteria |               | Výberové kritériá, na základe ktorých sa pre danú inštitúciu a gestora odosielajú informácie o zmenách. V prípade nezadania výberových kritérií sa posielajú informácie o každej zmene v úložisku eFLCM. 																											|

**Output Object:** ChangeSubscriberSearchCriteriaRes

| **Názov**  | **Typ** | **Povinnosť** | **Popis**                                                  |
|------------|---------|---------------|------------------------------------------------------------|
| ResultCode | int     |               | Kód chyby. V prípade korektného spracovania je hodnota 0.  |
| Message    | String  |               | Popis vzniknutej chyby                                     |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** SubscriberSearchCriteria

| **Meno**     | **Typ**                  | **Povinnosť** | **Popis**                                        |
|--------------|--------------------------|---------------|--------------------------------------------------|
| FormTemplate | FormTemplateId           |               | Identifikátor vzoru                              |
| Type         | SearchFormTemplateType   |               | Typ vzoru eFormulára                             |
| Title        | String                   |               | Názov vzoru eFormulára                           |
| Description  | String                   |               | Popis vzoru eFormulára                           |
| Publisher    | String                   |               | Identifikátor inštitúcie, ktorá vzor publikuje.  |
| Gestor       | String                   |               | Identifikátor gestora, ktorý vzor publikuje.     |
| FreeText     | String                   |               | Voľný text                                       |
| Keywords     | String                   |               | Zadaný text sa vyhľadáva v  kľúčových slovách.   |
| Status       | SearchFormTemplateStatus |               | Stav vzoru eformulára                            |

SearchFormTemplateType: string
-	All
-	eForm
-	teForm
-	POSP
-	NOTIFY

SearchFormTemplateStatus: string
-	All
-	PUBLISHED
-	INVALIDATED

#### 3.3.11.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000999
-	06000790
-	06000793

#### 3.3.11.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/ChangeSubscriberSearchCriteria)

### 3.3.12	ChangeSubscriberEndpointUrl

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** ChangeSubscriberEndpointUrl

**Input Object:** ChangeSubscriberEndpointUrlReq

| **Názov**           | **Typ** | **Povinnosť** | **Popis**                                                                                                                        |
|---------------------|---------|---------------|----------------------------------------------------------------------------------------------------------------------------------|
| SubscribedPublisher | String  | Áno           | Identifikátor inštitúcie, ktorá je prihlásená k odberu. Položka je povinná.                                                      |
| SubscribedGestor    | String  | Áno           | Identifikátor gestora, ktorý je prihlásený k odberu. Položka je povinná.                                                         |
| EndpointUrl         | String  | Áno           | Endpoint URL na ktoré bude odoslaná správa obsahujúca zmeny vo vypublikovaní/zneplatnení vzorov na základe výberových kritérií.  |

**Output Object:** ChangeSubscriberEndpointUrlRes

| **Názov**  | **Typ** | **Povinnosť** | **Popis**                                                  |
|------------|---------|---------------|------------------------------------------------------------|
| ResultCode | int     |               | Kód chyby. V prípade korektného spracovania je hodnota 0.  |
| Message    | String  |               | Popis vzniknutej chyby                                     |

#### 3.3.12.1	Chybové kódy služby

V nasledovnom zozname  sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000999
-	06000790
-	06000793

#### 3.3.12.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/ChangeSubscriberEndpointUrl)

### 3.3.13	GetSubscriberSearchCriteria

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov

- **Názov metódy:** GetSubscriberSearchCriteria

**Input Object:** GetSubscriberSearchCriteriaReq

| **Názov**           | **Typ** | **Povinnosť** | **Popis**                                                                    |
|---------------------|---------|---------------|------------------------------------------------------------------------------|
| SubscribedPublisher | String  | Áno           | Identifikátor inštitúcie, ktorá je prihlásená k odberu. Položka je povinná.  |
| SubscribedGestor    | String  | Áno           | Identifikátor gestora, ktorý je prihlásený k odberu. Položka je povinná.     |

**Output Object:** GetSubscriberSearchCriteriaRes

| **Názov**      | **Typ**                  | **Povinnosť** | **Popis**                                                  |
|----------------|--------------------------|---------------|------------------------------------------------------------|
| ResultCode     | int                      |               | Kód chyby. V prípade korektného spracovania je hodnota 0.  |
| Message        | String                   |               | Popis vzniknutej chyby                                     |
| SearchCriteria | SubscriberSearchCriteria |               | Výberové kritériá, na základe ktorých sa pre danú inštitúciu a gestora odosielajú informácie o zmenách. V prípade nezadania výberových kritérií sa posielajú informácie o každej zmene v úložisku eFLCM = v takomto prípade je výstupná hodnota NULL.						  |                                                            

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** SubscriberSearchCriteria

| **Meno**     | **Typ**                  | **Povinnosť** | **Popis **                                       |
|--------------|--------------------------|---------------|--------------------------------------------------|
| FormTemplate | FormTemplateId           |               | Identifikátor vzoru                              |
| Type         | SearchFormTemplateType   |               | Typ vzoru eFormulára                             |
| Title        | String                   |               | Názov vzoru eFormulára                           |
| Description  | String                   |               | Popis vzoru eFormulára                           |
| Publisher    | String                   |               | Identifikátor inštitúcie, ktorá vzor publikuje.  |
| Gestor       | String                   |               | Identifikátor gestora, ktorý vzor publikuje.     |
| FreeText     | String                   |               | Voľný text                                       |
| Keywords     | String                   |               | Zadaný text sa vyhľadáva v  kľúčových slovách.   |
| Status       | SearchFormTemplateStatus |               | Stav vzoru eFormulára                            |

SearchFormTemplateType: string
-	All
-	eForm
-	teForm
-	POSP
-	NOTIFY

SearchFormTemplateStatus: string
-	All
-	PUBLISHED
-	INVALIDATED

#### 3.3.13.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000999
-	06000790
-	06000793

#### 3.3.13.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetSubscriberSearchCriteria)

### 3.3.14	GetSubscriberEndpointUrl

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov

- **Názov metódy:** GetSubscriberEndpointUrl

**Input Object:** Input Object – GetSubscriberEndpointUrlReq

| **Názov**           | **Typ** | **Povinnosť** | **Popis**                                                                    |
|---------------------|---------|---------------|------------------------------------------------------------------------------|
| SubscribedPublisher | String  | Áno           | Identifikátor inštitúcie, ktorá je prihlásená k odberu. Položka je povinná.  |
| SubscribedGestor    | String  | Áno           | Identifikátor gestora, ktorý je prihlásený k odberu. Položka je povinná.     |

**Output Object:** Output Object – GetSubscriberEndpointUrlRes

| **Názov**   | **Typ** | **Povinnosť** | **Popis**                                                                                                                         |
|-------------|---------|---------------|-----------------------------------------------------------------------------------------------------------------------------------|
| ResultCode  | Int     |               | Kód chyby. V prípade korektného spracovania je hodnota 0.                                                                         |
| Message     | String  |               | Popis vzniknutej chyby                                                                                                            |
| EndpointUrl | String  |               | Endpoint URL, na ktoré bude odoslaná správa obsahujúca zmeny vo vypublikovaní/zneplatnení vzorov na základe výberových kritérií.  |

#### 1.1.13.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000999
-	06000790
-	06000793

#### 3.3.14.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetSubscriberEndpointUrl)

### 3.3.15	GetRelatedDocumentByType

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** GetRelatedDocumentByType

**Input Object:** GetRelatedDocumentByTypeReq

| **Meno**              | **Typ**                 | **Povinnosť**     | **Popis**                                                                 |
| --------------------- | ----------------------- | ----------------- | ------------------------------------------------------------------------- |
| FormTemplate			| FormTemplateID		  | Áno               | ID vzoru																  |
| RelatedDocumentType   | String                  | Áno               | Typ súvisiaceho dokumentu (typ súčasti formulára). Možné hodnoty:         |
|                       |                         |                   | CLS_F_XSLT_DEFAULT                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_SGN                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_BODY                                                 |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_SUBJECT                                              |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_BODY                                                |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_SUBJECT                                             |
|                       |                         |                   | CLS_F_XSLT_TXT_SMS                                                        |
|                       |                         |                   | CLS_F_HTML_FORM                                                           |
|                       |                         |                   | CLS_F_XML_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_DCT                                                             |
|                       |                         |                   | CLS_F_XSL_FO                                                              |
|                       |                         |                   | CLS_F_XSLT_RO                                                             |
|                       |                         |                   | CLS_F_DLL_VAL                                                             |
|                       |                         |                   | CLS_F_XML_MTD                                                             |
|                       |                         |                   | CLS_F_XSLT_NAT_EDOC                                                       |
|                       |                         |                   | CLS_F_XSLT_EDOC_NAT                                                       |
|                       |                         |                   | CLS_F_XSLT_HTML                                                           |
|                       |                         |                   | BalikXML                                                                  |
|                       |                         |                   | CLS_F_XML_DEF                                                             |
|                       |                         |                   | CLS_POSP                                                                  |
|                       |                         |                   | POSP_priloha, (táto hodnota sa už nesmie používať v nových formulároch)   |
|                       |                         |                   | POSP, (táto hodnota sa už nesmie používať v nových formulároch)           |
|                       |                         |                   | EFORM_STANDARD_ZIP_PACKAGE                                                |
| Language              | String                  | Áno               | Jazyk súvisiaceho dokumentu                                               |

**Output Object:** GetRelatedDocumentByTypeRes

| **Názov**       | **Typ**         | **Povinnosť** | **Popis**                                                                                 |
|-----------------|-----------------|---------------|-------------------------------------------------------------------------------------------|
| FormTemplate    | FormTemplateID  |               | ID vzoru                                                                                  |
| RelatedDocument | RelatedDocument |               | Štruktúra obsahujúca metadáta súvisiaceho dokumentu a jeho dáta vo formáte base64binary.  |

opis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** RelatedDocumentMetadata

| **Meno**              | **Typ**                 | **Povinnosť**     | **Popis**                                                                 |
| --------------------- | ----------------------- | ----------------- | ------------------------------------------------------------------------- |
| Type                  | String                  | Áno               | Typ súvisiaceho dokumentu (typ súčasti formulára). Možné hodnoty:         |
|                       |                         |                   | CLS_F_XSLT_DEFAULT                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_SGN                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_BODY                                                 |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_SUBJECT                                              |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_BODY                                                |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_SUBJECT                                             |
|                       |                         |                   | CLS_F_XSLT_TXT_SMS                                                        |
|                       |                         |                   | CLS_F_HTML_FORM                                                           |
|                       |                         |                   | CLS_F_XML_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_DCT                                                             |
|                       |                         |                   | CLS_F_XSL_FO                                                              |
|                       |                         |                   | CLS_F_XSLT_RO                                                             |
|                       |                         |                   | CLS_F_DLL_VAL                                                             |
|                       |                         |                   | CLS_F_XML_MTD                                                             |
|                       |                         |                   | CLS_F_XSLT_NAT_EDOC                                                       |
|                       |                         |                   | CLS_F_XSLT_EDOC_NAT                                                       |
|                       |                         |                   | CLS_F_XSLT_HTML                                                           |
|                       |                         |                   | BalikXML                                                                  |
|                       |                         |                   | CLS_F_XML_DEF                                                             |
|                       |                         |                   | CLS_POSP                                                                  |
|                       |                         |                   | POSP_priloha, (táto hodnota sa už nesmie používať v nových formulároch)   |
|                       |                         |                   | POSP, (táto hodnota sa už nesmie používať v nových formulároch)           |
|                       |                         |                   | EFORM_STANDARD_ZIP_PACKAGE                                                |
| Identifier            | String                  | Áno               | Identifikátor vzoru – názov súboru súvisiaceho dokumentu                  |
| Description           | String                  |                   | Popis súvisiaceho dokumentu                                               |
| Language              | String                  | Áno               | Jazyk súvisiaceho dokumentu                                               |

**Názov štruktúry:** EFormVersion

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

#### 3.3.15.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000999
-	06000798
-	06000796

#### 3.3.12.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetRelatedDocumentByType)

### 3.3.16	TransformRelatedDocument

Služba je určená pre transformáciu súvisiaceho dokumentu nachádzajúceho sa v elektronickom formulári na základe určeného XSLT elektronického formulára.

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** TransformRelatedDocument

**Input Object:** TransformRelatedDocumentReq

| **Názov**           | **Typ**        | **Povinnosť** | **Popis**                                                                                        |
|---------------------|----------------|---------------|--------------------------------------------------------------------------------------------------|
| FormTemplate        | FormTemplateID | Áno           | ID vzoru                                                                                         |
| RelatedDocumentXML  | String         | Áno           | Identifikátor súvisiaceho dokumentu, ktorý sa má vizualizovať. Súbor musí byť vo formáte XML.    |
| RelatedDocumentXSLT | String         | Áno           | Identifikátor súvisiaceho dokumentu, ktorý má character vizualizácie. Musí byť vo formáte XSLT.  |

**Output Object:** TransformRelatedDocumentRes

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**                                                                                                                                      |
|--------------|----------------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| FormTemplate | FormTemplateID |               | ID vzoru                                                                                                                                       |
| EDoc         | EDocument      |               | Štruktúra obsahuje názov dokumentu a data dokumentu vizualizovaného v požadovanom formáte s použitím vizualizácie, ktorá sa zadala ako vstup.  |

opis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

**Názov štruktúry:** EDocument

| **Názov** | **Typ** | **Povinnosť** | **Popis**                                                                                                  |
|-----------|---------|---------------|------------------------------------------------------------------------------------------------------------|
| Title     | string  |               | Názov elektronického dokumentu s príponou .pdf.                                                            |
| Data      | byte[]  |               | Dáta elektronického dokumentu vizualizovaného vo formáte .pdf. Kódovanie prenášaných dát je base64Binary.  |

#### 3.3.16.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
•	06000999
•	06000798
•	06000796
•	06000786

#### 3.3.16.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/TransformRelatedDocument)

### 3.3.17	TransformRelatedDocumentFromXML

Služba je určená pre transformáciu XML údajov vyplnených podľa el. formulára, ktoré sú vložené do volania služby s  identifikáciou XML transformácie (XSLT súvisiaceho dokumentu) v elektronickom formulári.

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov 

- **Názov metódy:** TransformRelatedDocumentFromXML

**Input Object:** TransformRelatedDocumentFromXMLReq

| **Názov**           | **Typ**        | **Povinnosť** | **Popis**                                                                                                                |
|---------------------|----------------|---------------|--------------------------------------------------------------------------------------------------------------------------|
| FormTemplate        | FormTemplateID | Áno           | ID vzoru                                                                                                                 |
| RelatedDocumentXML  | byte[]         | Áno           | Base64Binary kódované XML dáta elektronického formulára.                                                                 |
| RelatedDocumentXSLT | String         | Áno           | Identifikátor súvisiaceho dokumentu vizualizácie. Tento musí byť vo formáte XSLT.                                        |
| FOTransform         | bool           | Áno           | V prípade ak je nastavená hodnota na TRUE, tak po XSLT transformácii prebehne aj FO transformácia. Podmienkou však je to aby XSLT vizualizácia mala ako svoj výstup FO dokument.  																																								|

**Output Object:** TransformRelatedDocumentFromXMLRes

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**                                                                                   |
|--------------|----------------|---------------|---------------------------------------------------------------------------------------------|
| FormTemplate | FormTemplateID |               | ID vzoru                                                                                    |
| EDoc         | EDocument      |               | Štruktúra obsahuje názov dokumentu a data dokumentu vizualizovaného v požadovanom formáte.  |

opis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

**Názov štruktúry:** EDocument

| **Názov** | **Typ** | **Povinnosť** | **Popis**                                                                                                  |
|-----------|---------|---------------|------------------------------------------------------------------------------------------------------------|
| Title     | string  |               | Názov elektronického dokumentu s príponou .pdf.                                                            |
| Data      | byte[]  |               | Dáta elektronického dokumentu vizualizovaného vo formáte .pdf. Kódovanie prenášaných dát je base64Binary.  |

#### 3.3.17.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000999
-	06000798
-	06000796
-	06000786

#### 3.3.17.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/TransformRelatedDocumentFromXML)

### 3.3.18	TransformRelatedDocumentByType

Služba je určená pre transformáciu súvisiaceho dokumentu nachádzajúceho sa v elektronickom formulári na základe určeného XSLT elektronického formulára určeného jeho typom.

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov

- **Názov metódy:** TransformRelatedDocumentByType

**Input Object:** TransformRelatedDocumentReq

| **Názov**                    | **Typ**        | **Povinnosť** | **Popis**                                                                                                       |
|------------------------------|----------------|---------------|-----------------------------------------------------------------------------------------------------------------|
| FormTemplate                 | FormTemplateID | Áno           | ID vzoru                                                                                                        |
| RelatedDocumentXMLType       | String         | Áno           | Typ súvisiaceho dokumentu, ktorý sa má vizualizovať. Súbor musí byť vo formáte XML.                             |
| RelatedDocumentXMLLanguage*  | String         | Áno           | Jazyk súvisiaceho dokumentu, ktorý sa má vizualizovať. Súbor musí byť vo formáte XML.                           |
| RelatedDocumentXSLType       | String         | Áno           | Typ súvisiaceho dokumentu ktorý má charakter vizualizácie. Musí byť vo formáte XSLT                             |
| RelatedDocumentXSLTLanguage* | String         | Áno           | Jazyk súvisiaceho dokumentu, ktorý má charakter vizualizácie. Táto musí byť vo formáte XSLT                     |
| FOTransform                  | bool           | Áno           | V prípade ak je nastavená hodnota na TRUE, tak po XSLT transformácii prebehne aj FO transformácia. Podmienkou však je to aby XSLT vizualizácia mala ako svoj výstup FO dokument.  																																					|

> [!NOTE]
> *Služba vyhľadá dokumenty podľa jazyka z requestu. V prípade, že atribút „language“ je prázdny, alebo dokument v danom jazyku neexistuje, služba vyhľadá dokument podľa atribútu „language“ formulára. Ak dokument v jazyku formulára neexistuje, služba hľadá dokument v jazyku „sk“. Ak taký dokument neexistuje, služba v transformácii použije prvý nájdený dokument daného typu.

**Output Object:** TransformRelatedDocumentByTypeRes

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**                                                                                                                                      |
|--------------|----------------|---------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| FormTemplate | FormTemplateID |               | ID vzoru                                                                                                                                       |
| EDoc         | EDocument      |               | Štruktúra obsahuje názov dokumentu a data dokumentu vizualizovaného v požadovanom formáte s použitím vizualizácie, ktorá sa zadala ako vstup.  |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

**Názov štruktúry:** EDocument

| **Názov** | **Typ** | **Povinnosť** | **Popis**                                                                                                  |
|-----------|---------|---------------|------------------------------------------------------------------------------------------------------------|
| Title     | string  |               | Názov elektronického dokumentu s príponou .pdf.                                                            |
| Data      | byte[]  |               | Dáta elektronického dokumentu vizualizovaného vo formáte .pdf. Kódovanie prenášaných dát je base64Binary.  |

#### 3.3.18.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000999
-	06000798
-	06000796
-	06000786

#### 3.3.18.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/TransformRelatedDocumentByType)

### 3.3.19	TransformRelatedDocumentFromXMLByType

Služba je určená pre transformáciu XML údajov vyplnených podľa formulára vložených vo volaní služby špecifikáciou požadovaného typu prezentačnej schémy (XSLT).

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** TransformRelatedDocumentFromXML

**Input Object:** TransformRelatedDocumentFromXMLByTypeReq

| **Názov**                    | **Typ**        | **Povinnosť**  | **Popis**																							 |
|------------------------------|----------------|----------------|-------------------------------------------------------------------------------------------------------|
| FormTemplate                 | FormTemplateID | Áno            | ID vzoru 																							 |
| RelatedDocumentXML           | byte[]         | Áno            | Base64Binary kódované XML dáta elektronického formulára.          									 |
| RelatedDocumentXSLTType      | String         | Áno            | Typ súvisiaceho dokumentu vizualizácie. Tento musí byť vo formáte XSLT.         						 |
| RelatedDocumentXSLTLanguage* | String         | Áno            | Jazyk súvisiaceho dokumentu, ktorý má charakter vizualizácie. Táto musí byť vo formáte XSLT.          |
|							   |                |                | Možné hodnoty:                                                				    			         |
|                      		   |                |                | CLS_F_XSLT_TXT_SGN                                                							         |
|                              |                |                | CLS_F_XSLT_TXT_EMAIL_BODY                                                                             |
|                              |                |                | CLS_F_XSLT_TXT_EMAIL_SUBJECT                                                                          |
|                              |                |                | CLS_F_XSLT_HTML_EMAIL_BODY                                                                            |
|                              |                |                | CLS_F_XSLT_HTML_EMAIL_SUBJECT                                                                         |
|                              |                |                | CLS_F_XSLT_TXT_SMS                                                                                    |
|							   |                |                | CLS_F_XSLT_RO																			         	 |
|							   |                |                | CLS_F_XSLT_NAT_EDOC																				     |
|							   |                |                | CLS_F_XSLT_EDOC_NAT																				     |
|							   |                |                | CLS_F_XSLT_HTML																				         |
| FOTransform                  | bool           | Áno            | V prípade, ak je nastavená hodnota na TRUE , tak po XSLT transformácii prebehne aj FO transformácia. Podmienkou však je to aby XSLT vizualizácia mala ako svoj výstup FO dokument.         																																 |

> [!NOTE]
> *Služba vyhľadá dokumenty podľa jazyka z requestu. V prípade, že atribút „language“ je prázdny, alebo dokument v danom jazyku neexistuje, služba vyhľadá dokument podľa atribútu „language“ formulára a v prípade viacerých vyhovujúcich výsledkov poskytne prvý nájdený dokument. Ak dokument v jazyku formulára neexistuje, služba hľadá dokument v jazyku „sk“. Ak taký dokument neexistuje, služba v transformácii použije prvý nájdený dokument daného typu.

**Output Object:** TransformRelatedDocumentFromXMLByTypeRes

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**                                                                                   |
|--------------|----------------|---------------|---------------------------------------------------------------------------------------------|
| FormTemplate | FormTemplateID |               | ID vzoru                                                                                    |
| EDoc         | EDocument      |               | Štruktúra obsahuje názov dokumentu a data dokumentu vizualizovaného v požadovanom formáte.  |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

**Názov štruktúry:** EDocument

| **Názov** | **Typ** | **Povinnosť** | **Popis**                                                                                                  |
|-----------|---------|---------------|------------------------------------------------------------------------------------------------------------|
| Title     | string  |               | Názov elektronického dokumentu s príponou .pdf.                                                            |
| Data      | byte[]  |               | Dáta elektronického dokumentu vizualizovaného vo formáte .pdf. Kódovanie prenášaných dát je base64Binary.  |

#### 3.3.19.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000999
-	06000798
-	06000796
-	06000786

#### 3.3.19.2	Príklad volania služby - SOAP

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/TransformRelatedDocumentFromXMLByType)

### 3.3.20	GetFormTemplate

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** GetFormTemplate

**Input Object:** GetFormTemplateReq

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**  |
|--------------|----------------|---------------|------------|
| FormTemplate | FormTemplateID | Áno           | ID vzoru   |

**Input Object:** GetFormTemplateRes

| **Názov**     | **Typ**      | **Povinnosť** | **Popis**                          |
|---------------|--------------|---------------|------------------------------------|
| EFormTemplate | FormTemplate |               | Štruktúra obsahuje vzor eformulára |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** FormTemplate 

| **Meno**         | **Typ**              | **Povinnosť** | **Popis**                                                                 |
|------------------|----------------------|---------------|---------------------------------------------------------------------------|
| MetaData         | FormTemplateMetaData | Áno           | Názov žiadosti                                                            |
| RelatedDocuments | RelatedDocument[]    | Áno           | Súvisiace dokumenty                                                       |
| Data             | byte[]               |               | Nepoužívané – pôvodne používané pre uloženie prázdneho vzoru eFormuláru.  |

**Názov štruktúry:** FormTemplateMetaData

| **Meno**           | **Typ**          | **Povinnosť**  | **Popis**                                                                                              |
|--------------------|------------------|----------------|--------------------------------------------------------------------------------------------------------| 
| Identifier         | String           | Áno            | Identifikátor vzoru eFormulára                                                                         |
| Title              | String           | Áno            | Názov vzoru                                                                                            |
| Type               | FormTemplateType | Áno            | Typ vzoru                                                                                              |
| Description        | String           | Áno            | Popis vzoru                                                                                            |
| Gestor             | String           | Áno            | Gestor 																							      |             
| Publisher          | String           | Áno            | Inštitúcia                                                                                             |
| Section            | String           |                | Sekcia                                                                                                 |
| Agenda             | String           |                | Agenda                                                                                                 |
| Source             | String           |                | Pôvod vzoru                                                                                            |
| Version            | EFormVersion     | Áno            | Verzia vzoru.                                                                                          |
| ValidDateFrom      | DateTime         | Áno            | Začiatok platnosti vzoru                                                                               |
| ValidDateTo        | DateTime         |                | Koniec platnosti vzoru                                                                                 |
| Keywords           | String           |                | Kľúčové slová                                                                                          |
| AccessGroup        | String           |                | Prístupová skupina - toto pole sa aktuálne nevypĺňa (uvedené z historických dôvodov). Pre formuláre, ktoré majú uvedenú skupinu prístupu je táto hodnota pri vyhodnocovaní prístupu k formulárom ignorovaná a teda všetky formuláre sú prístupné.                                                                          |

**Názov štruktúry:** EFormVersion 

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

FormTemplateType: string
-	eForm
-	teForm
-	POSP
-	NOTIFY

**Názov štruktúry:** RelatedDocument

| **Meno** | **Typ**                 | **Povinnosť** | **Popis**                                            |
|----------|-------------------------|---------------|------------------------------------------------------|
| MetaData | RelatedDocumentMetaData | Áno           | Štruktúra popisujúca metadata súvisiaceho dokumentu  |
| Data     | byte[]                  | Áno           | Base64binary dáta súvisiaceho dokumentu    		    |                                                     

**Názov štruktúry:** RelatedDocumentMetadata

| **Meno**              | **Typ**                 | **Povinnosť**     | **Popis**                                                                 |
| --------------------- | ----------------------- | ----------------- | ------------------------------------------------------------------------- |
| Type                  | String                  | Áno               | Typ súvisiaceho dokumentu (typ súčasti formulára). Možné hodnoty:         |
|                       |                         |                   | CLS_F_XSLT_DEFAULT                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_SGN                                                        |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_BODY                                                 |
|                       |                         |                   | CLS_F_XSLT_TXT_EMAIL_SUBJECT                                              |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_BODY                                                |
|                       |                         |                   | CLS_F_XSLT_HTML_EMAIL_SUBJECT                                             |
|                       |                         |                   | CLS_F_XSLT_TXT_SMS                                                        |
|                       |                         |                   | CLS_F_HTML_FORM                                                           |
|                       |                         |                   | CLS_F_XML_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_NAT                                                             |
|                       |                         |                   | CLS_F_XSD_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_EDOC                                                            |
|                       |                         |                   | CLS_F_XML_DCT                                                             |
|                       |                         |                   | CLS_F_XSL_FO                                                              |
|                       |                         |                   | CLS_F_XSLT_RO                                                             |
|                       |                         |                   | CLS_F_DLL_VAL                                                             |
|                       |                         |                   | CLS_F_XML_MTD                                                             |
|                       |                         |                   | CLS_F_XSLT_NAT_EDOC                                                       |
|                       |                         |                   | CLS_F_XSLT_EDOC_NAT                                                       |
|                       |                         |                   | CLS_F_XSLT_HTML                                                           |
|                       |                         |                   | BalikXML                                                                  |
|                       |                         |                   | CLS_F_XML_DEF                                                             |
|                       |                         |                   | CLS_POSP                                                                  |
|                       |                         |                   | POSP_priloha, (táto hodnota sa už nesmie používať v nových formulároch)   |
|                       |                         |                   | POSP, (táto hodnota sa už nesmie používať v nových formulároch)           |
|                       |                         |                   | EFORM_STANDARD_ZIP_PACKAGE                                                |
| Identifier            | String                  | Áno               | Identifikátor vzoru – názov súboru súvisiaceho dokumentu                  |
| Description           | String                  |                   | Popis súvisiaceho dokumentu                                               |
| Language              | String                  | Áno               | Jazyk súvisiaceho dokumentu                                               |

#### 3.3.20.1	Chybové kódy služby

V nasledovnom zozname  sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000798

#### 3.3.20.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetFormTemplate)

### 3.3.21	SetFormTemplateStatus

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** SetFormTemplateStatus

**Input Object:** SetFormTemplateStatusReq

| **Názov**    | **Typ**            | **Povinnosť** | **Popis**   |
|--------------|--------------------|---------------|-------------|
| FormTemplate | FormTemplateID     | Áno           | ID vzoru    |
| FormStatus   | FormTemplateStatus | Áno           | Stav vzoru  |

**Output Object:** Output Object - SetFormTemplateStatusRes

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**                                                                            |
|--------------|----------------|---------------|--------------------------------------------------------------------------------------|
| FormTemplate | FormTemplateID |               | ID vzoru                                                                             |
| ResultCode   | int            |               | 0 = operácia prebehla OK. V prípade chyby je volaná FaultException s chybovým kódom  |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

FormTemplateStatus: string
-	PUBLISHED
-	INVALIDATED

#### 3.3.21.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000798
-	06000796
-	06000786

#### 3.3.21.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/SetFormTemplateStatus)

### 3.3.22	GetFilledEForm

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** GetFilledEForm

**Input Object:** GetFilledEFormReq

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**                                                                                                                           |
|--------------|----------------|---------------|-------------------------------------------------------------------------------------------------------------------------------------|
| FormTemplate | FormTemplateID | Áno           | ID vzoru                                                                                                                            |
| Actor        | String         | Áno           | Ideentifikátor actor ID, pre ktorého sa požaduje predvyplnenie vzoru eFormulára.                                                    |
| Subject      | String         |               | Identifikátor inštitúcie, za ktorú sa požaduje predvyplnenie vzoru eFormulára.                                                      |
| Data         | Byte[]         |               | Dáta vzoru eFormulára, ktoré sa predvypĺňajú. V prípade, ak sa tento parameter nevyplní, použije sa prázdny EDoc na predvyplnenie.  |

**Output Object:** GetFilledEFOrmRes

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**                     |
|--------------|----------------|---------------|-------------------------------|
| FormTemplate | FormTemplateID |               | ID vzoru                      |
| Data         | Byte[]         |               | Predvyplnený vzor eformulára  |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

#### 3.3.22.1	Chybové kódy služby

V nasledovnom zozname  sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000798
-	06000796
-	06000796
-	06000785
-	06000784

#### 3.3.22.2	Príklad volania služby – SOAP 

- [Request/Response](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetFilledEForm)

### 3.3.23	GetEFormPackage

Synchrónna služba určená na poskytnutie vzoru eformulára vo formáte predpísanom výnosom ISVS. V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov

- **Názov metódy:** GetEFormPackage

**Input Object:** GetEFormPackageReq

| **Názov**    | **Typ**          | **Povinnosť** | **Popis**                                                      |
|--------------|------------------|---------------|----------------------------------------------------------------|
| FormTemplate | FormTemplateID   | Áno           | ID vzoru                                                       |
| PackageType  | EFormPackageType | Áno           | Typ požadovaného balíka vzoru (ZIP)							   |

**Output Object:** GetEFormPackageRes

| **Názov**          | **Typ**              | **Povinnosť** | **Popis**                                        |
|--------------------|----------------------|---------------|--------------------------------------------------|
| InternalIdentifier | FormTemplateID       |               | Interný ÚPVS identifikátor vzoru eFormulára      |
| Identifier         | String               |               | Referencovateľný identifikátor vzoru eFormulára  |
| FormPackage        | eFormPackage         |               | Balík vzoru eFormulára			               |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

> [!NOTE]
> Pre zistenie aktuálne (účinnej) verzie vzoru eFormulára sa parameter EFormVersion v requeste neuvádza.

**Názov štruktúry:** EFormVersion

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

> [!NOTE]
> nulové hodnoty týchto atribútov v rámci requestu nie sú prípustné.

**Názov štruktúry:** EFormPackage

| **Meno**    | **Typ**          | **Povinnosť** | **Popis**                                                                                                                                                       |
|-------------|------------------|---------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| PackageType | EFormPackageType |               | Typ formátu balíka vzoru eformulára ZIP. Poznámka: V zmysle novely výnosu o štandardoch sa formát XML (EFORM STANDARD XML PACKAGE) od roku 2018 nemá používať.  |
| MetadataExt | EFormMetaDataExt |               | ÚPVS metadáta k balíku vzoru                                                                                                                                    |
| Data        | Byte[]           |               | Balík vzoru eFormulára                                                                                                                                          |

EFormPackageType: string
-	ZIP

**Názov štruktúry:** EFormMetaDataExt

| **Meno**    | **Typ** | **Povinnosť** | **Popis**                                                                              |
|-------------|---------|---------------|----------------------------------------------------------------------------------------|
| Section     | String  |               | Sekcia                                                                                 |
| Agenda      | String  |               | Agenda                                                                                 |
| Source      | String  |               | Pôvod vzoru                                                                            |
| Keywords    | String  |               | Kľúčové slová                                                                          |
| AccessGroup | String  |               | Prístupová skupina - toto pole sa aktuálne nevypĺňa (uvedené z historických dôvodov). Pre formuláre, ktoré majú uvedenú skupinu prístupu je táto hodnota pri vyhodnocovaní prístupu k formulárom ignorovaná a teda všetky formuláre sú prístupné.  														  |

#### 3.3.23.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000798
-	06000775
-	06000776

#### 3.3.23.2	Príklad volania služby – SOAP

- [Request](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetEFormPackage)

### 3.3.24	GetEFormTemplateManifestXML

Služba slúži na poskytnutie súboru manifest.xml, ktorý je predpísaný výnosom ISVS ako popisný súbor balíka vzoru eFormulára. V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** GetEFormPackage

**Input Object:** GetEFormPackageReq

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**                                                      |
|--------------|----------------|---------------|----------------------------------------------------------------|
| FormTemplate | FormTemplateID | Áno           | ID vzoru                                                       |

**Output Object:** GetEFormPackageRes

| **Názov**          | **Typ**              | **Povinnosť** | **Popis**                                        |
|--------------------|----------------------|---------------|--------------------------------------------------|
| InternalIdentifier | FormTemplateID       |               | Interný ÚPVS identifikátor vzoru eFormulára      |
| Identifier         | String               |               | Referencovateľný identifikátor vzoru eFormulára  |
| Data               | Byte[]               |               | manifest.xml subor encodovaný base64             |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

#### 3.3.24.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000798
-	06000773

#### 3.3.24.2	Príklad volania služby – SOAP

- [Reuqest](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetEFormTemplateManifestXML)

### 3.3.25	GetEFormTemplateAttachmentsXML

Služba slúži na poskytnutie súboru attachments.xml, ktorý je predpísaný výnosom ISVS ako popisný súbor príloh ktoré sa nachádzajú v balíku vzoru eformulára. V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** GetEFormPackage

**Input Object:** GetEFormPackageReq

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**                                                      |
|--------------|----------------|---------------|----------------------------------------------------------------|
| FormTemplate | FormTemplateID | Áno           | ID vzoru                                                       |

**Output Object:** GetEFormPackageRes

| **Názov**          | **Typ**              | **Povinnosť** | **Popis**                                        |
|--------------------|----------------------|---------------|--------------------------------------------------|
| InternalIdentifier | FormTemplateID       |               | Interný ÚPVS identifikátor vzoru eFormulára      |
| Identifier         | String               |               | Referencovateľný identifikátor vzoru eFormulára  |
| Data               | Byte[]               |               | attachments.xml subor encodovaný base64          |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

#### 3.3.25.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000798
-	06000772

#### 3.3.25.2	Príklad volania služby – SOAP

- [Request](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetEFormTemplateAttachmentsXML)

### 3.3.26	GetEFormTemplateMetaXML

Služba slúži na poskytnutie súboru metadát meta.xml, ktorý je predpísaný výnosom ISVS. V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** GetEFormPackage

**Input Object:** GetEFormPackageReq

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**                                                      |
|--------------|----------------|---------------|----------------------------------------------------------------|
| FormTemplate | FormTemplateID | Áno           | ID vzoru                                                       |

**Output Object:** GetEFormPackageRes

| **Názov**          | **Typ**              | **Povinnosť** | **Popis**                                        |
|--------------------|----------------------|---------------|--------------------------------------------------|
| InternalIdentifier | FormTemplateID       |               | Interný ÚPVS identifikátor vzoru eFormulára      |
| Identifier         | String               |               | Referencovateľný identifikátor vzoru eFormulára  |
| Data               | Byte[]               |               | meta.xml subor encodovaný base64                 |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

#### 3.3.26.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000798
-	06000774

#### 3.3.26.2	Príklad volania služby – SOAP

- [Request](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetEFormTemplateMetaXML)

### 3.3.27	GetEFormPackageArtefact

V tabuľke je pre metódu uvedený popis vstupných a výstupných parametrov.

- **Názov metódy:** GetEFormPackage

**Input Object:** GetEFormPackageReq

| **Názov**    | **Typ**        | **Povinnosť** | **Popis**                                                      |
|--------------|----------------|---------------|----------------------------------------------------------------|
| FormTemplate | FormTemplateID | Áno           | ID vzoru                                                       |
| FullPath     | String         | Áno           | Cesta k súboru vzoru eFormulára tak ako je vedená v meta.xml.  |

**Output Object:** GetEFormPackageRes

| **Názov**          | **Typ**              | **Povinnosť** | **Popis**                                        |
|--------------------|----------------------|---------------|--------------------------------------------------|
| InternalIdentifier | FormTemplateID       |               | Interný ÚPVS identifikátor vzoru eFormulára      |
| Identifier         | String               |               | Referencovateľný identifikátor vzoru eFormulára  |
| Artefact           | EFormPackageArtefact |               | Požadovaný súvisiaci dokument vzoru eformulára   |

Popis štruktúr použitých vo webovej službe: 

**Názov štruktúry:** FormTemplateID

| **Meno**   | **Typ**      | **Povinnosť** | **Popis**            |
|------------|--------------|---------------|----------------------|
| Identifier | string       | Áno           | Identifikátor vzoru  |
| Version    | EFormVersion |               | Verzia vzoru         |

**Názov štruktúry:** EFormVersion

| **Meno** | **Typ** | **Povinnosť** | **Popis**        |
|----------|---------|---------------|------------------|
| Major    | int     | Áno           | Verzia vzoru     |
| Minor    | int     | Áno           | Podverzia vzoru  |

**Názov štruktúry:** EFormPackageArtefact 

| **Meno** | **Typ** | **Povinnosť** | **Popis**                                                               |
|----------|---------|---------------|-------------------------------------------------------------------------|
| FullPath | String  |               | Cesta k požadovanému súboru                                             |
| Data     | Byte[]  |               | Požadovaný súvisiaci dokument vzoru eFormulára „encodovaný“ ako base64  |

#### 3.3.27.1	Chybové kódy služby

V nasledovnom zozname sú pre metódu uvedené možné chybové stavy. Ich bližší popis je uvedený v kapitole 6.

**Chybové stavy:**
-	06000997
-	06000998
-	06000999
-	06000798
-	06000771

#### 3.3.27.2	Príklad volania služby – SOAP

- [Request](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Extern%C3%A1%20zbernica%20(USR)/GetEFormPackageArtefact)

# 4	WSDL služieb publikovaných na Externej zbernici

## 4.1	Popis eForm WebService: http://< IP adresa eform servera >/_vti_bin/eFLCMService.svc

Adresa rozhrania externej zbernice:

- https://vyvoj.upvs.globaltel.sk/ServiceBus/ServiceBusToken.svc

Popis volania EZ (USR) je uvedený v integračnom manuály G2G. XML schémy jednotlivých služieb publikovaných na EZ uvádzame len ilustračné – generovanie klienta služieb eForm sa realizuje s využitím WSDLGeneratora EZ. 

- https://vyvoj.upvs.globaltel.sk/ServiceBus/SbWsdlGeneratorToken.aspx

Na [nasledujúcom linku](https://github.com/NASES-Slovakia/integration_manuals/tree/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/WSDL%20slu%C5%BEieb%20publikovan%C3%BDch%20na%20Externej%20zbernici) sú poskytnuté XML schémy všetkých synchrónnych služieb modulu eForm.

![Obr](https://github.com/NASES-Slovakia/integration_manuals/blob/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/Images/Zobrazenie%20GUI%20rozhrania%20EZ%20%E2%80%93%20%C4%8Das%C5%A5%20WSDL%20gener%C3%A1tor.jpg)

Aktuálne WSDL publikovaných služieb pre DEV prostredie je priložené nižšie. Jeho súčasťou sú aj všetky schémy potrebné pre volanie synchrónnych služieb modulu MEF.

https://github.com/NASES-Slovakia/integration_manuals/blob/main/Modul%20eFORM/Integra%C4%8Dn%C3%BD%20manu%C3%A1l%20eFORM/WSDL%20slu%C5%BEieb%20publikovan%C3%BDch%20na%20Externej%20zbernici/DEV_WSDL_SbWsdlGeneratorToken__eFORM.XML

> [!WARNING]
> Uvedené WSDL predstavuje príklad popisu služby modulu eForm. Reálnu implementáciu tejto služby na strane integrátora je vytváraná proti definícií služby publikovanej na externej zbernici na príslušnom integračnom prostredí ÚPVS. Pre FIX prostredie zvolením konkrétneho modulu generovaním wsdl cez tlačidlo „Generate WSDL“ na adrese https://usr.upvsfixnew.gov.sk/ServiceBus/SbWsdlGeneratorToken.aspx

# 5	Synchronizácia s podriadenými modulmi - Subscribe

## 5.1	Použitie

EForm modul poskytuje funkcionalitu odberu správ o zmenách stavu vzorov eFormulárov (publish/subscribe) pre podriadené moduly. Podriadeným modulom môže byť interný systém ÚPVS, ale I systém ISVS, ktorý je registrovaný prostredníctvom poskytovaných služieb k odberu správ.

Modul synchronizácie s podriadenými modulmi umožňuje pre podriadený modul:
-	prihlásenie sa k odberu zmien v úložisku vzorov,
-	zadanie výberových kritérií pre odoberanie správ o zmene stavu vzorov,
-	zadanie Endpoint adresy podriadeného systém na ktorú budú zasielané zmeny v úložisku vzorov prostredníctvom rozhrania UIR,
-	získanie informácií o nastavených výberových kritériách ako i ich následnú zmenu,
-	získanie informácií o nastavenej cieľovej end point adrese ako i jej následnú zmenu,
-	odhlásenie sa od odoberania správ o zmenách stavu vzorov v úložisku vzorov eFormulárov.

Z pohľadu použitia tejto množiny operácií je vhodné postupovať nasledovne:

1. Systém, ktorý potrebuje byť informovaný o aktuálne publikovaných alebo zneplatnených vzoroch v úložisku vzorov eFormulárov ÚPVS zavolá službu SubscribeForChanges. Pre úspešné zaregistrovanie však musí vyplniť vstupné parametre podľa popisu uvedenom v tomto manuáli. Od okamihu zaregistrovania eForm modul generuje pre tento prihlásený systém zmeny v úložisku a tieto mu odosiela v pravidelných intervaloch na adresu zadanú v registrácii prostredníctvom služby SubscribeForChanges.

2. V prípade, ak z nejakých dôvodov dôjde k zmene cieľovej adresy, kde podriadený systém chce dostávať takéto informácie, môže zavolať službu ChangeSubscriberEndpointUrl, s pomocou ktorej je možné URL adresu zmeniť. Taktiež môže zavolať službu GetSubscriberEndpointURL, kde si vie získať aktuálne nastavenú URL počas registrácie.

3. Obdobným spôsobom vie podriadený systém získať informácie o nastavených filtračných podmienkach, ktoré zužujú oblasť vzorov, o ktorých je požadované získavať notifikácie v prípade zmeny, slúži na to služba GetSubscriberSearchCriteria. Pokiaľ je požadovaná zmena vyhľadávacích kritérií, je potrebné volať službu ChangeSubscriberSearchCriteria, kde je možné aktuálne nastavené výberové podmienky zmeniť. Pokiaľ je požadované dostávať akékoľvek informácie o zmenách.

4. Pokiaľ už nie je potrebné získavať informácie o zmenách v úložisku vzorov, je potrebné sa odhlásiť. Toto sa vykoná prostredníctvom služby UnsubscribeSearchCriteria.

## 5.2	Implementácia subscribera

Podriadený modul, ktorý požaduje od EFLCM získať informácie o zmenách vo vzoroch musí implementovať také rozhranie umožňujúce prijať správu typu SKTalk vo verzii 3. 

Informácia o zmenách je v rámci SKTalk identifikovaná prostredníctvom CLASSNAME takejto správy, toto sa rovná hodnote **EFORM_SubscriptionMessageASync_01** . 

Vstupným parametrom takejto správy, t.j. obsahom BODY časti SKTalk správy je správa typu **eFLCMSubscriptionMessage**. Jedná sa o štruktúru ktorá obsahuje zoznam zmenených vzorov. Popis štruktúry je v popise služby EFORM_SubscriptionMessageASync_01 v tomto dokumente. Nasledovná kapitola obsahuje XSD schému pre túto správu.

V rámci rôznych implementácii na rôznych projektoch sa detegovala chybná implementácia štruktúry „subscriber“. Na projektoch implementovali spracovanie notifikácii ako synchrónnu službu, v rámci volania ktorej zároveň sťahovali dotknuté eFormulárové balíky z ÚPVS MEF modulu. Implementáciu je nutné riešiť ako asynchrónnu službu, t.j. Po prijatí notifikácie spustit samotné doťahovanie eformulárov paralelným procesom, prípadne ak je toto možné vytvoriť si  stahovanie formou časovej úlohy na iný čas ako sa príjme notifikácia – to z dôvodu zaťaženia UPVS MEF modulu počas synchronizácie voči každému subsriberovi.

Notifikácie o zmenách je možné zasielať buď na špecifikované integračné rozhranie „Subscribera“ – EndPoint, alebo priamo do jeho eDesk schránky. 

V prípade **externého endpointu** je potrebné, aby bolo rozhranie „Subscribera“ nakonfigurované ako obojsmerná komunikácia v zázname „UIR (URP, URZ - BPM)“ v rámci VPN tunela realizovaného pre FIX/PROD prostredie v záložke „Integračné aplikačné endpointy“.    

V prípade zasielania notifikácii priamo **do eDesk schránky**, „Subscriber“ v rámci elementu SubscribeForChangesReq / EndpointUrl uvedie svoje URI, ktoré reprezentuje identifikátor jeho eDesk schránky.

## 5.3	Schéma správy eFLCMSubscriptionMessage

```

<?xml version="1.0" encoding="utf-8"?>
<xs:schema xmlns:tns="http://schemas.gov.sk/eflcm/eFLCMSubscribtionMessage/1.0" elementFormDefault="qualified" targetNamespace="http://schemas.gov.sk/eflcm/eFLCMSubscribtionMessage/1.0" xmlns:xs="http://www.w3.org/2001/XMLSchema">
	<xs:element name="eFLCMSubscriptionMessage">
		<xs:complexType>
			<xs:sequence>
				<xs:element minOccurs="0" maxOccurs="1" name="SubscribedGestor" type="xs:string"/>
				<xs:element minOccurs="0" maxOccurs="1" name="SubscribedPublisher" type="xs:string"/>
				<xs:element minOccurs="0" maxOccurs="1" name="FormTemplates" type="tns:ArrayOfEFormTemplate"/>
			</xs:sequence>
		</xs:complexType>
	</xs:element>
	<xs:complexType name="ArrayOfEFormTemplate">
		<xs:sequence>
			<xs:element minOccurs="0" maxOccurs="unbounded" name="EFormTemplate" nillable="true" type="tns:EFormTemplate"/>
		</xs:sequence>
	</xs:complexType>
	<xs:complexType name="EFormTemplate">
		<xs:sequence>
			<xs:element minOccurs="0" maxOccurs="1" name="Publisher" type="xs:string"/>
			<xs:element minOccurs="0" maxOccurs="1" name="Gestor" type="xs:string"/>
			<xs:element minOccurs="0" maxOccurs="1" name="Identifier" type="xs:string"/>
			<xs:element minOccurs="0" maxOccurs="1" name="Version" type="tns:EFormTemplateVersion"/>
			<xs:element minOccurs="1" maxOccurs="1" name="Status">
				<xs:simpleType>
					<xs:restriction base="xs:string">
						<xs:enumeration value="PUBLISHED"/>
						<xs:enumeration value="INVALIDATED"/>
					</xs:restriction>
				</xs:simpleType>
			</xs:element>
			<xs:element minOccurs="1" maxOccurs="1" name="Changed" type="xs:dateTime"/>
		</xs:sequence>
	</xs:complexType>
	<xs:complexType name="EFormTemplateVersion">
		<xs:sequence>
			<xs:element minOccurs="1" maxOccurs="1" name="Major" type="xs:int"/>
			<xs:element minOccurs="1" maxOccurs="1" name="Minor" type="xs:int"/>
		</xs:sequence>
	</xs:complexType>
</xs:schema>

```


# 6 Zoznam chybových kódov

| **Kód chyby**   | **Verzia**  | **Chybová hláška (SK)**                                 | **Popis chyby**                                                                                                   |
| --------------- | ----------- | ------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------- |
| 06000997	      | 1.5	        | Chybný classname                                        | Chyba vznikne ak rozhranie nepodporuje danú classname obsiahnutú v SKTalk správe.                                 |     
| 06000998	      | 1.5	        | Chybný request                                          | Chyba vznikne ak je SKTalk request nekorektný, resp. obsahuje viac BODY elementov.                                |       
| 06000999	      | 1.5	        | Nešpecifikovaná chyba                                   |	Chyba nastane v prípade výskytu inej nešpecifikovanej udalosti.                                                   |
| 06000799	      | 1.5	        | Vzor už existuje	                                      | Nastáva pri pokuse o vloženie duplicitného vzoru.                                                                 |
| 06000798	      | 1.5	        | Vzor nebol nájdený	                                    | Nastáva v prípade ak je dotaz na nejestvujúci vzor, resp, vzor so stavom ktorý nejestvuje. Môže nastať aj v prípade ak je požiadavka na vizualizáciu zoru, ktorý jestvuje ale nie je publikovaný, resp. zneplatnený.                                                                                                                    |
| 06000797	      | 1.5	        | Zápis vzoru nie je povolený                             |	Chyba nastáva v prípade, ak nie je povolený zápis vzoru - jeho metadát. Toto je napríklad v prípade, ak nastáva pokus o vloženie žiadosti na zmenu metadát pre vzor so stavom „Na schválenie“.                                                                                                                                        |
| 06000796	      | 1.5	        | Súvisiaci dokument pre vzor nebol nájdený	              | Chyba nastáva v prípade, ak sa nepodarí vyhľadať hľadaný súvisiaci dokument .                                     |
| 06000795	      | 1.5	        | Chyba pri pokuse o zápis                                | žiadosti	Chyba nastáva, ak sa nepodarí založiť žiadosť.                                                          |
| 06000794	      | 1.5	        | Prístup zamietnutý	                                    | Chyba nastane, ak nie sú oprávnenia na zápis žiadosti.                                                            |
| 06000793	      | 1.6	        | Subscriber nebol nájdený	                              | Nastane v prípade, ak je volaná služba na zrušenie predplatného, resp. na zmenu endpointu alebo kritérií na vyhľadanie za predpokladu pokiaľ subscriber nie je nájdený.                                                                                                                                                                 |
| 06000792	      | 1.6	        | Subscriber už je zaevidovaný                            |	Nastane v prípade pokusu o vytvorenie predplatného pre subscribera, ktorý už predplatné má.                       |
| 06000791	      | 1.6	        | Požiadavka na subscription nie je definovaná            |	Nastane v prípade, ak nie je vôbec definovaný request pri požiadavke o predplatné.                                |
| 06000790	      | 1.6	        | Požiadavka na subscription nie je kompletne definovaná	| Nastane v prípade, ak nie je pri požiadavke o predplatné definovaný request so všetkými atribútmi.                |
| 06000789	      | 1.6	        | Endpoint pre subscription nebol definovaný              |	Nastane v prípade, ak pri vytváraní predplatného, resp. zmene endpointu nie je definovaný endpoint.               |
| 06000788	      | 1.6	        | Súvisiaca príloha vzoru už existuje                     |	Nastane v prípade, ak je pokus o vloženie duplicitnej súvisiacej prílohy k rovnakému vzoru.                       |
| 06000787	      | 1.6	        | Transformácia sa nepodarila                             |	Nastane v prípade chyby pri transformácii XSLT, resp. FO.                                                         |
| 06000786	      | 1.6	        | Nie je možné nastaviť stav vzoru                        |	Nastáva v prípade, ak nie je možné prostredníctvom SetFormTemplateStatus zmeniť stav vzoru na požadovanú hodnotu. Napríklad, nie je možné vzor publikovať pokiaľ je v stave na schválenie.                                                                                                                                      |
| 06000785	      | 1.7	        | Slovník vzoru nie je k dispozícii	                      | Nastáva v prípade ak nie je pre daný vzor k dispozícii súvisiaci dokument typu CLS_F_XML_DEF.                     |
| 06000784	      | 1.7	        | Slovník IAM nie je k dispozícii	                        | Nastáva v prípade, ak nie je k dispozícii slovník IAM, prípadne ak slovník IAM neobsahuje požadované kľúče        |
| 06000783	      | 1.7	        | Chyba v exporte eformulára do statickej cache	          | Interná chyba, ktorá môže nastať počas exportovania eFormulára po jeho publikovaní do statickej cache.            |
| 06000782	      | 1.7	        | Integračná chyba voči eDesku	                          | Chyba nastáva v prípade problémov integrácie modulu MEF na eDesk.                                                 |
| 06000781	      | 1.7	        | Chyba zápisu	                                          | Nepoužíva sa, bola nahradená viac konkretizujúcimi chybami.                                                       |
| 06000780	      | 1.7	        | Chyba prístupu	                                        | Nepoužíva sa, bola nahradená viac konkretizujúcimi chybami.                                                       |
| 06000779	      | 1.7	        | Chyba komunikácie voči G2G                              |	Nastáva v prípade problémov komunikácie MEF voči G2G.                                                             |
| 06000778	      | 1.7	        | Nepoužíva sa	                                          |                                                                                                                   |
| 06000777	      | 1.7	        | Chyba odosielania notifikácii                           |	Chyba nastáva v prípade problémov s odosielaním notifikácii o nastávajúcom publikovaní , resp. nastávajúcom zneplatnení vzoru eFormulára.                                                                                                                                                                                             |
| 06000776	      | 1.7	        | Požadovaný typ balíka nie je podporovaný	              | Typ balíka XML nie je podporovaný, použite typ balíka .zip.                                                       |
| 06000775	      | 1.7	        | Chyba generovania balíka vzoru eformulára podľa vyhlášky o štandardoch vo formáte ZIP a XML |	Chyba môže nastať v prípade problému počas generovania vzoru eFormulára do balíka podľa prílohy č. 1 Vyhlášky č. 78/2020 Z. z. o štandardoch pre IT VS.                                                                                                                                               |
| 06000774	      | 1.7	        | Chyba generovania metadát vzoru	                        | Chyba môže nastať počas volania služby na poskytovanie meta.xml podľa prílohy č. 1 Vyhlášky č. 78/2020 Z. z. o štandardoch pre IT VS.                                                                                                                                                                                                    |
| 06000773	      | 1.7	        | Chyba generovania manifest.xml	                        | Chyba môže nastať počas volania služby na poskytovanie manifest.xml podľa prílohy č. 1 Vyhlášky č. 78/2020 Z. z. o štandardoch pre IT VS.                                                                                                                                                                                        |
| 06000772	      | 1.7	        | Chyba generovania attachments.xml	                      | Chyba môže nastať počas volania služby na poskytovanie attachments.xml podľa prílohy č. 1 Vyhlášky č. 78/2020 Z. z. o štandardoch pre IT VS                                                                                                                                                                                         |
| 06000771	      | 1.7	        | Chyba počas poskytovania súboru z balíku vzoru eformulára |	Chyba môže nastať počas volania služby na poskytovanie súvisiaceho dokumentu zo vzoru eFormulára podľa prílohy č. 1 Vyhlášky č. 78/2020 Z. z. o štandardoch pre IT VS.                                                                                                                                                            |

> [!NOTE]
> kompletný zoznam aktuálne podporovaných chybových hlásení na ÚPVS je možné získať v dokumente „UPVS_Error_Codes_List_External“ dostupného na stiahnutie na PFP 

# 7	Mapovanie služieb z výzvy

| **Služby z výzvy**                                                                        | **Názov služby**                                                                      |
| ----------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------- |
| **Výzva I.**                                                                              |                                                                                       |
| A.21 Poskytnutie prázdneho eformulára	                                                    | GetEmptyEForm                                                                         |
| A.22 Generovanie eformulára podaného v danom čase	                                        | Zoznam poskytovaných služieb:                                                         |
|                                                                                           | GetEDocFromXML                                                                        |
|                                                                                           | TransformRelatedDocumentFromXML                                                       |
|                                                                                           | TransformRelatedDocumentFromXMLByType                                                 |
| A.23 Vytvorenie elektronického dokumentu	                                                | Zoznam poskytovaných služieb:                                                         |
|                                                                                           | GetEDoc (vizualizácia len eDoc - do PDF)                                              |
|                                                                                           | TransformRelatedDocument (vizualizácia na základe názvov súvisiacich dokumentov)      |
|                                                                                           | TransformRelatedDocumentByType (vizualizácia na základe typov súvisiacich dokumentov) |
| A.24 Poskytnutie vzoru eformulára na aktualizáciu	                                        | GetEFormTemplate alebo kompozitné volanie čiastkových služieb:                        |
|                                                                                           | GetRelatedDocument                                                                    |
|                                                                                           | GetRelatedDocumentByType                                                              |
|                                                                                           | GetRelatedDocumentList                                                                |
|                                                                                           | GetFormTemplateMetaData                                                               |
| A.25 Zápis vzoru eformulára do databázy vzorov	                                          | EFORM_ADD_FORM_TEMPLATE_ASYNC_01                                                      |
|                                                                                           | EFORM_ADD_FORM_TEMPLATE_ASYNC_02                                                      |
| A.26 Zápis stavu vzoru eformulára	                                                        | SetFormTemplateStatus                                                                 |
| A.27 Poskytnutie stavu vzoru eformulára	                                                  | GetFormTemplateStatus                                                                 |
| A.28 Zápis pravidiel pre prístupy k vzorom eformulárom	                                  | EFORM_ADD_ROLE_TO_FORM_TEMPLATE_ASYNC_01                                              |
|                                                                                           | EFORM_REMOVE_ROLE_TO_FORM_TEMPLATE_ASYNC_01                                           |
| A.29 Poskytnutie vzorov eformulárov podľa zadaných kritérií pre vyhľadávanie              | FindFormTemplates                                                                     |
| **Výzva II.**                                                                             |                                                                                       |
| A.27 Poskytnutie predvyplneného eformulára                                                | GetFilledEForm                                                                        |
| A.28 Poskytnutie súvisiacich informácií a dokumentov k vzoru eformulára                   | GetRelatedDocument                                                                    |
|                                                                                           | GetRelatedDocumentByType                                                              |
|                                                                                           | GetRelatedDocumentList                                                                |
| A.29 Zápis súvisiacich informácií a dokumentov k vzoru eformulára do databázy             | EFORM_ADD_FORM_TEMPLATE_ASYNC_01                                                      |
|                                                                                           | EFORM_CHANGE_FORM_TEMPLATE_RELATED_DOCUMENTS_ASYNC_01                                 |
|                                                                                           | EFORM_CHANGE_FORM_TEMPLATE_MEDATADATA_ASYNC_01                                        |
|                                                                                           | EFORM_CHANGE_FORM_TEMPLATE_METADATA_ASYNC_02                                          |
| A.30 Podanie žiadosti o zmenu stavu vzoru eformulára                                      | EFORM_ADD_FORM_TEMPLATE_ASYNC_01                                                      |
|                                                                                           | EFORM_INVALIDATE_FORM_TEMPLATE_ASYNC_01                                               |
|                                                                                           | EFORM_CHANGE_FORM_TEMPLATE_MEDATADATA_ASYNC_01                                        |
| A.31 Poskytnutie nástroja pre definovanie pravidiel postupu spracovania                   | Žiadosť na vloženie vzoru typu POSP (Notepad ++): EFORM_ADD_FORM_TEMPLATE_ASYNC_01    |
| A.32 Zápis pravidiel pre validáciu a postupu spracovania eformulára                       | Žiadosť na vloženie vzoru typu POSP: EFORM_ADD_FORM_TEMPLATE_ASYNC_01                 |
| A.33 Podanie žiadosti o vytvorenie repliky údajov pre podriadený modul správy eformulárov | Zadefinovanie nastavenia predplatiteľa zmien v eForm:                                 |
|                                                                                           | SubscribeForChanges                                                                   |
|                                                                                           | UnsubscribeForChanges                                                                 |
|                                                                                           | GetSubscriberEndpointUrl                                                              |
|                                                                                           | GetSubscriberSearchCriteria                                                           |
|                                                                                           | ChangeSubscriberEndpointUrl                                                           |
|                                                                                           | ChangeSubscriberSearchCriteria                                                        |
|                                                                                           | Informácia o zmene v module eForm: EFORM_SUBSCRIPTION_MESSAGE_ASYNC_01                |
|                                                                                           | Stiahnutie zmien:                                                                     |
|                                                                                           | GetEFormTemplate alebo kompozitné volanie čiastkových služieb:                        |
|                                                                                           | GetRelatedDocument                                                                    |
|                                                                                           | GetRelatedDocumentByType                                                              |
|                                                                                           | GetRelatedDocumentList                                                                |
|                                                                                           | GetFormTemplateMetaData                                                               |
| A.34 Zápis repliky údajov z podriadeného modulu správy eformulárov do MeF                 | EFORM_ADD_FORM_TEMPLATE_ASYNC                                                         |

# 8	Príklad SOAP správy volania eform služby na tokenovom rozhraní USR – externá zbernica

Nasledovný príklad obsahuje kompletnú SOAP správu, vrátane nastaveného SAML assertion.

```

<s:Envelope xmlns:s="http://www.w3.org/2003/05/soap-envelope" xmlns:u="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-utility-1.0.xsd">
	<s:Header>
		<ActivityId CorrelationId="4a081fc8-bed6-4e93-94dd-5627ad2b78e5" xmlns="http://schemas.microsoft.com/2004/09/ServiceModel/Diagnostics">760f5619-f2d7-44da-bfcc-632551a291d9</ActivityId>
		<VsDebuggerCausalityData xmlns="http://schemas.microsoft.com/vstudio/diagnostics/servicemodelsink">uIDPozIGBbWz95BOpdI47GPuPssAAAAAte3vzDWvZEaEiktw1MbY2g/3V+QIbtZJq4NKMn1Ek2kACQAA</VsDebuggerCausalityData>
		<o:Security s:mustUnderstand="1" xmlns:o="http://docs.oasis-open.org/wss/2004/01/oasis-200401-wss-wssecurity-secext-1.0.xsd">
			<u:Timestamp u:Id="_0">
				<u:Created>2014-02-12T19:02:34.822Z</u:Created>
				<u:Expires>2014-02-12T19:07:34.822Z</u:Expires>
			</u:Timestamp>
			<saml:Assertion ID="id-Zrd29MxmuBWPT1DiR8ViC-yZbeE-" IssueInstant="2014-02-12T19:02:22Z" Version="2.0" xmlns:saml="urn:oasis:names:tc:SAML:2.0:assertion" xmlns:dsig="http://www.w3.org/2000/09/xmldsig#" xmlns:enc="http://www.w3.org/2001/04/xmlenc#" xmlns:x500="urn:oasis:names:tc:SAML:2.0:profiles:attribute:X500" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance">
				<saml:Issuer>http://upvsdnv.sk/sts</saml:Issuer>
				<dsig:Signature>
					<dsig:SignedInfo>
						<dsig:CanonicalizationMethod Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
						<dsig:SignatureMethod Algorithm="http://www.w3.org/2000/09/xmldsig#rsa-sha1"/>
						<dsig:Reference URI="#id-Zrd29MxmuBWPT1DiR8ViC-yZbeE-">
							<dsig:Transforms>
								<dsig:Transform Algorithm="http://www.w3.org/2000/09/xmldsig#enveloped-signature"/>
								<dsig:Transform Algorithm="http://www.w3.org/2001/10/xml-exc-c14n#"/>
							</dsig:Transforms>
							<dsig:DigestMethod Algorithm="http://www.w3.org/2000/09/xmldsig#sha1"/>
							<dsig:DigestValue>B4Jjv5hAI2bbtrwU59O99vccIeY=</dsig:DigestValue>
						</dsig:Reference>
					</dsig:SignedInfo>
					<dsig:SignatureValue>pehS+sPnwNgpMJWe+Ho6pRzD4XVhjQ5RX4XuBNg1AZkQ4YVgMLhaEgtqRqjkQ62qRNCMMl8mUcq6vczrzUZGHOxdpKcV3hbVDm2/vWyU7/YkSirb3kToBpKAVCbUhSDldIxSNruHoQOMFc6vDXqAIiT3H1ric3e2Z6Sjl3VvWwo=</dsig:SignatureValue>
					<dsig:KeyInfo>
						<dsig:X509Data>
							<dsig:X509Certificate>MIIB0DCCATmgAwIBAgIBCjANBgkqhkiG9w0BAQQFADANMQswCQYDVQQDEwJhMjAeFw0xMjEwMTUxMDIzMjNaFw0yMjEwMTMxMDIzMjNaMA0xCzAJBgNVBAMTAmEyMIGfMA0GCSqGSIb3DQEBAQUAA4GNADCBiQKBgQCsLuR08/yKfDRMhir5qSUWDAZjhmwoxyxoRLLqtunyd5FfN2HeYwnc+lsze6gi5if2gelEl0aY+qRFYC6epoBA2VaeVa+vxUUo/AECHnLxJgecB5g+nEC3vrfGdli1gKR2p1NVVZRa87I94izUR4OnGn55rsD9QOGINQZYJ//WAQIDAQABo0AwPjAMBgNVHRMBAf8EAjAAMA8GA1UdDwEB/wQFAwMH2AAwHQYDVR0OBBYEFLaXefH8vgDmMb08pnyvFyJpVAS8MA0GCSqGSIb3DQEBBAUAA4GBAEE/MGVHWR8K8P0tcA7gm1BH19TNtRlpdn59UQfyRDhPbCIYnNti41AIalPVvwUQxOSsiqAt3dBdhaLnBY6wRET56Tci5sKVvSAuT85GPqi4zgF1AKfcUGfgGmCT0wSsDvUcV19NoMqKLMN7Ok1DVmq7bx1lD24Z0BWbPgK6RKzx</dsig:X509Certificate>
						</dsig:X509Data>
					</dsig:KeyInfo>
				</dsig:Signature>
				<saml:Subject>
					<saml:NameID Format="" NameQualifier="UpvsFederatedIdentification">TECH.ZBGIS17.DEV</saml:NameID>
					<saml:SubjectConfirmation Method="urn:oasis:names:tc:SAML:2.0:cm:bearer"/>
				</saml:Subject>
				<saml:Conditions NotBefore="2014-02-12T19:02:22Z" NotOnOrAfter="2014-02-13T05:02:22Z"/>
				<saml:AuthnStatement AuthnInstant="2014-02-12T19:02:27Z">
					<saml:AuthnContext>
						<saml:AuthnContextClassRef>urn:oasis:names:tc:SAML:2.0:ac:classes:X509</saml:AuthnContextClassRef>
					</saml:AuthnContext>
				</saml:AuthnStatement>
				<saml:AttributeStatement>
					<saml:Attribute Name="assertionType" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="DelegationType" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="Actor.IdentityType" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="Subject.PreferredLanguage" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="SubjectIDSector" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="Subject.REIdentityId" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="Subject.FormattedName" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="Actor.PreferredLanguage" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="Actor.UPVSIdentityID" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="ActorIDSector" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="Subject.Email" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="SubjectID" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="ActorID" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="Actor.Username" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="Subject.UPVSIdentityID" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="Roles" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="Actor.FormattedName" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
					<saml:Attribute Name="Actor.Email" NameFormat="urn:oasis:names:tc:SAML:2.0:attrname-format:basic">
						<saml:AttributeValue>
							<!-- Removed-->
						</saml:AttributeValue>
					</saml:Attribute>
				</saml:AttributeStatement>
			</saml:Assertion>
		</o:Security>
	</s:Header>
	<s:Body>
		<CallService xmlns="http://schemas.gov.sk/ServiceBus/service/1.0">
			<serviceClass>EFORM_GETRELATEDDOCUMENT_SOAP_V_1_0</serviceClass>
			<serviceParameter i:type="a:GetRelatedDocumentReq" xmlns:i="http://www.w3.org/2001/XMLSchema-instance" xmlns:a="http://schemas.gov.sk/ServiceBusServiceProvider/Ness/eFormProvider/1.0">
				<a:FormTemplate>
					<a:Identifier>ED.DeliveryReportAuthorization</a:Identifier>
					<a:Version>
						<a:Major>1</a:Major>
						<a:Minor>3</a:Minor>
					</a:Version>
				</a:FormTemplate>
				<a:RelatedDocument>form.31.xml</a:RelatedDocument>
			</serviceParameter>
		</CallService>
	</s:Body>
</s:Envelope>

```
