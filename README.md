# 👻 Ghost Bezpečnostní Modul
**PowerShell-založený nástroj pro zpevňování bezpečnosti Windows a Azure**

> **Proaktivní zpevňování bezpečnosti pro Windows koncové body a Azure prostředí.** Ghost poskytuje PowerShell-založené funkce zpevňování, které mohou pomoci snížit běžné vektory útoků zakázáním nepotřebných služeb a protokolů.

## ⚠️ Důležitá prohlášení o vyloučení

**TESTOVÁNÍ JE VYŽADOVÁNO**: Ghost vždy nejprve testujte v ne-produkčních prostředích. Zakázání služeb může ovlivnit legitimní obchodní funkce.

**ŽÁDNÉ ZÁRUKY**: Ačkoli Ghost cílí na běžné vektory útoků, žádný bezpečnostní nástroj nemůže zabránit všem útokům. Toto je jedna komponenta komplexní bezpečnostní strategie.

**OPERAČNÍ DOPAD**: Některé funkce mohou ovlivnit funkcionalitu systému. Před nasazením pečlivě zkontrolujte každé nastavení.

**PROFESIONÁLNÍ HODNOCENÍ**: Pro produkční prostředí se poraďte s bezpečnostními odborníky, abyste zajistili, že nastavení odpovídají potřebám vaší organizace.

## 📊 Bezpečnostní krajina

Škody od ransomware dosáhly **57 miliard dolarů v roce 2025**, přičemž výzkumy ukazují, že mnoho úspěšných útoků využívá základní Windows služby a chybné konfigurace. Běžné vektory útoků zahrnují:

- **90% ransomware incidentů** zahrnuje zneužití RDP
- **SMBv1 zranitelnosti** umožnily útoky jako WannaCry a NotPetya
- **Makra dokumentů** zůstávají primární metodou doručování malware
- **USB-založené útoky** nadále cílí na vzduchem izolované sítě
- **Zneužívání PowerShell** se výrazně zvýšilo v posledních letech

## 🛡️ Ghost bezpečnostní funkce

Ghost poskytuje **16 funkcí zpevňování Windows** plus **Azure bezpečnostní integrace**:

### Zpevňování Windows koncových bodů

| Funkce | Účel | Úvahy |
|--------|------|-------|
| `Set-RDP` | Spravuje přístup ke vzdálené ploše | Může ovlivnit vzdálenou správu |
| `Set-SMBv1` | Řídí zastaralý SMB protokol | Vyžadován pro velmi staré systémy |
| `Set-AutoRun` | Řídí AutoPlay/AutoRun | Může ovlivnit pohodlí uživatele |
| `Set-USBStorage` | Omezuje USB úložná zařízení | Může ovlivnit legitimní použití USB |
| `Set-Macros` | Řídí spouštění Office maker | Může ovlivnit dokumenty s povolenými makry |
| `Set-PSRemoting` | Spravuje PowerShell vzdálené připojení | Může ovlivnit vzdálenou správu |
| `Set-WinRM` | Řídí Windows Remote Management | Může ovlivnit vzdálenou správu |
| `Set-LLMNR` | Spravuje protokol rozlišování jmen | Obvykle bezpečné k zakázání |
| `Set-NetBIOS` | Řídí NetBIOS přes TCP/IP | Může ovlivnit zastaralé aplikace |
| `Set-AdminShares` | Spravuje administrativní sdílení | Může ovlivnit vzdálený přístup k souborům |
| `Set-Telemetry` | Řídí sběr dat | Může ovlivnit diagnostické schopnosti |
| `Set-GuestAccount` | Spravuje hostský účet | Obvykle bezpečné k zakázání |
| `Set-ICMP` | Řídí ping odpovědi | Může ovlivnit síťovou diagnostiku |
| `Set-RemoteAssistance` | Spravuje vzdálenou pomoc | Může ovlivnit operace helpdesku |
| `Set-NetworkDiscovery` | Řídí síťové objevování | Může ovlivnit procházení sítě |
| `Set-Firewall` | Spravuje Windows Firewall | Kritické pro síťovou bezpečnost |

