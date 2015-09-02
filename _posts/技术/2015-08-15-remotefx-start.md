---
layout: post
title: "remotefx study"
description: ""
category: 技术
tags: [RemoteFX]
---

# My study log 1

from: https://technet.microsoft.com/en-us/library/ff817578(v=ws.10).aspx

### about

*   which version: `Windows Server 2008 R2 with SP1`
*   feature: introduces a set of end-user experience enhancements for Remote Desktop Protocol (RDP)


### What does RemoteFX do?

by providing:

*   a 3D virtual adapter
*   intelligent codecs
*   and the ability to redirect USB devices in virtual machines

RemoteFX is integrated with the RDP protocol, which enables shared:

*   encryption,
*   authentication,
*   management,
*   and device support.

### Who will be interested in this feature?

*   that are available on virtual desktops, These applications may include the following:

    -   Sliverlight and Flash application
    -   3D applications built on DirectX
    -   USB devices that are used on a virtual machine
    -   Microsoft Office applications
    -   Media player applications
    -   Applications that are hosted on th Internet
    -   Line-of-business applications

*   Server administrators who are responsible for managing Remote Desktop Session Host servers

*   Client computer administrators who are responsible for managing devices that are similar to the following:
    -   Thin client that are running an embedded operating system, such as Windows Embedded
    -   Legacy personal computers
    -   Clinet computers running Windows Vista and Windows 7

*   Desktop administrators who are looking at desktop virualization as a set of technologies that enable the migration of Windows 7

### Are there any special consideration? -- hardware

the following hardware requirements must be met:

