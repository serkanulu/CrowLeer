# CrowLeer, the fast and flexible CLI web crawler with focus on pages download

[![Build status](https://ci.appveyor.com/api/projects/status/f0flhq9s2ujyiibu?svg=true)](https://ci.appveyor.com/project/ERap320/crowleer) [![License: ISC](https://img.shields.io/badge/license-ISC-brightgreen.svg)](https://github.com/ERap320/CrowLeer/blob/master/LICENSE.txt) [![BuyMeACoffee](https://img.shields.io/badge/coffee-donate-yellow.svg)](https://buymeacoff.ee/erap320)

## Install and update with [Chocolatey](https://chocolatey.org/packages/crowleer/)
## Download the latest version: [Releases](https://github.com/ERap320/CrowLeer/releases)

### Options:

| Option                                                                                  | Description                                                                                                                                                                                         |
|-----------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| -h --help                                                                               | View this help page                                                                                                                                                                                 |
| -u --url                                                                                | URL used to start crawling                                                                                                                                                                          |
| -t --threads                                                                            | Number of threads used                                                                                                                                                                              |
| -d --depth                                                                              | Maximum crawling depth (the starting URL spcified in -u is at depth 0)                                                                                                                              |
| -x --same-domain                                                                        | Quick flag to only follow URLs with the same domain as the starting URL, overrides the --f-domain option                                                                                            |
| -S --save                                                                               | Activates the download functionality of CrowLeer. If not used nothing will be saved on the disk                                                                                                     |
| -o --output                                                                             | Choose a directory where the selected files will be saved. The default value is the current directory                                                                                               |
| -e --exclude                                                                            | Rule tested on the whole parsed URL, excludes the URL from the crawling and saving steps if matched                                                                                                 |
| -c --curl-opt                                                                           | Name of the custom CURL option to use when downloading pages. Only to use before the -p flag that specifies the parameter for the option. Can be used multiple times to set more than one option |
| -p --curl-param                                                                         | Value of the custom CURL option specified before it with the -c flag                                                                                                                                |
| --f-global                                                                              | Follow rule to be tested on the whole parsed URL                                                                                                                                                    |
| --f-protocol --f-domain --f-path --f--filename --f-extension --f-querystring --f-anchor | Follow rules on single parts of parsed URLs                                                                                                                                                         |
| --s-global                                                                              | Save rule to be tested on the whole parsed URL                                                                                                                                                      |
| --s-protocol --s-domain --s-path --s--filename --s-extension --s-querystring --s-anchor | Save rules on single parts of parsed URLs                                                                                                                                                           |

### Rules:

CrowLeer uses Regular Expressions (https://en.wikipedia.org/wiki/Regular_expression) to apply conditions to URLs or parts of URLs.

The Follow and Save rules have a global component, that matches the Completed URL (see the URL section) and one for every URL part.
The Exclude rule only has a global component.

* Follow Rule: describes pages to follow while crawling
* Save Rule: describes pages to download and save locally
* Exclude Rule: describes pages to completely exclude from the crawling

If not specified every rule is set to match anything (with the exclude rule matching nothing). You can set every possible composition of rules to describe the exact scenario you need, including global rule and parts rules together.

### URLs:

CrowLeer completes the URLs found in the crawled pages to make its and your work easier.

Every URL is split in parts and completed with parts from the URL of the page it was found in if necessary.

The parts in which a URL is split are: protocol, domain, path, filename, extension, querystring and anchor.

#### Example

The URL ```"/example/one/file.txt"``` was found while running on ```"https://erap.space"```

The Completed URL will be ```"https://erap.space/example/one/file.txt"```, and its parts will be:

| Part        | Value         |
|-------------|---------------|
| protocol    | "https"       |
| domain      | "erap.space"  |
| path        | "example/one" |
| filename    | "file"        |
| extension   | "txt"         |
| querystring | ""            |
| anchor      | ""            |

#### Example

The URL ```"https://en.wikipedia.org/wiki/Dog?s=canis#Origin"``` will be split in parts this way:

| Part        | Value              |
|-------------|--------------------|
| protocol    | "https"            |
| domain      | "en.wikipedia.org" |
| path        | "wiki/Dog"         |
| filename    | ""                 |
| extension   | ""                 |
| querystring | "s=canis"          |
| anchor      | "Origin"           |

### Progress information

Every line of the information shown in the console corresponds to the crawling of one URL. The structure of the lines is the following:

```Number of URLs left >> Currently crawled URL : Depth of the URL```

When the saving feature is activated, the URLs of pages that meet the Save Condition will be highlighted in green.

### CURL Options
Since CrowLeer uses CURL to download pages, you can set custom options to fine-tune every detail.
For example, to set a custom User Agent you need to call CrowLeer with the following arguments:

```crowleer -c "CURLOPT_USERAGENT" -p "MyCustomUA"```

__Attention!__ The -c and -p arguments can only be used in this order

It's possible to set how many options you want, by repeating -c and -p arguments. For example:

```crowleer -c "CURLOPT_USERAGENT" -p "MyCustomUA" -c "CURLOPT_INTERFACE" -p "eth0"```

Keep in mind that these options will be set for every request made by the program.

You can find a complete list of CURL options here: https://curl.haxx.se/libcurl/c/curl_easy_setopt.html

### Third party libraries

* [curl 7.57.0](https://curl.haxx.se/)
* [cpp-netlib URI](https://github.com/cpp-netlib/uri)

## Repositories
This project is pushed to both GitHub and GitLab:

* [GitLab Repository](https://gitlab.com/ERap320/CrowLeer)
* [GitHub Repository](https://github.com/ERap320/CrowLeer)

## License

You can do pretty much what you want with this. If you do, it will be much appreciated to mention me in your project readme/info. Every project using this code will be added to the readme if you send me an email to the address provided below.

Copyright 2017 ERap320 battistonelia@erap.space

Permission to use, copy, modify, and/or distribute this software for any purpose with or without fee is hereby granted, provided that the above copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.