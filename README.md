# Navodila za člane laboratorija

Dobrodošli v repozitoriju za laboratorij! Ta repozitorij uporablja Hugo za izdelavo spletne strani s pomočjo GitHub Pages. V tem dokumentu so podrobna navodila, kako nastaviti svoj repozitorij, ustvariti objave, in poskrbeti, da bo vaša vsebina pravilno prikazana na spletni strani laboratorija.

## 1. Ustvarite osebni repozitorij iz predloge

1. **Ustvarite repozitorij**:

   - Uporabite predlogo repozitorija za člane laboratorija, ki je bila pripravljena, da pospeši postopek nastavitve.
   - Obiščite predlogo in kliknite **Use this template**, da ustvarite svoj osebni repozitorij na podlagi te predloge.

2. **Klonirajte repozitorij lokalno**:

   - Po ustvarjanju repozitorija ga klonirajte na svojo lokalno napravo:
     ```bash
     git clone https://github.com/vaš-uporabniški-ime/ime-repozitorija.git
     ```

3. **Konfiguracija v lokalnem okolju**:
   - Prepričajte se, da imate nameščen Hugo (če ga še nimate, sledite [navodilom](https://gohugo.io/getting-started/installing/)).
   - Po kloniranju repozitorija, odprite mapo in zaženite lokalni strežnik za predogled:
     ```bash
     cd ime-repozitorija
     hugo server
     ```
   - Spletno mesto bo na voljo na naslovu `http://localhost:1313`.

## 2. Osebni dostopni žeton (PAT)

Ker bo root repozitorij kloniral vsebino vašega repozitorija med gradnjo spletne strani, morate ustvariti osebni dostopni žeton (PAT) in ga posredovati administratorju.

1. **Ustvarite nov PAT**:

   - Pojdite na svoj profil na [GitHub](https://github.com) in izberite **Settings**.
   - V meniju na levi izberite **Developer settings** > **Personal access tokens**.
   - Kliknite **Generate new token**.
   - Dodajte opis (npr. "Dostop za root repozitorij") in označite naslednje pravice:
     - **repo** (za dostop do zasebnih repozitorijev)
     - **workflow** (za omogočanje GitHub Actions)
   - Kliknite **Generate token** in kopirajte žeton.

2. **Posredovanje žetona**:
   - Posredujte administratorju root repozitorija vaš PAT, da ga lahko shrani kot skrivnost (`Secret`) v root repozitoriju. Administrator bo dodal vaš PAT v GitHub Secrets, da bo omogočen dostop do vašega repozitorija.

## 3. Spremembe v root repozitoriju

Po nastavitvi vašega repozitorija in posredovanju PAT, bo moral administrator root repozitorija prilagoditi GitHub Actions skripto, da bo vsebina iz vašega repozitorija vključena na glavno spletno stran.

1. **Posodobitev GitHub Actions skripte**:

   - Administrator mora odpreti `.github/workflows/deploy.yml` v root repozitoriju in dodati naslednjo vrstico, ki omogoča kloniranje vašega repozitorija:
     ```bash
     git clone https://${{ secrets.MEMBER1_PAT }}@github.com/vaše-uporabniško-ime/ime-repozitorija.git content/members/vaše-uporabniško-ime/
     ```

2. **Prilagoditev navigacije**:
   - Administrator bo dodal vaš profil v **Seznam članov**, ki bo prikazan na glavni strani spletnega mesta.

## 4. Določite svojo biografijo

- Ustvarite datoteko `config.toml` v svojem repozitoriju, kjer lahko definirate podatke o sebi, na primer:
  ```toml
  bio = "Sem član laboratorija in me zanima področje umetne inteligence."
  cover = "/pot-do-slike-profila.jpg"
  ```

## Nastavitev osebnega dostopnega žetona (PAT)

Za omogočanje root repozitoriju, da dostopa do vašega repozitorija, potrebujete osebni dostopni žeton (PAT). Tukaj so koraki:

1. **Ustvarite nov PAT**:

   - Pojdite na svoj profil na [GitHub](https://github.com) in izberite **Settings**.
   - V meniju na levi izberite **Developer settings** > **Personal access tokens**.
   - Kliknite **Generate new token**.
   - Dajte žetonu opis (npr. "Dostop za root repozitorij") in izberite:
     - **repo** (za dostop do zasebnih repozitorijev)
     - **workflow** (za omogočanje GitHub Actions)
   - Kliknite **Generate token** in kopirajte žeton na varno mesto.

2. **Shranjevanje PAT v root repozitorij**:
   - Pošljite administratorju root repozitorija svoj PAT, da ga shrani v GitHub Secrets.

## Spremembe v root repozitoriju

Ko ustvarite svoj repozitorij, mora administrator root repozitorija izvesti naslednje korake:

1. **Posodobitev GitHub Actions skripte**:

   - V root repozitoriju odprite `.github/workflows/deploy.yml`.
   - Dodajte naslednjo vrstico za kloniranje vašega repozitorija:
     ```bash
     git clone https://${{ secrets.MEMBER1_PAT }}@github.com/username-content.git content/members/username/
     ```

2. **Prilagoditev navigacije**:
   - Poskrbite, da bo vaš profil pravilno dodan na **Seznam članov** v root repozitoriju, če je potrebno.

## Ustvarjanje objav

1. **Dodajanje nove objave**:

   - V svojem repozitoriju ustvarite mapo za novo objavo pod `content/post/` in ustvarite datoteko `index.md` z vsebino vaše objave.
   - Primer:

     ```
     content/
       post/
         druga-objava/
           index.md
     ```

   - Datoteka `index.md`:

     ```markdown
     ---
     title: "Naslov moje druge objave"
     date: 2024-09-15
     author: "Vaše ime"
     cover: "/pot-do-slike.jpg"
     ---

     Vsebina moje druge objave.
     ```

2. **Push spremembe**:

   - Ko končate z urejanjem, push-ajte svoje spremembe na GitHub:
     ```bash
     git add .
     git commit -m "Dodana nova objava"
     git push origin main
     ```

3. **Objave in prikaz**:
   - Vaše objave bodo samodejno vključene na vašo stran v root repozitoriju ob naslednjem zagonu GitHub Actions.

## Urejanje biografije

1. **Posodobitev biografije**:

   - Če želite posodobiti svojo biografijo ali slike, uredite datoteko `config.toml` v svojem repozitoriju.

2. **Struktura biografije**:
   - Prepričajte se, da vsebuje informacije, kot so `bio`, `cover` (pot do slike) in drugi podatki, ki jih želite prikazati na svoji osebni strani.

---
