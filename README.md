# koinbot

http://howdy.ai/botkit/

https://github.com/howdyai/botkit

http://www.sitepoint.com/getting-started-slack-bots/

```
SCHEMA
Balances
User Balance

API

POST koinbot mint [num] //for KAPIL only
  IF user == kapil
    DO +num kapil
  END IF

  error - command doesn't exist if not kapil
  error - num can't be negative (defaults to 0)

GET koinbot balance [user]
  SELECT num FROM BALANCES WHERE User = user || 0
  
  error - user doesn't exist

POST koinbot num user
  LOCK user
  current = DO balance user
  newVal = current + num
  UPSERT (user, newVal) INTO BALANCES
  UNLOCK user

  error - missing or invalid argument types or missing
  error - user doesn't exist
  error - you don't have the balance to give them

GET koinbot rank [min max]
  SELECT user, num FROM BALANCES
    SORT BY num DESC
    LIMIT ??

  no errors - the actual max is 500, so if you want more you need to page
```
