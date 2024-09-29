# Viikko 2

## Yhteen tauluun kohdistuvien kyselyjen harjoitukset

### 1. Tee kysely, joka tulostaa kaikki sarakkeet goal-taulusta:

`select * from goal;`

![](kuvat/viikko2/yksi-taulu/1.png)

### 2. Tee kysely, joka tulostaa nimen ja tyypin kaikista Suomessa sijaitsevista lentokentistä:

`select name, type from airport where iso_country = "FI";`

![](kuvat/viikko2/yksi-taulu/2.png)

### 3. Tee kysely, joka tulostaa suomalaisten lentokenttien nimet aakkosjärjestyksessä:

`select name from airport where iso_country = "FI" order by name;`

![](kuvat/viikko2/yksi-taulu/3.png)

### 4. Tee kysely, joka tulostaa nimen ja tyypin kaikista Suomessa sijaitsevista lentokentistä. Järjestä tulos ensisijaisesti tyypin mukaan ja toissijaisesti nimen mukaan:

`select name, type from airport where iso_country = "FI" order by type, name`

![](kuvat/viikko2/yksi-taulu/4.png)

### 5. Tee kysely, joka tulostaa kaikki F-kirjaimella alkavat maan nimet country-taulusta:

`select name from country where name like "F%"`

![](kuvat/viikko2/yksi-taulu/5.png)

### 6. Tee kysely, joka tulostaa kaikki country-taulun maiden nimet, joissa esiintyy F-kirjain:

`select name from country where name like "%f%"`

![](kuvat/viikko2/yksi-taulu/6.png)

### 7. Missä locationissa Vesa sijaitsee?

`select location from game where screen_name = "Vesa";`

![](kuvat/viikko2/yksi-taulu/7.png)

### 8. Kuinka paljon Ilkka on kuluttanut CO2 budjettia?

`select co2_consumed from game where screen_name = "Ilkka";`

![](kuvat/viikko2/yksi-taulu/8.png)

### 9. Kuinka paljon alkuperäinen CO2 budjetti on (tulosta CO2 budjetin arvo vain kerran)?

`select distinct co2_budget from game;`

![](kuvat/viikko2/yksi-taulu/9.png)

## Where-osan liitosehto harjoitukset

### 1. Tee kysely, joka listaa maan nimen ja lentokentän nimen. Valitse maaksi Islanti ja anna country-taulun name-kentälle alias ”country name” ja airport taulun name-kentälle alias ”airport name”.

`select country.name as "country name", airport.name as "airport name" from airport, country where country.iso_country = airport.iso_country and country.name = "Iceland";`

![](kuvat/viikko2/where/1.png)

### 2. Listaa Ranskan isojen lentokenttien nimet. Anna kentän nimelle alias "airport name":

`select name as "airport name" from airport where iso_country = "FR" and type = "large_airport";`

![](kuvat/viikko2/where/2.png)

### 3. Tee kysely, joka listaa kaikki Antarktiksella sijaitsevien lentokenttien nimet ja vastaava maan nimi. Käytä aliaksia country_name ja airport_name.

`select country.name as "country name", airport.name "airport name" from country, airport where country.iso_country = airport.iso_country and airport.continent = "AN";`

![](kuvat/viikko2/where/3.png)

### 4. Kuinka korkealla Heini on paraikaa merenpinnasta mitattuna?

`select elevation_ft from airport, game where airport.ident = game.location and game.screen_name = "Heini";`

![](kuvat/viikko2/where/4.png)

### 5. Kuinka korkealla Heini on paraikaa merenpinnasta mitattuna? Anna tulos metreissä, ja anna tulokselle alias elevation_m.

`select elevation_ft*0.3048 as elevation_m from airport, game where airport.ident = game.location and game.screen_name = "Heini";`

![](kuvat/viikko2/where/5.png)

### 6. Minkä nimisellä lentokentällä Ilkka on?

`select airport.name from airport, game where airport.ident = game.location and game.screen_name = "Ilkka";`

![](kuvat/viikko2/where/6.png)

### 7. Minkä nimisessä maassa Ilkka on?

`select country.name from airport, country, game where country.iso_country = airport.iso_country and airport.ident = game.location and game.screen_name = "Ilkka";`

![](kuvat/viikko2/where/7.png)

### 8. Minkä nimiset säätila-tavoitteet Heini on saavuttanut?

`select goal.name from goal_reached, goal, game where goal_reached.goal_id = goal.id and goal_reached.game_id = game.id and game.screen_name = "Heini";`

![](kuvat/viikko2/where/8.png)

### 9. Minkä nimisellä lentokentällä Ilkka saavutti säätilan clouds?

`select airport.name from airport, game, goal, goal_reached where game.location = airport.ident and game.id = goal_reached.game_id and goal_reached.goal_id = goal.id and goal.name = "CLOUDS" and game.screen_name = "Ilkka";`

![](kuvat/viikko2/where/9.png)

### 10. Minkä nimisessä maassa Ilkka saavutti säätilan clouds?

`select country.name from country, airport, game, goal, goal_reached where country.iso_country = airport.iso_country and game.location = airport.ident and goal_reached.game_id = game.id and goal_reached.goal_id = goal.id and goal.name = "CLOUDS" and game.screen_name = "Ilkka";`

![](kuvat/viikko2/where/10.png)