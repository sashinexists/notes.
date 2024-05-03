## (2024/05/03 10:10午前)
- drop the event sourcing stuff now and just let changes be made
    - it won't work very nicely on the mobile phone interface
-  okay you are going to need an api thing
- need to think about where to get the prescription_items_id
- you need to make an event too

## (2024/05/02 8:32午前)
- thinking about how to make it so that you can enter a point
- now you can think about how to handle this kind of feedback
    - only five from the IV category and only 6 cosmetics
- you will use the error
    - specifically an input error
- you probably want a boolean to check if there are input errors and hide add and add to favourites if that's the case
- every time a prescription item is added you want to do a count and reject it and add the error if applicable
- does it only go to 1.0
- you need to update the errors on edit or remove
- alright, you are now upto the doctors portal
- set up might need to happen twice...
    - actually!!!
- okay now you can test to see if everything works
- get existing products plugged in to this
- some kind of custom init thing
- seems to be working, find out where it gets the prescription items from and figure out a way to updated them
    - do you want a button that confirms the changes or not?
- you want to change the prescription items with the id in DoctorPortal
- going to want to set "prescription_item_lines"
    - on any change to the list basically, (edit, add, remove)
    - make a set_prescription_items_by_id in python and call it
- UP TO: Go to line 176 of `DoctorReviewPrescription.elm`

## (2024/05/01 9:38午前)
- okay now products aren't loading for some reason
- okay need to figure out how to get the product category from the product
- Justine's number, questions about the ticket 0409426955
- you need to fix the decimal points after you've worked on this error
- you need to make these error messages stop displaying when they are not neeeded and you full width
- also make them look nice



## (2024/04/26 8:23午前)
- yesterday was ANZAC day
    - need to know these public holidays in advance, it was a serendipitous day
- there was something that when it was empty it was requested
- okay it's not if the list it populated but if anything is there that isn't NoPrescriptionRequested
- make it only insert prescription items the first time, and update later
- make repeats default to 6 and capped at 6
    - bug fix then high priority
- this is super novel, I don't know anything about this bug
- products don't load after you select a new patient, you are branching off the branch `backup-21-aftermerge`
- 

### fixing bugs
- make it only insert once and after that update
    - first check what happens on insert, and see if you can tell if something is already inserted
        - it looks like the changes go into the PrescriptionState
    - have a look at what the default PrescrptionState.prescriptionItems are
        - okay it's Nothing
    - now you have to make an update route and have it access that route on subsequent times
    - should also check if there's any changes and only do it with changes
    - also make sure that there is at least one prescription item added in the view model


## (2024/04/24 8:06午前)
- restricting products
    - later, ask Ben about this
- bookmarks
- first up figure out how to get this out of hiding
    - that was moving the z-index of elm-ui higher
- you've also made the dropdowns smaller
- if this worked then you don't need the part there that inserts office messages
- how do I tell if the prescription has been requested?
- it's when it's empty, what it's been requested, come back to this and start again
- there was a kind of deep reason that I was sending a message early, it's because to submit in the first place you need a prescription id
- trying to insert prescription items
- need to figure out stuff with office prescriptions
    - right now the button does something else but you need to make it also request the prescription
- after this you should pull in Ben's changes
    - actually before this merge it in



## (2024/04/18 8:17午前)
- okay nothing is showing with the component, that's because it's a maybe
    - you have to make it so that when a nurse is selected it shows
- current problem is that it doesn't work if the nurse is not a part of any access group (chancey)
    - after that you have to push it through into the prescription state
- need to make it get all the products if the nurse isn't a part of any treatment access group
    - current plan is to go to the python itself and make it return every product
- thinking through this, you want to put stuff into the database
    - this can either happen on clicking next or adding an item
        - I feel that having it happen when adding an item would be better
        - at the moment they can only be inserted as a nurse or patient
- handle the the secret nurse, look at the existing thing
    - you want to think of a smart way to deal with the table that it is expecting
- going to do a pr 


- **Important** the back office prescriptions interface needs to be tested, does the doctor get the information?
- next up, doctor portal
- actually let's process Ben's comments
    - remove diff from shared (actually do this last)
    - get rid of the domain thing (done)
    - get rid of the update things in domain (done)
- okay thinking out loud, test to see if you can still it still works 
    - after that change the other thing
- I don't understand the checkprescriptionstate
- You are up to the doctor portal
    - you need to add the New SelectPrescriptionItems items to the doctorPortal, you left a nice comment

## (2024/04/17 9:08午前)
- currently working on getting this working for existing patients
    - maybe you should get this to a working state
- (10:18午前) okay, the state this ticket is in:
    - *you need to add a dropdown product selector!!!!*
- ProductsNew will be SelectPrescriptionItems
    - Doctor's screen
        - it's in DoctorPortal.elm, in the model, in the products field
    - Back Office Prescriptions
        - it's in OfficePrescriptions.elm, in the model, in the products field
        - admin user -> office prescriptions
    - Prescription form
        - found in PrescriptionForm.elm, ProductRouterModel type
        - ProductsWithAccess.elm if you choose a nurse that has a treatment access group
        - otherwise Products.elm
    - Send to patient form
- thinking carefully about this task, I will pull another folder with main-onion and set a different theme and see what happens
- so far it looks like when you fix Domain.productCategoryTable and decoder in it will work nicely
    - need to figure out how to get the server working here
        - lets do it all manually, it's probably a good thing
- right now I'm getting errors getting favourites
- okay, just now you were trying to get an sms and it wasn't working
    - okay tomorrow problem, fix shared with your email and everything
    - after that you need to sort out how the access works

