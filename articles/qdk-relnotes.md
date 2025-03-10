---
author: bradben
description: Learn about the latest updates to the Microsoft Quantum Development Kit preview.
ms.author: v-benbra
ms.date: 02/01/2021
ms.service: azure-quantum
ms.subservice: qdk
ms.topic: conceptual
no-loc: ['Q#', '$$v']
title: Quantum Development Kit Release Notes
uid: microsoft.quantum.relnotes-qdk
---

# Release Notes

This article contains information on each Quantum Development Kit release.

For installation instructions, please refer to the [install guide](xref:microsoft.quantum.install-qdk.overview).

For update instructions, please refer to the [update guide](xref:microsoft.quantum.update-qdk).

## QDK Version 0.17.2105.144881

*Release date: June 1st, 2021*

- Reverted a change in the `azure-quantum` Python client that could create authentication issues for some users (refer to issues [#66](https://github.com/microsoft/qdk-python/issues/66), [#67](https://github.com/microsoft/qdk-python/issues/67)).

## QDK Version 0.17.2105.143879

*Release date: May 26th, 2021*

- Added a new function to the `azure-quantum` Python client to support the translation of binary optimization terms from `npz` to Azure Quantum. See full details in [QDK Python](https://github.com/microsoft/qdk-python/pull/61).
- Published [QIR oracle generation sample](https://github.com/microsoft/Quantum/issues/496). This program allows turns classical Q# functions on Boolean inputs into quantum implementations of that functions in terms of Q# operations at the level of QIR. This allows, for example, to implement quantum algorithms that are used by many quantum algorithms readily as classical functions.
- Fixed a bug that prevents QIR generation from being enabled in the iqsharp-base Docker image. See details [here](https://github.com/microsoft/iqsharp/issues/432).
- Implemented new special functions (e.g.: factorial and log-gamma) in Microsoft.Quantum.Math (microsoft/QuantumLibraries#448). Thanks to @TheMagicNacho for the contribution (microsoft/QuantumLibraries#440)!
- C# Client: Changed input data format type to "v2" for Quantum Computing. 
- Released Az CLI quantum extension version 0.5.0: Adapted to 'az' tool version 2.23.0, adding user agent information on calls to Azure Quantum Service.

## Azure Quantum service update
- Added PA (population annealing) and SSMC (sub-stochastic Monte Carlo) solvers along with preview access via a specialized SKU available to a subset of customers.
- Added support for new regions: Japan East, Japan West, UK South, UK West
- Set Provider in Failed state if provisioning fails. Previously it would be stuck in Launching/Updating state.
- Added help button in portal to direct user to support forum.
- Rendered provider cost in localized currency from Azure Marketplace.
- Added feedback button in portal to gather user feedback.
- Added quickstart guide in portal in overview blade.


## Version 0.16.2105.140472

*Release date: May 10th, 2021*

- Fixed dependency error in IQSharp on System.Text.Json when submitting jobs to Azure Quantum. See full details in issue [iqsharp#435](https://github.com/microsoft/iqsharp/issues/435).
- Resolved issue affecting joint measurements of multi-qubit states on some combinations of Pauli basis resulting in incorrect values. For details, please refer to issue [qsharp-runtime#680](https://github.com/microsoft/qsharp-runtime/issues/680).

## Version 0.16.2104.138035

*Release date: April 27th, 2021*

- Improved Q# type inference based on the Hindley-Milner type inference algorithm.
- Added support for NumPy types in coefficient definitions for problems in QIO Python SDK.
- Updated control-plane swagger file to [support restricted access SKUs](https://github.com/Azure/azure-rest-api-specs/pull/13002).
- Added new `StreamingProblem` class in QIO Python SDK. It supports the same interface for adding terms to a problem definition as the `Problem` class. However, once terms are added to the problem they are queued to be uploaded by a background thread and are not kept in memory for future reference.
- Restored the packages size of Microsoft.Quantum.Sdk and Microsoft.Quantum.Compiler back to normal. (See related note in 0.15.2103.133969)
- Improved compiler performance.
- Released Az CLI quantum extension version 0.4.0: Exposed URL for restricted access SKUs. Fixed regression on offerings commands dependent on Azure Markeplace APIs.

## Version 0.15.2103.133969

*Release date: March 30th, 2021*

- Released QIR emission as experimental feature (https://github.com/microsoft/qsharp-compiler/tree/main/src/QsCompiler/QirGeneration#qir-emission---preview-feature). The inclusion of the necessary LLVM packages, and in particular LlvmLibs, causes an increase in package size of the Microsoft.Quantum.Sdk and the Microsoft.Quantum.Compiler, and correspondingly to longer download times the first time the new versions are used. We are working on reducing that again in the future.
- Loosen restriction on AllowAtMostNCallsCA operation (https://github.com/microsoft/QuantumLibraries/pull/431).
- Added missing APIs for Math Library (https://github.com/microsoft/QuantumLibraries/issues/413).
- Removed <xref:Microsoft.Quantum.Environment.GetQubitsAvailableToBorrow> and <xref:Microsoft.Quantum.Environment.GetQubitsAvailableToUse> (https://github.com/microsoft/QuantumLibraries/issues/418).
- Fixed Q# Language Server fails during initialization in Visual Studio due to JsonReaderException (https://github.com/microsoft/qsharp-compiler/issues/885).
- Added support for multiple entry points.
- Released Az CLI quantum extension version 0.3.0: Updated command 'az quantum workspace create' to require an explicit list of Quantum providers and remove a default. Fixed issue with incorrect location parameter during job submission.

## Version 0.15.2102.129448

*Release date: February 25th, 2021*

- Improved IQ# debug user experience by adding a horizontal scrollbar to scroll both execution path and basis state visualizations.
- New functions to represent the group product and group inverse on the single-qubit Clifford group, to quickly define common single-qubit Clifford operators, and to apply single-qubit Clifford operators as operations. For more information, see issue [#409](https://github.com/microsoft/QuantumLibraries/issues/409).
- Addressing security issue in the Microsoft Quantum Development Kit for Visual Studio Code extension. For details, refer to [CVE-2021-27082](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2021-27082).
- Released Az CLI quantum extension version 0.2.0: Added parameter '--provider-sku-list' to 'az quantum workspace create' to allow specification of Quantum providers. Added command group 'az quantum offerings' with 'list', 'accept-terms' and 'show-terms'.

## Version 0.15.2102.128318

*Release date: February 12th, 2021*

- Fix "'npm' is not recognized as an internal or external command" error during creation of Q# projects with Visual Studio Code extension. See issue [#848](https://github.com/microsoft/qsharp-compiler/issues/848). 

## Version 0.15.2101.126940

*Release date: January 29th, 2021*

- Added project templates to Q# compiler for executables targeting IonQ and Honeywell providers
- Update IQ# kernel syntax highlighting to include changes to Q# syntax introduced in version [0.15.2101125897](#version-0152101125897)
- Bugfix to support passing arrays as input arguments to Q# programs submitted to Azure Quantum via `%azure.execute`, see issue [#401](https://github.com/microsoft/iqsharp/issues/401)
- Fix "Permission denied" error encountered using `az` inside of `iqsharp-base` Docker images, see issue [#404](https://github.com/microsoft/iqsharp/issues/404)
- Released Az CLI quantum extension version 0.1.0: Provided command line tool for workspace management and quantum computing job submission.

## Version 0.15.2101125897

*Release date: January 26th, 2021*

- Simplified qubit allocation, providing more convenient syntax for allocating qubits, [see details in Q# language repository](https://github.com/microsoft/qsharp-language/blob/main/Approved/1-implicitly-scoped-qubit-allocation.md).
- Created QDK-Python repository that includes `azure-quantum`, the Python client for submitting quantum-inspired optimization jobs to the Azure Quantum service, as well as `qdk`, including `qdk.chemistry`, a Python-based convenience layer for the Q# chemistry library that includes molecular visualization and functionality to generate input files for several chemistry packages such as NWChem, Psi4 and OpenMolcas.
- Parentheses are now optional for operation and function types and `if`, `elif`, `while` and `until` statements. Parentheses for `for`, `use` and `borrow` statements have been deprecated.
- Improved width estimates for optimal depth, [see details](https://github.com/MicrosoftDocs/quantum-docs-pr/pull/1159).
- Apply unitary operation provided as explicit matrix using `ApplyUnitary` ([QuantumLibraries#391](https://github.com/microsoft/QuantumLibraries/pull/391), external contribution by Dmytro Fedoriaka)
- Fixed https://github.com/microsoft/iqsharp/issues/387 by mitigating performance impact on IQ# kernel startup.

## Version 0.14.2011120240

*Release date: November 25th, 2020*

- Improved compiler performance due to faster reference loading.
- Added an [ANTLR grammar for Q#](https://github.com/microsoft/qsharp-language/tree/main/Specifications/Language/5_Grammar) to the Q# language specification.
- Updated the [`Microsoft.Quantum.Preparation` namespace](xref:Microsoft.Quantum.Preparation) to be more consistent with style guide and API design principles, and to support purified mixed states with additional data (see [proposal](https://github.com/microsoft/QuantumLibraries/issues/344), [review notes](https://github.com/microsoft/QuantumLibraries/blob/main/Design/meetings/2020/api-design-2020-11-05.md) and PRs [#212](https://github.com/microsoft/QuantumLibraries/pull/212), [#322](https://github.com/microsoft/QuantumLibraries/pull/322), [#375](https://github.com/microsoft/QuantumLibraries/pull/375), [#376](https://github.com/microsoft/QuantumLibraries/pull/376)).
- Parentheses around repeated call expressions are now optional: `(Foo(x))(y)` may be written as `Foo(x)(y)`.
- Users of the Visual Studio or Visual Studio Code extensions who have installed .NET 5 or Visual Studio 16.8 may be prompted to install .NET Core 3.1 to continue to work with the extensions.

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+closed%3A2020-10-23..2020-11-18), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+closed%3A2020-10-23..2020-11-18), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+closed%3A2020-10-23..2020-11-18), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+closed%3A2020-10-23..2020-11-18), [IQ#](https://github.com/microsoft/iqsharp/pulls?q=is%3Apr+closed%3A2020-10-23..2020-11-18) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+closed%3A2020-10-23..2020-11-18).

## Version 0.13.20111004

*Release date: November 10th, 2020*

This release disables IntelliSense features for Q# files in Visual Studio and Visual Studio Code
when a project file is not present. This resolves an issue where IntelliSense features may stop
working after adding a new Q# file to a project (see [qsharp-compiler#720](https://github.com/microsoft/qsharp-compiler/issues/720)).

## Version 0.13.20102604

*Release date: October 27th, 2020*

This release contains the following:

- Resource estimation now emits simultaneously achievable depth and width estimates in addition to the qubit count. See [here](xref:microsoft.quantum.machines.overview.resources-estimator#metrics-reported) for details.

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+closed%3A2020-09-25..2020-10-22), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+closed%3A2020-09-25..2020-10-22), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+closed%3A2020-09-25..2020-10-22), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+closed%3A2020-09-25..2020-10-22), [IQ#](https://github.com/microsoft/iqsharp/pulls?q=is%3Apr+closed%3A2020-09-25..2020-10-22) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+closed%3A2020-09-25..2020-10-22).

## Version 0.12.20100504

*Release date: October 5th, 2020*

This release fixes a bug affecting load of Q# notebooks (see [iqsharp#331](https://github.com/microsoft/iqsharp/pull/331)).

## Version 0.12.20092803

*Release date: September 29th, 2020*

This release contains the following:

- Announcement and draft specification of [Quantum Intermediate Representation (QIR)](https://github.com/microsoft/qsharp-language/tree/main/Specifications/QIR#quantum-intermediate-representation-qir) intended as a common format across different front- and back-ends. See also our [blog post](https://devblogs.microsoft.com/qsharp/introducing-quantum-intermediate-representation-qir) on QIR.
- Launch of our new [Q# language repo](https://github.com/microsoft/qsharp-language) containing also the full [Q# documentation](https://github.com/microsoft/qsharp-language/tree/main/Specifications/Language#q-language).
- Performance improvements for QuantumSimulator for programs involving a large number of qubits: better application of gate fusion decisions; improved parallelization on Linux system; added intelligent scheduling of gate execution; bug fixes.
- IntelliSense features are now supported for Q# files in Visual Studio and Visual Studio Code even without a project file.
- Various Q#/Python interoperability improvements and bug fixes, including better support for NumPy data types.
- Improvements to the Microsoft.Quantum.Arrays namespace (see [microsoft/QuantumLibraries#313](https://github.com/microsoft/QuantumLibraries/issues/313)).
- Added a new [Repeat-Until-Success sample](https://github.com/microsoft/Quantum/tree/main/samples/algorithms/repeat-until-success) that uses only two qubits.

Since the last release, the default branch in each of our open source repositories has been renamed to `main`.

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+closed%3A2020-08-24..2020-09-24), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+closed%3A2020-08-24..2020-09-24), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+closed%3A2020-08-24..2020-09-24), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+closed%3A2020-08-24..2020-09-24), [IQ#](https://github.com/microsoft/iqsharp/pulls?q=is%3Apr+closed%3A2020-08-24..2020-09-24) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+closed%3A2020-08-24..2020-09-24).

## Version 0.12.20082513

*Release date: August 25th, 2020*

This release contains the following:

- New [Microsoft.Quantum.Random namespace](xref:Microsoft.Quantum.Random), providing a more convenient way to sample random values from within Q# programs. ([QuantumLibraries#311](https://github.com/microsoft/QuantumLibraries/pull/311), [qsharp-runtime#328](https://github.com/microsoft/qsharp-runtime/pull/328))
- Improved [Microsoft.Quantum.Diagnostics namespace](xref:Microsoft.Quantum.Diagnostics) with new [`DumpOperation` operation](xref:Microsoft.Quantum.Diagnostics.DumpOperation), and new operations for restricting qubit allocation and oracle calls. ([QuantumLibraries#302](https://github.com/microsoft/QuantumLibraries/pull/302))
- New [`%project` magic command](xref:microsoft.quantum.iqsharp.magic-ref.project) in IQ# and [`qsharp.projects` API](/python/qsharp-core/qsharp.projects.projects) in Python to support references to Q# projects outside the current workspace folder. See [iqsharp#277](https://github.com/microsoft/iqsharp/issues/277) for the current limitations of this feature. 
- Support for automatically loading `.csproj` files for IQ#/Python hosts, which allows external project or package references to be loaded at initialization time. See the guide for using [Q# with Python and Jupyter Notebooks](xref:microsoft.quantum.user-guide-qdk.overview.host-programs) for more details.
- Added ErrorCorrection.Syndrome sample.
- Added tunable coupling to SimpleIsing.
- Updated HiddenShift sample.
- Added sample for solving Sudoku with Grover's algorithm (external contribution)
- General bug fixes.

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+is%3Aclosed), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+is%3Aclosed), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed), [IQ#](https://github.com/microsoft/iqsharp/pulls?q=is%3Apr+is%3Aclosed) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+is%3Aclosed).  

## Version 0.12.20072031

*Release date: July 21st, 2020*

This release contains the following:

- Opened namespaces in Q# notebooks are now available when running all future cells. This allows, for example, namespaces to be opened once in a cell at the top of the notebook, rather than needing to open relevant namespaces in each code cell. A new `%lsopen` magic command displays the list of currently-opened namespaces.

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+is%3Aclosed), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+is%3Aclosed), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed), [IQ#](https://github.com/microsoft/iqsharp/pulls?q=is%3Apr+is%3Aclosed) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+is%3Aclosed).  

## Version 0.12.20070124

*Release date: July 2nd, 2020*

This release contains the following:

- New `qdk-chem` tool for converting legacy electronic structure problem serialization formats (for example, FCIDUMP) to [Broombridge](xref:microsoft.quantum.libraries.overview.chemistry.schema.broombridge)
- New functions and operations in the [`Microsoft.Quantum.Synthesis`](xref:Microsoft.Quantum.Synthesis) namespace for coherently applying classical oracles using transformation- and decomposition-based synthesis algorithms.
- IQ# now allows arguments to the `%simulate`, `%estimate`, and other magic commands. See the [`%simulate` magic command reference](xref:microsoft.quantum.iqsharp.magic-ref.simulate) for more details.
- New phase display options in IQ#. See the [`%config` magic command reference](xref:microsoft.quantum.iqsharp.magic-ref.config) for more details.
- IQ# and the `qsharp` Python package are now provided via conda packages ([qsharp](https://anaconda.org/quantum-engineering/qsharp) and [iqsharp](https://anaconda.org/quantum-engineering/iqsharp)) to simplify local installation of Q# Jupyter and Python functionality to a conda environment. See the [Q# Jupyter Notebooks](xref:microsoft.quantum.install-qdk.overview.jupyter) and [Q# with Python](xref:microsoft.quantum.install-qdk.overview.python) installation guides for more details.
- When using the simulator, qubits no longer need to be in the |0⟩ state upon release, but can be automatically reset if they were measured immediately before releasing.
- Updates to make it easier for IQ# users to consume library packages with different QDK versions, requiring only major & minor version numbers match rather than the exact same version
- Removed deprecated `Microsoft.Quantum.Primitive.*` namespace
- Moved operations:
  - `Microsoft.Quantum.Intrinsic.Assert` is now `Microsoft.Quantum.Diagnostics.AssertMeasurement`
  - `Microsoft.Quantum.Intrinsic.AssertProb` is now `Microsoft.Quantum.Diagnostics.AssertMeasurementProbability`
- Bug fixes 

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+is%3Aclosed), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+is%3Aclosed), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed), [IQ#](https://github.com/microsoft/iqsharp/pulls?q=is%3Apr+is%3Aclosed) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+is%3Aclosed).  

## Version 0.11.2006.403

*Release date: June 4th, 2020*

This release fixes a bug affecting compilation of Q# projects.

## Version 0.11.2006.207

*Release date: June 3rd, 2020*

This release contains the following:

- Q# notebooks and Python host programs will no longer fail when a Q# entry point is present
- Updates to [Standard library](xref:microsoft.quantum.libraries.overview.standard.intro) to use access modifiers
- Compiler now allows plug-in of rewrite steps between built-in rewrite steps
- Several deprecated functions and operations have been removed following the schedule described in our [API principles](xref:microsoft.quantum.contributing-qdk.overview.api-design). Q# programs and libraries that build without warnings in version 0.11.2004.2825 will continue to work unmodified.

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+is%3Aclosed), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+is%3Aclosed), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed), [IQ#](https://github.com/microsoft/iqsharp/pulls?q=is%3Apr+is%3Aclosed) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+is%3Aclosed).  

> [!NOTE]
> This version contains a bug affecting compilation of Q# projects. We recommend upgrading to a newer release.

## Version 0.11.2004.2825

*Release date: April 30th, 2020*

This release contains the following:

- New support for Q# applications, which no longer require a C# or Python host file. For more information on getting started with Q# applications, see [here](xref:microsoft.quantum.install-qdk.overview.standalone).
- Updated quantum random number generator quickstart to no longer require a C# or Python host file. See the updated  [Quickstart](xref:microsoft.quantum.tutorial-qdk.random-number)
- Performance improvements to IQ# Docker images

> [!NOTE]
> Q# applications using the new [`@EntryPoint()`](xref:Microsoft.Quantum.Core.EntryPoint) attribute currently cannot be called from Python or .NET host programs.
> See the [Python](xref:microsoft.quantum.install-qdk.overview.python) and [.NET interoperability](xref:microsoft.quantum.install-qdk.overview.cs) guides for more information.

## Version 0.11.2003.3107

*Release date: March 31, 2020*

This release contains minor bugfixes for version 0.11.2003.2506.

## Version 0.11.2003.2506

*Release date: March 26th, 2020*

This release contains the following:

- New support for access modifiers in Q#
- Updated to .NET Core SDK 3.1

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+is%3Aclosed), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+is%3Aclosed), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+is%3Aclosed).  

## Version 0.10.2002.2610

*Release date: February 27th, 2020*

This release contains the following:

- New Quantum Machine Learning library, for more information go to our [QML docs page](xref:microsoft.quantum.libraries-machine-learning.overview)
- IQ# bug fixes, resulting in up to a 10-20x performance increase when loading NuGet packages

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+is%3Aclosed), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+is%3Aclosed), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+is%3Aclosed).  

## Version 0.10.2001.2831

*Release date: January 29th, 2020*

This release contains the following:

- New Microsoft.Quantum.SDK NuGet package which will replace Microsoft.Quantum.Development.Kit NuGet package when creating new projects. Microsoft.Quantum.Development.Kit NuGet package will continue to be supported for existing projects. 
- Support for Q# compiler extensions, enabled by the new Microsoft.Quantum.SDK NuGet packge, for more information see the [documentation on Github](https://github.com/microsoft/qsharp-compiler/tree/main/src/QuantumSdk#extending-the-q-compiler), the [compiler extensions sample](https://github.com/microsoft/qsharp-compiler/tree/main/examples/CompilerExtensions) and the [Q# Dev Blog](https://devblogs.microsoft.com/qsharp/extending-the-q-compiler/)
- Added support for .NET Core 3.1, it is highly recommended to have version 3.1.100 installed since building with older .NET Core SDK versions may cause issues
- New compiler transformations available under Microsoft.Quantum.QsCompiler.Experimental
- New functionality to expose output state vectors as HTML in IQ#
- Added support for EstimateFrequencyA to Microsoft.Quantum.Characterization for Hadamard and SWAP tests
- AmplitudeAmplification namespace now uses Q# style guide

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+is%3Aclosed), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+is%3Aclosed), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+is%3Aclosed).  

## Version 0.10.1912.0501

*Release date: December 5th, 2019*

This release contains the following:

- New Test attribute for Q# unit testing, see updated API documentation [here](xref:Microsoft.Quantum.Diagnostics.Test) and updated testing & debugging guide [here](xref:microsoft.quantum.user-guide-qdk.overview.testingdebugging)
- Added stack trace in the case of a Q# program run error
- Support for breakpoints in Visual Studio Code due to an update in the [OmniSharp C# Visual Studio Code extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+is%3Aclosed), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+is%3Aclosed), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+is%3Aclosed).  

## Version 0.10.1911.1607

*Release date: November 17th, 2019*

This release contains the following:

- Performance fix for [Quantum Katas](https://github.com/Microsoft/QuantumKatas) and Jupyter notebooks

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+is%3Aclosed), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+is%3Aclosed), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+is%3Aclosed).  


## Version 0.10.1911.307

*Release date: November 1st, 2019*

This release contains the following:

- Updates to Visual Studio Code & Visual Studio extensions to deploy language server as a self-contained executable file, eliminating the .NET Core SDK version dependency  
- Migration to .NET Core 3.0
- Breaking change to Microsoft.Quantum.Simulation.Core.IOperationFactory with introduction of new `Fail` method. It affects only custom simulators that do not extend SimulatorBase. For more details, [view the pull request on GitHub](https://github.com/microsoft/qsharp-runtime/pull/59).
- New support for Deprecated attributes

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+is%3Aclosed), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+is%3Aclosed), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+is%3Aclosed).  

## Version 0.9.1909.3002

*Release date: September 30th, 2019*

This release contains the following:

- New support for Q# code completion in Visual Studio 2019 (versions 16.3 & later) & Visual Studio Code
- New [Quantum Kata](https://github.com/Microsoft/QuantumKatas) for quantum adders

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+is%3Aclosed), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+is%3Aclosed), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+is%3Aclosed).  

