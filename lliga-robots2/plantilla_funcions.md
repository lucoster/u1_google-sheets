# Les meves fitxes de funcions de Google Sheets

> Copia aquesta plantilla al teu repositori com a `funcions.md`. Fes una fitxa per funció.
> Escriu amb les teves paraules. Els exemples de la lliga, provats al teu full.

---

## COUNTIFS

**Documentació:** <https://support.google.com/docs/answer/3256550?hl=ca>

**Què fa:** Compta quantes caselles compleixen una o mes condicions, dins d'un interval.

**Sintaxi:**

```
COUNTIFS(interval_de_criteris1, criteri1, [interval_de_criteris2, criteri2, etc.])
```

| Argument | Obligatori? | Què és |
|---|---|---|
| `...` | Sí | ... |
| `...` | No | ... |

**Exemple de la documentació:** `COUNTIFS(B8:B27, ">" & B12, C8:C27, "<" & C13, D8:D27, “<>10”)`

**El meu exemple amb la lliga:**

```
=COUNTIFS(...)
```

Resultat: `...` (què vol dir aquest número?)

**Compte!** (una cosa que diu l'apartat *Notes* de la documentació i que pot fer fallar la fórmula)

---

## SUMIFS

**Documentació:** https://support.google.com/docs/answer/3238496?hl=ca

**Què fa:** Suma les caselles, dins d'un interval que compleixin una o mes condicions.

**Sintaxi:**

```
SUMIFS(interval_de_suma, interval_de_criteris1, criteri1, [interval_de_criteris2, criteri2, etc.])
```

| Argument | Obligatori? | Què és |
|---|---|---|
| `...` | Sí | ... |
| `...` | No | ... |

**Exemple de la documentació:** `SUMIFS(A1:A10, B1:B10, ">20", C1:C10, "<30")`

**El meu exemple amb la lliga:**

```
=COUNTIFS(...)
```

Resultat: `...` (què vol dir aquest número?)

**Compte!** (una cosa que diu l'apartat *Notes* de la documentació i que pot fer fallar la fórmula)

---


## IFS

**Documentació:** https://support.google.com/docs/answer/7014145?hl=ca

**Què fa:** Evalua una o mes condicions dins d'un interval i et torna el primer valor cert.

**Sintaxi:**

```
IFS(condició, valor1, [condició2, valor2, …])
```

| Argument | Obligatori? | Què és |
|---|---|---|
| `...` | Sí | ... |
| `...` | No | ... |

**Exemple de la documentació:** `IFS(A1:A5 > 3, "més gran", A1:A5 = 3, "igual")`

**El meu exemple amb la lliga:**

```
=COUNTIFS(...)
```

Resultat: `...` (què vol dir aquest número?)

**Compte!** (una cosa que diu l'apartat *Notes* de la documentació i que pot fer fallar la fórmula)

---

## XLOOKUP

**Documentació:** https://support.google.com/docs/answer/3238496?hl=ca

**Què fa:** Busca certa cosa en un interval i et tornal el equivalent en un altre

**Sintaxi:**

```
XLOOKUP(valor_de_cerca; interval_cerca; interval_de_resultats, valor_no_trobat; mode_de_coincidència; mode_de_cerca)
```

| Argument | Obligatori? | Què és |
|---|---|---|
| `...` | Sí | ... |
| `...` | No | ... |

**Exemple de la documentació:** `XLOOKUP("Poma"; E2:E7; A2:A7)`

**El meu exemple amb la lliga:**

```
=COUNTIFS(...)
```

Resultat: `...` (què vol dir aquest número?)

**Compte!** (una cosa que diu l'apartat *Notes* de la documentació i que pot fer fallar la fórmula)

---

## ⭐ Extres: AVERAGEIFS, MAXIFS, UNIQUE, SORT

(mateixa estructura)

---

## Preguntes de lectura

1. Què passa amb `SUMIFS` si l'interval de suma i l'interval del criteri no tenen la mateixa mida?
2. Què torna `IFS` si cap de les condicions és certa? Com ho podeu evitar?
3. Per a què serveix el quart argument de `XLOOKUP`? Què passa si no el poseu i no es troba res?
4. Escriu la sintaxi de `SUMIF` i la de `SUMIFS` una sota l'altra. Què canvia de lloc?