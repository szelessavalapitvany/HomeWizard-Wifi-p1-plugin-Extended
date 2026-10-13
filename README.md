# HomeWizard Wi-Fi P1 Plugin Extended for Domoticz

**What is it for?** This plugin exposes detailed electricity-meter readings in Domoticz so you can understand not only *how much* electricity your home uses, but also *when*, *on which phase*, and—in supported installations—how much is exported to the grid.

Python plugin for Domoticz to integrate the HomeWizard Wi-Fi P1 smart energy meter, including imported and exported energy, electricity tariffs, instantaneous power, voltage, current, reactive energy and other detailed electrical measurements.

This project extends the original HomeWizard P1 plugin with additional measurements, improved device handling and multi-language support. **You do not need to use every device it creates.** Basic energy monitoring works with just a few readings; the extra sensors are intended for diagnostics, automation and more advanced energy analysis.

## Features

Compared to the original HomeWizard Wi-Fi P1 plugin, this Extended version provides:

- Estimated power allocation for each electrical phase (L1, L2, L3)
- Per-phase voltage and current monitoring
- Imported and exported energy measurements by tariff
- Instantaneous imported and exported power
- Reactive energy measurements and power factor values
- Network frequency monitoring
- Active electricity tariff information
- Better handling of import/export values and tariffs
- More consistent device mapping in Domoticz
- Additional calculated values where available
- Improved stability and error handling
- Multi-language support using Domoticz language settings
- Cleaner and more structured device creation
- Designed for reliable long-term operation

The availability of individual measurements depends on the connected electricity meter and the information provided by the HomeWizard P1 interface.

The plugin aims to provide a more complete integration of the HomeWizard P1 meter into Domoticz.

## Why use the Extended plugin?

For a typical household, the most useful data are the current imported/exported power, accumulated energy consumption, and—if applicable—solar export. These can be used for monitoring and Domoticz automation. The extra measurements become useful if you want to:

- **Identify peak loads:** see when the household draws significant power and use Domoticz history to investigate changes.
- **Understand three-phase installations:** compare the voltage, current and power on L1, L2 and L3 to spot unusually uneven loading.
- **Monitor solar export:** distinguish electricity being drawn from the grid from electricity sent back to it, if reported by the meter.
- **Use tariffs in reports:** examine imported or exported energy counters by tariff, where your meter provides this information.
- **Support troubleshooting:** observe voltage, frequency, reactive values or power factor when investigating electrical-system behaviour.

The plugin is a monitoring/data source, **not** a replacement for certified electrical testing, safety devices or billing information from your energy provider. Extra readings do not necessarily imply a problem, and not every household needs them.

## Understanding the measurements

The table explains the **meaning and practical relevance** of each measurement group. Exact Domoticz device names, combinations and availability depend on the meter data and plugin version.

| Measurement in Domoticz | Unit | What it means | When it is useful |
| --- | --- | --- | --- |
| Total imported energy | kWh | Electricity accumulated while drawing from the grid | Long-term grid consumption and reporting |
| Total exported energy | kWh | Electricity accumulated while feeding into the grid | Monitoring solar or other generation exported to the grid |
| Imported/exported energy by tariff (T1–T4 where available) | kWh | Separate cumulative counters supplied for tariff periods | Comparing consumption across tariff registers; not a monetary cost calculation |
| Current imported power | W or kW | Instantaneous power being taken from the grid | Watching live demand and triggering automation |
| Current exported power | W or kW | Instantaneous power being sent to the grid | Identifying surplus generation where export is available |
| Per-phase power (L1, L2, L3) | kW | **Estimated** phase power calculated by the plugin, not a direct per-phase directional meter reading | Indication of phase loading; use with caution |
| Per-phase voltage (L1, L2, L3) | V | Electrical voltage on each phase | Observing voltage variations over time |
| Per-phase current (L1, L2, L3) | A | Current flowing on each phase | Estimating phase loading and identifying trends |
| Reactive energy / reactive power | kvarh / kvar | Reactive electrical energy or instantaneous reactive power, using distinct units | Advanced electrical analysis; usually not needed for basic household monitoring |
| Power factor | dimensionless | Relationship between active and apparent power | Advanced diagnosis of electrical loads; values require context |
| Grid frequency | Hz | Frequency of the AC supply | Observing grid frequency, when the meter reports it |
| Active tariff | tariff/register identifier | Tariff register indicated by the electricity meter | Identifying which register is active, if supported |

**Import vs export:** Import means electricity flowing *from the grid into the home*; export means electricity flowing *from the home back to the grid*. The two energy totals are distinct cumulative counters. A meter may report zero export or omit export data entirely.

**Power vs energy:** Power (W/kW) tells you what is happening *right now*. Energy (Wh/kWh) accumulates over time. For example, a constant 1 kW import maintained for one hour adds approximately 1 kWh to the imported-energy counter.

**Three phases:** In three-phase installations, L1, L2 and L3 are separate phases. Looking at them individually can reveal whether one phase carries significantly more load than the others. In single-phase installations, L2/L3 values may be absent.

