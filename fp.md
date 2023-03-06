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

Rene funksjoner

* Deterministiske - gir samme resultat hver gang
* Påvirker ikke omverdenen - eneste output er returverdi
* Idempotent 

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