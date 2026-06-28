# TW-Invest Dashboard

## Depot-Aktualisierung

Wenn der Benutzer „Depot" schreibt:

1. Hole aktuelle Positionswerte aus Parqet mit `parqet_query_portfolio` (view="holdings", portfolioId "682875b85bf20f788484a2b4")
2. Extrahiere ETF1 (nickname "Vanguard FTSE All-World"), ETF2 (nickname "L&G Global Dividends"), TG (nickname "TR Tagesgeld")
3. Berechne: Gesamt = ETF1 + ETF2 + TG, WW = ETF1 + ETF2, Prozentanteile, Differenzen zu Ziel 70/10/20
4. Aktualisiere `TW-Invest.html`:
   - Gesamtdepot-Karte
   - Donut-Gradient und Donut-Hole-Wert
   - Tabelle Kachel 1 (ETF1, ETF2, TG Werte)
   - Kachel 3 Rebalancing (Ist-%, Balkenbreite, Differenz in €, Farbe: + grün / - rot)
   - JS-Konstanten VAL_ETF1, VAL_ETF2, VAL_TG
   - Span `btd-ww` (Weltwirtschaft-Aktuellwert)
5. Committe mit Nachricht "Parqet-Update: [heutiges Datum]" und pushe zu GitHub (origin main)
6. Keine Tabelle ausgeben, keine Erklärung, kein Kommentar zu Börsenzeiten — immer aktualisieren und nur "✓ Dashboard aktualisiert ([Datum])" melden

## Formatierung

- Beträge in €: deutsches Format mit Tausenderpunkt und Komma (z.B. 100.325,33 €)
- Prozente: eine Dezimalstelle (z.B. 79,9 %)
- Differenzen: + grün (rebal-diff-pos), - rot (rebal-diff-neg)
