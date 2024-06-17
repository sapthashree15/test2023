

**HTTP Methods and REST APIs**
================================

 After reading this document, you should be able to:
 - Define terms related to HTTP methods
 - Explain guidelines and best practices for writing REST APIs
 
 The internet relies on a client-server architecture. The end-user interfaces with the client, while the servers house the **services**<sup>1</sup> that operate the applications, the business logic, and the data. Clients communicate with the servers to achieve desired functionality for the end user. Data is transferred between client and server using hypertext transfer protocol, more commonly known as **HTTP**<sup>2</sup>. This communication usually happens via **APIs**<sup>3</sup>. In 2000, a set of guidelines for writing these APIs for a client-server architecture was developed called **REST**<sup>4</sup> APIs.
 
 The acronym “REST” stands for REpresentational State Transfer. Before explaining this term in more detail, let’s discuss HTTP methods and some terminology first.

 In a client/server architecture, the applications are composed of one or more services that reside on the servers. These services contain **resources**<sup>5</sup>. The client makes a **request**<sup>6</sup> for a resource via a **request object**<sup>7</sup> using a **route**<sup>8</sup> that has an **endpoint**<sup>9</sup> within the service. The application sends a **response object**<sup>10</sup> back in **response**<sup>11</sup> to the client to honor that request.
 
 A request object contains three parts, a **URL**<sup>12</sup>, a **request header**<sup>13</sup>, and a **request body**<sup>14</sup>. The server uses the URL to identify the service and the endpoint within the service being acted upon. The URL contains
 four parts: a **protocol**<sup>15</sup>, a **hostname**<sup>16</sup>, a **path**<sup>17</sup>, and a **query string**<sup>18</sup>. The request header contains metadata about the resource of the requesting client, such as the user **agent**<sup>19</sup>, **host**<sup>20</sup>, **content type**<sup>21</sup>, **content length**<sup>22</sup>, and what type of data the client should expect in the response.
 
The server responds with a response object consisting of a **header**<sup>23</sup>, a **body**<sup>24</sup>, and a **status code**<sup>25</sup>. The response object body often contains a **JSON**<sup>26</sup> **payload**<sup>27</sup> to provide the data back to the client.
 
 There are a number of HTTP methods that can be used in the REST API that allow interaction between the client and a service. The most common methods are **GET**<sup>28</sup>,**POST**<sup>29</sup>, **PUT**<sup>30</sup>, **DELETE**<sup>31</sup>, and **PATCH**<sup>32</sup>.

 The name of the method describes what happens to the resource when the method is applied. PUT and DELETE methods result in **idempotent**<sup>33</sup> data if the same API method is called multiple times.

 HTTP has three ways to pass parameters: the **URL path parameter**<sup>34</sup>, the **URL query parameter**<sup>35</sup>, and the **header parameter**<sup>36</sup>. The path and query parameters are passed as part of the URL, but the header parameter is passed by the browser directly to the service.

 When the service completes a request, it returns a response. An HTTP status code should be part of that response. The HTTP status code indicates whether the response has been completed or not. Response
 code categories are shown in the following table.
<table>
    <tr>
        <td><b>Status Code Range</b></td>
        <td><b>Meaning</b></td>
    </tr>
    <tr>
        <td>200-299</td>
        <td>Everything is OK</td>
    </tr>
    <tr>
        <td>300-399</td>
        <td>Resource has moved</td>
    </tr>
    <tr>
        <td>400-499</td>
        <td>Client-side error</td>
    </tr>
    <tr>
        <td>500-599</td>
        <td>Server-side error</td>
    </tr>
</table>

 As mentioned earlier, REST is a set of guidelines. There are five requirements for an API to be considered
 RESTful, plus one optional criterion:
 1. The API leverages a client-server architecture made up of resources that are managed and
 delivered via HTTP.
 2. Communication between client and server is **stateless**<sup>37</sup>.
 3. Data is **cacheable**<sup>38</sup> to improve performance on the client side.
 4. The interface is transferred in a standard format such that the requested resources stored on the server are separated from the representation sent to the client. The representation sent to the client contains sufficient data so that the client can manipulate the representation.
 5. Requests and responses communicate through different layers, such as **middleware**<sup>39</sup>. The client and server often do not communicate directly with each other.
 6. (Optional) Resources are usually static but can also contain executable code. The code should
 only be executed when the client requests it.

  When the client makes a request, it also must pass information about its state to the server. Every communication between the client and server should contain all the information needed to perform the
 request. The client, not the service, maintains the state. Each request must contain the requisite information so the server understands the request. So, for example, if the user is viewing a database
 record and that record needs to be updated, the client must also send which record needs updating. The server doesn’t know which record is currently being viewed.

 An @app.route() method is used when defining a RESTful service. The @app.route() method takes two parameters, the route from the URL to the service being acted upon and an optional HTTP method parameter such as POST, GET, and so on. The route parameter can also include a variable, such as
 <username>, for example. The root of a route is ‘/’. So, for example, if you want the route to be www.mywebsite.com/accounts, you only need to specify “/accounts” as the route parameter in the
 @app.route function.

 REST APIs have the following characteristics:

