# nlw-madoc-models
Capture models and associated helpers for NLW madoc instance.


## Python Code

`gen_csv.py` -- can generate a CSV from a capture model URL in Omeka S.

`gen_json.py` -- can generate capture model JSON for import into Omeka S from a CSV file.


### Usage

#### Gen CSV

Can be passed the URI for a capture model (in Omeka S), and will generate a CSV file which exports that capture model for further editing, or transformation back to JSON for ingest into a new instance of the crowd sourcing platform.

The Annotation Studio on the crowdsourcing platform exposes the capture model as a single JSON file. The general pattern for the URL is:

`https://crowd.library.wales/s/{site}/annotation-studio/open/resource`

So, for the WW1 project, that URL is:

`https://crowd.library.wales/s/war-tribunal-records/annotation-studio/open/resource`

To run the code, and create a local CSV copy:

```bash
python gen_csv.py -i https://crowd.library.wales/s/war-tribunal-records/annotation-studio/open/resource -o ./test.csv
```

N.B. you will need a Python environment or virtualenv with the `requirements.txt` requirements installed, and a local copy of the two JSON `@context` files.

#### Gen JSON

The capture model tools can be run on the commandline, with commandline arguments passed in. The arguments are as follows:

```
 '-i', '--input', help='Input CSV file name', required=True
 '-o', '--output', help='Output JSON file name', required=True
 '-b', '--url_base', help='Base url for the Omeka instance', required=False
 '-t', '--top_index', help='Numbered element to treat as the top level group', required=False
 '-g', '--group_id', help='ID for the Crowd Source Group resource template', required=False
 '-e', '--element_id', help='ID for the Crowd Source Element resource template', required=False
 '-c', '--irclass', help='ID for the Interactive Resource class', required=False
 '-u', '--user', help='Omeka User ID for the Owner', required=False
 '-x', '--context', help='IDA Context', required=False
```

##### Input

The tool expects a pipe-delimited '|' file, with column heads as per `template.csv` provided as part of this repo.

e.g.

`-i gle.csv`

###### Output

The tool will produce a JSON-LD document.

e.g.

`-o gle.json`

##### URL Base

The JSON-LD uses the address of the server where the model will be deployed throughout, to ensure correct `@id`s that will resolve.

e.g. for NLW: 

`-b http://nlw-omeka.digtest.co.uk`

##### Top Index

The CSV should use numbered identifiers in each row, under the `dcterms:identifier` column.

`-t 1`

tells the tool to start building the model with the row numbered `1`.

#### Example

```bash
python gen_json.py -i test.csv -o ww1_test.json -t 1 -g 3 -e 2 -u 1 -b https://omeka.nlw.digtest.co.uk
```

## Models

* `kyffin_crowds.json` - the original model in Crowds.library.wales
* `kyffin_new.json` - new model, for Madoc.
* `gle_crowds.json` - the original model in Crowds.library.wales
* `gle_new.json` - new model, for Madoc.
* `dcharries_crowds.json` - the original model in Crowds.library.wales
* `dcharries_new.json` - new model, for Madoc.
* `ww1_crowds.json` - the original model in Crowds.library.wales
* `ww1_new.json` - new model, for Madoc.


## License

MIT License

Copyright Digirati (c) 2019

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction, including without limitation the rights
to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
copies of the Software, and to permit persons to whom the Software is
furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all
copies or substantial portions of the Software.

THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
SOFTWARE.