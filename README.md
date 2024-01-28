# Taproot Assets Tiramisu Metadata Format
This repository describes metadata format for taproot assets protocol used by the Tiramisu wallet. The protocol is loosely based on the OpenSea metadata format for ERC721 or ERC1155 NFTs. https://docs.opensea.io/docs/metadata-standards

## Taproot Assets Protocol
Taproot Assets was developed by lightning labs and is in detail described here https://docs.lightning.engineering/lightning-network-tools/taproot-assets.

## Motivation

It is a standard in the culture of crypto, NFTs and altcoins to associate information such as Ticker, image and descripting with assets. With taproot assets we have the option to include this information directly in the asset metadata.

## Fields

Note that name of the asset is not required as a part of this schema is it by default a part of the taproot assets protocol.

| Field name | Description | Optional/mandatory | Example |
| ------------- | ------------- | ------------- | ------------- |
| acronym  | Ticker / acronym describing the asset in less than 5 letters | Mandatory for non-collectable assets | AC |
| description  | Longer description of the asset explaining what is the asset purpose or the  | Mandatory | A coin dedicated to Adam from Genesis, the first man on earth. Also a first asset minted in Tiramisu wallet on mainnet. |
| image_data  | Data URL in the format [\<mediatype\>][;base64],\<data\> where mediatyle is the MIME media type and data is base64 encoded image data. The standard is defined in detail here https://developer.mozilla.org/en-US/docs/Web/HTTP/Basics_of_HTTP/Data_URLs | Optional | data:image/jpg;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAIAAAD8GO2jAAABc0lEQVR4nGK5skGaAQaUnTbA2ee2JsHZ00zuwtlzLMPhbO3f/Qi9zR/g7Gch7HA2EwONwdC3gOU5UzKcY/7TCs7+eagOzj5jzg9nh3HegLPv7JWFs63vF8HZ/E2IuBn6QUT7OFjXuh7O+TAbkZbPvxeAszO+NcHZSTwX4exCgxlw9s1QCThb0P0fnD30g4jmFjAeU9oI53yMeAFnux5B2N3aJgNnb/lqAmfHB5+Esy83voezWyKM4OyhH0S0zwdnlk6Fc67ORqR3v42OcLbWUic4O79/Jpy958IEODt79xU4m4+tE84e+kFE+3zgLrodzmlb+w7O9gqphbOPCCM0GG/dCmffi1oGZz+WegBn//2PiJuhH0S0j4MVlWlwzm0FGzh7veotONsquw/OnsSHyB/WPxFxMNvOAs62QGSVYRBEtI+D8GZEPvB2QdSr0qdz4Ow8cS84u/+RKZxtLoqoJ1q3IurwbHeE3qEfRDS3ABAAAP//hnBeQ7p8R+8AAAAASUVORK5CYII= |
| image  | URL to the page containing the image | Optional | https://mainnet.tiramisuwallet.com/walletapp/get_currency_preview_image/2 |

## Format

As the number of fields in this schema is likelly to be increased we suggest JSON as a method for formating this metadata.

## How to mint assets 

Here is an example how to mint a "normal" or fungible asset:

```
tapcli assets mint --type=normal --name=MyTestCoin --supply=1000000 --meta_bytes="{\"acronym\": \"MTC\",\"description": \"This is my test coin\", \"image_data\": \"data:image/jpg;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAIAAAD8GO2jAAABc0lEQVR4nGK5skGaAQaUnTbA2ee2JsHZ00zuwtlzLMPhbO3f/Qi9zR/g7Gch7HA2EwONwdC3gOU5UzKcY/7TCs7+eagOzj5jzg9nh3HegLPv7JWFs63vF8HZ/E2IuBn6QUT7OFjXuh7O+TAbkZbPvxeAszO+NcHZSTwX4exCgxlw9s1QCThb0P0fnD30g4jmFjAeU9oI53yMeAFnux5B2N3aJgNnb/lqAmfHB5+Esy83voezWyKM4OyhH0S0zwdnlk6Fc67ORqR3v42OcLbWUic4O79/Jpy958IEODt79xU4m4+tE84e+kFE+3zgLrodzmlb+w7O9gqphbOPCCM0GG/dCmffi1oGZz+WegBn//2PiJuhH0S0j4MVlWlwzm0FGzh7veotONsquw/OnsSHyB/WPxFxMNvOAs62QGSVYRBEtI+D8GZEPvB2QdSr0qdz4Ow8cS84u/+RKZxtLoqoJ1q3IurwbHeE3qEfRDS3ABAAAP//hnBeQ7p8R+8AAAAASUVORK5CYII=\"}"
```

Here is an example how to mint a "collectible" or a non-fungible asset:

```
tapcli assets mint --type=collectible --name=MyTestNft --supply=1000000 --meta_bytes="{\"description": \"This is my test NFT\", \"image_data\": \"data:image/jpg;base64,iVBORw0KGgoAAAANSUhEUgAAACAAAAAgCAIAAAD8GO2jAAABc0lEQVR4nGK5skGaAQaUnTbA2ee2JsHZ00zuwtlzLMPhbO3f/Qi9zR/g7Gch7HA2EwONwdC3gOU5UzKcY/7TCs7+eagOzj5jzg9nh3HegLPv7JWFs63vF8HZ/E2IuBn6QUT7OFjXuh7O+TAbkZbPvxeAszO+NcHZSTwX4exCgxlw9s1QCThb0P0fnD30g4jmFjAeU9oI53yMeAFnux5B2N3aJgNnb/lqAmfHB5+Esy83voezWyKM4OyhH0S0zwdnlk6Fc67ORqR3v42OcLbWUic4O79/Jpy958IEODt79xU4m4+tE84e+kFE+3zgLrodzmlb+w7O9gqphbOPCCM0GG/dCmffi1oGZz+WegBn//2PiJuhH0S0j4MVlWlwzm0FGzh7veotONsquw/OnsSHyB/WPxFxMNvOAs62QGSVYRBEtI+D8GZEPvB2QdSr0qdz4Ow8cS84u/+RKZxtLoqoJ1q3IurwbHeE3qEfRDS3ABAAAP//hnBeQ7p8R+8AAAAASUVORK5CYII=\"}"
```

## Asset examples

Here is a list of assets that were already minted using this metadata format:


