# CSCI-SHU 308 Notes

## 1. How to set up the environment

Prerequisites:
- [Python3](https://www.python.org/downloads). Please note some old versioned macOS and Linux defaults to Python 2.
- pip (shipped with Python in most cases)
- `networkx` pip package

```bash
pip3 install networkx
```

## 2. How to use pre-generated datasets
There are three pre-generated network flow data for a same 25-nodes topology called "ATT_NA (ATT North America)".

| directory | #nodes | #edges | #prefixes | Flow count | 
| --------- | ------ | ------ | --------- | ---------- |
| examples/att_na/AttMpls-10-egress_100 | 25 | 57 | 100 | 2585 |
| examples/att_na/AttMpls-10-egress_1000 | 25 | 57 | 1000 | 25456 |
| examples/att_na/AttMpls-10-egress_10000 | 25 | 57 | 10000 | 255003 |

You may start work on `load_example.py` to see how the flow database is organized. Now this script simply counts the number of flows and randomly print one flow:

```bash
$ python load_example.py examples/att_na/AttMpls-10-egress_100
Successfully read the example files.
There is a total of 2585 flows in a topology with 25 nodes and 57 edges.

This is a random flow: Flow(path=24 -> 12 -> 13 -> 5 -> 7, organization=Lao Telecommunication IX, prefix=115.84.82.0/24, bandwidth=204.43353242530557, sp=True
```

This example includes the features mentioned in the paper: `path`, `organization`, `bandwidth`, `is-shortest-path`.

## Appendix 1. Dataset generation
For your reference, they are generated using the following command:

```bash
$ cd examples/generator/
$ python example_generator.py ../att_na/AttMpls.graphml ../att_na/AttMpls-10-egress -a
```

Below is the README from [Net2Text original repository](https://github.com/nsg-ethz/net2text).

# Net2Text

This repository contains the code to generate the datasets used in the
NSDI'18 submission of the [Net2Text project](https://net2text.ethz.ch).

## Generating a Dataset

The script [examples/generator/example_generator.py](examples/generator/example_generator.py)
allows you to generate all the forwarding paths and flows for a given
number of prefixes and egresses.

The output consists of two files:

1. A dump of all paths (aggregated forwarding tables): ndb_dump.out
2. The topology: ndb_topo.out
3. A config file containing all settings for Net2Text

### Running the Script

```bash
$ python example_generator.py <graph_file> <output_path> [--automatically] [--debug]
```

#### Arguments

* __graph_file__ name of the file containing the graph in graphml format (e.g., from [TopologyZoo](http://www.topology-zoo.org/dataset.html)
* __output_path__ path to the directory where the output should be stored
* __-a/--automatically__ automatically generate names and pick egresses, if it is not specified, you have to provide
for each node in the graph the name and pick the egress routers manually.
* __-d/--debug__ enable debug output

__Note:__ to limit the number of prefixes used in the dataset, just
edit line 72 in `example_generator.py`.

### Helper Scripts

* `example_test.py` - check basic information of a generated example
(e.g., number of nodes, prefixes, prefixes per destination) and compute
the score of different summaries.

## Loading a Dataset

Use the scrip `load_example.py` to load a dataset from the generated files.

### Running the Script

```bash
$ python load_example.py <path>
```

#### Arguments

* __path__ path to the directory containing the generated files.


## Example using ATT NA

### Generating the Dataset

```bash
$ cd examples/generator
$ python example_generator.py ../att_na/AttMpls.graphml ../att_na -a
```

Now, you should have all the files in the directory `examples/att_na_X`
where X is the number of prefixes specified in line 72 of the generator
script.

### Loading the Dataset

```bash
$ cd ../..
$ python load_example.py examples/att_na_1000
```
