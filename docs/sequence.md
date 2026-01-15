# Sequence Diagram  

This sequence diagram illustrates the flow of a typical request from a client (such as a web frontend) through the Express.js API layer, into the ChirpStack gRPC client, and finally to the ChirpStack server.  

```mermaid  
sequenceDiagram  
    participant Client  
    participant ExpressAPI as Express API  
    participant GRPCClient as gRPC Client  
    participant ChirpStack as ChirpStack gRPC  

    Client->>ExpressAPI: HTTP request (e.g. GET /api/tenants)  
    ExpressAPI->>GRPCClient: build request + auth metadata  
    GRPCClient->>ChirpStack: service RPC call  
    ChirpStack-->>GRPCClient: gRPC response  
    GRPCClient-->>ExpressAPI: return result  
    ExpressAPI-->>Client: JSON response  

    Note over ExpressAPI,GRPCClient: The same pattern applies for tenants, applications, devices, and gateways.  
```
