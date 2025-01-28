# sql-practice
SQL PRACTICE
-- database creation
create database cricket; -- selecting the database
use cricket; -- table creation
create table cricket_players(player_id int primary key , player_name varchar(20), jersy_no int, country varchar(20), Dob date, role varchar(20), batting_style varchar(20), bowling_style varchar(20), matches_played int default 0, runs_scored int default 0, wickets_taken int default 0); -- DROP COMMAND
drop table cricket_players; -- inserting data into the table
insert into cricket_players(player_id,player_name,jersy_no, country,dob,role,batting_style,bowling_style,matches_played, runs_scored,wickets_taken) values
(1,'virat kohli',18,'india','1988-11-05','batsman','right hand bat','-',437,24350,4), (2,'Sachin Tendulkar',10,'india','1973-04-24','batsman','right hand bat','-',664,34357,3), (3,'Brian Lara',3,'West Indies','1969-05-02','Batsman','Left-hand bat','-',430,22358,1), (4,'Shane Warne',5,'Australia','1969-09-13','Bowler','Right-hand bat','Right-arm leg
spin',339,3154,1001), (5,'AB de Villiers',11,'South Africa','1984-02-17','Batsman','Right-hand
bat','Wicketkeeper',420,20014,2); -- ALTER COMMAND
alter table cricket_players add age int;
alter table cricket_players modify age float;
alter table cricket_players rename column age to gender;
alter table cricket_players rename to cricket_player;
alter table cricket_player rename to cricket_players;
alter table cricket_players drop column age;
alter table cricket_players drop column gender; -- TRUNCATE COMMAND
truncate table cricket_players; -- SELECT COMMAND
select * from cricket_players; -- UPDATE STATEMENT
update ipl_team set team_name='KKR',capitan='shreyas ayer' where player_id=3;
update cricket_players set dob='1998-09-12',wickets_taken=20 where player_id=11;
update cricket_players set jersy_no=15 where player_id=8; -- DELETE COMMAND
delete from cricket_players where player_id=11;
rollback; -- COMMIT COMMAND
insert into cricket_players(player_id,player_name,jersy_no, country,dob,role,batting_style,bowling_style,matches_played, runs_scored,wickets_taken) values
(11,'rohith sharma',45,'india','1995-04-22','batting','rigth hand bat','-',390,3645,0), (12,'jos buttler',13,'england','1993-06-27','batting','left hand bat','-',450,4532,0), (13,'trend bolt',37,'newzland','1994-02-23','bowling','-','left arm fast',430,0,1050);
commit; -- DISTINCT keyword
select distinct country from cricket_players; -- WHERE clause
select * from cricket_players where country='india'; -- ORDER BY clause
select player_name,dob from cricket_players order by dob; -- logical operation
-- AND
-- OR
-- NOT
select * from cricket_players where runs_scored>=3000 and runs_scored<=20000;
select * from cricket_players where runs_scored>=3000 or runs_scored<=20000;
select * from cricket_players where not runs_scored>=3500;
insert into cricket_players(player_id,player_name,jersy_no, country,dob,role,batting_style,bowling_style,matches_played, runs_scored,wickets_taken) values
(6,'jadeja',8,'india','1982-05-23','bowler','left hand bat','left arm spinner',98,2000,100), (7,'kl rahul',21,'india','1900-02-27','batsman','rigth hand bat','-',78,4500,0), (8,'chris gayel',10,'west indies','1975-04-02','batsman','rigth hand bat','rigth arm
spin',300,7000,20), (9,'david warner',35,'Australia','1984-09-12','batsman','rigth hand bat','-',250,4500,0), (10,'kn williamson',12,'newzland','1979-04-25','batsman','left hand bat','-',260,5000,0); -- IN operator -- NOT IN operator
select * from cricket_players where player_id in (1,4,8) order by dob; -- between operator
select * from cricket_players where runs_scored between 3000 and 5000; -- LIKE operator
select * from cricket_players where batting_style like '%left%';
select * from cricket_players where batting_style like 'left%';
select * from cricket_players where batting_style like '%left';
select * from cricket_players where player_name like '%i';
select * from cricket_players where player_name like '__a%'; -- REGEXP operator
-- ^ begining of string
select * from cricket_players where bowling_style regexp '^right'; -- $ ending of string
select * from cricket_players where bowling_style regexp 'spin$';
-- | logical or
select * from cricket_players where player_name regexp "^s|^a"; -- [abc]
select * from cricket_players where player_name regexp '^[a,c,f]';
select * from cricket_players where player_name not regexp '^[a,c,f]'; -- [a-z] range
select * from cricket_players where player_name regexp '^[b-f]';
select * from cricket_players where player_name regexp '^[b-f]|i$';
select * from cricket_players where batting_style regexp 'left'; -- LIMIT clause
select * from cricket_players limit 3; -- IPL team players table
create table ipl_team(player_id int auto_increment, team_name varchar(20),capitan varchar(20), unique(player_id));
insert into ipl_team(team_name,capitan)values
('RCB','faf duplesis'), ('mumbai indians','rohith'), ('LSG','kl rahul'), ('CSK','dhoni'), ('RCB','faf duplesis'), ('CSK','dhoni'), ('LSG','kl rahul'), ('RCB','faf duplesis'), ('Srh','pat commins'), ('SRH','pat commins');
select * from ipl_team; -- JOINS CONCEPT
-- INNER JOIN
select i.player_id,c.player_name,team_name from ipl_team i join cricket_players c on
i.player_id=c.player_id;
select * from ipl_team i join cricket_players c on i.player_id=c.player_id; -- LEFT JOIN
select * from ipl_team i left join cricket_players c on c.player_id=i.player_id;
-- RIGHT JOIN
select * from cricket_players c right join ipl_team i on c.player_id=i.player_id; -- SELF JOIN
select o.player_id,o.player_name,t.jersy_no from cricket_players o,cricket_players t
where o.player_id=t.jersy_no; -- BUILT-IN FUNCTIONS
-- > STRING FUNCTIONS
-- > NUMERIC FUNCTIONS
-- > AGGREGATE FUNCTIONS
-- > DATE AND TIME FUNCTIONS
-- STRING FUNCTIONS
-- >UPPER() FUNCTION
select upper(player_name) from cricket_players; -- >LOWER() FUNCTION
select lower(player_name) from cricket_players; -- >LENGTH() FUNCTION
select length(player_name) from cricket_players; -- >INSTR() FUNCTION
select instr(player_name,'k') from cricket_players; -- > SUBSTR() FUNCTION
select substr(player_name,1,6) from cricket_players; -- >CONCAT() FUNCTION
select concat(player_name,' ',jersy_no) from cricket_players; -- >TRIM() FUNCTION
select trim(' virat kohli ') as player_name from cricket_players; -- VIEWS CONCEPT
create view view1
as
select player_id,player_name,jersy_no from cricket_players;
select * from view1;
create view view2
as
select c.player_id,player_name,jersy_no,team_name from cricket_players c,ipl_team;
select * from view2;
delete from view1 where player_id=13;
NORMALIZATIONS
Definition : It a process of designing a database efficiently such we avoid
data redundancy intern it will help to avoid anomilies such that
insertion,deletion and updation anomalies. there are 6 normalforms in normalization
1 . 1NF:
rules:
1 . Every column/attribute need to have single value. 2 . Each row should be unique.Either through single or multiple columns.Not
mandatory to have primary key. 2 . 2NF:
1.Must be in 1NF. 2. All no- key attributes must be fully dependent on candidate key.
i.e if non-key column is partially dependent on candidate key(subset of
columns forming candidate key)then split them into separate columns. 3.Every table should have primary key and relationship between the tables
should be formed using foreign key. 3 . 3NF:
1 . Must be in 2NF
2 . Avoid transitive dependencies.
