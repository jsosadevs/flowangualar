# General Project Summary

This document provides a high-level overview of the project, its purpose, and its main modules.

## Project Purpose

The project appears to be a backoffice application for managing and running dynamic "flows." It seems to have two main sections: a dashboard for certificates and a backoffice for managing these flows.

## Main Modules

The application is divided into two primary modules:

* **Certificates:** This module, represented by the `CertificatesDashboardComponent`, likely displays a list of certificates and allows users to interact with them.
* **Backoffice:** This module, represented by the `BackofficeComponent`, is likely used for managing the "flows" that can be run within the application.

## Core Functionality

The core functionality of the application revolves around "flows." Users can select a flow and run it, which opens a modal (`FlowRunnerModalComponent`) to guide them through the process. The main application component (`AppComponent`) manages the state of the active module and the flow runner modal.