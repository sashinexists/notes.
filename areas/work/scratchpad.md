## (2024/08/09 8:38午前)
- (8:38午前) you have the api calls saved
- (8:51午前) maybe start with sorting favourites
- (10:30午前) go back to favourites, need to think about it
- (11:08午前) you probably want to copy all the code from that package in
    - probably in components
    - components drag drop
- (1:06午後) okay fixed all the errors in the model, next up make the buttons look nice
- (1:52午後) now to get this draggable in
- (3:44午後) you want to do this at the level of python and postgres, but you need to figure out how
    - you are up to update in ReorderFavourites.elm, line 58
    - also you need to get in touch with Toni about the wix










## (2024/08/08 8:28午前)
- (8:28午前) focusing on the wix as well as getting ready for the week without ben
- (11:07午前) Wix stores app id (required for this endpoint): 215238eb-22a5-4c36-9e7b-e7c08025e04e
- (11:58午前) sorted out the whole next week and a half
    - wix store integration
        - need to call toni so that she pays for staging
        - just see what this is about first
            - try to get into the staging thing
            - then try to call Toni
                - what to say in the call?
                    - Hi Toni, have been working on the wix integration and it's been going well
                        - to develop and test this we'll need a paid account for staging
                - then send an email explaining that you need staging's wix to be paid for when the call inevitably fails
    - sort favourites
    - photos
- (1:38午後) let's try and get the api calls working in cantero
- (2:28午後) all saved in your job folder




```json
{
checkoutTemplateObject: {
    lineItems: {
        quantity: 1,
        catalogReference: ""
    }
}}
    
```

