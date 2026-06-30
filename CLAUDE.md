# TW-Invest Dashboard

## Depot-Aktualisierung

Die 3 Positionswerte sind die einzige Quelle, aus der das Dashboard alles berechnet (Donut, Tabelle, Rebalancing, btd-ww etc. werden beim Laden per JS aus `renderWerte()`/`renderBtd()` erzeugt). Sie liegen in `settings.json` (geräteübergreifend via Git) und als Fallback in den HTML-Input-`value`-Attributen.

Wenn der Benutzer „Depot" schreibt:

1. Hole aktuelle Positionswerte aus Parqet mit `parqet_query_portfolio` (view="holdings", portfolioId "682875b85bf20f788484a2b4")
2. Extrahiere ETF1 (nickname "Vanguard FTSE All-World"), ETF2 (nickname "L&G Global Dividends"), TG (nickname "TR Tagesgeld")
3. Aktualisiere die 3 Werte `wert-etf1`, `wert-etf2`, `wert-tg` an **beiden** Stellen:
   - `settings.json` (maßgeblich für den Sync; übrige Felder unverändert lassen)
   - `TW-Invest.html`: die `value`-Attribute der Inputs `wert-etf1`/`wert-etf2`/`wert-tg` (Fallback) + `data-parqet-ts` auf `wert-etf1` auf den aktuellen Zeitstempel setzen
   - Nichts anderes im HTML anfassen (Donut, Tabelle, Rebalancing, VAL_-Konstanten, `btd-ww` werden automatisch berechnet)
4. Committe mit Nachricht "Parqet-Update: [heutiges Datum]" und pushe zu GitHub (origin main)
5. Keine Tabelle ausgeben, keine Erklärung, kein Kommentar zu Börsenzeiten — immer aktualisieren und nur "✓ Dashboard aktualisiert ([Datum])" melden

Manuelle Änderungen der 3 Positionswerte (über den DATEN-Knopf) werden vom Benutzer selbst gespeichert (Speichern → `settings.json`). Nur bei „Depot" passt Claude die Werte aus Parqet an.

## Formatierung

- Beträge in €: deutsches Format mit Tausenderpunkt und Komma (z.B. 100.325,33 €)
- Prozente: eine Dezimalstelle (z.B. 79,9 %)
- Differenzen: + grün (rebal-diff-pos), - rot (rebal-diff-neg)
