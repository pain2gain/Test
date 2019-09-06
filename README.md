<h1>Chatbot based on IBM Watson Assistant</h1>


<h2>Introduction</h2>

The program is a Chatbot project based on the engine of [IBM Watson Assistant](https://www.ibm.com/cloud/watson-assistant/). It is a simple demo of my internship at [CARL Software](https://www.carl-software.fr/) for six months.
It just has a French version, but the engine of IBM Watson supports many [languages](https://cloud.ibm.com/docs/services/assistant?topic=assistant-language-support).
![image](https://github.com/pain2gain/Chatbot_IBM_Watson/raw/master/images/architeture.png)

The frame diagram shows us the overview of the system.

<h2>Dependencies</h2>

1. [Node.js](https://nodejs.org/en/) v10.15.3 
2. Node-SDK IBM Watson `npm install ibm-watson`
3. Node-SDK Express `npm install express`

<h2>Explanation</h2> 
First of all, it's necessary to explain the `relations` between every part for the frame diagram:

<h4>*User & GUI</h4>

With the natural language, user can realise an friendly interaction with the GUI.

<h4>*GUI & Backend</h4>

With the [Ajax HTTP Request](https://api.jquery.com/jquery.ajax/), the GUI can send user's description to Chatbot. In the case of the asynchronous request, GUI will get the response of Chatbot engine.

<h4>*Backend & Chatbot</h4>

With the API of IBM Watson, backend sends the description of the production problem to chatbot engine for getting the processing result.
![image](https://github.com/pain2gain/Chatbot_IBM_Watson/raw/master/images/response_of_chatbot.png)

<h4>*Backend & CARL Source</h4>

With the REST API of CARL Source, backend will get the details of the equipment and send the request to CARL Source.
Now here the REST api we get from the CS:

With code of equipment, to get more details. 

`http://csref-rd.carl-intl.fr:8180/xnet/api/ui/v1/search?_limit=50`

With all entities found, to send the request of intervention. 

`http://csref-rd.carl-intl.fr:8180/xnet/api/entities/v1/mr`

With the id of equipment, to add the equipment information to the request already existing. 

`http://csref-rd.carl-intl.fr:8180/xnet/api/entities/v1/mreqpt`

***CARL Source & Chatbot**

Manually, we downloaded the data from CARL Source to get the entities of 'Equipement', 'Localisation', 'TypeEQPT', 'Marque', 'Symptômr', 'Modèle' and process these data.

<h2>Watson</h2>
With the [API of Watson Assistant](https://cloud.ibm.com/apidocs/assistant?code=node), we can send the message to chatbot engine.
```js
    const AssistantV1 = require('ibm-watson/assistant/v1');
    
    const service = new AssistantV1({
      version: '2019-02-28',
      iam_apikey: '{apikey}',
      url: '{url}'
    });
    
    service.message({
      workspace_id: '{workspace_id}',
      input: {'text': 'Hello'}
      })
      .then(res => {
        console.log(JSON.stringify(res, null, 2));
      })
      .catch(err => {
        console.log(err)
      });
```
![image](https://github.com/pain2gain/Chatbot_IBM_Watson/raw/master/images/response_of_chatbot.png)
<h2>

