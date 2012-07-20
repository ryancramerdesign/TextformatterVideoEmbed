# Video embed for YouTube and Vimeo

ProcessWire Textformatter module that enables translation of YouTube or Vimeo URLs to full embed codes, resulting in a viewable video in textarea fields you apply it to.

## How to install

- Copy the TextformatterVideoEmbed.module file to your /site/modules/ directory (or place it in /site/modules/TextformatterVideoEmbed/). 

- Click *check for new modules* in ProcessWire Admin Modules screen. Click *install* for the module labeled: "Video embed for YouTube/Vimeo".

## How to use

- Edit your *body* field in Setup > Fields (or whatever field(s) you will be placing videos in). On the *details* tab, find the *Text Formatters* field and select "Video embed for YouTube/Vimeo". Save. 

- Edit a page using the field you edited and paste in YouTube and/or Vimeo video URLs each on their own paragraph. 

### Example (pretend you are pasting this in TinyMCE): 

   Here are two videos about ProcessWire

   http://www.youtube.com/watch?v=Wl4XiYadV_k

   http://www.youtube.com/watch?v=XKnG7sikE-U 

   And here is a great video I watched earlier this week:

   http://vimeo.com/18280328

## How it works

This module uses YouTube and Vimeo oEmbed services to generate the embed codes populated in your content. After these services are queried the first time, the embed code is cached so that it doesn't need to be pulled again. 

The advantage of using the oEmbed services is that you get a video formatted at the proper width, height and proportion. You can also set a max width and max height (in the module config) and expect a proportional video. 

## Configuration

You may want to update the max width and max height settings on the module's configuration screen. You should make these consistent with what is supported by your site design. 

If you change these max width / max height settings you may also want to check the box to **clear cache**, so that YouTube/Vimeo oembed services will generate new embed codes for you. 

