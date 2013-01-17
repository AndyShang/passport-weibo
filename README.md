# Passport-weibo

copied from [Passport-github](https://github.com/jaredhanson/passport-github) by [Jared Hanson](http://github.com/jaredhanson)

[Passport](http://passportjs.org/) strategy for authenticating with [weibo](http://weibo.com/)
using the OAuth 2.0 API.

This module lets you authenticate using weibo in your Node.js applications.
By plugging into Passport, weibo authentication can be easily and
unobtrusively integrated into any application or framework that supports
[Connect](http://www.senchalabs.org/connect/)-style middleware, including
[Express](http://expressjs.com/).

## Installation

    $ npm install passport-weibo

## Usage

#### Configure Strategy

The weibo authentication strategy authenticates users using a weibo account
and OAuth 2.0 tokens.  The strategy requires a `verify` callback, which accepts
these credentials and calls `done` providing a user, as well as `options`
specifying a client ID, client secret, and callback URL.

    passport.use(new WeiboStrategy({
        clientID: app_key,
        clientSecret: app_secret,
        callbackURL: "http://127.0.0.1:3000/auth/weibo/callback"
      },
      function(accessToken, refreshToken, profile, done) {
        User.findOrCreate({ weiboId: profile.id }, function (err, user) {
          return done(err, user);
        });
      }
    ));

#### Authenticate Requests

Use `passport.authenticate()`, specifying the `'weibo'` strategy, to
authenticate requests.

For example, as route middleware in an [Express](http://expressjs.com/)
application:

    app.get('/auth/weibo',
      passport.authenticate('weibo'),
      function(req, res){
        // The request will be redirected to weibo for authentication, so this
        // function will not be called.
      });

    app.get('/auth/weibo/callback', 
      passport.authenticate('weibo', { failureRedirect: '/login' }),
      function(req, res) {
        // Successful authentication, redirect home.
        res.redirect('/');
      });

## License

(The MIT License)

Copyright (c) 2011 Andy Shang

Permission is hereby granted, free of charge, to any person obtaining a copy of
this software and associated documentation files (the "Software"), to deal in
the Software without restriction, including without limitation the rights to
use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of
the Software, and to permit persons to whom the Software is furnished to do so,
subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS
FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR
COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER
IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN
CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.
