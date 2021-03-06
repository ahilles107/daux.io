Very simple and flexible plugin to show an article of the day.

**Purpose:** Sets articles as an "Article of the Day" and displays it in nice calendar widget (look at **Screen 4**).

Features
-------------
- Set available articles as an Article of the Day
- Define the publication in which the article of the day may appear
- Define the date of the article of the day
- Define your own style sheet for the calendar widget appearance
- Choose publications in which articles may appear
- Select one of the available image resolution types (ex. issuethumb (130x70))
- Manually define articles image resolution (optional)
- Define first day of the month
- Set the first and last month (months range to be available in calendar)
- The ability to hide / show navigation (prev / next buttons, etc.)
- The ability to hide / show the names of days
- Available in diffrent languages ([list](https://github.com/newscoop/plugin-ArticlesCalendar/tree/master/Resources/translations))

Installation
-------------
Installation is a quick process:


1. Installing plugin through our Newscoop Plugin System
2. Include plugin smarty block
3. That's all!

### Step 1: Installing plugin through our Newscoop Plugin System
Run the command:
``` bash
$ php application/console plugins:install "newscoop/articles-calendar-plugin" --env=prod
```
Plugin will be installed to your project's `newscoop/plugins/Newscoop` directory.

### Step 2: Include plugin smarty block

Include below smarty block into template (ex. front.tpl - calendar will be shown on homepage)
```smarty
{{ articles_calendar }}{{ /articles_calendar }}
```
### Step 3: That's all!
Go to an article edition in Newscoop Admin Panel to see Newscoop Article Of The Day Plugin on the right sidebar in action.

If you included calendar smarty block in front.tpl file then go to your homepage to see the calendar widget!

###More about plugin 
Plugin allows you to fully control article of the day calendar in very simple way (admin panel). Through plugin administration panel you are able to define all the settings regarding plugin.

**Settings: (`Entity/Settings.php`)**
- `firstDay`      - define first day of the month in calendar view
- `earliestMonth` - define the earliest month in calendar view for specified year
- `latestMonth`   - define latest month of the current year in calendar view (similarly to an example above)
- `currentMonth`  - define if the latest month should be the current month (if set, `latestMonth` option doesn't apply)
- `showDayNames`  - show / hide day names on top of calendar view
- `navigation`    - show / hide navigation bar
- `imageWidth`    - articles image width (optional field)
- `imageHeight`   - articles image height (optional field)
- `rendition`     - image defined resolution (ex. issuethumb (130x70))
- `publicationNumbers` - list of publications IDs where articles of the day should appear (posibillity to add many publications)
- `styles`        - field to save CSS styles for calendar view
- `last_modified` - date when custom CSS was last edited

**NOTE:** `firstDay` should be only numeric value: minimum: 1, maximum: 31. `earliestMonth` and `latestMonth` should be numeric values from 1 to 12. 

Overriding Request parameters 
-------
All options listed above (without `last_modified`, `styles` and `currentMonth`) can be overridden by the request parameters as given in example:

```php
$firstDay = $request->get('firstDay', $settings->getFirstDay());
$navigation = $request->get('navigation', $settings->getNavigation());
...
```

If you wish to set your custom preferences by overriding Request parameters then you have to place your custom Javascript code with Ajax in any template file you wish calendar widget to appear.

Custom Ajax code example with all parameters possible to override: 

```js
<script type="text/javascript">
    $.ajax({
        type: 'POST',
        url: '/plugin/articlescalendar/widget',
        data: {
            'publication_numbers': '2',
            'currentMonth': true,
            'earliestMonth': '2012-05',
            'latestMonth': '2013-09',
            'navigation': true,
            'showDayNames': true,
            'image_width': 130
            'image_height': 70
        },
        dataType: 'html',
        success: function(msg){
            $('.js-articles-calendar-widget-container').html(msg);
        }
    });
</script>
```

When you set `currentMonth` option to `true` then the current month in calendar widget will be up to date - `latestMonth` option won't apply in that case anymore.

Plugin in action
-------
**Article edit screen:**

![Screen 1](https://dl.dropboxusercontent.com/u/35759363/NewscoopPlugins/ArticleOfTheDay/articleplugin1.png)

**Screen 1:** Plugin view before any action is taken.

- `Status` - determines whether the article is an Article of the Day
- `Date` - determines the date of an article (if set then the date format is: `yyyy-mm-dd`), when we set an article as an article of the day, option to change date will appear (look at **Screen 2**).
- `Visible in` - publications we wish an article of the day may show up. If defined, plublications list will show up (look at **Screen 2**)
- `Choose date` - define an article of the day date. Date picker will show up when clicked.
- `Choose publication` - multiple select box to choose publications where an article of the day may appear

![Screen 2](https://dl.dropboxusercontent.com/u/35759363/NewscoopPlugins/ArticleOfTheDay/articleplugin2.png)
**Screen 2:** Plugin view after we set an article as an article of the day.

`Unmark` button let us remove an article from an article of the day. If pressed then view on **Screen 1** will show up with message: `Article successfully unmarked.` and article will disappear from calendar view.

**Plugin Admin Panel screen:**
![Screen 3](https://dl.dropboxusercontent.com/u/35759363/NewscoopPlugins/ArticleOfTheDay/articleplugin4.png)

**Screen 3:** Plugin Admin Panel screen. [Full size here.](https://dl.dropboxusercontent.com/u/35759363/NewscoopPlugins/ArticleOfTheDay/articleplugin3.png)

All options from this screen are described in `More about plugin` section.

**Calendar widget screen: (with added articles)**

![Screen 4](https://dl.dropboxusercontent.com/u/35759363/NewscoopPlugins/ArticleOfTheDay/calendarmin.png)

**Screen 4:** Calendar widget screen. [Full size here.](https://dl.dropboxusercontent.com/u/35759363/NewscoopPlugins/ArticleOfTheDay/calendar.png)

License
-------

This bundle is under the GNU GPL v.3. See the complete license in the bundle: [LICENSE](https://raw.github.com/newscoop/plugin-ArticlesCalendar/master/LICENSE)

About
-------
Newscoop Article Of The Day Plugin is a [Sourcefabric o.p.s](https://github.com/sourcefabric) initiative.
