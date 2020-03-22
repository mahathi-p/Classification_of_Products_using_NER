# Classification of Flipkart Electronic Products using Named Entity Recognition

#### To create a NER model for the classification of various electronic office products

### 1. Data

As there is no a proper dataset, data was scraped from the flipkart website. For most of the products the entities were taken as those features listed along with the product. These entities included Brand Name, Model, RAM size, Capacity(harddisk), HDMI(monitors) and so on. Some entities were extracted from the Product Name. For example, the first word of each Product Name as the Brand.

The data of the following was scraped:
- Laptops
- Monitors
- Printers
- Harddisks

The data is cleaned and saved in separate csv files for each product where the various coloumn represent the entities(features). These are found in the folder /csvfiles.

![Alt text](/images/sample_laptop_data?raw=true "Optional Title")

### 2. Preparing the Data for NER

In order to use the Spacy NER model, the training data has to be given in a particular format shown below.
 
     train_data =             
                   [

                    ("content 1", entities : {
                            [(start,end, "TAG 1"), (start,end, "TAG 2"), (start,end, "TAG 3")]
                            }),

                    ("content 2", entities : {
                         [(start,end, "TAG 1"), (start,end,"TAG 2")]
                         }),

                    ("content 3", entities : {
                        [(start,end, "TAG 1"), (start,end, "TAG 2"), 
                        (start,end,"TAG 3"),(start,end, "TAG 4 ")]
                        })

                   ]


For this, the data had to tweaked with to get the 'content' in the format. The entities are present in the data. The approach taken for this was to jumble the entities and create a complete Product Name as the content in the training data. Also, now the entities had to annotated with their start and end points. The data in this format is made and stored in json format. The code for this step and the obtained files are in /create_train. 

![Alt text](/images/sample_laptop_train_data?raw=true "Optional Title")

    train_data = 
                [
                    ('Ideapad Intel Core i3 Processor (7th Gen) 64 bit Windows 10 Lenovo Laptop 39.62 cm (15.6 inch)  4 GB DDR4  1 TB HDD',
                      {'entities': [(0, 7, 'Model'),
                        (8, 41, 'Processor'),
                        (42, 59, 'OS'),
                        (60, 66, 'Brand'),
                        (67, 73, 'Category'),
                        (74, 95, 'Dim'),
                        (96, 106, 'RAM'),
                        (107, 115, 'Disk')]}) 
                        
                        ......
                        
                  ]




### 3. Training the NER model

A blank Spacy model was created and the entities are updated with the entities extracted above. 
In order to check if the Spacy Model was working, first entities of the Laptop were updated and test. This code can be found in /train_NER/Laptop.ipynb






