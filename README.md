# Heroku Buildpack for Oracle

Heroku buildpack for setting up Oracle Instant Client and the `LD_LIBRARY_PATH`.

# Usage

## Add a detect hook (required)

In order for this buildpack to execute, it will look for a `.oracle.yml` file in your app's root.  The file can be empty but it must exist.

    touch .oracle.yml

## Add Buildpack

You'll need to use multiple buildpacks. 
This buildpack will need to be invoked first, followed by your language buildpack.  
Heroku now supports configuring multiple buildpacks natively, or you can use the [heroku-buildpack-multi](https://github.com/ddollar/heroku-buildpack-multi) buildpack.

### Setup using heroku-buildpack-multi

Add the following contents to `.buildpacks`:

    https://github.com/luizalabs/oracle-heroku-buildpack
    https://github.com/heroku/heroku-buildpack-go

# Configuration (Optional)

It is sometimes desirable to use `tnsnames.ora` or `sqlnet.ora` to configure how Oracle connects to a database or to use `sqlnet.ora` to configure connection wallets.

The `tnsnames.ora` and `sqlnet.ora` files are often located in `$ORACLE_HOME/network/admin`.  
This buildpack will correctly setup `$ORACLE_HOME` and `$TNS_ADMIN` to point to `$ORACLE_HOME/network/admin`.  
A location for `tnsnames.ora` or `sqlnet.ora` can be configured inside the `.oracle.yml` file:

    cat .oracle.yml
    ---
    tnsnames.ora: config/tnsnames.ora
    sqlnet.ora: config/sqlnet.ora

The files will be symlinked into `vendor/oracle-instantclient/network/admin`

You do not need `tnsnames.ora` and `sqlnet.ora`, they're both optional. The buildpack and some other buildpacks will work fine without them.

## Tested buildpacks

Although I firmly believe it should work with basically any language, I can only say for the languages I've actually tested :)

If you need this buildpack to work with any other language, feel free to fork this repo and submit a Pull Request ;)

[Golang](https://github.com/heroku/heroku-buildpack-go) 

[Python](https://github.com/heroku/heroku-buildpack-python) 
