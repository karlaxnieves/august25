---
title: mdx invalid
deprecated: false
hidden: false
metadata:
  robots: index
---
Lingohub supports *Android* `.xml` files, which are used to localize Android applications.

Lingohub offers a tight coupling between [Apple iOS](doc:apple-ios) and Android projects to speed up your multi-mobile development. You must create one of these projects and export the translated resource files in another format.

<Embed typeOfEmbed="youtube" url="https://vimeo.com/778648841/6d82551cbe" html="%3Ciframe%20class%3D%22embedly-embed%22%20src%3D%22%2F%2Fcdn.embedly.com%2Fwidgets%2Fmedia.html%3Fsrc%3Dhttps%253A%252F%252Fplayer.vimeo.com%252Fvideo%252F778648841%253Fh%253D6d82551cbe%2526app_id%253D122963%26dntp%3D1%26display_name%3DVimeo%26url%3Dhttps%253A%252F%252Fvimeo.com%252F778648841%252F6d82551cbe%26image%3Dhttps%253A%252F%252Fi.vimeocdn.com%252Fvideo%252F1957382148-e4317a80a082e0c737155864ab35b9dd74bab367f82168bb1bbcff3482bd9512-d_1280%253Fregion%253Dus%26type%3Dtext%252Fhtml%26schema%3Dvimeo%22%20width%3D%221920%22%20height%3D%221080%22%20scrolling%3D%22no%22%20title%3D%22Vimeo%20embed%22%20frameborder%3D%220%22%20allow%3D%22autoplay%3B%20fullscreen%3B%20encrypted-media%3B%20picture-in-picture%3B%22%20allowfullscreen%3D%22true%22%3E%3C%2Fiframe%3E" href="https://vimeo.com/778648841/6d82551cbe" providerUrl="https://vimeo.com/" providerName="Vimeo" />

<br />

# Format

* this format is based on *XML*
* Lingohub supports `string, string-array, and plurals` elements
* comments can be specified using *XML* syntax and will be assigned to the following key/value pair
* syntax for placeholders can be found [here](http://developer.android.com/reference/java/util/Formatter.html)

# Example

Additional example files can be accessed [here](https://github.com/lingohub/Example-Resource-Files/tree/master/Android).

```xml
<?xml version="1.0" encoding="UTF-8"?>
<resources>
  <string name="deutscher string">actually german: muss grösser gleich %d sein</string>
  <string name="escaped quotes">Logged in as \"%s\"</string>
  <string name="escaped single quotes">Logged in as \'%s\'</string>
  
  <string name="surrounded quotes">"Logged in as '%s'"</string>
  <string name="surrounded quotes escaped">"Logged in as \'%s\'"</string>

  <!-- single line comment -->
  <string name="two placeholder newline">Hello %s!\nYou have got %s unread messages.</string>
               <!-- multi
               line -->
  <!-- comment -->
  <string name="with html content"><i>left</i></string>

  <!-- string-array comment -->
  <string-array name="planets_array">
    <item>Mercury</item>
    <!-- Venus comment -->
    <item>Venus</item>
    <item>Earth</item>
    <!-- Mars comment -->
    <item>Mars</item>
  </string-array>

  <string-array name="months">
    <item>January</item>
    <item>February</item>
    <item>March</item>
    <item>April</item>
    <item>May</item>
    <item>Jun</item>
    <item>July</item>
    <item>August</item>
    <item>September</item>
    <item>October</item>
    <item>November</item>
    <item>December</item>
  </string-array>

  <!-- strings quantity comment -->
  <plurals name="numberOfSongsAvailable">
    <!-- one comment -->
    <item quantity="one">Znaleziono jedną piosenkę.</item>
    <item quantity="few">Znaleziono %d piosenki.</item>
    <!-- other comment -->
    <item quantity="other">Znaleziono %d piosenek.</item>
  </plurals>

</resources>
```

<br />

# To consider

## XML format related export rules

**Rule**: `&` and `<` have to be escaped using `&amp;` and  `&lt;` unless they are used as an escape sequence (e.g. ") or element tag (e.g., `<b>`); otherwise, the *XML* document is not well-formed!

**Exception**: if a strings element contains HTML (e.g., `<u>`) the behavior depends on the **HTML export setting**:

**RAW**: *HTML* tags will not be escaped at all; only the characters `&` and `<` will be escaped according to the rule above

**ESCAPE**: all occurrences of `< `, `>` and `&` will be escaped, also for *HTML* tags

**CDATA**: the content will be wrapped inside a `CDATA` section and no escaping using *XML* entities is done at all

In case the content is already wrapped in a `CDATA` section during import, it will also be exported inside a `CDATA` section, irrespective of the *HTML* export setting!

<br />

## Android related export rules

* Whenever a single quote (‘) character is in the content, it has to be either escaped using `\'` or the whole string has to be quoted using double quotes (“)
* The character double quote (“) itself has to be escaped using `\”`
* For a quoted text like *”   this is some text   ”* no trimming will be done on import; the whitespace will also be contained in the exported file!
* In case HTML tags (e.g. `<b>`, `<i>`, `<u>`) are present. They are handled according to the HTML export settings; however, if format strings (e.g. `%1$d`) are also present; all HTML tags will be escaped as if the option export setting.`ESCAPE` was selected!
* If format strings are used, any other occurrences of “%” have to be escaped using the according unicode point representation `&#0025;`. Therefore, the percent sign will always be escaped if not used as format String (e.g., `“Save 50&#0025; only now!”`).\
  Exception: if the XML attribute `formatted = “false”` is present on the element, no escaping of the percent sign is done!
* The characters “@” and “?” are escaped with `\` if they are at the beginning of the content (or represent the only content) unless the whole string is quoted using double quotes (“) as well or they represent references (e.g., in the form `@string/keyName`)
* Newlines are escaped using `\n`, Tabs are escaped using `\t`,\
  the backslash character is escaped using `\\`

## Additional export rules

* The rules under *“Android-related Export Rules”* are always applied even if the content is inside a `CDATA` section (either because it was imported that way or a `CDATA` section is created because the according HTML export option is selected)
* In case the export option *“Escape Unicode Characters”* is selected in addition to the rules above, all non-ASCII characters will be replaced by the according unicode point representation as well
* In case a non-Unicode encoding (e.g., ASCII) is selected, Unicode escaping will be done implicitly

## Locale information

In typical Android projects, these files do not need to have any locale information in the filename (a typical name is `strings.xml`). The locale information can be found in the path. Therefore, we always recommend using our SCM integration to synchronize your repository with LingoHub.\
Otherwise, you must always specify the language in another step while importing this file.