-    Resource-based; that is, they describe sets of resources
- Only contain nouns, not verbs
- Use singular nouns when referring to a singular resource or plural nouns when referring to a collection of resources
- Always identified by URLs

<table>
    <tr>
        <td><b> NOT RESTful APIs</b></td>
        <td><b>RESTful equivalents</b></td>
    </tr>
    <tr>
        <td>GET http://api.myapp.com/getUser/123</td>
        <td> GET http://api.myapp.com/users/123</td>
    </tr>
    <tr>
        <td>POST http://api.myapp.com/addUser</td>
        <td> POST http://api.myapp.com/users</td>
    </tr>
    <tr>
        <td> GET http://api.myapp.com/removeUser/123</td>
        <td>DELETE http://api.myapp.com/users/123</td>
    </tr>
   
</table>

 URL format guidelines
 - Should use a slash ‘/’ to denote a hierarchical relationship in the directory structure
 - Should avoid using a trailing slash, e.g., /resource/
 - Should use hyphens, not camel case, e.g., /my-resource, not /myResource
- Should not use an underscore ‘_’ in the URL, e.g., /my-resource, not /my_resource
- Should use lowercase
 -Should not use a period ‘.’ in a URL
- May contain multiple subordinate resources and IDs in the URL, e.g., GET
 /resource/{id}/subordinate/{id}
### Terms and Definitions

