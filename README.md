**NB: Version 0.1 of Murmurations has been superseded by Version 1.0 - please see the [Murmurations Protocol](https://github.com/MurmurationsNetwork/MurmurationsProtocol) repo for the latest information**

# Murmurations Schemas

The Murmurations network uses structured data to describe organisations and projects. Files in this repo define how that data is structured, and specifications for extending the base schema. 

Each schema file contains a JSON object, which contains a property for each data field defined by the schema. The key for that property is the field's name, which is used as the primary identifier for that field throughout the network. The property's value is another JSON object that defines the attributes of the field as key:value pairs. 

These attributes can include:

**type** — the type of data this field will contain, once stored (string, required)  
**title** — human-readable title for the field (string, required)  
**inputAs** — specification for the HTML input for this field (string, optional)  
**validateAs** — specification for data validation (string, optional)  
**required** — whether this field is required (boolean, optional)  
**comment** — description of what this field is for or how it should be filled in (string, required)  
**maxLength** — maximun length of entered data in characters (number, optional)  
**options** — a JSON array of possible values for this field (array, optional)  
**multiple** — used with "options" if multiple values are allowed (boolean, optional)  

Please submit suggestions or recommendations to the schema or schema structure as issues on this repo or via the contact form at [http://murmurations.network](http://murmurations.network#contact)
