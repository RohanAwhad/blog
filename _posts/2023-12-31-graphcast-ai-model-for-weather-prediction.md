### Introduction

- **GraphCast**: A state-of-the-art AI model by Google DeepMind that can make 10-day weather forecasts with unprecedented accuracy and efficiency, using data instead of physics-based equations.
- **Performance**: GraphCast outperforms the industry gold-standard weather simulation system (HRES) on more than 90% of test variables and forecast lead times, and can identify severe weather events earlier than traditional models.
- **Impact**: GraphCast has the potential to save lives and reduce the impact of storms and extreme weather on communities, by providing more accurate and timely forecasts for decision-making across sectors.
- **Open Source and Pretrained Models**: The GraphCast model code is open-sourced and available on GitHub. It provides three pretrained models: `GraphCast`, `GraphCast_small`, and `GraphCast_operational`. These models are trained on ERA5 data from different periods and have different resolutions and pressure levels. The model weights, normalization statistics, and example inputs are available on Google Cloud Bucket.

Here's how it works:

1. **Data-Based Approach**: Unlike traditional weather forecasting methods that rely on physics equations, GraphCast uses data to create a weather forecast system. It is trained on decades of historical weather data to learn the cause-and-effect relationships that govern how Earth's weather evolves from the present into the future.

2. **Graph Neural Networks (GNNs)**: GraphCast is based on GNNs, which are particularly useful for processing spatially structured data. It makes forecasts at a high resolution of 0.25 degrees longitude/latitude (approximately 28km x 28km at the equator).

3. **Multi-Scale Graph Neural Network-Based Autoregressive Model**: GraphCast is a multi-scale graph neural network-based autoregressive model. It generates predictions at 6-hour time steps for a set of surface and atmospheric variables.

4. **Training Data**: GraphCast is trained on historical weather data from ECMWF’s ERA5 reanalysis archive.


### Deep GNN

One of the main files is `deep_typed_graph_net.py`. It is a library file that contains the implementation of a general purpose deep graph neural network (GNN) that operates on TypedGraph objects. A TypedGraph is a data structure that represents a graph with nodes and edges of different types, each with their own features. The deep GNN can take a TypedGraph as input and output another TypedGraph with updated node and edge features.

The deep GNN consists of three main components:

- A **message function** that computes messages for each edge based on the features of the source and target nodes and the edge itself. The messages are aggregated by type and summed across all incoming edges for each node.
- A **node update function** that updates the node features based on the aggregated messages and the previous node features. The node update function is applied separately for each node type.
- An **edge update function** that updates the edge features based on the features of the source and target nodes and the previous edge features. The edge update function is also applied separately for each edge type.

The deep GNN can be stacked to form multiple layers, each with its own message, node update, and edge update functions. The final output is a TypedGraph with updated node and edge features.

The `deep_typed_graph_net.py` file is used by the `graphcast.py` file to implement three GNNs for the GraphCast model: the Grid2Mesh GNN, the Multi-mesh GNN, and the Mesh2Grid GNN. These GNNs are responsible for transforming the input grid data into a multi-mesh representation, propagating information across the multi-mesh, and transforming the output multi-mesh back into a grid data. 

### TypedGraph

A `TypedGraph` is a data structure used in Graph Neural Networks (GNNs) to represent a graph where nodes and edges can have different types, each with their own features. This allows the GNN to process different types of nodes and edges differently, which can be useful in many applications.

Here's a simple example of how a `TypedGraph` might be represented in Python:

```python
    class Node:
        def __init__(self, node_type, features):
            self.node_type = node_type
            self.features = features
    
    class Edge:
        def __init__(self, edge_type, features, source_node, target_node):
            self.edge_type = edge_type
            self.features = features
            self.source_node = source_node
            self.target_node = target_node
    
    class TypedGraph:
        def __init__(self):
            self.nodes = []
            self.edges = []
    
        def add_node(self, node_type, features):
            node = Node(node_type, features)
            self.nodes.append(node)
            return node
    
        def add_edge(self, edge_type, features, source_node, target_node):
            edge = Edge(edge_type, features, source_node, target_node)
            self.edges.append(edge)
```

