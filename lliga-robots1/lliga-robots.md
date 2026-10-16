# Lliga de robots jornada 1 
##  M0 · Inspecció de l'arxiu en origen (abans d'obrir Sheets) 
### Quin caràcter s'utilitza com a delimitador de columnes?
* S'utilitza la coma
    
### Per quin motiu alguns camps de text estan delimitats entre cometes i d'altres no?
* Estan delimitats amb cometes perquè es text 
    
### Quantes files de registres conté el fitxer (sense comptar la capçalera)?
* En te 49

## M1 · Importació i configuració regional

### Justifiqueu per quin motiu aquesta configuració és necessària abans de realitzar la importació del fitxer.
* És necessària perquè el fitxer CSV utilitza el punt com a separador (el format de USA i altres paisos). Si mantens la configuració d'Espanya, no es convertiran correctament en números ni en dates perque agafara la coma com a separador.


## M4 · Càlcul de durades i representació temporal interna

 ### Quina diferència s'observa si s'aplica el format Hora respecte al format Durada? Quina és la causa d'aquest comportament?
 * Amb el format Hora es mostra 05:00:00 perquè actua com un rellotge que es reinicia en passar de 24 hores, pero que el format Durada mostra 29:00:00 perquè acumula tot el temps.

### Quin valor decimal s'obté i quin significat físic té?
* S'obté el valor decimal 0,5, que es la meitat d'un dia sencer (24h) hores.

## M5 · Format condicional mitjançant criteris predefinits
### És coherent comparar directament els temps de categories tècnicament diferents com Laberint i Velocitat? Com es podria millorar aquesta segmentació?

* No és coherent. Les proves laberint i Velocitat són massa diferents per comparar-les juntes. Un bon temps al laberint pot semblar molt lent a velocitat, i això fa que els colors enganyin i perdin el sentit si es barregen totes les dades de cop. Es podria millorar aplicant regles d'escala de colors diferents per a cada categoria.

## M6 · Format condicional basat en fórmules (ressaltat de files completes)

### Justifiqueu la necessitat d'utilitzar la referència mixta ($N2), amb bloqueig exclusiu de la columna.
* Fem servir $N2 per fixar la columna N (on hi ha DNF o DSQ). Així, totes les cel·les de la mateixa fila miren sempre la columna N per saber si tota la fila s'ha de pintar o no.

