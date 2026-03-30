# HomeWizard-Wifi-p1-plugin-Extended
Extended version of the original HomeWizard Wi-Fi P1 Domoticz plugin with more detailed data and multi-language support.

Python plugin for Domoticz to integrate the HomeWizard Wi-Fi P1 smart energy meter
(imported / exported energy, tariffs, power values, extended and detailed data).

This is an extended version of the original HomeWizard P1 plugin with additional data and multi-language support.

# Features

Compared to the original HomeWizard Wi-Fi P1 plugin, this Extended version provides:

- More detailed power data (per phase voltage, current, power)
- Better handling of import/export values and tariffs
- More accurate and consistent device mapping in Domoticz
- Additional calculated values (where available)
- Improved stability and error handling
- Multi-language support (all languages supported by Domoticz)
- Cleaner and more structured device creation
- Designed for long-term reliable operation

This plugin aims to provide a more complete and robust integration of the HomeWizard P1 meter into Domoticz.

# Prerequisites

* Domoticz 2022.1 or newer

* Domoticz with Python plugin support enabled
  https://www.domoticz.com/wiki/Using_Python_plugins

# Installation

You can install the plugin manually or by using the
[Domoticz Plugins Manager](https://github.com/stas-demydiuk/domoticz-plugins-manager)

## Manual installation

1. Clone or copy the plugin into your Domoticz plugins directory:

```
cd domoticz/plugins
git clone https://github.com/szelessavalapitvany/HomeWizard-Wifi-p1-plugin-Extended
```

2. Restart Domoticz
3. Make sure “Accept new Hardware Devices” is enabled in Domoticz settings
4. Go to Setup → Hardware
5. Add a new hardware device with type “HomeWizard P1 Extended”
6. Configure the required parameters:

* IP address of the HomeWizard device
* optional settings depending on plugin version

## Plugin update

1. Go to the plugin directory and pull the latest version:

```
cd domoticz/plugins/HomeWizard-Wifi-p1-plugin-Extended
git pull
```

2. Restart Domoticz

Note:
If you modified plugin files and git pull fails, you can stash local changes:

```
git stash
```

## Plugin downgrade

1. Reset the plugin to an earlier version:

```
cd domoticz/plugins/HomeWizard-Wifi-p1-plugin-Extended
git reset --hard <commit_hash>
```

2. Restart Domoticz
   (or disable and re-enable the plugin under Setup → Hardware; browser cache cleanup may be required)

---

---

# homewizard-wifi-p1-plugin-extended (magyarul)

Python plugin Domoticzhoz, amely a HomeWizard Wi-Fi P1 okosmérő integrációját valósítja meg
(importált / exportált energia, tarifák, teljesítmény adatok, kibővített és részletes adatokkal).

Ez a plugin az eredeti HomeWizard P1 plugin kibővített változata, több adattal és többnyelvű támogatással.

# Funkciók

Az eredeti HomeWizard Wi-Fi P1 pluginhoz képest ez a kibővített verzió az alábbi többletet nyújtja:

- Részletesebb teljesítmény adatok (fázisonkénti feszültség, áram, teljesítmény)
- Pontosabb import/export és tarifa kezelés
- Konzisztensebb és átláthatóbb eszközkezelés Domoticzban
- További számított értékek (ahol elérhető)
- Stabilabb működés és jobb hibakezelés
- Többnyelvű támogatás (a Domoticz összes támogatott nyelvén)
- Letisztultabb eszköz létrehozás és struktúra
- Hosszú távú stabil működésre tervezve

A plugin célja, hogy teljesebb és megbízhatóbb integrációt biztosítson a HomeWizard P1 mérőhöz Domoticz alatt.

# Előfeltételek

* Domoticz 2022.1 vagy újabb

* Python plugin támogatás engedélyezve a Domoticzban
  https://www.domoticz.com/wiki/Using_Python_plugins

# Telepítés

A plugin telepíthető manuálisan vagy a
[Domoticz Plugins Manager](https://github.com/stas-demydiuk/domoticz-plugins-manager) segítségével.

## Manuális telepítés

1. Másold / klónozd a plugint a Domoticz plugin könyvtárába:

```
cd domoticz/plugins
git clone https://github.com/szelessavalapitvany/HomeWizard-Wifi-p1-plugin-Extended
```

2. Indítsd újra a Domoticzot
3. Ellenőrizd, hogy az „Accept new Hardware Devices” engedélyezve van
4. Lépj a Setup → Hardware menübe
5. Add hozzá az új hardvert „HomeWizard P1 Extended” típussal
6. Állítsd be a szükséges paramétereket:

* HomeWizard eszköz IP címe
* opcionális beállítások (plugin verziótól függően)

## Plugin frissítése

1. Lépj be a plugin könyvtárába és frissítsd:

```
cd domoticz/plugins/HomeWizard-Wifi-p1-plugin-Extended
git pull
```

2. Indítsd újra a Domoticzot

Megjegyzés:
Ha módosítottad a plugin fájljait és a git pull nem fut le, a helyi változtatások eltárolhatók:

```
git stash
```

## Plugin visszaléptetése (downgrade)

1. Régebbi verzió visszaállítása:

```
cd domoticz/plugins/HomeWizard-Wifi-p1-plugin-Extended
git reset --hard <commit_hash>
```

2. Domoticz újraindítása
   (vagy a plugin letiltása majd újra engedélyezése a Setup → Hardware menüben; böngésző cache törlés szükséges lehet)
