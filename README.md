# 🏛️ Kapesní Účetní – Daňová legislativa ČR (OTA Feed)

Tento repozitář slouží jako centrální feed daňových a legislativních parametrů České republiky pro iOS aplikaci **Kapesní Účetní (DaněPro)**.

## 📡 Jak to funguje

1. Aplikace při startu na pozadí stahuje soubor:
   `https://raw.githubusercontent.com/gratusapp/legislation/main/tax_constants.json`
2. Pokud v něm najde novější parametry pro daný rok (např. nové minimální zálohy SP a ZP, rozhodnou částku pro vedlejší činnost nebo hranici 23% sazby daně), okamžitě začne počítat podle nových zákonů.
3. **Není nutné vydávat novou verzi aplikace na App Store.**

## 🤖 Automatická kontrola a e-mailová upozornění (GitHub Actions)

* Každý podzim běží automatický skript [update_tax_legislation.yml](.github/workflows/update_tax_legislation.yml).
* Pokud v souboru chybí parametry pro nadcházející rok, robot:
  1. Spočítá odhadované zákonné limity dle vládních vyhlášek.
  2. Vytvoří Pull Request.
  3. Založí Issue a přiřadí ho vám, což **automaticky odešle e-mail na váš účet**.
* V e-mailu stačí kliknout na odkaz, zkontrolovat čísla a jedním kliknutím potvrdit (**Merge pull request**).

## ✏️ Jak upravit parametry ručně

1. Otevřete soubor [tax_constants.json](tax_constants.json).
2. Klikněte na ikonu ✏️ **Edit**.
3. Upravte hodnoty pro daný rok a klikněte na **Commit changes**.
4. Všichni uživatelé aplikace získají nová čísla při příštím spuštění aplikace.
