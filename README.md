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
$ git clone https://github.com/cytvictor/net2text-CSCI-SHU-308-Fall23
$ cd net2text-CSCI-SHU-308-Fall23/
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

For further explanation on this data generation tool, please find README from [Net2Text original repository](https://github.com/nsg-ethz/net2text).
