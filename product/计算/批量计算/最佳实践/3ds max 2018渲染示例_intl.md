## Quick Start
This document illustrates how to submit a job in the Batch Console to render and export a 3ds Max 2018 image. The steps are as follows:
### I. Making a Custom Image
1. Make a custom Windows image.
2. See the [official webpage](https://www.autodesk.com/products/3ds-max/overview) for how to install 3ds Max 2018.

> **Note: **
- Please temporarily turn off the Windows Firewall to avoid blocking software downloads.
- See [Display Driver Selection Dialog](https://knowledge.autodesk.com/zh-hans/support/3ds-max/learn-explore/caas/CloudHelp/cloudhelp/2015/CHS/3DSMax/files/GUID-3D6B4C8E-8C0D-4A9C-BFB0-2463803268CE-htm.html) for selecting an appropriate graphics card type to avoid graphics card initialization failure. In normal circumstances, it is recommended to select "Nitrous Software".

### II. Preparing the Rendering Files
There are two mainstream ways to store the rendering materials: [Cloud Object Storage (COS)](https://intl.cloud.tencent.com/document/product/436) and [Cloud File Storage (CFS)](https://intl.cloud.tencent.com/document/product/582). By configuring the mount parameters, Batch will mount COS or CFS to the local storage before the rendering job runs, so the renderer can access COS or CFS as if it were a local file.

- If the rendering materials are small, it is recommended to compress them into a gzip package and upload the package to COS. For more information, see [Uploading Objects](https://intl.cloud.tencent.com/document/product/436/6233).
- If the rendering materials are large, it is recommended to store them in CFS.

### III. Creating a Task Template
1. Log in to the [Batch Console](), click **Task template** in the left navigation bar, select the target region and click **Create**.

2. Configure basic information. Below is an example:
![](https://main.qcloudimg.com/raw/cf2f94cec702e0d42abe34b6e0d38bde.jpg)
  * Name: rendering
  * Description: 3ds Max 2018 Demo
  * Resource configuration: S1.LARGE8 (4-core 8 GB)
  * Number of resources: Number of concurrent renderings, e.g. 1
  * Timeout: Default value
  * Number of retries: Default value
  * Image: Custom image ID, e.g. img-i64lx84h

3. Configure application information. Below is an example:
![](https://main.qcloudimg.com/raw/ef7c95752cfb266f855ea0e69436d245.jpg)
  * Execution method: PACKAGE
  * Package address: COS as an example, `cos://barrygz-1251783334.cos.ap-guangzhou.myqcloud.com/render/max.tar.gz`
  * Stdout log: For formats, see [Entering COS or CFS Path](https://cloud.tencent.com/document/product/599/13996)
  * Stderr log: Same as Stdout Log
  * Command line: `3dsmaxcmd Demo.max -outputName:c:\\render\\image.jpg`

4. Configure the storage mapping.
![](https://main.qcloudimg.com/raw/f5e1836e79852eb5d4c49b917bb870f8.jpg)
  * Output path mapping - local path: `C:\\render\\`
  * Output path mapping - COS or CFS path: For formats, see [Entering COS or CFS Path](https://cloud.tencent.com/document/product/599/13996)

5. Preview the task's JSON file and click **Save** after confirming it is correct.

### IV. Submitting the Job
1. Click **Job** in the left navigation bar, select the target region and click **Create**.

2. Configure basic job information. Below is an example:
  ![](https://main.qcloudimg.com/raw/7f19ede7710ec960fc4586297213d1fc.jpg)
  * Job name: max
  * Priority: Default value
  * Description: 3ds Max 2018 Demo

3. Select the **rendering** task on the left on the task flow page and move the task onto the canvas on the right using the mouse.

4. Turn on **Task details** to the right of the task flow, confirm the configuration is correct and click **Finish**.
![](https://main.qcloudimg.com/raw/00df21802b524cd684f43b68155e3483.jpg)

5. Query the job state. For more information, see [Querying Information](https://cloud.tencent.com/document/product/599/14567).

6. Rendering process demonstration.
![](https://main.qcloudimg.com/raw/4a0743f3a49045f59c0580deda1529f9.png)

7. Query the rendering result. For more information, see [Viewing Object Information](https://cloud.tencent.com/document/product/436/13326).
![](https://main.qcloudimg.com/raw/7997d36d8d08e0733fb372dfc6513034.jpg)

## What Can I Do Next?
This document illustrates a simple single-instance rendering job to show the most basic capabilities of Batch. You can continue to test the advanced capabilities according to the Console User Guide.
- **Rich CVM configuration items**: Batch provides a wide variety of CVM configuration items, so you can customize the CVM configuration based on the specific business scenario.
- **Remote storage mapping**: Batch optimizes storage access and simplifies access to remote storage services into local file system operations.
- **Concurrent multi-image rendering**: Batch supports specifying of the number of concurrent rendering instances which are distinguished through [Environment Variables](https://intl.cloud.tencent.com/document/product/599/11752) with each instance reading a different material for concurrent rendering.
