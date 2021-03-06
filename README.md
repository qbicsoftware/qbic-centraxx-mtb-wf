# qbic.mtbparser

[![GitHub top language](https://img.shields.io/github/languages/top/qbicsoftware/qbic.mtbparser.svg)]()
[![Build status](https://travis-ci.org/qbicsoftware/mtb-parser-lib.svg?branch=master)](https://travis-ci.org/qbicsoftware/mtb-parser-lib.svg?branch=master)
[![codecov](https://codecov.io/gh/qbicsoftware/mtb-parser-lib/branch/master/graph/badge.svg)](https://codecov.io/gh/qbicsoftware/mtb-parser-lib)
[![GitHub tag](https://img.shields.io/github/release/qbicsoftware/qbic.mtbparser/all.svg)](https://github.com/qbicsoftware/qbic.mtbparser/releases)
[![PyPI](https://img.shields.io/pypi/v/mtbparser.svg)](https://pypi.python.org/pypi/mtbparser/0.2)
[![license](https://img.shields.io/github/license/qbicsoftware/qbic.mtbparser.svg)]() 

A simple module that provides parser for different diagnostic variant information as part of the Molecular Tumor Board data provisioning in Tübingen.

## Documentation

File formats for
* [Somatic SNVs](./docs/somatic_snvs.md)
* [Somatic CNVs](./docs/cnvs.md)
* [Somatic structural variants](./docs/structural_variants.md)
* [Germline SNVs](./docs/germline_snvs.md)
* [Germline CNVs](./docs/cnvs.md)
* [Metadata](./docs/metadata.md)

Python class info
* SnvParser

### How to use the SnvParser class

Parsing a SNV file following the formats described above is fairly simple. Just create an ``SnvParser`` object with the path to the ``tsv``-file and specify its type by providing the correct header (``SSnvHeader, GSnvHeader, ...``).

```python
from mtbparser.snv_parser import SnvParser
from mtbparser.snv_utils import SSnvHeader

# Path to a valid SNV tsv file, as specified in
# the file format documentation.
somatic_snv_file = "/path/to/mySSnv.tsv"

# Create parser object for somatic SNVs
parser = SnvParser(somatic_snv_file, SSnvHeader)

# Iterate through parsed SNV items and get the gene name
for snv_item in parser.getSNVs():
    print(snv_item.get_snv_info(SSnvHeader.GENE.name))
    
```

## Author
This code implementation was done at the [Quantitative Biology Center](http://qbic.life). Please contact the author [@sven1103](https://github.com/sven1103) for more information.


## Changelog

### v0.2.7
Rename enums, so their names and values are equal.

### v0.2.6
You can now extract a copy of the complete SNV Item information as dictionary.

### v0.2.5
Bugfix: parsing of empty first columns failed because of the usage of strip() function. Columns can be empty, if they contain no information, so trimming whitespaces leads to a wrong total column number. We use rstrip() now, to remove escape characters and trailing whitespaces.

### v0.2.4
Fixed typo in 'tumor_content' definition in the metadata section.

### v0.2.3
Just v0.2.2, but had to rename the version on PyPi

### v0.2.2
Reading of files failed, because Python expects ACII encoding by default. Now, files are explicitely opened with utf-8 encoding.

### v0.2.1
Installation with ``pip`` failed, because the DESCRIPTION.rst for the module description was not provided in the sdist package.

### v0.2
The first _production-ready_ version of ``mtbparser``, that is also deployed on PyPI. Only updated documentation and proper formatting for PyPI deployment.

### v0.1dev
A first develeopment version, should work, tests are good, coverage > 90%.
