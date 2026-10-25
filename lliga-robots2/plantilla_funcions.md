# Les meves fitxes de funcions de Google Sheets

> Fitxer de documentació de funcions per a la Lliga de Robots (Missió 2).

---

## COUNTIFS

**Documentació:** <https://support.google.com/docs/answer/3256550?hl=ca>

**Què fa:** Compta quantes cel·les compleixen una o més condicions o criteris alhora, dins d'un o diversos intervals.

**Sintaxi:**

```excel
COUNTIFS(interval_de_criteris1, criteri1, [interval_de_criteris2, criteri2, ...])
```

| Argument | Obligatori? | Què és |
|---|---|---|
| `interval_de_criteris1` | Sí | L'interval de cel·les on es comprovarà el primer criteri. |
| `criteri1` | Sí | La condició o regla que han de complir les cel·les del primer interval. |
| `interval_de_criteris2` | No | Un segon interval de cel·les per avaluar una altra condició. |
| `criteri2` | No | La condició que ha de complir el segon interval. |

**Exemple de la documentació:** `COUNTIFS(B8:B27, ">" & B12, C8:C27, "<" & C13, D8:D27, "<>10")`

**El meu exemple amb la lliga:**

```excel
=COUNTIFS(Jornada1!G2:G49, "Laberint", Jornada1!N2:N49, "OK")
```

