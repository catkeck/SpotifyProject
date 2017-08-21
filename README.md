# My Favorite Genres

## Instructional info
Information about Promises as it relates to this app. It points you to pieces of code to look at for different examples about using Promises. There are many more comments in the source code.

### Where to start?
Start in the `index.js` file, at the `App.init` method. This method instantiates a `User` object as a Promise which we can chain methods on to.

### Working with Promises
Take a look at `Request.get`. From this function, we are returning the result of the call to [`fetch`](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API). We transform the value received by fetch by chaining two `then` calls to it.

### Creating new Promises
Inside of `Request.get` we are also creating a new Promise. In short, this Promise says, "after a certain amount of time, resolve this Promise with the value passed to the outer callback".

Inside the `User.constructor`, look at the returned value of the constructor -- the call to `Auth.init`. `Auth.init` returns a new Promise which does some work (gets the auth token) and determines how to deal with chained methods if the auth token is present.

### Chaining Promises
Since `Auth.init` returns a Promise object, we can then chain `then` and `catch` methods onto it. Going back to the `User.constructor`, you can see that we have exactly one `then` method and one `catch` method chained to it.

Take a look at the `GenreList.constructor` which behaves similarly to `User.constructor` in that it returns a Promise. Try to reason about the pipeline that this chain of Promises creates and why we would assign `self.items` once we're in a `then` callback.

### Dealing with multiple Promises
In `App.init`, we created a user Promise that we chain one `then` and one `catch` to. Uncomment one line at a time inside of the `then` callback and read the comments next to that method.

### Improve the application
It would be cool to see how your top genres have changed over time. Maybe a graph to display the number of artists in your top artists per genre. Maybe compare top genres by top artists and by top tracks over time. Draw lines between genres that show up in more than one list...

## Technical info
Get the app up and running on your machine and learn how to use it (there's not much to it).
### Set up
First, create an application for the [Spotify Web API](https://developer.spotify.com/web-api/) in order to get a client ID. For the application, you'll want to save a redirect URI. In order to temporarily host my local page online, I used an `npm` package `http-server` to serve from the current directory, then called [ngrok](https://ngrok.com/) with the port provided by `http-server`.

Once you have the redirect URI and the client ID, insert these values as variables in the `Auth.getLoginURI` function and navigate to your redirect URI.

### Using the application
The application alerts the user that there is no access token by default, and then provides them with a log in button. When the button is pressed, the current window redirects to the Spotify OAuth form, and then redirects to your redirect URI. Once authorized, you should see a list of all your top genres for each time period.
