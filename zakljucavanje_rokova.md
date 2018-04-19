## EVIDENTIRANJE OCJENE NULA TAMO GDJE NE POSTOJI KONACNA OCJENA, ZAKLJUCAVANJE ROKOVA KOJI SE DAJU ZAKLJUCATI, IZVJESTAJ = SLOZENO, DUZE TRAJE  
_ODABRANA OPCIJA (19.4.2018. Tanja)_


### DOHVAT PODATAKA O SVIM ISPITNIM ROKOVIMA, ZA SVE GODINE  
**POPIS PREDMETA**  
URL: `nastavniprogram/predmet/akademskagodina/{akademskaGodina}`  
HTTP metoda: `GET`  
Opis: Vraća popis svih predmeta koji se nalaze u nastavnom programu u akademskoj godini.  
Reprezentacija: `application/vnd.isvu.predmetuakgod.xml-v1.0+xml`  
Rezultat: 
```{xml}
<predmeti akademskaGodina="2007">
  <predmet sifra="37848">
    <naziv>Engleski jezik struke 2</naziv>
  </predmet>
 </predmeti>
```

**ROKOVI ZA PREDMET**    
URL: `nastavniplan/rok/predmet/{sifraPredmetaUIsvu}/akademskagodina/{akademskaGodina}`  
HTTP metoda: `GET`  
Opis: Vraća popis ispitnih rokova u akademskoj godini za predmet. Popis sadrži datume i vrste ispitnih rokova.
Reprezentacija: `application/vnd.isvu.ispitniroklista.xml-v1.1+xml`

**ZAKLJUCAVANJE ROKA**  
URL: `ispit/rok/{godinaRok}/{mjesecRok}/{danRok}/predmet/{sifraPredmetaUIsvu}/vrstaroka/{vrstaRoka}/zahtjevzazakljucavanje`  
HTTP metoda: `POST`  
Opis: Zaključavanje ispitnog roka. Ovisno o upisanoj vrijednosti (DA, NE) u elementu `<ponistiOslobodenje>`, studentima će se kod zaključavanja poništiti oslobođenja, odnosno neće ako je vrijednost elementa NE. Primjer xml dokumenta kojeg je potrebno postaviti u tijelo zahtjeva  
Reprezentacija: `application/vnd.isvu.zakljucavanjeispitnogroka.xml-v1.0+xml`  
```{xml}
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<zakljucavanjeIspitnogRoka>	
	<ponistiOslobodenje>NE</ponistiOslobodenje>
</zakljucavanjeIspitnogRoka>

```



### dohvat rezultata usmenog ispita za dohvacene rokove




### evidentirati za sve studente koji nemaju konacnu ocjenu
    1.	ocjena = 0 (nula)
    2.	datum ispita = datum roka
    3.	ocjenjivac = nositelj




### dohvat podataka o predmetu u akademskoj godini > oznaka nositelja

 -  ako NEMA NOSITELJA?




### zakljucavanje svih nezakljucanih rokova




### izvjestaj/popis rokova koji nisu mogli biti zakljucani
