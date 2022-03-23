# **Longhand** #
Longhand is a python notebook and associated Blender python (bpy) scripts that, combined, takes individual plain text transcriptions of a text corpus and return an immersive visualization for use in [Mozilla Hubs](https://hubs.mozilla.com/). Longhand allows non-technical end users to explore unwieldy text corpora early in the research lifecycle. 

![throughput diagram](https://images.squarespace-cdn.com/content/v1/532b70b6e4b0dca092974dbe/1627401430752-R7H10DTUUOSB4GKDDKD1/Longhand+Throughput_Cook2021.png?format=2500w)

Longhand takes as input plain text transcription files (e.g. .txt) of the sort generated by Mike Hucka's [Handprint](https://github.com/caltechlibrary/handprint) tool. Those individual transcriptions represent the textual (including handwritten) contents of digital images. Emerging big-tech OCR APIs to, like Microsoft's [Read API](), can transcribe such images with a high degree of accuracy, although manual analysis of the resulting plain text is still required. 

Beginning with the notebook script ("Longhand_notebook"), Longhand combines individual image transcriptions into a single plain text ["bag of words"-type](https://en.wikipedia.org/wiki/Bag-of-words_model) document. That document is then subjected to natural language processing, via [SpaCy](https://spacy.io/) where a researcher can customize the script to specify target parts-of-speech (e.g. nouns) or [named entity types](https://github.com/mchesterkadwell/named-entity-recognition), like people, objects, or locations. 

Once the bag-of-words has been parsed by sub-type, the x most common words are added to a dictionary of lists, in order, based their relative frequency in the transcribed corpus. That frequency - represented as a percentage - is included in a second output document along with urls, specific 3d model names, and UIDs, all generated via the [Sketchfab API](https://sketchfab.com/developers/data-api/v3)

### Usage
Customize "declarations" and "input/output" lines in the [Longhand_notebook.ipynb](https://github.com/Cook4986/Longhand/blob/main/Longhand_notebook.ipynb) to generate bag-of-words and "objects" documents in the target working directory. The notebook terminates with a terminal command that will launch Blender and run the first of three Blender Python ("bpy") scripts, [Longhand_downloader.py](https://github.com/Cook4986/Longhand/blob/main/Longhand_downloader.py). Once the Blender GUI launches, and the scene is populated with 3D models, run the [Longhand_aligner.py]() and [Longhand_exporter.py](), in sequence, to generate a binarized [.GLB]() file, which can be uploaded to Mozilla Spoke as an interactive Hubs scene. 

### Innovations
* Supports “raw” input data, at scale (HTR)
* Leverages large 3D asset collections (Sketchfab)
* Exposes text-centric fields to the benefits of XR
  * Depth of field
  * Embodied interactivity
  * Sense of scale
### Limitations
* Best for nouns (i.e. things) in the corpus
* Proprietary HTR (Amazon, Google, Microsoft)
* Model placement in scene is unsolved 
### Next Steps
* Link with [SAEF repo](https://github.com/Cook4986/SAEF_OCR)
* Automate model distribution in Blender 
* Automate GLB file hosting for Hubs
### Core Technologies
 * [HandPrint](https://github.com/caltechlibrary/handprint)(version: 1.5.1)
 * [SpaCy](https://github.com/explosion/spaCy)(3.2.1)
 * [Sketchfab data API, V3](https://docs.sketchfab.com/data-api/v3/index.html)
 * [Blender](https://www.blender.org/)(3.0.1)
 * [Blender 3.0.1 Python API](https://docs.blender.org/api/current/index.html)
 * [Mozilla Hubs](https://github.com/mozilla/hubs)
### Further Reading
...

Matt Cook (mncook.net)- 2022
