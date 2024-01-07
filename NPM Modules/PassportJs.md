# Passport.js 
Passport.js is npm module that is used **for manage Authentication into your express-project.**

Here, we will learn:
- Install Passport
- Config User Model
- Configration for app.js 
- LogIn, Register & Logout (with passport.js)
- Access loggedIn User in any route

## Steps:
### 1. Install Passport.js
First install passport.js using command prompt
```bash
npm i passport passport-local passport-local-mongoose 
```
Also install these if Not installed yet.
```bash
npm i mongoose express-session
``` 

### 2. Config User Model
Apply following configration to user's model. So that user schema is used for authentication.
```userModel.js
const mongoose = require("mongoose");
const Schema = mongoose.Schema;
const plm = require("passport-local-mongoose");

const userSchema = new Schema({
  username: {
    type: String,
    required: true,
    unique: true,
  },
  password: {
    type: String,
    // required: true,
  },
  
  /* Other Staff */
});

userSchema.plugin(plm);     // Must Include

module.exports = mongoose.model("User", userSchema);
```
**`Note:`** userSchema must have `userSchema.plugin(plm);`.

### 3. Applying Passport.js
Apply following configration into file with your starter server code, moslty `app.js` or `server.js`.
```app.js
const expressSession = require("express-session");
const mongoose = require("mongoose");
const passport = require("passport");

const app = express();

app.use(
  expressSession({
    resave: false,
    saveUninitialized: false,
    secret: process.env.SECRET,
  })
);
app.use(passport.initialize())
app.use(passport.session())

passport.serializeUser(usersRouter.serializeUser())
passport.deserializeUser(usersRouter.deserializeUser())

// Remaining Code
```

### 4. Implement Routes
Implement following code to file containing API routes, mostly `routes/index.js` or `app.js` or `routes.js`.
#### Basic Configration in `route/index.js`

```router/index.js
const userModel = require("../Model/userModel");
const passport = require("passport");
const localStategy = require("passport-local");

passport.use(new localStategy(userModel.authenticate()));

const router = express.Router();
```
After this Apply following routes accordingly.
#### To Check is User loggedIn or Not
```routes/index.js
const isLoggedIn = (req, res, next) => {
  if (req.isAuthenticated()) {
    return next();
  }
  res.redirect("/login");
};

/* Just use this func as middleware for protected route */

router.get(
    "/profile", 
    isLoggedIn,         // If loggedIn '/profile', else '/login' 
    (req, res, next) => {
        res.render("profile", user);
    }
);
``` 
#### To Register 
To use this just submit form to `/register` with `method="post"`
```routes/index.js
router.post("/register", function (req, res, next) {
  const { fullName, username, email, password } = req.body;

  const newUser = new userModel({ fullName, username, email });
  
  userModel.register(newUser, password)
    .then(() => {
        passport.authenticate("local")(req, res, () => {
            res.redirect("/profile");
        });
    });
});
```
#### To Login 
To use this just submit form to `/login` with `method="post"`
```routes/index.js
router.post(
  "/login",
  passport.authenticate("local", {
    successRedirect: "/profile",
    failureRedirect: "/",
  })
);
```
#### To Logout 
To use this just use `<a href='/logout'>Logout</a>`
```routes/index.js
router.get(
    "/logout", 
    (req, res, next) =>{
        req.logout(function (err) {
        if (err) {
            return next(err);
        }
    res.redirect("/");
  });
});
```
#### To Access current User 
If any user loggedIn, He is stored in `req.user`
```routes/index.js
router.get(
    "/profile", 
    (req, res, next) =>{
    res.send(`Hello, ${req.user.username}`);
  });
```
This will say Hello to current user that is loggedIn.

---