# Algorithmic Detection and Tracking of Moving Celestial Objects from Astronomical Data

### Academic Project (AP)

An astronomical image-analysis system designed to identify and track potential moving celestial objects across multiple observations.

---

## Problem Statement

Astronomical images can contain stationary stars, moving celestial objects, background noise, and image artifacts. Inspecting each image independently makes it difficult to determine whether a source has genuinely moved between observations or whether an apparent change is caused by noise, image alignment, or measurement error.

This project aims to develop an algorithmic pipeline that analyses multiple suitable observations of the same or comparable region of the sky, detects sources in each observation, matches detections across observations, and identifies candidates whose apparent positions change over time.

**Core question:** How can repeated astronomical observations be analysed to identify and track potential moving celestial objects while reducing false detections caused by stationary sources, noise, and image artifacts?

---

## Project Objectives

- Read astronomical images stored in FITS format and inspect their metadata.
- Discover and retrieve suitable astronomical observations from supported archive services.
- Detect sources and estimate their positions in each image.
- Handle astronomical coordinate information and align images onto a common coordinate grid when necessary.
- Match detections across observations.
- Identify potential moving objects and estimate their apparent trajectories when sufficient observations are available.
- Provide interactive visualizations that help users inspect astronomical images, detections, and candidate tracks.
- Present the processing results in a web-based interface.

---

## Data Source and Background

The project is intended to work with suitable publicly available astronomical observations, with NASA's SPHEREx mission as the current data context. The selected observations must be verified for their suitability for source detection and motion tracking.

FITS (Flexible Image Transport System) is a standard astronomical file format used to store image data and associated metadata. Metadata such as coordinate information, observation identifiers, and timestamps—where available—is important when comparing images and estimating apparent motion.

- **Astronomical data context:** NASA SPHEREx
- **Primary data format:** FITS
- **Archive resource:** [NASA/IPAC Infrared Science Archive (IRSA)](https://irsa.ipac.caltech.edu/)

---

## Proposed Workflow

1. **Discover and retrieve data** — Find suitable observations from supported astronomical archives and retrieve the relevant files.
2. **Load observations** — Read FITS image data and inspect the associated headers and metadata.
3. **Preprocess images** — Examine image quality and apply appropriate background or noise handling when required.
4. **Detect sources** — Identify potential astronomical sources and estimate their positions.
5. **Align observations** — Use coordinate metadata and reproject images onto a common grid when necessary for meaningful comparison.
6. **Match detections** — Associate detections that may represent the same source across different observations.
7. **Identify motion candidates** — Look for sources whose measured positions change across observations.
8. **Estimate trajectories** — Use positions and observation times, when available, to estimate apparent motion.
9. **Visualize and review** — Display astronomical images, detections, comparisons, and candidate tracks so results can be inspected.

The precise algorithms and processing steps will be finalized as the data and implementation are validated.

---

## Technology Stack and Implementation Priority

The stack is divided by implementation priority so the first version can focus on a working scientific pipeline and web interface. Supporting tools will be added only when the workflow or application requirements call for them.

### 1. Core — Scientific Processing

| Technology | Purpose |
| --- | --- |
| Python | Main language for scientific processing and algorithm development |
| Astropy | Reading FITS files and handling astronomical metadata and World Coordinate System (WCS) coordinates |
| NumPy | Numerical operations on image arrays |
| SciPy | Scientific computations and image-processing utilities |
| FITS | Astronomical image data and associated metadata format |

This layer establishes the foundation: loading observations, inspecting metadata, working with image arrays, and implementing the initial detection and tracking algorithms.

### 2. Core — Web Application

| Technology | Purpose |
| --- | --- |
| Next.js | Web application framework |
| React | Building reusable user-interface components |
| TypeScript | Type-safe frontend development |
| Tailwind CSS | Styling and responsive layouts |
| PostgreSQL | Persistent storage for observation metadata, processing jobs, detections, and candidate tracks. |
| FastAPI | Exposing REST API endpoints between the web interface and Python processing pipeline |

This layer connects the scientific pipeline to a web interface and provides a way to submit processing requests and view results.

### 3. As Needed — Scientific Analysis and Visualization

| Technology | Purpose |
| --- | --- |
| Reproject | Aligning astronomical images onto a common coordinate grid when required |
| Photutils | Source detection and photometry using established astronomy tools |
| Plotly | Interactive plots and scientific data visualization |
| Canvas | Displaying astronomical images and supporting image interaction in the browser |
| PyVO / Astroquery | Discovering and retrieving data from supported astronomical archives |

These tools will be introduced as the data and workflow require them. PyVO and Astroquery may be alternatives or complementary tools; the final choice will depend on the selected archive interface and the queries needed. Both do not need to be adopted before archive access is tested.

### 4. Later — When Requirements Justify Them

| Technology | Purpose |
| --- | --- |
| WebGL | Specialized high-performance rendering for large images or complex interactive visualizations, if browser Canvas rendering is insufficient |

WebGL are not required for the initial version. They can be introduced if actual persistence, query, or rendering requirements justify the added complexity.

### Version Control

| Technology | Purpose |
| --- | --- |
| Git | Tracking source-code changes |
| GitHub | Hosting the repository and supporting collaboration |

### Why This Technology Stack?

The project combines a web interface with astronomy-focused scientific processing. Python, Astropy, NumPy, and SciPy form the initial scientific foundation; Next.js, React, TypeScript, and FastAPI connect that processing to a web application. Reproject, Photutils, and Plotly can be added when the workflow needs image alignment, established source-detection methods, or interactive scientific plots. WebGL are later options only if persistent storage or specialized rendering becomes necessary. Archive access will be tested before deciding whether to use PyVO, Astroquery, or both.

---

## Expected Outputs

Depending on the selected observations and the final implementation, the system is intended to provide:

- Detected sources for each observation.
- Matches between sources in different observations.
- Candidate moving objects with measured positions.
- Estimated apparent trajectories for candidates with sufficient observations.
- Interactive astronomical image views and plots for inspecting detections and candidate tracks.
- Results that can be reviewed alongside the methods, data, and limitations used to produce them.

These are intended outputs, not claims of validated detection performance. Actual results and evaluation metrics should be reported after testing.

---

## Scope and Limitations

- The project focuses on algorithmic image analysis and tracking; machine learning is not a required component of the current AP scope.
- Tracking quality depends on the suitability of the observations and the availability of reliable metadata and timestamps.
- Noise, artifacts, overlapping sources, and imperfect image alignment can cause missed detections or false positives.
- A candidate identified by the system is not automatically a confirmed celestial object and may require further validation.
- The final algorithms, dataset selection, and evaluation criteria will depend on testing and the characteristics of the available data.

---

## Academic Project Note

This project investigates an algorithmic approach to detecting and tracking potential moving objects in astronomical image data. The technology stack and workflow described here represent the current plan and should be refined to reflect the final implementation and experimental findings.

- **Status:** In development
- **Project type:** Academic Project (AP)
- **Scientific processing:** Python
- **Web application:** Next.js / React / TypeScript
