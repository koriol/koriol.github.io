# LMS Ecosystem Integration & Security Compliance

## The Panopto Integration: Multimedia Governance
In a Medical University, video is high-stakes. Whether it's a recorded surgery or a HIPAA-sensitive lecture, it is a must to ensure the video is discoverable for the right students but invisible to the public.

Faculty often struggle with complex software. I recommend Panopto Express because it’s "zero-install"—it runs in the browser. This reduces the Attack Surface on the local machine (no need to install third-party apps) and ensures a quick "Capture-to-Cloud" workflow.

**Goal:** Integrate a secure video "Vault" using Panopto, automate the LTI handshake, and remediate common "Access Denied" credential loops.

**Tools**
* **Panopto Express:** For zero-footprint faculty recording.
* **LTI 1.3 (Learning Tools Interoperability):** The secure protocol that connects Brightspace to Panopto.
* **D2L Video Note:** The native LMS alternative for short-form media.

**Skills**
* **Media Architecture:** Building a streaming pipeline that avoids local storage.
* **Identity Federation:** Understanding how a user "shares" their login from the LMS to the video server.
* **Troubleshooting Metadata:** Fixing broken permissions at the folder level.

### Simulating the Faculty Recording
Since we know this trial version has "weak" internal checking, we aren't going to trust the native "Upload Video" button (which often just treats a video like a static file). Instead, we are going to simulate the Panopto LTI Integration.

**Why?** If you just upload an MP4 to Brightspace, a student could potentially right-click and "Save Video As." If you use Panopto, the video is streamed in chunks, making it much harder to steal the Intellectual Property (IP).

> In a real university system, this would upload directly to a "Folder," but for this lab, we are going to manually upload it to Brightspace to simulate the LTI Embed process.

![](./brightspace/)
> *Provisioned clinical video assets using a secure multimedia pipeline. By bypassing standard file uploads in favor of an LTI-integrated streaming model, I implemented a layer of Intellectual Property (IP) protection that prevents unauthorized local downloads of university lectures.*



