### GraphCast Model

The core logic of the GraphCast model consists of three main components: an encoder, a recurrent core, and a decoder.
- **The encoder** takes the input weather data and transforms it into a graph representation, where each node corresponds to a grid point and each edge corresponds to the distance between two grid points. The encoder also applies a convolutional neural network (CNN) to each node to extract local features from the input variables.
- **The recurrent core** takes the encoded graph and updates it iteratively using a GNN module. The GNN module consists of several graph convolutional layers, each of which applies a message-passing function to aggregate information from neighboring nodes and edges, and an update function to compute new node and edge features. The recurrent core also applies a gated recurrent unit (GRU) to each node to maintain a hidden state across time steps.
- **The decoder** takes the updated graph and transforms it back into a tensor representation, where each grid point corresponds to a row and each output variable corresponds to a column. The decoder also applies a CNN to each node to generate the output weather variables, such as temperature, wind speed, and pressure.

### Inference with GraphCast

![Inference with GraphCast](/blog/assets/img/graphcast_inference.png)
*Image of GraphCast inference pipeline*

During inference, the GraphCast model follows these steps:

1. **Input Preparation**: The model takes as input the current weather conditions, represented as a set of variables (such as temperature, pressure, wind speed, etc.) at each grid point on the Earth's surface. These variables are preprocessed and normalized to be suitable for the model.

2. **Encoding**: The input data is transformed into a graph representation, where each node corresponds to a grid point and each edge corresponds to the distance between two grid points. A convolutional neural network (CNN) is applied to each node to extract local features from the input variables.

3. **Recurrent Core**: The encoded graph is passed through a recurrent core, which updates the graph iteratively using a Graph Neural Network (GNN) module. The GNN module consists of several graph convolutional layers, each of which applies a message-passing function to aggregate information from neighboring nodes and edges, and an update function to compute new node and edge features. A gated recurrent unit (GRU) is applied to each node to maintain a hidden state across time steps.

4. **Decoding**: The updated graph is transformed back into a tensor representation, where each grid point corresponds to a row and each output variable corresponds to a column. A CNN is applied to each node to generate the output weather variables, such as temperature, wind speed, and pressure.

5. **Postprocessing**: The output data is postprocessed to convert it back to the original scale and units. The model generates predictions at 6-hour time steps for a set of surface and atmospheric variables.

6. **Autoregressive Forecasting**: The model generates a sequence of predictions by auto-regressively feeding the outputs back as inputs at each step. This allows the model to make medium-range forecasts up to 10 days in advance.

---

### References

- [[Paper] GraphCast: Learning skillful medium-range global weather forecasting](https://arxiv.org/abs/2212.12794)
- [[Article] GraphCast: AI model for faster and more accurate global weather forecasting](https://deepmind.google/discover/blog/graphcast-ai-model-for-faster-and-more-accurate-global-weather-forecasting/)
- [[Code] google-deepmind/graphcast](https://github.com/google-deepmind/graphcast)
- [[Nvidia] GraphCast for weather forecasting](https://docs.nvidia.com/deeplearning/modulus/modulus-core/examples/weather/graphcast/readme.html)
- [Google's New GraphCast AI model can forecast weather 10 days in advance](https://siliconangle.com/2023/11/14/googles-new-graphcast-ai-model-can-forecast-weather-10-days-advance/)
- [ECMWF Reanalysis v5 (ERA5)](https://www.ecmwf.int/en/forecasts/dataset/ecmwf-reanalysis-v5)
- [HRES](https://confluence.ecmwf.int/display/FUG/Section+2.1.2.4+HRES+-+High+Resolution+Forecasts)