## Version 0.9 (*PackageReference 0.9.1908.2902*)

*Release date: August 29th, 2019*

This release contains the following:

- New support for [conjugation statements](xref:microsoft.quantum.qsharp.conjugations#conjugations) in Q#
- New code actions in the compiler, such as: "replace with", "add documentation", and simple array item update
- Added install template and new project commands to Visual Studio Code extension
- Added new variants of ApplyIf combinator such as [Microsoft.Quantum.Canon.ApplyIfOne](xref:Microsoft.Quantum.Canon.ApplyIfOne)
- Additional [Quantum Katas](https://github.com/Microsoft/QuantumKatas) converted to Jupyter Notebooks
- Visual Studio Extension now requires Visual Studio 2019

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed), [compiler](https://github.com/microsoft/qsharp-compiler/pulls?q=is%3Apr+is%3Aclosed), [runtime](https://github.com/microsoft/qsharp-runtime/pulls?q=is%3Apr+is%3Aclosed), [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed) and [Katas](https://github.com/microsoft/QuantumKatas/pulls?q=is%3Apr+is%3Aclosed).  

The changes are summarized here as well as instructions for upgrading your existing programs.  Read more about these changes on the [Q# dev blog](https://devblogs.microsoft.com/qsharp).

## Version 0.8 (*PackageReference 0.8.1907.1701*)

*Release date: July 12, 2019*

This release contains the following:

- New indexing for slicing arrays, [see the language reference](xref:microsoft.quantum.qsharp.contextualexpressions#contextual-and-omitted-expressions) for more information.
- Added Dockerfile hosted on the [Microsoft Container Registry](https://github.com/microsoft/ContainerRegistry), see the [IQ# repository for more information](https://github.com/microsoft/iqsharp/blob/main/README.md)
- Breaking change for [the trace simulator](xref:microsoft.quantum.machines.overview.qc-trace-simulator.intro), update to configuration settings, name changes; see the [.NET API Browser for the updated names](/dotnet/api/microsoft.quantum.simulation.simulators.qctracesimulators.qctracesimulatorconfiguration).

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed) and [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed).  

## Version 0.7 (*PackageReference 0.7.1905.3109*)

*Release date: May 31, 2019*

This release contains the following:
- additions to the Q# language, 
- updates to the chemistry library, 
- a new numerics library.

See the full list of closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed) and [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed).  

The changes are summarized here as well as instructions for upgrading your existing programs.  Read more about these changes on the [Q# dev blog](https://devblogs.microsoft.com/qsharp).

### Q# language syntax
This release adds new Q# language syntax:
* Add named items for [user-defined types](xref:microsoft.quantum.qsharp.typedeclarations#type-declarations).  
* User-defined type constructors can now be used as functions.
* Add support for [copy-and-update](xref:microsoft.quantum.qsharp.copyandupdateexpressions#copy-and-update-expressions) and [apply-and-reassign](xref:microsoft.quantum.qsharp.variabledeclarationsandreassignments#evaluate-and-reassign-statements) in user-defined types.
* Fixup-block for [repeat-until-success](xref:microsoft.quantum.qsharp.conditionalloops#repeat-statement) loops is now optional.
* We now support while loops in functions (not in operations).

### Library 

This release adds a numerics library: Learn more about how to [use the new numerics library](xref:microsoft.quantum.libraries-numerics.usage) and try out the [new samples](https://github.com/microsoft/Quantum/tree/main/samples/numerics).  [PR #102](https://github.com/Microsoft/QuantumLibraries/pull/102).  
This release reorganizes extends and updates the chemistry library:

* Improves modularity of components, extensibility, general code cleanup.  [PR #58](https://github.com/microsoft/QuantumLibraries/pull/58).
* Add support for [multi-reference wavefunctions](xref:microsoft.quantum.libraries.overview-chemistry.concepts.multireference), both sparse multi-reference wavefunctions and unitary coupled cluster.  [PR #110](https://github.com/Microsoft/QuantumLibraries/pull/110).
* (Thank you!) [1QBit](https://1qbit.com) contributor ([@valentinS4t1qbit](https://github.com/ValentinS4t1qbit)): Energy evaluation using variational ansatz. [PR #120](https://github.com/Microsoft/QuantumLibraries/pull/120).
* Updating [Broombridge](xref:microsoft.quantum.libraries.overview.chemistry.schema.broombridge) schema to new [version 0.2](xref:microsoft.quantum.libraries.overview.chemistry.schema.spec_v_0_2), adding unitary coupled cluster specification. [Issue #65](https://github.com/microsoft/QuantumLibraries/issues/65).
* Adding Python interoperability to chemistry library functions. Try out this [sample](https://github.com/microsoft/Quantum/tree/main/samples/chemistry/PythonIntegration). [Issue #53](https://github.com/microsoft/QuantumLibraries/issues/53) [PR #110](https://github.com/Microsoft/QuantumLibraries/pull/110).

## Version 0.6.1905

*Release date: May 3, 2019*

This release contains the following:
- makes changes to the Q# language, 
- restructures the Quantum Development Kit libraries, 
- adds new samples, and 
- fixes bugs.  Several closed PRs for [libraries](https://github.com/Microsoft/QuantumLibraries/pulls?q=is%3Apr+is%3Aclosed) and [samples](https://github.com/Microsoft/Quantum/pulls?q=is%3Apr+is%3Aclosed).  

The changes are summarized here as well as instructions for upgrading your existing programs.  You can read more about these changes on devblogs.microsoft.com/qsharp.

### Q# language syntax
This release adds new Q# language syntax:
* Add a [shorthand way to express specializations of quantum operations](xref:microsoft.quantum.qsharp.specializationdeclarations) (control and adjoints) with `+` operators.  The old syntax is deprecated.  Programs that use the old syntax (for example, `: adjoint`) will continue to work, but a compile time warning will be generated.  
* Add a new ternary operator for [copy-and-update](xref:microsoft.quantum.qsharp.copyandupdateexpressions#copy-and-update-expressions), `w/` `<-`, can be used to express array creation as a modification of an existing array.
* Add the common [apply-and-reassign statement](xref:microsoft.quantum.qsharp.variabledeclarationsandreassignments#evaluate-and-reassign-statements), for example, `+=`, `w/=`.
* Add a way to specify a short name for namespaces in [open directives](xref:microsoft.quantum.qsharp.namespaces#open-directives).

With this release, we no longer allow an array element to be specified on the left side of a set statement.  This is because that syntax implies that arrays are mutable when in fact, the result of the operation has always been the creation of a new array with the modification.  Instead, a compiler error will be generated with a suggestion to use the new copy-and-update operator, `w/`, to accomplish the same result.  

### Library restructuring
This release reorganizes the libraries to enable their growth in a consistent way:
* Renames the Microsoft.Quantum.Primitive namespace  to Microsoft.Quantum.Intrinsic.  These operations are implemented by the target machine.  The Microsoft.Quantum.Primitive namespace is deprecated.  A runtime warning will advise when programs call operations and functions using deprecated names.

* Renames the Microsoft.Quantum.Canon package to Microsoft.Quantum.Standard.  This package contains namespaces that are common to most Q# programs.  This includes:  
    - Microsoft.Quantum.Canon for common operations
    - Microsoft.Quantum.Arithmetic for general purpose arithmetic operations
    - Microsoft.Quantum.Preparation for operations used to prepare qubit state
    - Microsoft.Quantum.Simulation for simulation functionality

With this change, programs that include a single "open" statement for the namespace Microsoft.Quatum.Canon may encounter build errors if the program references operations that were moved to the other three new namespaces.  Adding the additional open statements for the three new namespaces is a straightforward way to resolve this issue.  

* Several namespaces have been deprecated as the operations within have been reorganized to other namespaces. Programs that use these namespaces will continue to work, and a compile time warning will denote the namespace where the operation is defined.  

* The Microsoft.Quantum.Arithmetic namespace has been normalized to use the <xref:Microsoft.Quantum.Arithmetic.LittleEndian> user-defined type. Use the function [BigEndianAsLittleEndian](xref:Microsoft.Quantum.Arithmetic.BigEndianAsLittleEndian) when needed to convert to little endian.  

* The names of several callables (functions and operations) have been changed to conform to the [Q# Style Guide](xref:microsoft.quantum.contributing-qdk.overview.style).  The old callable names are deprecated.  Programs that use the old callables will continue to work with a compile time warning. 

### New Samples

We added a [sample of using Q# with F# driver](https://github.com/Microsoft/Quantum/pull/164).  

**Thank you!** to the following contributor to our open code base at http://github.com/Microsoft/Quantum. These contributions add significantly to the rich samples of Q# code:

* Mathias Soeken ([@msoeken](https://github.com/msoeken)): Oracle function synthesis. [PR #135](https://github.com/Microsoft/Quantum/pull/135).

### Migrating existing projects to 0.6.1905.

See the [install guide](xref:microsoft.quantum.install-qdk.overview) to update the QDK.
  
If you have existing Q# projects from version 0.5 of the Quantum Development Kit, the following are the steps to migrate those projects to the newest version.

1. Projects need to be upgraded in order.  If you have a solution with multiple projects, update each project in the order they are referenced.
2. From a command prompt, Run `dotnet clean` to remove all existing binaries and intermediate files.
3. In a text editor, edit the .csproj file to change the version of all the "Microsoft.Quantum" `PackageReference` to version 0.6.1904, and change the "Microsoft.Quantum.Canon" package name to "Microsoft.Quantum.Standard", for example:

    ```xml
    <PackageReference Include="Microsoft.Quantum.Standard" Version="0.6.1905.301" />
    <PackageReference Include="Microsoft.Quantum.Development.Kit" Version="0.6.1905.301" />
    ```
4. From the command prompt, run this command: `dotnet msbuild`  
5. After running this, you might still need to manually address errors due to changes listed above.  In many cases, these errors will also be reported by IntelliSense in Visual Studio or Visual Studio Code.
    - Open the root folder of the project or the containing solution in Visual Studio 2019 or Visual Studio Code.
    - After opening a .qs file in the editor, you should see the output of the Q# language extension in the output window.
    - After the project has loaded successfully (indicated in the output window) open each file and manually to address all remaining issues.

> [!NOTE]
> * For the 0.6 release, the language server included with the Quantum Development Kit does not support multiple workspaces.
> * In order to work with a project in Visual Studio Code, open the root folder containing the project itself and all referenced projects.   
> * In order to work with a solution in Visual Studio, all projects contained in the solution need to be in the same folder as the solution or in one of its subfolders.  
> * References between projects migrated to 0.6 and higher and projects using older package versions are **not** supported.

## Version 0.5.1904

*Release date: April 15, 2019*

This release contains bug fixes.


## Version 0.5.1903

*Release date: March 27, 2019*

This release contains the following:

- Adds support for Jupyter Notebook, which offers a great way to learn about Q#.  [Check out new Jupyter Notebook samples and learn how to write your own Notebooks](xref:microsoft.quantum.install-qdk.overview). 

- Adds integer adder arithmetic to the Quantum Canon library.  See also a Jupyter Notebook that [describes how to use the new integer adders](https://github.com/microsoft/Quantum/blob/main/samples/arithmetic/AdderExample.ipynb).

- Bug fix for DumpRegister issue reported by the community ([#148](https://github.com/Microsoft/Quantum/issues/148)).

- Added ability to return from within a [using- and borrowing-statement](xref:microsoft.quantum.qsharp.quantummemorymanagement#quantum-memory-management).

- Revamped [getting started guide](xref:microsoft.quantum.install-qdk.overview).


## Version 0.5.1902

*Release date: February 27, 2019*

This release contains the following:

- Adds support for a cross-platform Python host.  The `qsharp` package for Python makes it easy to simulate Q# operations and functions from within Python. Learn more about [Python interoperability](xref:microsoft.quantum.install-qdk.overview). 

- The Visual Studio and Visual Studio Code extensions now support renaming of symbols (for example, functions and operations).

- The Visual Studio extension can now be installed on Visual Studio 2019.

## Version 0.4.1901

*Release date: January 30, 2019*

This release contains the following:

- adds support for a new primitive type, BigInt, which represents a signed integer of arbitrary size.  Learn more about [BigInt](xref:microsoft.quantum.qsharp.valueliterals#bigint-literals).
- adds new Toffoli simulator, a special purpose fast simulator that can simulate X, CNOT and multi-controlled X quantum operations with very large numbers of qubits.  Learn more about [Toffoli simulator](xref:microsoft.quantum.machines.overview.toffoli-simulator).
- adds a simple resource estimator that estimates the resources required to run a given instance of a Q# operation on a quantum computer.  Learn more about the [Resource Estimator](xref:microsoft.quantum.machines.overview.resources-estimator).


## Version 0.3.1811.2802

*Release date: November 28, 2018*

Even though our VS Code extension was not using it, it was flagged and removed from the marketplace during
[the extensions purge](https://code.visualstudio.com/blogs/2018/11/26/event-stream) related to the `event-stream` NPM package. 
This version removes all runtime dependencies that could make the extension trigger any red flags.

If you had previously installed the extension you will need to install it again by visiting 
the [Microsoft Quantum Development Kit for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=quantum.quantum-devkit-vscode) extension on the Visual Studio Marketplace and press Install. We are sorry about the inconvenience.


## Version 0.3.1811.1511

*Release date: November 20, 2018*

This release fixes a bug that prevented some users to successfully load the Visual Studio extension.

## Version 0.3.1811.203

*Release date: November 2, 2018*

This release includes a few bug fixes, including:

* Invoking `DumpMachine` could change the state of the simulator under certain situations.
* Removed compilation warnings when building projects using a version of .NET Core previous to 2.1.403.
* Clean up of documentation, specially the tooltips shown during mouse hover in VS Code or Visual Studio.

## Version 0.3.1810.2508

*Release date: October 29, 2018*

This release includes new language features and an improved developer experience:

* This release includes a language server for Q#, as well as the client integrations for Visual Studio and Visual Studio Code. This enables a new set of IntelliSense features along with live feedback on typing in form of squiggly underlinings of errors and warnings. 
* This update greatly improves diagnostic messages in general, with easy navigation to and precise ranges for diagnostics and additional details in the displayed hover information.
* The Q# language has been extended in ways that unifies the ways developers can do common operations and new enhancements to the language features to powerfully express quantum computation.  There are a handful of breaking changes to the Q# language with this release.   

This release also includes a new quantum chemistry library:

* The chemistry library contains new Hamiltonian simulation features, including:
    - Trotter–Suzuki integrators of arbitrary even order for improved simulation accuracy.
    - Qubitization simulation technique with chemistry-specific optimizations for reducing $T$-gate complexity.
* A new open source schema, called Broombridge Schema (in reference to a [landmark](https://en.wikipedia.org/wiki/Broom_Bridge) celebrated as a birthplace of Hamiltonians), is introduced for importing representations of molecules and simulating them.
* Multiple chemical representations defined using the Broombridge Schema are provided.  These models were generated by [NWChem](http://www.nwchem-sw.org/), an open source high-performance computational chemistry tool.
* Tutorials and Samples describe how to use the chemistry library and the Broombridge data models to:
    - Construct simple Hamiltonians using the chemistry library
    - Visualize ground and excited energies of Lithium Hydride using phase estimation.
    - Perform resource estimates of quantum chemistry simulation.
    - Estimate energy levels of molecules represented by the Broombridge schema.
* Documentation describes how to use NWChem to generate additional chemical models for quantum simulation with Q#.

Learn more about the [Quantum Development Kit chemistry library](xref:microsoft.quantum.libraries.overview-chemistry.concepts.overview).

With the new chemistry library, we are separating out the libraries into a new GitHub repo, [Microsoft/QuantumLibraries](https://github.com/Microsoft/QuantumLibraries).  The samples remain in the repo [Microsoft/Quantum](https://github.com/Microsoft/Quantum).  We welcome contributions to both!

This release includes bug fixes and features for issues reported by the community.

### Community Contributions

**Thank you!** to the following contributors to our open code base at http://github.com/Microsoft/Quantum. These contributions add significantly to the rich samples of Q# code:

* Rolf Huisman ([@RolfHuisman](https://github.com/RolfHuisman)): Improved the experience for QASM/Q# developers by creating a QASM to Q# translator. [PR #58](https://github.com/Microsoft/Quantum/pull/58).

* Andrew Helwer ([@ahelwer](https://github.com/ahelwer)):  Contributed a sample implementing the CHSH Game, a quantum game related to non-locality.  [PR #84](https://github.com/Microsoft/Quantum/pull/84).

Thank you also to Rohit Gupta ([@guptarohit](https://github.com/guptarohit),[PR #90](https://github.com/Microsoft/quantum/pull/90)), Tanaka Takayoshi ([@tanaka-takayoshi](https://github.com/tanaka-takayoshi),[PR #289](https://github.com/MicrosoftDocs/quantum-docs-pr/pull/289)), and Lee James O'Riordan ([@mlxd](https://github.com/mlxd),[PR #96](https://github.com/Microsoft/Quantum/pull/96)) for their work improving the content for all of us through documentation, spelling and typo corrections! 

## Version 0.2.1809.701

*Release date: September 10, 2018*

This release includes bug fixes for issues reported by the community.

## Version 0.2.1806.3001

*Release date: June 30, 2018*

This releases is just a quick fix for [issue #48 reported on GitHub](https://github.com/Microsoft/Quantum/issues/48) (Q# compilation fails if user name contains a blank space). Follow same update instructions as `0.2.1806.1503` with the corresponding new version (`0.2.1806.3001-preview`).

## Version 0.2.1806.1503

*Release date: June 22, 2018*

This release includes several community contributions as well as an improved debugging experience and improved performance.  Specifically:

* Performance improvements on both small and large simulations for the QuantumSimulator target machine.
* Improved debugging functionality.
* Community contributions in bug fixes, new helper functions, operations and new samples.

### Performance improvements

This update includes significant performance improvements for simulation of large and small numbers of qubits for all the target machines.  This improvement is easily visible with the H<sub>2</sub> simulation that is a standard sample in the Quantum Development Kit.

### Improved debugging functionality

This update adds new debugging functionality:
* Added two new operations,  @"microsoft.quantum.extensions.diagnostics.dumpmachine" and @"microsoft.quantum.extensions.diagnostics.dumpregister" that output wave function information about the target quantum machine at a point in time.  
* In Visual Studio, the probability of measuring a $\ket{1}$ on a single qubit is now automatically shown in the debugging window for the QuantumSimulator target machine.
* In Visual Studio, improved the display of variable properties in the **Autos** and **Locals** debug windows. 

Learn more about [Testing and Debugging](xref:microsoft.quantum.user-guide-qdk.overview.testingdebugging).

### Community Contributions

The Q# coder community is growing and we are thrilled to see the first user contributed libraries and samples that were submitted to our open code base at http://github.com/Microsoft/quantum.  **A big Thank you!** to the following contributors:
* Mathias Soeken ([@msoeken](https://github.com/msoeken)):  contributed a sample defining a transformation based logic synthesis method that constructs Toffoli networks to implement a given permutation. The code is written entirely in Q# functions and operations.  [PR #41](https://github.com/Microsoft/Quantum/pull/41).
* RolfHuisman ([@RolfHuisman](https://github.com/RolfHuisman)): Microsoft MVP Rolf Huisman contributed a sample that generates flat QASM code from Q# code for a restricted class of programs that do not have classical control flow and restricted quantum operations. [PR #59](https://github.com/Microsoft/Quantum/pull/59)
* Sarah Kasier ([@crazy4pi314](https://github.com/crazy4pi314)): helped to improve our code base by submitting a library function for controlled operations. [PR #53](https://github.com/Microsoft/Quantum/pull/53)
* Jessica Lemieux ([@Lemj3111](https://github.com/Lemj3111)): fixed @"microsoft.quantum.canon.quantumphaseestimation" and created new unit tests.  [PR #54](https://github.com/Microsoft/Quantum/pull/54)
* Tama McGlinn ([@TamaMcGlinn](https://github.com/TamaMcGlinn)): cleaned the Teleportation sample by making sure the QuantumSimulator instance is disposed. [PR #20](https://github.com/Microsoft/Quantum/pull/20)

Additionally, a big **Thank You!** to these Microsoft Software Engineers from the Commercial Engineering Services team contributors who made valuable changes to our documentation during their Hackathon.  Their changes vastly improved the clarity and onboarding experience for all of us:
* Sascha Corti
* Mihaela Curmei
* John Donnelly
* Kirill Logachev
* Jan Pospisil
* Anita Ramanan
* Frances Tibble
* Alessandro Vozza

### Update existing projects

This release is fully backwards compatible. Just update the nuget pakages in your projects to version `0.2.1806.1503-preview` and do a **full rebuild** to make sure all intermediate files are regenerated.

From Visual Studio, follow the normal instructions on how to [update a package](/nuget/tools/package-manager-ui#updating-a-package).

To update project templates for the command line, run the following command:
```
dotnet new -i "Microsoft.Quantum.ProjectTemplates::0.2.1806.1503-preview"
```

After running this command, any new projects created using `dotnet new <project-type> -lang Q#` will automatically use this version of the Quantum Development Kit.

To update an existing project to use the newest version, run the following command from within the directory for each project:

```
dotnet add package Microsoft.Quantum.Development.Kit -v "0.2.1806.1503-preview"
dotnet add package Microsoft.Quantum.Canon -v "0.2.1806.1503-preview"
```

If an existing project also uses XUnit integration for unit testing, then a similar command can be used to update that package as well:
```
dotnet add package Microsoft.Quantum.Xunit -v "0.2.1806.1503-preview"
```

Depending on the version of XUnit that your test project uses, you may also need to update XUnit to 2.3.1:
```
dotnet add package xunit -v "2.3.1" 
```

After the update, make sure you remove all temporary files generated by the previous version by doing:
```
dotnet clean 
```

### Known Issues

No aditional known issues to report.


## Version 0.2.1802.2202

*Release date: February 26, 2018*

This release brings support for development on more platforms, language interoperability, and performance enhancements. Specifically:

- Support for macOS- and Linux-based development. 
- .NET Core compatibility, including support for Visual Studio Code across platforms.
- A full Open Source license for the Quantum Development Kit Libraries.
- Improved simulator performance on projects requiring 20 or more qubits.
- Interoperability with the Python language (preview release available on Windows).

### .NET Editions

The .NET platform is available through two different editions, the .NET Framework that is provided with Windows, and the open-source .NET Core that is available on Windows, macOS and Linux.
With this release, most parts of the Quantum Development Kit are provided as libraries for .NET Standard, the set of classes common to both Framework and Core.
These libraries are therefore compatible with recent versions of either .NET Framework or .NET Core.

Thus, to help ensure that projects written using the Quantum Development Kit are as portable as possible, we recommend that library projects written using the Quantum Development Kit target .NET Standard, while console applications target .NET Core.
Since previous releases of the Quantum Development Kit only supported .NET Framework, you may need to migrate your existing projects; see below for details on how to do this.

### Project Migration

Projects created using previous versions of Quantum Development Kit will still work, as long as you don't update the NuGet packages used in them. To migrate existing code to the new version, perform the following steps:
1. Create a new .NET Core project using the right type of Q# project template (Application, Library or Test Project).
2. Copy existing .qs and .cs/.fs files from the old project to the new project (using Add > Existing Item). Do not copy the AssemblyInfo.cs file.
3. Build and run the new project.

Please note that the operation RandomWalkPhaseEstimation from the namespace Microsoft.Quantum.Canon was moved into the namespace Microsoft.Research.Quantum.RandomWalkPhaseEstimation in the [Microsoft/Quantum-NC](https://github.com/microsoft/quantum-nc) repository.

### Known Issues

- The `--filter` option to `dotnet test` does not work correctly for tests written in Q#.
  As a result, individual unit tests cannot be run in Visual Studio Code; we recommend using `dotnet test` at the command prompt to re-run all tests.

## Version 0.1.1801.1707

*Release date: January 18, 2018*

This release fixes some issues reported by the community. Namely:

- The simulator now works with early non-AVX-enabled CPUs.
- Regional decimal settings will not cause the Q# parser to fail.
- `SignD` primitive operation now returns `Int` rather than `Double`.


## Version 0.1.1712.901

*Release date: December 11, 2017*

### Known Issues

#### Hardware and Software Requirements

- The simulator included with the Quantum Development Kit requires a 64-bit installation of Microsoft Windows to run.
- Microsoft's quantum simulator, installed with the Quantum Development Kit, utilizes Advanced Vector Extensions (AVX), and requires an AVX-enabled CPU. Intel processors shipped in Q1 2011 (Sandy Bridge) or later support AVX. We are evaluating support for earlier CPUs and may announce details at a later time.

#### Project Creation

- When creating a solution (.sln) that will use Q#, the solution must be one directory higher than each project (.csproj) in the solution. When creating a new solution, this can be accomplished by making sure that the "Create directory for solution" checkbox on the "New Project" dialog box is checked. If this is not done, the Quantum Development Kit NuGet packages will need to be installed manually.

#### Q#

- Intellisense does not display proper errors for Q# code. Make sure that you are displaying Build errors in the Visual Studio Error List to see correct Q# errors. Also note that Q# errors will not show up until after you've done a build.
- Using a mutable array in a partial application may lead to unexpected behavior.
- Binding an immutable array to a mutable array (let a = b, where b is a mutable array) may lead to unexpected behavior.
- Profiling, code coverage and other VS plugins may not always count Q# lines and blocks accurately.
- The Q# compiler does not validate interpolated strings. It is possible to create C# compilation errors by misspelling variable names or using expressions in Q# interpolated strings.

#### Simulation

- The Quantum Simulator uses OpenMP to parallelize the linear algebra required. By default OpenMP uses all available hardware threads, which means that programs with small numbers of qubits will often run slowly because the coordination required will dwarf the actual work. This can be fixed by setting the environment variable OMP_NUM_THREADS to a small number. As a very rough rule of thumb, 1 thread is good for up to about 4 qubits, and then an additional thread per qubit is good, although this is highly dependent on your algorithm.

#### Debugging

- F11 (step in) doesn't work in Q# code.
- Code highlighting in Q# code at a breakpoint or single-step pause is sometimes inaccurate. The correct line will be highlighted, but sometimes the highlight will start and end at incorrect columns on the line.

#### Testing

- Tests must be run in 64-bit mode. If your tests are failing with a BadImageFormatException, go to the Test menu and select Test Settings > Default Processor Architecture > X64.
- Some tests take a long time (possibly as much as 5 minutes depending on your computer) to run. This is normal, as some use over twenty qubits; our largest test currently runs on 23 qubits.

#### Samples

- On some machines, some small samples may run slowly unless the environment variable OMP_NUM_THREADS is set to "1". See also the release note under "Simulation".

#### Libraries

- There is an implicit assumption that the qubits passed to an operation in different arguments are all distinct. For instance, all of the library operations (and all of the simulators) assume that the two qubits passed to a controlled NOT are different qubits. Violating this assumption may lead to unpredictable unexpected. It is possible to test for this using the quantum computer tracer simulator.
- The Microsoft.Quantum.Bind function may not act as expected in all cases.
- In the Microsoft.Quantum.Extensions.Math namespace, the SignD function returns a Double rather than an Int, although the underlying System.Math.Sign function always returns an integer. It is safe to compare the result against 1.0, -1.0, and 0.0, since these doubles all have exact binary representations.