## (2024/04/12 8:10午前)
- Date entry looks like it is working fine now
- just need to validate it
- Next up you need to implement functionality for returning patients
    - this means you want to, in the send patient from, allow the nurse to either create a new patient or send to an existing patient
- git pull in the create treatment ticket and merge into current one
- you need a list of patients somehow
    - after you sort out the patient dropdown, then make the tabs component super nice
- ask ben about getting a list of patients given a nurse
- you were able to get all the patients in a clinic in the model, now you have to make a dropdown component for them and put it in the tabs model
    - after that make the tabs look nice
    - after that change the send form to patient interface to handle everything (you made an EnterPatient variable)
    - after that make sure that the pretreatment form can get the data given that the patient id should be passing through

### Meeting with Ben and Toni
- thinking about the future
    - priority shifting away from the video conferencing towards the ios app
- Toni was saying we have our MVP and now we have to start getting polished
- there's also a problem of the doctors getting too many texts
- toni says it looks good
    - have it so that you can text it to the patient (this would need the patient's email)
    - a realtime up date would be good (so if the patient hasn't signed the form)
    - alerts when the patient has finished
 

## (2024/04/11 8:25午前)
- okay, now you have a few things that you need to work on
    - the first is that when you load existing consents, the display is changed such that only the already signed consents appear, you have to fix this
- unticking anything seems to fix a lot of problems
- maybe when I convert types, I should be making a new things and sticking things in
- generate an expiry date (this would be in python)
- need a treatment date in the office use section (send patient form)
    - this goes into the submit form cmd
- implement functionality for return clients, starting with the sent patient form
- fix the display issues in the pretreatment form
    - medical history checkboxes
- add a meaningful preview to the submit form
- the date picker seems to gravitate towards 2024
- make it so there are no default values and that placeholders show in month and day


## (2024/04/10 8:09午前)
- my mind is a bit hazy from last week, let's try to figure out where we are at with the submit to doctor button
- sorted out the submit button with ben
- currently in type hell
- signatures are done in different ways
- list of things in this ticket that need doing
    - consents reorder as soon as you tick anything
    - when loading existing consents, all the other consents disappear
    - you can't reenter information in medical history and possibly bdd assessment
- getconsents seems to have fixed it
- next up fix the order

```sql
SELECT patient.patient_id, jsonb_pretty(medical_history.medical_history_details) AS "medical_history_details" FROM
     patient
     LEFT JOIN medical_history
     ON patient.patient_id = medical_history.patient_id
 WHERE patient.patient_id = 'ba639dd7-477f-4335-8cc3-3aa2743be44b';    
```
```sql
SELECT patient.patient_id, 
    jsonb_pretty(medical_history.medical_history_details) 
    AS "medical_history_details",
    jsonb_pretty(assessment_submission.assessment_submission_details) 
    AS "assessment_submission_details",
    jsonb_pretty(consent_submission.consent_submission_details) 
    AS "consent_submission_details"
    FROM patient
        LEFT JOIN medical_history
        ON patient.patient_id = medical_history.patient_id
        LEFT JOIN assessment_submission
        ON assessment_submission.patient_id = patient.patient_id
        LEFT JOIN consent_submission
        ON consent_submission.patient_id = patient.patient_id
     WHERE patient.patient_id = 'ba639dd7-477f-4335-8cc3-3aa2743be44b';    
```

        SELECT *
        FROM external_form_access
        INNER JOIN pretreatment_form
            ON pretreatment_form.external_form_access_id = external_form_access.external_form_access_id
        WHERE external_form_access.external_form_access_token= 'ba639dd7-477f-4335-8cc3-3aa2743be44b';

        
## (2024/04/05 8:19午前)
- okay the first major task is to make it so it fetches saved bdd assessments (the latest one)
- it looks like consents are disappearing again and you'll need to look into why
    - I thought you solved this already!!!
- sometimes the column is called created and at other times the column is called created_at
- it looks like you fixed the consents problem
- ben says just to stick it in the prescriptionState
- get a list of consents, stick them in the right place (you can split them fairly easily)
- sort out the submit to doctor button
- you are up to two different things, sorting out consents and sorting out the submit to doctor button


## (2024/04/04 8:28午前)
- okay you are building a data structure
- current problem on your mind is how to parse the list of consents into something
- I think the form prefill might be important, think through this, this seems like the right time to get everything
- maybe you can replace prefill with some logic
- as soon as you open the form, it checks if it's in the pretreatment table, if it is it fills everything it can in otherwise it fills the email, first name and last name
- okay, you'll add a new msg and cmd msg and after that you'll do the prefill
    - or you'll replace the prefill
- maybe this would be easier with two queries, one for consents, one for everything else
- I think the json queries are a nice way of doing it
- let's just get the first two things first
    - actually lets ONLY get the patient
- problem at the moment is that the none type is not iterable
- it's extremely interesting that state isn't coming in
    - need to figure this one out
- the state problem has been solved
- now you have to make it not create a new patient if it's already got a patient
- (3:36午後) next up you have to work with assessments (just get the latest)
- (3:37午後) after that it's consents and media consents
    - maybe this should be a single query?
    - then in elm the difference needs to be worked out
- (3:57午後) okay you are up to getting the existing assessments, this is at least partially implemented in elm, you should probably go to python next
    - you also want to get rid of the printing that's happening in the python



## rethinking the logic
- open form
- check if already exists
    - if it does it autofills the patient details and medical history
        - then it gets the latest assessment
        - then it gets the consents and media consents
    - else, it autofills the form


I think the below is it
```sql
select patient.patient_id, clinic_id, patient_details 
FROM patient 
inner join pretreatment_form 
ON pretreatment_form.patient_id = patient.patient_id 
inner join external_form_access
ON pretreatment_form.external_form_access_id = external_form_access.external_form_access_id
WHERE external_form_access.external_form_access_token='pform-egxLAXnTMWwZGKx8JoBCbwwWBDJUrYvNbEvd2wfR0';
```
### thinking through logic
- open form
- check if it already exists in the pretreatment form table
    - if it does then autofill the form with all the relevant details (from external forms table)
    - else, create autofill with details
- when the patient details have been added and they hit next, create an entry in the pretreatment form table
- okay, so you are getting a list, presumably a row for every consent


```sql

SELECT json_build_object(
    'patient', json_build_object(
        'patient_id', patient.patient_id,
        'patient_details', json_build_object(
            'clinic_id', patient.clinic_id,
            -- Add more patient details here as needed
        )
    ),
    'medical_history', json_build_object(
        'medical_history_details', json_build_object(
            -- Add more medical history details here as needed
        )
    ),
    'assessment_submission', json_build_object(
        'assessment_submission_details', json_build_object(
            -- Add more assessment submission details here as needed
        )
    ),
    'consent_submission', json_build_object(
        'consent_submission_details', json_build_object(
            -- Add more consent submission details here as needed
        )
    )
)
FROM patient
LEFT JOIN medical_history ON patient.patient_id = medical_history.patient_id
LEFT JOIN assessment_submission ON patient.patient_id = assessment_submission.patient_id
LEFT JOIN consent_submission ON patient.patient_id = consent_submission.patient_id
WHERE patient.patient_id = '%s';


SELECT jsonb_pretty(
    jsonb_build_object(
        'patient', json_build_object(
            'patient_id', patient.patient_id,
            'clinic_id', patient.clinic_id,
            'patient_details', patient.patient_details
        ),
        'medical_history_details', medical_history.medical_history_details
        ,'assessment_submission', assessment_submission.assessment_submission_details
        ,'consent_submission', consent_submission.consent_submission_details,
        )
    )

FROM patient
LEFT JOIN medical_history ON patient.patient_id = medical_history.patient_id
LEFT JOIN assessment_submission ON patient.patient_id = assessment_submission.patient_id
LEFT JOIN consent_submission ON patient.patient_id = consent_submission.patient_id
WHERE patient.patient_id = '4ae21730-39ad-4c28-aaa2-972bde79542f';
    
```


```elm
type alias PretreatmentFormData
{
    patient_id: String,
    ,clinic_id: String
    ,patient_details: Domain.PatientDetails
    ,medical_history_details : Domain.MedialHistoryDetails
    ,assessment_submission_details : Domain.AssessmentSubmission
    , consent_submission
}
```

```sql

SELECT *
FROM (
    SELECT 
        patient.*,
        jsonb_to_record(medical_history.medical_history_details)::text AS medical_history_details,
        jsonb_to_record(assessment_submission.assessment_submission_details)::text AS assessment_submission_details,
        jsonb_to_record(consent_submission.consent_submission_details)::text AS consent_submission_details
    FROM 
        patient 
    INNER JOIN 
        medical_history ON patient.patient_id = medical_history.patient_id  
    INNER JOIN 
        assessment_submission ON patient.patient_id = assessment_submission.patient_id
    INNER JOIN 
        consent_submission ON patient.patient_id = consent_submission.patient_id
    WHERE 
        patient.patient_id = '4ae21730-39ad-4c28-aaa2-972bde79542f'
) AS subquery;
    
```

## (2024/04/03 8:11午前)
- Somehow when you get to page four nothing is showing up, I wonder if there's an if condition that has to do with the pager
- Okay, media consent is there but pre-treatment isn't
- okay so patient id is nothing
    - this seems deep, you'll need to reason through this logically
    - you won't get a patient id unless you've created a patient and it's in the database (but that's what you want to happen)
- okay now you know that you lose the list of treatment type consents in the function `updatePrescriptionStatesInViewModel `
- okay the treatment types problem has been solved!!!
- Next up see if everything works and if you are adding anything to the database
- it looks like after signing something in media consents, it becomes consents
- okay, so the "treatmentTypeConsents" in media consents went from 2 to 11
- this problem is fixed!!!
- Okay, now you need to figure out what's happening to the consents and the media consents 
- maybe test adding the patient to the database with a brand new patient with a new name and everything
    - after this, try pulling everything from main in
- looks like everything works!!!
- okay you need to think about next steps, looks like you can start to polish it
    - maybe make the next buttons dependent on submissions rather than just filling everything in
- you can make a final page
    - you can also ask Ben tomorrow if you can just merge everything into main
- okay what to put on the final page? I guess you can actually use the datamodel here to view
    - personal details preview
    - medical history preview
    - bdd assessment preview
    - consents preview
    - media consents preview
- A whole other thing you should work on is to allow updates
- the behaviour you want it that when it opens a form, it checks the pretreatment table and loads all the data from there
- I guess when it creates a new pretreatment form with patient, now it should check instead if one already exists and preload things

### preloading data
```sql
SELECT * FROM pretreatment_form
    WHERE external_form_access_id = '%s'
 
```

```sql
SELECT * FROM patient
    left join medical_history
        on patient.patient_id = medical_history.patient_id
    left join assessment_submission
        on patient.patient_id = assessment_submission.patient_id  
    left join consent_submission
        on patient.patient_id = consent_submission.patient_id  
    where patient.patient_id = '%s';
```


```sql
    
 select * from patient 
    inner join medical_history 
        on patient.patient_id = medical_history.patient_id  
    inner join assessment_submission
        on patient.patient_id = assessment_submission.patient_id
    inner join consent_submission
        on patient.patient_id = consent_submission.patient_id
    where patient.patient_id = '4ae21730-39ad-4c28-aaa2-972bde79542f';
```



## (2024/03/28 8:10午前)
- Ask Ben about assessmentContainerToAssessmentContainerSubmission 
- Structure And Interpretation of computer programming
    - also lectures on youtube
- (2:07午後) the problem that you are facing now is that you lose unit completely, you need to fix that
- (4:02午後) up to line 376 of Pretreatment.elm, I need to convert a list of ConsentTypes to a list of TreatmentTypes


## (2024/03/27 10:06午前)
- okay some kind of plugging in what I have to the prescription state would be good
- let's think through this in english
- when you load the form you want to check if there is already a patient
    - so you check the pretreatment file
        - you get those patient details
- medical history isn't the same
- you also might need nurse id
- should I be storing the patient in the datamodel
- you are up to
    - validDataModelToPrescriptionState : String -> ValidDataModel -> Domain.PrescriptionState
    - you need a way to convert assessments

## (2024/03/22 4:02午後)
- you are up to the route function /add_patient_from_pretreatment_form


## (2024/03/22 8:19午前)
- okay if this works you have to remember to turn the result into a normal type for the toDomainAssessment function
- the model seems to be working
- you need to get patient into the consents model for this to really work, meaning you have to work on the database
- patient is in the prescripiton state, it needs to be put into everything
- do the same thing that you just did with media consents
- now you need to figure out how to deal with the database
- thinking out loud now 
    - okay you want to make a table that only has a patient id and the pform thing
    - you first have to make a new patient, then you make a new entry to this table
    - you do it on the first next, or maybe as soon as you have a patient
        - after this you want to first make the page check if there is an entry with the p-form id in that new database table
- you definitely want to use the add patient route
    - maybe another route that uses the add patient route
- now we'll create this and see if it makes a patient
- maybe the if can happen on the python
    - it can check to see if the patient already exists and then create it if it's not already created
- currently getting the following error
```python
pform-egxLAXnTMWwZGKx8JoBCbwwWBDJUrYvNbEvd2wfR0 :: external_form
'str' object is not callable
Traceback (most recent call last):
  File "/var/home/sashin/.work/global/Application/python-flask/helpers.py", line 120, in pool_decorated_function
    result = f(cursor, content, *args, **kwargs)
             ^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^^
  File "/var/home/sashin/.work/global/Application/python-flask/routes/pretreatment_form.py", line 50, in add_patient_from_pretreatment_form
    cursor.execute("""
                   ^^^
TypeError: 'str' object is not callable

127.0.0.1 - - [22/Mar/2024 15:41:12] "POST /add_patient_from_pretreatment_form HTTP/1.1" 200 -
```

# thinking slowly about this
# hmmm...
# do I want an upsert
# I want a function that checks if it's already in the pretreatment form table
# after that I can check if the clinic_id and email already exists

```
CREATE TABLE pretreatment_from (
    pretreatment_form_id SERIAL PRIMARY KEY NOT NULL,
    external_form_access_id UUID NOT NULL,
    patient_id UUID NOT NULL,
    FOREIGN KEY (external_form_access_id) REFERENCES external_form_access(external_form_access_id),
    FOREIGN KEY (patient_id) REFERENCES patient(patient_id)
);
```


## (2024/03/21 7:58午前)
- okay starting work
- bdd form is magically working
- you're going to make a pretreatment form database that only has a patient id and a pform id
- it looks like there is an assessment_submission and a consent_submission table and a patient can have many of each
- this is the commit hash b79fbc9d
    - or maybe this 80859e64
- okay back to the other ticket, you want to make a change to the database
- first let's make a new branch and get patient being created
- when you press next you want to try to make a patient table out of patient details
    - maybe the id should be 1
- now you have the function to make a patient table, where do you use it?
    - maybe on the update even, only if you can
- the patient table is now added
- let's do all the datamodels first then deal with the database
- maybe ask ben about how these models are transformed to data
- you are up to figuring out why the bdd datamodel doesn't work



## (2024/03/20 8:14午前)
- Whether or not the save assessment button is active is what you should use for the pager's next page too
- you just got rid of the shadow so this looks alright
- you should do global searches for Debug.log more often
- okay, so that's done, the consents look fine, next up is the media consents
- the next thing is to get all of this working with the states
- state is working now to add the media thing
- in the bdd form if you press yes you can't undo
- you should probably add a new ticket for adding media consents, I mean a new branch



## (2024/03/15 8:11午前)
- Maybe you can give those checkboxes a max width
- maybe a bit more spacing
- same with the bdd questionnaire form
- Let Ben know that you want to store the progress of the form in a new table in the database and only create the patient, medical history etc properly at the end
- for some reason when you do the first it negates the second
- for some reason when you enter *anything* everything goes blank
- you want to repeat the order of what you you've got with the medical history and the bdd assessment page
- let's fix the aesthetics of the bdd form and then the other thing with max-width
- okay you want to add the treatment type consents to the model
    - you can do this fairly early on I think, like at the beginning
- are there any consents if there are not treatment types? It seemed to me like there were
- (3:47午後) you should just put these forms in the same container that the are in the prescription state thing
- (3:51午後) you are up to making these forms look nice!!!
    - (3:51午後) after that you just have to add media consents
    - (3:57午後) you also want to stop printing in python





```sql
        select
            external_form_access_details
            from external_form_access 
            where external_form_access_token = 'pform-WxnKBcGmHP7BNmRDAdAcvD8kTTNHeZahxbpeTavU6D4'; 
```

```sql
        select
            external_form_access_details ->> 'patient_first_name' as patient_first_name
            ,external_form_access_details ->> 'patient_last_name' as patient_last_name
            ,external_form_access_details ->> 'patient_email_address' as patient_email_address
            from external_form_access where external_form_access_token = %s;
```
## (2024/03/14 9:47午前)
- you want to do *some* kind of validation now, maybe better validation later, to see if it is filled 
- maybe like a PatientDetails.Validate
- validation seems to be working *perfectly*
- now what to do about it?
    - let work on better next buttons?
    - or make it so the page is created on validate?
- do I need these different states if I have the stepper?
    - how do I make it change state when I push the stepper?
- okay now you have to figure out what to display for medical history
- you did it wrong you need to display a form
- okay it works
- get rid of the state here and replace it with the viewModel
- now the name autofill is broken
- everything broke again and you need to fix it again
- okay I think you can do this!!!
    - next up: the bdd assessment
- ask Ben if the patient should be able to leave all the fields in this form empty
- Next up: trying to figure out how the bdd form isn't working






## (2024/03/13 7:46午前)
- Ask Ben for a status update and what the patched release was for and everything
- Also mention to Ben that you feel the name and email should be automatically entered
    - also the pretreatment onboarding functionality ticket
- ask ben about the Token in the pretreatmentform
- I have an interest in refactoring it to use the datetype mentioned in the elm slack
- (8:42午前) Let's think through what this form needs... hmm...
    - it's on azure
- (9:19午前) Thinking about the ticket now, how do divide this work into tickets
- (9:31午前) after you fix that you want to make a really big ticket for the pretreatment form
- (9:49午前) I don't think you can fix the azure thing without ben's help
    - should be possible to finish the rest of the form though
- (9:57午前) you need to create a function in python that given a token returns the first_name, last_name and email
- (10:08午前) another quick mystery solved!
    - okay you are ready now to deal with autofill
- (10:53午前) okay now add it to app and access it through elm
- (12:09午後) you could make a stepper component
- (3:57午後) next up you are going to want to get the pager working


## (2024/03/08 8:41午前)
- [x] You should ask ben about the update office use section
- [x] you are still going through getting rid of the red lines
    - hopefully this still works perfectly fine afterwards
    - after this you should see if you can use that fancy date type
    - you should look at Patient.elm and all the decoder stuff to make sure you don't break anything
        - that's what you're scared about atm, it's what you need to consider when changing either the date or the address types
    - remember that your actual ticket is to get the interface working responsively
    - only six characters left
- I should always make a new ticket for refactoring, gotta remember this
    - okay if you want to refactor either date or address then use the new ticket
- next up you want to get the address dropdown working
- so far the address search isn't working, you want to make it that when you search the right update happens
- maybe figure out how the address search works and replicate it
- onInput InputAddressSearch
- (3:45午後) for next wednesday
    - you are going to want to open your email to access the pretreatment form
    - you should probably go over all the notes you've written today and yesterday
    - pretty sure you should enter the first name, last name and email for the patient
    - ask about the pretreatment onboarding functionality ticket
    - also switch branch to the 




## (2024/03/07 8:12午前)
- Okay now it works, submitting a patient is exactly as you would expect
- They don't want buttons
- also the two similar sets of consents can't be side by side
- I think I want to use a stepper
    - finish patient details and then use a stepper
- also need to figure out an on blur way of submitting things
- maybe this isn't the right way
    - surely you should be able to use a dropdown model
- okay so it's this azure search results thing, hmm...
    - how does this work with the rest of my model
    - I don't think I can easily plug and play my dropdown here
- (3:57午後) Okay, what you did was change the model and now you ared dealing with the fall out
    - after that you will see if you can improve the model further
    - after that you will make it responsive
- (3:57午後) Need to think of the database and scaling it up with Azure





## (2024/03/06 8:02午前)
- Good morning
- Okay, I'll look through Azure first and think about where we are at
- We will be first getting the external form working (unless Ben has done that already)
- actually I'll pull from main-onion and merge that in first
- okay, this is messy, I didn't make a new branch for this
    - maybe I should make a new branch and then merge main-onion here
- split external forms into onboarding and send to patient
- okay, now main is merged
- if nothing else is higher priority, let's get onboarding working again and then get the send form to patient working
- email validation in send to patient form
- make the email send a link, not plaintext link
- you can move out the enter patient details from the patient section AND you can redo it responsively with elmui -> or even without
- maybe you can even pull out an address component
- I feel like the patient's first name, last name and email should definitely be prefilled
- What *should* happen when you enter a patient's details?
    - looks like they all lock, it's kind of nice, I think I will add an edit button though
    - to get it working again on your branch you have to actually deal with the boolean that you are passing in for disabling the buttons
- definitely add better client validation (maybe dropdowns for the date?) for the phone number also!
- (4:01午後) Figure out why the fields are not being disabled



```python
import os
import psycopg2
from psycopg2 import pool
from contextlib import contextmanager

# Set up the PostgreSQL connection parameters
host = os.environ['DATABASE_URL']
dbname = os.environ['DATABASE_NAME'] 
user = os.environ['DATABASE_USER']
password = os.environ['DATABASE_PASSWORD']
sslmode = "require"

connection_pool = psycopg2.pool.SimpleConnectionPool(
        1, 2,
        user=user,
        password=password,
        host=host,
        database=dbname,
        sslmode=sslmode
    )
```



## (2024/03/01 9:20午前)
- NurseId, DoctorId, ClinicId
- everything else in a json blob called formData
    - patient details
    - list of prescription items
- [ ] (11:43午前) come back to the python to add a form entry to the patient_form database
- [ ] (12:10午後) come back to `sendFormToPatient.elm` and make it do something when a form is successfully sent (like make it say "form sent")
- (3:54午後) Okay you are up to getting the new external form working




```sql
CREATE TABLE patient_form(
    patient_form_id UUID primary key,
    nurse_id UUID not null,
    doctor_id UUID not null,
    clinic_id UUID not null,
    form_data JSONB not null
);```


```sql
CREATE TABLE patient_form (
    patient_form_id UUID PRIMARY KEY,
    nurse_id UUID NOT NULL,
    doctor_id UUID NOT NULL,
    clinic_id UUID NOT NULL,
    form_data JSONB NOT NULL,
    external_form_access_id UUID NOT NULL,
    posix_time bigint default extract(epoch from current_timestamp)::bigint not null,
    timestamp_with_timezone timestamp with time zone default (current_timestamp AT TIME ZONE 'Australia/Sydney') not null,
    FOREIGN KEY (nurse_id) REFERENCES nurse(nurse_id),
    FOREIGN KEY (doctor_id) REFERENCES doctor(doctor_id),
    FOREIGN KEY (clinic_id) REFERENCES clinic(clinic_id),
    FOREIGN KEY (external_form_access_id) REFERENCES external_form_access(external_form_access_id)
);
```


The JSON form data should have
- a list of *treatment types*
- a list of *prescription line items*
- patient_first_name
- patient_last_name
- patient_email

- ## (2024/02/29 12:38午後)
- Been spending all day helping Ben with fixing bits and pieces for the release
- Figure how to get your checkboxlist working, probably just have to follow the compiler


- ## (2024/02/28 8:05午前)
- Today there's an APA meeting, sounds like it will be fun
- [x] Okay first let's redo the desktop view
- [x] the little triangle shifts when you click on a dropdown, you should fix that
- (10:05午前) you gotta remember that you can do the min width in elm-ui with minimum
- add select doctor
    - (10:54午前) Going through the compilor errors now, adding the doctor field to the form
- add consent form select
- (1:15午後) okay, big merge problems, I can sort out officeuse.elm on my own
    - first do the ifOfficeUseSection cmd map
    - after this you have to do something that you wanted to do
        - oh right move the treatmenttypes to the domain
        - okay you are going to move over most messages
- drugbook, treatmentpad, video conferencing, ipad app, these are the fifty billion things that you need
- You need to deal with the fallout from the merge in *PrescriptionForm.elm*





## (2024/02/23 8:47午前)
- Those temporary ids are given you trouble
    - if you add the same of a prescription item then delete one it deletes both (ask ben if you even should be able to add the same item twice)
- Okay you have to think a bunch about what to do next
- mobile
- okay next up is the actual list, maybe you should make it vertical
- also add an empty list element
- next up you should think about how to get tablet looking good
- the iFrames width is 980px
- ask daniel how to handle the case of changing a database table to have a new field
- Ipads meet the desktop range
- next up, you want to fix desktop view, you want to make full width dropdowns
    - you also want to hide the table if there are no treatments
    - you can either make the text even smaller or copy over the phone view



## (2024/02/22 11:28午前)
- Okay now you have to do a different thing, update the database so the volume in favourite prescription items is a float
- after that you should come back to the ticket you are working on and deal with the damage that has been dealt
- okay no damage you just want this to work right away
- you can add the same favourite twice
- okay you know what's wrong, it's the assigned id
- (4:05午後) up to doing that table



## (2024/02/21 8:13午前)
- Nurse Joy doesn't seem to trigger a change in the product screen (if I remember right it was nurses with favourites that do)
- what's in the favourites box IS changing, when you change the stats, I think it should clear
- maybe there should be an add to favourites or remove from favourites button
- can the same favourite be added twice?
- I think I need to make a selectedFavourite in the viewModel that's a maybe domain.prescriptionItemLine
- after you fix the favourite you can work on making everything look nice
- new problem, the hit area is all wrong, you have to fix it
- the behaviour will be this, when the row is filled, if there is a favourite that corresponds with it there will be a remove button otherwise an add button
- next up get the favourites button working and then start building the table
    - adding the favourites will actually require some database magic
    - thinking carefully now, how does the command work?
- ask ben about the python routes for adding and deleting a favourite, why do they return things?
- adding to favourites seems to work but not immediately, you are not sure about removing from favourites
- adding and removing doesn't refresh?
- looks like remove isn't actually removing it from the database
-

## (2024/02/16 8:17午前)
- should we move all our cmd messages to a module so we can reuse them better?
- you should ask ben if this is the only interface where nurses will be chosen
- you should add moonlander shortcuts for starting a huddle as well as muting and unmuting your mic
    - entering and leaving a huddle is `ctrl+alt+shift+h`
    - muting and unmuting i think is `ctrl+shift+space`
- (1:14午後) I think you want to separate favourites to another line
    - after that you can work on the category filter
        - okay fine, you'll get the product categories, or you can get them from the products??
            - no you need to get all the categories
    - also want to make things look nicer
    - [x] you also want to change the default filter text
- (3:53午後) okay status, the fitler by category works, the favourites work
    - I believe what's next is, making the form look nice
        - I want to make it so that they use text areas
        - I want to make the selected one show in the list but with a cross next to it, maybe it's background should be red?





## (2024/02/15 10:11午前)
- First thing to do is to update the OfficeUse model
    - (10:59午前) this is taking a long time, after you eat lunch put on the japanese music pod and power through it
        - take a break now and catch up on your japanese flashcards
    - (12:35午後) oaky you fixed the update function, the next step is to move the whole form over to send form
    - (1:48午後) Next up you have to add a button to show the screen and hide it again
    - (3:51午後) okay, so you are going to add a nurse dropdown to the sendFormToPatient screen





## (2024/02/14 9:25午前)
- today your brain feels slow, even though oura said your condition is 90
- The data isn't sending through from the command messages
- Okay, you are making progress, you want to make a new page maybe you should look at how it's done elsewhere
- you want to make the form totally different
- maybe merge the dropdown stuff into the other ticket??
- after that you want to add the ability to choose a favourite
- you should actually make the things text areas, not just text




## (2024/02/09 8:47午前)
- Ask ben why there isn't an update function in shared


  const payload = '{"member":{"_id":"12357987893","contactId":"cfe0d2d0-74f3-4242-b805-506b9be5d050","loginEmail":"sashin@allurepacificaesthetics.com","profile":{"nickname":"Ben Tyler","slug":"ben-tyler","profilePhoto":{"id":"","url":"https://lh3.googleusercontent.com/a/AGNmyxZQQiQ34MEQkqSZR9zS6p2LkpAFmfiFC2np8O00=s96-c","height":0,"width":0}},"contactDetails":{"contactId":"cfe0d2d0-74f3-4242-b805-506b9be5d050","firstName":"Ben","lastName":"Tyler","phones":[],"emails":["ben.tyler@allurepacificaesthetics.com"],"addresses":[],"customFields":{}},"activityStatus":"ACTIVE","privacyStatus":"PUBLIC","status":"APPROVED","lastLoginDate":"2023-05-08T02:48:52Z","_createdDate":"2023-03-03T01:11:41Z","_updatedDate":"2023-03-15T03:11:27.390Z"},"licence":"wix_preview_authenticator","secret":"q_hGPysrBswcLMCuFaBYmQ"}' 


Thinking out loud
- you are building a component for 

## (2024/02/08 8:02午前)
- okay you have a new ticket
- but you realise that you can improve the back button further by resetting the model completely
- I've gotten the go ahead to start making this with elm ui, I'm really happy about this
- think through the states of this thing

```el
toHtml5DateString : Time.Zone -> Time.Posix -> String
toHtml5DateString timeZone time = 
    String.fromInt (Time.toYear timeZone time)
        ++ "-" 
        ++ toMonthNumber (Time.toMonth timeZone time) 
        ++ "-"
        ++ String.padLeft 2 '0' (String.fromInt (Time.toDay timeZone time))
```

- (2024/02/02 3:53午後)
- Next up you have 965 raised concerns for doctors and 966 Telephone link to call nurse


- (2024/02/02 11:45午前)
Alright let's organise this document and write some new ticket files
- you need to get a better alt on you keyboard, mabye in the thumbkeys


- (2024/01/26 2:40午前)
Okay, you want to do a little + on the right side of the accordionheader, it becomes minus when you open it
    - [x] you want to do it in a little circle (Border.radius and clip), position them with spacebetween I think
    - you also have to create two end points in python, a treatment access entry event (to store the event) and do an upsert on the treatment_access_entry table


- (2024/01/31 8:30午前)
Okay you have this query that seems to insert the event


- (2024/01/31 4:03午後)
- remember to modify shared at the beginning and install the requirements.pip
- you should make a guide on starting a new ticket


- (2024/02/01 9:26午前)
The following is necessary in main.js for you to log in with wixauthtester
- window.wixAuthTester = function()


- (2024/02/02 9:10午前)
- You have a ticket that you need to display the patient's bmi, that's 905, you can make a file for this ticket
    - review prescription request
    - make a table with all the patient's BMIs

Tickets you have active
- 905 display patient's bmi
    - display patient's past bmis in a table in review prescription request
- 965 raised concerns for doctors
    - list raised concerns by nurses on the main screen if they are there
- 966 telephone link to call nurse
    - telephone link to call nurse on main screen no matter what




```js
     const payload = '{"member":{"_id":"12357987893","contactId":"cfe0d2d0-74f3-4242-b805-506b9be5d050","loginEmail":"sashin@allurepacificaesthetics.com","profile":{"nickname":"Ben Tyler","slug":"ben-tyler","profilePhoto":{"id":"","url":"https://lh3.googleusercontent.com/a/AGNmyxZQQiQ34MEQkqSZR9zS6p2LkpAFmfiFC2np8O00=s96-c","height":0,"width":0}},"contactDetails":{"contactId":"cfe0d2d0-74f3-4242-b805-506b9be5d050","firstName":"Ben","lastName":"Tyler","phones":[],"emails":["ben.tyler@allurepacificaesthetics.com"],"addresses":[],"customFields":{}},"activityStatus":"ACTIVE","privacyStatus":"PUBLIC","status":"APPROVED","lastLoginDate":"2023-05-08T02:48:52Z","_createdDate":"2023-03-03T01:11:41Z","_updatedDate":"2023-03-15T03:11:27.390Z"},"licence":"wix_preview_authenticator","secret":"q_hGPysrBswcLMCuFaBYmQ"}' 

```


## what do you have to do now
- fix the changes for the merge, the main.js and the migration file, the extra ;)
- redo the doctor's notes table but with not nulls
- 
- back to [[911-doctors-notes]]
- (10:35午前) you've got the ssh key working!!!


