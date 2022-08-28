# Interview 9-24-21
* not married to any idea in particular -- let creative people do their thing
* let it be wearable, keep weight down
* start with COTS in first go around bc of supply chains
	* work our way to custom PCB, but crawl before walk
* INVITED TO VETCON!!! WOOOOO

## Answers to Capabilities 
* Goalposts:
	* i would like to have SW done by the end of next semester, bc defcon is done by August
	* shoot for 2 months lead time for sw and hardware finalized
	* end of this semester at least like SW design finalized
	* what it does, components, and general structure to software
	* have hardware in "quick cement"
* Add them to slack channel -- maybe link up every once in a while, doesn't have to be a weekly thing. Every other week is at most.
	* Every 2-3 weeks is sufficient.
	* Every second session can be timed in with check-in zoom on their thing. 8pm Eastern Sat Night.
	* first session is q&a w/ mini-presentation
* Any time we design anything -- shoot for cheapest thing possible.
	* want to have something be around $50 price tag. Start with benchmark of 50 dollars. It's comfortable for everyone to purchase one.
	* Balance features with cost.
	* not gonna have a problem with saying "incorp. features is impossible + valid explanation"

### Required

#### An OS
* enough to do firmware controll/support for features
* EE Prom metal style stuff is what came to mind

#### p2p networking
* wireless comm is EXTREMELY noisy -- lots of EM is in the air.
* thinking about IR bc wifi and bluetooth is gonna be so jammed/noisy
* BADGE to badge communication -- make a network to allow the badges to talk to each other
	* just communication do a possibly  "MESH" networking thing
	* rip protocol? fun games based on "crowds" of badges. exchange of something.

#### pc interface
* 
#### battery
* min amount of recommended sleep - 3 hours, enough time to plug in, sleep, unplug, go about your day
* shoot for 21 -- keep within weight and size alternatives
* run the badge off of USB, to allow power banks to power it.
* emphasis on latitude for creativity -- give leeway to work fun stuff into the design. Didn't want to railroad us into one "design" -- be creative and have fun.
 
#### usbc interface
* USB-C charge and data

#### dimensions
* typical -- govt contract or something
	* fudge room built into the contract : these are the reqs, but if you go over this (this is the threshold)
	* 10 percent deviation in mind for all specifications.
	* 20 percent on dimensions -- jeff
	* 10 percent on cost, weight 
* I can do ---this--- however, "X" parameter makes me tight. Can we do a tradeoff? 
#### mass

#### landyard attach pt

#### vetcon branding
* vetcon has some parameters, loose "collective" of guys
	* whiskeyhacker -- head honcho
	* logo is from his company, but we haven't had a chance to get a relay yet.
	* no design and branding guide as of yet, but will keep us posted
* Semper Disco -- our key motto "Always Learning:
* All veterans (not necessarily US vets, but vets).
* Stencil Fonts -- but keep in mind stencil sucks in small print (arial/helvetica fonts).
* camo can be cheesy, but hey, it is veteran related

### Desired/Add
side note: they seem to prefer piZero or anything 

#### display
* see attached link
* text displays only -- maybe potentially be able to display text based ascii art
* mayyybe ncurses? vs X-window system. 

#### wlan
* already discussed this
#### mesh

#### config led light
* cadillac night-rider-esque
* patterns/flashing 
 
#### user addons
* jeff: "crappy add on spec" -- defcon has their own defined spec/standard
* 6-pin style: v1.69 standard

#### puzzle game for acheivements
* commonalities: puzzles are related to infosec
	* a lot of them are related to cyphers, or grab a "flag" somewhere.
	* warn us ahead of time: (people) they're going to DUMP the badge firmware, obfuscate your strings. Hackers -- this is what people are going to do.
	* defcon involves different discplines, always a logic/hardware hack that involves decoding or something. tripping mag switches or shorting pins to solve a "challenge".
	* try and draw from different disciplines of tech/sectors 
	* make it a low level challenge.

ONE LAST NOTE: ABLE TO DO A MEM RESTORE

Licensing:
OUR IP -- full credit for SW/HW
we just want to be able to use it and hack it!

Branding belongs to vetcon though
BSD 3-clause is what they had in mind