### Things you need to know
ki9uy76t5r4\
#### how to do a hotfix
- make a new branch from the latest RC (that's in prod)
- make the fix on that branch
- run the pipeline to put it into staging and test it there to see it's all working
- make a release candidate branch
- run the pipeline to put the release candidate branch into production
- run migration up using postman
    - apaportal.com/migrations_up
    - apaportal.com/migrations_down (to bring them down again)

#### the reset button and the logs in the portal

#### Work to progress with (Wix Integration)


## (2024/08/07 8:00午前)
- (8:00午前) okay starting from last week
- (8:01午前) adding a maximum unique products rule
- (8:12午前) right now it's not entering into the database when you add a new rule
- (8:25午前) now you can enter the rule in the database as well as get it from the database
- (8:43午前) figure out how to get the number of unique products
- (9:57午前) thinking about how to have favourites sortable now
- (10:05午前) with this solution the sequence isn't just for the nurse
    - might not matter for implementation
- (12:11午後) now you want a button that switches the sections, maybe make the button that switches and goes back first
- (3:56午後) up to figuring out the wix api again


## (2024/08/02 8:00午前)
- (8:00午前) going to start by finishing that merge and then investigating removing favourites
    - it's readding specifically
    - on this bug, it seems to be if a favourite is no longer possible by the nurses treatment access group
- (12:06午後) okay, return to global rule
- (2:32午後) just gotta  do those checks when you apply a prescription template
- (3:14午後) now adding a new rule for maximum unique products
- (3:51午後) right now adding a new maximum unique products rule doesn't work, there is a server error, this is what you are working on
- (4:01午後) up to Domain/Rules.elm -> line 114








## (2024/08/01 7:59午前)
- (7:59午前) starting with the global rules 
- (8:45午前) looks like you just have to play with the compiler for a while
- (10:06午前) up to getting global rules in initCmdmsgs
- (11:50午前) editing the global rule doesn't work at the moment
- (12:16午後) okay editing the global rule works
    - let's test add, remove and edit of all three types of rule
- (12:20午後) everything seems to be working at the moment
- (12:22午後) now let's try to implement it in SelectPrescriptionItems, then work on the new rule
- (3:54午後) with the templates you need to make the star filled
    - definitely do this
- (3:55午後) also remove favourite didn't work











## (2024/07/31 8:01午前)
- (8:01午前) Maybe start with emailing Toni
- (8:28午前) okay you have a few new tickets to work on, and there is one that you'll have to call Jhordan
    - [x] remove HCP section
        - done this (but only so it doesn't show on the side bar, haven't removed the code entirely)
    - [ ] sorting favourites
    - [x] autoselect treatment areas
    - [ ] new product rules (global rules, maximum and max unique)
        - (9:05午前) what should I ask Jhordan
            - is it a maximum of twelve (only if it's the same product?)
                - so can you have twelve of one product and then some other lines?
                - there be the same product for the same area (or is that impossible or not make sense)
            - and is the other requirement that you can have at most six different products?
- (9:46午前) okay pull in the HCP ticked, add the new rule for autoselecting treatment areas, then work on how you'll do sorting favourites
- (10:29午前) the first thing to do is rename the ruletype AUTOSELCET with AUTOSELECT_INDICATION
    - next up you have to actually add the new rule
- (11:58午前) rule added to the database now you have to parse it in elm at get it working
- (12:18午後) start with editrule then applyrule and finally selectPrescriptionitems
    - (12:58午後) going to have to make an autoselect treatment area errors
        - (1:32午後) just need to add some things
- (2:35午後) next up make clearing work
- (2:44午後) looks like you just need to apply it now
    - may only need to look when selecting a product and a category "possiblyRelevantAutoselectRules"
- (3:33午後) for sorting favourites I think what's needed is a unique integer called order
- (3:43午後) work on the new product rules first
    - let's call the rules
        - maximum prescription items
            - this already exists, you just need to make it work globally
        - maximum unique products
- (3:51午後) this is what you will do
    - create the idea of a global rule
    - implement maximum prescripiton items globally
    - create the maximum unique products rule and implement it
- (4:04午後) up to m62.py, think about what you want the globalRule table to look like


## (2024/07/26 8:18午前)
- (10:07午前) strange behaviour 
- (11:19午前) it's possible that you need to get catalogue rather than products
- (11:41午前) okay filter by category now works!!!
- (11:55午前) now add a text filter
- (12:30午後) two things on the mind
    - 1. Product variants vs catalogue items, the add to cart api seems to want a catalogue
    - 2. pagination in the query you are using
- (4:05午後) above is where you were up to, but you have a new ticket regarding global rules










## (2024/07/25 8:47午前)
- (8:47午前) you should add
- (9:17午前) okay add the filter by category dropdown
- (9:28午前) stopping this to start work on a bug
- (9:38午前) I think what I have to is make it clear the category when you add a product
- (9:49午前) back to wix
- (11:40午前) now you are going to have to get all the wix product variants and stick them in the model
- (12:32午後) think about how you will have the wix things as type in elm
- (1:45午後) you are going to have to make a new route to accomodate this
- (3:51午後) okay what you are up to AlignProductsWithWixStore.elm, line 226, you need to figure out how to store and pass in the text and submsg






 






## (2024/07/24 8:20午前)
- (8:20午前) okay, probably want to email toni about Ben's leave, you can do it after talking to Ben
    - ask ben if he got his payslip and what it was, brief him on what happened, ask him if it's worth messaging toni
- (9:20午前) ben is off 12, 13, 19, 20
- (9:31午前) Ben said he's chasing it up for me
- (12:24午後) okay you have some data, first of all, put these in the database
    - (12:26午後) maybe call the table WixProductVariant
- (12:53午後) would it be good to clear the table and rebuild it every time?
- (2:49午後) actually rethinking this
    - you only really need the id
- (3:13午後) you should probably make this new one in superuser
- (3:50午後) okay now just need to edit this
    - think about how you want it to look?
    - maybe a list of products with a dropdown?
- (4:00午後) up to AlignProductsWithWixStore.elm











## (2024/07/19 8:03午前)
- (8:03午前) Good morning
- (8:03午前) you are going to try to build a structure in python
- (10:11午前) ask ben about how try and accept work, will it stop?
- (10:56午前) thinking about when to do this
    - quick select favourite
    - add item
    - remove item
- (1:09午後) okay a whole new really big task
    - learn about the JWT spec and the wix api
- (2:26午後) a hash is not encryption, it cannot be decrypted back
- (3:17午後) OAuth allows you go give one app permission to access data from another app (without sharing passwords or sensitive information)
- (3:26午後) you are going to have to learn how to do this
- (3:57午後) token that I just made now to the test wix

```
IST.eyJraWQiOiJQb3pIX2FDMiIsImFsZyI6IlJTMjU2In0.eyJkYXRhIjoie1wiaWRcIjpcImY5Yjk2YTQ3LTMwNzAtNGNmZi1iOWQ0LWZlMTQyMjRiZDhlM1wiLFwiaWRlbnRpdHlcIjp7XCJ0eXBlXCI6XCJhcHBsaWNhdGlvblwiLFwiaWRcIjpcImEwMmYzZjZkLTQwYTQtNDk3Zi1iZTZkLThjYzBkY2I1MjNjNlwifSxcInRlbmFudFwiOntcInR5cGVcIjpcImFjY291bnRcIixcImlkXCI6XCJmMzgxZjJmMi1kMjg0LTRhN2YtYjY4NS02ODRjMmVkNzQxMWJcIn19IiwiaWF0IjoxNzIxMzY4NjQxfQ.SPXgkvWhAO9bCb8KvOQC5-SKlIHy2WuaYNZPJjgVwPoBK6qHvA3u0WZ_WjsKFGGFM2KcSsT5HluiW9cU5Z1OQ2UxzuVblCufdAkud3ITU2VvYMXD7Ofpc6onOCQf5ihWdAgiLhuYSwrJI75zFP-6aOdp2LOrDGC_QXL5-6X0Y8g-9S7yV0SKdQBobC-Wj8asKG7XLnNTQkJGLCTLaiq8zdeLr05Vjv49NnbcY9FbbYpcbKJmVUyFLwzMZFWXvXdcaemNZ6mZ4oQv8__KLaDhuBj1_eObskVwR2Q49J4wJ9QuPXTEl_s8A0qE97JvbrofooAFPTHbiJqxC4Oh_747Mg
```









## (2024/07/18 8:38午前)
- (8:39午前) This looks like it's working
- (8:39午前) next up add a dropdown
- (9:18午前) big thing to remember is to make sure this is applied to phone as well
- (10:19午前) also check if the name is already taken
    - alright that's an error along with a blank one
- (3:53午後) postgres blues
- (3:59午後) try recreating the function in m59



SELECT check_prescription_lines('[{"product": {"product_id": 245, "product_name": "Dysport", "product_category_id": 6, "product_category_name": "Anti Wrinkle", "unit_of_measure_id": 1, "unit_of_measure_name": "unit"}, "treatment_area": {"treatment_area_id": 3, "treatment_area_name": "Chest"}, "indication": {"indication_id": 7, "indication_name": "Cosmetic use"}, "direction": "some direction", "repeats": 6}]');



SELECT check_prescription_lines('[{"product": {"product_id": 245, "product_name": "Dysport", "product_category_id": 6, "product_category_name": "Anti Wrinkle", "unit_of_measure_id": 1, "unit_of_measure_name": "unit"}, "treatment_area": {"treatment_area_id": 3, "treatment_area_name": "Chest"}, "indication": {"indication_id": 7, "indication_name": "Cosmetic use"}, "direction": "Some Direction", "repeats": 6}]');


## (2024/07/17 8:22午前)
- (8:22午前) probably need Ben's help testing this
- (9:18午前) Need to call Toni about Ben's holiday
- (9:35午前) new bug favourites direction
- (10:21午前) should call toni
    - about one week or two weeks that ben is on holiday
    - can I work full time
    - same hours
    - proportional pay
    - just for that period
- (10:27午前) next up do it for remove and edit
- (10:57午前) okay the edit pattern was a little complicated
    - you want to see if you are editing to an identical thing with entry_state 0
- (11:26午前) gotta make something to represent prescription_templates as well as decode it in domain
- (11:55午前) I guess now you can work on this
- (12:06午後) remember to do these changes on phone and desktop
- (1:36午後) up to making the prescription template api call match the python
- (2:38午後) you will probably start persona 4 soon
- (4:02午後) python problem with add_prescription_template query













## (2024/07/12 8:26午前)
- (8:26午前) how do I do this, hmmm?
    - okay first make the changes to the indications table
    - now make the elm page and get it working
- (8:43午前) actually now I have to do all the python
- (9:28午前) okay on to the next big thing
- (9:30午前) I'll make a script line tables and a favourite scripts table
- (10:47午前) I am stuck
- (10:50午前) maybe I'll call it a script template
    - it needs a list of prescription items lines
    - a nurse
    - a name
    - an id
- (11:00午前) maybe it can be a list
- (11:26午前) need a new ticket to add entry_state=1 to the get queries for indications, products and treatment areas
- (1:24午後) back to designing this json
- (2:12午後) maybe now think about the routes
    - add_prescription_template
    - get_prescription_templates
    - remove_prescription_template
    - edit_prescription_template
- (3:14午後) you also need to make an event table for this
- (3:42午後) gotta also add the foreign key relation for nurse id
- (3:54午後) next thing you have to do is make it so add_prescription_template adds to the prescription_table_event table
- (3:59午後) up to prescription_templates.py line 46, you are making it so adding also creates an event, that's what you are up to

## (2024/07/11 7:57午前)
- (8:11午前) starting by entering a maximum number of items
- (9:11午前) it looks like treatment areas and indications are one trick ponies
- (9:17午前) you are going to have to do this
    - you will have to change the treatment area table so that there is an updated at and presumably created at
- (9:18午前) also need to do some smoke and sanity testing
- (9:47午前) first up, add created_at and updated_at to treatment_area
- (10:02午前) next up you want to have a get request that gets the treatment areas in order
- (10:07午前) probably want to look through the release candidate changes as well
- (10:51午前) need to add entry_state as well, need to see how this was done with product
- (1:13午後) getting an error now
- (1:41午後) okay, edit isn't working as expected
- (1:49午後) editing seems to be working but it doesn't clear edit
- (1:51午後) Everything seems to be working
    - next up you need to enforce uniqueness
- (2:02午後) you should change how errors and validation work
- (2:57午後) you gotta do the switch thing with both treatment area and product
- (3:03午後) okay work out this switch rule logic then apply it to both products and treatment areas
    - next up you need to do this for product, then create the one for indication
- (4:04午後) done that, you are up to edit_indication now
    - after that it's the product groups


## (2024/07/10 8:24午前)
- (8:24午前) Let's try and finish this as swiftly as possible, then move on to treatment areas, then indications
    - will probably have to reread last week's scratch to fully tie all loose ends
- (9:02午前) there's only four errors that need to be handled it looks like
- (9:48午前) Need to add two more conditions to ensure that the rule name and description are unique
    - (line 2111 of EditRules.elm)
- (11:54午前) it looks like you just need to make the errors display now
    - also pretty sure you need to redo them with other inputs
- (12:36午後) things are starting to look good here
    - getting the desired behaviour gradually
- (12:41午後) treatment areas should be unique
    - you also want to make the plus button disappear if there are any errors
- (12:45午後) since you are storing validate view model you probably don't need it
- (1:01午後) the auto entry for rule name and description isn't working
- (1:09午後) need to go through everything that sets the name and description and revalidate it
- (2:11午後) all of these seem to be working now, now next step make it hide the + and don't rerun the function
- (2:17午後) you also need to make sure edit is working just as expected
- (2:24午後) you have to make these errors clear at the right time now
- (2:38午後) maybe now you can work on the more specific errors
    - for example now you have treatmentAreaNotSelected and volumeNotSelected
- (2:52午後) when you select anything you want not having that thing to no longer be an error
- (2:54午後) also, you want to make



















## (2024/07/05 8:13午前)
- (8:13午前) start by getting uniqueness working for rule name and description
    - then do the same for apply rules
- (8:40午前) right now the error is showing no matter what
- (9:32午前) it's lagging in a weird way
    - it's still lagging
    - you need to do it better
        - also do this for the other ruletypes
- (1:02午後) now just do it for treatment area and volume
- (2:44午後) rewrite validate view model to handle every kind of error
    - going to split it up to validate each kind of rule separately
- (3:47午後) you are up to working on viewModelValidation2 (space s then search 2, in EditRules.elm)
 - or go to line 2162
    - make volumeNotEntered just another volume validation error
        - these don't all have to display






## (2024/07/04 8:09午前)
- (8:09午前) okay the first thing you will do is make remove and add accomodate entry states, after that you will deal with the entry tables
- (8:41午前) it looks like the remove event is there any working
    - now just the edit
- (8:42午前) it looks like editing the products works perfectly too
- (8:46午前) I want to add an error condition where you can't add something with the same name
- (9:33午前) next up you want to add a rule event table
    - let's make a new ticket for this
- (10:00午前) okay made the table, next up you will start using it
    - ADD_RULE, REMOVE_RULE and EDIT_RULE events
- (10:51午前) you should check for uniqueness on the front end
    - this is too hard with the rule model
- (11:08午前) add the product_rule_events and product_category_rule_entry tables
    - you are up to adding the events for product_rule, add them to remove and edit product rule
        - then do the same to category, then test it all
- (12:07午後) found a new case, where edit something to be something old
    - think about how you want to handle the case
- (12:44午後) going to add a 'switch_rule' event to handle the edit edge case
    - new bug found when editing max_prescription_rules
- (1:32午後) now to implement switch for product_rule, category_rule and product
- (2:00午後) you *do* need to check duplicates
    - okay check for duplicates
        - maybe duplicate names and descriptions for rules
        - then think about product rules and category rules
        - okay maybe it doesn't have to be a part of validate viewModel
            - it can be validate
- (2:53午後) you gotta run these validate functions when it's automatically generated
- (3:46午後) you did it on submitting a name, but you should actually be doing it on input change
    - this was a mistake
    - no, this is right
- (3:58午後) up to "UpdateViewModelMetadata" on line 1045 of EditProducts.elm
    - add this new validation back into viewModelValidation
 















## (2024/07/03 8:01午前)
- (8:12午前) just handled the update method for entering a product name
    - next up is to start creating "viewAddProduct"
    - while you do this, also get the errors displaying
- (8:25午前) Edit rules and apply rules aren't pulling in for some reason
- (9:16午前) migration down for m51
    - then come back to these products
        - with products you are up to validateViewModel
- (10:57午前) okay all the rule changes have been merged in and the rules are pulling in!!!
    - now back to validateViewModel
- (11:37午前) okay now to add the add button
- (11:55午前) let's get this working but there are more input errors
    - like what if the name is the same as an existing product
- (12:36午後) next up remove product
- (12:45午後) next up edit products
    - you want to look at how it's done in rules and create a similar interface
    - you also want to add display server errors to rules
    - you should also do the same thing with server errors in products
    - now you should probably display the updated errors
        - also need to do a route to update the product
- (2:44午後) everything seems to be done
    - maybe you want to add a product event table
    - then a rule event table
- (3:51午後) now you want to add events for removing and editing
    - you need to add the events for removing and editing
    - AND you want to make removing and adding handle entry_state












## (2024/06/28 8:43午前)
- the way it works for a category is you can't have more than x lines from that category
- let's implement that rule and then get back
- (11:27午前) now you want to make it display errors
    - next you want to make it possible to apply the rules and for the rules to work
- (11:47午前) see how the maximums work now
- (12:51午後) okay you want to take in a list of maximum rules and a list of prescription items and see if any are broken
- (3:32午後) back to working on the edit products interface, start working on viewAddProduct
- (3:39午後) up to the view model
    - (3:51午後) you need to handle the update method for the searchboxes for categories and units of measure
        - then after that handle the view?
        - handled the updates for the search boxes, next up need to handle the update method for entering a product name
            - also the viewAddProduct
- (4:00午後) don't forget to display the errors



## (2024/06/27 8:21午前)
- (8:21午前) I think I want to change "validating volume" to "validating application"
    - after this test
    - after this with Ben's help have a look at the Doctor's portal
    - next ticket will be implementing the max number of prescription items rule, need to talk to ben about this
        - current behaviour is not replicable
- what to do if you delete a rule and it's linked, probably should give an error
    - yeah you can do this visually without touching the database
- slightly weird behaviours
- next up you need to call Toni, what do you ask her?
    - max prescription items, how should the behaviour work
        - if it's for a product it means you can't have more than a specified number but what about category
        - three interpretations
            - for any product in that category, you can't have more than a specified number of that product
            - you can't have more than a specified number of products from a category
            - you can't have more than a specified number of types of products from a category
- Now you're adding a products interface
    - a product has a name, a category and a unit of id
- you want to get all the units of measure with id
    - okay add a units of measure to domain along with a decoder and an end point to get them all
- maybe create cmd and the task
    - no create the type and decoder first
- you may not need unit of measure after all
    - no you do need it
- (2:11午後) plan
    - viewProductLine function
    - then process gotData, and stick everything in the model
        - see if you can get a line of products displaying
- (2:56午後) you need to replicate your other changes on mobile
    - let's do it now
- (3:53午後) next up (first up tomorrow you are going to create two new fields on the products table, created_at and updated_at)
    - after that add order by updated_at to the query
        - make it work the same way the others are
    - then start to add the viewaddproduct stuff
    - you also want a validateAddProduct function that takes in the productToAdd and validates it, for the name to be valid it needs to not be blank nor match an existing product name







## (2024/06/26 8:02午前)
- Okay, need to add the rule type and implement the UI
- gotta get my bearings
- you want to make it so the direction rule has a default name and description, then you want to go to the apply rule interface
- you need to ask Ben which products and categories require these things
- now find out how rules are applied and do the UI changes so that something different happens if it needs a direction
- you need to make the product rules show first if one has updated first
- remember to also do this changes in the phone view in SelectPrescriptionItems.elm
- you need to change the constraints on the favourite prescription item table
- this is a problem that has something to do with types
- this fail only occurs when there is a direction
- (12:44午後) thinking about how to implement directions, they have metadata, I think a new field is in order
    - instruction
- (2:36午後) looks like the database is good now
    - just need to reimplement the ui
- (3:04午後) you want to set the application depending on things
- (3:42午後) what if I made validating volume into validating application?
- (4:00午後) seems to be working need to test it






## (2024/06/21 9:57午前)
- (12:51午後) okay, it's finally loading favourites again!!!!!
    - I'm really happy about this
    - now you need to get add and remove favourites working similarly
- (1:06午後) okay, next up get add and remove working nicely
- (1:56午後) awesome you can add them, next up remove!!!
- (1:57午後) you should be handling the event table too
    - you can delete favourites too!!!
- (2:04午後) okay and now you've done stuff with the event tables, next up slowly go through SelectPrescriptionItems.elm and see if there's any mess left to do with direction
    - after that you can start adding the rules
- (2:31午後) gone through the thing, now can add the rules
    - okay a new ruletype 
        "Direction instead of Volume"
         - with no data


```sql
ALTER TABLE favourite_prescription_item
DROP COLUMN product_id;
ALTER TABLE favourite_prescription_item
DROP COLUMN indication_id;
ALTER TABLE favourite_prescription_item
DROP COLUMN treatment_area_id ;
ALTER TABLE favourite_prescription_item
DROP COLUMN volume;
    
```

```sql

INSERT INTO rule_type (rule_type_id, rule_type_name)
VALUES
    ('a5725423-8f16-49be-b696-832730c8fba8', 'DIRECTION_INSTEAD_OF_VOLUME'),
    
```




```sql

SELECT *
FROM favourite_prescription_item
WHERE favourite_prescription_item_details-> 'application' IS NOT NULL;



SELECT *
FROM favourite_prescription_item
WHERE JSON_EXTRACT(application, '$.application') IS NOT NULL;
```
```sql
UPDATE favourite_prescription_item
SET favourite_prescription_item_details= jsonb_set(
                        favourite_prescription_item_details,
                        '{volume}',
                        to_jsonb((favourite_prescription_item_details->>'volume')::int || '.0')
                      );
```


## (2024/06/20 8:42午前)
- (10:05午前) ask Ben about version numbers
- (10:36午前) think about the damage and how to deal with it
- (10:41午前) now change what a favourite is
- (2:28午後) next up you want to add repeats
    - you have the code in migration m51
- (4:03午後) up to working with nurse.py
    - getting the shape of the data right







## (2024/06/19 8:01午前)
- first things first, let's set up that ipad and get it so you so can look at the port
- (1:51午後) now need some functions that convert things
- (3:59午後) obviously you are up to the queries


-- add favourite_prescription_item_details jsonb)
```sql
ALTER TABLE favourite_prescription_item
ADD COLUMN favourite_prescription_item_details jsonb 
```
```
UPDATE favourite_prescription_item
SET favourite_prescription_item_details = json_build_object(
    'product_id', product_id,
    'indication_id', indication_id,
    'treatment_area_id', treatment_area_id,
    'volume', volume
)
WHERE favourite_prescription_item_details IS NULL;


ALTER TABLE favourite_prescription_item
ALTER COLUMN favourite_prescription_item_details
SET NOT NULL;
```
-- add version number ( do we need this )
```sql
ALTER TABLE favourite_prescription_item
ADD COLUMN version_number integer NOT NULL DEFAULT 2;

UPDATE favourite_prescription_item
SET version_number = 1;
```

-- add favourite_prescription_item_category_id

-- remove not null constraints from product_id, indication_id, volume and treatment_area_id
```sql
ALTER TABLE favourite_prescription_item
ALTER COLUMN product_id DROP NOT NULL;
ALTER TABLE favourite_prescription_item
ALTER COLUMN indication_id DROP NOT NULL;
ALTER TABLE favourite_prescription_item
ALTER COLUMN treatment_area_id DROP NOT NULL;
ALTER TABLE favourite_prescription_item
ALTER COLUMN volume DROP NOT NULL;
    
```

-- add favourite_prescription_item_category table

-- add fk to nurse 

```
type PrescriptionItemLine
    = PrescriptionItemLineWithVolume PrescriptionItemLineWithVolumeData
    | PrescriptionItemLineWithDirection PrescriptionItemLineWithDirectionData


type alias PrescriptionItemLineWithVolumeData =
    { product : Product
    , treatmentArea : TreatmentArea
    , indication : Indication
    , volume : Float
    , repeats : Int
    }


type alias PrescriptionItemLineWithDirectionData =
    { product : Product
    , treatmentArea : TreatmentArea
    , indication : Indication
    , direction : String
    , repeats : Int
    }


type Application
    = Volume Domain.Volume
    | Direction String


type alias ViewModelItemLine =
    { id : Int
    , product : Product
    , treatmentArea : TreatmentArea
    , indication : Indication
    , application : Application
    , repeats : Int
    }
```
## (2024/06/14 8:10午前)
- okay, you are now going to add those if statements to python
    - to all the add and edit routes for adding rules
    - you have six things to add this logic to
        - add rule, edit rule, add product rule, edit product rule
        - actually it doesn't need to be added to edit rule
- you also need to add the right constraint to the various updated_at
    - you also need to add updated_at and created_at to product_rule and product_category_rule
- update isn't working somehow
- editing and updating simply does not work, let's walk through it
- adding an editing interface would be good
- okay first fix the main problem and then work on the papercuts
- now you want to get the created_at and update_at constraints working (and apply the changes in a migration)
    - after that you want to add both of these fields to product_rule and product_category_rule
- now I have to add updated_at and created_at to two tables
- let's test add, remove and edit
- okay things are working really well
    - now you want to check that autoselect error
- you should make it when adding a rule (not just applying a rule) there is a form validation error when the rule is identical to another
- it looks like next you can actually do the directions thing, you'll want to build on what you've done with rules
- I'm going to make a branch and merge ben's changes into it
- ben really likes a flat structure
- I feel like I should change something
- maybe you should add the rule now?
    - it's direction

## (2024/06/13 8:21午前)
- Next up select rule and select category
- next up make it so the plus button shows, when everything is filled
    - then maybe start to get it working
- maybe a part of it being valid is not being the same
- a constraint is that you can have only one of a type
- you need to add updated at and created at to product and category rule
- it's fine and it's adding, you should make it that the fields clear on add
- you've added two rules to the category biostimulation
    - lets make the fields clear and then we'll test the category (another biostimulation) and product
- 3 applied rules for biostimulation and transemic acid need to be deleted
- I guess next up remove rule and then edit
- you need to add entry_states to continue
- they both already have entry states
- you want to edit then you want to fix the way entry states work, then you want to get things in the right order
- up to UpdateRule in the update function
- weird bugs with update
    - I think the cream is fake news
- (3:54午後) one thing that you can start with is sorting out the entry states, what happens when you add something that exists but the entry state is 0
    - this should happen on add and on edit
        - this *might* help with your problem with update
        - also you can refactor the python since you reuse code a lot



## (2024/06/12 7:59午前)
- Good morning!
- (8:11午前) I think that I'll first finish this interface then fix the entry state thing (adding something that is deleted won't work now)
- (8:42午前) you can probably change rule so that all the data that is passed in is a record
- (10:41午前) okay now you have the routes now you have to make the Tasks in Api
    - no you don't you already have it?
