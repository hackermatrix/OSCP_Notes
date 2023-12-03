# GitHub Recon

### Specific Org search:

* "Org\_name" password
* "org\_name" key
* "org\_name" api
* "org\_name" “filename:vim\_settings.xml”
* "org\_name" "Authorization: Bearer"
* "org\_name" "Language: PHP"

### Sensitive Files search:

* filename:manifest.xml
* filename:travis.yml
* filename:vim\_settings.xml
* filename:database
* filename:secrets.yml password
* filename:.esmtprc password
* filename:passwd path:etc
* filename:dbeaver-data-sources.xml
* path:sites databases password
* filename:config.php dbpasswd

### Specific Language based search:

* language:python username
* language:php username
* language:sql username
* language:html password
* language:perl password
* language:shell username
* language:java api
* HOMEBREW\_GITHUB\_API\_TOKEN language:shell

### API keys, Token & Hard-Coded Password search:

* SecretKey / Secrect\_key / skey
* privatekey / private\_key / pkey
* user\_secret / userSecret
* admin\_passwd / adminpasswd / adminPass etc
* “api keys”
* authorization\_bearer:
* oauth
* auth
* authentication
* client\_secret
* api\_token:
* “api token”
* client\_id
* password
* user\_password
* user\_pass
* passcode
* client\_secret
* secret
* password hash
* OTP
* user auth

### Username search:

* user:name (user:admin)
* org:name (org:google type:users)
* in:login ( in:login)
* in:name ( in:name)
* fullname:firstname lastname (fullname: )
* in:email (data in:email)

### GitHub Dorks for Finding Information using Dates:

* created:<2012–04–05
* created:>=2011–06–12
* created:2016–02–07 location:iceland
* created:2011–04–06..2013–01–14 in:username

### Extension based search:

* extension:pem private
* extension:ppk private
* extension:sql mysql dump
* extension:sql mysql dump password
* extension:json api.forecast.io

### Automated Tools:

1. [TruffleHog](https://github.com/dxa4481/truffleHog)
2. [WatchTower](https://radar.nightfall.ai/)

### NOTE :

If you find any API key or credentials or any other sensitive information under test directory then do not report it because that is an intended behaviour.

