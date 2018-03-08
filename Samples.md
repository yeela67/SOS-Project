< [Home](/README.md)

# Samples

## Book object partial code
```python
from bs4 import BeautifulSoup as beaut_soup
import os
import zipfile

"""
Creates a Book object from an epub file.
"""
class Book:

    def __init__(self, epub):

        # Example inside of an epub
        # mimetype
        # META-INF/
            # container.xml
        # OEBPS/
            # content.opf
            # title.html
            # content.html
            # stylesheet.css
            # toc.ncx
            # images/
                # cover.png

        # Instance variables unique to each instance
        self.root_file_path = ''
        self.root_file_OPF = None
        self.opf_directory = ''

        self.metadata = dict()
        self.manifest_items = dict()
        self.reading_order = list()
        self.base_xml_files = list()
        self.toc = None
        self.toc_navPoints = list()
        self.chapter_links = list()

        # unzip the epub file
        self.book_file = zipfile.ZipFile(epub)

        # parse the container.xml file in the META-INF directory
        meta_container = beaut_soup(self.book_file.read('META-INF/container.xml'), 'xml')

        # finds the path to the "root file"/the opf of the book
        rootfile_element = meta_container.find('rootfile')
        self.root_file_path = rootfile_element.get('full-path')

        # parse the OPF file
        self.root_file_OPF = beaut_soup(self.book_file.read(self.root_file_path), 'xml')

        # get metadata
        self.__extract_metadata__()

        # getting book content
        self.__extract_manifest__()
        self.__extract_spine__()
        self.__getOPF__()
        self.__extract_xml_files__()
        self.__extract_chapter_links__()
```

## Screenshots
### Regular Mode
![alt text](https://github.com/yeela67/SOS-project/raw/master/screenshots/regular.PNG "Regular")

### Solarized Light Mode
![alt text](https://github.com/yeela67/SOS-project/raw/master/screenshots/solarizedlight.PNG "Solarized Light")

### Solarized Dark Mode
![alt text](https://github.com/yeela67/SOS-project/raw/master/screenshots/solarizeddark.PNG "Solarized Dark")
