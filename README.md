# **Longhand** #
Longhand is a word cloud generator, but the words are 3D models projected in 360 degrees around the user. Longhand allows non-technical researchers to explore unwieldy text corpora (including in VR) earlier in the research lifecycle. Longhand is an extension of Mike Hucka's [HandPrint](https://github.com/caltechlibrary/handprint) and subsequent data management efforts by Harvard Library, including the [SAEF_OCR](https://github.com/Cook4986/SAEF_OCR) project.

![throughput diagram](https://images.squarespace-cdn.com/content/v1/532b70b6e4b0dca092974dbe/3543cdec-7455-4bed-8eb4-55e7c46cb76b/Longhand_Diagram_Cook2022.png?format=2500w)

Longhand takes as input plain text of the sort generated by Mike Hucka's [Handprint](https://github.com/caltechlibrary/handprint) handwriting transcription (HTR) tool. Those individual transcriptions represent the textual contents of digital images, which are more common in many archives than full text transcriptions. Fortunately, big-tech OCR APIs - like Microsoft's [Read API](https://docs.microsoft.com/en-us/azure/cognitive-services/computer-vision/vision-api-how-to-topics/call-read-api) - can accurately transcribe such images , although manual analysis of the resulting plain text is still required. That's where Longhand comes in. 

Beginning with the notebook script ("Longhand_notebook"), Longhand inputs a plain text ["bag of words"-type](https://en.wikipedia.org/wiki/Bag-of-words_model) document. That document is subjected to natural language processing, via [SpaCy](https://spacy.io/), whereby a researcher can customize the script to specify target parts-of-speech (e.g. nouns) or [named entity types](https://github.com/mchesterkadwell/named-entity-recognition), like plants or locations. 

Once the bag-of-words has been parsed by chosen sub-type, the "x" (number of) most common words are added to a dictionary of lists, in order, based their relative frequency in the transcribed corpus. That frequency is included in a second output document ("...objects.txt" output) along with urls, 3d model names, UIDs, and ply counts, all generated via the [Sketchfab API.](https://sketchfab.com/developers/data-api/v3)

### Usage
Customize "declarations" and "input/output" lines in the [Longhand_notebook.ipynb](https://github.com/Cook4986/Longhand/blob/main/Longhand_notebook.ipynb) to generate "objects" documents in the target working directory. The notebook concludes with a terminal command that will launch Blender and run the first of three Blender Python ("bpy") scripts, [Longhand_downloader.py](https://github.com/Cook4986/Longhand/blob/main/Longhand_downloader.py). Once the Blender GUI launches, and the scene is populated with 3D models from the objects.txt doc, use [the Blender text editor](https://docs.blender.org/manual/en/2.79/editors/text_editor.html) run the [Longhand_aligner.py](https://github.com/Cook4986/Longhand/blob/main/Longhand_aligner.py) and [Longhand_exporter.py](https://github.com/Cook4986/Longhand/blob/main/Longhand_exporter.py), in sequence, to generate a binarized [.GLB](https://en.wikipedia.org/wiki/GlTF) file, which includes model textures and can be [uploaded to Mozilla Spoke](https://hubs.mozilla.com/docs/spoke-creating-projects.html) as a multi-user virtual environment. 
#### Usage Notes:
* For prose/free text visualization, use the following named entity categories list, which have a higher likelihood of corresponding (and relevant) 3D models on Sketchfab. 
  * ["PRODUCT","EVENT","FAC","WORK_OF_ART","LOC","NORP","GPE","ORG"] 
* For inventories, recipies, collections, etc., use the noun POS and customize the Sketchfab query slug declaration using one or more of the categories found [here](https://help.sketchfab.com/hc/en-us/articles/115002765883-Category-Guidelines#Cultural-Heritage-History)

### Benefits
* Supports “raw” text input data
* Represents tokens as 3D objects, which are recognizable in a cluttered scene and from novel perspectives.
* Leverages large, existing 3D asset collections (i.e. Sketchfab)
* Exposes text-centric fields to the benefits of XR, like:
  * Depth-of-field
  * Embodied interactivity
### Limitations
* Best for nouns (i.e. things) in the corpus
* Proprietary HTR (Amazon, Google, Microsoft)
* Model placement in scene is work-in-progress 
### Next Steps
* Link with [SAEF repo](https://github.com/Cook4986/SAEF_OCR)
* Upgrade model distribution function in "Longhand_aligner.py" script
* Automate GLB file hosting (AWS?) for easier Hubs integration
### Core Technologies
 * [HandPrint](https://github.com/caltechlibrary/handprint)(version: 1.5.1)
 * [SpaCy](https://github.com/explosion/spaCy)(3.2.1)
 * [Sketchfab data API, V3](https://docs.sketchfab.com/data-api/v3/index.html)
 * [Blender](https://www.blender.org/)(3.0.1)
 * [Blender Python API](https://docs.blender.org/api/current/index.html)
 * [Mozilla Hubs](https://github.com/mozilla/hubs)
### Further Reading
* ["Perceiving layout and knowing distances: The integration, relative potency, and contextual use of different information about depth"](https://www.researchgate.net/profile/James-Cutting/publication/236964257_Perceiving_layout_and_knowing_distances_The_interaction_relative_potency_and_contextual_use_of_different_information_about_depth/links/0c96051a7a988e9232000000/Perceiving-layout-and-knowing-distances-The-interaction-relative-potency-and-contextual-use-of-different-information-about-depth.pdf) Cutting & Vishton 1995
* ["Promoting rotational-invariance in object recognition despite experience with only a single view"](https://www.sciencedirect.com/science/article/pii/S0376635715300735?casa_token=RFiw0OhRdPsAAAAA:7rb-Hsu-ZnPZs2l1iwr2g61yJCY4lXp6nfRIP299JcLv7G7L8EmALA3VzYyQ910dIfLKj1lh) Soto & Wasserman 2016
* ["Studying the effects of stereo, head tracking, and field of regard on a small-scale spatial judgment task"](https://ieeexplore.ieee.org/stamp/stamp.jsp?arnumber=6261311&casa_token=101RdCpGgAgAAAAA:tW7Hjpk6IvHNIcPI1gnoxbVBMCxtnU9sNHan2L0xB36jFL_Oz_kskc49IlVyb0YBsOcC5s0) Ragan et al. 2013
* ["Evaluating the benefits of the immersive space to think"](https://infovis.cs.vt.edu/sites/default/files/WEVR2020_Lisle.pdf) Lisle et al. 2020
* [Virtual replicas of real places: Experimental investigations](https://ieeexplore.ieee.org/abstract/document/9483619?casa_token=byJ-FUFnO6kAAAAA:U6WLbgSz5wMUsxrDZezeC--BmqKY7LKTPvpDBOOO2LL2UcBmgZAZ9XHMObFTFe6dy0nDzWY) Skarbez et al. 2021
* ["Quantitative evaluation of visual guidance effects for 360-degree directions"](https://link.springer.com/article/10.1007/s10055-021-00574-7) Harada & Oyhama 2021
* ["The Sensemaking Process and Leverage Points for Analyst Technology as Identified Through Cognitive Task Analysis"](https://www.e-education.psu.edu/geog885/sites/www.e-education.psu.edu.geog885/files/geog885q/file/Lesson_02/Sense_Making_206_Camera_Ready_Paper.pdf) Pirelli & Card 2005
* ["There Is No Spoon: Evaluating Performance, Space Use, and Presence with Expert Domain Users in Immersive Analytics"](https://ieeexplore.ieee.org/abstract/document/8820171?casa_token=YmPsNHmA6bgAAAAA:01jAPRcwrGHw6EMeOROp_HnbMAIpBqv-FFmSx1f7WwQSnqJUBC7D1PCNoR4QCJv8YDEIlmM) Batch et al. 2020
* ["Space to think: large high-resolution displays for sensemaking"](https://dl.acm.org/doi/abs/10.1145/1753326.1753336?casa_token=QaujgYdz_WwAAAAA:UxZS8_ZIvM1MnJxEDre7qjy4CKk4ay4DznPaUfbM0q52MWhq6J_LsT44q-Yd-STGeX7fSwzu4Sc) Andrews, Endert, and North 2010
* ["A theory of direct visual perception"](https://monoskop.org/images/1/12/Gibson_James_J_1972_2002_A_Theory_of_Direct_Visual_Perception.pdf) Gibson 1972
* ["The Capacity of Visual Short-Term Memory is Set Both by Visual Information Load and by Number of Objects"](https://journals.sagepub.com/doi/full/10.1111/j.0963-7214.2004.01502006.x?casa_token=hz68zoEojfAAAAAA%3AXgTymvc1EPi_b5RVMoBsseOrIK31B8MsuINWI46cGw8EldYvovacJIlQIRsJ1fjEX7drHwMpYMQ) Alvarez and Cavanaugh 2004
* ["Visual spatial learning of complex object morphologies through the interaction with virtual and real-world data"](https://www.sciencedirect.com/science/article/pii/S0142694X10000128?casa_token=8P-CO_HqYmkAAAAA:YsBBDG1svWOeaylHEqazgOIdRnRLxYIxUT403mSejcle87KsRDOEypAi-LnHe8-vkFGCyzwj) Silvestri et al. 2010
* ["Peripheral vision and pattern recognition: A review”](https://jov.arvojournals.org/article.aspx?articleid=2191825) Strasburger, Rentschler, and Juttner 2010
* ["An evaluation of Depth Enhancing Perceptual Cues for Vascular Volume Visualization in Neurosurgery”](https://ieeexplore.ieee.org/abstract/document/6620865?casa_token=IvrlmZRQ-J4AAAAA:Me20NjzNmt4e6xe_6PYt51zA91yDYvY8Od1drMeYfJtX-Uo-Vjfp-U_hTkxJue1US9Q6h_s)Kersten-Pertel, Jy-Shyang Chen, and Collins 2012 
* ["A New Framework for Theory-Based Interaction Design Applied to Serendipitous Information Retrieval"](https://dl.acm.org/doi/abs/10.1145/1352782.1352787?casa_token=fuqwjzCWagwAAAAA:_89FD0Vj44ap0SMjic3dZg1DjoZUcuJCDFG5-eoD7TEQV4pQl4G1fkG2n_oZBufy3-26dlYMt24) De Bruijn & Spence 2008
* ["Untangling invariant object recognition"] (https://www.sciencedirect.com/science/article/pii/S1364661307001593?casa_token=lWMfVNGhvZ8AAAAA:4brcwp3c0TCZgmV_oDi8xCx8Ia05pP6ZZp50TIuIP3u5f_hLvCkrrX4e5YvVBDPAr5C921VQD4Or) DiCarlo & Cox 2007

### Test Images
![army_cookbook](https://images.squarespace-cdn.com/content/v1/532b70b6e4b0dca092974dbe/1660659211783-6PMQRSA5076JD9BVLOA8/ArmyCookbook1_reduced.jpg?format=1000w)
<p align="center">
    "Manual for Army Cooks" - United States War Department, 1896
</p>

![diary entries1](https://images.squarespace-cdn.com/content/v1/532b70b6e4b0dca092974dbe/1659099069651-WCYENKMCF5OOF66CXYK3/JRC_nouns.png?format=1000w)
<p align="center">
    The personal diaries of one J.R. Coolidge - 1921
</p>

![UFOs](https://images.squarespace-cdn.com/content/v1/532b70b6e4b0dca092974dbe/1660658679021-ISG6E85XE5ZKMD8LOYLB/UFO4.png?format=1000w)
<p align="center">
    Esotericism and UFO Research - Blomquist, 2017
</p>

![Boston_cooking](https://images.squarespace-cdn.com/content/v1/532b70b6e4b0dca092974dbe/1660658486299-R9RUUMYY4PDFW9CAGWYA/EvidenceLocker.png?format=1000w)
<p align="center">
    "McLennan County Sheriff's Department Inventory of Evidence Locker" - 2021
</p>

![BostonCooking](https://images.squarespace-cdn.com/content/v1/532b70b6e4b0dca092974dbe/1659098222849-RLADGE36KJTNXLQIW7E0/Boston+Cooking+School_1.png?format=2500w)
<p align="center">
    "The Boston Cooking School Cookbook" - Farmer, 1896
</p>

![Religion](https://images.squarespace-cdn.com/content/v1/532b70b6e4b0dca092974dbe/1660658664190-4UL3TUOLIOCXB1AV7PGN/Religion2_reduced.jpg?format=1000w)
<p align="center">
    Comparative religion and the religion of the future - Martin 1926
</p>

Matt Cook [mncook.net](https://www.mncook.net/)- 2022
