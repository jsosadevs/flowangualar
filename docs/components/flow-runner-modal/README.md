# Flow Runner Modal Component

The `FlowRunnerModalComponent` is a key component in the application, responsible for rendering and managing the execution of a "flow." It dynamically builds a form based on the current step of the flow and handles navigation between steps.

## Functionality

*   **Dynamic Form Generation:** The component creates a form with fields defined in the current step of the flow. It supports various field types, including text inputs and select dropdowns.
*   **State Management:** It uses a `FlowService` to manage the state of the flow, including the current step, completed steps, and the final result.
*   **Step Navigation:** The component provides "Next" and "Back" buttons to navigate between the steps of the flow.
*   **Dynamic Select Options:** It can fetch options for select fields dynamically from a service, and even supports dependent select fields where the options of one field depend on the value of another.
*   **Final Result Display:** Once the flow is complete, the component displays the final result to the user.

## Inputs

*   `flow: Flow | null`: The flow object to be executed. This is a required input.

## Outputs

*   `closeModal: void`: An event emitted when the modal should be closed.

## Dependencies

*   **`FlowService`:** This service is used to manage the state of the flow, fetch options for dynamic fields, and advance or regress the flow.
*   **`FormBuilder`:** An Angular service used to create the dynamic form.
*   **Angular Signals:** The component uses signals for reactive state management, including `flowState`, `fieldOptions`, and `fieldLoading`.
*   **RxJS:** Used for handling asynchronous operations, particularly for dynamic field option loading and managing subscriptions.

## Technical Details

*   **Reactive Forms:** The component uses Angular's `ReactiveFormsModule` to build and manage the dynamic form.
*   **`effect` and `computed`:** Angular's `effect` and `computed` functions are used to react to changes in the flow state and update the UI accordingly.
*   **`takeUntilDestroyed`:** This operator from `@angular/core/rxjs-interop` is used to automatically unsubscribe from observables when the component is destroyed, preventing memory leaks.
*   **Dynamic Field Logic:** The component contains complex logic for handling dynamic select fields, including disabling and enabling dependent fields and loading their options based on user input.