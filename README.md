# Convert Classic Esri Story Map Series

This repo contains a Jupyter Notebook and *.py sidecar file that can be used in ArcGIS Online Notebooks to convert a Classic Esri Story Map Series (tabbed, bulleted or accordion) to a set of ArcGIS StoryMaps and then combines them into a ArcGIS Collection.

**What the notebook does**  
- Fetch JSON from an ArcGIS Online hosted Classic Esri Story Map Series App 
- Convert each tab/bullet/accordion into its own ArcGIS StoryMap with the cover supressed
- Uses the BeautifulSoup library to parse description.html from the side panel text and convert to StoryMap objects
- Identifies the main stage media type and converts each to the corresponding StoryMap object 
- Once converted, each ArcGIS StoryMap will need to be opened in a browser tab in order to complete the Story Checker 
- Once all are published, an ArcGIS StoryMap Collection is created that contains the converted app to replicate the classic app look and feel
- Note: Any entries that were hidden in the classic app will be published and will be visible by default. 
- If it is desired that they not appear they can be removed from the Collection after publishing 
- Also, as there is no AGSM Collection equivalent to the accordion layout, these layouts will be converted to the Tabbed format.
