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

XML za unos:
```{xml}
   <?xml version="1.0" encoding="UTF-8" standalone="yes"?>
<zakljucavanjeIspitnogRoka>	
	<ponistiOslobodenje>NE</ponistiOslobodenje>
</zakljucavanjeIspitnogRoka>

```


### DOHVAT REZULTATA USMENOG ISPITA ZA DOHVACENE ROKOVE

**POPIS REZULTATA USMENOG ISPITA**  
URL: `ispit/usmeni/{sifraPredmetaUISVU}/{godinaRok}/{mjesecRok}/{danRok}`  

HTTP metoda: `GET`  

Opis: Vraća popis JMBAG-ova studenata s pripradnom ocjenom usmenog ispita i rednim brojem izlaska na ispit. Omogućen dohvat ispita s ocjenama 'P' i 'N'.  

Reprezentacija: application/vnd.isvu.rezultatusmenilista.xml-v1.1+xml

**DETALJNI PODACI O REZULTATU USMENOG ISPITA ZA STUDENTA**  

>URL: `ispit/usmeni/{sifraPredmetaUISVU}/{godinaRok}/{mjesecRok}/{danRok}/{jmbag}`
>
>HTTP metoda: `GET`
>
>Opis: Vraća detaljne podatke o rezultatima usmenog ispita za nekog studenta. Uključuje podatke o studentu, ocjenjivaču, datum ispita i ocjenu. Omogućen dohvat ispita s ocjenama 'P' i 'N'.
>
>Reprezentacija: application/vnd.isvu.rezultatusmeni.xml-v1.1+xml  


URL: `ispit/usmeni/{sifraPredmetaUISVU}/{godinaRok}/{mjesecRok}/{danRok}/{jmbag}`

HTTP metoda: `PUT`

Opis: Omogućava izmjenu podataka o rezultatu usmenog ispita. Moguće je mijenjati oznaku ocjenjivača ispita, ocjenu (0, 1, 2, 3, 4, 5, P, N) i datum ispita.

Reprezentacija: application/vnd.isvu.rezultatusmeni.xml-v1.1+xml

XML Schema: ispit/rezultatusmeni-v1.1.xsd

XML za unos:
```{xml}
<?xml version="1.0" encoding="utf-8"?>
<rezultatUsmeni>
  <ispit redniBrojIzlaska="1">
    <student>
      <jmbag>0130280474</jmbag>
    </student>
    <ocjenjivac>
      <oznaka>ZB035</oznaka>
    </ocjenjivac>
    <ocjena>2</ocjena>
    <datumIspita>25.02.2018.</datumIspita>
<!--mora ici tockica iza godine!-->
  </ispit>
</rezultatUsmeni>
```


### EVIDENTIRATI ZA SVE STUDENTE KOJI NEMAJU KONACNU OCJENU
    1.	ocjena = 0 (nula)
    2.	datum ispita = datum roka (obavezno tocka iza godine!)
    3.	ocjenjivac = nositelj


### DOHVAT PODATAKA O PREDMETU U AKADEMSKOJ GODINI > OZNAKA NOSITELJA

 -  ako NEMA NOSITELJA

**PREDMET U AKADEMSKOJ GODINI**

URL: `nastavniprogram/predmet/akademskagodina/{akademskaGodina}/sifra/{sifraPredmeta}`

HTTP metoda: `GET`

Opis: Vraća podatke o predmetu u akademskoj godini: opis predmeta, literatura, **izvođač/nositelj** (`<izvodjac redniBrojNositelja="1">` i `<oznaka>HK012</oznaka>`) na predmetu za vrstu nastave, izvedba grupe za izvođača/nositelja u postocima, jezik.

Reprezentacija: `application/vnd.isvu.predakgod.xml-v1.1+xml`

Rezultat:
```{xml}
<predmetUAkademskojGodini sifra="118160" akademskaGodina="2017" sifraPredmeta="118160">
  <naziv>1968. - Uzroci i posljedice</naziv>
  <akademskaGodina>2017</akademskaGodina>
  <opisPredmeta />
  <literature />
  <izvodjaciZaPredmetUAkademskojGodini>
    <semestar redniBrojUAkademskojGodini="2">
      <izvedba redniBroj="1">
        <komponenta redniBroj="1">
          <vrstaNastave oznakaVrstaNastave="P">
            <izvodjaci>
              <izvodjac redniBrojNositelja="1">
                <oznaka>HK012</oznaka>
                <ime>Hrvoje</ime>
                <prezime>Klasić</prezime>
                <grupe />
              </izvodjac>
            </izvodjaci>
          </vrstaNastave>
        </komponenta>
      </izvedba>
    </semestar>
  </izvodjaciZaPredmetUAkademskojGodini>
  <jezici />
</predmetUAkademskojGodini>
```

### ZAKLJUCAVANJE SVIH NEZAKLJUCANIH ROKOVA

### IZVJESTAJ/POPIS ROKOVA KOJI NISU MOGLI BITI ZAKLJUCANI
