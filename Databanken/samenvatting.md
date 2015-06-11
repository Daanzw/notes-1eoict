#  Overzicht commando's

Door: Hanne Goossens

```sql
create table (...) engine='';	# tabel aanmaken
drop table ...;		# tabel verwijderen
unsigned;			# enkel positieve getallen
zerofill;			# voorloopnullen toevoegen
float;				# reeële getallen waarvoor grote precisie niet nodig is
double(m,d);		# m: aantal digits; d: aantal na de komma
decimal(m,d);		# idem, gebruik voor geld
char(n);			# korte string met lengte n
varchar(n);			# idem, max 255 chars
text/blob;			# langere string, text is niet hoofdlettergevoelig
date,time,datetime;	# YY-MM-DD; HH:MM:SS; YYYY-MM-DD; HH:MM:SS
# zet tussen aanhalingstekens
year;				# YYYY
now();				# nu
timestamp;			# wordt automatisch aangepast aan huidige tijd, YYYYMMDDHHMMSS
unix-timestamp;		# epochtijd in s
enum('bla','bla');	# verzameling van strings in hoofdletters
is null/ is not null;	# niet '=' of 'like' gebruiken voor null
auto_increment;		# automatisch +1 in combinatie met not null, pk, unique
alter tabelnaam add kolomnaam;	# kolom toevoegen
alter tabelnaam change kolomnaam;	# verander kolomdefinitie
alter tabelnaam rename to nieuweTabelnaam;	# verander tabelnaam
alter tabelnaam drop kolomnaam;	# drop een bepaalde kolom
insert into tabelnaam values(...);	#nieuwe records toevoegen aan een tabel (in volgorde van de kolommen)
update tabelnaam set ... = ...;		# verander een bepaalde waarde
delete from tabelnaam where ...;	# verwijder bepaalde records
# tip: test deze eerst met select
select kolomnaam from tabelnaam		# data opvragen
	where ... = ...
	where ... > ...
	where ... < ...
	where ... like '...%'
	where ... between ... and ...
	where ... in (...,...,...)
	order by kolomnaan
	desc
	limit a b 			# a is de limit; b de offset
```

# Niveaupeiling

```sql
SELECT brandstof, COUNT(*) FROM autos INNER JOIN autoinfo ON autos.autoinfo_id=autoinfo.id GROUP BY brandstof ORDER BY Count(*) DESC LIMIT 1;

SELECT COUNT(DISTINCT(autoinfo.bouwjaar)) AS aantal, verkopers.naam FROM verkopers INNER JOIN autos ON verkopers.id=autos.verkopers_id INNER JOIN autoinfo ON autoinfo.id=autos.autoinfo_id WHERE verkopers.naam='Katja';

SELECT autos.chassisNR, autoinfo.basisprijs+SUM(opties.prijs) AS verkoopprijs FROM opties INNER JOIN autos_has_opties ON autos_has_opties.opties_id=opties.id INNER JOIN autos ON autos.chassisNR=autos_has_opties.autos_chassisNR INNER JOIN autoinfo ON autoinfo.id=autos.autoinfo_id GROUP BY autos.chassisNR;
```
