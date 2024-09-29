# Viikko 4

## Koostetietokysely-harjoitukset

### 1. Kuinka korkealla sijaitsee korkeimmalla sijaitseva lentokenttä?

`select max(elevation_ft) from airport;`

![](kuvat/viikko4/koostetieto/1.png)

### 2. Tee kysely, joka listaa kunkin maanosan, ja niissä sijaitsevien maiden määrän.

`select continent, count(*) from country group by continent;`

![](kuvat/viikko4/koostetieto/2.png)

### 3. Tulosta pelaajien nimimerkit ja pelaajien saavuttamien säätilatavoitteiden lukumäärät.

`select game.screen_name, count(*) from game, goal_reached where game.id = goal_reached.game_id group by screen_name;`

![](kuvat/viikko4/koostetieto/3.png)

### 4. Mikä nimimerkki on kuluttanut vähiten hiilijalanjälkeä?

`select screen_name from game where co2_consumed in (select min(co2_consumed) from game);`

![](kuvat/viikko4/koostetieto/4.png)

### 5. Tulosta maan nimi ja lentokenttien lukumäärä kyseisessä maassa. Järjestä tulokset siten, että ylimpänä listassa ovat maat, joissa on eniten lentokenttiä. Ota mukaan vain 50 eniten lentokenttiä sisältävää maata.

`select country.name, count(*) from country, airport where airport.iso_country = country.iso_country group by country.name order by count(*) desc limit 50;`

![](kuvat/viikko4/koostetieto/5.png)

### 6. Tulosta niiden maiden nimi, joissa on yli 1000 lentokenttää.

`select country.name from country, airport where airport.iso_country = country.iso_country group by airport.iso_country having count(*) > 1000;`

![](kuvat/viikko4/koostetieto/6.png)

### 7. Minkä niminen on maailman korkeimmalla sijaitseva lentokenttä?

`select name from airport where elevation_ft in (select max(elevation_ft) from airport);`

![](kuvat/viikko4/koostetieto/7.png)

### 8. Missä maassa sijaitsee maailman korkeimmalla oleva lentokenttä?

`select country.name from country where country.iso_country in (select iso_country from airport where elevation_ft in (select max(elevation_ft) from airport));`

![](kuvat/viikko4/koostetieto/8.png)

### 9. Kuinka monta säätilatavoitetta Vesa on saavuttanut?

`select count(*) from goal_reached where game_id in (select id from game where screen_name = "Vesa");`

![](kuvat/viikko4/koostetieto/9.png)

### 10. Mikä on lähimpänä napa-alueita olevan lentokentän nimi?

`select name from airport where latitude_deg in (select min(latitude_deg) from airport);`

![](kuvat/viikko4/koostetieto/10.png)

## Päivityskyselyharjoitukset

### 1. Vesa lentää nykyiseltä sijainnilta Nottingham Airport:lle. Samalla Vesan hiilijalanjälki kasvaa 500:lla. Päivitä nämä tiedot tietokantaan.

`update game set location = (select ident from airport where name = "Nottingham Airport"), co2_consumed = co2_consumed + 500 where screen_name = "Vesa";`

![](kuvat/viikko4/update/1.png)

### 2. Ja nyt alustetaan oma tietokanta valmiiksi projektin kannalta. Eli poistetaan kaikki pelin tilaan liittyvä testidata. Viite-eheyden takia pystyt poistamaan datan vain fiksussa järjestyksessä. Täytyykö sinun poistaa ensin data game-taulusta vai goal_reached taulusta?

Vastaus: goal_reached

![](kuvat/viikko4/update/2.png)

### 3. Poista data goal_reahed-taulusta

`delete from goal_reached;`

![](kuvat/viikko4/update/3.png)

### 4. Poista data game-taulusta

`delete from game;`

![](kuvat/viikko4/update/4.png)