**Not all devices are necessary:** Start with total import, total export (if applicable), and current power. Enable or display additional devices only when they answer a specific question. An unavailable or zero reading is not by itself proof of a plugin fault; first check which fields the meter actually exposes.

> **Code compatibility:** The descriptions of Units 1–3 and 26–29 reflect the two fixes agreed during review. Apply those fixes to `plugin.py` before publishing this README as documentation of the installed code. The original uploaded `plugin.py` still contained the old implementation.

## Complete Domoticz device reference (plugin.py)

The **Unit** column is the plugin-local unit number, **not** the global Domoticz IDX. Device names below are the English keys; Domoticz may translate them according to its language settings.

### Energy

| Unit | Device name | Unit / format | What it represents |
| ---: | --- | --- | --- |
| 1 | Total imported energy | W;Wh | Total imported energy: instantaneous import power (W) and cumulative imported energy (Wh). |
| 2 | Total exported energy | W;Wh | Total exported energy: instantaneous export power (W) and cumulative exported energy (Wh). |
| 3 | Total active energy | W;Wh | Total bidirectional throughput: imported + exported power (W) and imported + exported energy (Wh). |
| 4 | Imported energy tariff 1 | kWh | Imported cumulative energy for the indicated tariff register. |
| 5 | Imported energy tariff 2 | kWh | Imported cumulative energy for the indicated tariff register. |
| 6 | Imported energy tariff 3 | kWh | Imported cumulative energy for the indicated tariff register. |
| 7 | Imported energy tariff 4 | kWh | Imported cumulative energy for the indicated tariff register. |
| 8 | Exported energy tariff 1 | kWh | Exported cumulative energy for the indicated tariff register. |
| 9 | Exported energy tariff 2 | kWh | Exported cumulative energy for the indicated tariff register. |
| 10 | Exported energy tariff 3 | kWh | Exported cumulative energy for the indicated tariff register. |
| 11 | Exported energy tariff 4 | kWh | Exported cumulative energy for the indicated tariff register. |
| 12 | Reactive imported energy | kvarh | Cumulative reactive energy received / delivered. |
| 13 | Reactive exported energy | kvarh | Cumulative reactive energy received / delivered. |
| 14 | Reactive energy QI | kvarh | Cumulative reactive energy in quadrant QI–QIV. |
| 15 | Reactive energy QII | kvarh | Cumulative reactive energy in quadrant QI–QIV. |
| 16 | Reactive energy QIII | kvarh | Cumulative reactive energy in quadrant QI–QIV. |
| 17 | Reactive energy QIV | kvarh | Cumulative reactive energy in quadrant QI–QIV. |

### Power

| Unit | Device name | Unit / format | What it represents |
| ---: | --- | --- | --- |
| 18 | Instantaneous imported power | kW | Direct instantaneous import / export reading. |
| 19 | Instantaneous exported power | kW | Direct instantaneous import / export reading. |
| 20 | Imported power L1 | kW | Estimated from U × I × power factor, then scaled to whole-meter power. |
| 21 | Imported power L2 | kW | Estimated from U × I × power factor, then scaled to whole-meter power. |
| 22 | Imported power L3 | kW | Estimated from U × I × power factor, then scaled to whole-meter power. |
| 23 | Exported power L1 | kW | Estimated from U × I × power factor, then scaled to whole-meter power. |
| 24 | Exported power L2 | kW | Estimated from U × I × power factor, then scaled to whole-meter power. |
| 25 | Exported power L3 | kW | Estimated from U × I × power factor, then scaled to whole-meter power. |
| 26 | Reactive power QI | kvarh* | Instantaneous reactive power, but the plugin currently labels it kvarh (energy). |
| 27 | Reactive power QII | kvarh* | Instantaneous reactive power, but the plugin currently labels it kvarh (energy). |
| 28 | Reactive power QIII | kvarh* | Instantaneous reactive power, but the plugin currently labels it kvarh (energy). |
| 29 | Reactive power QIV | kvarh* | Instantaneous reactive power, but the plugin currently labels it kvarh (energy). |

### Electrical quantities

| Unit | Device name | Unit / format | What it represents |
| ---: | --- | --- | --- |
| 30 | Voltage L1 | V | Measured voltage of the indicated phase. |
| 31 | Voltage L2 | V | Measured voltage of the indicated phase. |
| 32 | Voltage L3 | V | Measured voltage of the indicated phase. |
| 33 | Current L1 | A | Measured current of the indicated phase. |
| 34 | Current L2 | A | Measured current of the indicated phase. |
| 35 | Current L3 | A | Measured current of the indicated phase. |
| 36 | Current Bl1 | A | Calculated quadrature/reactive current from current and power factor. |
| 37 | Current Bl2 | A | Calculated quadrature/reactive current from current and power factor. |
| 38 | Current Bl3 | A | Calculated quadrature/reactive current from current and power factor. |
| 39 | Network frequency | Hz | Measured mains frequency. |
| 40 | Power factor | cos φ | Total or per-phase power factor. |
| 41 | Power factor L1 | cos φ | Total or per-phase power factor. |
| 42 | Power factor L2 | cos φ | Total or per-phase power factor. |
| 43 | Power factor L3 | cos φ | Total or per-phase power factor. |

