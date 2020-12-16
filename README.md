# Wikipedia-template
This repo contains the necessary scripts and documentation for creating Wikipedia templates of WikiPathways content.

## Introduction
An interactive pathway map template for Wikipedia has been developed that can be used to create pathway-specific maps that can be transcluded into relevant Wikipedia pages. Interactive pathway maps have clickable nodes which link to either Gene Wiki pages, or other public resources. Maps can be transcluded as a whole, or gene-focused subsets of pathways can be trasncluded. 

Main template: https://en.wikipedia.org/wiki/Template:Interactive_pathway_maps

The collaborative design of the template, which is actually a set of nested templates with an image map at the core, was initially proposed and refined in collaboration with Gene Wiki and MCB. 

### Usage examples
* Example template for a specific pathway: https://en.wikipedia.org/wiki/Template:TCACycle_WP78
* Full pathway template transcluded into a Wikipedia article: 
* https://en.wikipedia.org/wiki/Citric_acid_cycle#Citric_acid_cycle_intermediates_serve_as_substrates_for_biosynthetic_processes
Gene-centric subset of pathway template transcluded into a Wikipedia article: https://en.wikipedia.org/wiki/Alpha-Ketoglutaric_acid#Interactive_pathway_map

## Creating a pathway template

### Export pathway from PathVisio
* Install and launch [PathVisio](https://pathvisio.github.io/downloads).
* Go to **Plugins>Plugin Manager** and install the **WikiPathways plugin** and the **HTML export plugin**. 
* Open **Plugins>WikiPathways>Search** and find the pathway of intertest by searching for its title, WPID or gene content.
* With the pathway open in PathVisio, go to **File>Export**. Select **HTML with backpages** from the **File Format** menu. 
* The output is an html file, and a folder named **backpage** with individual html files in it. 

### Run the GeneWiki parser

The GeneWiki-parser.pl script parses human pathway output from PathVisio in html format into the [MediaWiki ImageMap format](http://www.mediawiki.org/wiki/Extension:ImageMap). It also changes hyperlinks, so that any Entrez ID links to the corresponding Gene Wiki entry using the [BioGPS portal](http://plugins.biogps.org/cgi-bin/wp.cgi?id=). Hyperlinks for other IDs are changed to point to the corresponding entry after the pathway template is created at Wikipedai (see instructions below). 

* Make sure you have Perl installed. MacOSX has Perl preinstalled, otherwise get it [here](https://www.perl.org/get.html). 
* Download the GeneWiki parser from this repo and place it in the same directory as the exported html.
* Run the parser script from command line by typing "perl GeneWiki-parser.pl".
* The output is a text file with imagemap and wiki template syntax, with the added extension ".txt".
* For problems with running the script related to your Perl installation, see Troubleshooting below.

### Upload the pathway image to Wikimedia Commons

The interactive pathway template relies on a figure of the pathway, which has to be uploaded to Wikimedia Commons. 

* Create an account at Wikipedia. This account will also work at Wikimedia Commons. 
* Go to [Wikimedia Commons](https://commons.wikimedia.org/wiki/Main_Page) and make sure you are logged in.
* Click the **Upload** button on the front page and select the pathway image from the html export. Click **Continue** once the file is uploaded.
* Under **Release Rights** select **This file is not my own work**. 
* For **Source** add the WikiPathways URL for the pathway, for example http://www.wikipathways.org/index.php/Pathway:WP78
* Under **Author** list the authors from the pathway page at WikiPathways. 
* Select the **Creative Commons CC0 Waiver** for license.
* Click **Next** and for **Description** add a one-sentence description of the pathway, for example "The citric acid cycle, also known as the tricarboxylic acid cycle (TCA cycle) or the Krebs cycle. Produced at WikiPathways."
* For **Title**, make sure the filename corresponds to this format "PathwayName_WPID.png", for example "TCACycle_WP78.png". 
* Under **Date** enter the original creation date of the pathway from WikiPathways. This is available in the **History** on the pathway page.
* Under **Categories** you can add categories relevant to the pathway topic, to make the file easier to find. For example, "Citric acid cycle", "Biochemistry diagrams", "Images from WikiPathways", "Metabolic pathways", "Homo sapiens".
* Click **Publish**

### Create template at Wikipedia

* Navigate to Wikipedia and make sure you are logged in. 
* To create a new page for your template, first decide on a title/URL based on the convention for existing pathway templates. For example, the template for the TCA cycle pathway, with WP id WP78, has the URL https://en.wikipedia.org/wiki/Template:TCACycle_WP78. 
The URL should be formatted as Template:PathwayName_WPID.
* Once you decide on a URL, simply paste it into the URL field of your browser. You should get a message saying that the page doesn't exist, and there should be a link for **Start the Template:PathwayName_WPID page.**. Click this link.
* In the edit field, paste in the contents of the text file generated from the GeneWiki parser. Describe your edits and click **Publish**.

The imagemap needs some updates before it is ready to use. The goal is to have as many links as possible link to Wikipedia articles, instead of external links. The script attempts to do this, but is not always successful.
Data nodes in the template are displayed in different colors depending on the type of link (blue=internal, green=external, red=missing). In addition to updating the actual link, the link color also needs to be updated. Finally, highlight references need to be updated as well. 
* Click **Edit** on the newly created template, and follow the instructions in the checklist at the top, also listed here: 
#### Update link ####
* Look for links to external resources, for example **HMDB**: `[http://www.hmdb.ca/metabolites/HMDB0001201 Go to HMDB]` for **Guanosine diphosphate**.
* Try to locate appropriate Wikipedia article: **https://en.wikipedia.org/wiki/Guanosine_diphosphate**. To update the link to an internal Wikipedia link, simply replace the external URL with the last part of the Wikipedia URL, `Guanosine_diphosphate`, switch the square brackets to double square brackets, and add a `\` symbol between the link and the link title, like this: `[[Guanosine_diphosphate|Go to HMDB]]`
* Repeat the above setps for any `search for` link.
#### Update link color ####
* To update the highlight color, first locate the `annotation` rectangle in the template that corresponds to the coordinates of the `rect` object where the link is defined. For example `rect 451.54940095851265 725.8886391664189 482.54940095851094 740.2596412986151 [[Guanosine_diphosphate|Go to HMDB]]` corresponds to `{{Annotation|0|0|[[<div style="display:block; width:30.9999999999983px; height:0px; overflow:hidden; position:relative; left:451.54940095851265px; top:725.259641298615px; background:transparent; border-top:3px green solid"></div>]]}}`. Searching for the first coordinate in the `rect` object works because it corresponds to the left coordinate of the `annotation` object. Switch the link color to `blue`.
#### Update reference highlighting ####
* Locate the annotation reference highlighting by searching for the original identifier of the node, for example `HMDB0001201`. For each mention, replace the identifier with the Wikipedia name, for example `Guanosine diphosphate`.

* Note that sometimes an entity is present more than once in the template, which is seen as more than one `rect` element and highlight references in the format `HMDB0001201_alt1`. In these cases, each entity needs to be updated in terms of the link, link color and highlight references.
* Consider modifying the `|Description=` entry at the very bottom of the template to provide a more descriptive pathway name.

### Troubleshooting

The Perl script requires some modules/packages that may not be present in your local installation. In that case, you might get errors while running the script like "Can't locate Switch.pm in @INC (you may need to install the Switch module)". 
* To install Perl modules, start cpan by typing the command `cpan` in Terminal. This will open the cpan prompt.
* At the cpan prompt, type `install Switch` (substitute Switch for the missing module).
* If you don't have write permissions for the Perl system directory, the install command may fail. If so, try manually changing the permissions for the relevant Perl directory (should be evident from the error message) by going to that directory in the **Finder** and using **Get Info** to change permissions.

