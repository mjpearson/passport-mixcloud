# Passport-MixCloud

[Passport](https://github.com/jaredhanson/passport) strategy for authenticating
with [MixCloud](http://mixcloud.com) using the OAuth 2.0 API.

## Install

    $ npm install passport-mixcloud

## Usage

#### Configure Strategy

The MixCloud authentication strategy authenticates users using a MixCloud
account and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which
accepts these credentials and calls `done` providing a user, as well as
`options` specifying a client ID, client secret, and callback URL.

    passport.use(new MixCloudStrategy({
        clientID: CLIENT_ID,
        clientSecret: CLIENT_SECRET
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ MixCloudId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authorize()`, specifying the `'MixCloud'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/mixcloud',
      passport.authorize('mixcloud'));

    app.get('/auth/mixcloud/callback', 
      passport.authorize('mixcloud', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## Thanks

  - [Jared Hanson](http://github.com/jaredhanson)

## License

[The MIT License](http://opensource.org/licenses/MIT)

Copyright (c) 2013 Michael Pearson <[http://github.com/mjpearson](http://github.com/mjpearson)>