- (10:52午前) okay, get all product ids and product category ids and use those to get the specific rules
    - okay you can do this
- (11:47午前) you are going to have to add "updated_at" to both the ProductRuleJoinTable and the ProductCategoryRuleJoinTable
    - come back to this later
- (11:48午前) let's start with views for each
    - not sure if you should translate this
- (12:28午後) when you select a tab, the init msgs don't work
- (12:55午後) solved that problem neatly!!!
- (12:55午後) I need snacks in the house, apricots would be great
- (1:35午後) Next up you want to add the drop boxes and get them working


## (2024/06/07 8:33午前)
- let's start by making it autofill when you select and indication
    - after that when you enter a volume + treatment area
    - after that figure out how to make the description box big
    - after that make the plus button show when everything is filled
        - after that get it working
- it would be nice to make the searchbox labels match the text input labels
- next up you will get the plus button to show and then get it actually working
- (10:19午前) you are up to validating the view model
- need to alias the components thing to view model and add errors to viewaddrule
- (10:59午前) you are actually now up to getting the add rule button here working
- (11:48午前) if you want to be able to remove them then they need ids
- (12:19午後) adding a volume amount that ends in 0 doesn't seem to work
- (2:27午後) you need to handle remove to handle entry_states
- (2:37午後) editing works!!!
- (2:39午後) now you have to work with entry_states
    - I think you have to change the unique constraint to include entry_state as well
