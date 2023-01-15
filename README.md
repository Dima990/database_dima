# database_dima

- test
- lol
- bvfghc

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
