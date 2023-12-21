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
Tato `Schedule` je určena pro práci s rozvrhem. Umožňuje získávat a zobrazovat informace o rozvrhu ve formě textu.

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
Třída `Watchdog` je nástroj pro sledování časového limitu a přerušení provádění procesu po dosažení daného časového intervalu.

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

Již při generování rozvrhů generuji pouze takové rozvrhy, které splňují následující podmínky:
1. Když je cvičení dvouhodinové, tříhodinové tak ty hodiny musí být u sebe v jednom dni.
   - To znamená, že pokud by se objevil předmět s ozanečením 'practice' na 10. hodině, tak se vrátí do listu všech možných předmětů pro daný týden a přidá se až když se budou moct obejcit dvě hodiny s označením 'practice' za sebou.
   - Tím se zajístí to, že se nebudou generovat nesmyslné rozvrhy, které by měli hodiny s označením 'practice' rozházené po celém týdnu náhodně.
2. Pokud je stejný předmět vícekrát v jeden den a není to vícehodinovka, tak to je špatně.
   - Ve svém generátoru také hlídám, že pokud by se měl určitý předmět objevit vícekrát v jeden den a zároveň tento předmět není vícehodinovka neboli předmět s označením 'practice', tak se do daného dne vloží pouze jednou. Zamezím tím tak generování dalších zbytečných rozvrhů, které by byly vyhodnoceny jako špatné.

Myslím si, že těmito pravidly zlepším kvalitu generování rozvrhů a zároveň snížím počet nesmyslných a špatných rozvrhů.







# *Třída Evaluator.py*
Třída `Evaluator` poskytuje funkce pro hodnocení a vyhodnocování rozvrhu na základě nastavených kritérií pro předměty a časové údaje.

## *Metody*
> __init__(self): Metoda inicializuje instanci třídy `Evaluator` a načítá konfiguraci pro hodnocení rozvrhu z konfiguračního souboru `config.ini`. Tato konfigurace obsahuje kritéria hodnocení pro různé předměty a také obsahuje časová kritéria.

> get_day_of_week(self, day_index): Tato metoda přijímá index dne v týdnu a vrací odpovídající název dne (např. pro index `0` vrátí `"Pondělí"`, pro index `1` vrátí `"Úterý"` atd.).

> evaluate_schedule(self, schedule): Metoda, která hodnotí zadaný rozvrh na základě nastavených kritérií pro předměty a čas. Kritéria hodnocení zahrnují délku trvání předmětů, posloupnost patra učeben, variabilitu učitelů, existence pauz na oběd a maximální délku jednotlivých dnů.</br></br>
> Při hodnocení rozvrhu tato metoda bere v úvahu následující kritéria:
> 1. **Rozdíl patra mezi dvěma po sobě jdoucími hodinami**:</br> Podle rozdílu mezi patry dvou po sobě jdoucích hodin se odečítá bodová hodnota 20. Čím větší rozdíl pater, tím větší penalizace bodů.
> 2. **Přidání bodů na základě délky trvání a kriterií předmětu**:</br> K hodnocení se přičítá délka trvání hodiny pro daný den a váha předmětu.
> 3. **Odečítání bodů za profilové předměty na začátku nebo na konci dne**:</br> Pokud jsou určité profilové předměty umístěny na začátku nebo na konci dne, odečítá se 100 bodů za každý profilový předmět.
> 4. **Kontrola, zda jsou pauzy na oběd**:</br> Odečtení bodů, pokud není v určitý časový rámec na daný den zařazena pauza na oběd.
> 5. **Penalizace za nadměrný počet hodin**:</br> Odečítání bodů za každou hodinu, pokud přesáhne počet hodin daný limit, který je nastaven na 6 hodin denně.
> 6. **Vaše vlastní pravidlo #1, jeho princip musí být zřejmý z dokumentace**:</br>
> **Variabilita učitelů**: Hodnotí různorodost učitelů v průběhu jednoho dne s cílem omezit monotónnost.