- (2:57午後) now you add entry_states to everything
    - lets see what tables are there
        - rules
        - rule types
        - product_rule
        - category_rule
- (3:26午後) now you have to change the queries that get rules to only get them when the entry state is 1 and the remove one to only change the entry state
- (3:35午後) now it looks like you only have to make it so that you can apply a rule
- (3:44午後) thinking out loud as to what's needed for apply rules
    - product or category
    - specified product or category (for products filer by catgory)
    - after this the rule
- (3:57午後) for the model, what do you need?
    - ruleToAdd (product or category)
    - filter by category
    - product
    - category
    - rule
- (3:58午後) so you need a list of products, categories and rules


## (2024/06/06 8:34午前)
- Okay I want to get all the rules and stick them in the model
- okay first make the list nice, then start to build up a view model to edit the list
- let's see they select the rule type, then the data fields then the name and description
- it's sending "change index 0" no matter what I do
- okay the impossible problem has been solved
- next up add the volume field and then make it when both of them are filled the name and description show (and are automatically entered)
- next up process update volume then add the fields for name and description
- (3:58午後) you are up to adding a field for the name and the description if the rest has been filled



## (2024/06/05 8:08午前)
- (8:17午前) another thing that you need to do is make it so the + button only shows when everything is entered (including the rule and description)
- (8:23午前) you also wanted to add the default rule names and descriptions too
    - if it has everything it will be a string that takes the necessary info otherwise it will be an empty string, or even Nothing
