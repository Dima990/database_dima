# database_dima

## Сдлать дома

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


### vy

```sql
begin;

create table students (
	id serial,
	name varchar(100) not null,
	surname varchar(100) not null,
	score numeric(2,2),
	date_br date not null,
	n_group numeric(4,0) not null,
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

*hghg*

**jjhj**

***jij***
