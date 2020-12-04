# Wikipedia-template
This repo contains the necessary scripts and documentation for creating Wikipedia templates of WikiPathways content.

## Introduction
An interactive pathway map template for Wikipedia has been developed that can be used to create pathway-specific maps that can be transcluded into relevant Wikipedia pages. Interactive pathway maps have clickable nodes which link to either Gene Wiki pages, or other public resources. Maps can be transcluded as a whole, or gene-focused subsets of pathways can be trasncluded. 

Main template: https://en.wikipedia.org/wiki/Template:Interactive_pathway_maps

The collaborative design of the template, which is actually a set of nested templates with an image map at the core, was initially proposed and refined in collaboration with Gene Wiki and MCB. 

### Examples
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

### Run GeneWiki parser

Th GeneWiki.pl script parses human pathway output from PathVisio in html format into the [MediaWiki ImageMap format](http://www.mediawiki.org/wiki/Extension:ImageMap). It also changes hyperlinks, so that any Entrez ID links to the corresponding Gene Wiki entry using the [BioGPS portal](http://plugins.biogps.org/cgi-bin/wp.cgi?id=). Hyperlinks for other IDs are changed to point to the corresponding entry after the pathway template is created at Wikipedai (see instructions below). 

* Download the GeneWiki parser from this repo and place it in the same directory as the exported html
* Run the parser script from command line by typing "perl GeneWiki-parser.pl".
.....

### Create template at Wikipedia

.....


