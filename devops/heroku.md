## Heroku Tips

## DB

For connecting to a remote postgres DB with Postico:

```
npm i heroku-postico -g
cd <dir-with-heroku-project>
heroku plugins:install heroku-postico
heroku postico:open
heroku postico:open --app <app_name>
```