*   A Hyper-V server that meets the hardware requirements is listed in the Windows Server Technical library. For more information about the hardware requirements, see [Hardware Considerations for RemoteFX](http://go.microsoft.com/fwlink/?LinkId=191918).
*   The client computer must be running Remote Desktop consideration 7.1.

### What functionality does RemoteFX provide?

The new functionality that is provided by RemoteFX is described in the following section.

*   Host side rendering

    **Host side rendering allows graphics to be rendered on the host device instead of on the client device**. This enables support for all graphics types by sending highly compressed bitmap image to endpoint device in an adaptive manner. This also allow the applications to run at full speed on the host computer by taking advantage of the GPU and the CPU, which proviedes an experience that is similar to a local computer.

*   GPU Virualization

    GPU Virualization is a technology that exposes a virtual graphics device to a virtual machine. RemoteFX exposes a WDDM driver with the virtual desktop, and **it allows multiple virtual desktops to share a single GPU on a Hyper-V server**.

    -   Why is this importants?

        Enterprise customers who have consolidated their desktops on to a Hyper-V server can take advantage of this technology. GPU Virualization in RemoteFX enables end users to run graphics applications on a virtual machine. It also enables administrators to share physical graphics devices across multiple knowledge workers with virtual machines running on a Hyper-V server.

*   Intelligent Screen Caption

    Interlligent Screen Caption is responsible for checking screen content changes between frames and transmitting the changed bits for encoding. **Interlligent Screen Caption tracks network speed and then dynamically adjusts according to the available bandwidth**.

    -   Why is this importants?

        Interlligent Screen Caption understands the network capability between the client and host devices with regards to rendering and compression(能屏幕捕捉通晓网络能力依赖于客户端与服务端之间设备的渲染和压缩). The virtual GPU renders the applications, and Interlligent Screen Caption understands which part of the screen has changed and then compression and transmits those changes. If network connection is degraded on the client device, Intelligent Screen Caption sends fewer frames across the Internet to avoid network congestion. Intelligent Screen Caption is designed to support fast networks, in which case it can send more frames to ensure a good user experience.

*   RemoteFX Encoder

    The RemoteFX Encoder allows encoding on the processor, on the GPU, or on dedicated hardware. After the screen data is compressed, it sends the data to the virtual desktop, which transfers the bitmaps by using Remote Desktop Connection(RDC) client computers.

    -   Why is this change important?

        This flexible encoding process porvides high fidelity and scalability. In computers where the processors are consistently busy, the dedicated hardware ensures that the user experience is not affected.

*   RemoteFX Decoder

    The RemoteFX Decoder decodes bitmaps tha have transfered from the virtual desktop to the client computer. RemoteFX Decoder the bitmaps on client computer by using software in the GPU or processor, or by using a hardware decoder.

    -   Why is this change important?

        The RemoteFX Decoder enables low cost, easily manageable client devices. The flexibility to use the processor, GPU, or a hardware decoder helps provide a RemoteFX experience to a wide variety of client devices ranging from low complexity devices to rich clients.

*   RemoteFX for Remote Desktop Session Host

    RemoteFX enables access to the RD Session Host server from rich clients, thin clients, and ultrathin clients. It also ensures lower bandwidth usage as compared to Windows Server 2008 R2 when transferring rich graphics applications.

    For more information about RemoteFX for Remote Desktop Session Host, see the [Using RemoteFX with Remote Desktop Session Host Step-by-Step Guide](http://go.microsoft.com/fwlink/?LinkId=192435) on the Windows Server 2008 R2 Technical Libary.

    **Note: A GPU is not required when using RemoteFX for Remote Desktop Session Host.**

*   RemoteFX USB Redirection

    RemoteFX USB Redirection allows many devices to be redirected to an RD Virualization Host server at the USB level. Advantage of this solution include that no device drivers are required on the client computer, and a universal interface is provided that works with any USB device on any platform where RemoteFX USB Redirection is supported. This solution redirects many types of devices, including audio devices, storage devices, human interface devices, all-in-one printers, and scanners.

    For more information about RemoteFX USB Redirection, see [Configuring USB Device Rediection with RemoteFX Step-by-Step Guide](http://go.microsoft.com/fwlink/?LinkId=192431) on the Windows Server 2008 R2 Technical Libary.

### What settings have been added or changed?

*   Services

    The following services are added when RemoteFX is enabled:

    -   **RemoteFX Session Manager**: Provides startup services for RemoteFX
    -   **RemoteFX Session Licensing**: Responsible for license validation and issuance for RemoteFX sessions

*   Windows Firewall settings

    A new Windows Firewall rule is added for RemoteFX. If you perform a new installation and enable Remote Desktop by using the **System** properties sheet, the rule is enabled automatically.

    You must enabled the RemoteFX Windows Firewall rule manually if you do either of the following:

    -   Enabled Remote Desktop by using the **netsh** command or the Windows Firewall APIs.
    -   Upgrade to Windows 7 with SP1 on a virtual desktop that already had Remote Desktop enabled.

    **To enable the RemoteFX rule by using Windows Firewall with Advanced Security**

    1. Click **Start**, point to **Administrative Tools**, and then click **Windows Firewall with Advanced Security**.
    2. Click **Inbound Rules**.
    3. Right-click **Remote Desktop - RemoteFX (TCP-In)**, and then click **Enable Rule**

    **To enable the RemoteFX rule by using netsh**

    1. Click **Start**, click All Programs, click **Accessories**, right-click **Command Prompt**, and then click **Run as administrator**.
    2. If the **User Account Control** dialog box appears, confirm that the action it displays is what you want, and then click **Yes**.
    3. Type **netsh advfirewall firewall set rule group=”Remote Desktop – RemoteFX” new enable=yes**, and then press ENTER.

*   Group Policy settings

    The following Group Policy settings allow you to configure RemoteFX within your environment:

    **Note:** To view detailed explanations about the Group Policy settings that are new with RemoteFX, open the Local Group Policy Editor and examine the provided description.

    | Group Policy setting name | Location | Description | Default value |
    | ------------- | ------------- | ------------- | ------------- |
    | Configure RemoteFX | Computer Configuration\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host \Remote Session Environment | Enable and disable RemoteFX. | Not configured |
    | Optimize visual experience when using RemoteFX | Computer Configuration\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host \Remote Session Environment | Specify the visual experience that users will have when connecting to RemoteFX-enabled sessions. | Not configured |
    | Allow RDP redirection of other supported RemoteFX USB devices from this computer| Computer Configuration\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Connection Client\RemoteFX USB Redirection | Permit redirection of supported RemoteFX USB devices. | Not configured |
    | Do not allow supported Plug and Play device redirection | Computer Configuration\Administrative Templates\Windows Components\Remote Desktop Services\Remote Desktop Session Host \Device and Resource Redirection | Disable Plug and Play device redirection and RemoteFX USB redirection. | Not configured |


*   Performance counters

    The following performance counters are added **on the RemoteFX server** when RemoteFX is enabled:

    -   RemoteFX Root GPU Management
        +   **Resources: TDRs in Server GPUs**: Total number of times that the TDR times out in the GPU on the server.
        +   **Resources: VMs running RemoteFX:** Total number of virtual machines that have the RemoteFX 3D Video Adapter installed.
        +   **VRAM: Available MB per GPU:** Amount of dedicated video memory that is not being used.
        +   **VRAM: Reserved % per GPU:** Percent of dedicated video memory that has been reserved for RemoteFX.
    -   RemoteFX Software
        +   **Capture Rate for monitor [1-4]:** Displays the RemoteFX capture rate for monitors 1-4.
        +   **Compression Ratio:** Displays the RemoteFX compression ratio.
        +   **Delayed Frames/sec:** Number of frames per second where graphics data was not sent within a certain amount of time.
        +   **GPU response time from Capture:** Latency measured within RemoteFX Capture (in microseconds) for GPU operations to complete.
        +   **GPU response time from Render:** Latency measured within RemoteFX Render (in microseconds) for GPU operations to complete.
        +   **Output Bytes:** Total number of RemoteFX output bytes.
        +   **Waiting for client count/sec:** Total number of times per second where graphics data is ready, but RemoteFX Capture is waiting for the client device to consume the previous data.
    -   RemoteFX vGPU Management
        +   **Resources: TDRs local to VMs**   Total number of TDRs that have occurred in this virtual machine. TDRs that the server propagated to the virtual machine are not included.
        +   **Resources: TDRs propagated by Server**   Total number of TDRs that occurred on the server and that have been propagated to the virtual machine.

    The following performance counters are added **on the virtual desktop** when RemoteFX is enabled:

    -   RemoteFX VM vGPU Performance
        +   **Data: Invoked presents/sec**   Total number (in seconds) of present operations to be rendered to the desktop of the virtual machine per second.
        +   **Data: Outgoing presents/sec**   Total number of present operations sent by the virtual machine to the server GPU per second.
        +   **Data: Read bytes/sec**   Total number of read bytes from the RemoteFX server per second.
        +   **Data: Send bytes/sec**   Total number of bytes sent to the RemoteFX server GPU per second.
        +   **DMA: Communication buffers average latency (sec)**   Average amount of time (in seconds) spent in the communication buffers.
        +   **DMA: DMA buffer latency (sec)**   Amount of time (in seconds) from when the DMA is submitted until completed.
        +   **DMA: Queue length**   DMA Queue length for a RemoteFX 3D Video Adapter.

### Which editions include RemoteFX?

RemoteFX is available in the following editions of Windows Server 2008 R2 with SP1:
Windows Server 2008 R2 Standard with SP1

*   Windows Server 2008 R2 Enterprise with SP1

*   Windows Server 2008 R2 Datacenter with SP1

*   Microsoft Hyper-V Server 2008 R2 with the Windows Server 2008 R2 SP1 update applied

RemoteFX is not available in the following editions of Windows Server 2008 R2 with SP1:

*   Windows Web Server 2008 R2 with SP1

*   Windows Server 2008 R2 for Itanium-Based Systems with SP1

To use RemoteFX on a virtual desktop, you must be running one of the following editions:

*   Windows 7 Enterprise with SP1

*   Windows 7 Ultimate with SP1

**Note**: The client computer that is used to connect to a RemoteFX-enabled session can be any operating system that is running Remote Desktop Connection 7.1.


### Additional references

For information about other new features in Remote Desktop Services, see [What's New in Remote Desktop Services](https://technet.microsoft.com/en-us/library/dd560658(v=ws.10).aspx).


other: https://github.com/FreeRDP/FreeRDP/tree/master/docs