Resultat: `11` (Indica que hi ha exactament 11 curses de la categoria *Laberint* que s'han completat amb estat *OK*).

**Compte!** Tots els intervals de criteris han de tenir exactament la mateixa mida (mateix nombre de files i columnes). Si no és així, la fórmula dona un error `#VALUE!`.

---

## SUMIFS

**Documentació:** <https://support.google.com/docs/answer/3238496?hl=ca>

**Què fa:** Suma els valors d'un interval de cel·les que compleixen una o més condicions especificades en altres intervals.

**Sintaxi:**

```excel
SUMIFS(interval_de_suma, interval_de_criteris1, criteri1, [interval_de_criteris2, criteri2, ...])
```

| Argument | Obligatori? | Què és |
|---|---|---|
| `interval_de_suma` | Sí | L'interval que conté els valors numèrics que es volen sumar. |
| `interval_de_criteris1` | Sí | El primer interval de cel·les on es comprovarà el criteri. |
| `criteri1` | Sí | La condició que han de complir les cel·les del primer interval. |
| `interval_de_criteris2` | No | Un segon interval de cel·les per avaluar un altre criteri. |
| `criteri2` | No | La condició del segon interval. |

**Exemple de la documentació:** `SUMIFS(A1:A10, B1:B10, ">20", C1:C10, "<30")`

**El meu exemple amb la lliga:**

```excel
=SUMIFS(Jornada1!R2:R49, Jornada1!E2:E49, "Cable Suelto", Jornada1!N2:N49, "OK")
```

Resultat: `34` (És la suma total dels punts obtinguts per l'equip *Cable Suelto* en les curses acabades en estat *OK*).

**Compte!** L'interval de suma va **sempre al principi** de la funció (a diferència de `SUMIF`, on va al final), i tots els intervals han de tenir la mateixa mida exacta.

---

## IFS

**Documentació:** <https://support.google.com/docs/answer/7014145?hl=ca>

**Què fa:** Avalua una seqüència de condicions en ordre i retorna el valor corresponent a la primera condició que sigui certa (`TRUE`).

**Sintaxi:**

```excel
IFS(condició1, valor1, [condició2, valor2, ...])
```

| Argument | Obligatori? | Què és |
|---|---|---|
| `condició1` | Sí | La primera prova lògica a avaluar (`TRUE` o `FALSE`). |
| `valor1` | Sí | El valor que es retorna si la `condició1` és certa. |
| `condició2` | No | Segona prova lògica si la primera és falsa. |
| `valor2` | No | Valor a retornar si la `condició2` és certa. |

**Exemple de la documentació:** `IFS(A1:A5 > 3, "més gran", A1:A5 = 3, "igual")`

**El meu exemple amb la lliga:**

```excel
=IFS(N2="DSQ", 0, N2="DNF", 1, J2=MINIFS(J$2:J$49, G$2:G$49, G2, N$2:N$49, "OK"), 10, J2<=AVERAGEIFS(J$2:J$49, G$2:G$49, G2, N$2:N$49, "OK"), 6, TRUE, 3)
```

Resultat: `6` (A la fila 2, avalua si la cursa és DSQ, DNF, millor temps o per sota de la mitjana. Com que el temps és menor o igual a la mitjana de la seva categoria, li assigna 6 punts).

**Compte!** Si cap de les condicions avaluades és certa (`TRUE`), la funció retorna un error `#N/A`. S'evita posant com a darrera condició el valor `TRUE` amb un valor per defecte.

---

## XLOOKUP

**Documentació:** <https://support.google.com/docs/answer/12405947?hl=ca>

**Què fa:** Busca un valor concret en un interval i retorna el valor equivalent situat a la mateixa posició d'un altre interval.

**Sintaxi:**

```excel
XLOOKUP(valor_de_cerca, interval_de_cerca, interval_de_resultats, [valor_no_trobat], [mode_de_coincidència], [mode_de_cerca])
```

| Argument | Obligatori? | Què és |
|---|---|---|
| `valor_de_cerca` | Sí | El valor o text que es vol buscar. |
| `interval_de_cerca` | Sí | L'interval o columna on es realitzarà la cerca. |
| `interval_de_resultats` | Sí | L'interval o columna d'on s'agafarà el resultat equivalent. |
| `valor_no_trobat` | No | El text o valor que es mostra si no es troba cap coincidència. |
| `mode_de_coincidència` | No | Especifica el tipus de cerca (0 per a coincidència exacta). |
| `mode_de_cerca` | No | Especifica la direcció de cerca (1 de primer a darrer). |

**Exemple de la documentació:** `XLOOKUP("Poma", E2:E7, A2:A7)`

**El meu exemple amb la lliga:**

```excel
=XLOOKUP("J1-029", Jornada1!A2:A49, Jornada1!E2:E49, "No existeix")
```

Resultat: `"Cable Suelto"` (Cerca l'ID de la cursa `J1-029` a la columna A i ens torna el nom de l'equip corresponent de la columna E).

**Compte!** Si no es posa el quart argument (`valor_no_trobat`) i la cerca no troba cap resultat, la funció torna un error `#N/A`.

---

## ⭐ Extres: AVERAGEIFS, MAXIFS, UNIQUE, SORT

---

## AVERAGEIFS

**Documentació:** <https://support.google.com/docs/answer/3256534?hl=ca>

**Què fa:** Calcula la mitjana aritmètica dels valors d'un interval que compleixen un o diversos criteris.

**Sintaxi:**

```excel
AVERAGEIFS(interval_mitjana, interval_de_criteris1, criteri1, [interval_de_criteris2, criteri2, ...])
```

| Argument | Obligatori? | Què és |
|---|---|---|
| `interval_mitjana` | Sí | L'interval de cel·les numèriques de les quals es vol calcular la mitjana. |
| `interval_de_criteris1` | Sí | El primer interval on es comprovarà el criteri. |
| `criteri1` | Sí | La condició que han de complir les cel·les del primer interval. |
| `interval_de_criteris2` | No | Segon interval de criteris. |
| `criteri2` | No | Segona condició. |

**Exemple de la documentació:** `AVERAGEIFS(A1:A10, B1:B10, ">20", C1:C10, "<30")`

**El meu exemple amb la lliga:**

```excel
=AVERAGEIFS(Jornada1!J2:J49, Jornada1!G2:G49, "Seguidor de línia", Jornada1!N2:N49, "OK")
```

Resultat: `25.74` (Indica que el temps mitjà en segons de les curses acabades en estat *OK* a la categoria *Seguidor de línia* és de 25,74 segons).

**Compte!** Si cap cel·la compleix tots els criteris o si totes les cel·les avaluades estan buides, la funció torna un error `#DIV/0!`.

---

## MAXIFS

**Documentació:** <https://support.google.com/docs/answer/7013817?hl=ca>

**Què fa:** Retorna el valor màxim d'un interval de cel·les que compleixen una o més condicions.

**Sintaxi:**

```excel
MAXIFS(interval_de_màxims, interval_de_criteris1, criteri1, [interval_de_criteris2, criteri2, ...])
```

| Argument | Obligatori? | Què és |
|---|---|---|
| `interval_de_màxims` | Sí | L'interval de cel·les d'on s'obtindrà el valor màxim. |
| `interval_de_criteris1` | Sí | El primer interval on s'avaluaran els criteris. |
| `criteri1` | Sí | La condició del primer interval. |
| `interval_de_criteris2` | No | Segon interval de criteris. |
| `criteri2` | No | Segona condició. |

**Exemple de la documentació:** `MAXIFS(A1:A10, B1:B10, ">20", C1:C10, "<30")`

**El meu exemple amb la lliga:**

```excel
=MAXIFS(Jornada1!J2:J49, Jornada1!G2:G49, "Laberint", Jornada1!N2:N49, "OK")
```

Resultat: `117.54` (Representa el pitjor temps / temps màxim registrat en una cursa acabada en *OK* de la categoria *Laberint*).

**Compte!** Si cap cel·la compleix els criteris, la funció retornarà `0` (no pas un error), la qual cosa pot ser enganyosa si es treballa amb valors positius i negatius.

---

## UNIQUE

**Documentació:** <https://support.google.com/docs/answer/10522653?hl=ca>

**Què fa:** Extreu i retorna els valors o files úniques d'un interval, descartant totes les repeticions.

**Sintaxi:**

```excel
UNIQUE(interval, [per_columna], [exactament_una_vegada])
```

| Argument | Obligatori? | Què és |
|---|---|---|
| `interval` | Sí | El rang de cel·les del qual es volen extreure els valors únics. |
| `per_columna` | No | Indica si es filtren columnes (`TRUE`) o files (`FALSE`). |
| `exactament_una_vegada` | No | Si és `TRUE`, només retorna els valors que no apareixen cap vegada repetits. |

**Exemple de la documentació:** `UNIQUE(A1:C10)`

**El meu exemple amb la lliga:**

```excel
=UNIQUE(Jornada1!E2:E49)
```

Resultat: Genera automàticament la llista vertical dels `10 equips` de la lliga, eliminant les repeticions de les 48 curses.

**Compte!** Com que la funció desplega els resultats cap avall en cel·les inferiors, si aquestes cel·les contenen dades prèvies, la fórmula donarà un error `#REF!`.

---

## SORT

**Documentació:** <https://support.google.com/docs/answer/3093150?hl=ca>

**Què fa:** Ordena les files d'un interval o matriu segons els valors d'una o més columnes.

**Sintaxi:**

```excel
SORT(interval, columna_d_ordenació, és_ascendent, [columna_d_ordenació2, és_ascendent2, ...])
```

| Argument | Obligatori? | Què és |
|---|---|---|
| `interval` | Sí | El rang de dades que es vol ordenar. |
| `columna_d_ordenació` | Sí | L'índex o columna per la qual s'ordenarà l'interval. |
| `és_ascendent` | Sí | `TRUE` per ordenar de menor a major / A-Z, o `FALSE` per ordenar de major a menor / Z-A. |
| `columna_d_ordenació2` | No | Segona columna d'ordenació en cas d'empat. |
| `és_ascendent2` | No | Sentit d'ordenació de la segona columna. |

**Exemple de la documentació:** `SORT(A1:C10, 1, TRUE)`

**El meu exemple amb la lliga:**

```excel
=SORT(UNIQUE(Jornada1!E2:E49))
```

Resultat: Desplega la llista dels 10 equips de la lliga ordenats alfabèticament de la A a la Z (des de *Bits de Mar* fins a *Team Arduino*).

**Compte!** Igual que passa amb `UNIQUE`, si el rang on s'ha de desplegar el resultat ordenat no està buit, la fórmula fallarà amb un error `#REF!`.

---

## Preguntes de lectura

1. **Què passa amb `SUMIFS` si l'interval de suma i l'interval del criteri no tenen la mateixa mida?**  
   Retorna un error de tipus `#VALUE!`. Google Sheets requereix que tots els intervals tinguin exactament les mateixes dimensions (mateix nombre de files i columnes) per poder relacionar cada cel·la de criteri amb la cel·la corresponent a sumar.

2. **Què torna `IFS` si cap de les condicions és certa? Com ho podeu evitar?**  
   Torna l'error `#N/A`. Es pot evitar afegint com a darrera condició el valor `TRUE` (o `1=1`) seguit del valor o text per defecte que es vol mostrar quan cap condició anterior s'hagi après (per exemple: `, TRUE, 3`).

3. **Per a què serveix el quart argument de `XLOOKUP`? Què passa si no el poseu i no es troba res?**  
   Serveix per especificar el text o valor personalitzat que ha de retornar la funció quan no es troba cap coincidència (per exemple `"No existeix"`). Si no es posa i la cerca no troba cap resultat coincident, la funció retornarà l'error per defecte `#N/A`.

4. **Escriu la sintaxi de `SUMIF` i la de `SUMIFS` una sota l'altra. Què canvia de lloc?**  
   - `SUMIF(interval, criteri, [interval_suma])`
   - `SUMIFS(interval_suma, interval_criteris1, criteri1, [interval_criteris2, criteri2, ...])`  
   **Què canvia de lloc:** A `SUMIF` l'interval de suma és opcional i es col·loca **al final**, mentre que a `SUMIFS` l'interval de suma és obligatori i es col·loca **al principi de tot** (com a primer argument).