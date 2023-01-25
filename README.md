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

***jij***
