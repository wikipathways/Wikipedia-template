# Wikipedia-template
This repo contains the necessary scripts and documentation for creating Wikipedia templates of WikiPathways content.

## Introduction
An interactive pathway map template for Wikipedia has been developed that can be used to create pathway-specific maps that can be transcluded into relevant Wikipedia pages. Interactive pathway maps have clickable nodes which link to either Gene Wiki pages, or other public resources. Maps can be transcluded as a whole, or gene-focused subsets of pathways can be trasncluded. 

Main template: https://en.wikipedia.org/wiki/Template:Interactive_pathway_maps

The collaborative design of the template, which is actually a set of nested templates with an image map at the core, was initially proposed and refined in collaboration with Gene Wiki and MCB. 

### Usage examples
Example template for a specific pathway: https://en.wikipedia.org/wiki/Template:TCACycle_WP78
Full pathway template transcluded into a Wikipedia article: 
https://en.wikipedia.org/wiki/Citric_acid_cycle#Citric_acid_cycle_intermediates_serve_as_substrates_for_biosynthetic_processes
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

* Download the GeneWiki parser from this repo and place it in the same directory as the exported html.
* Run the parser script from command line by typing "perl GeneWiki-parser.pl".
* The output is a text file with imagemap and wiki template syntax, with the added extension ".txt".

### Create template at Wikipedia

* Create an account at Wikipedia and login. 
* To create a new page for your template, first decide on a title/URL based on the convention for existing pathway templates. For example, the template for the TCA cycle pathway, with WP id WP78, has the URL https://en.wikipedia.org/wiki/Template:TCACycle_WP78. 
The URL should be formatted as Template:PathwayName_WPID.
* Once you decide on a URL, simply paste it into the URL field of your browser. You should get a message saying that the page doesn't exist, and there should be a link for **Start the Template:PathwayName_WPID page.**. Click this link.
* In the edit field, paste in the contents of the text file generated from the GeneWiki parser. Describe your edits and click **Publish**.

Now the imagemap needs some editing before it is ready to use: 
* Click Edit on the newly created template, and follow the instructions in the checklist at the top, also copied here: 
* Locate appropriate pathway article and update imagemap default link accordingly. Also consider modifying the "Description" at the very bottom of the template to provide a more descriptive pathway name.
* Check pathway for "search for" links when hovering and attempt to locate an appropriate wikipedia article. Update imagemap link, link color, and highlight references accordingly. 
* Check pathway for external links in green and attempt to locate appropriate wikipedia content instead. Update imagemap link, link color, and highlight references accordingly.


