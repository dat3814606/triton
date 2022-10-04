
# Triton

There are two ways of model deployment: embedding and serving.

Model embedding is entire trained model is embedded onto the device and loaded into memory when run. The pros here is low latency. The cons however are not scalable, requires techniques to optimize speed, reduce size of model.

Model serving is porting trained model on a server and making it accessible to other applications as a client-server architecture.

History of Model serving:

Flask or FastAPI:

Pros: Straightforward to incorporate into existing environments

Cons: Inefficient, inconsistent across developers, requires lots of customization to meet infrastructure needs.

We need model serving frameworks to: 

1. Shorten time from dev to production
2. Standardize deployment
3. Deliver reliable ML products at scale with high throughput and low latency predictions

## NVIDIA Triton Inference Server

![Triton architecture](https://drive.google.com/uc?id=1PoruVGwEDdyYAotgLLRigRIpWEAqExM1)

The full workflow of Triton can be seen in Figure and described as follows:
1. Client sends a request through HTTP or gRPC.
2. The request goes to the Request Handler.
3. Then, the request goes to a Per Model Scheduler Queue.
4. When it’s ready, the schedule will send the request to the worker backend for computation (GPU/CPU).
5. At the same time, the health metrics of the server are exposed through another port.
6. Once the computation is complete, the response goes to the Response Handler.
7. The response is then sent back to the client.

Triton features:
1. Model ensemble: Allows engineers to customize data pipeline, reducing computation cost on client side by run preprocessing and postprocessing on server side.
2. Concurrent model runs: In case you have many GPU/CPU. Triton helps to utilize them all under high demand to ensure higher throughput.
3. Dynamic batching: Batching requests within short period of time to increase throughput.
