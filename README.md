# gRPC Microservices Example (Node.js)

This project demonstrates a simple microservices architecture using **gRPC** and **Node.js**. It consists of three services:

- **main**: REST API gateway and gRPC client
- **degree**: Degree selector microservice (gRPC server)
- **process**: Onboarding processing microservice (gRPC server with streaming)

## Project Structure

```
grpc-js/
├── main/
│   └── main.js         # Main microservice (REST + gRPC client)
├── degree/
│   └── main.js         # Degree microservice (gRPC server)
├── process/
│   └── main.js         # Processing microservice (gRPC server, streaming)
├── protos/
│   ├── degree.proto    # Protobuf for degree service
│   └── processing.proto# Protobuf for processing service
├── package.json
├── .gitignore
└── README.md
```

## Technologies Used
- [Node.js](https://nodejs.org/)
- [Express](https://expressjs.com/)
- [@grpc/grpc-js](https://www.npmjs.com/package/@grpc/grpc-js)
- [@grpc/proto-loader](https://www.npmjs.com/package/@grpc/proto-loader)
- [concurrently](https://www.npmjs.com/package/concurrently)
- Protocol Buffers (Protobuf)

## Setup Instructions

1. **Clone the repository**
   ```bash
   git clone <your-repo-url>
   cd grpc-js
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Project structure**
   - `main/` - REST API and gRPC client
   - `degree/` - Degree gRPC server
   - `process/` - Processing gRPC server (with streaming)
   - `protos/` - Protobuf definitions

4. **Run all services concurrently**
   Add this to your `package.json` scripts section:
   ```json
   "scripts": {
     "start": "concurrently \"node degree/main.js\" \"node process/main.js\" \"node main/main.js\""
   }
   ```
   Then run:
   ```bash
   npm start
   ```

## Usage

### Main Service (REST API)
- Runs on **port 3000**
- Endpoints:
  - `GET /degree/:id` - Get degree information by ID
  - `POST /process` - Start onboarding process (body: `{ "degreeId": <number>, "orderId": <number> }`)

### Degree Service (gRPC)
- Runs on **port 50051**
- Implements the `Find` RPC to return degree info by ID

### Process Service (gRPC, Streaming)
- Runs on **port 50052**
- Implements the `Process` RPC to stream onboarding status updates

## Protobuf Definitions

See `protos/degree.proto` and `protos/processing.proto` for service and message definitions.

## Development
- Modify or add services in their respective folders
- Update protobufs in `protos/` and reload in your services as needed
- Use `npm start` to run all services together

## License
MIT
