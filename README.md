# Dataset

We provide here the dataset that lead to the IMC paper "Multilevel MDA-Lite Paris Traceroute".
In this dataset, we provide four different files: 

The MDA traceroute survey, the Multilevel MDA-Lite traceroute survey, the MDA/MDA-Lite comparison, and the midar results.

The dataset can be found at the following URL:
```
ftp://venus.planet-lab.eu/
```

## Exploring the data

To explore the MDA traceroute, which are in the mda_survey_dump.tar.gz file, you need to type the following command.

Be careful, this needs approximately 150 GB.
```
rethinkdb restore mda_survey_dump.tar.gz
```

Look at the rethinkdb restore documentation if you have memory problems.
Common problems can be resolved with the following:
```
rethinkdb restore --temp-dir /path/to/dir/with/memory mda_survey_dump.tar.gz
```

To explore the MDA-Lite traceroutes, and MDA/MDA-Lite evaluation dataset, you will need to install graph-tool, as the
serialized output of the MDA-Lite traceroute is a graph that is saved with the graph-tool library.

Follow the instructions in the following link to install graph-tool. As the C++ Library makes an extensive use of metaprogramming and templates, it can take a while (up to 30 minutes on a recent laptop) to compile graph-tool: 

[Graph-tool](https://graph-tool.skewed.de)

Once you have graph-tool, you can use the following code to explore the data:

```python
from graph_tool import *
g = load_graph("/path/to/serialized/graphs.xml")

# Manipulate the graph via its properties.
v_properties = g.vertex_properties
e_properties = g.edge_properties
g_properties = g.graph_properties

# Example: ip_ids, print ip_ids of an ip_address
ip_address = g.vertex_properties["ip_address"]
ip_ids = g.vertex_properties["ip_ids"]
for v in g.vertices():
    if ip_address[v] == "an_ip_of_your_choice_in_the_traceroute":
        print ip_ids[v]

```

Lots of other properties are available in the graph. You can find a list of it in the head of the .xml file of the serialized traceroute.

<!--- ## Contributing

Please read [CONTRIBUTING.md](https://gist.github.com/PurpleBooth/b24679402957c63ec426) for details on our code of conduct, and the process for submitting pull requests to us.

## Versioning

We use [SemVer](http://semver.org/) for versioning. For the versions available, see the [tags on this repository](https://github.com/your/project/tags). 

## Authors

* **Billie Thompson** - *Initial work* - [PurpleBooth](https://github.com/PurpleBooth)

See also the list of [contributors](https://github.com/your/project/contributors) who participated in this project.

## License

This project is licensed under the MIT License - see the [LICENSE.md](LICENSE.md) file for details

## Acknowledgments

* Hat tip to anyone who's code was used
* Inspiration
* etc
-->
