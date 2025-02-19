---
layout: docs
comment: no
header: true
seotitle: Release Notes | John Snow Labs
title: Release Notes
permalink: /docs/en/alab/release_notes
key: docs-training
modify_date: "2021-10-27"
use_language_switcher: "Python-Scala"
show_nav: true
sidebar:
    nav: annotation-lab
---

## 2.2.2
### Highlights
- Support for pretrained Relation Extraction and Assertion Status models. A valid Spark NLP for HealthCare License is needed to download pretrained models via the Models Hub page. After download, they can be added to the Project Config and used for preannotations.
- Support for uploading local images. Until this version, only images from remote URLs could be uploaded for Image projects. With this version the Annotation Lab supports uploading images from you local storage/computer. It is possible to either import one image or multiple images by zipping them together. The maximum image file size is 16 MB. If you need to upload files exceding the default configuration, please contact your system administrator who will change the limit size in the installation artifact and run the upgrade script.
- Improved support for Visual NER projects. A sample task can be imported from the Import page by clicking the "Add Sample Task" button. Also default config for the Visual NER project contains zoom feature which supports maximum possible width for low resolution images when zooming.
- Improved Relation Labeling. Creating numerous relations in a single task can look a bit clumsy. The limited space in Labeling screen, the relation arrows and different relation types all at once could create difficulty to visualize them properly. We improved the UX for this feature:
  - Spaces between two lines if relations are present
  - Ability to Filter by certain relations
  - When hovered on one relation, only that is focused
- Miscellaneous. Generally when a first completion in a task is submitted, it is very likely for that completion to be the ground truth for that task. Starting with this version, the first submitted completion gets automatically starred. Hitting submit button on next completion, annotator are asked to either just submit or submit and star it.

### Bug fixes
- On restart of the Annotation Lab machine/VM all Downloaded models (from Models Hub) compatible with Spark NLP 3.1 version were deleted. We have now fixed this issue. Going forward, it is user's responsibility to remove any incompatible models. Those will only be marked as "Incompatible" in Models Hub.
- This version also fixes some reported issues in training logs.
- The CONLL exports were including Assertion Status labels too. Going forward Assertion Status labels will be excluded given correct Project Config is setup.

{:.btn-block}
[Read more](https://www.johnsnowlabs.com/active-learning-for-relation-extraction-and-assertion-status-models-with-annotation-lab/){:.button.button--primary.button--rounded.button--lg}


## 2.1.0

### Highlights
- A new project configuration "Visual NER Labeling" was added, which provides the skeleton for text annotation on scanned images.
- Project Owners or Project Manager can train open-source models too.
- The UI components and navigation of Annotation Lab - as a SPA - continues to improve its performance.
- The application has an increased performance (security and bug fixes, general optimizations).
- More models & embeddings included in the Annotation Lab image used for deployments. This should reduce the burden for system admins during the installation in air-gapped or enterprise environments.
- Easier way to add relations. 
- Project Owners and Managers can see the proper status of tasks, taking into account their own completions.
- Security Fixes. We understand and take the security issues as the highest priority. On every release, we run our artifacts and images through series of security testings (Static Code analysis, PenTest, Images Vulnerabilities Test, AWS AMI Scan Test). This version resolves a few critical issues that were recently identified in Python Docker image we use. We have upgraded it to a higher version. Along with this upgrade, we have also refactored our codebase to pass our standard Static Code Analysis.

### Bug fixes
- An issue with using Uploaded models was fixed so any uploaded models can be loaded in Project Config and used for preannotation.
- Issues related to error messages when uploading a valid Spark OCR license and when trying to train NER models while Spark OCR license was expired are now fixed.
- The issue with exporting annotations in COCO format for image projects was fixed. Project Owners and Managers should be able to export COCO format which also includes images used for annotations.
- The bug reports related to unexpected scrolling of the Labeling page, issues in Swagger documentation, and typos in some hover texts are now fixed.

{:.btn-block}
[Read more](https://www.johnsnowlabs.com/model-tuning-and-transfer-learning-in-the-annotation-lab/){:.button.button--primary.button--rounded.button--lg}

## 2.0.1
### Highlights
- Inter-Annotation Agreement Charts. To get a measure of how well multiple annotators can make the same annotation decision for a certain category, we are shipping seven different charts. To see these charts users can click on the third tab “Inter-Annotator Agreement” of the Analytics Dashboard of NER projects. There are dropdown boxes to change annotators for comparison purposes. It is also possible to download the data of some charts in CSV format by clicking the download button present at the bottom right corner of each of them. 
- Updated CONLL Export. In previous versions, numerous files were created based on Tasks and Completions. There were issues in the Header and no sentences were detected. Also, some punctuations were not correctly exported or were missing. The new CONLL export implementation results in a single file and fixes all the above issues. As in previous versions, if only Starred completions are needed in the exported file, users can select the “Only ground truth” checkbox.
- Search tasks by label. Now, it is possible to list the tasks based on some annotation criteria. Examples of supported queries: "label: ABC", "label: ABC=DEF", "choice: Mychoice", "label: ABC=DEF".
- Validation of labels and models is done beforehand. An error message is shown if the label is incompatible with models.
- Transfer Learning support for Training Models. Now its is possible to continue model training from an already available model. If a Medical NER model is present in the system, the project owner or manager can go to Advanced Options settings of the Training section in the Setup Page and choose it to Fine Tune the model. When Fine Tuning is enabled, the embeddings that were used to train the model need to be present in the system. If present, it will be automatically selected, otherwise users need to go to the Models Hub page and download or upload it.
- Training Community Models without the need of License. In previous versions, Annotation Lab didn’t allow training without the presence of Spark NLP for Healthcare license. But now the training with community embeddings is allowed even without the presence of Valid license. 
- Support for custom training scripts. If users want to change the default Training script present within the Annotation Lab, they can upload their own training pipeline. In the Training section of the Project Setup Page, only admin users can upload the training scripts. At the moment we are supporting the NER custom training script only.
- Users can now see a proper message on the Modelshub page when annotationlab is not connected to the internet (AWS S3 to be more precise). This happens in air-gapped environments or some issues in the enterprise network.
- Users now have the option to download the trained models from the Models Hub page. The download option is available under the overflow menu of each Model on the “Available Models” tab.
- Training Live Logs are improved in terms of content and readability.
- Not all Embeddings present in the Models Hub are supported by NER and Assertion Status Training. These are now properly validated from the UI.
- Conflict when trying to use deleted embeddings. The existence of the embeddings in training as well as in deployment is ensured and a readable message is shown to users.
- Support for adding custom CA certificate chain. Follow the instructions described in instruction.md file present in the installation artifact.


### Bug fixes

- When multiple paged OCR file was imported using Spark OCR, the task created did not have pagination.
- Due to a bug in the Assertion Status script, the training was not working at all. 
- Any AdminUser could delete the main “admin” user as well as itself. We have added proper validation to avoid such situations.

{:.btn-block}
[Read more](https://www.johnsnowlabs.com/inter-annotator-agreement-charts-transfer-learning-training-without-license-custom-training-script-with-annotation-lab/){:.button.button--primary.button--rounded.button--lg}
