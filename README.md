<p align="center">

  <p align="center">
    Full Stack ChatApp Using Django and Django Channels with React.js for frontend
  </p>
</p>

# Full stack django and react.js app for my interview as a programming instructor.



This app implements chat app using django and django channels which enables django through asgi (web server gateway interface) to use web socket for real-time processes. In other words, with the implementation of django channels, I am able to build a django application that does not load the server side with request by the client app, I also extended the functionality of the app by implementing the client side using react.js. A client side javascript framework that is based on a single page application implimentation, does't load the broswer on page change or routing into another page. It's a wonderful framework I've used for many projects.

To run the backend, run:

```json
virtualenv env
source env/bin/activate
pip install -r requirements.txt
python manage.py runserver
```

To run the frontend:

```json
npm i
npm start
```

To develop locally:

```
1. Change the `DEBUG` flag in `src/settings.js`
2. Create two users (easiest way might be to run `python manage.py createsuperuser` twice)
3. Using django admin, create a `Contact` object for each user.
4. Make sure you have an instance of redis running. 
```

To build for deployment:

```json
npm run build
```