### Status and combined meter

| Unit | Device name | Unit / format | What it represents |
| ---: | --- | --- | --- |
| 44 | Meter serial number | text | Meter identifier reported in the telegram. |
| 45 | Circuit breaker status | On/Off | Breaker state from meter telegram (ON → On, else Off). |
| 46 | Active tariff | text | Current tariff code, usually 0001–0004. |
| 47 | Current - daily consumption | P1 smart meter | Domoticz six-field P1 smart-meter device: T1/T2 import, T1/T2 export (Wh), instantaneous import/export (W); displays daily use via Domoticz. |

### Important interpretation notes

- **Units 1–3:** after the agreed fix, all three use Domoticz `Type=113, Subtype=0` and the `power_W;energy_Wh` format. Unit 1 is import, Unit 2 export, and Unit 3 is their **sum (bidirectional throughput)**, not net consumption. The existing translated name “Total active energy” is retained for compatibility, but its meaning is the combined throughput.
- **Units 20–25:** per-phase imported/exported power is **estimated**, not read from separate per-phase import/export registers. It is calculated from voltage, current and power factor and scaled to the meter-wide imported/exported power. In some circumstances, especially where a signed power factor is unavailable, the estimate may be zero or unreliable.
- **Units 26–29:** the corrected custom unit is `kVAr`, consistent with instantaneous reactive power from `5.7.0`–`8.7.0`. Existing devices may still retain the old `kVArh` label until their Domoticz Options are updated.
- **Units 36–38:** reactive current component is a calculation, not a separate current measurement.
- **OBIS inputs:** the plugin expects the required OBIS fields to be present in the P1 telegram. No additional missing-field handling was added. The parser retains its existing `0.0` fallback; this is a technical limitation, not a guarantee that an absent field was measured as zero.
- **Unit 47:** only tariffs 1 and 2 are used in the combined six-field Domoticz P1 device. Tariffs 3 and 4, if present, remain in separate devices. The daily value is calculated/displayed by Domoticz, rather than coming directly from a daily counter in the telegram.
- **Device creation:** the plugin currently creates all 47 devices, even if a particular meter does not supply every field. Users can choose which devices to display or use.


## Example uses in Domoticz

1. **Live household load:** place current import power on your dashboard to see how an EV charger, water heater or other large load changes demand.
2. **Solar monitoring:** track current export and the cumulative exported-energy counter to see when and how much energy is sent to the grid, if supported.
3. **Three-phase load overview:** compare L1/L2/L3 currents or power over time to identify sustained imbalances worth investigating.

These are monitoring examples, not preconfigured automations. Device data and suitable thresholds vary by installation.

## Screenshots

### Dashboard – Energy monitoring

The plugin integrates HomeWizard P1 energy measurements directly into the Domoticz dashboard.

The dashboard provides a quick overview of current power consumption, daily energy usage and the active electricity tariff.

![HomeWizard P1 Extended - Domoticz Dashboard](images/dashboard.png)

### Utility – Detailed electrical measurements

The Extended plugin creates a comprehensive set of Domoticz devices for detailed electricity monitoring.

Available measurements include imported and exported energy by tariff, instantaneous power, per-phase voltage and current, reactive energy, power factor and network frequency.

These measurements make it possible to monitor the electrical network in significantly greater detail.

![HomeWizard P1 Extended - Detailed Utility Sensors](images/utility.png)

### Hardware – Plugin configuration

The plugin can be configured directly from the Domoticz hardware settings.

The configuration includes the Domoticz connection parameters, HomeWizard P1 IP address and data refresh interval.

![HomeWizard P1 Extended - Hardware Configuration](images/hardware.png)

## Prerequisites

- Domoticz 2022.1 or newer
- Domoticz with Python plugin support enabled
- HomeWizard Wi-Fi P1 meter connected to the local network
- Network connectivity between Domoticz and the HomeWizard device
- HomeWizard local API enabled, where required by the device firmware

For information about Python plugins, see:

