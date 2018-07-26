# Rails 5.2 'Credentials' and Catch XXII



So the story went somehow like this: I was setting up a production
environment for a Rails 5.2 application  we are just about
to release while it occured to me: Hey! What a great opportunity
to try out this 'credentials' thing that just arrived to Rails!

So I did.

Googled for 'Rails 5.2. credentials', skimmed several tutorials
and thought: Hey! This must be easy! So I deleted secrets.yml
(who needs it anyway ;), ran

`bin/rails credentials:edit`

entered a production DB password, saved, exited Emacs and look!
There are those `config/master.yml` and `credentials.yml.enc`
I read so much about!

Cool. 

so I am opening `config/database.yml` and using my brand new encrypted
credentials like:

  password: <%= Rails.application.credentials.production.db.password %>

and running the console ... and then ... :(

    (erb):20:in `<main>': Cannot load `Rails.application.database_configuration`:                                                     
    undefined method `db' for nil:NilClass (Method)

well that's easy, I just messed up something in the credentials file so I just edit the credentials
to fix it:

    bin/rails credentials:edit
    
and 

    (erb):20:in `<main>': Cannot load `Rails.application.database_configuration`: (NoMethodError)
    undefined method `db' for nil:NilClass
    
Oh wait...    

----
    
TL;DR `rails credentials:edit` tries to connect to the database
so if you are using Rails credentials in your `database.yml`
    
