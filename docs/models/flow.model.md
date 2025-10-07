# Flow Model Documentation

This document describes the data models related to the "flow" functionality in the application. These models define the structure of flows, steps, fields, and the state of a running flow.

### `FormFieldOption`

Represents a single option in a select dropdown.

-   `value: string | number`: The actual value of the option.
-   `label: string`: The text displayed to the user for the option.

### `FormField`

Defines a single field within a form in a flow step.

-   `key: string`: A unique identifier for the field.
-   `label: string`: The text label displayed next to the form field.
-   `type: 'text' | ...`: The type of the input field (e.g., 'text', 'select').
-   `required: boolean`: Whether the field is mandatory.
-   `options?: FormFieldOption[]`: An array of options for 'select' type fields.
-   `queryName?: string`: The name of a query to execute to fetch options for a dynamic 'select' field.
-   `dependencyKey?: string`: The key of another field that this field depends on. Used for creating dependent dropdowns.

### `QueryChainAction`

Defines a query to be executed after a form step is successfully submitted.

-   `queryName: string`: The name of the query to execute.
-   `resultKey: string`: The key under which the result of the query will be stored.
-a  `parameters: { [key: string]: string }`: A map of parameters to be passed to the query. The values can be references to data from previous steps.

### `FlowStep`

Represents a single step within a flow.

-   `stepId: string`: A unique identifier for the step.
-   `title: string`: The title of the step, displayed to the user.
-   `description: string`: A description of what the step involves.
-   `formFields: FormField[]`: An array of form fields to be rendered in this step.
-   `queryChain?: QueryChainAction[]`: An optional chain of queries to be executed after this step is completed.

### `Flow`

The main interface representing a complete flow.

-   `id: string`: A unique identifier for the flow.
-   `name: string`: The name of the flow.
-   `description: string`: A description of the flow's purpose.
-   `steps: FlowStep[]`: An array of steps that make up the flow.
-   `locked?: boolean`: Whether the flow is locked for editing.
-   `availableInCertificates?: boolean`: A flag to indicate if the flow should be visible in the certificates dashboard.

### `FlowGroup`

A way to group related flows together in the UI.

-   `category: string`: The name of the category (e.g., "User Management").
-   `flows: Flow[]`: An array of flows belonging to this group.

### `FlowState`

Represents the complete state of a flow that is currently being executed.

-   `status: 'loading' | 'ready' | ...`: The current status of the flow execution.
-   `currentStep?: FlowStep`: The current active step.
-   `currentStepIndex?: number`: The index of the current step.
-   `completedStepsPayload: { [key: string]: any }`: An object containing all the data collected from the forms in the completed steps.
-   `error?: string`: An error message if the flow has encountered an error.
-   `flowId?: string`: The ID of the currently running flow.
-   `finalQueryResult?: any`: The result from the final query chain execution.

### `AdvanceFlowPayload`

The data payload required to advance a flow from one step to the next.

-   `flowId: string`: The ID of the flow to advance.
-   `currentStepId: string`: The ID of the step that was just completed.
-   `payload: { [key: string]: any }`: The form data from the completed step.