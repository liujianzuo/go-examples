# Jon's example web application 

This example web application is written in Go (GoLang).  It will be used as a starting point for any secure web applications that I build. 

### Take it for a spin:
* Run `go build`
* Run `./web`
* Open browser to `http://localhost:8080/auth`
  * notice how it redirects you to https (you will have to set an exception to accept the certificate)
  * when it asks for credentials enter `joe@example.com` and `supersecret`

### It currently does these things:
* Redirects to https if http is used
* When started, it builds/rebuilds a sqlite3 user table with example users and passwords
* Provides a couple of resources (/info and /auth)
  * go to http://localhost:8080/auth
  * enter username: joe@example.com password: supersecret
* Request handlers can be wrapped with Basic authentication checks

### Do Next
* Absorb this:    http://blog.8thlight.com/uncle-bob/2011/09/30/Screaming-Architecture.html
* And this:       http://blog.8thlight.com/uncle-bob/2012/08/13/the-clean-architecture.html
* And then this:  http://manuel.kiessling.net/2012/09/28/applying-the-clean-architecture-to-go-applications/

### It will eventually do these things
* Provide REST resources that:
  * return user data as JSON (from the user table)
  * inserts and updates data in the user table
* An HTML5 Login web page
* An HTML5 "Forgot Password" web page that sends an email with a reset link
* A login monitor that prevents brute force password attacks by blocking account for 20 minutes after 10 invalid passwords are tried
* An HTML5 index page that provides links to REST resources

### Pretty important to have
* Permission and role tables
* A user resource (GET, PUT, POST, DELETE)
* An HTML5 web page to display all users (if user has the right permission)
* An HTML5 web page to edit a user (user can always edit his own user)
* An HTML5 web page to create a user

### Libraries used:
* net/http          
* http://godoc.org/golang.org/x/crypto/bcrypt - for hash/salting passwords
* https://github.com/jmoiron/sqlx - maps rows to objects
* https://github.com/mattes/migrate - handles database migration
* https://github.com/stvp/assert - assertions for testing
* Bootstrap for styling web pages
* Angular JS for browser->server interactions

### I may use these libraries:
* httprouter:         go get -u github.com/julienschmidt/httprouter
* codegansta/negroni: go get -u github.com/codegangsta/negroni
* go-flags:           go get -u github.com/jessevdk/go-flags

### How to recreate the DB using the command-line
migrate -url sqlite3://web.db -path ./migrations reset
migrate -url sqlite3://web.db -path ./migrations up

### Future ideas for startup
* `./web --url 'sqlite3://database.db' --https-cert=https-cert.pem --https-key=https-key.pem`
* create a web.sh script to start it up with the above command
