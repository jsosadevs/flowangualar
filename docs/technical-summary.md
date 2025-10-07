# Technical Summary

This document provides a summary of the technical aspects of the project, including the technologies used and the overall architecture.

## Technologies Used

* **Angular:** The application is built using the Angular framework, which provides a robust structure for building single-page applications.
* **TypeScript:** The code is written in TypeScript, which adds static typing to JavaScript, improving code quality and maintainability.
* **TailwindCSS:** The application uses TailwindCSS for styling, which allows for rapid development of custom user interfaces.
* **RxJS:** The project uses RxJS for reactive programming, which is a core part of the Angular framework.

## Architecture

The application follows a standard component-based architecture, which is typical for Angular projects. The main components are:

* **`AppComponent`:** The root component of the application, which manages the main layout and the state of the active module.
* **`CertificatesDashboardComponent`:** A component that likely displays a dashboard of certificates.
* **`BackofficeComponent`:** A component for managing "flows."
* **`FlowRunnerModalComponent`:** A modal component for running a selected "flow."

The application's state is managed using Angular Signals, a new feature in Angular that provides a more granular and efficient way to manage state changes.

## Dependencies

The project's dependencies are managed using `npm`. The key dependencies are listed in the `package.json` file and include:

* `@angular/core`: The core Angular framework.
* `@angular/common`: Common Angular pipes and directives.
* `@angular/forms`: Support for building forms in Angular.
* `rxjs`: The reactive programming library.
* `tailwindcss`: The CSS framework.