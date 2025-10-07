# Certificates Dashboard Component

The `CertificatesDashboardComponent` is responsible for displaying a filtered list of flow groups that are available in the "certificates" module.

## Functionality

*   **Filtered Flow Groups:** The component retrieves all flow groups from the `FlowService` and filters them to only include flows that have the `availableInCertificates` property set to `true`.
*   **Run Flow Requests:** It allows users to select a flow and emits an event to request its execution.

## Inputs

This component does not have any inputs.

## Outputs

*   `runFlowRequest: Flow`: An event emitted when the user requests to run a flow.

## Dependencies

*   **`FlowService`:** This service is used to retrieve the list of all flow groups.
*   **Angular Signals:** The component uses a `computed` signal (`publishedFlowGroups`) to create a derived list of filtered flow groups.

## Technical Details

*   **Standalone Component:** The component is a standalone Angular component.
*   **Computed Signal:** The use of a `computed` signal is an efficient way to derive the list of published flow groups. The list will automatically be recalculated whenever the `flowGroups` signal in the `FlowService` changes.
*   **Filtering Logic:** The filtering logic is simple and easy to understand, making the component's purpose clear.