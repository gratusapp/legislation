# 🏛️ Kapesní Účetní – Daňová legislativa ČR (OTA Feed)

Tento repozitář slouží jako centrální feed daňových a legislativních parametrů České republiky pro iOS aplikaci **Kapesní účetní**.

## 📡 Jak to funguje

1. Aplikace při startu a návratu do popředí na pozadí stahuje soubor:
   `https://raw.githubusercontent.com/gratusapp/legislation/main/tax_constants.json`
2. Pokud v něm najde novější parametry pro daný rok (např. nové minimální zálohy SP a ZP, rozhodnou částku pro vedlejší činnost, paušální daň nebo hranici 23% sazby daně), okamžitě je uloží i pro offline provoz a začne podle nich počítat.
3. **Není nutné vydávat novou verzi aplikace na App Store.**

## 🤖 Automatická měsíční kontrola a připomínky (GitHub Actions)

* Kontrolní workflow [update_tax_legislation.yml](.github/workflows/update_tax_legislation.yml) běží **každou neděli**:
  1. Pokud je poslední commit starší než **28 dní**, provede lehký udržovací commit do `.github/keepalive.txt` (*keep-alive*), aby GitHub po 60 dnech nevypnul plánované spouštění (rezerva ~32 dní a 4–5 nedělních běhů proti výpadku).
  2. Jakmile od září chybí schválené hodnoty pro nadcházející rok (`"isEnacted": true`), robot připraví **Pull Request** s předběžným výpočtem a orientačním náhledem z ČSSZ/VZP.
  3. Zároveň založí **Issue** přiřazené vlastníkovi repozitáře (**pošle e-mail**) a **1× za ~25–30 dní** do něj přidá měsíční připomínku, dokud parametry nepotvrdíte a nesloučíte do `main`.
* V e-mailu stačí kliknout na odkaz, ověřit oficiální částky z vyhlášky, nastavit `"isEnacted": true`, upravit `lastUpdated` na aktuální datum a potvrdit **Merge pull request** (a zavřít Issue).

## ✏️ Jak upravit parametry ručně

1. Otevřete soubor [tax_constants.json](tax_constants.json).
2. Klikněte na ikonu ✏️ **Edit**.
3. Upravte hodnoty pro daný rok, nastavte aktuální `lastUpdated` (formát `YYYY-MM-DD`) a `"isEnacted": true`, poté klikněte na **Commit changes**.
4. Aplikace si nová čísla stáhne automaticky při dalším spuštění (do ~5 minut od commitu).
