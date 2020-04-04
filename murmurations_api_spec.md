# Murmurations API

## Node communications

### Index submission

Add a node to the index

HTTP POST request to the index URL.

#### Parameters

| key | value 
--- | ---
action | 'put_node'
node_data | Array of data about the node

Node data must include:

key | value
--- | ---
apiUrl | The URL where the node's JSON can be accessed
url | The public-facing URL of the node


#### Returns

JSON string

**Return parameters**

key | value
--- | ---
status | 'success', 'failure'
message | Error message string

Note: before the index returns a result, it makes a query to the node to confirm that the node's data is accessible and valid


### Retrieve networks list

Retrieve list of available networks from the index

HTTP GET request to index URL

#### Parameters
```
action: 'get_networks'
```

#### Returns

A JSON string of networks

Parameters for each network:

key | value
--- | ---
url | main URL of the network, used as ID
schemaUrl | URL of the network's schema JSON
updated | Unix timestamp of the time the network was last updated in the index
name | Human-friendly name for the network

Example JSON: 
```
{
	"http://murmurations_test_network_example.com":{
		"url":"http://murmurations_test_network_example.com",
		"schemaUrl":"http://murmurations_test_network_example.com/murmurations_test_network_schema.json",
		"updated":1564350606,
		"name":"Murmurations Test Network"
	},
	"http://example.com/murmurations_test_network2":{
		"url":"http://example.com/murmurations_test_network2",
		"schemaUrl":"http://example.com/murmurations_test_network2/schemas/TestNet2Schema.json",
		"updated":1564438875,
		"name":"TestNet2"
	}
}
```

### Retrieve network schema from network

Retrieve field schema for a network

HTTP GET request to network schema URL.

Response should be valid JSON string that matches the [Murmurations schema specification](https://github.com/Photosynthesis/MurmurationsSchema)


### Respond to aggregator request

Provide node data to an aggregator

HTTP GET request to node's apiUrl

Response: valid JSON string including at least the required fields in the [Murmurations base schema](https://github.com/Photosynthesis/MurmurationsSchema/blob/master/base.json)

Example JSON:
```
{
"name": "Test Static Node",
"url": "http://example.com",
"tagline": "Making Movements Visible",
"mission": "Testing Murmurations",
"location": "London, UK",
"nodeTypes" : "co-op",
"logo": "http://example.com/projects/murmurations/wordpress/wp-content/uploads/2019/06/murmurations.png",
"feed": "http://example.com/feed/",
"lat": "51.5073219",
"lon": "-0.1276474"
}
```

## Aggregator communications

### Index query
Query the index for node data and URLs

HTTP POST request

parameter | value
--- | ---
action | 'get_nodes',
conditions | Array of subject, predicate, object conditions

Example conditions:
```
[ 'updated',  'isGreaterThan', 1580797437],
[ 'nodeTypes',  'includes', 'co-op']
```
#### Returns

JSON string of node data. Data will include at least the node's URL, API URL, update date, and node types.

Example:
```
"http://example.com/man_coop":{
  "url":"http://example.com/man_coop",
  "apiUrl":"http://test.photosynth.ca/murmurations_nodes/manchester_coop.json",
  "updated":1561718129,
  "nodeTypes":"co-op",
  "location":"Manchester",
  "lat":"53.48",
  "lon":"-2.24"
}

```


### Node query
Query a node for node data

HTTP GET request to node's apiUrl

Response: valid JSON string including at least the required fields in the [Murmurations base schema](https://github.com/Photosynthesis/MurmurationsSchema/blob/master/base.json)

# Network communications
Add a network to the index

HTTP POST request to index

Parameters:

key | value
--- | ---
action | 'put_network'
network_data | Array of data about the network

Network data must include:

key | value
--- | ---
url | Public-facing URL of the network
schemaUrl | Location of the network's schema
name | Name of the network



