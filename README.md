# Video embed for YouTube (and Vimeo)

ProcessWire Textformatter module that enables translation of YouTube or Vimeo URLs 
to full embed codes, resulting in a viewable video in textarea fields you apply it to.

*If upgrading from a 1.x version, please see the “How to upgrade” instructions in this
document as there have been significant changes to the module.* 

## How to install

- Copy the module files into directory /site/modules/TextformatterVideoEmbed/

- Click “Modules > Refresh” in ProcessWire Admin. Click *install* for the module labeled:
  “Video embed for YouTube (and Vimeo)”.

- Now you will be on the module config screen. Please make note of the config options 
  and set as you see fit.


## How to upgrade (1.x to 2.x)

If upgrading from a 1.x version of this module to a 2.x version, please note that the module
has largely been rewritten and uses a different database structure. I recommend the following
steps to upgrade: 

1. Uninstall the old version of this module.
2. Replace its files (in /site/modules/TextformatterVideoEmbed/) with those from this version.
3. Proceed with the “How to install” instructions. 

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
  
## How to use

- Edit your *body* field in “Setup > Fields” (or whatever fields you will be placing 
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

This module uses YouTube and Vimeo oEmbed services to generate the embed codes 
populated in your content. After these services are queried the first time, the 
embed code is cached so that it doesn't need to be pulled again. 

The advantage of using the oEmbed services is that you get a video formatted at 
the proper width, height and proportion. You can also set a max width and max 
height (in the module config) and expect a proportional video. 

## Configuration

You may want to update the max width and max height settings on the module
configuration screen. You should make these consistent with what is supported 
by your site design. 

If you change these max width / max height settings you may also want to check 
the box to **clear cache**, so that YouTube/Vimeo oembed services will generate 
new embed codes for you. 

### Using with Markdown, Textile or other LML

This text formatter is looking for a YouTube or Vimeo video URL surrounded by 
paragraph tags. As a result, if you are using Markdown or Textile (or something 
else like it) you want that text formatter to run before this one. That ensures 
that the expected paragraph tags will be present when TextformatterVideoEmbed 
runs. You can control the order that text formatters are run in by drag/drop 
sorting in the field editor.

------
Copyright 2021 by Ryan Cramer