### This query adds the event for adding a treatment area to an access group
```sql
INSERT INTO treatment_access_group_entry_event  (treatment_access_group_entry_id , event_type, event_data)
VALUES ('ab2ff657-cd14-4f26-9bd7-436cc0564852', 'insert_treatment_entry', '{
  "product_id": 162,
  "treatment_area_id": 1,
  "treatment_access_group_id": "fa555423-5fc9-468f-b63c-aa2e1f764b6c"
} ');
```

### This query adds the event for removing a treatment area to an access group
```sql
INSERT INTO treatment_access_group_entry_event  (treatment_access_group_entry_id , event_type, event_data)
VALUES ('ab2ff657-cd14-4f26-9bd7-436cc0564852', 'remove_treatment_access_group_entry', '{
  "product_id": 162,
  "treatment_area_id": 1,
  "treatment_access_group_id": "fa555423-5fc9-468f-b63c-aa2e1f764b6c"
} ');
```

### this query adds a treatment area to a treatment access group
```sql
insert into treatment_access_group_entry (treatment_access_group_entry_id, treatment_access_group_id, product_id, treatment_area_id ) 
values (gen_random_uuid(),'07468ded-b80e-447b-a956-2fba8213efa0', 174, 3 )
on conflict (treatment_access_group_id, product_id, treatment_area_id) 
do update set entry_state = 1;
```