### Azure Cloud bezpečnost

| Funkce | Účel | Požadavky |
|--------|------|-----------|
| `Set-AzureSecurityDefaults` | Povoluje základní Azure AD bezpečnost | Microsoft Graph oprávnění |
| `Set-AzureConditionalAccess` | Konfiguruje přístupové politiky | Azure AD P1/P2 licencování |
| `Set-AzurePrivilegedUsers` | Audituje privilegované účty | Global Admin oprávnění |

### Možnosti podnikového nasazení

| Metoda | Případ použití | Požadavky |
|--------|----------------|-----------|
| **Přímé spuštění** | Testování, malá prostředí | Lokální admin práva |
| **Group Policy** | Doménová prostředí | Domain admin, GP správa |
| **Microsoft Intune** | Cloud-spravovaná zařízení | Intune licencování, Graph API |

## 🚀 Rychlý start

### Bezpečnostní hodnocení
```powershell
# Načtěte Ghost modul
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')

# Zkontrolujte současnou bezpečnostní pozici
Get-Ghost
```

### Základní zpevňování (nejprve testujte)
```powershell
# Základní zpevňování - nejprve testujte v laboratorním prostředí
Set-Ghost -SMBv1 -AutoRun -Macros

# Zkontrolujte změny
Get-Ghost
```

### Podnikové nasazení
```powershell
# Group Policy nasazení (doménová prostředí)
Set-Ghost -SMBv1 -AutoRun -GroupPolicy

# Intune nasazení (cloud-spravovaná zařízení)
Set-Ghost -SMBv1 -RDP -USBStorage -Intune
```

## 📋 Metody instalace

### Možnost 1: Přímé stažení (testování)
```powershell
IEX(Invoke-WebRequest 'https://raw.githubusercontent.com/jimrtyler/Ghost/main/Ghost.ps1')
```

### Možnost 2: Instalace modulu
```powershell
# Instalujte z PowerShell Gallery (když bude k dispozici)
Install-Module Ghost -Scope CurrentUser
Import-Module Ghost
```

### Možnost 3: Podnikové nasazení
```powershell
# Zkopírujte do síťového umístění pro Group Policy nasazení
# Nakonfigurujte Intune PowerShell skripty pro cloud nasazení
```

## 💼 Příklady případů použití

### Malý podnik
```powershell
# Základní ochrana s minimálním dopadem
Set-Ghost -SMBv1 -AutoRun -Macros -ICMP
```

### Zdravotnické prostředí
```powershell
# HIPAA-zaměřené zpevňování
Set-Ghost -SMBv1 -RDP -USBStorage -AdminShares -Telemetry
```

### Finanční služby
```powershell
# Vysoce bezpečnostní konfigurace
Set-Ghost -RDP -SMBv1 -AutoRun -USBStorage -Macros -PSRemoting -AdminShares
```

### Cloud-First organizace
```powershell
# Intune-spravované nasazení
Connect-IntuneGhost -Interactive
Set-Ghost -SMBv1 -RDP -AutoRun -Macros -Intune
```

## 🔍 Podrobnosti funkcí

### Základní funkce zpevňování

#### Síťové služby
- **RDP**: Blokuje přístup ke vzdálené ploše nebo randomizuje port
- **SMBv1**: Zakáže zastaralý protokol sdílení souborů
- **ICMP**: Brání ping odpovědím pro průzkum
- **LLMNR/NetBIOS**: Blokuje zastaralé protokoly rozlišování jmen

#### Bezpečnost aplikací
- **Makra**: Zakáže spouštění maker v Office aplikacích
- **AutoRun**: Brání automatickému spuštění z vyměnitelných médií

#### Vzdálená správa
- **PSRemoting**: Zakáže PowerShell vzdálené relace
- **WinRM**: Zastaví Windows Remote Management
- **Remote Assistance**: Blokuje připojení vzdálené pomoci

