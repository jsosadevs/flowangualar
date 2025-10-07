# Flow Service Documentation

The `FlowService` is a critical service in the application, acting as the central hub for all flow-related operations. It manages the state of running flows, handles CRUD operations for flows and their components, and orchestrates the execution of complex query chains.

## Responsibilities

*   **State Management:** Manages the entire lifecycle and state of a flow being executed by a user.
*   **Flow Execution Logic:** Contains the logic for starting, advancing, and regressing (going back) through the steps of a flow.
*   **Data Management:** Provides methods to create, read, update, and delete flow groups, flows, steps, and form fields. It currently uses mock data (`MOCK_FLOW_GROUPS`) but is designed to be connected to a real backend.
*   **Dynamic Data Fetching:** Collaborates with the `QueryManagerService` to fetch dynamic options for form fields (e.g., populating a 'Careers' dropdown based on a selected 'Faculty').
*   **Query Chain Execution:** Manages the execution of a series of dependent queries (`queryChain`) after a form step is submitted.

## State Management

The service exposes an observable `flowState$` that components can subscribe to for real-time updates on the status of a running flow.

-   **`flowState$: Observable<FlowState>`**: An observable that emits the current `FlowState` object. The state includes the `status` (`loading`, `ready`, `completed`, etc.), the `currentStep`, all data collected so far (`completedStepsPayload`), and any potential errors.

## Core Methods

### Flow Execution

-   **`startFlow(flowId: string): void`**: Initializes a flow execution. It finds the specified flow and sets the state to the first step.
-   **`advanceFlow(payload: AdvanceFlowPayload): void`**: Advances the flow to the next step. It collects the form data from the current step, updates the `completedStepsPayload`, and determines the next step. If the current step has a `queryChain`, it triggers its execution.
-   **`regressFlow(flowId: string): void`**: Moves the flow back to the previous step.

### Dynamic Options

-   **`fetchOptions(queryName: string, parentField: FormField, parentValue: string): Observable<FormFieldOption[]>`**: Fetches a list of options for a dynamic select field by executing a query via the `QueryManagerService`. It can pass the value of a parent field as a parameter for dependent queries.

## Query Chain Execution

One of the most powerful features of this service is its ability to execute a `queryChain`.

-   **`executeQueryChain(chain: QueryChainAction[], payload: ...): Observable<any>`**: This private method is triggered by `advanceFlow` when a step defines a `queryChain`. It executes a series of queries in sequence.
-   **Parameter Resolution**: It can resolve parameters for a query using data from the `payload` (all form data collected so far) or from the `results` of previous queries in the same chain. This allows for complex, dependent data operations (e.g., enroll a student, get the new student ID, and then use that ID to assign them a course).

## Data (CRUD) Operations

The service provides a set of methods to manage the flow definitions. These methods currently operate on the in-memory `MOCK_FLOW_GROUPS` data.

-   **Flow Groups:** `createFlowGroup(category: string)`
-   **Flows:** `createFlow(...)`, `updateFlow(...)`, `deleteFlow(...)`, `toggleFlowLock(...)`
-   **Steps:** `createStep(...)`, `updateStep(...)`, `reorderSteps(...)`
-   **Form Fields:** `addFormField(...)`, `updateFormField(...)`, `deleteFormField(...)`, `reorderFields(...)`

## Dependencies

-   **`QueryManagerService`**: This is a crucial dependency injected into the `FlowService`. It is responsible for the actual execution of named queries, which are used for both fetching dynamic field options and executing query chains. The `FlowService` acts as an orchestrator, while the `QueryManagerService` is the executor.

## Mock Data

The service is initialized with a set of mock flows and flow groups (`MOCK_FLOWS`, `MOCK_FLOW_GROUPS`). This allows the application to be developed and tested without a live backend. In a production scenario, all methods that modify flow data would be updated to make API calls to a persistent data store.