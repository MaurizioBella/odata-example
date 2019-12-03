##  OData test URLs

This following table contains test URLs that can be used with the Olingo V2 demo project.

| URL                                      | Description                                     |
|------------------------------------------|-------------------------------------------------|
| `http://localhost:8080/odata/$metadata`  | fetch OData metadata document |
| `http://localhost:8080/odata/CarMakers?$top=10&$skip=10` | Get 10 entities starting at offset 10 |
| `http://localhost:8080/odata/CarMakers?$count` | Return total count of entities in this set |
| `http://localhost:8080/odata/CarMakers?$filter=startswith(Name,'B')` | Return entities where the *Name* property starts with 'B' |
| `http://localhost:8080/odata/CarModels?$filter=Year eq 2008 and CarMakerDetails/Name eq 'BWM'` | Return *CarModel* entities where the *Name* property of its maker  starts with 'B' |
| `http://localhost:8080/odata/CarModels(1L)?$expand=CarMakerDetails` | Return the *CarModel* with primary key '1', along with its maker|
| `http://localhost:8080/odata/CarModels(1L)?$select=Name,Sku` | Return the *CarModel* with primary key '1', returing only its *Name* and *Sku* properties |
| `http://localhost:8080/odata/CarModels?$orderBy=Name asc,Sku desc` | Return *CarModel* entities, ordered by the their *Name* and *Sku* properties |
| `http://localhost:8080/odata/CarModels?$format=json` | Return *CarModel* entities, using a JSON representation|


Code retrieved from https://github.com/eugenp/tutorials/tree/master/apache-olingo



-- Drop table

-- DROP TABLE public.car_model;

CREATE TABLE public.car_model (
	id int8 NOT NULL,
	"name" varchar(255) NULL,
	sku varchar(255) NULL,
	"year" int4 NULL,
	maker_fk int8 NOT NULL,
	CONSTRAINT car_model_pkey null,
	CONSTRAINT fkoo0ednvdaf7o678krlkvoclej null
);

-- Permissions

ALTER TABLE public.car_model OWNER TO XXXXXX;
GRANT ALL ON TABLE public.car_model TO XXXXXX;


-- Drop table

-- DROP TABLE public.car_maker;

CREATE TABLE public.car_maker (
	id bigserial NOT NULL,
	"name" varchar(255) NULL,
	CONSTRAINT car_maker_pkey null
);

-- Permissions

ALTER TABLE public.car_maker OWNER TO XXXXXX;
GRANT ALL ON TABLE public.car_maker TO XXXXXX;


DML

insert into car_maker(id,name) values (1,'Special Motors');
insert into car_maker(id,name) values (2,'BWM');
insert into car_maker(id,name) values (3,'Dolores');

insert into car_model(id,maker_fk,name,sku,year) values(1,1,'Muze','SM001',2018);
insert into car_model(id,maker_fk,name,sku,year) values(2,1,'Empada','SM002',2008);

insert into car_model(id,maker_fk,name,sku,year) values(4,2,'BWM-100','BWM100',2008);
insert into car_model(id,maker_fk,name,sku,year) values(5,2,'BWM-200','BWM200',2009);
insert into car_model(id,maker_fk,name,sku,year) values(6,2,'BWM-300','BWM300',2008);

alter sequence hibernate_sequence restart with 100;