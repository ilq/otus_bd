
```SQL
CREATE DATABASE contasters;
CREATE SCHEMA IF NOT EXISTS users;
CREATE SCHEMA IF NOT EXISTS contasters;
CREATE SCHEMA IF NOT EXISTS films;
CREATE tablespace tspace_films LOCATION '/var/lib/postgresql/tspace_films';
CREATE ROLE contasters with LOGIN PASSWORD 'GUGfhjkm';

```
```SQL
CREATE TABLE users.User
(
 user_id BIGSERIAL PRIMARY KEY,
 username varachar UNIQUE,
 password varchar
)

CREATE TABLE users.Profile 
(
 profile_id BIGSERIAL PRIMARY KEY,
 user_id bigint REFERENCES users.User ON DELETE CASCADE,
 role varchar
)

CREATE TABLE contasters.Score 
(
 score_id BIGSERIAL PRIMARY KEY,
 score int
 user_id bigint REFERENCES users.User ON DELETE CASCADE,
 film_id bigint REFERENCES films.Film ON DELETE CASCADE,
)

CREATE TABLE contasters.Wishlist
(
 wish_list_id SERIAL PRIMARY KEY, 
 add_date date,
 user_id bigint REFERENCES users.User ON DELETE CASCADE,
 film_id bigint REFERENCES films.Film ON DELETE CASCADE,
)

CREATE TABLE contasters.Contaste
(
 contaste_id BIGSERIAL PRIMARY KEY,
 "percent" smallint NOT NULL,
 genre_id int REFERENCES films.Genre,
 user_id int REFERENCES users.User (user_id) ON DELETE CASCADE,
 user_id_1 int REFERENCES users.User (user_id) ON DELETE CASCADE
);

CREATE TABLE films.Film
(
 film_id BIGSERIAL PRIMARY KEY,
 name vacrchar NOT NULL,
 year smallint NOT NULL,
 cover varchar
) TABLESPACE tspace_films;

CREATE TABLE fllms.Genre
(
 genre_id SERIAL PRIMARY KEY,
 name vacrchar NOT NULL
) TABLESPACE tspace_films;

CREATE TABLE films.film_genre (
  film_id    bigint REFERENCES films.Film ON DELETE CASCADE,
  genre_id   int REFERENCES films.Genre ON DELETE RESTRICT,
  CONSTRAINT film_genre_pkey PRIMARY KEY (film_id, genre_id)
);

CREATE TABLE films.IMDB 
(
 imdb_id BIGSERIAL PRIMARY KEY,
 film_id bigint REFERENCES films.Film ON DELETE CASCADE,
 rating decimal NOT NULL,
 url varchar NOT NULL
) TABLESPACE tspace_films;

CREATE TABLE films.Kinoposk
(
 kinopoisk_id BIGSERIAL PRIMARY KEY,
 film_id int REFERENCES films.Film ON DELETE CASCADE,
 rating decimal NOT NULL,
 url varchar NOT NULL
) TABLESPACE tspace_films;
```
```SQL
CREATE INDEX ON films.Film (upper(name));
CREATE INDEX ON contasters.Contaste (percent);
CREATE INDEX ON films.Film (year);
```