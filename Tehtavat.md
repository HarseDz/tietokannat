### Yhteen tauluun kohdistuvien kyselyiden harjoitukset
# 1
select * from goal;
![image](https://github.com/user-attachments/assets/bf561f0c-26f9-4e16-86d2-7d0e5f62dedb)

# 2
select name from airport where iso_country like "%FI%";
![image](https://github.com/user-attachments/assets/6a96ead4-dbe5-49fa-837f-85681c3c79cc)

# 3
select name from airport where iso_country like "%FI%" order by name;
![image](https://github.com/user-attachments/assets/e38ed9a4-44ea-4d64-8088-94984f0ee08c)

# 4
select name, type from airport where iso_country like "%FI%"
order by type asc, name asc;
![image](https://github.com/user-attachments/assets/5ef4960d-e9e6-4543-9486-df6230b6a2ef)

# 5
select name from country where name like "F%"
![image](https://github.com/user-attachments/assets/704109a3-94f0-476f-8a3a-b6312eb7079d)

# 6
select name from country where name like "%F%"
![image](https://github.com/user-attachments/assets/0cdcf921-b05d-4945-9d04-b3dc01b2a64b)

# 7
select location from game where screen_name="Vesa";
![image](https://github.com/user-attachments/assets/47d20611-851d-4f1e-9d67-b57ab858e982)

# 8
select co2_consumed from game where screen_name = "Ilkka";
![image](https://github.com/user-attachments/assets/fd844c1c-d800-4ec3-ae30-aeadd1090512)

# 9
select co2_budget from game where screen_name = "Ilkka";
![image](https://github.com/user-attachments/assets/e19619ad-f159-4bb3-a15d-17356e262d82)

### Where-osan liitosehto harjoitukset

# 1
select country.name as "country name", airport.name as "airport name"
from airport, country
where airport.iso_country = country.iso_country and country.name="Iceland";
![image](https://github.com/user-attachments/assets/ab63cc08-62f5-48d4-b30f-1997f511630e)

# 2
select airport.name as "airport name"
from airport, country
where airport.iso_country = country.iso_country and country.name="France" and airport.type ="large_airport";
![image](https://github.com/user-attachments/assets/17c582fd-0781-4a4e-b432-5422ce4e4c55)

# 3
select country.name as country_name, airport.name as airport_name
from airport, country
where airport.iso_country = country.iso_country and country.continent="AN";
![image](https://github.com/user-attachments/assets/bda334fa-d855-4776-904b-e69e7d608e2d)

# 4
select elevation_ft
from airport, game
where location=ident and screen_name = "Heini";
![image](https://github.com/user-attachments/assets/0ca213cf-10cd-4e7f-8906-a94a1528404c)

# 5
select elevation_ft * 0.3048 as elevation_m
from airport, game where location=ident and screen_name="Heini";
![image](https://github.com/user-attachments/assets/ac32be4d-3ced-4ce5-83df-e4c2ea6f7197)

# 6
select name from airport, game where location = ident and screen_name = "Ilkka";
![image](https://github.com/user-attachments/assets/7bfe2aed-db3e-438b-9245-8797fba0569b)

# 7
select country.name from airport,country, game where location = ident and airport.iso_country=country.iso_country and screen_name = "Ilkka";
![image](https://github.com/user-attachments/assets/4cacffa0-bcde-40fa-ba4a-dac158bbc9c1)

# 8
select name from goal,goal_reached, game where game.id = game_id
and goal.id=goal_id and screen_name = "Heini";
![image](https://github.com/user-attachments/assets/c39076e1-6f77-49be-af79-7e346664e48f)

# 9
select airport.name
from airport, game, goal, goal_reached
where ident = location and game.id = game_id 
and goal.id = goal_id and screen_name = "Ilkka" 
and goal.name = "CLOUDS";
![image](https://github.com/user-attachments/assets/ccaacc21-4815-4c09-8005-a2fefce4e1ee)

# 10
select country.name
from country,airport,game, goal, goal_reached
where airport.iso_country=country.iso_country and ident = location and game.id = game_id and goal.id = goal_id and screen_name = "Ilkka" and goal.name = "CLOUDS";
![image](https://github.com/user-attachments/assets/8a890d5e-b910-4e6e-8c91-c40629e6e209)

### Join harjoitukset

# 1
select country.name as "country name", airport.name as "airport name" from country inner join airport
on airport.iso_country=country.iso_country where country.name="Finland"and scheduled_service="yes"
![image](https://github.com/user-attachments/assets/aed61123-f316-43dc-8568-3168965df3a1)

# 2
select screen_name, airport.name from game inner join airport on location=ident;
![image](https://github.com/user-attachments/assets/55396fc4-572c-4527-b7dc-20aff82a31fb)

# 3
select screen_name, country.name from game inner join airport on location=ident inner join country on airport.iso_country = country.iso_country;
![image](https://github.com/user-attachments/assets/8d995ba5-5cd6-4324-b820-6e812dc644ad)

# 4
select airport.name, screen_name
from airport left join game on ident = location where name like "%Hels%";
![image](https://github.com/user-attachments/assets/9d17a688-ea04-4540-99ed-af901248acd9)

# 5
select name, screen_name
from goal left join goal_reached on goal.id = 
goal_id  left join game on game.id = game_id;
![image](https://github.com/user-attachments/assets/5f37c19a-5ba8-45b6-83a1-e5622de0c462)

### Sisäkysely harjoitukset

# 1
select name
from country
where iso_country in(
select iso_country
from airport
where name like "Satsuma%"
);
![image](https://github.com/user-attachments/assets/137e6bfc-247e-4fa4-865d-13799f0a15ef)


# 2
select name
from airport where
iso_country in(
select iso_country
from country
where name = "Monaco"
);
![image](https://github.com/user-attachments/assets/7f52ea19-c6b0-40f3-9264-158d1ed448b2)

# 3
select screen_name
from game
where id in (
select game_id
from goal_reached
where goal_id in(
select id
from goal
where name = "CLOUDS"));
![image](https://github.com/user-attachments/assets/8016f4c7-fa87-494f-b61b-6f68ae4b8246)

# 4
	
select country.name
from country
where iso_country not in
(select airport.iso_country
from airport);
![image](https://github.com/user-attachments/assets/b6de91e8-9944-4ec1-8251-9c7d06cb5e6b)

# 5
select name
from goal
where id not in(
select goal.id
from goal, goal_reached, game
where game.id = game_id and goal.id = goal_id and screen_name = "Heini"
);
![image](https://github.com/user-attachments/assets/7c23f0a2-bae7-4a92-92e1-a7b2e2cf45dc)







### Koostetieto kyselyt harjoitukset
# 1
select max(elevation_ft)
from airport;
![image](https://github.com/user-attachments/assets/16b02bd1-de51-42fd-8fbc-ea1253b07049)

# 2
select continent, count(*)
from country
group by continent;
![image](https://github.com/user-attachments/assets/a25b4192-fa14-48aa-861a-1437ebd03967)

# 3
select screen_name, count(*)
from game, goal_reached
where id = game_id
group by screen_name;
![image](https://github.com/user-attachments/assets/c7b96e4c-107e-47ab-bc11-c9b202e69a78)

# 4
select screen_name
from game
where co2_consumed in(
select min(co2_consumed)
from game
);
![image](https://github.com/user-attachments/assets/15ec1ad5-33b1-4777-b810-0b6e12c18b7b)

# 5
select country.name, count(*)
from airport, country
where airport.iso_country = country.iso_country group 
by country.iso_country
order by count(*) desc
limit 50;
![image](https://github.com/user-attachments/assets/cc57a28b-e923-4155-9730-747774dfb918)

# 6
select country.name from airport, country
where airport.iso_country = country.iso_country
group by country.iso_country having count(*)>1000;
![image](https://github.com/user-attachments/assets/d180092c-6fed-4eb3-a217-d973d57afdcd)

# 7
select name from airport where elevation_ft in (select max(elevation_ft) from airport)
![image](https://github.com/user-attachments/assets/51c42a1e-c885-4b85-9d96-76b3ee274794)

# 8
select name
from country
where iso_country in (
select iso_country
from airport
where elevation_ft in(
select max(elevation_ft)
from airport
)
);
![image](https://github.com/user-attachments/assets/00c5e697-e0f2-4f52-b7ad-f869ee22940f)

# 9
select count(*)
from game, goal_reached
where id = game_id and screen_name = "Vesa"
group by screen_name
![image](https://github.com/user-attachments/assets/a70049af-6a68-4690-8d51-6df43884b808)

# 10
select name
from airport
where latitude_deg in(
select min(latitude_deg)
from airport
);
![image](https://github.com/user-attachments/assets/190f4e51-bef4-49fe-b5a8-73aafd3c424c)


### Päivityskyselyt harjoitukset

# 1

update game
set  location = (select ident from airport where name = "Nottingham Airport"), co2_consumed = co2_consumed+500
where screen_name = "Vesa";

select * from game;
![image](https://github.com/user-attachments/assets/666dcadb-7810-4e58-9964-b853b0c3d513)

# 3
delete from goal_reached;
select * from goal_reached
![image](https://github.com/user-attachments/assets/16771b76-2545-4e39-a462-47817ef7f949)

# 4
delete from game;
select * from game
![image](https://github.com/user-attachments/assets/ba71a040-1a3f-4f15-b43c-a539d1220fc6)

### Tietokannan suunnittelun harjoitukset