#### Řízení přístupu
- **Admin Shares**: Zakáže C$, ADMIN$ sdílení
- **Guest Account**: Zakáže přístup hostského účtu
- **USB Storage**: Omezuje použití USB zařízení

### Azure integrace
```powershell
# Připojte se k Azure tenant
Connect-AzureGhost -Interactive

# Povolte výchozí nastavení bezpečnosti
Set-AzureSecurityDefaults -Enable

# Nakonfigurujte podmíněný přístup
Set-AzureConditionalAccess -BlockLegacyAuth -RequireMFA

# Auditujte privilegované uživatele
Set-AzurePrivilegedUsers -AuditOnly
```

### Intune integrace (nové ve v2)
```powershell
# Připojte se k Intune
Connect-IntuneGhost -Interactive

# Nasaďte prostřednictvím Intune politik
Set-IntuneGhost -Settings @{
    RDP = $true
    SMBv1 = $true
    USBStorage = $true
    Macros = $true
}
```

## ⚠️ Důležité úvahy

### Požadavky na testování
- **Laboratorní prostředí**: Nejprve testujte všechna nastavení v izolovaném prostředí
- **Postupné nasazení**: Postupně nasazujte pro identifikaci problémů
- **Plán návratu**: Ujistěte se, že můžete vrátit změny v případě potřeby
- **Dokumentace**: Zaznamenejte, která nastavení fungují pro vaše prostředí

### Potenciální dopad
- **Produktivita uživatele**: Některá nastavení mohou ovlivnit denní pracovní toky
- **Zastaralé aplikace**: Starší systémy mohou vyžadovat určité protokoly
- **Vzdálený přístup**: Zvažte dopad na legitimní vzdálenou správu
- **Obchodní procesy**: Ověřte, že nastavení neporuší kritické funkce

### Bezpečnostní omezení
- **Obrána do hloubky**: Ghost je jedna vrstva bezpečnosti, ne kompletní řešení
- **Kontinuální správa**: Bezpečnost vyžaduje kontinuální monitorování a aktualizace
- **Uživatelské školení**: Technické kontroly musí být spárovány s bezpečnostním povědomím
- **Evoluce hrozeb**: Nové metody útoků mohou obejít současnou ochranu

## 🎯 Příklady scénářů útoků

Zatímco Ghost cílí na běžné vektory útoků, specifická prevence závisí na správné implementaci a testování:

### WannaCry-styl útoky
- **Zmírnění**: `Set-Ghost -SMBv1` zakáže zranitelný protokol
- **Úvaha**: Ujistěte se, že žádný zastaralý systém nevyžaduje SMBv1

### RDP-založený ransomware
- **Zmírnění**: `Set-Ghost -RDP` blokuje přístup ke vzdálené ploše
- **Úvaha**: Může vyžadovat alternativní metody vzdáleného přístupu

### Malware založený na dokumentech
- **Zmírnění**: `Set-Ghost -Macros` zakáže spouštění maker
- **Úvaha**: Může ovlivnit legitimní dokumenty s povolenými makry

### USB-doručené hrozby
- **Zmírnění**: `Set-Ghost -USBStorage -AutoRun` omezuje USB funkcionalitu
- **Úvaha**: Může ovlivnit legitimní použití USB zařízení

## 🏢 Podnikové funkce

### Podpora Group Policy
```powershell
# Aplikujte nastavení prostřednictvím Group Policy registru
Set-Ghost -SMBv1 -RDP -AutoRun -GroupPolicy

# Nastavení se aplikují doménově po GP aktualizaci
gpupdate /force
```

### Microsoft Intune integrace
```powershell
# Vytvořte Intune politiky pro Ghost nastavení
Set-IntuneGhost -Settings $GhostSettings -Interactive

# Politiky se automaticky nasazují na spravovaná zařízení
```

