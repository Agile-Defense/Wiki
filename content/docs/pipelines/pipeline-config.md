---
title: "GoCD Configurations"
description: ""
lead: ""
date: 2020-10-06T08:48:57+00:00
lastmod: 2020-10-06T08:48:57+00:00
draft: false
images: []
menu:
  docs:
    parent: "pipelines"
weight: 50
toc: true
---

## Pipeline Configuration

### General

**Basic Settings**
| | | 
|-|-|
| Label Template | Defaults to `${COUNT}` which will uptick the run count each time the pipeline is run. For more information [see this](https://docs.gocd.org/21.2.0/configuration/pipeline_labeling.html). |
| Automatic pipeline scheduling | Uncheck this box only if you want the pipeline to be manually or API started. |

**Timer Settings**
| | | 
|-|-|
| Cron Timer Specification | Uses Cron-like syntax to schedule pipeline runs on specific intervals. For more information [see this](https://docs.gocd.org/21.2.0/configuration/admin_timer.html). |
| Run only on new material | Only available if Automatic Pipeline scheduling is off. This will ensure that timed or API based pipeline runs only run with new material. |

**Pipeline Locking Behavior**
| | | 
|-|-|
| Run multiple instances | Will allow multiple runs of the pipeline (`default`) |
| Run single instance of the pipeline and lock on failure | Will only allow a single instance of the pipeline to be run at one time. Will lock if pipeline fails. |
| Run single instance of pipeline at a time | Will only allow a single instance of the pipeline to be run at one time. Will **not** lock if pipeline fails. |


### Project Management

**Tracking Tool Integration**
| | | 
|-|-|
| Pattern | A regular expression to identify card or bug numbers from your checkin comments. For more information, [see this](https://docs.gocd.org/21.2.0/integration). |
| URI | The URI to your tracking tool. This must contain the string ${ID} which will be replaced with the number identified using the pattern. For more information, [see this](https://docs.gocd.org/21.2.0/integration). |

### Materials

Add or delete materials from the pipeline


### Stages

Add or delete stages from the pipeline.

You can also re-arrange the order by dragging and dropping the stage in the table by the 8 dots on the left side of the stage.

### Environment Variables

Add or delete environment variables for the entire pipeline

### Parameters

Add or delete parameters for the entire pipeline

## Stage Configuration

### Stage Settings
| | | 
|-|-|
| Stage name | The name of the stage **REQUIRED** |
| Trigger on completion of previous stage | If on, automatically starts this stage when the previous one is done |
| Allow only on success of previous stage | If on, only automatically triggers on `success` of previous stage |
| Fetch materials | Perform a git-fetch (or other equivalent) before running jobs |
| Never cleanup artifacts | If `Purge Artifacts` is configured at the GoCD server level, this ensures the artifacts are not removed. |
| Clean Working Directory | Removes working directory files *before* the start of a new run |

### Jobs

Add or delete jobs in the stage

### Environment Variables

Add or delete environment variables for just this stage

### Permissions
| | | 
|-|-|
| Inherit from Pipeline Group | Inherits permissions from group at the Pipeline level (`default`) |
| Specify locally | Define permission locally (will override pipeline group permissions) |

## Job Configuration

### Job Settings

**Basic Settings**
| | | 
|-|-|
| Job Name | Name of the job. **REQUIRED** |
| Resources | Specify which Agent resources are needed to complete all tasks in the job |
| Elastic Agent Profile ID | SThe Elastic Agent Profile that the current job requires to run. Requires a configured Elastic Agent Profile. |

**Job Timeout**
| | | 
|-|-|
| Never | Will run forever until succeeds or fails. |
| Use Default | Use default timeout of 30 minutes |
| Cancel after | Specify timeout in minutes of inactivity |

**Run Type**
| | | 
|-|-|
| Run on one instance | Will only run on a single agent (`default`) |
| Run on all agents | Will run on all available agents with matching resources. |
| Run instances | Will run the specified number of instances with available agents |


### Tasks

Add, edit, or delete tasks within the job.

### Artifacts

Add or remove artifacts. 

**Source**
The `Source` is the file or relative path to upload. If the source is set to `coverage.xml` it will look for that file in the job working directory. If the source is set to `outputs/*`, it will grab all files in the `outputs` directory.

**Destination**
The `Destination` directory is where it will put the artifacts on the GoCD server. If nothing is specified, it will put it in `testoutput` if it's a test artifact or in the artifact root if it's a built artifact. 

### Environment Variables

Add or delete environment variables for just this job

### Custom Tabs

Add or delete custom tabs for the job. 

| | | 
|-|-|
| Tab Name | The name for the tab |
| Path | The path to the file in the artifacts you want to display in the Job Details page. |