### this query removes a treatment area from a treatment access group
```sql
UPDATE treatment_access_group_entry
SET entry_state = 0
WHERE treatment_access_group_id = '07468ded-b80e-447b-a956-2fba8213efa0'
  AND product_id = 174
  AND treatment_area_id = 3;
```

I think that's a portmanteau of insert and update, so it checks if the record exists and updates it if it does and inserts it if it doesn't

this is for the treatment entry table

thinking through this, given a groupid you want to remove or add an area

okay checks to see if the same
    - treatment_access_group_id
    - product_id
    - treatment_area_id
are there, if they ARE then update the entry state (1 if add and 0 if remove)

if they are not there then add a new entry



okay I guess you could have a remove and an add


okay so you want to add the entry and remove the entry


(2024/01/31 11:30午前)
- add two new columns, prescription count (total count)
    - prescriptions (excluding semiglutide)
    - semiglutide
    - total


```elm
        Element.layout []
            (Element.row [] [])
 ```

--- 
### New ticket
```sql
SELECT
    clinic.clinic_id,
    clinic.clinic_details->>'clinic_name' AS clinic_name,
    COUNT(prescription.prescription_id) AS prescription_count,
    (
        SELECT COUNT(DISTINCT prescription.prescription_id)
        FROM prescription
        INNER JOIN provision_prescription_line_item ON prescription.prescription_id = provision_prescription_line_item.prescription_id
        INNER JOIN product ON product.product_id = provision_prescription_line_item.product_id
        INNER JOIN product_category ON product.product_category_id = product_category.product_category_id
        LEFT JOIN nurse AS innerNurse ON innerNurse.nurse_id = prescription.nurse_id
        LEFT JOIN clinic AS innerClinic ON innerNurse.clinic_id = innerClinic.clinic_id
        WHERE
            product.product_category_id = 18
            AND innerClinic.clinic_id = clinic.clinic_id
            AND prescription.entry_state = 1
            AND EXTRACT(MONTH FROM prescription.timestamp_with_timezone) = 1
            AND EXTRACT(YEAR FROM prescription.timestamp_with_timezone) = 2024
    ) AS SemiglutideScripts
FROM prescription
LEFT JOIN nurse ON nurse.nurse_id = prescription.nurse_id
LEFT JOIN clinic ON nurse.clinic_id = clinic.clinic_id
WHERE
    EXTRACT(MONTH FROM prescription.timestamp_with_timezone) = 1
    AND EXTRACT(YEAR FROM prescription.timestamp_with_timezone) = 2024
    AND prescription.entry_state = 1
GROUP BY clinic.clinic_id, clinic.clinic_details->>'clinic_name';
```


you need to replace the month and the year
---
## Active Tickets
- [[911-doctors-notes]]


--- 

## The Stack
### Postgresql
- You should watch [this video on database migrations](https://www.youtube.com/watch?v=dJDBP7pPA-o)
- maybe show this video to Ben [SQLx is my favourite PostgresQL driver to use with Rust](https://www.youtube.com/watch?v=TCERYbgvbq0)
### Python + Flask
- You currently feel rather comfortable with this and believe you can gradually learn what you need as you do tickets
- you need to run `pip install requirements.txt` in the python-flask folder whenever you start a new ticket
### Vite + Elm

### Nice things to do (archived/outdated)
- a command line workflow for interfacing with the postgres database
    - (2024/02/16 4:00午後) Okay you've made progress, now just a script to start it
- maybe a script that opens three terminals and goes into the dev
- there is a bug at the moment with concerns raised
    - bring this up with Ben -> they don't get added to the table until you hit next, we should make a new ticket
- can a prescription request only have one nurse?
- okay you need to fix two bugs now
    - one of the bugs is blocking release, this one is... the time one, you want to change the toHtml5DateString to what it was before
    - replace with the following