### Hlášení souladu
```powershell
# Generujte hlášení bezpečnostního hodnocení
Get-Ghost | Export-Csv -Path "SecurityAudit-$(Get-Date -Format 'yyyy-MM-dd').csv"

# Azure hlášení bezpečnostní pozice
Get-AzureGhost | Out-File "AzureSecurityReport.txt"
```

## 📚 Nejlepší praktiky

### Před-nasazení
1. **Dokumentujte současný stav**: Spusťte `Get-Ghost` před změnami
2. **Důkladně testujte**: Validujte v ne-produkčním prostředí
3. **Plánujte návrat**: Vědci, jak vrátit každé nastavení
4. **Přezkoumání zúčastněných stran**: Ujistěte se, že obchodní jednotky schvalují změny

### Během nasazení
1. **Postupný přístup**: Nasazujte nejprve do pilotních skupin
2. **Monitorujte dopad**: Sledujte uživatelské stížnosti nebo systémové problémy
3. **Dokumentujte problémy**: Zaznamenejte všechny problémy pro budoucí reference
4. **Komunikujte změny**: Informujte uživatele o bezpečnostních vylepšeních

### Po-nasazení
1. **Pravidelné hodnocení**: Periodicky spouštějte `Get-Ghost` pro ověření nastavení
2. **Aktualizujte dokumentaci**: Udržujte bezpečnostní konfigurace aktuální
3. **Přezkoumejte efektivnost**: Monitorujte bezpečnostní incidenty
4. **Kontinuální zlepšování**: Upravte nastavení na základě hrozby krajiny

## 🔧 Řešení problémů

### Běžné problémy
- **Chyby oprávnění**: Ujistěte se o zvýšené PowerShell relaci
- **Závislosti služeb**: Některé služby mohou mít závislosti
- **Kompatibilita aplikací**: Testujte s obchodními aplikacemi
- **Síťové připojení**: Ověřte, že vzdálený přístup stále funguje

### Možnosti obnovy
```powershell
# Znovu povolte specifické služby v případě potřeby
Set-RDP -Enable
Set-SMBv1 -Enable
Set-AutoRun -Enable
Set-Macros -Enable
```

## 👨‍💻 O autorovi

**Jim Tyler** - Microsoft MVP pro PowerShell
- **YouTube**: [@PowerShellEngineer](https://youtube.com/@PowerShellEngineer) (10 000+ odběratelů)
- **Newsletter**: [PowerShell.News](https://powershell.news) - Týdenní bezpečnostní inteligence
- **Autor**: "PowerShell for Systems Engineers"
- **Zkušenosti**: Desetiletí PowerShell automatizace a Windows bezpečnosti

## 📄 Licence a prohlášení o vyloučení

### MIT licence
Ghost je poskytován pod MIT licencí pro bezplatné použití, úpravy a distribuci.

### Bezpečnostní prohlášení o vyloučení
- **Žádná záruka**: Ghost je poskytován "jak je" bez záruky jakéhokoli druhu
- **Testování vyžadováno**: Vždy nejprve testujte v ne-produkčních prostředích
- **Profesionální vedení**: Poraďte se s bezpečnostními odborníky pro produkční nasazení
- **Operační dopad**: Autoři nejsou odpovědní za žádná operační přerušení
- **Komplexní bezpečnost**: Ghost je jedna komponenta kompletní bezpečnostní strategie

### Podpora
- **GitHub problémy**: [Nahlaste chyby nebo požádejte o funkce](https://github.com/jimrtyler/Ghost/issues)
- **Dokumentace**: Použijte `Get-Help <function> -Full` pro podrobnou nápovědu
- **Komunita**: PowerShell a bezpečnostní komunitní fóra

---

**🔐 Posílejte svou bezpečnostní pozici s Ghost - ale vždy nejprve testujte.**

```powershell
# Začněte s hodnocením, ne s předpoklady
Get-Ghost
```

**⭐ Označte tento repozitář hvězdičkou, pokud Ghost pomáhá zlepšit vaši bezpečnostní pozici!**