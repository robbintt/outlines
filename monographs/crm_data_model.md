### Simple Data Model for CRM


#### Types of data

1. `Customer Organization`
    - Data Fields
        - `Date first entered into this table`
        - `Organization Name`
        - `Active?`
        - `Definite end date?`
        - `Over 10k future value?`
        - `Missed payment?`
        - `History of late payment?`
        - `Did we ever do a project with them?`
        - `Do we want to work with them again?`
2. `Contact` @ `Customer Organization`
    - Data Fields
        - `Customer Organization`
        - `Date first entered into this table`
        - `Name`
        - `Job Role`
        - `Office Phone Number`
        - `Cell Phone Number`
        - `Supervisor Name`
        - `Supervisor Job Role`
        - `Email`
        - `Notes`
3. `Interaction` with `Contact` at `Customer Organization`
    - Data Fields
        - `Customer Organization`
        - `Contact`
        - `Date of Interaction` 
        - `Time of Interaction`
        - `Type of Interaction (phone, email, etc.)`
        - `Purpose`
        - `Notes`
4. `New Lead` with `Contact` at `Customer Organization`
    - Data Fields
        - `Contact`
        - `Customer Organization`
        - `Date`
        - `Source of Client (advertising, referral, website, etc.)`
        - `Referred By (optional)`
        - `Estimated Project Value`
        - `Estimated Client Long-Term Value`
        - `Contact` (implies link to `Customer Organization`)
        - `Lead Status` follows a branching control flow
            1. `Open or Outstanding Lead`
            2. `Won Lead` or `Dead Lead`


#### Using a spreadsheet

A sheet for each type, a row for each entry.  

This can easily be exported as CSV and imported to an ORM data model.

Filters can easily be written on the fly for simple analysis in the meantime.


