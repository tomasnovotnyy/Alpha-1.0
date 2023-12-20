# Alpha-1.0

# *Třída Subjects.py*
Třída `Subjects` slouží k načítání informací o předmětech a jejich rozvrhu ze souboru `subjects.json`, který je dostupný pro konfiguraci vlastního rozvrhu.

## *Metody*
> __init__(self, filename="subjects.json"): Inicializační metoda třídy Subjects, jejíž argument je soubor obsahujícího informace o předmětech.</br> Výchozí hodnota je nastavena na: "subjects.json".

> load_subjects(self): Metoda load_subjects načítá informace o předmětech z JSON souboru. Výchozím názvem souboru pro načtení je `subjects.json`, ale může být specifikován jiný název souboru v konstruktoru třídy.</br>
> - Při spuštění se pokusí načíst informace o předmětech ze souboru `subjects.json`. V případě, že soubor není nalezen, vrátí prázdný seznam a vypíše chybu o chybě souboru.

## *Ukázka jednoho uloženého dne v souboru subjects.json*
![Pondeli_Rozvrh](https://github.com/tomasnovotnyy/Alpha-1.0/assets/84340580/f601298f-cb5c-4538-bb3e-c928221bb0f2)

## *Konfigurace vlastního rozvrhu*
Třída `Subjects` umožňuje načíst data o předmětech a jejich rozvrhu ze souboru `subjects.json`, který se nachází ve složce `config`. Tento soubor musí obsahovat informace o předmětech v následujícím formátu:

```json
[
    {
        "code": "WA",
        "teacher": "Mgr. Mykyta Narusevych",
        "classroom": "17b",
        "type": "practice",
        "floor": 3
    },
    // Další položky
]
```

## *Popis atributů*
- code: Název / Kód předmětu.
- teacher: Název učitele či lektora daného předmětu.
- class: Označení třídy, kde se předmět koná.
- type: Typ předmětu (teorie nebo cvičení).
- floor: Patro, kde se výuka daného předmětu koná.
</br></br></br>

# *Třída Schedule.py*
Tato třída je určena pro práci s rozvrhem. Umožňuje získávat a zobrazovat informace o rozvrhu ve formě textu.

## *Metody*
> __init__(self, schedule): Inicializační metoda třídy Schedule, která vytváří objekt rozvrhu na základě poskytnutého rozvrhového plánu.

> get_schedule(self): Metoda, která vrací rozvrhový plán jako 2D pole.

> print_schedule(self): Metoda, která vytváří textový výpis rozvrhu dle vnitřního rozvrhového plánu.

### **Detailní popis metody _print_schedule(self)_**
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
> __init__(self, timeout, pool): Konstruktor třídy, inicializuje instanci Watchdog s daným timeoutem v sekundách a seznamem sledovaných procesů.
> - timeout: Časový limit (timeout) ve vteřinách, po jehož uplynutí bude ukončen sledovaný proces.
> - pool: Seznam sledovaných procesů.

> start(self): Spustí stopky.
> - Funkce inicializuje časový údaj pro sledování uplynutí časového limitu.

> stop(self) -> bool: Zastaví stopky a vrátí informaci, zda byl dosažen timeout.
> - Vrátí True, pokud uplynul časový limit. False, pokud časový limit ještě neuplynul.
> - Funkce vypočítá uplynulý čas od spuštění stopky a porovná jej s časovým limitem. Vrací True, pokud uplynul časový limit, jinak False.

> wait(self): Spustí čekání na timeout a poté ukončí sledované procesy.

# *Třída Generator.py*
Třída `Generator` slouží k vytvoření náhodného rozvrhu pro daný počet dnů z poskytnutého seznamu předmětů.

## *Metody*
> __init__(self, subjects, days): Inicializuje třídu Generator se zadaným seznamem předmětů a počtem dnů pro tvorbu rozvrhu.

> check_value(self, list, item) -> bool: Metoda pro kontrolu existence položky v seznamu. Vrací True, pokud je položka v seznamu, jinak False.

> generate_schedule(self, shared): Generuje náhodný rozvrh pro zadaný počet dnů. Ukládá vytvořený rozvrh do sdíleného seznamu.

### **Detailní popis metody _generate_schedule(self, shared)_**
Tato metoda generuje náhodný rozvrh pro zadaný počet dnů. Vytváří seznam obsahující rozvrh pro každý den na základě poskytnutého seznamu předmětů.

Parametry:
- shared: Sdílený seznam, do kterého se ukládá vytvořený rozvrh.

Postup metody:
1. Iniciace proměnných:
   - Vytvoří kopii seznamu předmětů a zamíchá jej.
2. Generování rozvrhu pro každý den:
   - Pro každý den vytváří seznam obsahující náhodně vybrané předměty.
    - Vytvoření nového dne:
        - Inicializuje prázdný seznam pro každý den a seznam použitých předmětů.
   - Generování jednotlivých hodin: Postupně přidává hodiny do rozvrhu pro daný den.
    - Pravidla pro generování hodin:
        - Pokud je potřeba přidat praktickou hodinu na poslední hodinu dne, přesune ji na konec seznamu pro zabránění jednohodinové praxe v 10. hodině.
        - Pro každou hodinu přidává náhodně vybrané předměty do rozvrhu.
        - Zajišťuje, že teoretické předměty jsou přidávány do denního rozvrhu pouze jednou a nepřekračují 10 hodin denně.
        - Udržuje seznam použitých předmětů pro každý den a zabrání duplicitám v denním rozvrhu.
        - Pokud je předmět již v seznamu použitých předmětů a nejde o "Volnou hodinu", vrátí jej zpět do seznamu všech předmětů pro další použití.
3. Ukládání rozvrhu: Ukládá vytvořený rozvrh do sdíleného seznamu.
