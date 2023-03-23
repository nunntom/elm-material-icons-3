# Material Icons for Elm

All the SVG icons from Google's [Material Icons](https://fonts.google.com/icons?selected=Material+Icons) as a handy Elm type.

Why another Material Icons package? I wanted a nice opaque custom type `Icon` that I could pass around my views.

## Example Usage

### A button that doesn't care which variant of icon you use:

```elm
import Material.Icon as Icon exposing (Icon)

button : Icon a -> String -> Html msg
button icon label =
    Html.button []
        [ Icon.toSvg icon
        , Html.text label
        ]
```

### A button that only lets you pass an outlined icon:

```elm
import Material.Icon as Icon exposing (Icon, Outlined)

button : Icon Outlined -> String -> Html msg
button icon label =
    Html.button []
        [ Icon.toSvg icon
        , Html.text label
        ]
```

### Or if you only ever use outlined icons in your app:

```elm
import Material.Icons.Outlined as Icon exposing (Icon)

button : Icon -> String -> Html msg
button icon label =
    Html.button []
        [ Icon.toSvg icon
        , Html.text label
        ]
```

### Size and style

With `toSvg` the icon will take the current font colour and size (1em), but if you need more control you can pass arbitrary Html/Svg attributes using `toSvgWith`:

```elm
    Icon.toSvgWith
        [ style "width" "1em"
        , style "color" "red"
        ]
        icon
```

Note that if you don't provide a width and/or height (via inline style, css etc.) and the parent doesn't have a size, you won't see anything.

## Full Example

```elm
import Html exposing (Attribute, Html)
import Html.Attributes exposing (class)
import Material.Icon as Icon exposing (Icon)
import Material.Icons.Filled as Filled
import Material.Icons.Outlined as Outlined
import Material.Icons.Round as Round


button : List (Attribute msg) -> Icon a -> String -> Html msg
button attrs icon label =
    Html.button (class "button" :: attrs)
        [ Icon.toSvg icon
        , Html.text label
        ]


buttonPrimary : Filled.Icon -> String -> Html msg
buttonPrimary =
    button [ class "button-primary" ]


buttonSecondary : Outlined.Icon -> String -> Html msg
buttonSecondary =
    button [ class "button-secondary" ]


view : Html msg
view =
    Html.div []
        [ buttonPrimary Filled.thumbUp "Press this!"
        , buttonSecondary Outlined.thumbDown "Don't press this!"
        , button [] Round.rollerSkating "Go roller skating!"
        ]

```
