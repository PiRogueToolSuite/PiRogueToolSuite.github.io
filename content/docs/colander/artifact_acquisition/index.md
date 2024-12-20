---
title: "Artifact acquisition"
draft: true
images: []
menu:
  docs:
    parent: "colander"
weight: 547
toc: true
---

## Abstract
Artifact acquisition can be done three ways :
  - Uploaded and created manually via [Artifact creation form](/docs/colander/artifact-management/#artifact-creation-form)
  - Imported remotely via [PiRogue experiment](/guides/g9/#import-artifacts) outcomes
  - Grabbed with a browser extension called [Colander Companion](#colander-companion)

## Colander Companion


{{< callout context="caution" title="Requirements" icon="alert-triangle" >}}
* Colander Companion is compatible with Mozilla Firefox
{{< /callout >}}

### Abstract

Colander Companion is a browser extension that facilitates web content capture.
The extension captures a static rendering of a webpage and transfers it to your personal Colander [drop zone](#drop-zone).

### Installation

{{< link-card
  icon="notes"
  title="Setup Colander Companion for desktop"
  description="Learn how to install and configure Colander Companion for desktop"
  href="/cookbooks/colander-companion-setup"
>}}

{{< link-card
  icon="notes"
  title="Setup Colander Companion for mobile or tablet"
  description="Learn how to install and configure Colander Companion for mobile or tablet"
  href="/cookbooks/colander-companion-mobile-setup"
>}}

### Usage

* Web content acquisition can be initiated at any point during a browsing session by clicking the Colander Companion extension icon.
* A pre-capture prompt allows the user to designate a case for association, but this step is not mandatory.
* To finalize the capture, press the `Capture` button.

Depending on the richness of the web content, the user has to wait the Colander Companion popup `Captured !`.

That's it, the user can continue its browsing session.

## Drop zone

### Abstract

The drop zone (aka drop box) is a temporary storage
where the user can easily and quickly upload any kind of file,
regardless of its nature.
All these files are potential evidences to be sorted and associated to a specific case.

Each Colander user has its own drop zone.

Evidences are uploaded into the drop zone using third party tools like [Colander Companion](#colander-companion).

When evidence acquisition is done, the user can then go back to its Colander account and
convert each dropped files into proper [Artifacts](/docs/colander/artifact-management/).

### Drop zone location

When connected to your Colander account:
  1. Click on `Colander` header to go back to home page
  2. Select `Drops` menu entry

{{< figure src="img/colander-dropzone-location.png" alt="Drop zone location" caption="Drop zone location" class="d-block mx-auto shadow" >}}

### Batch actions

In its drop zone, the user can process evidences in batches. The user has the choice to convert them to artifact or to delete them.

{{< callout context="caution" title="Requirements" icon="alert-triangle" >}}
* Delete action is destructive and can't be undone
{{< /callout >}}

If the user chooses not to keep certain uploads, it proceeds as follow:

1. Select one or more dropped files to delete
2. Click `Delete` action

{{< figure src="img/colander-dropzone-delete.png" alt="Drop zone delete action" caption="Drop zone delete action" class="d-block mx-auto shadow" >}}

If the user wants to keep files and associate them with a case, they're converted to Artifacts as follows:

1. Select one or more dropped files to review
2. Click `Review` action

{{< figure src="img/colander-dropzone-review.png" alt="Drop zone review action" caption="Drop zone review action" class="d-block mx-auto shadow" >}}

### Review and convert drops to Artifact

The review process is a wizard devided into few steps.
Each step asks the user various Artifact properties to be applied to **all** selected reviewed drops.
The user can cancel the reviewing process at any point in the wizard.

The case association is an important step, as it can't be changed later. Take care if you review drops in batch.
{{< figure src="img/colander-dropzone-review-step-1.png" alt="Drop zone review wizard" caption="Drop zone review wizard" class="d-block mx-auto shadow" >}}

In single drop review, the user can modify the `Name` of the destination Artifact.
In batch mode, the `Name` field keeps its original value, but the user can change it later in [Artifact management section](/docs/colander/artifact-management/).
All other properties are applied to the whole batch.
{{< figure src="img/colander-dropzone-review-step-2.png" alt="Drop zone review wizard" caption="Drop zone review wizard" class="d-block mx-auto shadow" >}}

The user can add attributes to Artifact at this step. All attribute values that are empty will be omitted.
{{< figure src="img/colander-dropzone-review-step-3.png" alt="Drop zone review wizard" caption="Drop zone review wizard" class="d-block mx-auto shadow" >}}

Last, the user can provide a more detailed description.
Clicking `Convert` will validate and launch the conversion to Artifact.
{{< figure src="img/colander-dropzone-review-step-4.png" alt="Drop zone review wizard" caption="Drop zone review wizard" class="d-block mx-auto shadow" >}}

After the conversion, Artifacts can be found in each destination case under [Artifact management section](/docs/colander/artifact-management/).