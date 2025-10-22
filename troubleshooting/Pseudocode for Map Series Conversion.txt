# Pseudocode for Map Series Conversion

Get Classic Story id as input
Fetch Classic Story JSON
Parse title, subtitle?, settings, and data
Parse the "entries" list from data to get the tabs/bullets/sections
Parse the theme data (currently only using light/dark for summit/obsidian)
for each entry:
    parse the title of the entry
    create a new Story() object
    assign the theme
    create a Sidecar() object
    add the Sidecar to the Story
    parse the type of content from the main stage that will become the Sidecar media (i.e. webmap, image, video, embed, etc. Account for all types)
        Each main stage content requires its own handler
        We will create AGSM objects for each type
        Also create a thumbnail from the main stage content to be assigned to the Story cover page. This will serve as its thumbnail in the Collection
    fetch the description as html from the side panel
    parse the description with Beautiful Soup
    convert each part of the description html into StoryMap objects/nodes, preserving any styling as much as possible
        for paragraphs, create a Text() object
            ensure <a> tags, text color and formatting are included
        for pictures, create an Image() object
            assign metatdata to the Image() object (i.e. alt_text, caption, hyperlink)
        for maps, create a Map() object
    create a Text() object to story all of the side panel nodes
    use the .add_slide() method to add the main stage media and side panel content to the Sidecar
        *TODO check for layout settings (side panel on left/right side, panel width, etc.)
    if the main stage content was a map, we can now configure its settings. This must be done AFTER the map is added to the story
        parse extent, layer visibility (anything else?) and assign to Map()    
    set the Story cover properties
        title, byline, date, media=thumbnail
        As the Cover class does not include a setting to hide the cover, we hide it by adding the 'config' key to the Cover json
        `for k,v in story.properties['nodes'].items():
            if v['type'] == 'storycover':
                v['config'] = {'isHidden': 'true'}`
    save and publish the Story()
    fetch the new Story() Item()
    auto (or manual) launch the Story in a browser to complete the publishing process and check for errors
after all entries are created:
check for successful publication by fetching each Item() object
fetch the Classic Story's thumbnail from its item page
create a Collection() object
use the collection.add() method to add each entry to the collection
assign the classic story's metadata to the Collection
    title, byline, theme, date?
    style - use 'tab' or 'bullet' and convert 'accordion' to 'tab'
    media - assign the Classic story's thumbnail to the Collection(). NB: This is not currently working, likely due to how the builder creates the Collection thumbnail as a grid from the entries
Save and publish the Collection
auto (or manual) launch the Collection to check for errors

Note - any entries that were hidden in the classic story will be converted and added to the Collection. They can be removed using the builder if desired.