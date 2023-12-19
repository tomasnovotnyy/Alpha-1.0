# Alpha-1.0

# *Třída Subjects.py*
Tato třída obsahuje seznam předmětů a jejich vlastností.

## *Metody*
> __init__(self): Inicializační metoda třídy Subjects, která vytváří seznam předmětů.

## *Ukázka jednoho uloženého dne*
![Pondeli_Rozvrh](https://github.com/tomasnovotnyy/Alpha-1.0/assets/84340580/08deca94-e8b7-45df-94ec-b637b5e9a0cb)

## *Popis atributu*
self.subjects: Seznam obsahující informace o předmětech.
> - code: Název / Kód předmětu.
> - teacher: Název učitele či lektora daného předmětu.
> - class: Označení třídy, kde se předmět koná.
> - type: Typ předmětu (teorie nebo cvičení).
> - floor: Patro, kde se výuka daného předmětu koná.

# *Třída Schedule.py*
Tato třída je určena pro práci s rozvrhem. Umožňuje získávat a zobrazovat informace o rozvrhu ve formě textu.

## *Metody*
> __init__(self, schedule): Inicializační metoda třídy Schedule, která vytváří objekt rozvrhu na základě poskytnutého rozvrhového plánu.

> get_schedule(self): Metoda, která vrací rozvrhový plán jako 2D pole.

> print_schedule(self): Metoda, která vytváří textový výpis rozvrhu dle vnitřního rozvrhového plánu.
### **Detailní popis metody _print_schedule_**
![print_schedule](https://github.com/tomasnovotnyy/Alpha-1.0/assets/84340580/4b9e9bd0-55fc-4c85-a01c-6ae8357076d3)
Tato metoda vytváří textový výpis rozvrhu na základě interního rozvrhu. Prochází jednotlivé dny v rozvrhu a pro každou hodinu v daném dni vytváří textový řetězec obsahující kódy předmětů.
> - days: Pole obsahující zkratky dnů v týdnu.
> - schedule_text: Proměnná pro ukládání vytvořeného textového výpisu rozvrhu.
> - První for cyklus iteruje přes jednotlivé dny v rozvrhovém plánu.
> - Druhý for cyklus prochází hodiny v daném dni a vytváří textový řetězec obsahující kódy předmětů.
> - Pokud pro danou hodinu nejsou k dispozici informace o předmětu, pouze se vypíše kód předmětu.
> - Metoda vrací textový řetězec reprezentující rozvrh, přičemž odstraní prázdné řádky na konci výstupu pomocí metody strip().

# *Třída Watchdog.py*
Třída Watchdog je nástroj pro sledování časového limitu a přerušení provádění procesu po dosažení daného časového intervalu.

Tato třída umožňuje:

- Nastavit časový limit sledování.
- Spustit stopky pro sledování času.
- Zjistit, zda uplynul zadaný časový limit
## *Metody*
> __init__(self, timeout): Konstruktor třídy, inicializuje instanci Watchdog s daným timeoutem v sekundách.
> - timeout: Časový limit (timeout) ve vteřinách, po jehož uplynutí bude ukončen sledovaný proces.

> start(self): Spustí stopky.
> - Funkce inicializuje časový údaj pro sledování uplynutí časového limitu.

> stop(self) -> bool: Zastaví stopky a vrátí informaci, zda byl dosažen timeout.
> - return: True, pokud uplynul časový limit. False, pokud časový limit ještě neuplynul.
> - Funkce vypočítá uplynulý čas od spuštění stopky a porovná jej s časovým limitem. Vrací True, pokud uplynul časový limit, jinak False.
