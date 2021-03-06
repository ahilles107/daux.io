Usefull services for integration Newscoop and Facebook.

Facebook caches shared urls for better performance. It can cause some problems at the time we want to change title, decscripton of our article because we still have an older version of our article. This is why this plugin is designed for.

**Purpose:** Clear an article cache on Facebook and add Open Graph tags.

Installing Newscoop Facebook Plugin Guide
-------------
Installation is a quick process:


1. Installing plugin through our Newscoop Plugin System
2. That's all!

### Step 1: Installing plugin through our Newscoop Plugin System
Run the command:
``` bash
$ php application/console plugins:install "newscoop/facebook-newscoop-bundle" --env=prod
```
Plugin will be installed to your project's `newscoop/plugins/Newscoop` directory.


### Step 2: That's all!
Go to an article edition in Newscoop to see Newscoop Facebook Plugin on the right sidebar in action.

Also read more about [Lifecycle Subscriber Managing](https://wiki.sourcefabric.org/display/NPS/Lifecycle+Subscriber+Managing).

###More about plugin 


Plugin has only one Entity: `Facebook.php`. After plugin is installed in your database will show up new table: `plugin_facebook_informations`.

This table keeps informations from Facebook about an article, such a:
- `article` - article ID
- `language` - article's language ID
- `title` - article title
- `description` - article description
- `created_at` - date when informations were added
- `is_active` - informations status

**Generating Open Graph tags using Smarty Plugin**

In `Newscoop/FacebookNewscoopBundle/Resources/smartyPlugins` directory you will find file called: `block.facebook_meta_block.php`

This file is facebook metadata block plugin. It generates the Facebook Meta information for a page.

Smarty Plugin will be automatically autoloaded and available in your templates.

To test and display meta data generated by smarty plugin just put this block:
````
{{ facebook_meta_block admins="123422,234223432,234234234,23423423" }}{{ /facebook_meta_block }}
````
 into `_html-head.tpl`

Smarty plugin will generate HTML code:

```
//ex.
<meta property="og:title" content="Lionel Messi: the Argentinean who makes children dream all over the world" />
<meta property="og:type" content="article" />
<meta property="og:url" content="http:/newscoop.dev/en/may2013/sports/80/Lionel-Messi-the-Argentinean-who-makes-children-dream-all-over-the-world.htm" />
<meta property="og:site_name" content="The New Custodian" />
<meta property="og:locale" content="en" />
<meta property="og:description" content="Malorum prompta maiestatis ius at, vim movet cotidieque ei. Erroribus torquatos vel et, pri nostro causae gubergren id. Per ut cetero laoreet recteque, cetero lucilius phaedrum his at" />
<meta property="article:section" content="Sports" />
<meta property="article:author" content="Amerigo Vespucci" />
<meta property="article:published_time" content="2013-05-02 08:17:08" />
<meta property="fb:app_id" content="499467366771848" />
<meta property="fb:admins" content="123422,234223432,234234234,23423423" />
<meta property="og:image" content="http://newscoop.dev/images/cms-image-000000124.jpg" />
```

More about Open Graph tags [here](https://developers.facebook.com/docs/opengraph/howtos/maximizing-distribution-media-content/).

Plugin in action:
-------
When you enter an article edition in Newscoop, plugin will automatically look into database and check if there are already informations about that article, if not then it will connect to Facebook Graph API and download all necessary informations. Next, informations will be inserted into database.


To simply clear article cache on Facebook, just click `Clear article cache on Facebook` button.
After you click It, proper message will show up (look at **Screen 2**).

If connection to Facebook success, status message on **Screen 1** will show up.

If for some reasons connection to Facebook won't be possible, we will see error message (look at **Screen 3**)

![Screen 1](http://i42.tinypic.com/30k65x0.png)

**Screen 1:** General Plugin view.

![Screen 2](http://i42.tinypic.com/2qve24x.png)
**Screen 2:** Connecting message after button click.

![Screen 3](http://i42.tinypic.com/6tp9nl.png)
**Screen 3:** Connection to Facebook failed - status message.


License
-------

This bundle is under the GNU GPL v.3. See the complete license in the bundle: [LICENSE.txt](https://raw.github.com/newscoop/plugin-NewscoopFacebook/master/LICENSE.txt)

About
-------
FacebookNewscoopBundle is a [Sourcefabric o.p.s](https://github.com/sourcefabric) initiative.