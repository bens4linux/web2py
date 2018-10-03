10/02/2018
The is a rewrite of the the old extract_pgsql_models.py
program.

I have added the getopts parameters to better facitlate option parameters, 
made some expected parameters GLOBOL if they are not passed.

To run:

$> extract_pgsql_models_v2.0.0.py 
  -d <db name> 
  -s <server name / ip> 
  -p <port> 
  -u <user id> 
  -a <password> 
  -m <migrate> 
  -w

where parameters are :
 -d is the dbname you wish to connect to
 -s is the server name as in hosts or the IP address of the server (default is "localhost")
 -p is the port number (defaults to 5432 - stndard postgres port)
 -u is the user id  (defaults to postgres)
 -a is the password
 -m is the migration flag 
 -w is the "foreign key" typing.

The -m is there to force a "migration type" for legacy / exsisting databases.
Where the prameters are as follows:
   t_off - Disallow migration at table level
   d_off - Disallow migration at database level
   d_force - Disallow migration at database level BUT force fake migrate

   No Migration settings or any other will simple do the default migration

The -w is a parameter to fix the "*&#%@#" DAL issues with foreign keyes where
IF muiltple foreign keyes are defined for a given table and IF those keyes are 
compsite and IF a field is reused in the fk definition, the python program BLOWS
up becuse DAL cannot handle that kind of situation.
To work around this I create NEW single foreign keys named with "dalfkey" in them 
and when the flag is set, this program will ONLY extract those foreign definitions
and bypass all the other saving one much grief !

Ben Duncan
bend@linux4ms.net

