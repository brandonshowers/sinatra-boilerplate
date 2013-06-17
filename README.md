# Sinatra Boilerplate
A great place to start with [Sinatra](http://www.sinatrarb.com/), [HTML5 Boilerplate](http://html5boilerplate.com/), [Compass](http://compass-style.org/), [CoffeeScript](http://coffeescript.org/) and [Sprockets (aka the asset pipeline)](https://github.com/sstephenson/sprockets) all cooked together.

## TL;DR: Get me up and running
1. Grab the code and `bundle` the gems.
2. Make sure you have [memcached](http://www.memcached.org/) installed.
3. Run `rake s` to start the development server.

# What's in the Box
## HTML5 Boilerplate
sinatra-boilerplate uses *some* of the utter uber-hawtness that is the [HTML5 Boilerplate](http://html5boilerplate.com/) but *not all*. I opted not to use the build script stuff because I feel like it adds an extra layer of trouble when working with Sinatra.

The base layout file is pretty compliant with what the Boilerplate puts out except for a few minor tweaks. Most of the comments have been left in place as well.

Direct implementations from HTML5BP:

* `html` scoping by class.
* Viewport settings for mobile browsers.
* Better analytics script.
* More awesome CSS base.
* ... probably more that I've forgotten :)

## Modernizr
[Modernizr](http://www.modernizr.com/) is fantastic and I threw it in because... well, it's fantastic!

## Compass
Because CSS sucks and SASS + Compass doesn't.

Compass + SASS gives you all kinds of great mixins and nesting stuff that would surely make anyone who's done a lot of CSS quiver in schoolgirl-like delight. Take, for example, some CSS:

```css
#content { border: 1px solid red; }
#content p { font-size: 34em; }
#content p.small { font-size: 12em; }
#content em { color: white; }
```

Not so great. You have to write `#content` each time you want to address that element. How about with Compass?

```scss
#content {
  border: 1px solid red;

  p {
    font-size: 34em;

    &.small {
      font-size: 12em;
    }
  }
  em {
    color: white;
  }
}
```

Wait, **what**? Yeah, you can nest it all. If you do any CSS at all in your life ever then you should be using Compass.

[Scope the docs and get crackin'.](http://compass-style.org/)

### Susy
Susy is a fantastic grid system built to be responsive and lithe. [Check out the docs here and get griddin'](http://susy.oddbird.net/)

## Sinatra Addons
### Run Later

After filters are great and all, but they block the rendering of the page and that sucks. I want to be able to, mid-render, tell Ruby to go off and do some stuff that I know will take a long time without it stopping the current page. Think of it as an asynchronous (ya know, like AJAX) Ruby request!

This is a plain insert of my [Sinatra run_later module](https://github.com/l3ck/sinatra_run_later), which I based off of [this run_later module](https://github.com/pmamediagroup/sinatra_run_later) which is based off of [THIS run_later module](https://github.com/mattmatt/run_later). Use it like so:

```ruby
require 'rubygems'
require 'sinatra'
require 'run_later'

get '/' do
  run_later do
    # some task that you don't want to block.
    sleep 20
  end

  "Hello World"
end
```

### Form Tag Helpers
The thing I missed most in Sinatra was the glorious `input_for` kind of stuff you get with Rails, so I made some! I've included them by way of the [gem I made, 'sinatra-tag-helpers'](https://github.com/l3ck/sinatra-tag-helpers).

## Extra Hawt Sauce
I've added a bunch of modules and helper functions that I use all the time to this to (hopefully) make your life easier when you're getting your app first setup. Some of the helpers methods I've added include:

* **Sprockets**
  * holy crap that's nice!!
  * there's a Rake task that pre-compiles your assets so nginx (or Apache or whatever) can serve them up _super_ fast too!
* **core extensions**
  * adds a `try` method and `blank?` method to everything (totally stolen from Rails)
* **Sinatra extensions**
  * a better `erb` method so you don't have to do crap like `erb :"folder/file"` anymore

## Server Goodies
* **nginx configuration** - all based on H5BP and a simple upstream setup for Unicorn.
* **logrotate configuration** - so your logs don't get crazy.

## How to Use It
You like it? **Awesome!** Here's how to use it:

1. Download the sauce (either through git or the download button).
2. `bundle`
3. Make sure you have [memcached](http://www.memcached.org/) installed and running (`memcached -d`).
4. Run `rake s` from the directory of the sauce.
5. Profit!

If you have suggestions or think I goofed please let me know or send a pull request.

## Acknowledgements
All the stuff used here is either open source or donation ware and totally the work of the people who made it, not me. I just put the pieces together and bundled it up all pretty-like. This little starter package wouldn't be possible without the awesome work these guys have done and their generosity in sharing their code with the rest of us.

Oh, and...

<pre>
# . . . . . . . . . . . . . . . . _,,,--~~~~~~~~--,_
# . . . . . . . . . . . . . . ,-' : : : :::: :::: :: : : : : :º '-, ITS A TRAP!
# . . . . . . . . . . . . .,-' :: : : :::: :::: :::: :::: : : :o : '-,
# . . . . . . . . . . . ,-' :: ::: :: : : :: :::: :::: :: : : : : :O '-,
# . . . . . . . . . .,-' : :: :: :: :: :: : : : : : , : : :º :::: :::: ::';
# . . . . . . . . .,-' / / : :: :: :: :: : : :::: :::-, ;; ;; ;; ;; ;; ;; ;\
# . . . . . . . . /,-',' :: : : : : : : : : :: :: :: : '-, ;; ;; ;; ;; ;; ;;|
# . . . . . . . /,',-' :: :: :: :: :: :: :: : ::_,-~~,_'-, ;; ;; ;; ;; |
# . . . . . _/ :,' :/ :: :: :: : : :: :: _,-'/ : ,-';'-'''''~-, ;; ;; ;;,'
# . . . ,-' / : : : : : : ,-''' : : :,--'' :|| /,-'-'--'''__,''' \ ;; ;,-'/
# . . . \ :/,, : : : _,-' --,,_ : : \ :\ ||/ /,-'-'x### ::\ \ ;;/
# . . . . \/ /---'''' : \ #\ : :\ : : \ :\ \| | : (O##º : :/ /-''
# . . . . /,'____ : :\ '-#\ : \, : :\ :\ \ \ : '-,___,-',-`-,,
# . . . . ' ) : : : :''''--,,--,,,,,,¯ \ \ :: ::--,,_''-,,'''¯ :'- :'-,
# . . . . .) : : : : : : ,, : ''''~~~~' \ :: :: :: :'''''¯ :: ,-' :,/\
# . . . . .\,/ /|\\| | :/ / : : : : : : : ,'-, :: :: :: :: ::,--'' :,-' \ \
# . . . . .\\'|\\ \|/ '/ / :: :_--,, : , | )'; :: :: :: :,-'' : ,-' : : :\ \,
# . . . ./¯ :| \ |\ : |/\ :: ::----, :\/ :|/ :: :: ,-'' : :,-' : : : : : : ''-,,
# . . ..| : : :/ ''-(, :: :: :: '''''~,,,,,'' :: ,-'' : :,-' : : : : : : : : :,-'''\\
# . ,-' : : : | : : '') : : :¯''''~-,: : ,--''' : :,-'' : : : : : : : : : ,-' :¯'''''-,_ .
# ./ : : : : :'-, :: | :: :: :: _,,-''''¯ : ,--'' : : : : : : : : : : : / : : : : : : :''-,
# / : : : : : -, :¯'''''''''''¯ : : _,,-~'' : : : : : : : : : : : : : :| : : : : : : : : :
# : : : : : : : :¯''~~~~~~''' : : : : : : : : : : : : : : : : : : | : : : : : : : : :
</pre>

So, ya know, watch out...