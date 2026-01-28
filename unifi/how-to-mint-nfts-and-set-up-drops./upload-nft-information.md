# Upload NFT Information

## A. Original Contents(Mandatory) <a href="#b.-original-contents" id="b.-original-contents"></a>

<table><thead><tr><th>Label</th><th width="412.5865478515625">Guide</th><th>Example</th></tr></thead><tbody><tr><td>Collection Name</td><td>Please enter one of the issued collections.</td><td>Fate Genesis 99</td></tr><tr><td>Meta</td><td>Please input the NFT's metadata in the specified format and upload it.<br>This must be a file containing all the attributes of the NFT you wish to mint. If you are minting 10,000 NFTs, there must be 10,000 lines of input data. Even if all the information is identical, please input all 10,000 lines.</td><td>Please refer to the sample file linked below.</td></tr></tbody></table>

{% file src="../../.gitbook/assets/meta sample.csv" %}



## B. Pre-reveal(Optional) <a href="#a.-pre-reveal" id="a.-pre-reveal"></a>

This feature is used when original content needs to be disclosed at a specific time. It is unnecessary if the NFT at the time of purchase is the same as the one being held.

| Label                 | Guide                                                        | Example                                      |
| --------------------- | ------------------------------------------------------------ | -------------------------------------------- |
| Collection Name       | Please enter one of the issued collections.                  | Fate Genesis 99                              |
| Pre-reveal Image      | Image Size: 600x600                                          |                                              |
| Description           | List of Supported languages in the Unifi Apps                | This NFT will be revealed on January 1, 2026 |
| Requested Reveal Date | Only complete this field if a pre-reveal is being conducted. | yyyy-mm-dd tt:mm (in UTC)                    |

