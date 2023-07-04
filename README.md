
# nft-generator-py

nft-generator-py is a python based NFT generator which programatically generates unique images using weighted layer files.

## Usage
As of v2.0.0, nft-generator-py will use the argparse library in order to support external configuration files and won't require users to interact with the python files themselves.

1. Install requirements: `python3 -m pip install -r requirements.txt`
2. Make a configuration JSON file. See the configuration section below for specifications.
3. Add layer files into the `/images` folder.
4. Run the command `python3 generate.py --amount AMOUNT --config CONFIG`
   
   where:
   1. `AMOUNT` is the amount of images to generate
   2. `CONFIG` is the path pointing to a `.json` file containing valid program configuration.

## How it works
- A call to `generate_unique_images(amount, config)` is made, which is the meat of the application where all the processing happens.
- The `config` object is read and for each object in the `layers` list, random values are selected and checked for uniqueness against all previously generated metadata files.
- Once we have `amount` unique tokens created, we layer them against eachother and output them and their metadata to their respective folders, `./metadata` and `./images`.

### Configuration
The `config` object is a dict that contains configuration instructions that can be changed to produce different outputs when running the program. Within metadata files, tokens are named using the configuration's `name` parameter, and described using the `description` parameter. 
- In ascending order, tokenIds are appended to the `name` resulting in NFT metadata names such as NFT #0001. 
- tokenIds are padded to the largest amount generated. IE, generating 999 objects will result in names NFT #001, using the above configuration, and generating 1000 objects will result in NFT #0001.
- As of `v1.0.2`, padding filenames has been removed.

The `layers` list contains `layer` objects that define the layers for the program to use when generating unique tokens. Each `layer` has a name,  which will be displayed as an attribute, values, trait_path, filename, and weights.
- `trait_path` refers to the path where the image files in `filename` can be found. Please note that filenames omit .png, and it will automatically be prepended.
- `weight` corresponds with the percent chance that the specific value that weight corresponds to will be selected when the program is run. The weights must add up to 100, or the program will fail.

#### Troubleshooting
- All images should be in .png format.
- All images should be the same size in pixels, IE: 1000x1000.
- The weight values for each attribute should add up to equal 100.

### Credits
This project is completely coded by [Jonathan Becker](https://jbecker.dev), using no external libraries.