<table>
    <tr>
        <td><b>Term</b></td>
        <td><b>Description</b></td>
    </tr>
    <tr>
        <td>1.Service</td>
        <td>A software component that makes up part of an application and serves a specific purpose. Generally, a service takes input from a client or another service and produces an output.</td>
    </tr>
    <tr>
        <td>2.HTTP</td>
        <td>The protocol used by a client-server architecture on the internet for fetching or exchanging resources’ data.</td>
    </tr>
    <tr>
        <td>3.API</td>
        <td>An Application Programming Interface is a set of definitions and protocols that allow two services to communicate with each other. The API requests data that can be exchanged between a resource and the results that are returned from that resource.</td>
    </tr>
    <tr>
        <td>4. REST</td>
        <td>A set of architectural guidelines that describe how to write an interface (API) between two components, usually a client and server, that describe how these components communicate with each other. REST stands for REpresentational State Transfer. REST describes a standard way to identify and manipulate resources. REST ensures the messages passed between the client and server are self-descriptive and define how the client interacts with the server to access resources on the server.</td>
    </tr>
    <tr>
        <td>5. Resource</td>
        <td>A resource is the fundamental concept of a RESTful API. It is an object that has a defined type, associated data, relationships to other resources, and a set of methods that can operate on it. A resource is commonly defined in JSON format but can also be XML.</td>
    </tr>
    <tr>
        <td>6. Request</td>
        <td>A request is made by a client to a host on a server to access a resource. The client uses parts of a URL to determine the information needed from the resource. Most common request methods include GET, POST, PUT, PATCH, and DELETE but also include HEAD, CONNECT, OPTIONS, TRACE, and PATCH.</td>
    </tr>
    <tr>
        <td>7. Request Object</td>
        <td>Contains the HTTP request data. It contains three parts: a URL, a header, and a body.</td>
    </tr>
    <tr>
        <td>8. Route</td>
        <td>The combination of an HTTP method and the path to the resource from the root of the path.</td>
    </tr>
    <tr>
        <td>9. Endpoint</td>
        <td>The location of the resource specified by a REST API that is being accessed on the server. It is usually identified through the URL in the HTTP method of the API.</td>
    </tr>
    <tr>
        <td>10. Response Object</td>
        <td>Contains the HTTP response data in response to a request. It contains a header, a body, and a status.</td>
    </tr>
    <tr>
        <td>11. Response</td>
        <td>A response is made by a server and sent to a client to either provide the client with the requested resource, tell the client the requested action has been completed, or let the client know there has been an error processing the request.</td>
    </tr>
    <tr>
        <td>12. URL</td>
        <td>A “Uniform Resource Identifier” is used interchangeably with the term URL. They are part of a RESTful API that locates the endpoint of the requested resource and contains the data about how that endpoint should be manipulated. The client issues an HTTP request using the URI/URL to manipulate the resource. They should consist of four parts: the hostname, the path, the header, and a query string.</td>
    </tr>
    <tr>
        <td>13. Request Header</td>
        <td>Information passed to the server about the retrieved resource or the requesting client. Examples include:
            <ul>
                <li>Method with endpoint: POST /car-reviews</li>
                <li>User-agent: The type of browser the client is using.</li>
                <li>Host: A computer on a network that communicates with other hosts.</li>
                <li>ContentType: The media type of a resource such as text, audio, or an image.</li>
                <li>Content length: The number of bytes of data being sent in a response.</li>
                <li>Accept-Encoding: Expected return data format, e.g., application/json</li>
                <li>Connection information</li>
            </ul>
        </td>
    </tr>
    <tr>
        <td>14. Request Body</td>
        <td>Provides the data being passed to the server.</td>
    </tr>
    <tr>
        <td>15. Protocol</td>
        <td>Tells the service how the data is to be transferred between the server and the client.</td>
    </tr>
    <tr>
        <td>16. Hostname</td>
        <td>The name of a device on a network, also often called the site name.</td>
    </tr>
    <tr>
        <td>17. Path</td>
        <td>The path identifies the location of the resource in the service and its endpoint. For example: https://www.customerservice/customers/{customer_id}</td>
    </tr>
    <tr>
        <td>18. Query String</td>
        <td>The part of a URL that contains the query.</td>
    </tr>
 <tr>
        <td>19. User-agent</td>
        <td>The type of browser the client is using.</td>
    </tr>
 <tr>
        <td>20.Host</td>
        <td>A computer on a network that communicates with other hosts.</td>
    </tr>
 <tr>
        <td>21.Content type</td>
        <td>The media type of a resource such as text, audio, or an image.</td>
    </tr>
  <tr>
        <td>22.Content length</td>
        <td>The number of bytes of data being sent in a response.</td>
    </tr>
    <tr>
        <td>23. Response Header</td>
        <td>Contains metadata about the response, such as a time stamp, caching control, security info, content type, and the number of bytes in the response body.</td>
    </tr>
    <tr>
        <td>24. Response Body</td>
        <td>The data from the requested resource is sent back to the client.</td>
    </tr>
    <tr>
        <td>25. Response Status</td>
        <td>The return code that communicates the result of the request’s status to the client.</td>
    </tr>
    <tr>
        <td>26. JSON</td>
        <td>“JavaScript Object Notation” is a format for storing and transporting data, usually as a way to send data from a service on a server to the client. It consists of key-value pairs and is self-describing. The format of JSON data is the same as the code for creating JavaScript objects, making it easy to convert this data into JavaScript objects but can be written in any programming language. JSON has three data types: scalars (numbers, strings, Booleans, null), arrays, and objects.</td>
    </tr>
    <tr>
        <td>27. Payload</td>
        <td>The payload is the data in the body of a response being transported from a server to the client due to an API request.</td>
    </tr>
    <tr>
        <td>28. GET</td>
        <td>The GET method is used as a request that retrieves a representation of a resource. GET() should never modify a resource and only return a representation of the requested resource.</td>
    </tr>
    <tr>
        <td>29. POST</td>
        <td>HTTP method that sends data to the server to create a resource and should return 201_CREATED status code.</td>
    </tr>
    <tr>
        <td>30. PUT</td>
        <td>HTTP method that updates a resource or replaces an existing one. Calling PUT multiple times in a row does not have side effects, whereas POST does. It should return a 200_OK code if the resource exists and can be updated or return a 404_NOT_FOUND code if the resource doesn’t exist.</td>
    </tr>
    <tr>
        <td>31. DELETE</td>
        <td>HTTP method that deletes a resource and returns 204_NO_CONTENT if the resource exists and can be deleted by the server or if the resource cannot be found, which means it has already been deleted.</td>
    </tr>
    <tr>
        <td>32. PATCH</td>
        <td>HTTP method that applies partial modifications to a resource.</td>
    </tr>
    <tr>
        <td>33. Idempotent</td>
        <td>Describes an element of a set that remains unchanged when making multiple identical requests. PUT and DELETE methods result in idempotent data if the same API method is called multiple times.</td>
    </tr>
    <tr>
        <td>34. URL Path Parameter</td>
        <td>Passed into the operation by the client as a variable in the URL’s path.</td>
    </tr>
    <tr>
        <td>35. URL Query Parameter</td>
        <td>Contains key-value pairs, usually in JSON format, and are separated from the path by a ‘?’. If there are multiple key-value pairs, they should be separated by an ‘&’. The query can be used to pass in a filter to be applied to the results that are returned by the operation.</td>
    </tr>
    <tr>
        <td>36. Header Parameter</td>
        <td>Contains additional metadata about the query, such as identifying the client that is calling the operation.</td>
    </tr>
    <tr>
        <td>37. Stateless</td>
        <td>All requests from a client to a server for resources happen in isolation from each other. The server is unaware of the application’s state on the client, so this information needs to be passed with every request.</td>
    </tr>
    <tr>
        <td>38. Cacheable</td>
        <td>The ability to store data on the client so that data can be used in a future request.</td>
    </tr>
    <tr>
        <td>39. Middleware</td>
        <td>Software that sits between applications, databases, or services and allows those different technologies to communicate.</td>
    </tr>
</table>
