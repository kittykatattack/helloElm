Fun with Elm!
=============

Elm is a fun and easy way to create all kinds of interactive applications, websites and games. It's a programming language that includes all the best new ideas in programming language design from the past 20 years, and has built-in support for web technologies. 

http://elm-lang.org

Here's a video introduction to Elm by Evan Czaplicki (Elm's creator)

https://youtu.be/XJ9ckqCMiKk

And a few more good introductory talks:

https://youtu.be/FV0DXNB94NE
https://youtu.be/txxKx_I39a8

And an excellent practical introduction to Elm coding and its benefits:

https://youtu.be/3_M2G9U51GA

You can try out Elm programming here:

http://elm-lang.org/try

Let's look at some examples....

Display some text
-----------------

```
import Html exposing (..)

main =
  text "Hello!"
```


Use a variable
--------------
```
import Html exposing (..)

greeting = "Hello!"

main =
  text greeting
```


Create a function
-----------------
```
import Html exposing (..)

add a b = a + b

main =
  text (add 3 4)
```

This will give you an error message!

```
The argument to function `text` is causing a mismatch.

6|   text (add 3 4)

Function `text` is expecting the argument to be:

    String

But it is:

    number
```

You can fix this by using the `toString` function to convert a number into a string, like this:

```
import Html exposing (..)

add a b = a + b

main =
  text (toString (add 3 4))
```


Use some HTML
-------------
```
import Html exposing (..)

main =
  h1 [] [text "Hello!"]
```


Add some style
--------------

```
import Html.Attributes exposing (..)
import Html exposing (..)

main =
  h1 [ style [("color", "green")] ] [ text "Hello!" ]
```


Use An Image
------------

```
import Html.Attributes exposing (..)
import Html exposing (..)

main =
  img [ src "imgs/yogi.jpg", alt "Yogi Bear!" ] [ ]
```


Start building a web page
-------------------------

```
import Html.Attributes exposing (..)
import Html exposing (..)

main =
  div [ ]
    [ h1 [] [ text "We love bears!" ] 
    , p [ ] [ text "Yay, bears!" ] 
    , img [ src "imgs/yogi.jpg" ] [ ]
    ]
```


Add a variable
--------------

```
import Html.Attributes exposing (..)
import Html exposing (..)

thingWeLove = "cartoons"

main =
  div [ ]
    [ h1 [] [ text thingWeLove ] 
    , p [] [ text ("Yay, " ++ thingWeLove) ] 
    , img [ src "imgs/yogi.jpg" ] [ ]
    ]

```


Amazing compiler messages
-------------------------

Change `thingWeLove` to `thingweLove` in one spot.

```
import Html.Attributes exposing (..)
import Html exposing (..)

thingweLove = "cartoons"

main =
  div [ ]
    [ h1 [] [ text thingWeLove ] 
    , p [] [ text ("Yay, " ++ thingWeLove) ] 
    , img [ src "imgs/yogi.jpg" ] [ ]
    ]
```

Note the helpful error message:

```
Cannot find variable `thingWeLove`
Maybe you want one of the following?

thingweLove
```

Take that, JavaScript!


Modularize your styles
----------------------

```
import Html.Attributes exposing (..)
import Html exposing (..)

thingWeLove = "cartoons"

textStyle =
  style
    [ ("color", "green")
    , ("font-family", "Futura")
    ]

main =
  div [ ]
    [ h1 [ textStyle ] [ text thingWeLove ] 
    , p [ textStyle ] [ text ("Yay, " ++ thingWeLove) ] 
    , img [ src "imgs/yogi.jpg" ] [ ]
    ]
```


Re-use your code
----------------

```
import Html.Attributes exposing (..)
import Html exposing (..)


user name =
  div [ ]
    [ h1 [] [ text name ] 
    , img [ src "imgs/yogi.jpg" ] [ ]
    ]
  

main =
  div [ ]
    [ user "Rex" 
    , user "Sarah"
    , user "Dave"
    ] 
```


Create an interactive application
---------------------------------

`StartApp` is Elm's simple framework for helping you to easily make things interactive. It listens for changes to the user interface, updates the application model with those changes, and then displays a new view (what you see on-screen) that reflects those changes.
Here's one of the simplest interactive applications you can make.

```
import Html.Attributes exposing (..)
import Html exposing (..)
import StartApp.Simple as StartApp
import Html.Events exposing (..)


-- MODEL

type alias Model = Int

model = 0


-- UPDATE

type Action = Increment | Decrement

update action model =
  case action of
    Increment ->
      model + 1
      
    Decrement ->
      model - 1
      

-- VIEW

view address model =
  div []
    [ button [ onClick address Increment ] [ text "plus" ]
    , div [] [ text (toString model) ]
    , button [ onClick address Decrement ] [ text "minus" ] 
    ]
    
    
-- Wire up the application

main =
  StartApp.start
    { model = model
    , view = view
    , update = update
    } 
```

All Elm applications follow this exact same format. You can create big, complex applications just by connecting lots of smaller simpler modules like this together. Because it's easy to test each small module, and they all use the same structure, you have a strong guarantee that your final application will work the way you expect. 

Next steps
----------

Follow Elm's Complete Guide, here:

http://elm-lang.org/docs

The **Elm Architecture** is the standard way to build Elm Apps:

https://github.com/evancz/elm-architecture-tutorial/

If you get stuck don't be afraid to ask questions!

https://www.reddit.com/r/elm

and

https://groups.google.com/forum/#!forum/elm-discuss
