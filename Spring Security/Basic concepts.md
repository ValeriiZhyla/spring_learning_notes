


**Authentication** - answering the question "Who are you" with proofs.
There are three main types of authentication:

- Knowledge based authentication: password, pin code, secret question
- Possession based authentication: phone message, key card, access token device
- Multi Factor Authentication: combination of different types of authentication, like password + code from SMS.


**Authorization** - answering the question "Has this user the permission to perform the desired action?".

**Principal** - currently log in account.


How does authorization happen - how to decide, whether user can perform the action or not? This is controlled by some set of permissions. Each permission is called **Authority**. 

The set of all Authorities of the use is called **Granted Authority**.

**Role** - group of authorities, that are assigned together. For exampe, role User, role Moderator and Role admin, that can use different API endpoints.

Video: https://www.youtube.com/watch?v=I0poT4UxFxE&list=PLqq-6Pq4lTTYTEooakHchTGglSvkZAjnE&index=2