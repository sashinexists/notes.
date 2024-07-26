# 911 Doctor's Notes
[Link to ticket](https://dev.azure.com/allurepacificaesthetics/global/_sprints/taskboard/global%20Team/global/Sprint%2019?workitem=911)

## Scratch
- (2024/02/02 9:39午前)
- you want to make it so they load right away before you enter a new note
- the time isn't working any more
    - it looks like it loads wrong at the beginning and fixes on submit for some reason







- (2024/02/01 3:55午後)
- I need to make the doctors notes load sooner
- the time isn't working, it's all 1970s for some reason





### possibly old
- you want to add the ability for doctors to take notes on their patients
- there was a long process to even see the screen, think it through
- you need to make a change to the table (and therefore a migration)
    - for each patient a doctor can make multiple notes
- you want a posix timestamp, and one with the timezone
- okay
    - note_id(uuid)
    - doctor_id(uuid) fk references doctor.doctor_id
    - patient_id(uuid) fk references patient.patient_id
    - note_contents(text)
    - created(timestamp)
    

- You will have to add the following two to the migrations first
```sql
CREATE TABLE doctors_notes (
    note_id uuid primary key,
    doctor_id uuid not null,
    patient_id uuid not null,
    note_details jsonb not null,
    posix_time bigint default extract(epoch from current_timestamp)::bigint not null,
    timestamp_with_timezone timestamp with time zone default (current_timestamp AT TIME ZONE 'Australia/Sydney') not null
)
```


```sql

create table doctors_notes_event (
            doctors_notes_event_id bigserial primary key,
            note_id uuid not null,
            event_type text not null,
            event_data jsonb not null,
            created_at timestamp not null default current_timestamp
        );
```