[Domoticz Python Plugins Documentation](https://www.domoticz.com/wiki/Using_Python_plugins)

## Installation

The plugin can be installed manually or by using the [Domoticz Plugins Manager](https://github.com/stas-demydiuk/domoticz-plugins-manager).

### Manual installation

**1. Clone the repository into the Domoticz plugins directory:**

```bash
cd domoticz/plugins
git clone https://github.com/szelessavalapitvany/HomeWizard-Wifi-p1-plugin-Extended
```

Adjust the directory path to match your Domoticz installation.

**2. Restart Domoticz.**

**3. Enable "Accept new Hardware Devices"** in the Domoticz settings.

**4. Open Setup → Hardware.**

**5. Add a new hardware device** using the type:

`Home Wizard Electric P1 meter extended`

**6. Configure the plugin parameters:**

- **Name:** HomeWizard Extended
- **Domoticz IP Address:** 127.0.0.1 (for a local installation)
- **Port:** 8080 (or your configured Domoticz HTTP port)
- **HomeWizard P1 IP Address:** The IP address of your HomeWizard device
- **Data interval – Frissítés:** Select the required data refresh interval
- **Debug:** Enable only when diagnostic information is needed

**7. Click Add** to create the hardware device.

The plugin will create the supported devices in Domoticz and update their measurements periodically.

The available devices depend on the capabilities of the connected smart meter.

## Plugin update

To update the plugin to the latest version:

**1. Open the plugin directory and download the latest changes:**

```bash
cd domoticz/plugins/HomeWizard-Wifi-p1-plugin-Extended
git pull
```

**2. Restart Domoticz.**

### Local modifications

If you modified the plugin files and `git pull` fails because of local changes, you can temporarily save those changes:

```bash
git stash
git pull
```

If you want to restore your local modifications afterward:

```bash
git stash pop
```

Be aware that restoring local modifications may cause merge conflicts.

## Plugin downgrade

If a previous version is required, the repository can be restored to an earlier commit.

**1. Open the plugin directory:**

```bash
cd domoticz/plugins/HomeWizard-Wifi-p1-plugin-Extended
```

**2. Review the available commits:**

```bash
git log --oneline
```

**3. Reset to the required version:**

```bash
git reset --hard <commit_hash>
```

Replace `<commit_hash>` with the selected commit identifier.

**Warning:** `git reset --hard` discards uncommitted changes to tracked files. Back up any local modifications before running this command.

**4. Restart Domoticz.**

Alternatively, disabling and re-enabling the plugin under Setup → Hardware may be sufficient in some situations.

Browser cache cleanup may also be required after interface-related changes.

## Language support

The plugin supports multiple languages and uses the language configured in Domoticz for supported device descriptions.

This allows users to integrate HomeWizard P1 measurements into their existing Domoticz installation without requiring a separate language-specific plugin version.

## Notes

- The HomeWizard P1 device should preferably have a fixed IP address or a DHCP reservation.
- All communication with the HomeWizard P1 meter takes place through the local network.
- Supported measurements vary depending on the smart meter model and its available P1 data.
- Some values may not be available from every electricity meter.
- Enable Debug mode when troubleshooting communication or device creation problems.

## Project

Developed and maintained by **Szélessáv Közhasznú Alapítvány**.

Website: [Szélessáv Műhely](https://www.szelessavmuhely.hu)

GitHub: [HomeWizard-Wifi-p1-plugin-Extended](https://github.com/szelessavalapitvany/HomeWizard-Wifi-p1-plugin-Extended)

---

# HomeWizard Wi-Fi P1 Plugin Extended – Magyar leírás

**Mire való?** A plugin a villamos fogyasztásmérő részletes adatait jeleníti meg a Domoticzban. Így nemcsak azt követhetjük, mennyi áramot fogyasztottunk, hanem azt is, hogy mikor, melyik fázison jelentkezett a terhelés, és – megfelelő mérő esetén – mennyi energiát tápláltunk vissza a hálózatba.

Python plugin Domoticzhoz, amely a HomeWizard Wi-Fi P1 okosmérő integrációját valósítja meg.

A plugin segítségével megjeleníthetők az importált és exportált energiamennyiségek, az aktuális teljesítmény, az egyes tarifák, a fázisonkénti feszültség és áramerősség, a meddő energia, valamint további részletes villamosenergia-hálózati adatok.

Ez a projekt az eredeti HomeWizard P1 plugin továbbfejlesztett változata. **Nem szükséges az összes létrehozott eszközt használni.** Az alapvető fogyasztásfigyeléshez néhány érték elegendő; a többi adat részletesebb elemzést, hibakeresést és automatizálást segíthet.

## Funkciók

Az eredeti HomeWizard Wi-Fi P1 pluginhoz képest a kibővített változat az alábbi többletfunkciókat biztosítja:

- Becsült fázisonkénti teljesítmény (L1, L2, L3)
- Fázisonkénti feszültség- és áramerősség-értékek
- Importált és exportált energia mérése tarifánként
- Pillanatnyi vételezett és visszatáplált teljesítmény
- Meddőenergia-adatok és teljesítménytényezők
- Hálózati frekvencia figyelése
- Aktuális villamosenergia-tarifa megjelenítése
- Pontosabb import/export és tarifakezelés
- Konzisztensebb és átláthatóbb eszközkezelés a Domoticzban
- További számított értékek, ahol rendelkezésre állnak
- Stabilabb működés és jobb hibakezelés
- Többnyelvű támogatás a Domoticz nyelvi beállításainak felhasználásával
- Letisztultabb és strukturáltabb eszközlétrehozás
- Hosszú távú, megbízható működésre tervezve

Az egyes mérési adatok elérhetősége a csatlakoztatott villamos fogyasztásmérő típusától és a HomeWizard P1 interfész által szolgáltatott információktól függ.

A plugin célja, hogy a HomeWizard P1 mérő teljesebb és részletesebb integrációját biztosítsa a Domoticz rendszerben.

## Miért lehet hasznos a kibővített plugin?

Egy átlagos háztartásban a pillanatnyi vételezett vagy visszatáplált teljesítmény és az összesített energiamennyiség a legfontosabb. A további mérések akkor értékesek, ha:

- **A fogyasztási csúcsokat keresed:** követhető, mikor nő meg a hálózatból felvett teljesítmény.
- **Háromfázisú hálózatod van:** összehasonlítható az L1, L2 és L3 fázis feszültsége, árama és teljesítménye.
- **Napelemes rendszered van:** elkülöníthető a hálózatból vételezett és a hálózatba visszatáplált energia, ha a mérő ezt jelenti.
- **Tarifánként szeretnél adatokat gyűjteni:** külön vizsgálhatók a mérő által biztosított tarifaregiszterek.
- **Részletes hibakeresést végzel:** a feszültség, frekvencia, meddő értékek és teljesítménytényező további támpontot adhatnak.

A plugin **monitorozásra** szolgál. Nem helyettesít hiteles villamos mérést, érintésvédelmi vizsgálatot vagy a szolgáltató elszámolási adatait. Nem minden mérési adat fontos minden felhasználónak.

## A mérési adatok jelentése és gyakorlati haszna

A táblázat a mérési csoportokat magyarázza el. Az eszközök pontos neve és elérhetősége a mérőtől és a plugin verziójától függ.

| Mérési adat | Mértékegység | Mit jelent? | Mire használható? |
| --- | --- | --- | --- |
| Összes importált energia | kWh | A hálózatból vételezett összes energia | Hosszú távú fogyasztáskövetés |
| Összes exportált energia | kWh | A hálózatba visszatáplált összes energia | Napelemes visszatáplálás követése |
| Importált/exportált energia tarifánként (T1–T4, ha elérhető) | kWh | A mérő külön tarifaregisztereinek számlálói | Tarifák szerinti összehasonlítás; önmagában nem költségszámítás |
| Pillanatnyi importált teljesítmény | W vagy kW | A hálózatból éppen felvett teljesítmény | Nagy fogyasztók és terhelési csúcsok megfigyelése |
| Pillanatnyi exportált teljesítmény | W vagy kW | A hálózatba éppen visszatáplált teljesítmény | Pillanatnyi többlettermelés figyelése |
| Fázisonkénti teljesítmény (L1–L3) | kW | Számított, a mért összteljesítményhez arányosított becslés | Terheléseloszlás ellenőrzése |
| Fázisonkénti feszültség (L1–L3) | V | Az egyes fázisok feszültsége | Feszültségingadozások követése |
| Fázisonkénti áramerősség (L1–L3) | A | Az egyes fázisokon folyó áram | Fázisterhelés hosszú távú figyelése |
| Meddő energia / meddő teljesítmény | kvarh / var (a kijelzett adat szerint) | Meddő energia, illetve pillanatnyi meddő teljesítmény | Haladó villamos hálózati elemzés |
| Teljesítménytényező | dimenzió nélküli | A hatásos és látszólagos teljesítmény aránya | Villamos terhelések részletes vizsgálata |
| Hálózati frekvencia | Hz | A váltakozó áramú hálózat frekvenciája | Frekvencia megfigyelése, ha a mérő közli |
| Aktuális tarifa | tarifa-/regiszterazonosító | A mérő által jelzett aktív tarifaregiszter | Az éppen aktív tarifa azonosítása |

**Import és export:** Importnak nevezzük a hálózatból a házba érkező, exportnak a házból a hálózatba távozó energiát. Külön összesített számlálókról van szó. Visszatáplálás nélküli rendszernél az exportérték nulla vagy hiányzó is lehet.

**Teljesítmény és energia:** A W/kW a pillanatnyi teljesítményt, a Wh/kWh az idő alatt felhasznált vagy visszatáplált energiamennyiséget jelöli. Például 1 kW állandó vételezés egy óra alatt körülbelül 1 kWh energiát jelent.

**Három fázis:** Az L1, L2 és L3 külön fázisok. Külön mérésükkel látható, ha az egyik fázis tartósan nagyobb terhelést kap. Egyfázisú rendszernél az L2 és L3 értékek hiányozhatnak.

**Nem kell mindent megjeleníteni:** Elsőként az összes vételezett energia, az esetleges visszatáplálás és a pillanatnyi teljesítmény megjelenítését érdemes használni. A többi értéket akkor célszerű elővenni, ha konkrét kérdésre keresünk választ. A nulla vagy hiányzó érték önmagában nem bizonyít pluginhibát.

> **Kód és dokumentáció összhangja:** Az 1–3. és 26–29. eszközök leírása a közösen egyeztetett két javítást tükrözi. A README publikálása előtt ezeket a módosításokat a `plugin.py` fájlban is alkalmazni kell, mert az eredetileg feltöltött fájl még a régi működést tartalmazta.

## Teljes Domoticz-eszközjegyzék (plugin.py)

A **Unit** a pluginen belüli eszközsorszám, **nem** a globális Domoticz IDX. Az alábbi elnevezések az angol kulcsok; a Domoticz nyelvi beállításai alapján fordítva jelenhetnek meg.

### Energia

| Unit | Device name | Unit / format | Jelentés, értelmezés |
| ---: | --- | --- | --- |
| 1 | Total imported energy | W;Wh | Vételezett pillanatnyi teljesítmény (W) és összes vételezett energia (Wh). |
| 2 | Total exported energy | W;Wh | Visszatáplált pillanatnyi teljesítmény (W) és összes visszatáplált energia (Wh). |
| 3 | Total active energy | W;Wh | Kétirányú energiaforgalom: import + export teljesítmény (W) és energia (Wh); nem nettó fogyasztás. |
| 4 | Imported energy tariff 1 | kWh | Vételezett energia gyűjtött értéke az adott tarifaregiszterben. |
| 5 | Imported energy tariff 2 | kWh | Vételezett energia gyűjtött értéke az adott tarifaregiszterben. |
| 6 | Imported energy tariff 3 | kWh | Vételezett energia gyűjtött értéke az adott tarifaregiszterben. |
| 7 | Imported energy tariff 4 | kWh | Vételezett energia gyűjtött értéke az adott tarifaregiszterben. |
| 8 | Exported energy tariff 1 | kWh | Visszatáplált energia gyűjtött értéke az adott tarifaregiszterben. |
| 9 | Exported energy tariff 2 | kWh | Visszatáplált energia gyűjtött értéke az adott tarifaregiszterben. |
| 10 | Exported energy tariff 3 | kWh | Visszatáplált energia gyűjtött értéke az adott tarifaregiszterben. |
| 11 | Exported energy tariff 4 | kWh | Visszatáplált energia gyűjtött értéke az adott tarifaregiszterben. |
| 12 | Reactive imported energy | kvarh | Összesített vételezett / visszatáplált meddő energia. |
| 13 | Reactive exported energy | kvarh | Összesített vételezett / visszatáplált meddő energia. |
| 14 | Reactive energy QI | kvarh | A QI–QIV negyedhez tartozó összesített meddő energia. |
| 15 | Reactive energy QII | kvarh | A QI–QIV negyedhez tartozó összesített meddő energia. |
| 16 | Reactive energy QIII | kvarh | A QI–QIV negyedhez tartozó összesített meddő energia. |
| 17 | Reactive energy QIV | kvarh | A QI–QIV negyedhez tartozó összesített meddő energia. |

### Teljesítmény

| Unit | Device name | Unit / format | Jelentés, értelmezés |
| ---: | --- | --- | --- |
| 18 | Instantaneous imported power | kW | Közvetlen pillanatnyi vételezési / visszatáplálási mérés. |
| 19 | Instantaneous exported power | kW | Közvetlen pillanatnyi vételezési / visszatáplálási mérés. |
| 20 | Imported power L1 | kW | U × I × teljesítménytényező alapján becsült, majd a teljes mérőteljesítményhez skálázott. |
| 21 | Imported power L2 | kW | U × I × teljesítménytényező alapján becsült, majd a teljes mérőteljesítményhez skálázott. |
| 22 | Imported power L3 | kW | U × I × teljesítménytényező alapján becsült, majd a teljes mérőteljesítményhez skálázott. |
| 23 | Exported power L1 | kW | U × I × teljesítménytényező alapján becsült, majd a teljes mérőteljesítményhez skálázott. |
| 24 | Exported power L2 | kW | U × I × teljesítménytényező alapján becsült, majd a teljes mérőteljesítményhez skálázott. |
| 25 | Exported power L3 | kW | U × I × teljesítménytényező alapján becsült, majd a teljes mérőteljesítményhez skálázott. |
| 26 | Reactive power QI | kvar | Pillanatnyi meddő teljesítmény, nem összesített meddő energia. |
| 27 | Reactive power QII | kvar | Pillanatnyi meddő teljesítmény, nem összesített meddő energia. |
| 28 | Reactive power QIII | kvar | Pillanatnyi meddő teljesítmény, nem összesített meddő energia. |
| 29 | Reactive power QIV | kvar | Pillanatnyi meddő teljesítmény, nem összesített meddő energia. |

### Villamos jellemzők

| Unit | Device name | Unit / format | Jelentés, értelmezés |
| ---: | --- | --- | --- |
| 30 | Voltage L1 | V | Az adott fázis mért feszültsége. |
| 31 | Voltage L2 | V | Az adott fázis mért feszültsége. |
| 32 | Voltage L3 | V | Az adott fázis mért feszültsége. |
| 33 | Current L1 | A | Az adott fázis mért áramerőssége. |
| 34 | Current L2 | A | Az adott fázis mért áramerőssége. |
| 35 | Current L3 | A | Az adott fázis mért áramerőssége. |
| 36 | Current Bl1 | A | Áramerősségből és teljesítménytényezőből számított meddőáram-komponens. |
| 37 | Current Bl2 | A | Áramerősségből és teljesítménytényezőből számított meddőáram-komponens. |
| 38 | Current Bl3 | A | Áramerősségből és teljesítménytényezőből számított meddőáram-komponens. |
| 39 | Network frequency | Hz | Mért hálózati frekvencia. |
| 40 | Power factor | cos φ | Összesített vagy fázisonkénti teljesítménytényező. |
| 41 | Power factor L1 | cos φ | Összesített vagy fázisonkénti teljesítménytényező. |
| 42 | Power factor L2 | cos φ | Összesített vagy fázisonkénti teljesítménytényező. |
| 43 | Power factor L3 | cos φ | Összesített vagy fázisonkénti teljesítménytényező. |

### Állapot és összetett mérő

| Unit | Device name | Unit / format | Jelentés, értelmezés |
| ---: | --- | --- | --- |
| 44 | Meter serial number | text | A táviratból kiolvasott mérőazonosító. |
| 45 | Circuit breaker status | On/Off | A mérőtávirat megszakítóállapota (ON → On, egyébként Off). |
| 46 | Active tariff | text | Aktuális tarifakód, általában 0001–0004. |
| 47 | Current - daily consumption | P1 smart meter | Hatmezős Domoticz P1 mérő: T1/T2 import, T1/T2 export (Wh), pillanatnyi import/export (W); a napi értéket a Domoticz jeleníti meg. |

### Fontos értelmezési megjegyzések

- **1–3. eszköz:** az egyeztetett javítás után mindhárom `Type=113, Subtype=0` típusú eszköz `teljesítmény_W;energia_Wh` formátumú adatot kap. Az 1. vételezés, a 2. visszatáplálás, a 3. pedig ezek **összege (kétirányú energiaforgalom)**, nem nettó fogyasztás. A „Total active energy” eredeti név kompatibilitási okból megmaradt, de ezt a jelentést kell hozzá társítani.
- **20–25. eszköz:** a fázisonkénti import/export teljesítmény **becslés**, nem külön fázisonkénti irányhelyes mérőregiszterek közvetlen kiolvasása. A kód a feszültségből, áramerősségből és teljesítménytényezőből számol, majd a teljes mért import/export értékhez igazítja. Bizonyos körülmények között, különösen előjeles teljesítménytényező nélkül, az eredmény nulla vagy pontatlan lehet.
- **26–29. eszköz:** a javított mértékegység `kVAr`, összhangban a `5.7.0`–`8.7.0` OBIS-mezők pillanatnyi meddő teljesítményével. A korábban létrehozott Domoticz-eszközökön külön szükséges lehet a régi `kVArh` felirat átállítása.
- **36–38. eszköz:** a meddőáram-komponens számított érték, nem külön mérés.
- **OBIS-adatok:** a plugin a szükséges OBIS-mezők jelenlétével számol; nem építettünk be külön hiányzóadat-kezelést. A parser meglévő `0.0` alapértéke megmaradt, ezért technikailag egy hiányzó mező is nullát eredményezhet.
- **47. eszköz:** az összetett, hatmezős Domoticz P1 eszköz csak az 1. és 2. tarifát használja. A 3–4. tarifa külön eszközökben marad. A napi adatot a Domoticz számítja és jeleníti meg; nem egy napi P1 számláló közvetlen kiolvasása.
- **Eszközlétrehozás:** a plugin mind a 47 eszközt létrehozza, és a szükséges OBIS-mezők rendelkezésre állását feltételezi. A felhasználó kiválaszthatja, melyeket szeretné megjeleníteni.


## Gyakorlati példák Domoticzban

1. **Pillanatnyi házterhelés:** figyelhető, hogyan változik a hálózati vételezés villanyautó-töltés, villanybojler vagy más nagy fogyasztó bekapcsolásakor.
2. **Napelemes visszatáplálás:** a pillanatnyi exportteljesítmény és az összes exportált energia együtt mutatja a hálózatba leadott energiát, ha rendelkezésre állnak az adatok.
3. **Fázisok összehasonlítása:** az L1/L2/L3 áram- vagy teljesítményadataiból kiderülhet, van-e tartósan egyenlőtlen terhelés.

Ezek felhasználási példák, nem előre beállított automatizmusok. A rendelkezésre álló eszközök és az alkalmazható határértékek rendszerenként eltérnek.

## Képernyőképek

### Dashboard – Energiafogyasztás áttekintése

A plugin a HomeWizard P1 mérő által szolgáltatott adatokat közvetlenül a Domoticz kezelőfelületén jeleníti meg.

A Dashboard oldalon gyorsan áttekinthető a pillanatnyi teljesítményfelvétel, a napi energiafogyasztás és az aktuális villamosenergia-tarifa.

![HomeWizard P1 Extended - Domoticz Dashboard](images/dashboard.png)

### Utility – Részletes villamosenergia-adatok

A kibővített plugin számos Domoticz mérőeszközt hoz létre, amelyek segítségével részletesen követhető a villamosenergia-hálózat működése.

A megjelenített adatok között megtalálható a tarifánként importált és exportált energiamennyiség, a pillanatnyi teljesítmény, a fázisonkénti feszültség és áramerősség, a meddő energia, a teljesítménytényező és a hálózati frekvencia.

![HomeWizard P1 Extended - Részletes mérési adatok](images/utility.png)

### Hardware – Plugin beállításai

A plugin a Domoticz Setup → Hardware menüpontjában konfigurálható.

Itt adhatók meg a Domoticz kapcsolati paraméterei, a HomeWizard P1 eszköz IP-címe, valamint az adatfrissítés gyakorisága.

![HomeWizard P1 Extended - Hardverbeállítások](images/hardware.png)

## Előfeltételek

- Domoticz 2022.1 vagy újabb verzió
- Engedélyezett Python plugin támogatás
- Helyi hálózathoz csatlakoztatott HomeWizard Wi-Fi P1 mérő
- Hálózati kapcsolat a Domoticz és a HomeWizard eszköz között
- A HomeWizard helyi API engedélyezése, amennyiben azt az eszköz firmware-verziója megköveteli

A Python pluginokról további információ:

[Domoticz Python plugin dokumentáció](https://www.domoticz.com/wiki/Using_Python_plugins)

## Telepítés

A plugin telepíthető manuálisan vagy a [Domoticz Plugins Manager](https://github.com/stas-demydiuk/domoticz-plugins-manager) segítségével.

### Manuális telepítés

**1. Másold vagy klónozd a plugint a Domoticz plugins könyvtárába:**

```bash
cd domoticz/plugins
git clone https://github.com/szelessavalapitvany/HomeWizard-Wifi-p1-plugin-Extended
```

A könyvtár elérési útját a saját Domoticz telepítésednek megfelelően állítsd be.

**2. Indítsd újra a Domoticzot.**

**3. Ellenőrizd, hogy az „Accept new Hardware Devices” beállítás engedélyezve van-e.**

**4. Lépj a Setup → Hardware menüpontba.**

**5. Adj hozzá új hardvert az alábbi típussal:**

`Home Wizard Electric P1 meter extended`

**6. Állítsd be a szükséges paramétereket:**

- **Name:** HomeWizard Extended
- **Domoticz IP Address:** 127.0.0.1 (helyi telepítés esetén)
- **Port:** 8080 (vagy a Domoticz beállított HTTP-portja)
- **HomeWizard P1 IP Address:** A HomeWizard eszköz IP-címe
- **Data interval – Frissítés:** Az adatok lekérdezésének gyakorisága
- **Debug:** Hibakeresés esetén engedélyezhető

**7. Kattints az Add gombra** a hardver létrehozásához.

A plugin létrehozza a támogatott mérőeszközöket a Domoticzban, majd a beállított időközönként frissíti azok adatait.

Az elérhető mérési értékek a csatlakoztatott villamos fogyasztásmérő képességeitől függnek.

## Plugin frissítése

A plugin legújabb verzióra történő frissítéséhez:

**1. Lépj be a plugin könyvtárába és töltsd le a legújabb módosításokat:**

```bash
cd domoticz/plugins/HomeWizard-Wifi-p1-plugin-Extended
git pull
```

**2. Indítsd újra a Domoticzot.**

### Helyi módosítások kezelése

Ha a plugin fájljait korábban módosítottad, és emiatt a `git pull` nem fut le, a helyi módosításokat ideiglenesen eltárolhatod:

```bash
git stash
git pull
```

A korábbi helyi módosítások visszaállításához:

```bash
git stash pop
```

A helyi módosítások visszaállítása bizonyos esetekben ütközéseket okozhat.

## Plugin visszaléptetése (downgrade)

Szükség esetén a plugin egy korábbi verziója is visszaállítható.

**1. Lépj be a plugin könyvtárába:**

```bash
cd domoticz/plugins/HomeWizard-Wifi-p1-plugin-Extended
```

**2. Tekintsd meg a korábbi verziókat:**

```bash
git log --oneline
```

**3. Állítsd vissza a kívánt verziót:**

```bash
git reset --hard <commit_hash>
```

A `<commit_hash>` helyére a visszaállítani kívánt verzió commitazonosítóját kell beírni.

**Figyelem:** A `git reset --hard` visszavonhatatlanul eldobja a követett fájlokon végzett, még nem mentett helyi módosításokat. A parancs futtatása előtt célszerű biztonsági mentést készíteni.

**4. Indítsd újra a Domoticzot.**

Bizonyos esetekben elegendő lehet a plugin letiltása, majd ismételt engedélyezése a Setup → Hardware menüpontban.

A kezelőfelületet érintő változtatások után szükség lehet a böngésző gyorsítótárának törlésére is.

## Többnyelvű támogatás

A plugin több nyelvet támogat, és a Domoticzban beállított nyelvet használja a támogatott eszközleírásokhoz.

Így ugyanaz a plugin külön nyelvi változat telepítése nélkül használható különböző nyelvű Domoticz rendszerekben.

## Megjegyzések

- A HomeWizard P1 eszköz számára célszerű fix IP-címet vagy DHCP-foglalást beállítani.
- A HomeWizard P1 mérővel történő kommunikáció a helyi hálózaton keresztül valósul meg.
- Az elérhető mérési adatok a villamos fogyasztásmérő típusától és a P1 interfész által biztosított információktól függnek.
- Egyes mérési értékek bizonyos fogyasztásmérőknél nem állnak rendelkezésre.
- Kommunikációs vagy eszközlétrehozási hibák esetén érdemes a Debug módot engedélyezni.

## Projekt

Fejlesztő és karbantartó: **Szélessáv Közhasznú Alapítvány**

Weboldal: [Szélessáv Műhely](https://www.szelessavmuhely.hu)

GitHub: [HomeWizard-Wifi-p1-plugin-Extended](https://github.com/szelessavalapitvany/HomeWizard-Wifi-p1-plugin-Extended)
