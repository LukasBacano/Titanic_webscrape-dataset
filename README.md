# Titanic Passenger List Scraping

## Beskrivelse
Dette script er udviklet til at scrape data fra **Encyclopedia Titanica** og organisere information om Titanic-passagerer i en struktureret dataset. Oprindeligt var opgaven at finde passagerer mellem K-O, men vi tog i stedet alle vi kunne.

## Krav
Før du kører scriptet, skal du sikre dig, at du har følgende R-pakker installeret:
```r
install.packages(c("rvest", "httr", "stringr", "dplyr"))
```

## Hvad gør scriptet?
### 1. Henter passager-links
- Laver en forespørgsel til siden med Titanic-passagerlisten.
- Ekstraherer links til **Titanic-victim** og **Titanic-survivor** profiler.

### 2. Scraper individuelle passagerer
- Loop'er igennem alle passagerlinks og henter deres "summary"-sektion.
- Samler information i en dataframe.

### 3. Rydder og strukturerer data
- **Ekstraherer** specifikke informationer med `stringr`, herunder:
  - Navn, alder, køn, fødested, nationalitet, civilstatus.
  - Klasse, billetnummer, billetpris, kahytnummer.
  - Hvor de gik ombord og afskibede, om de blev reddet eller døde.
  - Begravelsessted, hvis relevant.
- **Renser HTML-artefakter**, såsom `.fa-secondary{opacity:.4}`.
- **Omdøber dobbelte navne** (James Kelly) for at differentiere dem.
- **Omstrukturerer kolonner** så dataset er let at analysere.

### 4. Eksporterer datasæt
- Gemmer `scrapedTitanic` som en `.RDS`-fil til senere brug.

## Sådan bruger du scriptet
1. **Definér din sti til data**:
   - Opdater `DIN_PATH_HER` med din ønskede gemmeplacering.
2. **Kør scriptet i RStudio eller R**.
3. **Indlæs datasættet senere med**:
   ```r
   scrapedTitanic <- readRDS("DIN_PATH_HER")
   ```

## Forventet output
Efter kørsel af scriptet vil du have et pænt struktureret datasæt med Titanic-passagerer i følgende format:

| Name | Sex | Age | Class | Ticket_No | Ticket_price | Rescued |
|------|-----|-----|-------|-----------|--------------|---------|
| Mr. John Smith | Male | 32 | 1st Class | 112233 | £150 | Yes |
| Miss Anna Brown | Female | 19 | 2nd Class | 445566 | £75 | No |

---
### 🚢 **Nu kan du analysere Titanic-passagerer i R!** 🚢

