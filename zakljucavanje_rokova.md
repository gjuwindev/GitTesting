## EVIDENTIRANJE OCJENE NULA TAMO GDJE NE POSTOJI KONACNA OCJENA, ZAKLJUCAVANJE ROKOVA KOJI SE DAJU ZAKLJUCATI, IZVJESTAJ = SLOZENO, DUZE TRAJE  
_ODABRANA OPCIJA (19.4.2018. Tanja)_


### 1. DOHVAT PODATAKA O SVIM ISPITNIM ROKOVIMA, ZA SVE GODINE  
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



**DETALJNI PODACI O ISPITNOM ROKU**    
URL: `nastavniplan/rok/predmet/{sifraPredmetaUIsvu}/{godina}/{mjesec}/{dan}/vrstaroka/{vrstaRoka}`

HTTP metoda: `GET`

Opis: Dohvat detaljnih podataka o ispitnom roku po datumu i vrsti roka. 

Reprezentacija: `application/vnd.isvu.ispitnirok.xml-v1.0+xml`

Rezultat: 
```{xml}
<ispitniRok>
  <predmet sifra="36534">
    <naziv>Djelovanje carskog i kraljevskog središnjeg povjerenstva u Istri i Dalmaciji 1850.-1918.</naziv>
  </predmet>
  <rok>
    <datumRoka>13.09.2010.</datumRoka>
    <vrstaRoka oznaka="R">redovni rok</vrstaRoka>
    <pismeni>DA</pismeni>
    <vrijemePrijaveDo>07.09.2010. 23:59</vrijemePrijaveDo>
    <vrijemeOdjaveDo>10.09.2010. 12:00</vrijemeOdjaveDo>
    <zakljucan>DA</zakljucan>
    <objavljeniRezultatiPismenog>NE</objavljeniRezultatiPismenog>
    <obavijesti />
  </rok>
</ispitniRok>
```

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


### 2. DOHVAT REZULTATA USMENOG ISPITA ZA DOHVACENE ROKOVE

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


### 3. EVIDENTIRATI ZA SVE STUDENTE KOJI NEMAJU KONACNU OCJENU
    1.	ocjena = 0 (nula)
    2.	datum ispita = datum roka (obavezno tocka iza godine!)
    3.	ocjenjivac = nositelj


### 4. DOHVAT PODATAKA O PREDMETU U AKADEMSKOJ GODINI > OZNAKA NOSITELJA

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

### 5. AKO NEMA EVIDENTIRANOG NOSITELJA - ocjenjivac je procelnik

- popis procelnika (oznakaOsobe) po godinama za ustrojstvene jedinice (mimo REST API-ja)
- ustrojstvena jedinica koja izvodi kolegij 

**DETALJNI PODACI O PREDMETU**

URL: `nastavniprogram/predmet/sifra/{sifraPredmetaUIsvu}`

HTTP metoda: `GET`

Opis: Vraća detaljne podatke o predmetu.

Reprezentacija: `application/vnd.isvu.predmet.xml-v1.1+xml`

Rezultat:
`<ustrojstvenaJedinicaKojojPripada sifra="100073">`

- preuzeti podatak o osobi koja je procelnik za tu ustrojstvenu jedinicu u akademskoj godini (istoj onoj za koju smo dohvatili podatke o izvodjacima) - za to moramo imati posebnu tablicu:  
|UstrJedinica|AkadGodina|Procelnik|  
- evidentirati procelnika kao nositelja

**IZVODJAC**

URL: `nastavniprogram/predmet/akademskagodina/{akademskaGodina}/sifra/{sifraPredmeta}/semestar/{semestar}/izvedba/{izvedbaPredmeta}/komponenta/{komponentaPredmeta}/vrstanastave/{vrstaNastave}/izvodjac`

HTTP metoda: `POST`

Opis: Evidencija **izvođača** za predmet u akademskoj godini.

Reprezentacija: `application/vnd.isvu.predakgodizvodjac.xml-v1.0+xml`


URL: `nastavniprogram/predmet/akademskagodina/{akademskaGodina}/sifra/{sifraPredmeta}/semestar/{semestar}/izvedba/{izvedbaPredmeta}/komponenta/{komponentaPredmeta}/vrstanastave/{vrstaNastave}/izvodjac/oznaka/{oznakaOsoba}`

HTTP metoda: `PUT`

Opis: Promjena rednog broja **nositelja** za evidentiranog izvođača na predmetu u akademskoj godini. 

Reprezentacija: `application/vnd.isvu.predakgodnositelj.xml-v1.0+xml`



### 6. ZAKLJUCAVANJE SVIH NEZAKLJUCANIH ROKOVA

### 7. IZVJESTAJ/POPIS ROKOVA KOJI NISU MOGLI BITI ZAKLJUCANI
