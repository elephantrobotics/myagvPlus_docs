# ROS2 Introduction

- What is ROS2?

ROS2 ： [https://docs.ros.org/ ](https://docs.ros.org/)

ROS2 Tutorials：[https://docs.ros.org/en/rolling/Tutorials.html](https://docs.ros.org/en/rolling/Tutorials.html)

ROS2 humble  Installation：[https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html ](https://docs.ros.org/en/humble/Installation/Ubuntu-Install-Debs.html)

ROS 2 (Robot Operating System 2) is the second-generation open-source software development framework for robots, led by Open Robotics. It was initiated in 2015, officially released after 2018, and continues to iterate. Its goal is to meet the full range of needs from research prototypes to industrial-grade products. ROS 2 is not an operating system in the traditional sense but a **distributed middleware and toolchain** that runs on Linux, Windows, macOS, and embedded RTOS/MCU, providing core capabilities such as hardware abstraction, communication mechanisms, device drivers, functional algorithms, package management, and development tools.

ROS 2 inherits the core concept of ROS 1: "modularity, node-based design, and code reuse," but the **underlying architecture was completely rewritten**. The biggest change is abandoning the centralized Master in ROS 1 and adopting the industrial-standard **DDS (Data Distribution Service)** as the communication middleware. This achieves decentralization, automatic node discovery, and real-time reliable data distribution, completely addressing the issues in ROS 1 such as single points of failure, poor real-time performance, and weak cross-platform support.

**Skip to sections:**

- [1.Installation](6.2.1-ROS2_Installation.md)
- [2.ROS2 basic](6.2.2-Using_Common_ROS2_Tools.md)
- [3.Basic Control](6.2.3-Basic_Control_Based_on_ROS2.md)
- [4.Gmapping Real-time Mapping](6.2.4-Real-time_Mapping_with_Gmapping.md)
- [5.Map Navigation](6.2.5-Navigation-Map_Navigation.md)
- [6.Rtabmap mapping and navigation](6.2.6-Rtabmap.md)

---

[← Previous Section](../6.1-ApplicationBasePython/README.md) | [Next Page →](../6.2-ApplicationBaseROS2/6.2.2-Using_Common_ROS2_Tools.md)

