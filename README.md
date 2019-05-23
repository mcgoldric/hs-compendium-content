# Hades' Star Compendium Content

This repository contains the textual elements of the content for the Hades' Star Compendium App.

I am making the files available here so that the community can contribute to the content directly. Existing content can 
be updated, expanded, and translated. You can also contribute new data by adding files.

## How to Contribute
In order to contribute here, you will need to have a GitHib account.
1. Create a GitHub account or log in to your existing GitHub account.
2. Fork this repository (this only needs to be done once). This will create a copy of all of the files into your GitHub account. You will find the Fork button on the top right of the page.
3. Edit or Create files in your copy of the repository. When you save the files, select the option to create a new branch and submit a pull request. This will signal to me to merge your changes into the master copy. You can perform multiple edits and add them you the same branch/pull request. Files can be edited and created directly in the GitHub user interface. 

If you wish to contribute a new file (topic), create the new file in the folder that you think is most appropriate. Don't worry about adding it to an index file, as I will review it and add it appropriately. See the file format section below.


## File Formats
The files included here are in YAML format. YAML is a text format that is easy to read and edit. The most important thing 
to remember is that indentation in the file is significant, and columns must line up correctly.

There are two file types in this data: index files and page files. Don't worry about index files.

Page files consist of header information and content. A typical page file looks like:

```yaml
title: Transport Ship
subtitle: Trusty Courier
type: page
icon: icons/ships/Transport_lv5_rot.png
headerImage: artwork/transport.jpeg
content:

  - type: text
    text: >
      Transport ships are crucial for trade. Use them to deliver shipments between planets and moons,
      and to transfer Artifacts from Red Stars.
  -
    type: text
    text: >
      Transport ships are also used to retrieve Relics from White Stars.

  - type: excel-table
    filename: tables/ships.xlsx
    sheet: Transport
```

### Header Fields
#### title and subtitle
  - These are just what the name implies, but subtitle, while required, is not currently used in the app. For now I put
  the same values in both fields
  - Both of these fields support translations (see below).
#### type
  - Should always be `page`.
#### icon and headerImage
  - These refer to image files used in the app. Leave them alone. If you are submitting a new page you can indicate the file 
  in this field and include the file in your pull request, by adding it to the images folder.
#### other header fields
  - You may see other header fields. You can ignore them. You can feel free to add a comment field to the header, for
  ongoing comments or other info that will not appear in the app.

### Content Fields
All content appears within the `content` field as a list of sub-items.

All content entries must start with a `-` at the first indent level, and contain a `type` field.

### Content types
#### text
  - This is the most commonly used field type. After the `type: text`, the content must contain a `text` element which contains the textual content. 
    - If the first character is `>` (most common) then the text will automatically be formatted into paragraphs, and single line breaks will be ignored. This is useful to make the file readable. A blank line in the text will 
  indicate a paragraph break
    - If the first character is '|' then line breaks will be respected in the output. This is useful for creating lists.
    - The text field is translatable. If translations are provided, the content will appear as sub-items to the text item (see below).
    ##### Examples
       ```yaml
          - type: text
            text: >
               This is long breaking text that will form as single paragraph. The line break
               here will be ignored in the output
          - type: text
            text: |
               This is text which will retain its line breaks in the output.
               This will always be on its own line.
          - type: text
            text:
              en: >
                 This is a text translation. This is the english version.
              fr: This should be in French. Since its short I didnt use a line break specifier.
              de: --OMIT--
              es: > 
                This should be Spanish. This entry will be ignored in the German translation
                because the translation is set to --OMIT--
    ```
    
#### title and attrib
  - Requires a `text` element.
  - This is similar to `text` and works the same way, but will be formatted accordingly. 
  - Titles should be short text that fit on a single line (e.g. should not require `>` or '|')
  - `title` and `attrib` are translatable
  - `attrib` is used for attribution and usually follows another element. 

#### image
  - Requires an `image` element which is the path to the image file relative to root.yml.

#### excel-table
  - Requires a `filename` relative to root.yml for the excel file
  - Requires a `sheet` which is the name of the tab in the excel sheet.
  - All rows which do not have an empty/blank A column will be included.
  
#### prop
  - This indicates a named property, and will be displayed as a name/value pair in the app.
  - Required fields are `name` and `value`, both are translatable.
  - Example
     ```yaml
        - type: prop
          name: 
             en: Speed
             fr: La Vitesse
             es: Velocidad
          value: 60 AU/m
     ```
#### Other
  - You may notice other field types. They should probably be ignored, but if a special case
  arises, please let me know.
 
 ## Translations
 Several field types are translatable. These include `title` and `subtitle` in the header, and `text`, `title`, `attrib` and `prop` types in the content.
 
 Translatable fields should contain either the english language default text as a direct element:
 
 ```yaml
       title: An Untranslated title
       content: 
         - type: text
           text: This is an untranslated content entry.
         - tyle: text
           text: >
              This is a multiline unstranslated entry. This will
              be combined to a pararagraph.
            
              This will be a second paragraph.
```
     
or a list of translations keyed on the 2 letter language ISO code:
     
```yaml
       title:
         en: A Translated Title
         es: Un título traducido
       content:  
         - type: text
           text: 
             en: This is an translated content entry.
             fr: Ceci est une entrée de contenu traduit.
             es: Esta es una entrada de contenido traducido.
         - tyle: text
           text:
             en: >
               This is a multiline untranslated entry. This will
               be combined to a paragraph.
            
               This will be a second paragraph.
             es: >
               Esta es una entrada multilínea sin traducir. Esto se 
               combinará en un párrafo. 
             
               Ese será un segundo párrafo.
```
     
When a transaltion is missing a specific language, as French is missing in the second text entry above, the English language translation will be subsitituted.
     
  
