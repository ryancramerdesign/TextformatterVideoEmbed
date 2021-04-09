# Video embed for YouTube (and Vimeo)

ProcessWire Textformatter module that enables translation of YouTube or Vimeo URLs 
to full embed codes, resulting in a viewable video in textarea fields you apply it to.

*If upgrading from a 1.x version, please see the “How to upgrade” instructions in this
document as there have been significant changes to the module.* 

## How to install

1. Copy the module files into directory /site/modules/TextformatterVideoEmbed/

2. Click “Modules > Refresh” in ProcessWire Admin. Click *install* for the module labeled:
   “Video embed for YouTube (and Vimeo)”.

3. Now you will be on the module config screen. Please make note of the config options 
   and update as you see fit.

## How to upgrade (1.x to 2.x)

If upgrading from a 1.x version of this module to a 2.x version, please note that the module
has largely been rewritten and uses a different database structure. I recommend the following
steps to upgrade: 

1. Uninstall the old version of this module.
2. Replace its files (in /site/modules/TextformatterVideoEmbed/) with those from this version.
3. Proceed with the “How to install” instructions starting from step #2 (above). 

Upgrade notes: 

- It is not necessary to remove the TextformatterVideoEmbed selection from any
  existing fields, as it will remain with those fields and continue to work after the module 
  is re-installed. 

- After you have upgraded, double check that existing videos are working and output how you 
  want, as significant changes have been made in this version. 
  
- The max width/height settings have been dropped in this version and replaced with a 
  "Max size" selection of predefined resolutions. 

- A new "Aspect ratio" setting has been added. Most will want to either leave this at the 
  default/auto setting or select the 16:9 setting.   
  
## Where to use  

- Textarea field using CKEditor. This is the most common use case.  

- URL or Text field containing only a YouTube or Vimeo URL. In this use case, the URL 
  should not be accompanied by any additional markup or text. 
  
- Textarea field containing HTML markup, whether starting that way or formatted that way
  as a result of another Textformatter module like Markdown. Note that the Video Embed
  Textformatter should be applied only after the value is formatted to HTML markup. 
  For example, if using the Markdown Textformatter, then make this Video Embed 
  Textformatter apply after the Markdown one (the order of Textformatters is sortable).

## How to use

- Edit your *body* field in “Setup > Fields” (or whatever field you will be placing 
  videos in). On the *details* tab, find the *Text Formatters* field and select 
  “Video embed for YouTube/Vimeo”. Save. 

- Edit a page using the field you edited and paste in YouTube and/or Vimeo video URLs 
  each on their own paragraph. 

### Example 

How it might look in your editor (like CKEditor): 

> Here are two videos about ProcessWire
>
> https://www.youtube.com/watch?v=Wl4XiYadV_k
>
> https://youtu.be/XKnG7sikE-U
> 
> And here is a great video I watched earlier this week:
> 
> https://vimeo.com/18280328

## How it works

The module automatically replaces video URLs from YouTube or Vimeo (such as those 
copied from the browser address bar) with the actual embedded video, so that it can
be viewed in the same spot where the URL was placed. 

This module uses YouTube and Vimeo oEmbed services to generate the embed codes 
populated in your content. After these services are queried the first time, the 
embed code is cached so that it doesn't need to be pulled again until the cache
time expires. 

Note that embed activity and errors are logged (in your admin) to: 
Setup > Logs > textformatter-video-embed. This can help you be aware of what videos
are embedded throughout your site, as well as identify videos that no longer exist or 
that have an invalid URL. 

Unless the video embed cache is set to never expire, the module performs maintenance
by removing expired video embed codes once per day. 

## Configuration

These configuration settings can be accessed in the ProcessWire admin at: 
Modules > Configure > TextformatterVideoEmbed.

### Sizes

**Max video size to request:**  
Select the appropriate video size/resolution for your website. If you aren't sure
then select 720p or 480p. 

**Aspect ratio:**  
This is the proportion of width to height that the video will use. For most 
cases you should leave this set at “Auto”. Or if you want all videos to display 
in a consistent size, then select one of the predefined aspect ratios. The most
common aspect ratio on YouTube is 16:9. 

### Embed styles

These are the style attributes applied to the wrapping element and iframe used 
by the video embeds. The default styles enable the video to display responsively
and fill the available space proportionally. Note that the `{pct}` placeholder
in these styles is dynamically replaced with a percentage of the video
proportion to ensure that it displays at the correct height. If you don't want 
any margin between videos, remove the `margin:1em 0;` style from the “Wrap Styles”.
If you prefer to apply these styles from your own CSS stylesheet then you may 
remove them from here, but you should leave the `padding-bottom:{pct}%;` style
in the “Wrap styles” since it contains a percentage that can change for every
video. 

### Fail action

If YouTube or Vimeo returns an error for a video embed request then the video URL in
the content will not be converted to a video player and instead will be left in the 
content. However, the HTTP error code will be appended to it. For example, 
`https://youtu.be/abc123` would be changed to `https://youtu.be/abc123 (404)`.
When you view the page this is an indicator to you that it's not a problem with how 
or where you pasted in the video URL but instead that the video itself is not 
recognized by the service. The URL will also be wrapped in a 
`span.TextformatterVideoEmbedError` element in case you want to style it red or 
something. If you would prefer to hide the URL instead, use the Fail action 
setting to select the second option and this will wrap an HTML comment around it.
For a custom fail action, you can also hook the `TextformatterVideoEmbed::embedError`
method in your /site/ready.php file, i.e. 
~~~~~
$wire->addHookAfter('TextformatterVideoEmbed::embedError', function($event) {
  $url = htmlentities($event->arguments(1));
  $data = $event->arguments(2);
  $error = htmlentities($data['embedCode']); // embedCode is an error code number
  $event->return = "<p class=error>Video $url is not available (error: $error)</p>";
});
~~~~~

### Cache

**Refresh time:**  
If you want the module to pull fresh embed codes every once in awhile, enter 
the number of days after which it shoule expire embed codes. This is also useful
as a period maintenance to remove old videos that may no longer be in use or 
videos that have been removed from YouTube or Vimeo. If you don't want to ever 
expire the embed codes then set to 0. 

**Clear videos:**  
This option removes all videos that are currently cached. Use this option when 
you have changed any setting in the “Sizes” section so that fresh embed codes
can be pulled with the new settings. 

**Recently embedded videos in cache:**  
This will show the most recently embedded videos in the cache. This is primarily
just informational. 

------
Copyright 2021 by Ryan Cramer

