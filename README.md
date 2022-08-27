# GH_Project_Portfolio
Title: Project Portfolio

Description: Formula One database that includes various entities and attributes including team name, driver names, schedule, standings (both constructors and drivers), tickets etc.

API Reference Table of endpoint paths, methods, parameters
Endpoint paths: DELETE, SHOW, GET_DRIVER, GET_ALL_DRIVERS, GET_TEAM, GET_ALL_TEAMS and UPDATE.

Methods: GET, DELETE, PUT/PATCH, POST

Retrospective answering of the following questions:
How did the project's design evolve over time?

I had to routinely alter what I wanted to show, as I am not knowledgeable enough to do everything I wanted to do. I would've loved to go deeper with certain queries and use alternate methods/HTTP requests, but thought it best to stick with what I came to know. 

Did you choose to use an ORM or raw SQL? Why?
I chose SQL over ORM, because this course doesn't allow for full understanding of learning the ORM model. The time to learn that in 2 weeks just isn't realistic. So I went with SQL.

What future improvements are in store, if any?
No future improvements.

Postgres database schema
Tables designs (column names, data types, constraints etc.)
CREATE TABLE Teams(
    id SERIAL primary key,
    team_name TEXT NOT NULL,
    team_points INT --default 0
);

CREATE TABLE Drivers(
    id SERIAL primary key,
    driver_name TEXT NOT NULL,
    driver_country TEXT NOT NULL,
--    driver_points INT default 0,
    team_id INT 
);

CREATE TABLE Standings(
    id SERIAL primary key,
    driver_points INT, --default 0,
    team_points INT, --default 0,
    driver_id INT,
    team_id INT
);

CREATE TABLE Schedule(
    id SERIAL primary key,
    track TEXT NOT NULL,
    date DATE NOT NULL,
    time TIME NOT NULL
);

CREATE TABLE Tickets(
    id SERIAL primary key,
    price float NOT NULL,
    date DATE NOT NULL,
    seat_number INT NOT NULL
);

CREATE TABLE Formula_One(
    id SERIAL primary key,
    driver_id INT,
    ticket_id INT,
    team_id INT,
    schedule_id INT,
    standing_id INT,
    post_id INT
);

CREATE TABLE Posts(
    id SERIAL primary key,
    content TEXT,
    likes INT,
    views INT
);

ALTER TABLE Drivers add constraint fk_team_id foreign key(team_id) references Teams ON DELETE CASCADE;
ALTER TABLE Formula_One add constraint fk_team_id foreign key(team_id) references Teams ON DELETE CASCADE;
ALTER TABLE Formula_One add constraint fk_ticket_id foreign key(ticket_id) references Tickets ON DELETE CASCADE;
ALTER TABLE Formula_One add constraint fk_driver_id foreign key(driver_id) references Drivers ON DELETE CASCADE;
ALTER TABLE Formula_One add constraint fk_standing_id foreign key(standing_id) references Standings ON DELETE CASCADE;
ALTER TABLE Formula_One add constraint fk_schedule_id foreign key(schedule_id) references Schedule ON DELETE CASCADE;
ALTER TABLE Standings add constraint fk_standings_driver_id foreign key(driver_id) references Drivers ON DELETE CASCADE;
ALTER TABLE Standings add constraint fk_standings_team_id foreign key(team_id) references Teams ON DELETE CASCADE;
ALTER TABLE Formula_One add constraint fk_post_id foreign key(post_id) references Posts ON DELETE CASCADE;

1-1 exmple: Driver to Country
1-many example: Formula One to Standings
many-many example: Schedule and Date
