This is a fork of the ASP.NET Core 'Samples' repo, so it contains lots of stuff unrelated to the presentation.

The relevant parts of the code are in `samples\aspnetcore\blazor\FlightFinder`.

The relevant branches are:

 * `pre-demo-state`
 * `grpc` (switch to this early in the demo, and do the rest of the demo here)
 * `master` (finished post-demo state)

## Flow

  - [4] Look at flightfinder app
        - See functionality
        - See Main.razor
        - See JSON-over-HTTP requests on wire
  - [8] gRPC
        - What people need to understand about gRPC:
          - it's an alternate kind of API endpoint, using lang-independent descriptor and protobuf messages
          - pros/cons vs json-over-http: more strongly typed, more compact, no REST arguments. It's just RPC.
          - normally requires HTTP2 (and hence not callable from JS/WebAssembly) but gRPC-Web works over HTTP1.1
        - See FlightFinder doing traditional JSON
          - Problem 1: verbose on the wire
          - Problem 2: if server and client don't agree about URLs (etc) then it will fail -- versioning
        - Switch to version that has .proto in Shared and implements service in .Server
          - `git checkout grpc`
          - See .proto file
          - See that the DTO types are now codegenned, but we can still add more members via partial classes
          - See gRPC-Web enabled service on server
        - Make client issue calls via gRPC
          - Add FlightDataClient DI service
          - Update AirportsList.razor to call via gRPC - see it in browser
          - Update AppState.cs to do search via gRPC - see it in browser
        - Demo adding a new RPC endpoint to track items being added to shortlist
  - [6] Unit testing
        - Explain goals, pros/cons of unit vs browser automation tests
        - Add new ShortlistTests.cs class
          - Implement test for CanDisplayEmpty - passes
          - Implement test for RoundsUpPrice - fails, then implement, then passes
        - Look at SearchTests.cs
          - Read SendsSearchCriteria and ShowsSearchResults tests
          - Add new WhileSearchIsPending_ShowsLoadingState test - fails, then implement, then passes
        - Summarise purpose and that this is an experiment so far
  - [3] Attach-to-process from VS
  - [8] WebWindow
        - create new console app project
        - paste in some csproj stuff
        - see it runs except got wrong backend URL
        - fix via adding appsettings.json & Startup.cs code
        - see same thing running on macOS

Total: 29 mins
