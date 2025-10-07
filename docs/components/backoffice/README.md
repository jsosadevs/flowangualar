# Backoffice Component

The `BackofficeComponent` serves as the main view for the "backoffice" module of the application. It's responsible for displaying a list of flow groups and providing access to the flow and query designers.

## Functionality

*   **Display Flow Groups:** The component retrieves and displays a list of flow groups from the `FlowService`.
*   **Design Mode:** It features a "design mode" that can be toggled by the user. When design mode is active, it displays the `FlowDesignerComponent` or `QueryDesignerComponent`.
*   **Tabbed Navigation:** In design mode, the component provides tabs to switch between the "flows" and "queries" designers.
*   **Run Flow Requests:** It emits an event to request the execution of a flow.

## Inputs

This component does not have any inputs.

## Outputs

*   `runFlowRequest: Flow`: An event emitted when the user requests to run a flow.

## Dependencies

*   **`FlowService`:** This service is used to retrieve the list of flow groups.
*   **`FlowDesignerComponent`:** A child component used for designing and editing flows.
*   **`QueryDesignerComponent`:** A child component used for designing and editing queries.
*   **Angular Signals:** The component uses signals (`designMode`, `designerTab`) to manage its internal state.

## Technical Details

*   **Standalone Component:** The component is a standalone Angular component, which means it manages its own dependencies.
*   **State Management:** The component's state is managed using Angular Signals, which provides a simple and efficient way to handle state changes.
*   **Child Components:** The component acts as a container for the `FlowDesignerComponent` and `QueryDesignerComponent`, which are displayed conditionally based on the `designMode` and `designerTab` signals.