- (8:30午前) okay a bit disorganised but a todo list
    - make it so when all details are filled there is an automatic name and description
    - make the + button only appear when the rule name and description are there
    - create and handle the msg for changing the rule name and the description
- (8:35午前) hmmm... the rules are all gone
    - and therefore they are not working
    - this is sad!!!
- (8:46午前) okay getting the migrations working will be the first mission
- (8:52午前) I definitely need to ask Ben all about this asap
- (9:42午前) a lot of big changes you are going to change this to use UUID
- (11:55午前) okay after lunch you should go back to the rules CRUD, that was going well
- (2:33午後) remember the following
        window.onmessage( { data :
- (2:43午後) you might have to rethink this, rules and rule descriptions apply to rules and not product rule and product category rule
    - this is not obvious to the end users who may give a name or description according to the specific product
        - I want to think about the whole applying the same rule to multiple products or categories, how is that handled?
            - it is absolutely possible, I wonder how it would be handled here
- (2:49午後) you need to rethink this, you have rule types, generic rules and active rules
    - make two subtabs now, one to add rule, one to apply them
- (4:00午後) just created sub tabs, now I need to implement them
    - need to create a new generic rule type in domain









## (2024/05/30 8:41午前)
- okay now to figure out how to get the routes working
    - you need to send some json data representing a rule to a route called "add rule"
- not sure if you need two separate routes for product rule and product category rule
    - you probably do
- okay you have to change Rule 
- (11:04午前) in the process of adding Metadata to the rule (that is; the name and the description)
- 951618c7
- (4:01午後) go to SuperUser/ManagePrescriptionItems.elm line 236 this is where you were up to
    - you want to finish implementing rule name and description
    - you haven't processed the message and you haven't done it for category in the ui

## (2024/05/29 9:00午前)
- Okay, you've fixed the problems from yesterday and you've also merged in the new main-onion into the current branch you are working on
- why is it still in the loading stage?
- okay next up make it so that it displays the rule type info
- next up is add select volume
    - maybe indication first since it's similar
- now add volume, then make the add button?
- maybe make the add button visually and then implement the category functionality
- you need to look at how you validated your volume in the past and do the same thing
- now implement the display and after that get everything working for product category
- next up show an add button if the form is filled
- need to organise to pick up the ipad from North Sydney
- maybe think about how you want to handle errors
- need to make it so clearing the volume error happens


## (2024/05/28 8:07午前)
- so far the filter by category and product seems to be working as expected
- think about rule type, should it show up after product is selected? 
    - this makes sense to me
- gonna fix the category problem
    - going to make everything load in a predictable order just like in ManageTreatmentItems.elm
- the only unique things that nurses do are getting favourites and products
    - you also need to get favourites
- going to have to turn getNurseFavourites and getNurseProducts into a task
    - after that see if we can use it in an if statement
- figure out what add favourites and refresh favourites are
- now sort out the merge conflicts with the rules
- you need to readd quick select favourites to SelectPrescriptionItems.elm
    - you also need to make it so treatment areas don't load initially

## (2024/05/24 10:26午前)
- now all the rules are displaying nicely
- maybe create components to select a rule
- maybe you should make a component, then you can handle the update also
- after the scope is chosen, the product/category dropbox shows as well as the rule typedrop box
- search boxes to add
    - product
    - category
    - ruletype
    - indication
    - volume
    - treament area
- now you have to get the category search box working
    - connect it to the product so it actually filters products, also get rid of nones
    - maybe have a look at SelectPrescriptionItems.elm first
- tomorrow we need to fill out that form and also get vaccinated


## (2024/05/23 9:59午前)
- move everything for this ticket to a new module called ManagePrescriptionItems.elm
- figure out how to use tasks to make things go in order
    - if it works you can replicate this for SelectPrescriptionItems.elm
- think of a nice english way to describe the rules
    - at the moment there's really two rule types max volume for a product or product category on a treatment area
    - and autoselect
- up to making the rules look all nice, next you will have to add the ability to add, then edit, then delete them

## (2024/05/22 8:26午前)
- ask ben about these two different pull requests
 - one has a backwards merge and the other doesn't
- after this maybe you can start working on the interface to add new rules
    - also ask if you can add him as a refence on your tenancy form and about next week
- first up work on two bugs after that make an interface
- move the error messages to the top on mobile and change it to a wrappedRow
- so both those bugs are done now, next up is for me to work on the crud
- I'm going to need help from ben as to where in the interface and where in the code to put this
- okay now you just need to do it, you need to get the rules, hmm...
- make documents for each of these
- you are in the midst of activity
    - in PrescriptionActivityByClinic, see if you can implement the new components that you made
    - up to line 106 in this file

```
type Tab
    = GlobalPatientLookupTab GlobalPatientLookup.Model
    | PrescriptionsByClinic
    | ManageDoctor
    | PrescriptionActivityByClinic
    | ManageClinics
    | ManageRules
```
## (2024/05/17 8:07午前)
- Okay, now do you have to create the rules?
    - I guess you do, you also need to put them in the system
- This time the rule type will be 1 (max volume for treatment area) and you will need a treatment_area_id and a max volume in the json
- connect rules 11, 12, 14,15 with the filler type
- we gotta enforce this being done AFTER the treatment areas are loaded
- now we need to run the rules, it's the same place where the volume validation happens
- I see autoselect indication doesn't actually add it
- need to test the below volume validation rules (under 2024/06/16)
- at the moment, you can add more than six different types of products
- looks like the rules are
    - up to five different IV products
    - up to six different "cosmetic use" products
- What I think I am up to is figuring out the max prescription items rule
    - you could implement it for IV products
        - try to explain the problem with "cosmetic use" products
    - then work on an interface to create rules


        INSERT INTO rule (rule_type_id, name, description, data)
        VALUES (
            1,
            'Max Volume of 4ml for "Cheeks" treatment area',
            'Ensures a maximum volume of 4ml on the "Cheeks" treatment area when specified product or product category is selected',
            '{"max_volume": 4, "treatment_area_id": 2}'
        );

## (2024/05/16 7:59午前)
- I want to make the first part of the selected prescription item line longer and the repeats and volume shorter
- you can get the rules after you've gotten the indications, products and product categories provided you have all of them and don't already have rules
- maybe you should have product category rules separate
- now process the rules when you select a product or category
- you also need to make it so that a product
- now you are implementing the rest of the rules
- you are going to need a new rule or edit the existing maxVolume rule to apply for treatment areas
- rules you will need, MoreThan
- max volume will become max volume for a treatment area

- 
UPDATE rule_type SET rule_type_name = 'MAX_VOLUME_FOR_TREATMENT_AREA' WHERE rule_type_name = 'MAX_VOLUME';

- (4:01午後) you are up to the Rules.elm file, you are changing max_volume to maxVolumeForTreatmentArea
    - need to figure out how to get the treatment area from the id (probably just pass something in)


```
type VolumeValidationError
    = LessThanZero
    | Over4mlFillerUsedOnCheeks
    | Over4mlFillerUsedOnChin
    | Over4mlFillerUsedOnJawline
    | Over1mlFillerUsedOnTearTrough
    | ContainsInvalidCharacters
    | UnknownVolumeValidationError



type SelectedPrescriptionItemsValidationError
    = UnknownSelectedPrescriptionItemsError
    | MoreThanTwelveCosmeticsItemsSelected
    | MoreThanFiveIVItemsSelected
```


    
## (2024/05/15 8:44午前)
- if a product has no treatment areas that the nurse has permissions to show, it shouldn't show
    - ask if indication has anything to do with it
    - ask Ben to test it, possibly in front of you, with data that he is familar with
    - fix the behaviour so that products don't show if there are no treatment areas for the product that the nurse has permissions to use
        - unless there is something higher priority
- okay it's good, do a pull request and then switch to autoselect indications
- thinking about adding a way of adding rules
    - there are max volumes, autoselect
        - presumably these are for categories and products
- thinking about rules
- now I'll add the rules in the database right away
- (2:56午後) okay now to a slightly more fun part, the python and the elm
- (2:56午後) when do you get the rules? I am guessing it a left join?
- (3:18午後) how and when do we get the rules?
- (3:23午後) okay you should just get the rules and implement the rules, with a "got_rules" kind of thing
    - you can do it when you've got the products and the categories respectively
- (3:27午後) you need to add python to get the rules given the product ids and given the products
- (3:56午後) next up you have to access the python with elm (and therefore test the python)
    - you pass in a list of product or product category ids and expect something that can be Decodes into a rule
- (4:00午後) maybe move the working for this ticket into a new document (the sql code blocks seem to be intense on the cpu)


```
        select * from product_rule
            left join product on product.product_id = product_rule.product_id
            left join rule on rule.rule_id = product_rule.rule_id
            left join rule_type on rule.rule_type_id = rule_type.rule_type_id
            where product.entry_state = 1
            order by product.product_id desc;

        select * from product_category_rule
            left join product_category on product_category.product_category_id = product_category_rule.product_category_id
            left join rule on rule.rule_id = product_category_rule.rule_id
            left join rule_type on rule.rule_type_id = rule_type.rule_type_id
            order by product_category.product_category_id desc;
```



### thinking out loud about rules
- there's one where you select a product or product category and the indication is autoselected
- there's max number of prescription items
- maxVolume
- we'll start with it not being strict and we'll make it strict (the json that is)

### plan for database
- RuleType
    - pk name
        - (max_volume, autoselect, max_prescription_items)
- Rule
    - pk rule_id
    - RuleType
    - Data

- ProductRule
    - fk product_id
    - fk rule_id

- ProductCategoryRule
    - fk product_category_id
    - fk rule_id


```sql
CREATE TABLE rule_type (
    rule_type_id SERIAL PRIMARY KEY,
    rule_type_name VARCHAR (50) UNIQUE NOT NULL,
    created_at TIMESTAMP NOT NULL,
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
)

CREATE TABLE [IF NOT EXISTS] rule (
    rule_id SERIAL PRIMARY KEY,
    rule_type_id INT NOT NULL,
    data JSONB NOT NULL,
    name VARCHAR (50) UNIQUE NOT NULL,
    description VARCHAR (200) UNIQUE NOT NULL,
    created_at TIMESTAMP NOT NULL
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP
    CONSTRAINT fk_rule_type
        FOREIGN KEY rule_type_id
        REFERENCES rule_type(rule_type_id)
)

CREATE TABLE [IF NOT EXISTS] product_rule (
    product_rule_id SERIAL PRIMARY KEY,
    product_id INT NOT NULL,
    rule_id INT NOT NULL,
    CONSTRAINT fk_product_id
    FOREIGN KEY product_id
        REFERENCES product(product_id)
    CONSTRAINT fk_rule_id
    FOREIGN KEY rule_id
            REFERENCES rule(rule_id)
    CONSTRAINT unique_product_rule UNIQUE (product_id, rule_id)
)

CREATE TABLE [IF NOT EXISTS] product_category_rule (
    product_category_rule_id SERIAL PRIMARY KEY,
    product_category_id INT NOT NULL,
    rule_id INT NOT NULL,
    CONSTRAINT fk_product_category_id
    FOREIGN KEY product_category_id
        REFERENCES product_category(product_category_id)
    CONSTRAINT fk_rule_id
    FOREIGN KEY rule_id
        REFERENCES rule(rule_id)
    CONSTRAINT unique_product_category_rule UNIQUE (product_category_id, rule_id)
)
    
```

### attempt 2
```sql
CREATE TABLE rule_type (
    rule_type_id SERIAL PRIMARY KEY,
    rule_type_name VARCHAR (50) UNIQUE NOT NULL,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP 
)

CREATE TABLE rule (
    rule_id SERIAL PRIMARY KEY,
    rule_type_id INT NOT NULL,
    data JSONB NOT NULL,
    name VARCHAR (50) UNIQUE NOT NULL,
    description VARCHAR (200) UNIQUE NOT NULL,
    created_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    updated_at TIMESTAMP NOT NULL DEFAULT CURRENT_TIMESTAMP,
    CONSTRAINT fk_rule_type
        FOREIGN KEY (rule_type_id)
        REFERENCES rule_type(rule_type_id)
)

CREATE TABLE product_rule (
    product_rule_id SERIAL PRIMARY KEY,
    product_id INT NOT NULL,
    rule_id INT NOT NULL,
    CONSTRAINT fk_product_id
    FOREIGN KEY (product_id)
        REFERENCES product(product_id),
    CONSTRAINT fk_rule_id
    FOREIGN KEY (rule_id)
            REFERENCES rule(rule_id),
    CONSTRAINT unique_product_rule UNIQUE (product_id, rule_id)
)

CREATE TABLE product_category_rule (
    product_category_rule_id SERIAL PRIMARY KEY,
    product_category_id INT NOT NULL,
    rule_id INT NOT NULL,
    CONSTRAINT fk_product_category_id
    FOREIGN KEY (product_category_id)
        REFERENCES product_category(product_category_id),
    CONSTRAINT fk_rule_id
    FOREIGN KEY (rule_id)
        REFERENCES rule(rule_id),
    CONSTRAINT unique_product_category_rule UNIQUE (product_category_id, rule_id)
)
    
```


```postrgesql
INSERT INTO product_category_rule (product_category_id, rule_id)
VALUES (
    10,
    3
    
);
INSERT INTO product_category_rule (product_category_id, rule_id)
VALUES (
    6,
    3
    
);
INSERT INTO product_category_rule (product_category_id, rule_id)
VALUES (
    8,
    3
    
);
INSERT INTO product_category_rule (product_category_id, rule_id)
VALUES (
    7,
    3
    
);
INSERT INTO product_category_rule (product_category_id, rule_id)
VALUES (
    13,
    3
    
);
INSERT INTO product_category_rule (product_category_id, rule_id)
VALUES (
    20,
    3
    
);
```
```sql

INSERT INTO rule_type (rule_type_name)
VALUES
    ('MAX_VOLUME'),
    ('AUTOSELECT'),
    ('MAX_PRESCRIPTION_ITEMS');    


    



INSERT INTO rule (rule_type_id, name, description, data)
VALUES (
    2,
    'Autoselect "Cosmetic Use" indication',
    'Autoselect "Cosmetic Use" indication when specified product or product category is selected',
    '{"indication_id": 7}'
);

INSERT INTO rule (rule_type_id, name, description, data)
VALUES (
    2,
    'Autoselect "Nutrient Therapy" indication',
    'Autoselect "Nutrient Therapy" indication when specified product or product category is selected',
    '{"indication_id": 8}'
);
INSERT INTO rule (rule_type_id, name, description, data)
VALUES (
    2,
    'Autoselect "Nausea / Vomiting" indication',
    'Autoselect "Nausea / Vomiting" indication when specified product or product category is selected',
    '{"indication_id": 11}'
);
INSERT INTO rule (rule_type_id, name, description, data)
VALUES (
    2,
    'Autoselect "Obesity" indication',
    'Autoselect "Obesity" indication when specified product or product category is selected',
    '{"indication_id": 9}'
);
INSERT INTO rule (rule_type_id, name, description, data)
VALUES (
    2,
    'Autoselect "Ptosis" indication',
    'Autoselect "Ptosis" indication when specified product or product category is selected',
    '{"indication_id": 10}'
);

    
```
(1, 'Autoselect \"Cosmetic Use\" indication', 'Autoselect \"Cosmetic Use\" indication when specified product or product category is selected', '{indication_id: 7}')

## (2024/05/09 8:16午前)
- going to try one more thing, getting rid of read only
- what to do now
    - when you get the products, put them in the search model
    - handle the searchbox message
- now I just need to handle the messages and then work with the view
- remember to do this on mobile as well
- also need to make sure that product categories work
- maybe the selectedFavourite field is no longer necessary
- up to adding got categories to the new thing
- right now clearing the category box doesn't do anything
- let's keep going and see if everything is still working
    - indication and treatment area next
- next up quick select favourites, this will be a little harder
- now you want to clear the boxes when you add a product
- I wanna rename the view products
- next up you want to inline the package
- okay next up you want to make things bigger when the product name is bigger
- you should make it so that the favourites don't show unless there are favourites
- make it so adding a favourite clears the prescription item
- you can definitely do some code reuse here
    - one this is resetting the states of everything
- (4:00午後) categories didn't seem to be pulled on the office prescription side
    - also, the new search dropdowns stretch the phone screen

## (2024/05/08 8:15午前)
- okay, I've increated the cosmetic items to 12
- I think the best thing to do would be to make it so the keyboard pops up
- need to make the remove from favourites easier to see (on the card makes sense)
- make it so that edit is more obvious
- going to make it distinct items
- next up distinct items
- you want to take a list, for each item in the list you want to count how many in that list have that items product id, return true if over a specific amount
- next up you can make the edit button say edit
- next step is to make it only for nurse
- I should have taken screenshots for those tickets
- tomorrow you will finish merging in the add+remove favourites button


- make a new file for the following
```js
          const payload =
        '{"member":{"_id":"12357987893","contactId":"cfe0d2d0-74f3-4242-b805-506b9be5d050","loginEmail":"sashin@allurepacificaesthetics.com","profile":{"nickname":"Ben Tyler","slug":"ben-tyler","profilePhoto":{"id":"","url":"https://lh3.googleusercontent.com/a/AGNmyxZQQiQ34MEQkqSZR9zS6p2LkpAFmfiFC2np8O00=s96-c","height":0,"width":0}},"contactDetails":{"contactId":"cfe0d2d0-74f3-4242-b805-506b9be5d050","firstName":"Ben","lastName":"Tyler","phones":[],"emails":["ben.tyler@allurepacificaesthetics.com"],"addresses":[],"customFields":{}},"activityStatus":"ACTIVE","privacyStatus":"PUBLIC","status":"APPROVED","lastLoginDate":"2023-05-08T02:48:52Z","_createdDate":"2023-03-03T01:11:41Z","_updatedDate":"2023-03-15T03:11:27.390Z"},"licence":"wix_preview_authenticator","secret":"q_hGPysrBswcLMCuFaBYmQ"}';
      app.ports.wixIntergationPort.send(payload);
    };  
```

```js

  app.ports.autofocus.subscribe((id) => {
    setTimeout(()=> {
    let inputfield = document.getElementById(id);
    inputfield.focus();
    console.log("the autofocus port is being run!")
        }
      ,500);
  })
```

## (2024/05/03 10:10午前)
- drop the event sourcing stuff now and just let changes be made
    - it won't work very nicely on the mobile phone interface
-  okay you are going to need an api thing
- need to think about where to get the prescription_items_id
- you need to make an event too
- ask ben if he tested the add_select_items to the doctors portal
    - also finish the pull request
- thinking through going back in time
- can have an int representing the offset, in increases as you go back, decreases as you go forward, if you get to negative it sets it back to 0 (also the button for next doesn't show)
- you should display the day
    - you definitely want to display this
- you have the buttons and a number of days ago displaying but it's not working


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
