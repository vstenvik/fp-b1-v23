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

- Rene funksjoner
- Immutabilitet
- Higher order functions

---

# Rene funksjoner

* Deterministiske - gir samme resultat hver gang
* Påvirker ikke omverdenen - eneste output er returverdi
* Idempotent 

---

```typescript
async function saveDataToDatabase(data: Data): Promise<void> {
    await database.SaveData(data);
}
```
---

```typescript
function getYearsFromToday(date: Date): int {
    const now = new Date();
    return now.getYear() - date.getYear();
}
```
---
```typescript
function getYearsFromToday(date: Date, now: Date): int {
    return now.getYear() - date.getYear();
}
```
---

```typescript
function Example(a: int, b: boolean): void
```
---
```typescript
function Example(): int
```

---
```typescript
const PI = 3.1415

function hentOmkretsAvSirkel(circle: Circle): int {
    return 2 * circle.radius * PI;
}
```
---

# Fordeler med rene funksjoner?

---

* Lette å skrive enhetstester for
* Lett å cache resultatet
    * Memoisering

---

```typescript
function memoize<TFunction>(fn: TFunction): TFunction {
    const cache = {}

    return (...args) => {
        let argsHash: string = hash(args);
        if(cache[argsHash]){
            return cache[argsHash]
        }
        else {
            const result = fn(...args);
            cache[argsHash] = result;
            return result;
        }
    }
}
```
---

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

OOP

- Klasser = data + oppførsel

```C#
public class Ansatt {
    public string Name { get; set; }
    public DateTime Birthdate { get; set; }
    public int Ansennitet { get; set; }

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

# Tilstand vs. Data

Når klasser har objekter for å oppdatere seg selv, oppfordrer dette til mutasjon. Mutasjon betyr at et objekt kan ha ulike tilstander.

---

```c#
var kari = new Ansatt("Kari", new Date(1990, 1, 1));

var bedrift = new Bedrift("Konsulentselskapet AS");

Ansettelsesforhold ansettelsesforhold = bedrift.Ansett(kari);

ansattelsesforhold.BeregnAnsennitet();
ansattelsesforhold.Lagre();

kari.GetAge(); // Resultat: 0
```

---

```f#
let kari = { name = "Kari", birthdate = DateTime(1990, 1, 1) }

let bedrift = { name = "Konsulentselskapet AS" );

let ansettelsesforhold = Bedrift.ansett bedrift kari

let kariMedAnsennitet = { kari with ansennitet = ansattelsesforhold.BeregnAnsennitet() }
ansattelsesforhold.Lagre();

kari.GetAge(); // Resultat: 33
```

---

HIGHER ORDER FUNCTIONS


TODO: ICOMPARABLE VS SORTBY

---

CURRYING

```FSHARP
let add a b = a + b
```

```javascript
const add = (a) => (b) => a + b
```