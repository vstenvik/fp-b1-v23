---
marp: true
theme: default
paginate: true
_class: invert
author: Vegard Stenvik
---

# Hva er funksjonell programmering?

BouvetOne 28.03.2023
Vegard Stenvik

![w:600](xkcd.png)

---

> In computer science, functional programming is a programming paradigm where programs are constructed by applying and composing functions.
> -wikipedia

---

- Begreper
- Fordeler med FP?

---

# Begreper 

- Rene funksjoner
- Immutabilitet
- Higher order functions

---

# Rene funksjoner

## Egenskaper
* Deterministiske
* Ingen sideeffekter
* Påvirker ikke omverdenen - eneste output er returverdi
* Referential transparency
* Muterer ikke input-parameterne

---

## Ikke-deterministisk

```typescript
function getYearsFromToday(date: Date): number {
const now = new Date();
return now.getYear() - date.getYear();
}
```

## Deterministisk
```typescript
function getYearsFromToday(date: Date, now: Date): int {
return now.getYear() - date.getYear();
}
```

---

# Begrep: Sideeffekter

Betydning: *Endring* av noe utenfor en funksjon

```typescript
// Lagre til database
async function saveDataToDatabase(data: Data): Promise<void> {
    await _db.SaveData(data);
}

// Skrive til en output/logg
function logHallo(): void {
    console.log('Hallo')
}

// Skrive noe til et API
async function postTilApi(data): Promise<void> {
    const result = await http.post(data);
    if(result.ok)
        ...
}
```
---

```typescript
class Person {
    private string navn;
    private number alder;

    constructor(navn: string; alder: string){
        this.navn = navn;
        this.alder = alder;
    }

    public setAlder(alder: number): void {
        this.alder = alder;
    }
}
```

---

```typescript
function Example(a: number, b: boolean): void
```
---

```typescript
function Example(): number
```

---
```typescript
const PI = 3.1415

function hentOmkretsAvSirkel(circle: Circle): number {
return 2 * circle.radius * PI;
}
```
---

## Referential transparency

```typescript
const add = (a, b) => a + b;

add(add(2, 3), 1) 

// Er nøyaktig det samme som

add(5, 1)
```

---

# Fordeler med rene funksjoner?

* Forutsigbare
* Lett å kombinere med andre funksjoner
* Lette å skrive enhetstester for
* Lett å cache resultatet
* Memoisering

---

# Memoisering

```typescript
const tungBeregning = () => { console.log('hallo') }

tungBeregning()
// console: hallo
tungBeregning()
// console: hallo
tungBeregning()
// console: hallo

const memoizedTungBeregning = memoize(tungBeregning);

memoizedTungBeregning()
// console: hallo
memoizedTungBeregning()
memoizedTungBeregning()

```
---

# Høyere ordens funksjoner

<!-- Innlednigsvis handler fp om å komponere funksjoner
    HOF er en måte å gjøre det på
-->

Funksjoner som tar funksjoner som parameter
eller returnerer en funksjon

---

## Eksempel: map

map: gjør *noe* med hvert element i en liste


```ts
// toUppercase: string -> string
let toUppercase = (str: string) => ...

// toUppercaseList: string[] -> string[]
let toUppercaseList = map(toUppercase)

toUppercaseList(['Hund', 'Katt', 'Frosk']) //['HUND', 'KATT', 'FROSK']

```
---

# FP vs. OOP

---

## Tilstand

> (...) The reason that many of these errors exist is that the presence of state makes programs hard to understand. It makes them complex.
> -- *B. Moseley, P. Marks (2006), Out of the Tar Pit*


---

OOP

- Klasser = data + oppførsel

```C#
public class Ansatt {
    private string Name { get; set; }
    private DateTime Birthdate { get; set; }
    private int Ansennitet { get; set; }

    public Human(string name, DateTime birthdate)
    {
        Name = name;    
        Birthdate = birthdate;
        Ansennitet = 0;
    }

    public int GetAge()
    {
        ...
    }
}
```

---

FP

- data og oppførsel separat

```F#
type Ansatt = {
    name: string;
    birthdate: DateTime;
}

let getAge human = ...

```

---

# Muterbar tilstand vs. immutable data

<!--
Når klasser har *metoder* for å oppdatere seg selv, oppfordrer dette til mutasjon. Mutasjon betyr at et objekt kan ha ulike *tilstander*.

Ved å begrense mutasjon, må tvinges vi til å være bevviste på hvor i en applikasjon vi har tilstand.
-->
---
![](carlos-aranda-Spq4fuFM4Kw-unsplash.jpg)
Foto: Carlos Aranda


<!--
- En mulig tilstand kan være en delvis initiert tilstand, hvor man har fylt noen men ikke alle påkrevde properties på en klasse

Ved å bruke språk som oppfordrer til immutabilitet vil vi få mer lesbar kode, fordi vi vet at når en verdi er satt, så er den satt og man slipper å lete gjennom en metode etter andre steder hvor verdien kan endres fra
-->

---

Blir det ikke ineffektivt hvis man skal kopiere alt hele tiden?

---

![w:800](link-list-1.png)

---

![w:800](link-list-2.png)

<!--

-->