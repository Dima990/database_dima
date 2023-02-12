# database_dima

## Сдeлать дома

- https://github.com/RyabovNick/databasecourse_p1/tree/master/Theory/6_Functions#%D1%84%D1%83%D0%BD%D0%BA%D1%86%D0%B8%D0%B8
- https://www.postgresql.org/docs/12/functions-string.html
- https://github.com/RyabovNick/databasecourse_p1/tree/master/Tasks/2_Queries (однотабличные)

## hjhljh

1. gvk
2. bcnhj
3. ghj



dfghdhg | vfucfjg| hyuigty
-----|-----|-----
vghjk|hvghivi|nhigi
vfghm|jklnhkj|njbhk


## Students

```sql
begin;

create table students (
	id serial,
	name varchar(100) not null,
	surname varchar(100) not null,
	score numeric,
	date_br date not null,
	n_group numeric not null,
	location varchar(255), 
	constraint students_id_pk primary key (id)
);

-- create sequence students_seq;

alter table students 
add constraint students_score_check 
check(score>=2 and score<=5);

alter table students 
add constraint students_ngroupe_check 
check(n_group>=1000 and n_group<=9999);

commit;
```
## Hobby
```sql
CREATE TABLE IF NOT EXISTS public.hobby
(
    id integer NOT NULL DEFAULT nextval('hobby_id_seq'::regclass),
    name character varying(100) COLLATE pg_catalog."default" NOT NULL,
    risk numeric NOT NULL,
    CONSTRAINT hobby_pkey PRIMARY KEY (id),
    CONSTRAINT risk_hobby CHECK (risk >= 1::numeric AND risk <= 10::numeric)
)

TABLESPACE pg_default;

ALTER TABLE IF EXISTS public.hobby
    OWNER to postgres;
```
## hobby_students
```sql
CREATE TABLE IF NOT EXISTS public.hobby_students
(
    id integer NOT NULL DEFAULT nextval('hobby_students_id_seq'::regclass),
    id_hb integer NOT NULL,
    id_st integer NOT NULL,
    dt_start date NOT NULL,
    dt_finish date,
    CONSTRAINT hobby_students_pkey PRIMARY KEY (id),
    CONSTRAINT id_hobby_fk FOREIGN KEY (id_hb)
        REFERENCES public.hobby (id) MATCH SIMPLE
        ON UPDATE NO ACTION
        ON DELETE NO ACTION
)

TABLESPACE pg_default;

ALTER TABLE IF EXISTS public.hobby_students
    OWNER to postgres;
```
*hghg*

**jjhj**












***10***
```sql
select *
from
	(
	select left(st.n_group::varchar,1) course, count(st.id) hcount
	from students st
	Group by course
	) total,
	(
	select left(st.n_group::varchar,1) course, count(st_count_hb.stud) count_st
	from (
		select  st.id stud, count(id_hb) count_hb
		from students st, hobby_students hb_st
		where st.id = hb_st.id_st 
		Group by st.id
		Having count(id_hb)>1
		) st_count_hb, students st
	where st.id = st_count_hb.stud
	Group by course
	)  count_st_usl
		
where total.course = count_st_usl.course and total.hcount/2 <= count_st
```
***11***
```sql
select *
from
	(
	select n_group course, count(st.id) hcount
	from students st
	Group by course
	) total,
	(
	select n_group course, count(st_count_hb.stud) score_n
	from (
		select  st.id stud, score count_hb
		from students st, hobby_students hb_st
		where score>=4 
		Group by st.id
		) st_count_hb, students st
	where st.id = st_count_hb.stud
	Group by course
	)  count_st_usl
		
where total.course = count_st_usl.course and total.hcount/2.5 <= score_n
```
***12***
```sql
select aaa.n_group, count(n_group)
from (select st.name, hb.name, n_group
from hobby hb, hobby_students hb_st, students st
where st.id = hb_st.id_st and hb.id = hb_st.id_hb and dt_finish is null
group by st.name, hb.name, n_group) aaa
group by aaa.n_group
```

***13***
```sql
SELECT st.id, st.name, st.surname, st.date_br, left(st.n_group::varchar,1) course
FROM students st
WHERE st.score = 4
EXCEPT SELECT DISTINCT stb.id, stb.name, stb.surname, stb.date_br, left(stb.n_group::varchar,1) course
FROM hobby_students sh, students stb
WHERE stb.id = sh.id_st AND sh.dt_finish IS NULL
ORDER BY course, date_br
```

***14***
```sql
create OR REPLACE view student_v as
select st.name, st.surname, st.score, st.date_br, (now()::date - hb_st.dt_start)/365 years
from students st, hobby hb, hobby_students hb_st
where st.id = hb_st.id_st and hb.id = hb_st.id_hb and dt_finish is not null and (now()::date - hb_st.dt_start)/365 >=5
```

***15***
```sql
select hb.name, count(hb_st.id_st)
from hobby hb, students st, hobby_students hb_st
where hb.id = hb_st.id_hb and st.id = hb_st.id_st
group by hb.name
```

***16***
```sql
select hb.name, count(DISTINCT hb_st.id_st)
from hobby hb, students st, hobby_students hb_st
where hb.id = hb_st.id_hb and st.id = hb_st.id_st
group by hb.name
order by count desc
limit 1
```

***17***
```sql
select st.name, st.surname, st.score, st.date_br
from students st, hobby_students hb_st
where st.id = hb_st.id_st  and hb_st.id_hb =(select hb.id
											 from hobby hb, students st, hobby_students hb_st
											 where hb.id = hb_st.id_hb and st.id = hb_st.id_st
											 group by hb.id
											 order by  count(DISTINCT hb_st.id_st) desc
											 limit 1)
```

***18***
```sql
select hb.id, hb.risk
from hobby hb
order by risk desc
limit 3
```

***19***
```sql
select st.id , now()::date - hb_st.dt_start days
from students st, hobby hb, hobby_students hb_st
where st.id = hb_st.id_st and hb.id = hb_st.id_hb and dt_finish is not null 
order by days desc
limit 10
```

***20***
```sql
select *
from (select n_group
from students st, hobby hb, hobby_students hb_st
where st.id = hb_st.id_st and hb.id = hb_st.id_hb and dt_finish is not null 
order by now()::date - hb_st.dt_start desc
limit 10) gr
group by gr.n_group
```

***21***
```sql
create OR REPLACE view student_bal as
select st.name, st.surname
from students st
order by score
```

***22***
```sql
SELECT DISTINCT ON (1) LEFT(st.n_group::VARCHAR,1) cours, hb.id
FROM students st, hobby hb, hobby_students hb_st
where st.id = hb_st.id_st and hb.id = hb_st.id_hb 
GROUP BY LEFT(st.n_group::VARCHAR,1), hb.id
ORDER BY LEFT(st.n_group::VARCHAR,1), COUNT(hb.id) DESC
```