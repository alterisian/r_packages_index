R Index
=======

* Goal: Improve the way R users are looking for new packages.

* Implementation: A website written in Ruby On Rails that catalogues the R packages.

* Hosted: http://rindex.herokuapp.com 

* Hashtag: #Rindex see: 

* Dependencies: CRAN Network, Ruby 2.6, Rails 6.x
* Useful: RVM(or Rbenv) for multiple ruby projects.

* Installation
Via the commandline follow these steps:

git clone 
rvm use ruby-2.6.3
rvm gemset create rindex
rvm gemset use rindex
bundle install
(install is optional)
rails s 
(short for rails server)

* This project is developed with a tight time restriction. 
  It is expected to be made available to the public without finishing the roadmap.
  We welcome external contributors and the intention is to release this as open source, under an appropiate license.

* Methodoloy/Approach:

  - This project will import the existing R packages from a CRAN server.

  - It will store them in a database, or ActiveRecord compatible store.

  - It will provide a web interface using Ruby On Rails to alow searching

  - It is anticipated that it would be hosted on a free tier of heroku, 
  this defaults to a postgres database.

* Terminology: 

  - R: A statiscial computing language. More:
  - R Package: A module used by R to import functionality.
  - CRAN: Network of ftp and web servers hosting R Packages.
  - Ruby: A programming language. More: https://www.ruby-lang.org/en/
  - Ruby On Rails: Rails, is a popular, mature MVC framework. More: https://rspec.info
  - RVM: Ruby Version Manager. Provides a way to develop with multiple ruby versions, and gemsets. More: 
  - rspec: automated test coverage. Run on command line with rspec. More: https://rspec.info

* Stakeholder Input

  Create a Ruby application to index all the packages in a CRAN server
  1. Extract some information regarding every package and store it. 
    - You will need to get some info from PACKAGES file 
    - and some other info from DESCRIPTION
  2. Design the business logic needed for storing all the information 
    - models, libs, DB structure...
  3. A task that will run every day at 12pm to index any new package that appeared during the day 
    - (we want to store all the versions of a given package. 
    It means that the package 
      abc_1.2.1.tar.gz could be tomorrow 
      abc_1.3.0.tar.gz, and we want to store version 1.2.1 and 1.3.0
  4. A simple view listing all the packages you have indexed
  5. Tests
  6. Push the code to github
  
* Project Requirements:

 - There should be a way for people to search for R packages.

 - There should be a way for people to import new R packages.
  
  - - The project shall be able to read a CRAN server to obtain a list of all packages.

  * Roadmap

  - Milestone 1:
  - - We can access a package index programmatically
  - - We have a Ruby On Rails server. 
  - - We have a Package model defined.

  - Milestone 2:
  - - We have an initial test around the package index retriever.
  - - The database is populated with some Pacakages.
  - - A user can search for packages.

  - Milestone 3:
  - - There is a runnable rake task to retrieve the packages.
  - - The author details are being saved
  - - We are storing all versions of a package.

  - Milestone 4:
  - - The system is available on heroku for the R programmer to test.
  - - There is a timed rake task at 12pm (German / Spanish time /CEST) to import the packages.

  * Extensions: 

  - Since the primary purpose is to allow search, we could look into dedicated search engines such as solr.
  - Since most representations of a package will not change daily, we can add caching around the elements in use.
  - We need to expect that a particular CRAN server is unavailable, and have secondary server options.  
  - We should be able to export the data, so that others maybe able to build a R Package Index web service easily.

--------------------
* Technical Details.

  rails new --minimal 

  was released in May, and I've not had chance to try it. 
  This project doesn't have requirements for mailing, and user authentication, 
  so I would not use jumpstart template (bootstrap/devise benefit) as I often use. 
  I will add included bootstrap as an extension though, as it does give it a 
  richer interface for people to interact with.
  (See: https://github.com/rails/rails/pull/39282 )

  --------------
  Try the example package url: http://cran.r-project.org/src/contrib/shape_1.4.1.tar.gz
  Unfortunately, not found.

  Action: Try to find a new example that works.
  --------------
  
  add in rspec 

  create a package list fetcher in the lib directory. It could also be perhaps considered a service utility.